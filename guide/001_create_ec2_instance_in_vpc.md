***TODO: 文章の推敲***
# VPCにEC2インスタンスを作成する

### VPC
JSONでVPCを作る。CIDR Blockには、RFC1918で規定されているグローバルIPとして使えないIPアドレス範囲えらぶ。  
[理由要調査]VPC内部だけで通用するプライベートIPとして、グローバルIPとして使えないIPアドレス群がふさわしいから？  

名称タグは別I/F経由で設定する必要あり；出力結果JSONのVpcIdをメモする。

ちなみに、VPC上限は5なので、それ以上作ろうとするとエラーが返る。

```
aws ec2 create-vpc --cli-input-json '{"DryRun":false,"CidrBlock":"172.16.0.0/16","InstanceTenancy":"default"}'
```

メモしておいたVpcIdを対象リソースとして、Nameタグに名称を設定する。リソースごとのタグ上限は10ということなので注意。

```
aws ec2 create-tags --cli-input-json '{"DryRun":false,"Resources":["<VpcId>"],"Tags":[{"Key":"Name","Value":"some name"}]}'
```

### メモ
- CIDRブロックは後から変更できない。変更したかったら希望のCIDRブロックを持ったVPCを新規作成し、既存のVPCのインスタンスを全て新規のVPCに移動させるフローをとる。
- VPCの作成と同時にRoute Tableも作成され、VPCに割り当てられる。
- VPCの作成と同時にNetwork Access Control Listも作成され、VPCに割り当てられる。

### SecurityGroup
JSONでSecurityGroupを作る。VPCのIDが必要なので控えておく。
名称タグは別I/F経由で設定する必要あり；出力結果JSONのGroupIdをメモする。

```
aws ec2 create-security-group --cli-input-json '{"DryRun":false,"GroupName":"some security grp","Description":"dscr comes here.","VpcId":"<VpcId>"}'
```

メモしておいたGroupIdを対象リソースとして、Nameタグに名称を設定する。リソースごとのタグ上限は10ということなので注意。

```
aws ec2 create-tags --cli-input-json '{"DryRun":false,"Resources":["<GroupId>"],"Tags":[{"Key":"Name","Value":"some name"}]}'
```

#### Inbound/Outbound
JSONでSecurityGroupのInbound/Outboundを作る。可能なフローとして、新規に作るものと、同一VPC以下の既存のSecurityGroup群をベースに作るものがある。当面、新規に作るフローを用いる。

全ポートを指定する場合は、FromPortとToPortを省略する。単一ポートを指定したい場合はFromPortとToPortに同じ値を設定する。

***FIXME: 2016/08/19: UserIdGroupPairsとPrefixListIdsの用途が不明なので空にしておく。***

```
: # SSH Gateway向け設定の追加
aws ec2 authorize-security-group-ingress --cli-input-json '{"DryRun":false,"GroupId":"<GroupId>","IpPermissions":[{"IpProtocol":"tcp","FromPort":22,"ToPort":22,"UserIdGroupPairs":[],"IpRanges":[{"CidrIp":"0.0.0.0/0"}],"PrefixListIds":[]}]}'
```

設定を削除する場合、以下のようにコマンドを実行する。

```
: # SSH Gateway向け設定の削除
aws ec2 revoke-security-group-ingress --cli-input-json '{"DryRun":false,"GroupId":"<GroupId>","IpPermissions":[{"IpProtocol":"tcp","FromPort":22,"ToPort":22,"UserIdGroupPairs":[],"IpRanges":[{"CidrIp":"0.0.0.0/0"}],"PrefixListIds":[]}]}'
```

### Subnet
JSONでSubnetを作る。VPCのIDが必要なので控えておく。

CIDRブロックはVPCのCIDRブロックのサブネットである必要がある（VPCのCIDRブロックと同一でもOK）。

名称タグは別I/F経由で設定する必要あり；出力結果JSONのSubnetIdをメモする。

```
aws ec2 create-subnet --cli-input-json '{"DryRun":false,"VpcId":"<VpcId>","CidrBlock":"172.16.1.0/24","AvailabilityZone":"<AvailabilityZone>"}'
```

AvailabilityZoneは以下のコマンドで候補を確認でき、結果JSONのZoneNameフィールドの値を用いればよい。

```
aws ec2 describe-availability-zones
```

メモしておいたSubnetIdを対象リソースとして、Nameタグに名称を設定する。リソースごとのタグ上限は10ということなので注意。

```
aws ec2 create-tags --cli-input-json '{"DryRun":false,"Resources":["<SubnetId>"],"Tags":[{"Key":"Name","Value":"some name"}]}'
```

最後に、Subnet以下のEC2インスタンスに公開IPアドレスが割り当てられるように、Subnetの該当設定の変更を行う。

```
aws ec2 modify-subnet-attribute --client-input '{"SubnetId":"<SubnetId>","MapPublicIpOnLaunch":{"Value":true}}'
```

### Internet Gateway
JSONでInternet Gatewayを作る。VPCのIDが必要なので控えておく。

名称タグは別I/F経由で設定する必要あり；出力結果JSONのInternetGatewayIdをメモする。

```
aws ec2 create-internet-gateway --cli-input-json '{"DryRun":false}'
```

メモしておいたInternetGatewayIdを対象リソースとして、Nameタグに名称を設定する。リソースごとのタグ上限は10ということなので注意。

```
aws ec2 create-tags --cli-input-json '{"DryRun":false,"Resources":["<InternetGatewayId>"],"Tags":[{"Key":"Name","Value":"some name"}]}'
```

Internet GatewayをVPCにアタッチするので、メモしておいたInternetGatewayIdと控えておいたVPCのIDを用いて以下のコマンドを実行する。

```
aws ec2 attach-internet-gateway --cli-input-json '{"DryRun":false,"InternetGatewayId":"<InternetGatewayId>","VpcId":"<VpcId>"}'
```

### Route Table
VPC作成時に自動作成されたメインRoute Tableを参照する。以下のコマンドの結果JSONのRouteTableIdをメモする。

```
aws ec2 describe-route-tables --filter 'Name=association.main,Values=true' --filter "Name=vpc-id,Values=<VpcId>"
```

JSONでRoute Tableにルーティングルールを追加する。InternetGatewayIdが必要なので控えておく。
今回の場合、IGWに対するルーティングルール。

```
: # SSH Gateway向け設定の追加
aws ec2 create-route --cli-input-json '{"DryRun":false,"RouteTableId":"<RouteTableId>","DestinationCidrBlock":"0.0.0.0/0","GatewayId":"<InternetGatewayId>"}'
```

JSONでRoute TableにSubnetを紐づける。SubnetIdが必要なので控えておく。
```
aws ec2 associate-route-table --cli-input-json '{"DryRun":false,"SubnetId":"<SubnetId>","RouteTableId":"<RouteTableId>"}'
```

### Instance
***TODO: 途中***
```
: # 単一インスタンス、
'{"DryRun":false,"ImageId":"","KeyName":"","SecurityGroups":[""],"SecurityGroupIds":[""],"UserData":"","InstanceType":"","Placement":{"AvailabilityZone":"","GroupName":"","Tenancy":"","HostId":"","Affinity":""},"KernelId":"","RamdiskId":"","BlockDeviceMappings":[{"VirtualName":"","DeviceName":"","Ebs":{"SnapshotId":"","VolumeSize":0,"DeleteOnTermination":true,"VolumeType":"","Iops":0,"Encrypted":true},"NoDevice":""}],"Monitoring":{"Enabled":true},"SubnetId":"","DisableApiTermination":true,"InstanceInitiatedShutdownBehavior":"","PrivateIpAddress":"","ClientToken":"","AdditionalInfo":"","NetworkInterfaces":[{"NetworkInterfaceId":"","DeviceIndex":0,"SubnetId":"","Description":"","PrivateIpAddress":"","Groups":[""],"DeleteOnTermination":true,"PrivateIpAddresses":[{"PrivateIpAddress":"","Primary":true}],"SecondaryPrivateIpAddressCount":0,"AssociatePublicIpAddress":true}],"IamInstanceProfile":{"Arn":"","Name":""},"EbsOptimized":true}'
```
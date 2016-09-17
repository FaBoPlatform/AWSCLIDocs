# VPCにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[002 VPCの作成](/vpc/002_create_vpc.md)で環境変数に設定|
|VPC_TAG| vpc of fabo|

## VPCにタグをつける

OS X

```bash
$ export VPC_TAG="vpc of fabo"
$ aws ec2 create-tags --resources ${VPC_ID} --tags "Key=Name,Value=${VPC_TAG}"
```

Windows

```bash
$ set VPC_TAG=vpc of fabo
$ aws ec2 create-tags --resources %VPC_ID% --tags "Key=Name,Value=%VPC_TAG%"
```

## vpc-idで絞って情報を表示し反映されているか確認する

OS X

```bash
$ aws ec2 describe-vpcs --vpc-ids "${VPC_ID}"
```

Windows

```bash
$ aws ec2 describe-vpcs --vpc-ids "%{VPC_ID}%"
```

JSONにTagsの項目が出現する。

```json
{
    "Vpcs": [
        {
            "VpcId": "vpc-#######", 
            "InstanceTenancy": "default", 
            "Tags": [
                {
                    "Value": "vpc of fabo", 
                    "Key": "Name"
                }
            ], 
            "State": "available", 
            "DhcpOptionsId": "dopt-0f3f206d", 
            "CidrBlock": "172.16.0.0/16", 
            "IsDefault": false
        }
    ]
}
```

## 確認

![](/img/vpc/tag001.png)

![](/img/vpc/tag002.png)

![](/img/vpc/tag003.png)


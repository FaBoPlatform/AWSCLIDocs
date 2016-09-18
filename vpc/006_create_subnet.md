# 006 Subnetの作成

## つくるもの

![](/img/vpc/vpc006.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[002 VPCの作成](/vpc/002_create_vpc.md)で環境変数に設定|
|AVAILABILITY_ZONE|[005 Availablity Zoneを調べる](/vpc/005_describe_availability_zone.md)で環境変数に設定|
|SUBNET_CIDR_BLOCK|172.16.1.0/24|
|SUBNET_ID|本項で設定|

## Subnetのネットマスク

/24の意味は、[RFC 4632](https://tools.ietf.org/html/rfc4632) で詳細を確認。/24は、サブネットが`255.255.255.0`となりIP数が`256`個。今回は、256個のIP数のサブネットを作成する。Amazonが予約しているIP数は5つなので、/24では、251個のIPが利用可能な設定になる。

* n.n.n.x/26              64       67108864
* n.n.n.x/25             128       33554432
* n.n.n.0/24             256       16777216    legacy "Class C"
* n.n.x.0/23             512        8388608
* n.n.x.0/22            1024        4194304

## Subnetの作成

OS X

```bash
$ export SUBNET_CIDR_BLOCK="172.16.1.0/24"
$ aws ec2 create-subnet --vpc-id ${VPC_ID} --cidr-block ${SUBNET_CIDR_BLOCK} --availability-zone ${AVAILABILITY_ZONE}
```

Windows


```bash
$ set SUBNET_CIDR_BLOCK=172.16.1.0/24
$ aws ec2 create-subnet --vpc-id %VPC_ID% --cidr-block %SUBNET_CIDR_BLOCK% --availability-zone %AVAILABILITY_ZONE%
```

処理結果のJSON

```json
{
    "Subnet": {
        "VpcId": "vpc-########", 
        "CidrBlock": "172.16.1.0/24", 
        "State": "pending", 
        "AvailabilityZone": "ap-northeast-1a", 
        "SubnetId": "subnet-########", 
        "AvailableIpAddressCount": 251
    }
}
```

SubnetIdを環境変数に定義する。

OS X

```bash
$ export SUBNET_ID="subnet-########"
```

Windows

```bash
$ set SUBNET_ID=subnet-########
```

## Subnetの予約アドレス

|IP|意味|
|:--|:--|
|172.16.1.0|ネットワークアドレス|
|172.16.1.1|VPC ルーター用に AWSが予約|
|172.16.1.2|Amazon が提供する DNS へのマッピング用に AWS が予約|
|172.16.1.3|AWSが予約(未使用)|
|172.16.1.255|ネットワークブロードキャストアドレス(未使用)|

## Subnetのルール

* アベイラビリティーゾーンごとに 1 つ以上のサブネットを追加可能
* 1つのサブネットが複数のゾーンにまたがることはできない
* 各サブネットに固有の ID が割り当てられる
* インターネットゲートウェイにルーティングされる場合、そのサブネットは`パブリックサブネット`と呼ぶ
* インターネットゲートウェイにルーティングされていない場合、`プライベートサブネット`と呼ぶ
* インターネットゲートウェイにルーティングされていない仮想プライベートゲートウェイにルーティングされているサブネットは、`VPN のみのサブネット`と呼ぶ
* VPCに配置できるSubnetの数の上限は250。



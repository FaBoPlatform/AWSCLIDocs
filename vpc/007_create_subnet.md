# Subnetの作成

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](001_create_vpc.md)で環境変数に設定|
|AVAILABILITY_ZONE|[006 Availabirity Zonenの一覧](vpc/006_describe_availability_zone.md)で環境変数に設定|
|SUBNET_CIDR_BLOCK|172.16.1.0/24|
|SUBNET_ID|本項で設定|

## Subnetの作成

```bash
$ export SUBNET_CIDR_BLOCK="172.16.1.0/24"
$ export AVAILABILITY_ZONE="ap-northeast-1c"
$ aws ec2 create-subnet --vpc-id ${VPC_ID} --cidr-block ${SUBNET_CIDR_BLOCK} --availability-zone ${AVAILABILITY_ZONE}
```

処理結果のJSON

```json
{
    "Subnet": {
        "VpcId": "vpc-########", 
        "CidrBlock": "172.16.1.0/24", 
        "State": "pending", 
        "AvailabilityZone": "ap-northeast-1c", 
        "SubnetId": "subnet-########", 
        "AvailableIpAddressCount": 251
    }
}
```

SubnetIdを環境変数に定義する。

```bash
$ export SUBNET_ID="subnet-########"
```

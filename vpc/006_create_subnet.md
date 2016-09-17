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
        "AvailabilityZone": "ap-northeast-1c", 
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
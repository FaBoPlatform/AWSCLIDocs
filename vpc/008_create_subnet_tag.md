# SubnetにTagをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SUBNET_ID|[007 Subnetの作成](vpc/007_create_subnet.md)|
|SUBNET_TAG|fabo subnet|

## SubnetにTagをつける

```bash
$ export SUBNET_TAG="fabo subnet"
$ aws ec2 create-tags --resources ${SUBNET_ID} --tags "Key=Name,Value=${SUBNET_TAG}"
```

確認

```bash
aws ec2 describe-subnets --subnet-id=${SUBNET_ID}
```

タグの項目が追加される。

```json
{
    "Subnets": [
        {
            "VpcId": "vpc-########", 
            "Tags": [
                {
                    "Value": "fabo subnet", 
                    "Key": "Name"
                }
            ], 
            "CidrBlock": "172.16.1.0/24", 
            "MapPublicIpOnLaunch": false, 
            "DefaultForAz": false, 
            "State": "available", 
            "AvailabilityZone": "ap-northeast-1c", 
            "SubnetId": "########", 
            "AvailableIpAddressCount": 251
        }
    ]
}
```
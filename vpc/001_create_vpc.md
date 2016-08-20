# VPCの作成

|環境変数|値|
|:--|:--|
|CIDR_BLOCK|172.16.0.0/16|
|VPC_ID|本項で環境変数に設定|

## VPCの作成

```bash
$ export CIDR_BLOCK="172.16.0.0/16"
$ aws ec2 create-vpc --cidr-block ${CIDR_BLOCK} 
```

返り値は、JSONでくるが、VpcIdだけの取得ができないので手動で環境変数に設定する。

```json
{
    "Vpc": {
        "VpcId": "vpc-########", 
        "InstanceTenancy": "default", 
        "State": "pending", 
        "DhcpOptionsId": "dopt-0f3f206d", 
        "CidrBlock": "172.16.0.0/16", 
        "IsDefault": false
    }
}
```

```bash
export VPC_ID="vpc-########"
```

## 確認

``bash
excho ${VPC_ID}
```

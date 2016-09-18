# 011 Route Tableの編集

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[002 VPCの作成](/vpc/002_create_vpc.md)で環境変数に設定|
|ROUTE_TABLE_ID|本項で設定|

## Route Table IDの取得

VPC作成時に自動的にRoute Tableが作成されている。今回は、そのRoute Tableを編集する。

`OS X`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=${VPC_ID}"
```

`Windows`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=%VPC_ID%"
```

結果

```json
{
    "RouteTables": [
        {
            "Associations": [
                {
                    "RouteTableAssociationId": "rtbassoc-########", 
                    "Main": true, 
                    "RouteTableId": "rtb-########"
                }
            ], 
            "RouteTableId": "rtb-########", 
            "VpcId": "vpc-########", 
            "PropagatingVgws": [], 
            "Tags": [], 
            "Routes": [
                {
                    "GatewayId": "local", 
                    "DestinationCidrBlock": "172.16.0.0/16", 
                    "State": "active", 
                    "Origin": "CreateRouteTable"
                }
            ]
        }
    ]
}
```

Rounte Table Idを環境変数に設定.

`OS X`

```bash
$ export ROUTE_TABLE_ID="rtb-########"
```

`Windows`

```bash
$ set ROUTE_TABLE_ID=rtb-########
```
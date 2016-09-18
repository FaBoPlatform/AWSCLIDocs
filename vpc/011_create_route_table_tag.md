# 011 Route Tableにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|ROUTE_TABLE_ID|本項で設定|
|ROUTE_TABLE_TAG|fabo route table|

## Route Tableにタグをつける

`OS X`

```bash
$ export ROUTE_TABLE_TAG="fabo route table"
$ aws ec2 create-tags --resources ${ROUTE_TABLE_ID} --tags "Key=Name,Value=${ROUTE_TABLE_TAG}"
```

`Windows`

```bash
$ set ROUTE_TABLE_TAG=fabo route table
$ aws ec2 create-tags --resources %ROUTE_TABLE_ID% --tags "Key=Name,Value=%ROUTE_TABLE_TAG%"
```

確認

`OS X`

```bash
$ aws ec2 describe-route-tables --filter "Name=route-table-id,Values=${ROUTE_TABLE_ID}"
```
`Windows`

```bash
$ aws ec2 describe-route-tables --filter "Name=route-table-id,Values=%ROUTE_TABLE_ID%"
```

結果。Tagsの項目が追加される。

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
            "Tags": [
                {
                    "Value": "fabo route table", 
                    "Key": "Name"
                }
            ], 
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



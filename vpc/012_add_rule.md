# Route Tableにルーティングルールを追加

## 本項で使用する環境変数

|環境変数|値|意味|
|:--|:--|:--|
|ROUTE_TABLE_ID|[009 RouteTableの編集](/vpc/009_modify_route_table.md)で環境変数に設定||
|GATEWAY_ID|[004 Internet Gatewayの作成](/vpc/004_create_gateway.md)で環境変数に設定||
|DESTINATION_CIDR_BLOCK|0.0.0.0/0|すべてのトラフィック|

## Route Tableにルーティングルーツを追加

```bash
$ aws ec2 create-route --route-table-id ${ROUTE_TABLE_ID} --destination-cidr-block DESTINATION_CIDR_BLOCK --gateway-id ${GATEWAY_ID}
```

結果

```json
{
    "Return": true
}
```

## 確認

```bash
$ aws ec2 describe-route-tables --filter "Name=route-table-id,Values=${ROUTE_TABLE_ID}"
```

Routesに

```json
                {
                    "GatewayId": "igw-########", 
                    "DestinationCidrBlock": "0.0.0.0/0", 
                    "State": "active", 
                    "Origin": "CreateRoute"
                }
```

のオブジェクトが追加される。


結果

```json
{
    "RouteTables": [
        {
            "Associations": [
                {
                    "RouteTableAssociationId": "rtbassoc-82620be6", 
                    "Main": true, 
                    "RouteTableId": "rtb-4d5a8e29"
                }
            ], 
            "RouteTableId": "rtb-4d5a8e29", 
            "VpcId": "vpc-48362d2d", 
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
                }, 
                {
                    "GatewayId": "igw-########", 
                    "DestinationCidrBlock": "0.0.0.0/0", 
                    "State": "active", 
                    "Origin": "CreateRoute"
                }
            ]
        }
    ]
}
```



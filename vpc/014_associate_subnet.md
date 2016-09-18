# 014 Route TableをSubnetに関連づける

## つくるもの

![](/img/vpc/vpc014.png)

## 本項で使用する環境変数

|環境変数|値|意味|
|:--|:--|:--|
|ROUTE_TABLE_ID|[009 RouteTableの編集](/vpc/009_modify_route_table.md)で環境変数に設定||
|SUBNET_ID|[007 Subnetの作成](/vpc/007_create_subnet.md)で環境変数に設定|

## Route TableにSubnetを関連づける

```bash
aws ec2 associate-route-table --subnet-id ${SUBNET_ID} --route-table-id ${ROUTE_TABLE_ID}
```

結果

```json
{
    "AssociationId": "rtbassoc-########"
}
```

## 確認

```bash
$ aws ec2 describe-route-tables --filter "Name=route-table-id,Values=${ROUTE_TABLE_ID}"
```

Routesに

```json
                 {
                    "SubnetId": "subnet-########", 
                    "RouteTableAssociationId": "rtbassoc-########", 
                    "Main": false, 
                    "RouteTableId": "rtb-########"
                }, 
```

のオブジェクトが追加される。


結果

```json
{
    "RouteTables": [
        {
            "Associations": [
                {
                    "SubnetId": "subnet-########", 
                    "RouteTableAssociationId": "rtbassoc-########", 
                    "Main": false, 
                    "RouteTableId": "rtb-########"
                }, 
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



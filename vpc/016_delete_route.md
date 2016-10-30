# 016 Route Tableからルーティングルールの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|DESTINATION_CIDR_BLOCK|[013 Route Tableにルーティングルールを追加](/vpc/013_add_rule.md)で環境変数に設定|
|ROUTE_TABLE_ID|[011 RouteTableのIDの取得](/vpc/011_modify_route_table.md)で環境変数に設定|

## ルーティングルールの削除

`OS X`

```bash
$ aws ec2 delete-route --route-table-id ${ROUTE_TABLE_ID} --destination-cidr-block ${DESTINATION_CIDR_BLOCK}
```

`Windows`

```bash
$ aws ec2 delete-route --route-table-id %ROUTE_TABLE_ID% --destination-cidr-block %DESTINATION_CIDR_BLOCK%
```

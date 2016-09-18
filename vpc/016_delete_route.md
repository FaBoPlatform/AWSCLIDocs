# 016 Route Tableからルーティングルールの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SUBNET_UD|[013 Route Tableにルーティングルールを追加](vpc/013_add_rule.md)で環境変数に設定|

## ルーティングルールの削除

`OS X`

```bash
$ aws ec2 delete-route --route-table-id ${ROUTE_TABLE_ID} --destination-cidr-block ${DESTINATION_CIDR_BLOCK}
```

`Windows`

```bash
$ aws ec2 delete-route --route-table-id %ROUTE_TABLE_ID% --destination-cidr-block %DESTINATION_CIDR_BLOCK%
```

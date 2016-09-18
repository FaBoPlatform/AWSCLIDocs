# インスタンスの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SEC_GROUP_ID|[001 Security Groupの作成](/ec2/001_create_security.md)で環境変数に設定|

## インスタンスの削除

```bash
$ aws ec2 delete-security-groups --group-ids ${SEC_GROUP_ID}
```

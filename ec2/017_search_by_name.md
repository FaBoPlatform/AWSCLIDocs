# 017 Secuirty Groupの名前での検索

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SEC_GROUP_NAME|[002 Security Groupの作成](/ec2/002_create_security.md)で環境変数に設定|

## Security Groupの削除の削除

`OS X`

```bash
$ aws ec2 describe-security-groups --filters Name=group-name,Values={$SEC_GROUP_NAME}
```

`Windows`

```bash
$ aws ec2 describe-security-groups --filters Name=group-name,Values=%SEC_GROUP_NAME%
```


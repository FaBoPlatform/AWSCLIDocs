# Key Pairの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|KEY_NAME|[004 Key pairの作成](/ec2/004_key_pair.md)で環境変数に設定|

## Key Pairの削除

```bash
$ aws ec2 delete-key-pair --key-name ${KEY_NAME}
```

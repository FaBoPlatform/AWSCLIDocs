# 作成したインスタンスにSSHでログイン

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|KEY_NAME|[004 Key pairの作成](/ec2/004_key_pair.md)で環境変数に設定|
|IP|[007 インスタンスのIPアドレスを取得](/ec2/007_get_instance_ip.md)|

## SSHでログイン

defaultでは、ec2-userで、ログインできる。

```bash
$ ssh -i ~/.ssh/${KEY_NAME}.pem ec2-user@${IP}
```

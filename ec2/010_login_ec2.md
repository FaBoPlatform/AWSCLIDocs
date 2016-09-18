# 010 作成したインスタンスにSSHでログイン

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|KEY_NAME|[004 Key pairの作成](/ec2/004_key_pair.md)で環境変数に設定|
|IP|[009 インスタンスのIPアドレスを取得](/ec2/009_get_instance_ip.md)|

## Windowsユーザ

SSHクライアントを事前にインストールしておいてください。

下記クライアントがSSHに対応しています。

|アプリ名|URL
|:--|:--|
|PUTTY|http://www.chiark.greenend.org.uk/~sgtatham/putty/|
|Tera Term|https://osdn.jp/projects/ttssh2/|


## SSHでログイン

defaultでは、ec2-userで、ログインできる。

```bash
$ ssh -i ~/.ssh/${KEY_NAME}.pem ec2-user@${IP}
```

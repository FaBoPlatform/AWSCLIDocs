# 006 Key Pairを生成する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|KEY_NAME|fabo_key|

## Key Pairを生成する

`OS X`

```bash
$ export KEY_NAME="fabo_key"
$ sudo aws ec2 create-key-pair --key-name ${KEY_NAME} | jq -r ".KeyMaterial" > ~/.ssh/${KEY_NAME}.pem
$ sudo chmod 400 ~/.ssh/${KEY_NAME}.pem
```
`~/.ssh/にfabo_key.pem` が作成される。EC2のログイン時に使うために、以後保管には気をつける。


`Windows`

```bash
$ set KEY_NAME=fabo_key
$ aws ec2 create-key-pair --key-name %KEY_NAME%
```

取得した文字列を、`~/.ssh/にfabo_key.pem` に保存。
Windowsは動作未確認.



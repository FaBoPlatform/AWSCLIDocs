# 017 Inaternet Gatewayの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|GATEWAY_ID|[008 Internet Gatewayの作成](vpc/008_create_gateway.md)で環境変数に設定|

## VPCの削除

`OS X`

```bash
$ aws ec2 delete-internet-gateway --internet-gateway-id=${GATEWAY_ID}
```

`Windows`

```bash
$ aws ec2 delete-internet-gateway --internet-gateway-id=%GATEWAY_ID%
```
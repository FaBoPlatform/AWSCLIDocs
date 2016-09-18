# 017 Inaternet Gatewayの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](/vpc/001_create_vpc.md)で環境変数に設定|
|GATEWAY_ID|[008 Internet Gatewayの作成](vpc/008_create_gateway.md)で環境変数に設定|

## VPCからのDetach

`OS X`

```bash
$ aws ec2 detach-internet-gateway --internet-gateway-id ${GATEWAY_ID} --vpc-id ${VPC_ID}
```

`Windows`

```bash
$ aws ec2 detach-internet-gateway --internet-gateway-id %GATEWAY_ID% --vpc-id %VPC_ID%
```

## Internet Gatewayの削除

`OS X`

```bash
$ aws ec2 delete-internet-gateway --internet-gateway-id=${GATEWAY_ID}
```

`Windows`

```bash
$ aws ec2 delete-internet-gateway --internet-gateway-id=%GATEWAY_ID%
```
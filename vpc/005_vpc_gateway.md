# Internet Gatewayの作成

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](001_create_vpc.md)で環境変数に設定|
|GATEWAY_ID|[004 Internet Gatewayの作成](vpc/004_create_gateway.md)で環境変数に設定|

## Internet Gatewayの作成

```bash
$ aws ec2 attach-internet-gateway --internet-gateway-id ${GATEWAY_ID} --vpc-id ${VPC_ID}
```
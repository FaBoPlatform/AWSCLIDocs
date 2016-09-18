# 009 Internet GatewayとVPCを関連付ける

## つくるもの

![](/img/vpc/vpc009.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](/vpc/001_create_vpc.md)で環境変数に設定|
|GATEWAY_ID|[004 Internet Gatewayの作成](/vpc/004_create_gateway.md)で環境変数に設定|

## Internet Gatewayの作成

OS X

```bash
$ aws ec2 attach-internet-gateway --internet-gateway-id ${GATEWAY_ID} --vpc-id ${VPC_ID}
```

Windows

```bash
$ aws ec2 attach-internet-gateway --internet-gateway-id %GATEWAY_ID% --vpc-id %VPC_ID%
```

## 対応付けを確認する

OS X

```bash
$ aws ec2 describe-internet-gateways --internet-gateway-id ${GATEWAY_ID}
```

Windows

```bash
$ aws ec2 describe-internet-gateways --internet-gateway-id %GATEWAY_ID%
```

Attachmentsの項目ができ、アタッチされたVPCのIDが追加される。

```json
{
    "InternetGateways": [
        {
            "Tags": [], 
            "InternetGatewayId": "igw-########", 
            "Attachments": [
                {
                    "State": "available", 
                    "VpcId": "vpc-########"
                }
            ]
        }
    ]
}
```


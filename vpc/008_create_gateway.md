# Internet Gatewayの作成

## 作るもの

![](/img/vpc/gateway001.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|GATEWAY_ID|本項で環境変数に設定|

## Internet Gatewayの作成

```bash
$ aws ec2 create-internet-gateway
```

返り値

```json
{
    "InternetGateway": {
        "Tags": [], 
        "InternetGatewayId": "igw-406f1a25", 
        "Attachments": []
    }
}
```

環境変数に設定しておく。

```bash
$ export GATEWAY_ID="igw-########"
```
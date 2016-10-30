# 009 Internet Gatewayへタグを追加する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|GATEWAY_TAG|[008 Internet Gatewayの作成](vpc/008_create_gateway.md)で設定|
|GATEWAY_ID|本項で環境変数に設定|

## Internet Gatewayの作成

`OS X`

```bash
$ export GATEWAY_TAG="gateway of fabo."
$ aws ec2 create-tags --resources ${GATEWAY_ID} --tags "Key=Name,Value=${GATEWAY_TAG}"
```

`Windows`

```bash
$ set GATEWAY_TAG=gateway of fabo.
$ aws ec2 create-tags --resources %GATEWAY_ID% --tags "Key=Name,Value=%GATEWAY_TAG%"
```

## 確認
`OS X`

```bash
$ aws ec2 describe-internet-gateways --internet-gateway-ids ${GATEWAY_ID}
```
`Windows`

```bash
$ aws ec2 describe-internet-gateways --internet-gateway-ids %GATEWAY_ID%
```

返り値

```bash
{
    "InternetGateways": [
        {
            "Tags": [
                {
                    "Value": "gateway of fabo", 
                    "Key": "Name"
                }
            ], 
            "InternetGatewayId": "igw-c56c12a0", 
            "Attachments": []
        }
    ]
}
```

## 確認(WebConsole)

![](/img/vpc/gateway_tag001.png)


# Cloud Formation

AWSアカウントに新しいInternet Gatewayを作成する。Internet Gatewayの作成できる数は5個まで。タグをつける場合、Tagsの中にKey, Valueを書く。

[AWS::EC2::InternetGateway](http://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-internet-gateway.html)

```json
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Template by FaBo",
    "Resources": {
    "FaBo Internet Gateway": {
        "Type": "AWS::EC2::InternetGateway",
        "Properties": {
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "gateway of fabo."
                }
            ]
        }
    }
}
```

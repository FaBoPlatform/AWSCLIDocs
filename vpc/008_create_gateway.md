# 008 Internet Gatewayの作成

## 作るもの

![](/img/vpc/vpc008.png)


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
        "InternetGatewayId": "igw-########", 
        "Attachments": []
    }
}
```

環境変数に設定しておく。

`OS X`

```bash
$ export GATEWAY_ID="igw-########"
```

`Windows`

```bash
$ set GATEWAY_ID=igw-########
```

# Cloud Formation

AWSアカウントに新しいInternet Gatewayを作成する。Internet Gatewayの作成できる数は5個まで。

[AWS::EC2::InternetGateway](http://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-internet-gateway.html)

```json
{
	"AWSTemplateFormatVersion": "2010-09-09",
	"Description": "Template by FaBo",
	"Resources": {
	"FaBoInternetGateway": {
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

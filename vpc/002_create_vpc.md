# 002 VPCの作成

## 作るもの

![](/img/vpc/vpc002.png)

* VPC
* VPC作成時にRouteTableも作成される
* VPC作成時にDefaultのSecurityGroupも作成される

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|CIDR_BLOCK|172.16.0.0/16|
|VPC_ID|本項で環境変数に設定|


CIDR_BLOCKは、[RFC 1918](http://www.faqs.org/rfcs/rfc1918.html) で定義されているPrivateアドレスを使うと良い。

* 10.0.0.0        -   10.255.255.255  (10/8 prefix)
* 172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
* 192.168.0.0     -   192.168.255.255 (192.168/16 prefix)

/16は、[RFC 4632](https://tools.ietf.org/html/rfc4632) で詳細を確認。/16は、サブネットが`255.255.0.0`となりIP数が`65,536`個。

* n.n.x.0/18           16384         262144
* n.n.x.0/17           32768         131072
* n.n.0.0/16           65536          65536    legacy "Class B"
* n.x.0.0/15          131072          32768
* n.x.0.0/14          262144          16384
* n.x.0.0/13          524288           8192


## VPCの作成

OS X
```bash
$ export CIDR_BLOCK="172.16.0.0/16"
$ aws ec2 create-vpc --cidr-block ${CIDR_BLOCK} 
```

Windows
```bash
$ set CIDR_BLOCK=172.16.0.0/16
$ aws ec2 create-vpc --cidr-block %CIDR_BLOCK%
```

返り値は、JSONでくるが、VpcIdだけの取得ができないので手動で環境変数に設定する。

```json
{
    "Vpc": {
        "VpcId": "vpc-########", 
        "InstanceTenancy": "default", 
        "State": "pending", 
        "DhcpOptionsId": "dopt-0f3f206d", 
        "CidrBlock": "172.16.0.0/16", 
        "IsDefault": false
    }
}
```

## 環境変数に設定

OS X

```bash
$ export VPC_ID="vpc-########"
```

Windows

```bash
$ set VPC_ID=vpc-########
```

## 確認

`OS X`

```bash
$ echo ${VPC_ID}
```

`Windows`

```bash
$ echo %VPD_ID%
```

## Route Tableの確認

VPC生成時にRouteTableも生成される

`OS X`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=${VPC_ID}"
```

`Windows`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=%VPC_ID%"
```

## DefaultのSecurity Groupの確認

`OS X`

```bash
$ aws ec2 describe-security-groups --filter "Name=vpc-id,Values=${VPC_ID}"
````

`Windows`

```bash
$ aws ec2 describe-security-groups --filter "Name=vpc-id,Values=%VPC_ID%"
```

## Reference

* [Amazon VPCの制限](http://docs.aws.amazon.com/ja_jp/AmazonVPC/latest/UserGuide/VPC_Appendix_Limits.html)
* [DHCPオプションセット](http://docs.aws.amazon.com/ja_jp/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS)


# Cloud Formation

Vpcを作成する。

[AWS::EC2::VPC](http://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-vpc.html)

```json
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "Template by FaBo",
    "Resources": {
	"FaBoVpc": {
      "Type": "AWS::EC2::VPC",
      "Properties": {
        "CidrBlock": "172.16.0.0/16",
        "InstanceTenancy": "default",
        "EnableDnsSupport": true,
        "EnableDnsHostnames": false,
        "Tags": []
      }
    }
}
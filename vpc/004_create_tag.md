# VPCにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[002 VPCの作成](/vpc/002_create_vpc.md)で環境変数に設定|
|VPC_TAG| vpc of fabo|

## VPCにタグをつける

`OS X`

```bash
$ export VPC_TAG="vpc of fabo"
$ aws ec2 create-tags --resources ${VPC_ID} --tags "Key=Name,Value=${VPC_TAG}"
```

`Windows`

```bash
$ set VPC_TAG=vpc of fabo
$ aws ec2 create-tags --resources %VPC_ID% --tags "Key=Name,Value=%VPC_TAG%"
```

## vpc-idで絞って情報を表示し反映されているか確認する

`OS X`

```bash
$ aws ec2 describe-vpcs --vpc-ids "${VPC_ID}"
```

`Windows`

```bash
$ aws ec2 describe-vpcs --vpc-ids "%{VPC_ID}%"
```

JSONにTagsの項目が出現する。

```json
{
    "Vpcs": [
        {
            "VpcId": "vpc-#######", 
            "InstanceTenancy": "default", 
            "Tags": [
                {
                    "Value": "vpc of fabo", 
                    "Key": "Name"
                }
            ], 
            "State": "available", 
            "DhcpOptionsId": "dopt-0f3f206d", 
            "CidrBlock": "172.16.0.0/16", 
            "IsDefault": false
        }
    ]
}
```

## 確認

![](/img/vpc/tag001.png)

![](/img/vpc/tag002.png)

![](/img/vpc/tag003.png)

## DefaultのSecurity Groupにもタグ付けしておく(おまけ)

`OS X`

DefaultのSecurity GroupのIDを取得

```bash
$ aws ec2 describe-security-groups --filter "Name=vpc-id,Values=${VPC_ID}"
```

```bash
$ export DEFAULT_SEC_GROUP_ID="sg-#########"
```

```bash
$ export DEFAULT_SEC_GROUP_TAG="default sec of fabo"
$ aws ec2 create-tags --resources ${DEFAULT_SEC_GROUP_ID} --tags "Key=Name,Value=${DEFAULT_SEC_GROUP_TAG}"
```

`Windows`

DefaultのSecurity GroupのIDを取得

```bash
$ aws ec2 describe-security-groups --filter "Name=vpc-id,Values=%VPC_ID%"
```

```bash
$ export DEFAULT_SEC_GROUP_ID=sg-#########
```

```bash
$ export DEFAULT_SEC_GROUP_TAG=default sec of fabo
$ aws ec2 create-tags --resources %DEFAULT_SEC_GROUP_ID% --tags "Key=Name,Value=%DEFAULT_SEC_GROUP_TAG%"
```

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
        "Tags": [
          {
            "Key": "Name",
            "Value": "vpc of fabo"
          }
        ]
      }
    }
}

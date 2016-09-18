# 003 VPC関連情報を表示

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[002 VPCの作成](/vpc/002_create_vpc.md)で環境変数に設定|

## 現在存在するVPCの検索

```bash
$ aws ec2 describe-vpcs
```

## vpc-idで絞る

`OS X`

```bash
$ aws ec2 describe-vpcs --vpc-ids ${VPC_ID}
```

`Windows`

```bash
$ aws ec2 describe-vpcs --vpc-ids %VPC_ID%
```
## Route Tableの確認

`OS X`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=${VPC_ID}"
```

`Windows`

```bash
$ aws ec2 describe-route-tables --filter "Name=vpc-id,Values=%VPC_ID%"
```

## VPCと関連するサブネットの検索

VPCの初期作成時には、生成されないので空の値が返ってくる

`OS X`

```
$ aws ec2 describe-subnets --filter "Name=vpc-id,Values=${VPC_ID}"
```

`Windows`

```
$ aws ec2 describe-subnets --filter "Name=vpc-id,Values=%VPC_ID%"
```
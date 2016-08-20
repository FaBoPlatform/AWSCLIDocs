# VPCの一覧の表示

## 現在存在するVPCの検索

```bash
$ aws ec2 describe-vpcs
```

## vpc-idで絞る

```bash
$ aws ec2 describe-vpcs --vpc-ids "${VPC_ID}"
```

## 現在存在するサブネットの検索

> aws ec2 describe-subnets

どのVPCの下にあるかは、VPCの情報を取得した際と VpcId を比較して判断すること。

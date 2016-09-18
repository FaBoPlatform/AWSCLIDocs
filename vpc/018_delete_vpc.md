# 016 VPCの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](/vpc/001_create_vpc.md)で環境変数に設定|

## VPCの削除

```bash
$ aws ec2 delete-vpc --vpc-id=${VPC_ID} 
```

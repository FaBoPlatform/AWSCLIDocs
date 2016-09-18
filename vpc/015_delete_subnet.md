# 015 VPCの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SUBNET_UD|[006 Subnetの作成](vpc/006_create_subnet.md)で環境変数に設定|

## VPCの削除

`OS X`

```bash
$ aws ec2 delete-subnet --subnet-id=${SUBNET_ID} 
```

`Windows`

```bash
$ aws ec2 delete-subnet --subnet-id=%SUBNET_ID% 
```

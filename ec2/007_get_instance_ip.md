# インスタンスのIPアドレスを取得する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[005 インスタンスを生成する](/ec2/005_create_instance.md)で環境変数に設定|

## インスタンスのIPアドレスを取得する

```bash
$ aws ec2 describe-instances --instance-id ${INSTANCE_ID} --query Reservations[0].Instances[0].PublicIpAddress
```

## 環境変数に設定

```bash
$ export IP=`aws ec2 describe-instances --instance-id ${INSTANCE_ID} --query Reservations[0].Instances[0].PublicIpAddress --output text`
````


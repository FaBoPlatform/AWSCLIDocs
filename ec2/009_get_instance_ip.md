# 009 インスタンスのIPアドレスを取得する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[007 インスタンスを生成する](/ec2/007_create_instance.md)で環境変数に設定|

## インスタンスのIPアドレスを取得する

`OS X`

```bash
$ aws ec2 describe-instances --instance-id ${INSTANCE_ID} --query Reservations[0].Instances[0].PublicIpAddress
```

`Windows`

```bash
$ aws ec2 describe-instances --instance-id %INSTANCE_ID% --query Reservations[0].Instances[0].PublicIpAddress
```


## 環境変数に設定

`OS X`

```bash
$ export IP=`aws ec2 describe-instances --instance-id ${INSTANCE_ID} --query Reservations[0].Instances[0].PublicIpAddress --output text`
```

`Windows`

```bash
$ aws ec2 describe-instances --instance-id %INSTANCE_ID% --query Reservations[0].Instances[0].PublicIpAddress
```

```bash
$ set IP=###.###.###.###
```
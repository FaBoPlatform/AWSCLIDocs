# 005 AMIの検索

AMIは、Amazon マシンイメージの略で、AMIからインスタンスを起動することができる。

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AMI_ID|本項で設定|

## AMIの検索

```bash
$ aws ec2 describe-images
```

## AmazonがオーナーのAMIを検索

```bash
$ aws ec2 describe-images --owners self amazon
```

## Amazon LinuxのAMIを検索し作成日付順に並べる

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))"
```

## 作成日指定でAmazon Linuxを検索

`2012-10-08T18:19:50.000Z`に作成されたAmazon Linuxを取得

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query 'Images[?CreationDate==`2012-10-08T18:19:50.000Z`]'
```

## 最新のAmazon LinuxのImageIDを取得　

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))[0].ImageId"
```

## 最新のAmazon LinuxのImage IDを環境変数に定義

`OS X`

```bash
$ export AMI_ID=`aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))[0].ImageId" \
--output text`
```

`Windows`

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))[0].ImageId" \
```

結果

```bash
"ami-37cc1b56"
```

環境変数に設定

```bash
$ set AMI_ID=ami-37cc1b56
```

## 確認

`OS X`

```bash
echo ${AMI_ID}
```

`Windows`

```bash
echo %AMI_ID%
```


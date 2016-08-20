# Amazon LinuxのImageIDの取得

本項目では、環境変数　`AMI_ID`　にAMIのImageIDを設定する

## Amazon Linuxの取得

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
```

## 最新のAmazon LinuxのImage IDを取得(日付順)

```bash
$ aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))"
```

## 最新のAmazon LinuxのImage IDを環境変数に定義

```bash
$ export AMI_ID=`aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query "reverse(sort_by(Images,&CreationDate))[0].ImageId" \
--output text`
```

## 確認

```bash
echo ${AMI_ID}
```
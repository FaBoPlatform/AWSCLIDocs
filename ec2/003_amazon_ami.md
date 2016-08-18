# Amazon LinuxのImageIDの取得

## Amazon Linuxの取得

> aws ec2 describe-images \<br>
> --owners self amazon \<br>
> --filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \<br>

## 最新のAmazon LinuxのImage IDを取得(日付順)

> aws ec2 describe-images \<br>
> --owners self amazon \<br>
> --filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \<br>
> --query "reverse(sort_by(Images,&CreationDate))"<br>

## 最新のAmazon LinuxのImage IDを環境変数に定義

```shell
export AMI_ID=`aws ec2 describe-images \<br>
--owners self amazon \<br>
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \<br>
--query "reverse(sort_by(Images,&CreationDate))[0].ImageId" \<br>
--output text'<br>
```

確認

> echo ${AMI_ID}

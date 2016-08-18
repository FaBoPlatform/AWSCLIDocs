# 日付指定でAmazon LinuxのAMIの情報を取得

## Amazon LinuxのImage情報の取得

```shell
aws ec2 describe-images \
--owners self amazon \
--filters "Name=root-device-type,Values=ebs" "Name=name,Values=amzn-ami-hvm-*" "Name=virtualization-type,Values=hvm" \
--query 'Images[?CreationDate==`2012-10-08T18:19:50.000Z`]'
```


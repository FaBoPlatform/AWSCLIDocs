# 004 EBSをInstanceにAtacheする

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VOLUME_ID|[002 EBSの作成](/ebs/002_create_ebs.md)で設定|
|INSTANCE_ID|本項目で設定|
|DEVICE|本項目で設定|

## Security Groupの作成

`OS X`

```bash
$ export INSTANCE_ID="i-########"
$ export DEVICE="/dev/sdh"
$ aws ec2 attach-volume --volume-id ${VOLUME_ID} --instance-id ${INSTANCE_ID} --device ${DEVICE}
```

`Windows`

```bash
$ export INSTANCE_ID=i-########
$ export DEVICE="/dev/sdh"
$ aws ec2 attach-volume --volume-id %VOLUME_ID% --instance-id %INSTANCE_ID% --device %DEVICE%
```

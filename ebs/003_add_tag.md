# 003 EBSにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VOLUME_ID|[002 EBSの作成](/ebs/002_create_ebs.md)で設定|

## Security Groupの作成

`OS X`

```bash
$ export VOLUME_TAG="fabo volume."
$ aws ec2 create-tags --resources ${VOLUME_ID} --tags "Key=Name,Value=${VOLUME_TAG}"
```

`Windows`

```bash
$ export VOLUME_TAG=fabo volume.
$ aws ec2 create-tags --resources %VOLUME_ID% --tags "Key=Name,Value=%%VOLUME_TAG%"

```

## 確認

`OS X`

```bash
$ aws ec2 describe-volumes --volume-id ${VOLUME_ID}
```

`Windows`

```bash
$ aws ec2 describe-volumes --volume-id %VOLUME_ID%
```

```
{
    "Volumes": [
        {
            "AvailabilityZone": "ap-northeast-1a", 
            "Attachments": [], 
            "Tags": [
                {
                    "Value": "fabo volume.", 
                    "Key": "Name"
                }
            ], 
            "Encrypted": false, 
            "VolumeType": "gp2", 
            "VolumeId": "vol-############", 
            "State": "available", 
            "Iops": 100, 
            "SnapshotId": "", 
            "CreateTime": "2016-09-24T13:13:29.023Z", 
            "Size": 10
        }
    ]
}
```
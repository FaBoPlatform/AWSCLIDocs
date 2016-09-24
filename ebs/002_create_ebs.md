# 002 EBSの作成

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SIZE|本項目で設定|
|REGION|本項目で設定|
|VOLUME_TYPE|本項目で設定|
|AVAILABILITY_ZONE|本項目で設定|

## EBSの種類

### SSD
* プロビジョンド IOPS SSD (io1) ボリューム
* 汎用 SSD (gp2) ボリューム

### HDD
* スループット最適化 HDD (st1) ボリューム
* Cold HDD (sc1) ボリューム

## EBSの作成

```bash
$ export SIZE=10
$ export REGION="ap-northeast-1"
$ export VOLUME_TYPE="gp2"
$ export AVAILABILITY_ZONE="ap-northeast-1a"
$ aws ec2 create-volume --size ${SIZE} --region ${REGION} --availability-zone ${AVAILABILITY-ZONE} --volume-type ${VOLUME_TYPE}
```

```bash
{
    "AvailabilityZone": "ap-northeast-1a", 
    "Encrypted": false, 
    "VolumeType": "gp2", 
    "VolumeId": "vol-########", 
    "State": "creating", 
    "Iops": 100, 
    "SnapshotId": "", 
    "CreateTime": "2016-09-24T13:13:29.023Z", 
    "Size": 10
}
```

## Volume IDを環境変数に設定

```bash
$ export VOLUME_ID="vol-########"
```



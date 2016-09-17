# Subnetの作成

## 調べる事

![](/img/vpc/available001.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AVAILABILITY_ZONE|本項で設定|

## Subnetの作成

```bash
$ aws ec2 describe-availability-zones
```

結果

```json
{
    "AvailabilityZones": [
        {
            "State": "available", 
            "RegionName": "ap-northeast-1", 
            "Messages": [], 
            "ZoneName": "ap-northeast-1a"
        }, 
        {
            "State": "available", 
            "RegionName": "ap-northeast-1", 
            "Messages": [], 
            "ZoneName": "ap-northeast-1b"
        }, 
        {
            "State": "available", 
            "RegionName": "ap-northeast-1", 
            "Messages": [], 
            "ZoneName": "ap-northeast-1c"
        }
    ]
}
```

今回は、`ap-northeast-1a`を環境変数に設定します。

```bash
$ export AVAILABILITY_ZONE="ap-northeast-1a"
```

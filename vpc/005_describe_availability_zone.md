# 005 Availability Zoneを調べる

## 調べる事

![](/img/vpc/vpc005.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AVAILABILITY_ZONE|本項で設定|

## Availability Zoneを調べる

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

OS X

```bash
$ export AVAILABILITY_ZONE="ap-northeast-1a"
```

Windows

```bash
$ set AVAILABILITY_ZONE=ap-northeast-1a
```
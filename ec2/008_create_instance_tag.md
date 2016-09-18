# 008 インスタンスにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[007 インスタンスを生成する](/ec2/007_create_instance.md)で環境変数に設定|
|INSTANCE_TAG|fabo web|

## インスタンスにタグをつける

`OS X`

```bash
$ export INSTANCE_TAG="fabo web"
$ aws ec2 create-tags --resources ${INSTANCE_ID} --tags "Key=Name,Value=${INSTANCE_TAG}"
```

`Windows`

```bash
$ set INSTANCE_TAG=fabo web
$ aws ec2 create-tags --resources %INSTANCE_ID% --tags "Key=Name,Value=%INSTANCE_TAG%"
```

## 確認

`OS X`

```bash
$ aws ec2 describe-instances --instance-id ${INSTANCE_ID}
```

`Windows`

```bash
$ aws ec2 describe-instances --instance-id %INSTANCE_ID%
```


Tagsの項目が追加される

```
                    "Tags": [
                        {
                            "Value": "fabo web", 
                            "Key": "Name"
                        }
                    ], 
```

結果

```json
{
    "Reservations": [
        {
            "OwnerId": "############", 
            "ReservationId": "r-########", 
            "Groups": [], 
            "Instances": [
                {
                    "Monitoring": {
                        "State": "disabled"
                    }, 
                    "PublicDnsName": "", 
                    "State": {
                        "Code": 16, 
                        "Name": "running"
                    }, 
                    "EbsOptimized": false, 
                    "LaunchTime": "2016-08-21T01:11:05.000Z", 
                    "PublicIpAddress": "##.##.##.##", 
                    "PrivateIpAddress": "172.16.1.151", 
                    "ProductCodes": [], 
                    "VpcId": "vpc-########", 
                    "StateTransitionReason": "", 
                    "InstanceId": "i-########", 
                    "ImageId": "ami-374db956", 
                    "PrivateDnsName": "ip-172-16-1-151.ap-northeast-1.compute.internal", 
                    "KeyName": "fabo", 
                    "SecurityGroups": [
                        {
                            "GroupName": "fabo", 
                            "GroupId": "sg-########"
                        }
                    ], 
                    "ClientToken": "", 
                    "SubnetId": "subnet-########", 
                    "InstanceType": "t2.micro", 
                    "NetworkInterfaces": [
                        {
                            "Status": "in-use", 
                            "MacAddress": "0a:b9:7a:cb:c8:0d", 
                            "SourceDestCheck": true, 
                            "VpcId": "vpc-########", 
                            "Description": "", 
                            "Association": {
                                "PublicIp": "##.##.##.##", 
                                "PublicDnsName": "", 
                                "IpOwnerId": "amazon"
                            }, 
                            "NetworkInterfaceId": "eni-########", 
                            "PrivateIpAddresses": [
                                {
                                    "Association": {
                                        "PublicIp": "##.##.##.##", 
                                        "PublicDnsName": "", 
                                        "IpOwnerId": "amazon"
                                    }, 
                                    "Primary": true, 
                                    "PrivateIpAddress": "172.16.1.151"
                                }
                            ], 
                            "Attachment": {
                                "Status": "attached", 
                                "DeviceIndex": 0, 
                                "DeleteOnTermination": true, 
                                "AttachmentId": "eni-attach-a0f9aa55", 
                                "AttachTime": "2016-08-21T01:11:05.000Z"
                            }, 
                            "Groups": [
                                {
                                    "GroupName": "fabo", 
                                    "GroupId": "sg-########"
                                }
                            ], 
                            "SubnetId": "subnet-########", 
                            "OwnerId": "############", 
                            "PrivateIpAddress": "172.16.1.151"
                        }
                    ], 
                    "SourceDestCheck": true, 
                    "Placement": {
                        "Tenancy": "default", 
                        "GroupName": "", 
                        "AvailabilityZone": "ap-northeast-1c"
                    }, 
                    "Hypervisor": "xen", 
                    "BlockDeviceMappings": [
                        {
                            "DeviceName": "/dev/xvda", 
                            "Ebs": {
                                "Status": "attached", 
                                "DeleteOnTermination": true, 
                                "VolumeId": "vol-########", 
                                "AttachTime": "2016-08-21T01:11:06.000Z"
                            }
                        }
                    ], 
                    "Architecture": "x86_64", 
                    "RootDeviceType": "ebs", 
                    "RootDeviceName": "/dev/xvda", 
                    "VirtualizationType": "hvm", 
                    "Tags": [
                        {
                            "Value": "fabo web", 
                            "Key": "Name"
                        }
                    ], 
                    "AmiLaunchIndex": 0
                }
            ]
        }
    ]
}
```



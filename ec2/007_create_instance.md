# 007 インスタンスを生成する

## つくるもの

![](/img/ec2/ec2_007.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AMI_ID|[005 AMIの検索](/ec2/005_search_ami.md)で環境変数に設定|
|SEC_GROUP_ID|[002 Security Groupの作成](/ec2/002_create_security.md)で環境変数に設定|
|SUBNET_UD|	[VPC-006 Subnetの作成](/vpc/006_create_subnet.md)で環境変数に設定|
|KEY_NAME| [006 Key pairの作成](/ec2/006_key_pair.md)で環境変数に設定|
|INSTANCE_TYPE|t2.micro|
|MY_REGION|ap-noetheast-1|
|INSTANCE_ID|本項で設定|


## ストレージ設定JSON

32GのEBSでインスタンスを作成する場合は、下記のようなJSONを用意。Defaultは8G。

storage.json

```bash
[
    {
        "DeviceName": "/dev/xvda",
        "Ebs":{"VolumeSize":32}
    }
]
```

/dev/xvdaにするとルートデバイスが拡張される。/dev/sdh等にするとブロックデバイスが別途追加される。

## インスタンスを生成する

```bash
$ export INSTNCE_TYPE="t2.micro"
$ export MY_REGION="ap-northeast-1"
$ aws ec2 run-instances \
--image-id ${AMI_ID} \
--instance-type ${INSTNCE_TYPE} \
--key-name ${KEY_NAME} \
--region ${MY_REGION} \
--security-group-ids ${SEC_GROUP_ID} \
--subnet-id ${SUBNET_ID} \
--associate-public-ip-address \
--block-device-mapping file://storage.json
```

結果

```json
{
    "OwnerId": "###########", 
    "ReservationId": "r-########", 
    "Groups": [], 
    "Instances": [
        {
            "Monitoring": {
                "State": "disabled"
            }, 
            "PublicDnsName": "", 
            "RootDeviceType": "ebs", 
            "State": {
                "Code": 0, 
                "Name": "pending"
            }, 
            "EbsOptimized": false, 
            "LaunchTime": "2016-08-21T01:11:05.000Z", 
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
                    "VpcId": "vpc-48362d2d", 
                    "Description": "", 
                    "NetworkInterfaceId": "eni-########", 
                    "PrivateIpAddresses": [
                        {
                            "Primary": true, 
                            "PrivateIpAddress": "172.16.1.151"
                        }
                    ], 
                    "Attachment": {
                        "Status": "attaching", 
                        "DeviceIndex": 0, 
                        "DeleteOnTermination": true, 
                        "AttachmentId": "eni-attach-########", 
                        "AttachTime": "2016-08-21T01:11:05.000Z"
                    }, 
                    "Groups": [
                        {
                            "GroupName": "fabo", 
                            "GroupId": "sg-########"
                        }
                    ], 
                    "SubnetId": "subnet-#########", 
                    "OwnerId": "###############", 
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
            "BlockDeviceMappings": [], 
            "Architecture": "x86_64", 
            "StateReason": {
                "Message": "pending", 
                "Code": "pending"
            }, 
            "RootDeviceName": "/dev/xvda", 
            "VirtualizationType": "hvm", 
            "AmiLaunchIndex": 0
        }
    ]
}
```

## Instance Idを環境変数に設定

`OS X`

```bash
$ export INSTANCE_ID="i-########"
```

`Windows`

```bash
$ set INSTANCE_ID=i-########
```

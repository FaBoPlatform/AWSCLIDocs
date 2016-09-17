# インスタンスを生成する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AMI_ID|[003 AMIの検索](/ec2/003_search_ami.md)で環境変数に設定|
|SEC_GROUP_ID|[001 Security Groupの作成](/ec2/001_create_security.md)で環境変数に設定|
|SUBNET_UD|	[007 Subnetの作成](/vpc/007_create_subnet.md)で環境変数に設定|
|KEY_NAME| [004 Key pairの作成](/ec2/004_key_pair.md)で環境変数に設定|
|INSTANCE_TYPE|t2.micro|
|MY_REGION|ap-noetheast-1|
|INSTANCE_ID|本項で設定|

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
--associate-public-ip-address 
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

```bash
$ export INSTANCE_ID="i-########"
```

## User Dataを指定しての実行

インスタンスを起動時に、初回に実行するユーザデータを引き渡し、実行することも可能である。


install.sh

```bash
#!/bin/bash
yum update -y
yum install -y httpd24 php56 mysql55-server php56-mysqlnd
service httpd start
chkconfig httpd on
groupadd www
usermod -a -G www ec2-user
chown -R root:www /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} +
find /var/www -type f -exec chmod 0664 {} +
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

install.shをユーザデータに渡してインスタンスを起動

```bash
$ aws ec2 run-instances \
 --image-id ${AMI_ID} \
 --instance-type ${INSTNCE_TYPE} \
 --key-name ${KEY_NAME} \
 --region ${MY_REGION} \
 --security-group-ids ${SEC_GROUP_ID} \
 --subnet-id ${SUBNET_ID} \
 --associate-public-ip-address \
 --user-data=file://install.sh
```


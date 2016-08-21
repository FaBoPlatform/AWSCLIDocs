# インスタンスを生成する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AMI_ID|[003 AMIの検索](/ec2/003_search_ami.md)で環境変数に設定|
|SEC_GROUP_ID|[001 Security Groupの作成](/ec2/001_create_security.md)で環境変数に設定|
|SUBNET_UD|	[007 Subnetの作成](/vpc/007_create_subnet.md)で県境変数に設定|
|INSTANCE_TYPE|t2.micro|
|KET_NAME|fabo|
|MY_REGION|ap-noetheast-1|

## インスタンスを生成する

```bash
$ export INSTNCE_TYPE="t2.micro"
$ export KEY_NAME="fabo"
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




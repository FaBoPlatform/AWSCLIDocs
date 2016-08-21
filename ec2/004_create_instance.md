# インスタンスを生成する

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|AMI_ID|本項で設定|
|SEC_GROUP_ID|本項で設定|
|SUBNET_UD|本項で設定|
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

# インスタンスを生成する

## インスタンスを生成する

```bash
$ export INSTNCE_TYPE="t2.micro"
$ export KEY_NAME="fabo"
$ export MY_REGION="ap-northeast-1"
$ aws ec2 run-instances --image-id ${AMI_ID} --instance-type ${INSTNCE_TYPE} --key-name ${KEY_NAME} --region ${MY_REGION}--security-group-ids ${SECURITY_GROUP_ID}
```


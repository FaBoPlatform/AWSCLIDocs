# Security Groupの作成

## Security Groupの削除
```bash
$ export SEC_GROUP_NAME="fabo"
$ aws ec2 delete-security-group --group-name ${SEC_GROUP_NAME} 
```
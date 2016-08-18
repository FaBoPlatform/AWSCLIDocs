# Security Groupの作成

## Security Groupの作成

```bash
$ export SEC_GROUP_NAME="fabo"
$ export SEC_GROUP_DESC="group of fabo."
$ aws ec2 create-security-group --group-name ${SEC_GROUP_NAME} --description "${SEC_GROUP_DESC}"
```

## Security Groupの削除

```bash
$ aws ec2 delete-security-group --group-name ${SEC_GROUP_NAME} 
```

## Security Groupの情報の表示

```bash
$ aws ec2 describe-security-groups --group-names ${SEC_GROUP_NAME}
```

## Security Groupの情報からGroup IDを取得

```bash
$ aws ec2 describe-security-groups --group-names ${SEC_GROUP_NAME}
```

## Securiy Groupの情報からGroup IDを抽出

```bash
$ aws ec2 describe-security-groups --group-names ${SEC_GROUP_NAME} --query 'SecurityGroups[0].GroupId'
```

## Securiy Groupの情報からGroup IDを抽出し環境変数に設定


```bash
$ export SEC_GROUP_ID=`aws ec2 describe-security-groups --group-names ${SEC_GROUP_NAME} --query 'SecurityGroups[0].GroupId' --output text`
```

確認

```bash
$ echo ${SEC_GROUP_ID}
```
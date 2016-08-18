# インバウンドをSecurity Groupに設定

## TCP 80ポートを全許可

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```

## TCP 23ポートを全許可

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```

## Security Groupの情報を取得

```bash
$ aws ec2 describe-security-groups --group-id ${SEC_GROUP_ID}
```

## TCP 80ポートを削除

```bash
$ aws ec2 revoke-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```
## TCP 23ポートを削除

```bash
$ aws ec2 revoke-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```
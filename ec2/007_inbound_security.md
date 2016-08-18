# インバウンドをSecurity Groupに設定

## TCP 80ポートを全許可

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```

## TCP 23ポートを全許可

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```
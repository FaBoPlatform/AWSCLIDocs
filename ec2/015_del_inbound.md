# インバウンドをSecurity Groupから削除

## TCP 22ポートを削除

`OS X`

```bash
$ aws ec2 revoke-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 22 --cidr 0.0.0.0/0
```

`Windows`

```bash
$ aws ec2 revoke-security-group-ingress --group-id %SEC_GROUP_ID% --protocol 'tcp' --port 22 --cidr 0.0.0.0/0
```


## TCP 80ポートを削除

`OS X`

```bash
$ aws ec2 revoke-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```

`Windows`

```bash
$ aws ec2 revoke-security-group-ingress --group-id %SEC_GROUP_ID% --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```

## TCP 23ポートを削除

`OS X`


```bash
$ aws ec2 revoke-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```

`Windows`


```bash
$ aws ec2 revoke-security-group-ingress --group-id %SEC_GROUP_ID% --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```
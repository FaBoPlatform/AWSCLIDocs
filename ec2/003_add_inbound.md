# インバウンドをSecurity Groupに追加

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[003 Security Groupの作成](/ec2/003_create_security.md)|

## TCP 22ポートを全許可(AMIリクエストポート, 必須)

OS X

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 22 --cidr 0.0.0.0/0
```

Winows

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol tcp --port 22 --cidr 0.0.0.0/0
```

## TCP 80ポートを全許可(HTTP, 任意)

OS X

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 80 --cidr 0.0.0.0/0
```

Windows

```bash
$ aws ec2 authorize-security-group-ingress --group-id %SEC_GROUP_ID% --protocol tcp --port 80 --cidr 0.0.0.0/0
```

## TCP 23ポートを全許可(SSH, 任意)

OS X

```bash
$ aws ec2 authorize-security-group-ingress --group-id ${SEC_GROUP_ID} --protocol 'tcp' --port 23 --cidr 0.0.0.0/0
```

Windows

```bash
$ aws ec2 authorize-security-group-ingress --group-id %SEC_GROUP_ID% --protocol tcp --port 23 --cidr 0.0.0.0/0
```


## Security Groupの情報を取得

OS X
```bash
$ aws ec2 describe-security-groups --group-id ${SEC_GROUP_ID}
```

Windows
```bash
$ aws ec2 describe-security-groups --group-id %SEC_GROUP_ID%
```

```json
{
    "SecurityGroups": [
        {
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1", 
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ], 
                    "UserIdGroupPairs": [], 
                    "PrefixListIds": []
                }
            ], 
            "Description": "group of fabo.", 
            "IpPermissions": [], 
            "GroupName": "fabo", 
            "VpcId": "vpc-#########", 
            "OwnerId": "#############", 
            "GroupId": "sg-#########"
        }
    ]
}
```

追加後。`IpPermissions`のタグに80番と23番が追加。

```json
{
    "SecurityGroups": [
        {
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1", 
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ], 
                    "UserIdGroupPairs": [], 
                    "PrefixListIds": []
                }
            ], 
            "Description": "group of fabo.", 
            "IpPermissions": [
                {
                    "PrefixListIds": [], 
                    "FromPort": 80, 
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ], 
                    "ToPort": 80, 
                    "IpProtocol": "tcp", 
                    "UserIdGroupPairs": []
                }, 
                {
                    "PrefixListIds": [], 
                    "FromPort": 22, 
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ], 
                    "ToPort": 22, 
                    "IpProtocol": "tcp", 
                    "UserIdGroupPairs": []
                },
                {
                    "PrefixListIds": [], 
                    "FromPort": 23, 
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ], 
                    "ToPort": 23, 
                    "IpProtocol": "tcp", 
                    "UserIdGroupPairs": []
                }
            ], 
            "GroupName": "fabo", 
            "VpcId": "vpc-########", 
            "OwnerId": "############", 
            "GroupId": "sg-########"
        }
    ]
}
```

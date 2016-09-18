# 003 Security Groupにタグをつける

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SEC_GROUP_ID|[002 Security Groupの作成](/ec2/002_create_security.md)で環境変数に設定|
|SEC_GROUP_TAG|fabo security.|

## Security Groupの作成

`OS X`

```bash
$ export SEC_GROUP_TAG="fabo security."
$ aws ec2 create-tags --resources $SEC_GROUP_ID --tags "Key=Name,Value=${SEC_GROUP_TAG}"
```

`Windows`

```bash
$ set SEC_GROUP_TAG=fabo security.
$ aws ec2 create-tags --resources %SEC_GROUP_ID% --tags "Key=Name,Value=%SEC_GROUP_TAG%"

```

## 確認

`OS X`

```bash
$ aws ec2 describe-security-groups --group-ids ${SEC_GROUP_ID}
```

`Windows`

```bash
$ aws ec2 describe-security-groups --group-ids %SEC_GROUP_ID%
```

```
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
            "Tags": [
                {
                    "Value": "fabo security", 
                    "Key": "Name"
                }
            ], 
            "IpPermissions": [], 
            "GroupName": "fabo", 
            "VpcId": "vpc-########", 
            "OwnerId": "############", 
            "GroupId": "sg-04d1cc60"
        }
    ]
}
```

## 確認(WebConsole)

![](/img/ec2/security001.png)
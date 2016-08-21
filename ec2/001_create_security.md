# Security Groupの作成

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|VPC_ID|[001 VPCの作成](/vpc/001_create_vpc.md)|
|SEC_GROUP_NAME| fabo |
|SEC_GROUP_DESC| group of fabo |
|SEC_GROUP_ID| 本項で設定 |


## Security Groupの作成

```bash
$ export SEC_GROUP_NAME="fabo"
$ export SEC_GROUP_DESC="group of fabo."
$ aws ec2 create-security-group --group-name ${SEC_GROUP_NAME} --description "${SEC_GROUP_DESC}" --vpc-ip=${VPC_IP}
```

返り値

```bash
{
    "GroupId": "sg-########"
}
```

## GroupIDを環境変数に設定

```bash
$ export SEC_GROUP_ID="########"
```

## Security Groupの情報を表示

```bash
$ aws ec2 describe-security-groups --group-ids ${SEC_GROUP_ID}
```

結果

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
            "VpcId": "vpc-########", 
            "OwnerId": "############", 
            "GroupId": "sg-########"
        }
    ]
}
```
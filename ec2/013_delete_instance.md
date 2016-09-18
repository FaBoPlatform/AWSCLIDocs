# 013 インスタンスの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[007 インスタンスを生成する](/ec2/007_create_instance.md)で環境変数に設定|

## インスタンスの削除

`OS X`

```bash
$ aws ec2 terminate-instances --instance-id ${INSTANCE_ID}
```

`Windows`

```bash
$ aws ec2 terminate-instances --instance-id %INSTANCE_ID%
```

結果

```json
{
    "TerminatingInstances": [
        {
            "InstanceId": "i-########", 
            "CurrentState": {
                "Code": 32, 
                "Name": "shutting-down"
            }, 
            "PreviousState": {
                "Code": 16, 
                "Name": "running"
            }
        }
    ]
}
```
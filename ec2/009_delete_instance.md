# インスタンスの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[004 インスタンスを生成する](/ec2/004_create_instance.md)|

## インスタンスの削除

```bash
$ aws ec2 terminate-instances --instance-id ${INSTANCE_ID}
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
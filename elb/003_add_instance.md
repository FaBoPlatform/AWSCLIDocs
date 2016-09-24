# 003 ELBにインスタンスの追加

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|INSTANCE_ID|[007 インスタンスを生成する](/ec2/007_create_instance.md)で設定|
|ELB_NAME|[002 ELBの作成](/elb/002_create_elb.md)で設定|



## ELBの作成

```bash
$ aws elb register-instances-with-load-balancer --load-balancer-name ${ELB_NAME} --instances ${INSTANCE_ID}
```

結果

```bash
{
    "Instances": [
        {
            "InstanceId": "i-########"
        }
    ]
}
```
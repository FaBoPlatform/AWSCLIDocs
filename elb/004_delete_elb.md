# 004 ELBの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|ELB_NAME|[002 ELBの作成](/elb/002_create_elb.md)で設定|

## ELBの作成

```bash
$ aws elb delete-load-balancer --load-balancer-name ${ELB_NAME}
```


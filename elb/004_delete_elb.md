# 003 ELBの削除

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|ELB_NAME|本項で環境変数に設定|

## ELBの作成

```bash
$ aws elb delete-load-balancer --load-balancer-name ${ELB_NAME}
```


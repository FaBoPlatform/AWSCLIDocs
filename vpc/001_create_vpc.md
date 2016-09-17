# VPCの作成

## 作るもの

![](/img/vpc/vpc001.png)

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|CIDR_BLOCK|172.16.0.0/16|
|VPC_ID|本項で環境変数に設定|


CIDR_BLOCKは、[RFC 1918](http://www.faqs.org/rfcs/rfc1918.html) で定義されているPrivateアドレスを使うと良い。

* 10.0.0.0        -   10.255.255.255  (10/8 prefix)
* 172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
* 192.168.0.0     -   192.168.255.255 (192.168/16 prefix)

/16は、[RFC 4632](https://tools.ietf.org/html/rfc4632) で詳細を確認。/16は、サブネットが`255.255.0.0`となりIP数が`65,536`個。

* n.n.x.0/18           16384         262144
* n.n.x.0/17           32768         131072
* n.n.0.0/16           65536          65536    legacy "Class B"
* n.x.0.0/15          131072          32768
* n.x.0.0/14          262144          16384
* n.x.0.0/13          524288           8192


## VPCの作成

```bash
$ export CIDR_BLOCK="172.16.0.0/16"
$ aws ec2 create-vpc --cidr-block ${CIDR_BLOCK} 
```

返り値は、JSONでくるが、VpcIdだけの取得ができないので手動で環境変数に設定する。

```json
{
    "Vpc": {
        "VpcId": "vpc-########", 
        "InstanceTenancy": "default", 
        "State": "pending", 
        "DhcpOptionsId": "dopt-0f3f206d", 
        "CidrBlock": "172.16.0.0/16", 
        "IsDefault": false
    }
}
```

環境変数に設定

```bash
$ export VPC_ID="vpc-########"
```

## 確認

```bash
$ echo ${VPC_ID}
```

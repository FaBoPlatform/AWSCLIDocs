# VPC

## VPCの上限

5個

http://docs.aws.amazon.com/ja_jp/general/latest/gr/aws_service_limits.html#limits_vpc

## VPCで使えるIPアドレス範囲

RFC1918で規定されているグローバルIPとして使えないIPアドレス範囲から必要な範囲を自分で定義して使います。（10.0.0.0/16とか）

http://www.faqs.org/rfcs/rfc1918.html

```bash
3. Private Address Space
     10.0.0.0        -   10.255.255.255  (10/8 prefix)
     172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
     192.168.0.0     -   192.168.255.255 (192.168/16 prefix)
```


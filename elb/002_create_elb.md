# 002 ELBの作成

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|SUBNET_ID|[006 Subnetの作成](/vpc/006_create_subnet.md)で設定|
|ELB_NAME|本項で環境変数に設定|

## 設定ファイル

setting.json

```json
[
        {
          "Protocol": "HTTP",
          "LoadBalancerPort": 80,
          "InstanceProtocol": "HTTP",
          "InstancePort": 80
        }
]
```

## ELBの作成

```bash
$ export ELB_NAME="faboble"
$ aws elb create-load-balancer --load-balancer-name ${ELB_NAME} --listeners file://setting.json --subnets ${SUBNET_ID}
```

特に指定がない場合、SecruityGroupはVPC作成時のDefaultのSecurityGroupが対応付けされる。

## 確認

```bash
$ aws elb describe-load-balancers --load-balancer-names ${ELB_NAME}
```

```bash
{
    "LoadBalancerDescriptions": [
        {
            "Subnets": [
                "subnet-###########"
            ], 
            "CanonicalHostedZoneNameID": "###############", 
            "CanonicalHostedZoneName": "faboble-##########.ap-northeast-1.elb.amazonaws.com", 
            "ListenerDescriptions": [
                {
                    "Listener": {
                        "InstancePort": 80, 
                        "LoadBalancerPort": 80, 
                        "Protocol": "HTTP", 
                        "InstanceProtocol": "HTTP"
                    }, 
                    "PolicyNames": []
                }
            ], 
            "HealthCheck": {
                "HealthyThreshold": 10, 
                "Interval": 30, 
                "Target": "TCP:80", 
                "Timeout": 5, 
                "UnhealthyThreshold": 2
            }, 
            "VPCId": "vpc-#############", 
            "BackendServerDescriptions": [], 
            "Instances": [], 
            "DNSName": "faboble-##########.ap-northeast-1.elb.amazonaws.com", 
            "SecurityGroups": [
                "sg-########"
            ], 
            "Policies": {
                "LBCookieStickinessPolicies": [], 
                "AppCookieStickinessPolicies": [], 
                "OtherPolicies": []
            }, 
            "LoadBalancerName": "faboble", 
            "CreatedTime": "2016-09-24T09:01:19.710Z", 
            "AvailabilityZones": [
                "ap-northeast-1a"
            ], 
            "Scheme": "internet-facing", 
            "SourceSecurityGroup": {
                "OwnerAlias": "#############", 
                "GroupName": "default"
            }
        }
    ]
}
```


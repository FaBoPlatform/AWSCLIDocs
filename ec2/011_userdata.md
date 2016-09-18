# 011 Userdataを指定してインスタンスを生成する

インスタンスの生成は、Userdataを指定して生成時にScriptを起動する事も可能です。

## User Dataを指定しての実行

インスタンスを起動時に、初回に実行するユーザデータを引き渡し、実行することも可能である。

install.sh

```bash
#!/bin/bash
yum update -y
yum install -y httpd24 php56 mysql55-server php56-mysqlnd
service httpd start
chkconfig httpd on
groupadd www
usermod -a -G www ec2-user
chown -R root:www /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} +
find /var/www -type f -exec chmod 0664 {} +
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

install.shをユーザデータに渡してインスタンスを起動

OS X
```bash
$ aws ec2 run-instances \
 --image-id ${AMI_ID} \
 --instance-type ${INSTNCE_TYPE} \
 --key-name ${KEY_NAME} \
 --region ${MY_REGION} \
 --security-group-ids ${SEC_GROUP_ID} \
 --subnet-id ${SUBNET_ID} \
 --associate-public-ip-address \
 --user-data=file://install.sh
```

Windows

`--user-data=file:c:¥home¥install.sh` はinstall.shのフォルダに合わせる

```bash
$ aws ec2 run-instances \
 --image-id ${AMI_ID} \
 --instance-type ${INSTNCE_TYPE} \
 --key-name ${KEY_NAME} \
 --region ${MY_REGION} \
 --security-group-ids ${SEC_GROUP_ID} \
 --subnet-id ${SUBNET_ID} \
 --associate-public-ip-address \
 --user-data=file:c:¥home¥install.sh
```


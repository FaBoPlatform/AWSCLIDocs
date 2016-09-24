# 005 EBSをAmazon Linuxでマウント

## 本項で使用する環境変数

|環境変数|値|
|:--|:--|
|DEVICE|[004 EBSにEC2インスタンスに追加](/ebs/004_attach_instance.md)で設定|

## EBSをAmazon Linuxにマウント

SSHでEC2にログイン

```bash
$ sudo mkdir /mydata
$ sudo mount ${DEVICE} /mydata
```

```bash
$ df -h
ファイルシス   サイズ  使用  残り 使用% マウント位置
/dev/xvda1       7.8G  7.7G   18M  100% /
devtmpfs         995M   60K  995M    1% /dev
tmpfs           1003M     0 1003M    0% /dev/shm
/dev/xvdh        9.8G   23M  9.2G    1% /mydata
```

次回起動時にも反映されるようにfstabに追記

```bash
$ sudo vi /etc/fstab
```

最後の行に追加
```bash
#
LABEL=/     /           ext4    defaults,noatime  1   1
tmpfs       /dev/shm    tmpfs   defaults        0   0
devpts      /dev/pts    devpts  gid=5,mode=620  0   0
sysfs       /sys        sysfs   defaults        0   0
proc        /proc       proc    defaults        0   0
/dev/sdh    /data       ext4    defaults        1   1
```

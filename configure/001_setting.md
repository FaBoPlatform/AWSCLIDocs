# Configure

## AWS Access key IDとAWS Secret Access Key

```AWS Access key ID```と```AWS Secret Access Key```は、AWS Consoleから発行する。

![](/img/config/config001.png)

![](/img/config/config002.png)

![](/img/config/config003.png)

![](/img/config/config004.png)

アクセスキーIDとシークレットアクセスキーをメモする。

## Configure

```
$ aws configure
AWS Access Key ID [****************CJCQ]: アクセスキーIDを入力
AWS Secret Access Key [****************nLqr]: シークレットアクセスキーを入力
Default region name [ap-northeast-1]: ap-northeast-1
Default output format [json]: json
```
## 設定できるRegion

|リージョン名|場所|
|:-:|:-:|
| us-east-1 | 米国東部（バージニア北部） |
| us-west-2 | 米国西部（オレゴン） |
| us-west-1 | 米国西部（北カリフォルニア） |
| eu-west-1 | 欧州（アイルランド） |
| eu-central-1 | 欧州（フランクフルト） |
| ap-southeast-1 | アジアパシフィック（シンガポール） |
| ap-northeast-1 | アジアパシフィック (東京) |
| ap-southeast-2 | アジアパシフィック（シドニー） |
| ap-northeast-2 | アジアパシフィック (ソウル) |
| ap-south-1 | アジアパシフィック (ムンバイ) |
| sa-east-1 | 南米 (サンパウロ) |
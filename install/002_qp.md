# AWSCLIのInstall

Mac OS X 10.10以上であることを想定します。  
OS Xでは Python、および Python パッケージ管理ツール *setuptools* が標準でインストールされています。  
*setuptools* が提供するCLIツール `easy_install` を使い、Pythonパッケージ管理ツールの決定版である `pip` を事前にインストールします。
そののち、`pip` を使って `awscli` をインストールします。

```sh
easy_install pip
pip install awscli
```

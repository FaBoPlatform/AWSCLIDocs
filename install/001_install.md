# 必要なもの

* Python 2.7系
* PIP
* AWSCLI

## Pythonの確認

```sh
$ python --version 
```

を実行し、PythonのVersionを確認します。

## PIPのInstall

OS Xでは Python、および Python パッケージ管理ツール *setuptools* が標準でインストールされています。  
*setuptools* が提供するCLIツール `easy_install` を使い、Pythonパッケージ管理ツールの決定版である `pip` を事前にインストールします。

```sh
easy_install pip
```

## AWCLIのInstall

`pip` を使って `awscli` をインストールします。


```sh
pip install awscli
```

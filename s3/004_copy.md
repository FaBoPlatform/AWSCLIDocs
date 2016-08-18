# BucketにCopy

## Local->BucketにCopy

```bash
$ aws s3 cp test.txt s3://fabo_bucket/test2.txt
```
## Bucket->LocalにCopy

```bash
$ aws s3 cp s3://fabo_bucket/test2.txt test3.txt
```

## jpg形式のファイルを除き指定ディレクトリのファイルを再帰的なコピー

```bash
$ aws s3 cp ./ s3://fabo_bucket/ --recursive --exclude "*.jpg"
```

## .log形式を除いた指定ディレクトリのファイルの再帰的なコピー

```bash
$ aws s3 cp ./ s3://fabo_bucket/ --recursive --exclude "*" --include "*.log"
```
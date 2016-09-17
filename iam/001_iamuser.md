# IAM User

## Root UserとIAM User

Root Userはアカウントを発行したユーザ。すべてのAWS Componetへのアクセスできる強力な権限を持っている。
IAMは、Identity and Access Managementの略で、ユーザ単位で、各コンポーネントへのアクセス許可を記載したポリシーを付与することで、権限管理ができる仕組み。

## IAM Userの作成

![](/img/iam/iam001.png)

![](/img/iam/iam002.png)

![](/img/iam/iam003.png)

![](/img/iam/iam004.png)


## IAM Userのログイン

https://`AWSアカウントID`.signin.aws.amazon.com/console

で発行されたIAM UserでAWS Consoleへアクセスできる。

## IAM Userへのパスワード変更の権限付与

権限を付与したいIAMユーザのユーザーロールに下記のJSONで権限を付与。

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": [
      "iam:ChangePassword",
      "iam:GetAccountPasswordPolicy"
    ],
    "Resource": "*"
  }
}
```
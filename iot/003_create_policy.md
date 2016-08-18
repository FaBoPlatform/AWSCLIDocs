# ThingのPolicy作成

## ThingのPolicy作成する

policy.json
```json
{"Version": "2012-10-17",
"Statement": [{
	"Effect": "Allow",
	"Action":["iot:*"],
	"Resource": ["*"]
	}]
}
```

```bash
$ export POLICY_NAME="fabo_policy"
$ export MY_REGION="ap-northeast-1"
$ aws iot create-policy --thing-name ${POLICY_NAME} --region ${MY_REGION} --policy-document file://policy.json
```
# ThingのPolicyを削除

## ThingのPolicy削除する

```bash
$ export POLICY_NAME="fabo_policy"
$ export MY_REGION="ap-northeast-1"
$ aws iot delete-policy --thing-name ${POLICY_NAME} --region ${MY_REGION}
```
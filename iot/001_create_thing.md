# Thingの作成

## Thingを作成する

```bash
$ export THING_NAME="fabo_thing"
$ export MY_REGION="ap-northeast-1"
$ aws iot create-thing --thing-name ${THING_NAME} --region ${MY_REGION}
```
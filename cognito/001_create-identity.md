# Identity Poolを作成する

## Identity Poolを作成する

```bash
export POOL_NAME = "fabo_pool"
export MY_REGION="ap-northeast-1"
$ aws cognito-identity create-identity-pool
--identity-pool-name ${POOL_NAME} 
--region ${MY_REGION}
```


## Identity Poolを作成する(非認証ユーザのアクセスを許可する)

```bash
export POOL_NAME = "fabo_pool"
export MY_REGION="ap-northeast-1"
$ aws cognito-identity create-identity-pool
--identity-pool-name ${POOL_NAME} 
--region ${MY_REGION}
--allow-unauthenticated-identities
```

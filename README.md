# sample-sam

## Procedure

**samで雛形を作る**

```
sam init --runtime nodejs10.x
```

**node_modulesのinstall**

```
cd hello_world
yarn
yarn test
```

**start**

```
sam local start-api
open http://127.0.0.1:3000/hello
```

**S3バケットを作る**

```
aws s3 mb s3://{BUCKET_NAME}
```

**package化してS3にUploadする**

```
sam package --output-template-file packaged.yaml --s3-bucket {BUCKET_NAME} --profile {AWS_CREDENTIAL}
```

**デプロイ**

```
sam deploy --template-file packaged.yaml --stack-name {CFN_STACK_NAME} --capabilities CAPABILITY_IAM --profile {AWS_CREDENTIAL}
```

**API Gatewayのエンドポイントを調べる**

```
aws cloudformation describe-stacks --stack-name sam-app --query 'Stacks[].Outputs[?OutputKey==`HelloWorldApi`]' --output table
```

**curlでテスト**

```
curl https://i0vy28y2pk.execute-api.ap-northeast-1.amazonaws.com/Prod/hello/
```

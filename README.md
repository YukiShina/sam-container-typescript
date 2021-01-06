# sam-container-typescript

Lambda でコンテナイメージがサポートされたので、試してみました。

`sam init` の Quick Start Templates をベースに TypeScript を使えるように改造しています。

localstack(S3) + puppeteer も入っています。

## localstack

S3 をローカルで検証する

コンテナ起動

```bash
docker-compose up -d
```

credential 登録

```bash
~/.aws/credentials

[localstack]
aws_access_key_id = dummy
aws_secret_access_key = dummy
```

テストバケット作成

```bash
aws s3 mb s3://test-bucket --endpoint-url=http://localhost:4566 --profile=localstack
```

テストオブジェクト作成

```bash
aws s3 --endpoint-url=http://localhost:4566 cp SAMPLE.txt s3://test-bucket --profile=localstack
```

localstack と同一の docker network を利用して api サーバーを起動

```bash
sam local start-api --docker-network [NETWORK ID] --profile=localstack
```

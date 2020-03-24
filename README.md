# AWS Elasticsearch Proxy

This a basic reverse proxy that automatically signs incoming requests using the AWS V4 signing method and redirects to the defined host. It's intended for use with AWS Elasticsearch but should work with any HTTP service.

## Configure

Requires AWS credentials, which can be configured using standard AWS methods such as shared credentials file (~/.aws/credentials) or environment variables (e.g. AWS_ACCESS_KEY_ID + AWS_SECRET_ACCESS_KEY). See: https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials

### Environment variables

Any custom environment variables should be added to a file called `.env`. Env vars in this file will override any system environment vars and also the defaults contained within `.env.default`.

- AWS_ACCESS_KEY_ID - Used to authenticate with AWS
- AWS_SECRET_ACCESS_KEY - Used to authenticate with AWS
- AWS_REGION - Used to authenticate with AWS
- AWS_ESPROXY_ENVIRONMENTS - A list of environments to configure. Each environment requires a _LISTEN_PORT and _HOST variable.

Example configuration for a STAGE and PROD environment, which sets up two HTTP proxies to route to two separate hosts and listen on ports 9001 (staging) and 10001 (production):
```
AWS_ESPROXY_ENVIRONMENTS=STAGE,PROD
AWS_ESPROXY_STAGE_LISTEN_PORT=9001
AWS_ESPROXY_STAGE_HOST=my-staging-elasticsearch.us-east-1.es.amazonaws.com
AWS_ESPROXY_PROD_LISTEN_PORT=10001
AWS_ESPROXY_PROD_HOST=my-production-elasticsearch.us-east-1.es.amazonaws.com
```

## Run

```
go run main.go
```
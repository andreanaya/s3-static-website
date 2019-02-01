# Static AWS S3 Website

Example of a static website deployed on AWS S3 with a custom domain using Serverless framework.

The website contents are stored on a S3 bucket and distributed with Cloudfront and redirect http requests to https.

Another S3 bucket redirects www to non www requests.

## Requirements

- [Serverless framework](https://serverless.com/) with [AWS credentials](https://serverless.com/framework/docs/providers/aws/guide/credentials#setup-with-the-aws-cli) configured
- Valid domain name using Route 53 as [DNS provider](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/CreatingHostedZone.html)
- Valid certificate created with [AWS Certificate Manager](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html)*

*\* Must be located in `us-east-1` region to be used with the [Cloudfront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-and-https-requirements.html#https-requirements-aws-region) distribution*

## Instalation

- Run `serverless install --url https://github.com/andreanaya/s3-static-website.git`
- Rename `env-sample.yml` to `env.yml`
- Replace `DOMAIN_NAME` by valid domain name on `env.yml`
- Replace `ACM_CERTIFICATE_ARN` by valid certificate Amazon Resource Name (ARN) on `env.yml`

## Deployment

Run `sls deploy -v` or `sls deploy -r REGION_CODE -v` to deploy to a specific [region](https://docs.aws.amazon.com/general/latest/gr/rande.html).

## Bucket synchronization

Run `aws s3 sync build s3://BUCKET_NAME` to upload contents from `build` directory to the S3 bucket. The bucket name will be printed by the CloudFormation output.
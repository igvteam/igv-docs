<p class="page-title"> Amazon Web Services support </p>

Public data files hosted in Amazon S3 buckets can be loaded into IGV using [https URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-bucket-intro.html).

Authenticated access using s3:// urls is supported by either (1) enabling OAuth access with Cognito using the UMCCR
contributed AWS configuration option, or (2) setting AWS credentials and region information as described
[here]( https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and
[here](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-region-selection.html).

For more details on using Cognito for OAuth access, see the 
[UMCCR documentation on the backend](https://umccr.org/blog/igv-amazon-backend-setup/)
and [frontend for a provisioning URL step by step guide](https://umccr.org/blog/igv-amazon-frontend-setup/).
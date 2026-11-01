# Al-Asfour Consulting website

A responsive static website for Al-Asfour Consulting. The site uses plain HTML, CSS, and
JavaScript and can be previewed locally by opening `index.html` or serving the repository root
with any static file server. DM Sans is self-hosted in `assets/fonts/`.

The visual palette uses white surfaces with navy `#12304A` typography, accents, and artwork.

## AWS deployment with GitHub Actions

The workflow in `.github/workflows/deploy.yml` deploys the site to an S3 bucket whenever changes
are pushed to `main`. If a CloudFront distribution ID is configured, it also invalidates the
distribution cache. No AWS keys are stored in the repository; the workflow assumes an AWS IAM role
through GitHub's OIDC identity provider.

Configure these repository settings under **Settings → Secrets and variables → Actions**:

| Name | Type | Purpose |
| --- | --- | --- |
| `AWS_ROLE_ARN` | Secret | ARN of the IAM role that trusts this repository's GitHub OIDC identity |
| `AWS_REGION` | Variable | AWS region containing the S3 bucket |
| `S3_BUCKET` | Variable | Bucket used as the CloudFront origin |
| `CLOUDFRONT_DISTRIBUTION_ID` | Variable, optional | Distribution to invalidate after deployment |

The assumed role needs permission to list and write/delete objects in the target bucket. When
CloudFront invalidation is enabled, it also needs `cloudfront:CreateInvalidation` on the configured
distribution. Configure the bucket and CloudFront distribution separately, including HTTPS,
default root object `index.html`, and private S3 origin access.

The contact link is `dr.ahmedalasfour@gmail.com`.

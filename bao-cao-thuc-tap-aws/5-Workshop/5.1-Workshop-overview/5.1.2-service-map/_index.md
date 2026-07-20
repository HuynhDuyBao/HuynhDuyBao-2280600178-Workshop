---
title: "Service map"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.1.2. </b> "
---

| Service | Status | Role in Netflop |
| --- | --- | --- |
| Cloudflare | In use | Domain `netflop.win`, DNS, HTTPS |
| Amazon EC2 | Running | Hosts Node.js backend, frontend build, Nginx reverse proxy |
| Amazon RDS MySQL | Running | Main database `web_xem_phim_final` |
| Amazon S3 | In use | Stores video input, HLS output, images, avatars, subtitles |
| AWS Elemental MediaConvert | In use | Converts MP4/MKV to HLS 360p/480p/720p/1080p |
| Amazon CloudFront | In use | Delivers HLS stream and protects stream with signed cookies |
| AWS Lambda | In use | Handles MediaConvert events and converts SRT to VTT |
| Amazon EventBridge | In use | Captures MediaConvert COMPLETE/ERROR/CANCELED events |
| Amazon CloudWatch | In use | Monitors EC2, RDS, Lambda |
| Amazon SNS | In use | Alert topic `netflop-alerts` |
| IAM Role | In use | Grants permissions for EC2, MediaConvert, Lambda |
| AWS Systems Manager | In use | Deploys/reloads EC2 from local AWS CLI |
| Amazon Cognito | Configured | Cognito/Google auth needs account/region confirmation |

{{% notice info %}}
Image needed: AWS services list or Netflop service map.
{{% /notice %}}

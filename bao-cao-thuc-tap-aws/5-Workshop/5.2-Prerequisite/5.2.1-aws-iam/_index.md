---
title: "AWS and IAM preparation"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

#### Required AWS permissions

The AWS account needs permissions for EC2, RDS, S3, MediaConvert, CloudFront, Lambda, EventBridge, CloudWatch, SNS, IAM, and Systems Manager.

#### Confirmed resources

| Group | Resource |
| --- | --- |
| EC2 | `netflop-web`, instance ID `i-059adda84b4d65714`, type `t3.micro`, public IP `18.143.150.109` |
| RDS | `netflop-db`, MySQL, `db.t4g.micro`, database `web_xem_phim_final`, port `3306` |
| S3 input | `netflop-input-source` |
| S3 output | `netflop-output-source` |
| Main CloudFront | `d11jdx7259stge.cloudfront.net` |
| Lambda | `netflop-mediaconvert-notifier`, `netflop-subtitle-converter` |
| EventBridge | `netflop-mediaconvert-job-state-change` |
| SNS | `netflop-alerts` |

![role](/pic/role.png)



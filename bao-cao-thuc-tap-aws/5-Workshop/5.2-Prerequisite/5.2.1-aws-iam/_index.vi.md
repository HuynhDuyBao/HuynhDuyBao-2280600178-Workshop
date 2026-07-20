---
title: "Chuẩn bị AWS và IAM"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

#### Yêu cầu tài khoản AWS

Tài khoản AWS cần có quyền thao tác các dịch vụ:

* EC2, RDS, S3
* MediaConvert, CloudFront
* Lambda, EventBridge
* CloudWatch, SNS
* IAM, Systems Manager

#### Tài nguyên chính đã xác nhận

| Nhóm | Tài nguyên |
| --- | --- |
| EC2 | `netflop-web`, instance ID `i-059adda84b4d65714`, type `t3.micro`, public IP `18.143.150.109` |
| RDS | `netflop-db`, MySQL, `db.t4g.micro`, database `web_xem_phim_final`, port `3306` |
| S3 input | `netflop-input-source` |
| S3 output | `netflop-output-source` |
| CloudFront chính | `d11jdx7259stge.cloudfront.net` |
| Lambda | `netflop-mediaconvert-notifier`, `netflop-subtitle-converter` |
| EventBridge | `netflop-mediaconvert-job-state-change` |
| SNS | `netflop-alerts` |

#### Lưu ý bảo mật

* Không dùng root account để triển khai.
* Không đưa access key, secret key, password database hoặc private key vào báo cáo.
* IAM role cho EC2, Lambda và MediaConvert chỉ nên có quyền đúng nhu cầu.

![role](/pic/role.png)


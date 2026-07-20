---
title: "Chuẩn bị source code và biến môi trường"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

#### Mục tiêu

Chuẩn bị source code Netflop và các biến môi trường để backend có thể kết nối RDS, S3, MediaConvert, CloudFront, Cognito/Google OAuth và frontend production domain.

#### Source code chính

```text
netflop/
  backend/
    src/
    package.json
  frontend/
    src/
    package.json
  database/
    web_xem_phim_final_dump.sql
```

#### Nhóm biến môi trường backend

Các biến quan trọng cần có trong `.env` backend:

```text
NODE_ENV=production
PORT=5000

DB_HOST=netflop-db.c76we6m8scy0.ap-southeast-1.rds.amazonaws.com
DB_PORT=3306
DB_NAME=web_xem_phim_final
DB_USER=<db-user>
DB_PASSWORD=<db-password>

CORS_ORIGIN=https://netflop.win
APP_BASE_URL=https://netflop.win

AWS_REGION=ap-southeast-1
AWS_S3_INPUT_BUCKET=netflop-input-source
AWS_S3_OUTPUT_BUCKET=netflop-output-source
AWS_MEDIACONVERT_ENDPOINT=https://mediaconvert.ap-southeast-1.amazonaws.com
AWS_MEDIACONVERT_ROLE_ARN=<mediaconvert-role-arn>

AWS_CLOUDFRONT_DOMAIN=<cloudfront-domain>
AWS_CLOUDFRONT_KEY_PAIR_ID=<key-pair-id>
AWS_CLOUDFRONT_PRIVATE_KEY_PATH=<private-key-path>

JWT_SECRET=<jwt-secret>
AWS_MEDIACONVERT_WEBHOOK_SECRET=<webhook-secret>
```

#### Nhóm biến môi trường frontend

Frontend production cần trỏ API về domain production:

```text
VITE_API_BASE_URL=https://netflop.win/api
```

Nếu dùng OAuth callback, các URL cần đồng bộ:

```text
GOOGLE_REDIRECT_URI=https://netflop.win/auth/callback
AWS_COGNITO_REDIRECT_URI=https://netflop.win/auth/callback
AWS_COGNITO_LOGOUT_URI=https://netflop.win/
```

#### Nguyên tắc bảo mật

* Không commit file `.env` thật lên Git.
* Không chụp màn hình access key, client secret, database password hoặc private key.
* Production nên dùng IAM Role cho EC2 thay vì access key.
* Các secret có thể chuyển sang AWS Systems Manager Parameter Store hoặc AWS Secrets Manager ở bước hoàn thiện.


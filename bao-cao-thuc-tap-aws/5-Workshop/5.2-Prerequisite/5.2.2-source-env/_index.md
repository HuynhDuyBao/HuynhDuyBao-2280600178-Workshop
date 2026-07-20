---
title: "Source code and environment variables"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

#### Source code checklist

Check the React frontend, Node.js backend, video upload API, stream session API `/api/stream/session`, MediaConvert webhook `/api/uploads/mediaconvert/events`, subtitle logic, and AWS configuration.

#### Important environment variables

```env
DB_HOST=netflop-db.c76we6m8scy0.ap-southeast-1.rds.amazonaws.com
DB_PORT=3306
DB_NAME=web_xem_phim_final

AWS_REGION=ap-southeast-1
S3_INPUT_BUCKET=netflop-input-source
S3_OUTPUT_BUCKET=netflop-output-source
CLOUDFRONT_DOMAIN=d11jdx7259stge.cloudfront.net
```


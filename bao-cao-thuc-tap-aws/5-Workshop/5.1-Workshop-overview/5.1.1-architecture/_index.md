---
title: "Overall architecture"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.1.1. </b> "
---

#### Goal

Netflop separates the web application, database, media storage, video processing, and content delivery into different AWS components for easier operation, monitoring, and scaling.

#### Main access flow

```text
User / Admin
   |
   v
Cloudflare DNS + HTTPS
   |
   v
netflop.win
   |
   v
EC2 netflop-web
   |-- Nginx reverse proxy
   |-- React frontend
   |-- Node.js backend API
   |
   |---- RDS MySQL netflop-db
   |
   |---- S3 netflop-input-source
   |          |
   |          v
   |      MediaConvert
   |          |
   |          v
   |---- S3 netflop-output-source
              |
              v
        CloudFront protected HLS
              |
              v
        Video Player
```

#### Video and automation flow

Admin uploads MP4/MKV video to backend, backend stores it in S3 input and creates a MediaConvert job. MediaConvert generates HLS output in S3 output. EventBridge receives job state changes, invokes Lambda, and Lambda calls backend webhook `/api/uploads/mediaconvert/events` to update episode status in RDS.

{{% notice info %}}
Image needed: main access flow and MediaConvert -> EventBridge -> Lambda -> Backend flow.
{{% /notice %}}

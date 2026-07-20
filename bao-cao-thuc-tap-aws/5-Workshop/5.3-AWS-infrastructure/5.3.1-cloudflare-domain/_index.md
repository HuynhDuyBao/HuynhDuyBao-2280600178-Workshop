---
title: "Configure Cloudflare domain"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

Cloudflare manages `netflop.win`, DNS, and user-facing HTTPS.

```text
User -> Cloudflare DNS + HTTPS -> netflop.win -> EC2 public IP -> Nginx
```

#### Checking steps

1. Open Cloudflare Dashboard.
2. Select `netflop.win`.
3. Check the DNS record pointing to EC2 public IP `18.143.150.109`.
4. Check proxy/HTTPS status.
5. Open `https://netflop.win`.

{{% notice info %}}
Image needed: Cloudflare DNS record and successful website access through domain.
{{% /notice %}}

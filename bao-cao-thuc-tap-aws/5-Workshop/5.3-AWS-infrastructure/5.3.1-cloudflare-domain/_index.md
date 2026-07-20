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

<img width="1534" height="732" alt="DNSrecord" src="https://github.com/user-attachments/assets/94fd5bf5-31aa-497a-b305-47372831b1ad" />
<img width="1533" height="705" alt="console" src="https://github.com/user-attachments/assets/0bd988e4-f1d1-4be9-9c62-8e3c059035ca" />

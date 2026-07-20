---
title: "Configure EC2, Nginx, and backend"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

EC2 `netflop-web` runs the React frontend build, Node.js backend API, and Nginx reverse proxy.

| Attribute | Value |
| --- | --- |
| Instance name | `netflop-web` |
| Instance ID | `i-059adda84b4d65714` |
| Instance type | `t3.micro` |
| Public IP | `18.143.150.109` |
| Security Group | `netflop-ec2-sg` |

#### Checking steps

1. Check instance `netflop-web` is running.
2. Check Security Group `netflop-ec2-sg`.
3. Access EC2 through SSH or Systems Manager.
4. Check Nginx and backend process:

```bash
sudo systemctl status nginx
pm2 status
pm2 logs
```

{{% notice info %}}
Image needed: EC2 instance, Security Group, Nginx running, and PM2/backend running.
{{% /notice %}}

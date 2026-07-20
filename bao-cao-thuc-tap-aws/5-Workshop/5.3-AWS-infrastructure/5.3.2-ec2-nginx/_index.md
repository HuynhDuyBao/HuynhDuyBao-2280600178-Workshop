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

<img width="1530" height="653" alt="ec2running" src="https://github.com/user-attachments/assets/2eff03bf-a377-4a53-803a-100974030c59" />
<img width="1514" height="680" alt="security gr" src="https://github.com/user-attachments/assets/d00c0456-a9ed-49c5-a4d3-927feecbf8b1" />
<img width="836" height="425" alt="ngix status" src="https://github.com/user-attachments/assets/b204e162-527a-4707-ab2f-68f6fe4fa22f" />


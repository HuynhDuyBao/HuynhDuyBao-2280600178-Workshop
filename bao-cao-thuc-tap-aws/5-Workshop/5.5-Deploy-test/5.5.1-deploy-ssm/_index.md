---
title: "Deploy/reload with EC2 and Systems Manager"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

#### Goal

Deploy or reload Netflop on EC2 `netflop-web`. Systems Manager can be used to run deploy/reload commands from local AWS CLI.

#### Deployment steps

1. Pull latest source code or upload a new build to EC2.
2. Install dependencies if needed.
3. Build React frontend.
4. Restart Node.js backend.
5. Reload Nginx.
6. Open `https://netflop.win`.

#### Commands to check

```bash
sudo systemctl status nginx
pm2 status
pm2 logs
```

{{% notice info %}}
Image needed: deploy/reload terminal, Nginx status, PM2/backend status, and website after deployment.
{{% /notice %}}

---
title: "Configure RDS and Security Group"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

RDS MySQL stores Netflop's main data: accounts, movies, episodes, subtitles, watch history, favorites, ratings, comments, and metadata.

| Attribute | Value |
| --- | --- |
| DB identifier | `netflop-db` |
| Engine | MySQL |
| Class | `db.t4g.micro` |
| DB name | `web_xem_phim_final` |
| Endpoint | `netflop-db.c76we6m8scy0.ap-southeast-1.rds.amazonaws.com` |
| Port | `3306` |

#### Checking steps

1. Check RDS `netflop-db` is Available.
2. Check endpoint and port `3306`.
3. Check backend environment variables.
4. Check RDS Security Group.
5. Test movie list API from frontend/backend.

{{% notice warning %}}
RDS is noted as public accessible. The improvement direction is to restrict its Security Group so only EC2 can access RDS.
{{% /notice %}}

{{% notice info %}}
Image needed: RDS database, endpoint, Security Group, and successful movie data API.
{{% /notice %}}

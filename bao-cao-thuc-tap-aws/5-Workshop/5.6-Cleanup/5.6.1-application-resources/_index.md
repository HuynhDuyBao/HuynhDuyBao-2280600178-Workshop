---
title: "Clean up application resources"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

#### Resources to check

* EC2 `netflop-web`
* EBS volume attached to EC2
* Elastic IP if used
* RDS `netflop-db`
* RDS snapshot
* Security Groups for EC2/RDS

#### Cleanup steps

1. Back up RDS data if needed.
2. Stop or terminate EC2 if the website no longer needs to run.
3. Delete unused EBS volumes.
4. Release unused Elastic IP.
5. Delete unnecessary RDS database/snapshots.
6. Review unused Security Groups.

{{% notice info %}}
Image needed: EC2/RDS before cleanup and status after cleanup.
{{% /notice %}}

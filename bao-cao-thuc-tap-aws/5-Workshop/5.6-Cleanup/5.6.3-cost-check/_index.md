---
title: "Check cost after cleanup"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

#### Items to check

* EC2 running instances
* Unattached EBS volumes
* Unused Elastic IPs
* RDS databases/snapshots
* S3 storage
* CloudFront distributions
* CloudWatch logs/alarms
* Lambda functions
* NAT Gateway if created

#### Checking steps

1. Open AWS Billing Dashboard.
2. Check cost by service.
3. Open Cost Explorer if detailed checking is needed.
4. Check AWS Budgets alerts.
5. Record cleanup results in the report.

{{% notice info %}}
Image needed: Billing Dashboard, Cost Explorer, or AWS Budgets after cleanup.
{{% /notice %}}

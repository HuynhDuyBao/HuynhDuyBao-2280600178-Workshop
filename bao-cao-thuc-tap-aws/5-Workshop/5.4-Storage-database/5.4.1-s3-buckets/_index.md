---
title: "Configure S3 input/output buckets"
date: 2026-07-10
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

S3 stores media files instead of saving them directly on EC2.

| Bucket | Role |
| --- | --- |
| `netflop-input-source` | Original uploaded files, video input, subtitle input |
| `netflop-output-source` | HLS output, public images, avatars, VTT subtitles |

```text
netflop-input-source
  |-- video-input/
  |-- subtitle-input/

netflop-output-source
  |-- hls/
  |-- images/
  |-- avatars/
  |-- subtitles/
```

{{% notice info %}}
Image needed: two S3 buckets, video input object, HLS output, and subtitle output.
{{% /notice %}}

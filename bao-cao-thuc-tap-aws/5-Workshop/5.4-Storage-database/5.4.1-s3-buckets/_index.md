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

<img width="1534" height="574" alt="s3ouput" src="https://github.com/user-attachments/assets/615d4283-777e-4178-81d4-bbc86843a31f" />
<img width="1534" height="549" alt="s3input" src="https://github.com/user-attachments/assets/f122a0fa-6354-403b-a208-d31d25ae2e82" />

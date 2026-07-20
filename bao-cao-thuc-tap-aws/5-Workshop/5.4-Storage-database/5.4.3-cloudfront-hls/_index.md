---
title: "Configure CloudFront HLS streaming"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

CloudFront distribution `d11jdx7259stge.cloudfront.net` delivers HLS streams from S3 output to the video player.

```text
Frontend -> Backend movie/episode info
Backend -> /api/stream/session signed cookies
Video Player -> CloudFront -> S3 output HLS
```

#### Checking steps

1. Open CloudFront console.
2. Check distribution `d11jdx7259stge.cloudfront.net` is Enabled.
3. Check origin points to S3 output.
4. Open a movie episode in Netflop.
5. Confirm the player streams HLS through CloudFront.

<img width="1485" height="709" alt="cf2" src="https://github.com/user-attachments/assets/a0da6e11-70f7-489e-ad7f-73b6ff4a3e6c" />
<img width="1533" height="802" alt="player1" src="https://github.com/user-attachments/assets/5c0aac26-5105-4d96-8303-b21634de05b7" />
<img width="1301" height="636" alt="cloudfront1" src="https://github.com/user-attachments/assets/bc229de8-2c2e-4e4c-8105-82e6d1b84f50" />

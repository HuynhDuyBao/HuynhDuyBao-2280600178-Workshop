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

{{% notice info %}}
Image needed: CloudFront distribution, S3 output origin, stream session API, and HLS player.
{{% /notice %}}

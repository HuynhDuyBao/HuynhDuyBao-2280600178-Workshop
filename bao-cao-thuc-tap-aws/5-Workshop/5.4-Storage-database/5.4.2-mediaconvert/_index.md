---
title: "Configure MediaConvert"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

MediaConvert converts uploaded MP4/MKV videos to HLS for browser playback.

```text
Admin upload video -> S3 input -> MediaConvert job -> S3 output HLS
```

Output qualities:

* 360p
* 480p
* 720p
* 1080p

#### Checking steps

1. Upload MP4/MKV from admin page.
2. Confirm the source video in `netflop-input-source`.
3. Open MediaConvert console.
4. Check the created job.
5. Wait for Complete.
6. Check `.m3u8` and segments in `netflop-output-source`.
7. Check backend saved `jobId`, `hls_url`, `cloudfront_url`, and `upload_status`.

<img width="1533" height="692" alt="hls" src="https://github.com/user-attachments/assets/0d87c576-6231-4414-ac61-736cd4db891d" />
<img width="1505" height="597" alt="mediaconvert" src="https://github.com/user-attachments/assets/89163e25-2ce0-46f9-9df5-ffaa15caa7c1" />

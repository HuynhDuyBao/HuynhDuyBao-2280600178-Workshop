---
title: "Test admin video upload"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

#### Upload flow

1. Admin signs in to the admin page.
2. Admin selects a movie/episode.
3. Admin selects an MP4/MKV video file.
4. Backend receives multipart upload request.
5. Video is uploaded to `netflop-input-source`.
6. Backend creates a MediaConvert job.
7. MediaConvert writes HLS output to `netflop-output-source`.
8. EventBridge receives COMPLETE.
9. Lambda `netflop-mediaconvert-notifier` calls backend webhook.
10. Backend updates episode `upload_status` to ready.

#### Backend values to check

* `jobId`
* `hls_url`
* `cloudfront_url`
* `upload_status`

{{% notice info %}}
Image needed: admin upload screen, S3 input object, MediaConvert Complete job, HLS output, and episode ready status.
{{% /notice %}}

---
title: "Test user features"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

#### Test checklist

| Feature | Expected result |
| --- | --- |
| Home page | Website loads through `netflop.win` |
| Movie list | Movies from RDS are displayed correctly |
| Search | Results match the keyword |
| Movie detail | Metadata and episode list are displayed |
| Login | User can sign in |
| Watch history/favorites | User activity is saved in database |
| HLS playback | Player streams video through CloudFront |
| Subtitles | Player displays VTT subtitles |

#### Common issues

* API fails because backend is not running.
* Images/videos fail due to wrong S3/CloudFront URL.
* Stream is blocked because signed cookies are not issued correctly.
* Subtitles do not show because `.vtt` file is missing or path is wrong.

![home](/pic/home.png)
![watch](/pic/tieptucxem.png)
![watch](/pic/tieptucxem2.png)
![play](/pic/moviedetail.png)
![play](/pic/movie1.png)

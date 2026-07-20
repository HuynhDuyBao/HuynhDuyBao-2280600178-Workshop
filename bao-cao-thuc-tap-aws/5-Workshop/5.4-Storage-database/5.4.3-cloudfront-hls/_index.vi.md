---
title: "Cấu hình CloudFront phát HLS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

#### Mục tiêu

CloudFront được dùng để phân phối HLS stream từ S3 output đến người xem. Distribution chính cho stream được cấu hình dạng protected HLS và sử dụng signed cookies để hạn chế truy cập trực tiếp vào video.

#### Distribution stream

```text
d11jdx7259stge.cloudfront.net
```

Origin chính trỏ về:

```text
netflop-output-source.s3.ap-southeast-1.amazonaws.com
```

#### Luồng phát video

```text
Frontend -> Backend lấy thông tin tập phim
Backend -> cấp stream session / signed cookies
Video Player -> CloudFront -> S3 output HLS
```

#### API liên quan

Backend cấp phiên xem stream qua API:

```text
/api/stream/session
```

API này tạo CloudFront signed cookies để trình duyệt được phép tải manifest và segment HLS trong một khoảng thời gian nhất định. Nhờ vậy, frontend không cần public trực tiếp toàn bộ object HLS trên S3.

#### Media proxy fallback

Backend có thêm API proxy:

```text
/api/media-proxy
```

API này dùng để xử lý một số trường hợp cần proxy media/phụ đề hoặc tránh lỗi CORS/mixed content. Khi triển khai production, thông báo lỗi trên video player không nên hiển thị raw stream URL để tránh lộ link nguồn.

#### Kiểm tra

1. Vào CloudFront console.
2. Kiểm tra distribution stream đang Enabled.
3. Kiểm tra origin trỏ đúng S3 output.
4. Mở một tập phim trên Netflop.
5. Kiểm tra request `/api/stream/session` trả cookie hợp lệ.
6. Kiểm tra player tải `index.m3u8` và segment qua HTTPS.

<img width="1485" height="709" alt="cf2" src="https://github.com/user-attachments/assets/4a658fd7-076f-4960-89af-3e224ea2b76c" />
<img width="1533" height="802" alt="player1" src="https://github.com/user-attachments/assets/7092bae1-fe58-4c31-9800-6b09fcc122d6" />
<img width="1301" height="636" alt="cloudfront1" src="https://github.com/user-attachments/assets/180ad1ab-5505-4689-a0ae-5189becf91bb" />

<!-- NETFLOP_DETAIL_START -->
#### Cách bảo vệ stream bằng signed cookies

Khi người dùng mở tập phim, frontend gọi backend để xin phiên xem stream. Backend tạo CloudFront signed cookies rồi set vào response. Sau đó player tải HLS qua CloudFront.

#### Code mẫu backend cấp stream session

~~~js
async function createStreamSession(req, res, next) {
  const sourceUrl = req.body?.sourceUrl || req.query?.sourceUrl;
  const signedSession = cloudFrontSignedCookieService.buildSignedCookies(sourceUrl);

  cloudFrontSignedCookieService.setSignedCookies(res, signedSession);

  res.json({
    success: true,
    data: {
      enabled: signedSession.enabled,
      playbackUrl: signedSession.playbackUrl,
      expiresAt: signedSession.expiresAt || null
    }
  });
}
~~~

#### Code mẫu tạo cookie

~~~js
return {
  enabled: true,
  playbackUrl,
  expiresAt,
  cookies: {
    'CloudFront-Policy': toCloudFrontBase64(policy),
    'CloudFront-Signature': signPolicy(policy),
    'CloudFront-Key-Pair-Id': awsConfig.cloudFrontKeyPairId
  }
};
~~~

#### Code mẫu frontend player

Frontend chỉ gửi credentials khi đang dùng signed playback URL. Với Cloudflare Stream hoặc nguồn public khác, player không gửi credentials để tránh lỗi CORS.

~~~js
const useCredentialedPlayback = useMemo(
  () => shouldUseCredentialedPlayback(mediaUrl, signedPlaybackUrl),
  [mediaUrl, signedPlaybackUrl]
);

const hls = new Hls({
  xhrSetup: (xhr) => {
    xhr.withCredentials = useCredentialedPlayback;
  }
});
~~~
<!-- NETFLOP_DETAIL_END -->

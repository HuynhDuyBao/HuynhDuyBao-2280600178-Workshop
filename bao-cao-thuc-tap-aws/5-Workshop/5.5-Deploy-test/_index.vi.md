---
title: "Triển khai và kiểm thử ứng dụng"
date: 2026-07-10
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

Phần này mô tả quy trình deploy Netflop lên EC2 và kiểm thử các chức năng chính sau khi hệ thống chạy ở domain production. Các bước kiểm thử cần bao phủ cả người dùng cuối, admin upload video và monitoring.

<img width="1529" height="749" alt="cw2" src="https://github.com/user-attachments/assets/470b714f-b41e-41a9-9de3-171c1dac9650" />
<img width="1534" height="701" alt="cw1" src="https://github.com/user-attachments/assets/92619c98-7d82-4215-81df-2584c0bf3fce" />

#### Nội dung

1. [Deploy/reload bằng EC2 và Systems Manager](5.5.1-deploy-ssm/)
2. [Kiểm thử chức năng người dùng](5.5.2-user-test/)
3. [Kiểm thử admin upload video](5.5.3-admin-upload-video/)
4. [Kiểm tra monitoring và cảnh báo](5.5.4-monitoring-alerts/)

#### Checklist sau deploy

* `https://netflop.win` load được frontend.
* API `/api/movies`, `/api/catalog/genres`, `/api/auth/me` hoạt động.
* Đăng nhập/đăng ký local hoạt động.
* Trang xem phim phát được HLS.
* Phụ đề hiển thị đúng trên desktop và mobile.
* Admin upload video lên S3 và MediaConvert chạy tự động.
* CloudWatch không có alarm nghiêm trọng.

<!-- NETFLOP_DETAIL_START -->
#### Cách kiểm thử tổng thể sau deploy

Sau khi deploy, kiểm thử theo thứ tự:

1. Kiểm tra domain và frontend.
2. Kiểm tra backend API.
3. Kiểm tra RDS bằng API danh sách phim/thể loại.
4. Kiểm tra đăng nhập/đăng ký.
5. Kiểm tra trang xem phim và player HLS.
6. Kiểm tra admin upload video.
7. Kiểm tra CloudWatch alarm/log.

#### Lệnh kiểm tra nhanh

~~~bash
curl -I https://netflop.win
curl https://netflop.win/api/movies?limit=12
curl https://netflop.win/api/catalog/genres
pm2 status
sudo systemctl status nginx --no-pager
~~~
<!-- NETFLOP_DETAIL_END -->

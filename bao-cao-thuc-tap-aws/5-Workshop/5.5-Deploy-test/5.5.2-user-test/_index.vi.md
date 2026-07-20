---
title: "Kiểm thử chức năng người dùng"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

#### Mục tiêu

Kiểm thử các chức năng người dùng cuối của Netflop sau khi deploy lên production domain `netflop.win`.

#### Các nhóm chức năng cần kiểm thử

| Nhóm chức năng | Kết quả mong đợi |
| --- | --- |
| Trang chủ | Hiển thị banner, danh sách phim mới cập nhật, phim xem nhiều, phim bộ/phim lẻ |
| Tìm kiếm | Tìm phim theo tên hoặc diễn viên |
| Chi tiết phim | Hiển thị poster, banner, thông tin phim, đánh giá và danh sách tập |
| Xem phim | Player phát HLS, có tua, fullscreen, chọn phụ đề |
| Mobile responsive | Movie card kéo ngang được, player không mất nút, subtitle selector dễ bấm |
| Đăng nhập/đăng ký | Tạo tài khoản và đăng nhập local thành công |
| Tiếp tục xem | Lưu tiến độ theo từng tài khoản, tài khoản khác không bị lẫn dữ liệu |
| Lịch sử xem | Hiển thị phim đã xem đúng theo user |
| Yêu thích/đánh giá/bình luận | Dữ liệu được lưu vào RDS |
| Avatar | Người dùng đổi avatar, ảnh upload lên S3 và UI cập nhật |

#### Kiểm thử player trên mobile

Các điểm cần kiểm tra riêng:

* Nút play/pause bấm được bằng cảm ứng.
* Thanh tua không bị kẹt khi có thông báo tiếp tục xem.
* Nút phụ đề, cài đặt và fullscreen không bị tràn ra ngoài khung.
* Phụ đề không bị hiển thị trùng hai lớp.
* Khi chọn tiếp tục xem, video chạy từ thời điểm đã lưu.

#### Kết quả mong đợi

Người dùng có thể xem phim ổn định trên desktop và điện thoại, không gặp lỗi CORS/mixed content, không lộ raw stream URL trong thông báo lỗi, và dữ liệu cá nhân được tách theo từng tài khoản.

<img width="1534" height="821" alt="home" src="https://github.com/user-attachments/assets/21f28798-75be-4cc3-9bb5-ab89d6cc49c0" />
<img width="1529" height="792" alt="tieptucxem2" src="https://github.com/user-attachments/assets/438bd33e-9524-47bd-addc-e702fec5c654" />
<img width="1528" height="805" alt="tieptucxem" src="https://github.com/user-attachments/assets/e5ffc911-2f26-4051-9e91-87a84e5845b8" />
<img width="1534" height="786" alt="movierun" src="https://github.com/user-attachments/assets/6effc59c-5a37-45c3-8842-1bca9ed1209e" />
<img width="1512" height="820" alt="moviedetail" src="https://github.com/user-attachments/assets/23a6b9e3-61b6-4828-bf0d-af86406491a2" />


<!-- NETFLOP_DETAIL_START -->
#### Cách thực hiện chức năng tiếp tục xem

Frontend lưu tiến độ xem theo tài khoản bằng cách gọi API history trong khi người dùng xem video. Không lưu bằng localStorage cho chức năng này, vì localStorage sẽ bị lẫn giữa các tài khoản trên cùng trình duyệt.

#### Code mẫu frontend lưu tiến độ

~~~js
const persistWatchProgress = useCallback((progress, force = false) => {
  if (!user || !movie?.id) return;

  const watchedSeconds = Math.max(0, Math.floor(Number(progress?.currentTime || 0)));
  if (!force && watchedSeconds < 1) return;

  movieApi.saveHistory(movie.id, {
    episodeId: selectedEpisode?.id || null,
    watchedSeconds
  }).catch(() => {});
}, [movie?.id, selectedEpisode?.id, user]);
~~~

#### Code mẫu backend upsert lịch sử xem

~~~js
await pool.execute(
  `INSERT INTO lichsu (UserID, TenDN, MaPhim, MaTap, ThoiGianXem, ThoiGian)
   VALUES (:userId, :username, :movieId, :episodeId, :watchedSeconds, NOW())
   ON DUPLICATE KEY UPDATE
     MaTap = VALUES(MaTap),
     ThoiGianXem = VALUES(ThoiGianXem),
     ThoiGian = VALUES(ThoiGian)`,
  { userId: user.id, username: user.ten_dang_nhap, movieId, episodeId, watchedSeconds }
);
~~~

#### Kịch bản test

1. Đăng nhập tài khoản A, xem phim đến phút 1.
2. Thoát trang, quay lại trang chủ.
3. Kiểm tra mục Tiếp tục xem có phim đó.
4. Đăng xuất, đăng nhập tài khoản B.
5. Kiểm tra tài khoản B không thấy lịch sử của tài khoản A.
6. Bấm Tiếp tục xem ở tài khoản A và xác nhận player nhảy đúng thời điểm đã lưu.
<!-- NETFLOP_DETAIL_END -->

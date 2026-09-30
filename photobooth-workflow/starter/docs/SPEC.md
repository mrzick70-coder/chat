# Photobooth — Đặc tả (SPEC)

> Điền qua giai đoạn 1 của workflow. Mỗi user story có mã `US-xx` và tiêu chí chấp nhận
> kiểm chứng được — lệnh `/feature` dựa vào đây để viết test.

## 1. Bối cảnh
- Loại sự kiện:
- Số lượt khách ước tính / giờ:
- Có Internet tại sự kiện không:

## 2. Phần cứng
| Thiết bị   | Model | Kết nối | Ghi chú |
|------------|-------|---------|---------|
| Máy tính   |       |         |         |
| Màn hình   |       | cảm ứng?|         |
| Camera     |       |         |         |
| Máy in     |       |         | khổ giấy|

## 3. Luồng khách
IDLE → CHỌN LAYOUT → ĐẾM NGƯỢC → CHỤP (×N) → GHÉP KHUNG → XEM LẠI → IN / QR → CẢM ƠN → IDLE
(mọi màn hình có timeout về IDLE)

## 4. User stories

### US-01 — Màn hình chờ
**Là** khách, **tôi muốn** thấy màn hình hấp dẫn mời chạm, **để** biết cách bắt đầu.
Tiêu chí chấp nhận:
- [ ] AC-01.1 Hiển thị slideshow/video cấu hình được khi không có ai dùng
- [ ] AC-01.2 Chạm bất kỳ đâu chuyển sang CHỌN LAYOUT trong < 300 ms

### US-02 — …
<!-- Thêm story theo cùng mẫu -->

## 5. Màn hình admin
- Truy cập bằng:
- Chức năng:

## 6. Yêu cầu phi chức năng
- Thời gian từ bấm chụp đến ảnh preview:
- Chạy liên tục tối thiểu:
- Hoạt động offline:
- Lưu trữ ảnh gốc:

## 7. Ngoài phạm vi (phiên bản này)
-

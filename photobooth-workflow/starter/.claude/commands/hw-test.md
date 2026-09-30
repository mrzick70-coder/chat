---
description: Chuẩn bị script chẩn đoán và checklist thử tay cho một thiết bị phần cứng
argument-hint: <camera|printer> <model và cách kết nối>
---

Thiết bị cần tích hợp/kiểm tra: **$ARGUMENTS**

Bạn không truy cập được thiết bị thật; tôi sẽ chạy thử và gửi lại kết quả. Hãy:

1. Tìm hiểu cách thiết bị này làm việc với hệ điều hành của máy kiosk (driver, gphoto2,
   CUPS, SDK hãng) và những hạn chế đã biết (thời gian lấy nét, khổ giấy, cắt giấy,
   profile màu, số ảnh/phút).
2. Viết script chẩn đoán độc lập trong `scripts/hw/` (chạy được không cần mở app):
   phát hiện thiết bị, in thông tin, thao tác thử (chụp 1 ảnh / in 1 trang thử), đo thời
   gian từng bước, ghi log chi tiết ra file. Thoát với mã lỗi rõ ràng.
3. Kiểm tra provider tương ứng trong `src/` đã xử lý: mất kết nối và tự kết nối lại,
   timeout, lỗi hết giấy/kẹt giấy, thiết bị bận. Đề xuất (chưa sửa) các thay đổi cần thiết.
4. Tạo `docs/hw/<tên-thiết-bị>.md` gồm: cách cài đặt, cấu hình khuyến nghị, lệnh chạy
   script, checklist thử tay dạng `- [ ]`, và bảng "triệu chứng → nguyên nhân → cách xử lý".
5. Cho tôi biết chính xác lệnh cần chạy và output nào cần dán lại cho bạn.

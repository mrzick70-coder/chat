---
description: Báo một lỗi hoặc điều không như ý để Claude tìm nguyên nhân và sửa
argument-hint: mô tả điều bạn thấy (kèm ảnh chụp màn hình nếu có)
---

Người dùng báo có vấn đề: $ARGUMENTS

1. Nếu mô tả chưa đủ, hỏi lại **tối đa 2 câu** đơn giản: họ đã làm gì, mong thấy gì, lại thấy
   gì; xin ảnh chụp màn hình nếu hữu ích. Xem kỹ mọi ảnh họ gửi.
2. Tự tìm nguyên nhân: đọc code, đọc nhật ký lỗi, tự chạy thử bằng Chrome camera giả để tái
   hiện. Không bắt người dùng làm các bước kỹ thuật.
3. Giải thích nguyên nhân bằng **một câu đời thường** (ví dụ: "Trình duyệt chưa được phép dùng
   camera nên màn hình đen").
4. Sửa ở mức nhỏ nhất đủ để hết lỗi, không đổi thứ khác. Tự kiểm tra lại.
5. Kết thúc bằng **"Bạn thử thế này:"** và hỏi họ đã hết lỗi chưa. Chỉ lưu điểm khôi phục khi
   họ xác nhận.
6. Nếu lỗi nằm ở thiết bị hay cài đặt máy tính (máy in, webcam, Windows/Mac), hướng dẫn từng
   bước đánh số, nói rõ bấm vào đâu.

---
description: Quay lại một phiên bản cũ còn chạy tốt (điểm khôi phục)
---

Người dùng muốn quay lại phiên bản trước.

1. Liệt kê khoảng 10 điểm khôi phục gần nhất (git log) thành danh sách đánh số bằng tiếng
   Việt: thời gian dễ đọc (ví dụ "hôm qua 21:30") + nội dung.
2. Hỏi họ muốn quay về điểm nào. **Không làm gì trước khi họ chọn.**
3. Khi họ chọn: nếu có thay đổi chưa lưu, lưu lại trước thành một điểm tên
   "Bản nháp trước khi quay lại". Sau đó đưa các file về trạng thái của điểm đã chọn bằng
   cách tạo một commit mới (không dùng reset --hard), để vẫn có thể quay lại bản mới hơn.
4. Báo họ đã quay lại, và hướng dẫn **"Bạn thử thế này:"**.

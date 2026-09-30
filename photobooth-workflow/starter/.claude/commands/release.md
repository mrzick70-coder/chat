---
description: Kiểm tra toàn diện, đóng gói bản kiosk và tạo tag phát hành
argument-hint: <version, ví dụ 1.0.0>
---

Chuẩn bị phát hành phiên bản **$ARGUMENTS**.

1. Đảm bảo working tree sạch và đang ở nhánh chính mới nhất.
2. Chạy `npm run lint`, `npm run typecheck`, `npm run test`, `npm run test:e2e`. Dừng và báo
   tôi nếu có gì đỏ — không phát hành khi test lỗi.
3. Rà cấu hình kiosk và báo cáo từng mục đạt/chưa đạt:
   - Fullscreen/kiosk, chặn Alt+F4 / Cmd+Q / DevTools ở bản production
   - Ẩn con trỏ chuột, tắt menu chuột phải, chặn zoom/cuộn
   - Tự khởi động cùng hệ điều hành, tự khởi động lại khi crash
   - Chặn màn hình ngủ (`powerSaveBlocker`)
   - Lối thoát cho admin (cử chỉ bí mật + PIN)
   - Log ra file theo ngày, thư mục ảnh sự kiện đúng đường dẫn cấu hình
4. Cập nhật version trong `package.json` và thêm mục vào `CHANGELOG.md` từ các commit kể từ
   tag trước.
5. Chạy `npm run build`, liệt kê file đầu ra và kích thước.
6. Commit `chore(release): v$ARGUMENTS` và tạo tag `v$ARGUMENTS`. Không push — hỏi tôi trước.
7. In checklist thử tại chỗ trước sự kiện (lấy từ `docs/hw/*.md`).

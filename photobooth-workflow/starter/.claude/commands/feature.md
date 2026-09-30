---
description: Làm một user story từ docs/SPEC.md theo vòng lặp plan → test → code → kiểm tra → commit
argument-hint: <US-id> <mô tả ngắn>
---

Làm tính năng: **$ARGUMENTS**

Thực hiện đúng thứ tự, không bỏ bước:

1. **Hiểu yêu cầu.** Đọc user story tương ứng trong `docs/SPEC.md`, `docs/ARCHITECTURE.md`
   và ADR liên quan. Nếu story chưa có trong SPEC hoặc tiêu chí chấp nhận mơ hồ, hỏi tôi
   trước khi tiếp tục.
2. **Kế hoạch.** Tạo nhánh `feat/<US-id>-<slug>`. Trình bày kế hoạch ngắn: file sẽ sửa/tạo,
   thay đổi state machine/IPC (nếu có), test sẽ viết, rủi ro. **Dừng lại chờ tôi duyệt.**
3. **Test trước.** Viết test từ từng tiêu chí chấp nhận (Vitest cho logic, Playwright cho
   luồng UI, dùng Mock provider). Chạy để xác nhận test đỏ vì đúng lý do.
4. **Code.** Cài đặt tối thiểu để test xanh, tuân thủ quy tắc trong `CLAUDE.md`.
5. **Kiểm tra.** Chạy `npm run lint`, `npm run typecheck`, `npm run test`, `npm run test:e2e`.
   Sửa cho đến khi tất cả xanh. Nếu có Playwright MCP, mở app, đi qua luồng vừa làm và
   chụp màn hình để tự kiểm tra giao diện kiosk (chữ to, nút lớn, không tràn).
6. **Tài liệu.** Cập nhật `docs/ARCHITECTURE.md` nếu kiến trúc thay đổi; đánh dấu story
   hoàn thành trong `docs/SPEC.md`.
7. **Commit** với message `feat(<US-id>): <mô tả>` và tóm tắt cho tôi: đã làm gì, test nào,
   còn gì chưa làm, cần tôi thử tay phần nào (đặc biệt phần cứng thật).

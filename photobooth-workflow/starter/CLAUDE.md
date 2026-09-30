# Photobooth — bối cảnh cho Claude

Phần mềm photobooth chạy kiosk tại sự kiện: khách chạm màn hình → đếm ngược → chụp
nhiều ảnh → ghép khung → in và/hoặc lấy ảnh qua QR.

## Tài liệu nguồn (đọc trước khi làm việc lớn)
- `docs/SPEC.md` — user story (US-xx) và tiêu chí chấp nhận. Đây là nguồn sự thật về hành vi.
- `docs/ARCHITECTURE.md` — module, luồng dữ liệu, IPC.
- `docs/adr/` — các quyết định kiến trúc đã chốt. Không làm trái ADR mà không hỏi.
- `docs/hw/` — ghi chú và checklist từng thiết bị phần cứng.

## Công nghệ
Electron + React + TypeScript + Vite · XState · sharp · Vitest · Playwright · electron-builder

## Lệnh thường dùng
<!-- Cập nhật sau khi dựng khung dự án (giai đoạn 3) -->
- `npm run dev` — chạy app ở chế độ phát triển (camera/máy in giả nếu `PB_MOCK=1`)
- `npm run lint` · `npm run typecheck` · `npm run test` · `npm run test:e2e`
- `npm run build` — đóng gói bằng electron-builder

## Quy tắc
- Mọi truy cập phần cứng đi qua `CameraProvider` / `PrinterProvider`. Không gọi
  getUserMedia, gphoto2 hay lệnh in trực tiếp từ component UI.
- Luôn giữ bản Mock của mỗi provider chạy được; test và E2E dùng mock.
- Luồng màn hình chỉ thay đổi qua state machine; mọi state khách phải có timeout về IDLE.
- Compositor là hàm thuần (ảnh + template → buffer), có test snapshot.
- Renderer không có quyền Node; mọi thứ qua IPC có kiểu trong `src/shared/ipc.ts`.
- Không bao giờ mất ảnh của khách: lưu ảnh gốc xuống đĩa ngay sau khi chụp, trước khi xử lý.
- UI kiosk: nút tối thiểu 80px, chữ to, không cần bàn phím, không hộp thoại hệ thống.
- Chuỗi hiển thị cho khách đặt trong file i18n (mặc định tiếng Việt), không hard-code.
- Trước khi báo xong: chạy lint, typecheck, test; sửa đến khi xanh.
- Commit nhỏ, message dạng `feat(US-03): ...`, `fix: ...`.

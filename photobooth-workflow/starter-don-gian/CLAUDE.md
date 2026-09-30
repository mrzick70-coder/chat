# Photobooth — lời dặn cho Claude

## Người bạn đang làm việc cùng
Chủ dự án **không biết lập trình và không rành kỹ thuật**. Họ là người quyết định
phần mềm trông thế nào và hoạt động ra sao; bạn lo toàn bộ phần kỹ thuật.

Cách giao tiếp:
- Luôn trả lời bằng **tiếng Việt đời thường**, câu ngắn. Tránh thuật ngữ; nếu buộc phải dùng
  thì giải thích ngay trong ngoặc bằng một ví dụ đời thường.
- Không bắt họ đọc code, mở terminal hay gõ lệnh. Nếu họ phải làm gì bằng tay (cài máy in,
  đổi cài đặt Windows/Mac), hướng dẫn **từng bước đánh số**, nói rõ bấm vào đâu, tên nút là gì.
- Sau mỗi thay đổi, luôn kết thúc bằng mục **"Bạn thử thế này:"** — các bước cụ thể để
  họ tự kiểm tra, và điều họ nên thấy nếu đúng.
- Khi có nhiều lựa chọn, đưa tối đa 2–3 phương án, nói ưu/nhược bằng lời thường và
  **đề xuất một phương án**. Đừng hỏi những câu kỹ thuật mà bạn tự quyết được.
- Mỗi lần chỉ làm một việc nhỏ, thấy được kết quả ngay. Không tự ý làm thêm tính năng họ chưa xin.
- Khi họ gửi ảnh chụp màn hình, xem kỹ ảnh trước khi trả lời.

## Bản mô tả sản phẩm
`MO-TA.md` là bản mô tả họ đã duyệt: tính năng, màu sắc, chữ, thiết bị. Đọc nó ở đầu mỗi
cuộc trò chuyện. Khi họ đổi ý, cập nhật file này và cho họ biết. Cuối file có mục
**"Tiến độ"** — đánh dấu việc đã xong / đang làm / sắp làm.
Nếu `MO-TA.md` chưa tồn tại: phỏng vấn họ từng câu một rồi tạo nó trước khi viết code.

## Ràng buộc kỹ thuật (bạn tự lo, không cần giải thích với họ)
- Ứng dụng web thuần: HTML + CSS + JavaScript, **không có bước build, không cần cài Node,
  Python hay bất cứ thứ gì** ngoài Google Chrome. Thư viện bên ngoài (nếu cần) tải về và
  để trong thư mục `thu-vien/`, không dùng CDN (sự kiện có thể không có Internet).
- Chạy bằng cách **bấm đúp** file khởi động: `CHAY-PHOTOBOOTH.bat` (Windows) và
  `CHAY-PHOTOBOOTH.command` (Mac, nhớ `chmod +x`). File này mở Chrome ở chế độ kiosk với
  hồ sơ Chrome riêng và các cờ cần thiết, ví dụ `--kiosk`, `--kiosk-printing` (in thẳng
  máy in mặc định), cấp quyền camera tự động, cho phép đọc ảnh cục bộ để canvas không bị
  "tainted" khi chạy từ `file://`. Tự kiểm chứng các cờ này hoạt động, đừng đoán.
- Thêm file `CHAY-THU-CUA-SO.*` mở ở chế độ cửa sổ thường để họ thử và thoát dễ dàng.
- Mọi cài đặt họ có thể muốn đổi (chữ trên khung, số ảnh, thời gian đếm ngược, màu) nằm
  trong **một** file `cai-dat.js` có chú thích tiếng Việt, và/hoặc trang cài đặt có mật khẩu.
- Ảnh khung, logo, âm thanh của họ đặt trong thư mục `hinh/`.
- Không bao giờ để mất ảnh của khách: lưu ảnh ngay sau khi chụp; lỗi in không được làm mất ảnh.
- Mọi màn hình của khách tự quay về màn hình chờ nếu không có ai chạm một lúc.
- Giao diện cho khách: chữ rất to, nút rất lớn, dùng được hoàn toàn bằng cảm ứng/chuột,
  không cần bàn phím, không hiện hộp thoại của trình duyệt.
- Khi gặp lỗi, khách chỉ thấy thông báo thân thiện ("Máy in đang bận, ảnh của bạn đã được lưu 💛");
  chi tiết kỹ thuật ghi vào nhật ký để bạn đọc sau.
- Có thể tự kiểm tra bằng cách mở trang trong Chrome không giao diện với camera giả
  (`--use-fake-device-for-media-stream --use-fake-ui-for-media-stream`) và chụp màn hình.
  Làm điều này trước khi bảo họ thử.

## Lưu tiến độ ("điểm khôi phục")
- Dùng git. Nếu thư mục chưa có git, tự khởi tạo (không cần hỏi) và nói với họ:
  "Tôi đã bật tính năng lưu điểm khôi phục."
- Sau mỗi bước **họ xác nhận chạy tốt**, tạo commit với message tiếng Việt dễ hiểu, ví dụ
  `Thêm đếm ngược 3-2-1 có tiếng bíp`. Báo họ: "Đã lưu điểm khôi phục: …".
- Không bao giờ dùng lệnh xoá lịch sử (reset --hard, push --force…). Quay lại phiên bản cũ
  bằng cách tạo commit mới (revert/checkout file), để luôn còn đường quay lại.

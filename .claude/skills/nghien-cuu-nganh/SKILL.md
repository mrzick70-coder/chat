---
name: nghien-cuu-nganh
description: Quy trình chính để tìm hiểu, đánh giá hoặc so sánh ngành nghề để đầu tư và viết báo cáo. Dùng khi người dùng nói "nghiên cứu ngành…", "có nên đầu tư vào…", "tìm ngành để đầu tư", "so sánh ngành A và B".
---

# Nghiên cứu ngành để đầu tư

Bạn là người điều phối. Bạn không tự đi tìm dữ liệu chi tiết; việc đó giao cho sub agent. Việc của bạn: xác định phạm vi, giao việc, kiểm tra chất lượng, chấm điểm và viết báo cáo.

## Bước 0: Hồ sơ

- Đọc hồ sơ trong `CLAUDE.md`. Nếu còn trống vốn, hình thức hoặc thời gian nắm giữ → chạy skill `ho-so-dau-tu` trước.

## Bước 1: Chọn ngành

- **Người dùng đã nêu ngành:** chốt phạm vi cụ thể (ví dụ "cà phê" → chuỗi cà phê mang đi tại TP.HCM, hay xuất khẩu cà phê nhân?). Nếu phạm vi mơ hồ, hỏi một câu với 2–4 lựa chọn.
- **Chưa có ngành:** gọi agent `trinh-sat-nganh`, truyền nguyên hồ sơ nhà đầu tư. Đưa danh sách rút gọn cho người dùng chọn 1–2 ngành.
- Tạo `research/<slug>/00-pham-vi.md` gồm: hồ sơ nhà đầu tư, ngành, phạm vi (phân khúc, địa lý, chuỗi giá trị), câu hỏi chính cần trả lời, ngày bắt đầu.

## Bước 2: Nghiên cứu song song

Gọi **cùng lúc, trong một lượt** 5 agent:

| Agent | File kết quả |
|---|---|
| `quy-mo-thi-truong` | `01-quy-mo-thi-truong.md` |
| `canh-tranh` | `02-canh-tranh.md` |
| `phap-ly-chinh-sach` | `03-phap-ly-chinh-sach.md` |
| `tai-chinh-nganh` | `04-tai-chinh-nganh.md` |
| `xu-huong-rui-ro` | `05-xu-huong-rui-ro.md` |

Prompt cho mỗi agent phải tự đủ thông tin, gồm:
- Tên ngành và phạm vi (lấy từ `00-pham-vi.md`).
- Hồ sơ nhà đầu tư, đặc biệt là hình thức đầu tư và vốn.
- Đường dẫn file kết quả đầy đủ: `research/<slug>/0X-....md`.
- Nhắc: tuân theo quy tắc nghiên cứu trong `CLAUDE.md`.

## Bước 3: Phản biện

- Gọi agent `phan-bien` với đường dẫn thư mục `research/<slug>/`.
- Nếu `06-phan-bien.md` có mục "Lỗ hổng nghiêm trọng": gọi lại **đúng agent liên quan** một lần, kèm danh sách lỗ hổng cần bổ sung. Tối đa **một vòng** bổ sung; lỗ hổng còn lại ghi vào báo cáo như rủi ro dữ liệu.

## Bước 4: Chấm điểm

- Áp dụng skill `khung-danh-gia`, ghi kết quả vào `research/<slug>/07-cham-diem.md`.

## Bước 5: Báo cáo

- Viết `research/<slug>/bao-cao.md` theo skill `mau-bao-cao`.
- Trả lời người dùng trong chat bằng: kết luận 1 câu, điểm tổng, 3 điểm cộng, 3 điểm trừ, đường dẫn báo cáo. Không dán toàn bộ báo cáo vào chat.

## So sánh nhiều ngành

- Chạy Bước 1–4 cho từng ngành (có thể chạy song song các nhóm agent nếu tối đa 2 ngành; từ 3 ngành trở lên thì chạy lần lượt để tránh quá tải).
- Viết thêm `research/so-sanh-<slug1>-vs-<slug2>.md`: bảng điểm cạnh nhau theo cùng khung đánh giá, khác biệt chính, ngành nào hợp với hồ sơ hơn và vì sao.

## Nguyên tắc tiết kiệm ngữ cảnh

- Agent ghi chi tiết vào file và chỉ trả về tóm tắt ngắn; bạn chỉ mở file khi cần chấm điểm hoặc viết báo cáo.
- Không gọi thêm agent ngoài danh sách trên trừ khi người dùng yêu cầu.

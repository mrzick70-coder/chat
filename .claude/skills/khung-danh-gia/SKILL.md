---
name: khung-danh-gia
description: Khung chấm điểm thống nhất để đánh giá mức hấp dẫn của một ngành với một nhà đầu tư cụ thể. Dùng ở bước chấm điểm của nghien-cuu-nganh, khi sàng lọc ngành, hoặc khi so sánh nhiều ngành.
---

# Khung đánh giá ngành

Chấm mỗi tiêu chí từ 1 đến 5 dựa trên các file `01`–`06` trong `research/<slug>/`. Mỗi điểm phải kèm 1–2 câu lý do và dẫn về file/nguồn.

## Tiêu chí và trọng số

| # | Tiêu chí | Trọng số | 1 điểm | 3 điểm | 5 điểm |
|---|---|---|---|---|---|
| 1 | Quy mô và tăng trưởng thị trường | 20% | Thu hẹp hoặc đi ngang | Tăng 5–10%/năm | Tăng trên 15%/năm, quy mô đủ lớn |
| 2 | Cấu trúc cạnh tranh | 15% | Cạnh tranh về giá khốc liệt, không có rào cản | Cạnh tranh vừa, có vài ngách | Ít đối thủ mạnh, có rào cản và lợi thế bền vững |
| 3 | Kinh tế đơn vị và lợi nhuận | 20% | Biên lợi nhuận mỏng, hoàn vốn trên 7 năm | Biên trung bình, hoàn vốn 3–5 năm | Biên cao, hoàn vốn dưới 2–3 năm |
| 4 | Pháp lý và chính sách | 10% | Điều kiện khắt khe, chính sách bất lợi hoặc thay đổi liên tục | Có điều kiện nhưng rõ ràng | Thủ tục đơn giản, có ưu đãi |
| 5 | Rủi ro và độ bất định (điểm cao = rủi ro thấp) | 15% | Nhiều rủi ro lớn khó kiểm soát | Rủi ro vừa, có cách giảm thiểu | Rủi ro thấp, dễ dự báo |
| 6 | Mức phù hợp với nhà đầu tư | 20% | Vượt vốn, trái khẩu vị rủi ro, không có lợi thế | Phù hợp một phần | Khớp vốn, thời gian, kỹ năng và lợi thế sẵn có |

**Điều chỉnh theo hình thức đầu tư:**
- *Cổ phiếu/quỹ:* tiêu chí 3 xét biên lợi nhuận và ROE của doanh nghiệp niêm yết, cộng thêm mức định giá ngành (P/E, P/B so với lịch sử). Tiêu chí 6 xét thêm thanh khoản và số lượng mã niêm yết đáng đầu tư.
- *Tự kinh doanh/nhượng quyền/góp vốn:* tiêu chí 3 xét vốn ban đầu, điểm hoà vốn và thời gian hoàn vốn của một mô hình cỡ vốn của nhà đầu tư.

## Điểm tổng

`Điểm tổng = Σ (điểm × trọng số)`, làm tròn 1 chữ số thập phân.

| Điểm tổng | Kết luận |
|---|---|
| ≥ 4.0 | Hấp dẫn, đáng đi tiếp bước kiểm chứng thực tế |
| 3.0–3.9 | Cân nhắc, chỉ nên vào nếu giải quyết được các điểm yếu chính |
| < 3.0 | Không ưu tiên |

## Điều kiện loại trực tiếp

Kết luận là **Không ưu tiên** bất kể điểm tổng nếu có một trong các điều sau:
- Vốn tối thiểu để tham gia vượt quá vốn của nhà đầu tư và không có hình thức nhỏ hơn khả thi.
- Pháp luật cấm hoặc hạn chế nhà đầu tư này tham gia (ví dụ giới hạn sở hữu nước ngoài).
- Kịch bản xấu gây lỗ vượt mức lỗ tối đa chịu được và không có cách giảm thiểu.

## Độ tin cậy

- Ghi độ tin cậy dữ liệu cho mỗi tiêu chí (Cao/Trung bình/Thấp), lấy từ đánh giá trong `06-phan-bien.md`.
- Nếu từ 2 tiêu chí trở lên có độ tin cậy Thấp, ghi rõ trong kết luận: "Điểm mang tính tạm thời, cần thêm dữ liệu".

## Định dạng `07-cham-diem.md`

```markdown
| Tiêu chí | Trọng số | Điểm | Độ tin cậy | Lý do (nguồn) |
|---|---|---|---|---|
...
**Điểm tổng:** x.x / 5 → <Kết luận>
**Điều kiện loại trực tiếp:** Không có / <mô tả>
```

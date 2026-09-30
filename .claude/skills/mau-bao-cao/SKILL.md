---
name: mau-bao-cao
description: Mẫu báo cáo đầu tư ngành cuối cùng. Dùng ở bước viết báo cáo của nghien-cuu-nganh, sau khi đã có các file 01–07 trong research/<slug>/.
---

# Mẫu báo cáo đầu tư ngành

Viết vào `research/<slug>/bao-cao.md`. Viết cho người không chuyên: câu ngắn, giải thích thuật ngữ lần đầu xuất hiện, ưu tiên bảng và gạch đầu dòng. Độ dài mục tiêu 2.500–4.000 từ. Giữ nguyên các trích nguồn `[Nguồn, năm]` từ file của agent.

## Cấu trúc

```markdown
# Báo cáo ngành: <Tên ngành> (<phạm vi>)
_Ngày: <YYYY-MM-DD> · Dành cho: <tóm tắt hồ sơ 1 dòng>_

## Tóm tắt (đọc 2 phút)
- **Kết luận:** <Hấp dẫn / Cân nhắc / Không ưu tiên> — điểm x.x/5
- **Một câu:** <vì sao>
- **3 lý do nên:** …
- **3 lý do không nên:** …
- **Cách tham gia phù hợp nhất với bạn:** …

## 1. Hồ sơ và phạm vi
## 2. Tổng quan ngành và chuỗi giá trị
   (ngành làm gì, tiền chảy từ đâu đến đâu, khâu nào lời nhất)
## 3. Quy mô và tăng trưởng
## 4. Cạnh tranh
## 5. Pháp lý và chính sách
## 6. Tài chính và kinh tế đơn vị
## 7. Xu hướng và rủi ro
   (kèm ma trận rủi ro: xác suất × tác động)
## 8. Điểm yếu của dữ liệu
   (tóm tắt từ phản biện: số liệu nào còn yếu, nhận định nào chưa chắc)
## 9. Chấm điểm
   (chép bảng từ 07-cham-diem.md)
## 10. Ba kịch bản
| | Xấu | Cơ sở | Tốt |
|---|---|---|---|
| Giả định chính | | | |
| Kết quả với số vốn của bạn | | | |
| Xác suất ước tính | | | |

## 11. Các cách tham gia ngành
   (cổ phiếu/ETF, tự mở, nhượng quyền, góp vốn, làm nhà cung cấp cho ngành…;
    so sánh vốn cần, rủi ro, công sức; đánh dấu cách hợp với hồ sơ nhất)
## 12. 5 việc cần kiểm chứng tiếp theo
   (việc cụ thể ngoài đời thực: gặp ai, hỏi câu gì, xem số liệu gì,
    đi khảo sát ở đâu; mỗi việc trả lời được nghi vấn nào trong báo cáo)
## 13. Dấu hiệu cảnh báo sớm
   (các chỉ báo nên theo dõi định kỳ; nếu xảy ra thì cần xem lại quyết định)

## Nguồn tham khảo
   (danh sách đầy đủ, nhóm theo loại nguồn)

---
_Báo cáo do AI tổng hợp từ nguồn công khai, chỉ để tham khảo, không phải lời khuyên đầu tư.
Hãy kiểm chứng các con số quan trọng và tham khảo chuyên gia trước khi quyết định._
```

## Kiểm tra trước khi giao

- [ ] Mọi con số trong phần Tóm tắt đều có nguồn ở các mục bên dưới.
- [ ] Kết luận khớp với điểm tổng và điều kiện loại trực tiếp trong `07-cham-diem.md`.
- [ ] Kịch bản xấu được tính bằng số vốn thật của nhà đầu tư, so với mức lỗ tối đa chịu được.
- [ ] Mục 12 là việc làm được ngay, không phải lời khuyên chung chung.

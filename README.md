# Workflow nghiên cứu ngành để đầu tư (Claude Code)

Bộ skill và sub agent giúp Claude Code tìm hiểu thị trường một ngành và viết báo cáo đầu tư bằng tiếng Việt.

## Cách dùng

Mở repo bằng Claude Code rồi nói, ví dụ:

- `Tìm giúp tôi ngành để đầu tư` → sàng lọc 3–5 ngành hợp với hồ sơ của bạn.
- `Nghiên cứu ngành chuỗi cà phê mang đi tại TP.HCM` → báo cáo đầy đủ.
- `So sánh ngành spa và ngành phòng gym` → hai báo cáo và một bảng so sánh.

Lần đầu, Claude sẽ hỏi vài câu để hoàn thiện hồ sơ nhà đầu tư trong `CLAUDE.md`.

## Quy trình

```
ho-so-dau-tu ─► trinh-sat-nganh (nếu chưa có ngành)
             ─► 5 agent chạy song song:
                  quy-mo-thi-truong · canh-tranh · phap-ly-chinh-sach
                  tai-chinh-nganh · xu-huong-rui-ro
             ─► phan-bien (kiểm chứng, tối đa 1 vòng bổ sung)
             ─► khung-danh-gia (chấm điểm)
             ─► mau-bao-cao ─► research/<ngành>/bao-cao.md
```

## Thành phần

| Loại | Tên | Vai trò |
|---|---|---|
| Skill | `nghien-cuu-nganh` | Quy trình điều phối chính |
| Skill | `ho-so-dau-tu` | Thu thập hồ sơ nhà đầu tư |
| Skill | `khung-danh-gia` | Thang điểm 6 tiêu chí có trọng số, điều kiện loại trực tiếp |
| Skill | `mau-bao-cao` | Mẫu báo cáo cuối |
| Agent | `trinh-sat-nganh` | Sàng lọc ngành |
| Agent | `quy-mo-thi-truong` | TAM/SAM/SOM, tăng trưởng |
| Agent | `canh-tranh` | Đối thủ, 5 áp lực Porter, rào cản |
| Agent | `phap-ly-chinh-sach` | Giấy phép, thuế, chính sách |
| Agent | `tai-chinh-nganh` | Biên lợi nhuận, vốn, hoà vốn, hoàn vốn |
| Agent | `xu-huong-rui-ro` | Xu hướng, chu kỳ, ma trận rủi ro |
| Agent | `phan-bien` | Kiểm chứng số liệu, lập luận phía bi quan |

Hồ sơ nhà đầu tư, quy tắc trích nguồn và danh sách nguồn ưu tiên nằm trong `CLAUDE.md`.

> Báo cáo do AI tổng hợp chỉ để tham khảo, không phải lời khuyên đầu tư.

# Hướng dẫn dùng bộ công cụ dự án photobooth

## Có gì trong repo

| Thành phần | Loại | Việc |
|---|---|---|
| `.claude/skills/photobooth-du-an/` | Skill **điều phối** | Điểm bắt đầu. Chạy toàn bộ quy trình và dừng ở 2 mốc để bạn duyệt |
| `.claude/skills/photobooth-checklist/` | Skill kiến thức | Checklist hạng mục, tỷ lệ chia ngân sách, các bẫy chi phí |
| `.claude/skills/du-toan-ngan-sach/` | Skill + script | Script tính tổng, tự chọn mức giá, xuất Excel. Kèm **bảng giá đã khảo** (21 hạng mục, khu vực Bắc Ninh/HN, 30/09/2026) |
| `.claude/agents/khao-gia.md` | **Sub agent** | Tra giá trên web, chỉ chạy khi thiếu giá hoặc giá cũ, ghi thẳng vào bảng giá |
| Skill `interior-design-expert` | Có sẵn trong tài khoản | Kiến thức thiết kế nội thất (bố cục, màu, ánh sáng) |

Quy trình:

```
/photobooth-du-an
  → hỏi đầu vào → chọn hạng mục (checklist) → thiết kế (interior-design-expert)
  → [BẠN DUYỆT concept]
  → hang-muc.json → du_toan.py ──thiếu giá──► sub agent khao-gia → chạy lại
                               ──vượt──► đề xuất cắt/thay (tối đa 2 vòng)
                               ──đạt──► [BẠN DUYỆT dự toán] → du-an/<ten>/du-toan.xlsx
```

## Cách dùng ở phiên mới

1. Mở phiên Claude Code mới **trên repo này**. Nếu làm trên Claude Code web, hãy chọn nhánh chứa bộ công cụ, hoặc merge nhánh đó vào `main` trước.
2. Gõ:
   ```
   /photobooth-du-an
   ```
   rồi dán thông tin dự án và đính kèm ảnh tham khảo, ví dụ:
   > Mặt bằng thô 3×6m quây vách ngăn trong mặt bằng lớn, Hiệp Hòa – Bắc Ninh. Ngân sách cải tạo 50tr, chưa gồm thiết bị chụp. Phong cách warm minimal, ảnh đính kèm.
3. Duyệt concept khi Claude hỏi, sau đó duyệt dự toán.
4. Kết quả nằm trong `du-an/<ten>/`: `thiet-ke.md`, `hang-muc.json`, `du-toan.xlsx`.
5. Mở `du-toan.xlsx` và đổi cột **Mức chọn** (TK/CB/NB/KHONG) để tự thử các phương án. Tổng tiền tự tính lại, không tốn token.

## Vì sao setup này tiết kiệm token
- **Phép cộng do script làm**, không để AI cộng. Việc chọn mức giá cho vừa ngân sách cũng do script làm, nên không cần vòng lặp giữa agent thiết kế và agent khảo giá.
- **Bảng giá được lưu lại**: dự án sau dùng lại giá cũ, chỉ khảo những mã còn thiếu hoặc giá đã quá 120 ngày.
- **Chỉ có 1 sub agent**, và sub agent chỉ nhận danh sách mã cần tra, không nhận cả dự án. Kết quả tìm kiếm web dài dòng nằm lại trong sub agent.
- **Thiết kế và hạng mục chạy trong agent chính** vì cần toàn bộ bối cảnh; tách ra sub agent thì lại phải đọc lại từ đầu.
- **Vòng cắt giảm có giới hạn**: tối đa 2 vòng, sau đó bạn quyết.

## Tùy chỉnh
- **Model của sub agent**: trong `.claude/agents/khao-gia.md`, dòng `model: sonnet`. Có thể đổi sang `haiku` để rẻ hơn, đổi lại kết quả tra giá kém kỹ hơn.
- **Hạn giá cũ**: biến `HAN_GIA_NGAY` trong `scripts/du_toan.py`.
- **Dùng cho dự án khác** (quán cà phê, tiệm nail…): skill `du-toan-ngan-sach` và agent `khao-gia` dùng chung được. Chỉ cần viết thêm một skill checklist cho loại hình đó.
- **Muốn dùng ở repo khác**: xem mục "Dùng cho repo khác" bên dưới.

## Dùng cho repo khác

Bảng giá dùng thật nằm trong thư mục dự án (`du-an/bang-gia.csv`), không nằm trong skill. Lần đầu chạy, script tự tạo file này từ `bang-gia-mau.csv`. Nhờ vậy mỗi repo có bảng giá riêng, và bộ công cụ chạy được ở bất kỳ đâu.

| Cách | Làm gì | Hợp với |
|---|---|---|
| 1. Cài cho cá nhân | `cp -r .claude/skills/* ~/.claude/skills/` và `cp .claude/agents/*.md ~/.claude/agents/` | Claude Code **trên máy**: một lần cài, mọi repo trên máy đều dùng được |
| 2. Chép vào repo | Chép thư mục `.claude/skills/` và `.claude/agents/` sang repo mới rồi commit | Claude Code **trên web** (mỗi phiên là máy mới, không có `~/.claude`), hoặc khi cần chia sẻ cho người khác cùng repo |
| 3. Đóng gói plugin | Đưa bộ công cụ thành một plugin trong một repo riêng, các repo khác chỉ cần khai báo để cài | Dùng ở **nhiều repo** mà muốn sửa một chỗ là tất cả cùng cập nhật |

## Lưu ý từ lần khảo giá đầu (mặt bằng 3×6m, 50tr)
Nếu làm **đủ mọi hạng mục ở mức rẻ nhất**, tổng vẫn khoảng **60tr** (gồm 10% dự phòng). Ba khoản lớn nhất là vách ngăn cùng cửa (~9,7tr), điều hòa (7,5tr) và điện (5,5tr). Muốn vừa 50tr phải cắt phạm vi: thay cửa bằng rèm, bỏ ghế lười, bỏ quầy, và chỉ cán nền khi thật cần. File `mau-hang-muc.json` đã đặt sẵn các mục này là tùy chọn. Chạy thử với file mẫu cho kết quả ~49,9tr, ĐẠT.

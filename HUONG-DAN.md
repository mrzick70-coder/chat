# Hướng dẫn dùng bộ công cụ dự án photobooth

## Có gì trong repo

Repo này là một **plugin marketplace** tên `photobooth-tools`, chứa plugin `photobooth`:

| Thành phần | Loại | Việc |
|---|---|---|
| `plugins/photobooth/skills/photobooth-du-an/` | Skill **điều phối** | Điểm bắt đầu. Chạy toàn bộ quy trình, dừng ở 2 mốc để bạn duyệt |
| `plugins/photobooth/skills/photobooth-checklist/` | Skill kiến thức | Checklist hạng mục, tỷ lệ chia ngân sách, các bẫy chi phí |
| `plugins/photobooth/skills/du-toan-ngan-sach/` | Skill + script | Script tính tổng, tự chọn mức giá, xuất Excel. Kèm bảng giá mẫu (21 hạng mục, Bắc Ninh/HN, 30/09/2026) |
| `plugins/photobooth/agents/khao-gia.md` | **Sub agent** | Tra giá trên web, chỉ chạy khi thiếu giá hoặc giá cũ, ghi vào `du-an/bang-gia.csv` |
| Skill `interior-design-expert` | Có sẵn trong tài khoản | Kiến thức thiết kế nội thất |

Quy trình:

```
/photobooth:photobooth-du-an
  → hỏi đầu vào → chọn hạng mục (checklist) → thiết kế (interior-design-expert)
  → [BẠN DUYỆT concept]
  → hang-muc.json → du_toan.py ──thiếu giá──► sub agent khao-gia → chạy lại
                               ──vượt──► đề xuất cắt/thay (tối đa 2 vòng)
                               ──đạt──► [BẠN DUYỆT dự toán] → du-an/<ten>/du-toan.xlsx
```

## Cài vào repo bất kỳ (1 bước)

Tạo file **`.claude/settings.json`** trong repo muốn dùng, dán nội dung sau vào, rồi commit (nếu repo đã có file này thì thêm hai khóa bên dưới vào):

```json
{
  "extraKnownMarketplaces": {
    "photobooth-tools": {
      "source": {
        "source": "git",
        "url": "https://github.com/mrzick70-coder/chat.git",
        "ref": "claude/laughing-albattani-6iszfl"
      }
    }
  },
  "enabledPlugins": {
    "photobooth@photobooth-tools": true
  }
}
```

Lần sau mở Claude Code trong repo đó (trên máy hay trên web đều được), plugin tự được cài. Nếu Claude Code hỏi có tin tưởng marketplace/plugin không, chọn đồng ý. Để kiểm tra, gõ `/plugin` sẽ thấy `photobooth` đang bật.

> Dòng `"ref"` trỏ vào nhánh hiện tại. Khi đã merge nhánh này vào `main`, hãy **xóa dòng `"ref"`** (và dấu phẩy ở dòng trước) để luôn lấy bản mới nhất trên `main`.

**Cách khác, cài cho cá nhân trên máy** (mọi repo đều dùng được, không cần file settings):
```
/plugin marketplace add https://github.com/mrzick70-coder/chat.git#claude/laughing-albattani-6iszfl
/plugin install photobooth@photobooth-tools
```

## Cách dùng

1. Trong repo đã cài, gõ:
   ```
   /photobooth:photobooth-du-an
   ```
   (chỉ cần gõ `/photobooth-du-an` rồi chọn trong gợi ý). Sau đó dán thông tin dự án và đính kèm ảnh tham khảo.
2. Duyệt concept, rồi duyệt dự toán.
3. Kết quả nằm trong `du-an/<ten>/`: `thiet-ke.md`, `hang-muc.json`, `du-toan.xlsx`. Bảng giá của repo nằm ở `du-an/bang-gia.csv`.
4. Trong `du-toan.xlsx`, đổi cột **Mức chọn** (TK/CB/NB/KHONG) để tự thử phương án; tổng tự tính lại, không tốn token.

## Cập nhật plugin
Sửa file trong `plugins/photobooth/` ở repo này, tăng `version` trong `plugins/photobooth/.claude-plugin/plugin.json`, rồi push. Ở các repo khác, gõ `/plugin`, chọn marketplace `photobooth-tools` rồi cập nhật (hoặc chạy `claude plugin marketplace update photobooth-tools`).

## Vì sao setup này tiết kiệm token
- **Phép cộng do script làm**, không để AI cộng. Việc chọn mức giá cho vừa ngân sách cũng do script làm, nên không cần vòng lặp giữa agent thiết kế và agent khảo giá.
- **Bảng giá được lưu lại**: dự án sau dùng lại giá cũ, chỉ khảo những mã còn thiếu hoặc giá đã quá 120 ngày.
- **Chỉ có 1 sub agent**, và sub agent chỉ nhận danh sách mã cần tra, không nhận cả dự án. Kết quả tìm kiếm web dài dòng nằm lại trong sub agent.
- **Thiết kế và hạng mục chạy trong agent chính** vì cần toàn bộ bối cảnh; tách ra sub agent thì lại phải đọc lại từ đầu.
- **Vòng cắt giảm có giới hạn**: tối đa 2 vòng, sau đó bạn quyết.

## Tùy chỉnh
- **Model của sub agent**: trong `plugins/photobooth/agents/khao-gia.md`, dòng `model: sonnet`. Có thể đổi sang `haiku` để rẻ hơn, đổi lại kết quả tra giá kém kỹ hơn.
- **Hạn giá cũ**: biến `HAN_GIA_NGAY` trong `plugins/photobooth/skills/du-toan-ngan-sach/scripts/du_toan.py`.
- **Dùng cho dự án khác** (quán cà phê, tiệm nail…): skill `du-toan-ngan-sach` và agent `khao-gia` dùng chung được. Chỉ cần viết thêm một skill checklist cho loại hình đó.

## Lưu ý từ lần khảo giá đầu (mặt bằng 3×6m, 50tr)
Nếu làm **đủ mọi hạng mục ở mức rẻ nhất**, tổng vẫn khoảng **60tr** (gồm 10% dự phòng). Ba khoản lớn nhất là vách ngăn cùng cửa (~9,7tr), điều hòa (7,5tr) và điện (5,5tr). Muốn vừa 50tr phải cắt phạm vi: thay cửa bằng rèm, bỏ ghế lười, bỏ quầy, và chỉ cán nền khi thật cần. File `mau-hang-muc.json` đã đặt sẵn các mục này là tùy chọn. Chạy thử với file mẫu cho kết quả ~49,9tr, ĐẠT.

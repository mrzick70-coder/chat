---
name: ho-so-dau-tu
description: Thu thập hoặc cập nhật hồ sơ nhà đầu tư (vốn, hình thức, thời gian, khẩu vị rủi ro, lợi thế). Dùng khi hồ sơ trong CLAUDE.md còn trống, khi người dùng muốn thay đổi hồ sơ, hoặc trước lần nghiên cứu ngành đầu tiên.
---

# Hồ sơ nhà đầu tư

Hồ sơ quyết định kết luận của báo cáo: cùng một ngành, mua cổ phiếu hay tự mở cơ sở kinh doanh sẽ cho đánh giá rất khác nhau.

## Cách làm

1. Đọc mục "Hồ sơ nhà đầu tư" trong `CLAUDE.md`. Chỉ hỏi những mục còn trống hoặc người dùng muốn đổi.
2. Gom câu hỏi vào **một lượt hỏi** (dùng AskUserQuestion nếu có, tối đa 4 câu mỗi lượt), đưa sẵn lựa chọn để người dùng chọn nhanh:
   - **Vốn dự kiến:** dưới 200 triệu · 200 triệu–1 tỷ · 1–5 tỷ · trên 5 tỷ
   - **Hình thức:** cổ phiếu/quỹ · tự mở cơ sở kinh doanh · góp vốn/mua lại doanh nghiệp nhỏ · nhượng quyền · chưa rõ, muốn được gợi ý
   - **Thời gian nắm giữ:** dưới 1 năm · 1–3 năm · 3–5 năm · trên 5 năm
   - **Mức lỗ tối đa chịu được:** 10% · 25% · 50% · có thể mất toàn bộ phần vốn này
3. Lượt hỏi thứ hai (chỉ khi cần): mức tham gia vận hành, kinh nghiệm/lợi thế sẵn có (nghề nghiệp, quan hệ, mặt bằng…), khu vực địa lý, ngành quan tâm hoặc muốn loại trừ.
4. Ghi câu trả lời vào mục "Hồ sơ nhà đầu tư" trong `CLAUDE.md`, xoá dòng "Chưa điền" và các chữ _(chưa điền)_ đã được trả lời.
5. Tóm tắt lại hồ sơ trong 3–4 dòng để người dùng xác nhận.

## Lưu ý

- Nếu người dùng không muốn trả lời mục nào, ghi "Không cung cấp" và tiếp tục; không ép hỏi lại.
- Nếu vốn nhỏ nhưng người dùng muốn ngành cần vốn lớn, nêu mâu thuẫn này ngay và gợi ý hình thức phù hợp hơn (ví dụ cổ phiếu/ETF của ngành đó).

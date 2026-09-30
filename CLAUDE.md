# Workflow nghiên cứu ngành để đầu tư

Repo này là bộ công cụ để Claude Code nghiên cứu một ngành nghề và viết báo cáo đầu tư.
Quy trình chính nằm ở skill `nghien-cuu-nganh`; các chuyên viên nằm ở `.claude/agents/`.

## Hồ sơ nhà đầu tư

> Điền một phần. Các mục còn _(chưa điền)_ sẽ được skill `ho-so-dau-tu` hỏi trước lần nghiên cứu đầu tiên.

- Vốn dự kiến: 1 tỷ VND
- Hình thức đầu tư: kinh doanh trực tiếp (tự mở và vận hành cơ sở kinh doanh; có thể cân nhắc nhượng quyền)
- Thời gian nắm giữ: _(chưa điền)_
- Mức lỗ tối đa chịu được: _(chưa điền)_
- Mức tham gia vận hành: _(thụ động · bán thời gian · toàn thời gian)_
- Kinh nghiệm / lợi thế sẵn có: _(chưa điền)_
- Khu vực địa lý: _(mặc định: Việt Nam)_
- Ngành quan tâm / ngành loại trừ: _(chưa điền)_

## Quy tắc nghiên cứu (áp dụng cho mọi agent)

1. **Mọi con số phải có nguồn** theo dạng `[Tên nguồn, năm]`, kèm link khi có.
   Không có nguồn thì ghi `ƯỚC TÍNH` và nói rõ cách tính, giả định.
2. **Ghi mức độ tin cậy** cho mỗi kết luận quan trọng: `Cao` / `Trung bình` / `Thấp`.
3. **Ưu tiên số liệu trong 2 năm gần nhất.** Số liệu cũ hơn phải ghi rõ năm.
4. **Ghi rõ đơn vị tiền tệ** (VND hoặc USD) và năm của giá trị.
5. **Không bịa.** Không tìm được thì ghi "Không tìm thấy dữ liệu" thay vì đoán.
6. Báo cáo là tài liệu tham khảo, **không phải lời khuyên đầu tư**. Luôn kèm phần "việc cần kiểm chứng ngoài đời thực".

## Nguồn ưu tiên

- Thống kê chính thức: Tổng cục Thống kê (gso.gov.vn), Ngân hàng Nhà nước, Bộ/Sở ngành liên quan, Tổng cục Hải quan.
- Pháp lý: vbpl.vn, thuvienphapluat.vn, Cổng thông tin quốc gia về đầu tư.
- Báo cáo ngành: công ty chứng khoán (SSI, VNDirect, FPTS, HSC, Vietcap, MBS…), hiệp hội ngành, các hãng nghiên cứu (Statista, Euromonitor, Mordor, Nielsen, Decision Lab…).
- Doanh nghiệp: báo cáo tài chính và báo cáo thường niên của doanh nghiệp niêm yết (cafef.vn, vietstock.vn).
- Quốc tế: World Bank, IMF, ADB, WTO, OECD.
- Tin tức chỉ dùng để tham khảo bối cảnh; con số quan trọng phải đối chiếu với nguồn gốc.

## Quy ước thư mục

```
research/
  sang-loc/<YYYY-MM-DD>.md        # kết quả của agent trinh-sat-nganh
  <slug-nganh>/
    00-pham-vi.md                  # hồ sơ + phạm vi nghiên cứu (người điều phối ghi)
    01-quy-mo-thi-truong.md
    02-canh-tranh.md
    03-phap-ly-chinh-sach.md
    04-tai-chinh-nganh.md
    05-xu-huong-rui-ro.md
    06-phan-bien.md
    07-cham-diem.md
    bao-cao.md                     # báo cáo cuối cùng
```

`<slug-nganh>` viết thường, không dấu, nối bằng gạch ngang, ví dụ `chuoi-ca-phe`, `dien-mat-troi-ap-mai`.

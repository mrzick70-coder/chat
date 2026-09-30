# Tự làm phần mềm Photobooth với Claude Code — dành cho người không biết lập trình

Bạn **không cần biết code**. Bạn chỉ cần biết mình muốn gì và nói ra bằng tiếng Việt
bình thường. Claude sẽ viết code, chạy thử, sửa lỗi và giải thích cho bạn.

Hãy nghĩ thế này: **bạn là chủ nhà, Claude là đội thợ.** Chủ nhà không cần biết trộn xi
măng — chỉ cần nói "tôi muốn phòng khách rộng, cửa sổ hướng đông", rồi đi xem và góp ý.

---

## Bạn sẽ có gì khi xong?

Một ứng dụng chạy trên máy tính có webcam, mở toàn màn hình:

1. Màn hình chờ: "Chạm để chụp ảnh!"
2. Khách chạm → đếm ngược 3‑2‑1 → chụp 3–4 ảnh
3. Ảnh được ghép vào khung đẹp (có logo, tên sự kiện, ngày)
4. Khách xem lại → bấm **In** → máy in ra ảnh
5. Ảnh tự lưu vào một thư mục trên máy
6. Quay về màn hình chờ cho khách tiếp theo

Không cần cài đặt phức tạp: **bấm đúp một file là chạy.**

---

## Cần chuẩn bị gì?

| Thứ cần có | Ghi chú |
|---|---|
| Máy tính Windows hoặc Mac | Laptop bình thường là được |
| Webcam | Webcam có sẵn của laptop cũng được để làm thử; sự kiện thật nên dùng webcam rời tốt hơn |
| Trình duyệt **Google Chrome** | Tải miễn phí tại google.com/chrome |
| Tài khoản Claude trả phí (gói Pro hoặc Max) | Để dùng được Claude Code |
| Ứng dụng **Claude** trên máy tính | Tải tại claude.ai/download — Claude Code nằm trong ứng dụng này, không cần gõ lệnh |
| Máy in ảnh (có thể để sau) | Máy in nào in được từ máy tính là dùng được |
| Hình khung ảnh, logo (có thể để sau) | File PNG; nếu chưa có, Claude sẽ tự vẽ khung đơn giản |

Thời gian: khoảng **3–5 buổi tối** cho bản dùng được ở sự kiện.

---

## 5 quy tắc vàng khi làm việc với Claude

1. **Mỗi lần chỉ xin một thứ.** "Thêm đếm ngược" — thử — xong rồi mới "thêm khung ảnh".
   Xin 10 thứ một lúc thì khó biết cái nào hỏng.
2. **Tả kết quả, đừng tả cách làm.** Nói "tôi muốn khách thấy số to giữa màn hình, kèm
   tiếng bíp" — không cần biết nó làm bằng gì.
3. **Luôn tự tay thử sau mỗi bước.** Claude sẽ bảo bạn thử thế nào. Thấy lạ thì nói ngay.
4. **Báo lỗi bằng hình.** Chụp màn hình và kéo thả vào khung chat — Claude hiểu hình ảnh.
5. **Không hiểu thì hỏi.** "Giải thích lại đơn giản hơn" hoặc "cái đó nghĩa là gì?" —
   Claude đã được dặn phải trả lời bằng ngôn ngữ đời thường.

---

## Các bước thực hiện

### Bước 1 — Chuẩn bị chỗ làm việc (15 phút)

1. Cài ứng dụng **Claude** trên máy tính và đăng nhập.
2. Tạo một thư mục mới, ví dụ `Photobooth` trong Documents.
3. Chép **toàn bộ nội dung** thư mục [`starter-don-gian/`](./starter-don-gian) vào thư mục
   `Photobooth` đó.
   > ⚠️ Trong đó có một thư mục tên `.claude` — trên Mac/Windows nó có thể bị ẩn. Trên Mac
   > bấm `Cmd + Shift + .` để hiện file ẩn; trên Windows vào *View → Show → Hidden items*.
   > Nhớ chép cả nó, vì đó là nơi chứa "lời dặn" cho Claude.
4. Mở ứng dụng Claude → chọn mục **Code** → chọn thư mục `Photobooth`.

Nếu kẹt ở bước nào, cứ hỏi Claude (trong ứng dụng chat thường): "tôi đang cài Claude Code
và bị kẹt ở chỗ …".

### Bước 2 — Kể cho Claude nghe ý tưởng (20 phút)

Gõ vào ô chat (chép nguyên đoạn này rồi sửa theo ý bạn):

```
Chào Claude. Tôi không biết lập trình. Tôi muốn làm phần mềm photobooth
cho [đám cưới / sự kiện công ty / quán cà phê].
Khách chạm màn hình, đếm ngược, chụp [3] ảnh, ghép vào khung rồi in ra.
Tôi dùng máy [Windows/Mac], webcam [của laptop / webcam rời],
máy in [tên máy in, hoặc "chưa có"].

Trước khi làm gì, hãy hỏi tôi từng câu một để hiểu rõ tôi muốn gì,
rồi viết lại thành một bản mô tả ngắn cho tôi duyệt.
```

Claude sẽ hỏi bạn vài câu (màu sắc, chữ trên khung, có cần QR không…). Trả lời thoải mái,
không có câu trả lời sai. Cuối cùng Claude sẽ ghi lại thành file `MO-TA.md`. **Đọc kỹ file
đó** — đó là "bản vẽ ngôi nhà". Sai chỗ nào thì bảo Claude sửa.

### Bước 3 — Bản đầu tiên, thật đơn giản (30 phút)

```
/buoc-tiep
```

Lệnh `/buoc-tiep` là lệnh có sẵn: Claude xem bản mô tả, chọn việc nhỏ tiếp theo nên làm,
làm nó, rồi **hướng dẫn bạn thử**. Lần đầu tiên nó sẽ làm bản đơn giản nhất: chạm → đếm
ngược → chụp 1 ảnh → hiện ảnh.

Claude sẽ nói kiểu: *"Bấm đúp vào file `CHAY-PHOTOBOOTH` trong thư mục. Chrome sẽ mở toàn
màn hình. Chạm vào màn hình và xem có đếm ngược không. Để thoát, bấm Alt+F4 (Windows) hoặc
Cmd+Q (Mac)."*

Bạn làm theo và báo lại: "được rồi" hoặc "không được, nó hiện cái này" + ảnh chụp màn hình.

### Bước 4 — Thêm từng thứ một (mỗi thứ 15–45 phút)

Cứ gõ `/buoc-tiep` lặp lại, hoặc tự nói điều bạn muốn. Thứ tự gợi ý và câu nói mẫu:

| # | Tính năng | Bạn có thể nói |
|---|---|---|
| 1 | Chụp nhiều ảnh | "Mỗi lượt chụp 3 ảnh, giữa các ảnh nghỉ 2 giây." |
| 2 | Âm thanh & hiệu ứng | "Mỗi số đếm ngược kêu bíp, lúc chụp màn hình nháy trắng như đèn flash." |
| 3 | Khung ảnh | "Ghép 3 ảnh thành dải dọc, bên dưới ghi 'Tiệc cưới Nam & Mai – 12/10/2026', nền màu kem." |
| 4 | Dùng khung của tôi | "Tôi để file `khung.png` trong thư mục `hinh`. Đặt ảnh vào các ô trống của khung." *(gửi kèm ảnh khung)* |
| 5 | Xem lại & chụp lại | "Sau khi chụp, cho khách xem và có nút 'Chụp lại' và 'In'." |
| 6 | Tự lưu ảnh | "Mỗi ảnh ghép tự lưu vào thư mục `anh-su-kien`, không hỏi gì." |
| 7 | Tự quay về | "Nếu 30 giây không ai chạm thì quay về màn hình chờ." |
| 8 | Màn hình chờ đẹp | "Màn hình chờ chạy lần lượt các ảnh khách vừa chụp, chữ 'Chạm để chụp' nhấp nháy." |
| 9 | Chỗ cài đặt cho bạn | "Làm một trang cài đặt có mật khẩu 1234 để tôi đổi chữ trên khung, số ảnh, thời gian đếm ngược mà không phải nhờ bạn." |
| 10 | (Nâng cao) QR tải ảnh | "Tôi muốn khách quét QR để lấy ảnh về điện thoại. Giải thích cho tôi các cách, cái nào miễn phí, cái nào cần Internet." |

Sau mỗi tính năng chạy tốt, Claude sẽ tự **lưu một "điểm khôi phục"** (giống lưu game).
Nếu sau này làm hỏng, bạn quay lại được.

### Bước 5 — Khi có gì đó không đúng

Gõ:

```
/bao-loi
```

rồi mô tả **3 điều**: (1) bạn đã làm gì, (2) bạn mong thấy gì, (3) bạn lại thấy gì.
Kèm ảnh chụp màn hình nếu có.

Ví dụ: *"Tôi chạm màn hình, mong là đếm ngược, nhưng màn hình đen thui. [ảnh]"*

Nếu mọi thứ rối tung và bạn muốn về lúc còn chạy tốt:

```
/quay-lai
```

Claude sẽ cho bạn xem danh sách các điểm khôi phục bằng tiếng Việt và hỏi bạn muốn về
điểm nào.

### Bước 6 — Kết nối máy in

```
Giờ tôi muốn in. Máy in của tôi là [tên máy], giấy [4x6 / khổ A6 / ...].
Hướng dẫn tôi từng bước cài đặt để bấm "In" là in luôn, không hiện hộp thoại.
```

Claude sẽ hướng dẫn cài máy in làm máy in mặc định, chỉnh khổ giấy, và sửa file khởi động
để in thẳng. Hãy in thử vài tấm và chụp ảnh tờ in gửi cho Claude nếu bị lệch, thiếu viền,
màu sai.

### Bước 7 — Chuẩn bị trước sự kiện (1 buổi)

```
/chuan-bi-su-kien
```

Claude sẽ tạo cho bạn một **danh sách kiểm tra** bằng tiếng Việt để in ra giấy, gồm những
việc như:

- [ ] Chạy thử liên tục 2–3 tiếng, chụp 30–50 lượt, xem có bị đơ không
- [ ] Rút webcam ra cắm lại — phần mềm có tự nhận lại không
- [ ] Hết giấy in — khách có thấy thông báo dễ hiểu không, ảnh có còn được lưu không
- [ ] Tắt chế độ ngủ/tắt màn hình của máy tính
- [ ] Sạc đầy / cắm điện; mang dây dự phòng
- [ ] Sao chép ảnh sự kiện ra USB sau buổi tiệc

---

## Gặp tình huống này thì nói gì?

| Tình huống | Nói với Claude |
|---|---|
| Claude nói toàn từ khó hiểu | "Giải thích lại như cho người không biết máy tính." |
| Claude hỏi "cho phép chạy lệnh…?" mà bạn không hiểu | "Lệnh này làm gì, có an toàn không?" — rồi mới bấm đồng ý |
| Claude đang làm sai hướng | Bấm **Esc** (hoặc nút dừng) rồi nói lại rõ hơn |
| Không thấy file Claude nói tới | "Mở thư mục đó giúp tôi" hoặc "file đó nằm ở đâu, tên chính xác là gì?" |
| Muốn đổi màu/chữ/kích thước | Nói thẳng: "Chữ to gấp đôi", "nút màu hồng pastel" — kèm ảnh mẫu càng tốt |
| Cuộc trò chuyện quá dài, Claude có vẻ quên | Bắt đầu cuộc trò chuyện mới và gõ `/buoc-tiep` — Claude đọc lại file mô tả và tiếp tục |
| Muốn nhờ người khác xem giúp | "Viết cho tôi một đoạn giải thích phần mềm này đang làm được gì, để tôi gửi bạn tôi." |

## Những điều nên tránh

- ❌ Tự sửa/xoá file trong thư mục nếu không chắc — hãy nhờ Claude.
- ❌ Làm tính năng mới ngay trước giờ sự kiện. Chốt phiên bản trước **ít nhất 2 ngày**.
- ❌ Đổi máy tính/webcam/máy in vào phút chót mà chưa thử lại.
- ❌ Gửi mật khẩu, số tài khoản ngân hàng vào khung chat.

## Một vài từ Claude có thể nhắc tới

| Từ | Nghĩa đơn giản |
|---|---|
| Code / mã nguồn | Các file "công thức" làm nên phần mềm |
| Chế độ kiosk | Mở toàn màn hình, khách không thoát ra được |
| Webcam permission | Trình duyệt xin phép dùng camera |
| Commit / điểm khôi phục | Một lần "lưu game" của dự án |
| Bug | Lỗi |
| Test | Chạy thử để xem có đúng không |

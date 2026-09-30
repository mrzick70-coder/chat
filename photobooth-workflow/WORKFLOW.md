# Workflow xây dựng phần mềm Photobooth bằng Claude Code

Tài liệu này mô tả quy trình từ ý tưởng đến triển khai tại sự kiện cho một phần mềm
photobooth, với Claude Code làm "lập trình viên chính" còn bạn giữ vai trò product
owner + reviewer. Thư mục [`starter/`](./starter) chứa sẵn `CLAUDE.md`, slash command,
hook và template spec để bạn chép vào dự án mới.

---

## 0. Tổng quan

```
 Giai đoạn 0      1          2            3          4 (lặp)          5            6           7
 ┌───────┐   ┌───────┐   ┌─────────┐   ┌───────┐   ┌──────────┐   ┌─────────┐   ┌───────┐   ┌────────┐
 │ Setup │ → │ Spec  │ → │ Kiến    │ → │ Khung │ → │ Tính năng│ → │ Phần    │ → │ Đóng  │ → │ Vận    │
 │ môi   │   │ (PRD) │   │ trúc    │   │ dự án │   │ theo vòng│   │ cứng    │   │ gói & │   │ hành & │
 │ trường│   │       │   │         │   │ + CI  │   │ lặp      │   │ thật    │   │ kiosk │   │ bảo trì│
 └───────┘   └───────┘   └─────────┘   └───────┘   └──────────┘   └─────────┘   └───────┘   └────────┘
   CLAUDE.md   Plan mode   Plan mode     TDD         /feature        /hw-test      /release    logs,
   settings    docs/SPEC   ADR           mock HW     /code-review    checklist     electron-   cấu hình
   hooks                                             worktree song   thủ công      builder     sự kiện
                                                     song
```

Nguyên tắc xuyên suốt:

1. **Viết ra trước, code sau.** Mọi thứ Claude cần nhớ nằm trong file (`CLAUDE.md`,
   `docs/SPEC.md`, `docs/ARCHITECTURE.md`), không nằm trong trí nhớ phiên chat.
2. **Phần cứng luôn có bản giả (mock).** Camera và máy in được bọc sau interface; 90%
   việc phát triển và test chạy không cần thiết bị thật.
3. **Vòng lặp nhỏ.** Mỗi tính năng = 1 nhánh = 1 PR, có test, được review trước khi merge.
4. **Máy tự kiểm tra.** Hook chạy format/lint, CI chạy test — Claude tự sửa khi đỏ.

---

## 1. Chọn công nghệ (khuyến nghị)

| Thành phần        | Khuyến nghị                                             | Phương án khác                          |
|-------------------|---------------------------------------------------------|-----------------------------------------|
| App shell         | **Electron + React + TypeScript + Vite**                | Tauri (nhẹ hơn, Rust), web thuần + Chrome kiosk |
| Luồng màn hình    | **XState** (state machine)                              | Zustand + reducer tự viết               |
| Camera – webcam   | `getUserMedia` (WebRTC)                                 | —                                       |
| Camera – DSLR     | `gphoto2` (Linux/macOS) qua child process              | digiCamControl (Windows), Canon EDSDK   |
| Ghép ảnh / khung  | **sharp** (Node) cho bản in; Canvas cho preview         | node-canvas, ImageMagick                |
| In ảnh            | `webContents.print` / lệnh `lp` (CUPS)                  | Driver riêng của DNP / Canon Selphy     |
| Chia sẻ           | QR code (`qrcode`) → link tải ảnh; email tuỳ chọn       | Upload S3/Cloudinary, AirDrop-like      |
| Lưu trữ           | Thư mục sự kiện trên đĩa + SQLite (`better-sqlite3`)    | JSON file                               |
| Test              | **Vitest** (unit) + **Playwright** (E2E, camera giả)    | Jest                                    |
| Đóng gói          | **electron-builder**, auto-start, kiosk mode            | —                                       |

> Nếu chỉ cần webcam và chạy trên 1 máy, có thể bỏ Electron và dùng web app + Chrome
> `--kiosk`. Nhưng in ảnh im lặng (không hộp thoại) và điều khiển DSLR cần Electron/Node.

Bạn có thể giao việc so sánh cho Claude ngay ở giai đoạn 2 (xem prompt bên dưới).

---

## 2. Các giai đoạn chi tiết

### Giai đoạn 0 — Setup môi trường (≈30 phút)

```bash
mkdir photobooth && cd photobooth && git init
cp -r <repo-này>/photobooth-workflow/starter/. .   # CLAUDE.md, .claude/, docs/
claude
```

Trong Claude Code:

- `/init` — nếu đã có code, để Claude bổ sung `CLAUDE.md` từ codebase (starter đã có sẵn
  bản mẫu, chỉ cần chỉnh).
- `/permissions` — kiểm tra các lệnh được phép tự chạy (starter cho phép `npm run test`,
  `lint`, `typecheck`, `playwright`…).
- Cài MCP hữu ích (tuỳ chọn):
  - **Playwright MCP** để Claude tự mở app, chụp màn hình UI kiosk và tự kiểm tra:
    `claude mcp add playwright -- npx @playwright/mcp@latest`
  - **GitHub MCP / `gh`** để tạo issue, PR.

Kết quả: repo trống có `CLAUDE.md`, `.claude/settings.json` (hook format), `.claude/commands/`.

### Giai đoạn 1 — Viết Spec (≈1 giờ, bạn quyết định, Claude soạn)

Bật **Plan mode** (`Shift+Tab` hai lần) để Claude chỉ hỏi và soạn, không sửa code.

> **Prompt mẫu**
> ```
> Tôi muốn làm phần mềm photobooth cho sự kiện (đám cưới, sự kiện công ty).
> Hãy phỏng vấn tôi từng câu một để hoàn thiện docs/SPEC.md theo template có sẵn:
> đối tượng dùng, luồng khách, số ảnh/lượt, layout in (strip 2x6, 4x6),
> phần cứng (webcam hay DSLR, máy in gì), chia sẻ (QR, email), màn hình admin,
> yêu cầu offline. Sau khi đủ thông tin, viết SPEC.md gồm user story và
> tiêu chí chấp nhận (acceptance criteria) đánh số.
> ```

Đầu ra: `docs/SPEC.md` với user story đánh mã (`US-01`…) và tiêu chí chấp nhận
kiểm chứng được. Bạn đọc và sửa — đây là "hợp đồng" cho mọi bước sau.

Luồng khách điển hình (đưa vào SPEC):

```
IDLE (attract loop) ─chạm─▶ CHỌN LAYOUT ─▶ ĐẾM NGƯỢC ─▶ CHỤP ─┐
      ▲                                       ▲              │ còn ảnh?
      │                                       └──── có ──────┤
      │                                                      ▼ hết
  CẢM ƠN ◀── IN / QR ◀── XEM LẠI (chụp lại ảnh N?) ◀── GHÉP KHUNG
      └─ timeout bất kỳ màn hình nào ─▶ IDLE
```

### Giai đoạn 2 — Kiến trúc (≈1 giờ)

Vẫn ở Plan mode.

> **Prompt mẫu**
> ```
> Đọc docs/SPEC.md. Đề xuất kiến trúc cho app Electron + React + TS.
> Yêu cầu:
> - State machine XState cho toàn bộ luồng khách, có timeout về IDLE.
> - Interface CameraProvider (startPreview, capture, dispose) với 3 bản:
>   WebcamProvider, Gphoto2Provider, MockCameraProvider.
> - Interface PrinterProvider với CupsPrinter và MockPrinter (ghi file PDF/PNG).
> - Compositor thuần (input: ảnh + template JSON → output: buffer ảnh in 300 DPI).
> - Tách main process / renderer, IPC có kiểu rõ ràng.
> - Cấu trúc thư mục, danh sách module, luồng dữ liệu.
> Viết vào docs/ARCHITECTURE.md và ghi các quyết định lớn thành ADR trong docs/adr/.
> Chỉ ra rủi ro kỹ thuật lớn nhất và cách giảm rủi ro.
> ```

Nên hỏi thêm: *"So sánh Electron với Tauri cho trường hợp của tôi, ưu tiên in không hộp
thoại và điều khiển DSLR"* — rồi ghi kết luận vào ADR.

### Giai đoạn 3 — Khung dự án + CI (≈1–2 giờ)

Thoát Plan mode.

> **Prompt mẫu**
> ```
> Dựng khung dự án theo docs/ARCHITECTURE.md:
> - Electron + Vite + React + TS, ESLint, Prettier, Vitest, Playwright.
> - Scripts: dev, build, test, test:e2e, lint, typecheck.
> - MockCameraProvider trả ảnh mẫu trong fixtures/; MockPrinter ghi ra out/prints/.
> - State machine rỗng với đủ các state trong SPEC, mỗi state 1 màn hình placeholder.
> - 1 test E2E chạy hết luồng IDLE → CẢM ƠN bằng mock.
> - GitHub Actions chạy lint + typecheck + test + test:e2e.
> Chạy tất cả lệnh kiểm tra cho đến khi xanh rồi commit.
> ```

Sau bước này cập nhật `CLAUDE.md` với lệnh thật (Claude có thể tự làm: *"cập nhật
CLAUDE.md phần Lệnh thường dùng"*).

### Giai đoạn 4 — Phát triển tính năng theo vòng lặp (phần lớn thời gian)

Mỗi user story đi qua đúng vòng này:

```
 ┌──────────────┐   ┌──────────────┐   ┌───────────────┐   ┌──────────────┐   ┌─────────────┐
 │ 1. Chọn story│ → │ 2. Plan mode │ → │ 3. Test trước │ → │ 4. Code tới  │ → │ 5. Review & │
 │ /feature US-x│   │ duyệt kế     │   │ (đỏ)          │   │ khi xanh     │   │ PR          │
 └──────────────┘   │ hoạch        │   └───────────────┘   └──────────────┘   │ /code-review│
                    └──────────────┘                                          └─────────────┘
```

Dùng lệnh có sẵn trong starter:

```
/feature US-03 đếm ngược 3-2-1 có âm thanh và flash màn hình
```

Lệnh `/feature` yêu cầu Claude: đọc SPEC → đề xuất kế hoạch và chờ bạn duyệt → viết test
từ tiêu chí chấp nhận → code → chạy lint/typecheck/test → chụp màn hình UI (nếu có
Playwright MCP) → commit trên nhánh `feat/US-03-...`.

Thứ tự tính năng gợi ý (mỗi mục 1 vòng):

1. Luồng state machine hoàn chỉnh + timeout (mock toàn bộ)
2. Preview camera live + đếm ngược + chụp (Webcam)
3. Compositor: template JSON (vị trí khung, overlay PNG, chữ, logo) → ảnh 300 DPI
4. Màn hình xem lại + chụp lại từng ảnh
5. In ảnh (MockPrinter → CUPS) + hàng đợi in, số bản in
6. QR chia sẻ (server nội bộ hoặc upload cloud)
7. Màn hình admin (PIN): chọn sự kiện, template, camera, máy in, đếm lượt
8. Hiệu ứng: filter, GIF/boomerang, sticker (tuỳ chọn)
9. DSLR (Gphoto2Provider)

**Làm song song:** các module độc lập (compositor, admin, QR) có thể giao cho nhiều
phiên Claude cùng lúc, mỗi phiên một git worktree:

```bash
git worktree add ../pb-compositor -b feat/US-05-compositor
cd ../pb-compositor && claude "/feature US-05 ..."
```

Hoặc trong một phiên, yêu cầu Claude dùng subagent: *"Dùng subagent riêng để viết test
cho compositor trong lúc bạn làm màn hình admin."*

**Review:** trước khi merge chạy `/code-review` (lỗi logic) và `/simplify` (làm gọn code).
Với mọi thứ đụng tới file hệ thống, upload, IPC: chạy thêm `/security-review`.

**Khi Claude đi sai hướng:** nhấn `Esc` để dừng, `Esc Esc` để quay lại điểm trước,
nói rõ điều sai và — nếu đó là quy tắc lâu dài — thêm vào `CLAUDE.md` (hoặc gõ `#` + quy
tắc để Claude tự ghi nhớ).

### Giai đoạn 5 — Tích hợp phần cứng thật

Claude không nhìn thấy camera/máy in của bạn, nên bạn là "tay chân" — Claude chuẩn bị
công cụ chẩn đoán và checklist.

```
/hw-test camera Canon EOS 250D qua gphoto2
/hw-test printer DNP DS-RX1HS khổ 4x6 cắt đôi 2x6
```

Lệnh `/hw-test` yêu cầu Claude viết script chẩn đoán độc lập (liệt kê thiết bị, chụp
thử, đo thời gian, in trang thử), rồi tạo checklist thử tay trong
`docs/hw/<thiết-bị>.md`. Bạn chạy script, dán log lỗi lại cho Claude để sửa.

Checklist tối thiểu trước sự kiện:

- [ ] Rút/cắm lại camera khi app đang chạy → app tự kết nối lại, không treo
- [ ] Hết giấy / kẹt giấy → thông báo cho khách, ảnh vẫn lưu, in lại được từ admin
- [ ] Mất mạng → chụp/in vẫn chạy, QR xếp hàng upload sau
- [ ] Chạy liên tục 4–6 giờ (soak test) không rò bộ nhớ
- [ ] Màu in khớp màn hình (profile ICC nếu cần)
- [ ] Ảnh gốc được lưu đủ độ phân giải trong thư mục sự kiện

### Giai đoạn 6 — Đóng gói & chế độ kiosk

```
/release 1.0.0
```

Lệnh `/release`: chạy toàn bộ kiểm tra, cập nhật CHANGELOG, build bằng electron-builder,
kiểm tra cấu hình kiosk (fullscreen, chặn thoát bằng phím tắt, ẩn con trỏ, tự khởi động
cùng hệ điều hành, tắt ngủ màn hình), tạo tag.

### Giai đoạn 7 — Vận hành & bảo trì

- Log có cấu trúc (JSON) ra file theo ngày; khi lỗi tại sự kiện, dán log cho Claude:
  *"Đây là log sự kiện tối qua, tìm nguyên nhân máy treo lúc 21:14."*
- Mỗi sự kiện = 1 file cấu hình (template, logo, text) — thêm sự kiện mới không cần sửa code.
- Lỗi tìm thấy → issue → quay về vòng lặp giai đoạn 4.

---

## 3. Mẹo làm việc với Claude Code cho dự án này

| Tình huống                                | Cách làm                                                              |
|-------------------------------------------|-----------------------------------------------------------------------|
| Việc lớn, nhiều file                      | Plan mode trước, duyệt kế hoạch rồi mới cho code                      |
| Phiên chat dài, Claude bắt đầu "quên"     | `/compact` hoặc `/clear` — mọi thứ quan trọng đã nằm trong file docs |
| Giao diện kiosk khó mô tả bằng lời        | Kéo thả ảnh mockup/screenshot vào terminal                            |
| Muốn Claude tự kiểm UI                    | Playwright MCP: "mở app, đi hết luồng, chụp màn hình từng bước"       |
| Lặp đi lặp lại cùng một lời dặn           | Đưa vào `CLAUDE.md` hoặc tạo slash command mới trong `.claude/commands/` |
| Code nhạy cảm (IPC, file system, upload)  | `/security-review` trước khi merge                                    |
| Muốn chạy không cần hỏi quyền từng lệnh   | Thêm lệnh an toàn vào `permissions.allow` trong `.claude/settings.json` |

## 4. Nội dung starter kit

```
starter/
├── CLAUDE.md                     # bối cảnh dự án, quy tắc, lệnh — Claude đọc mỗi phiên
├── .claude/
│   ├── settings.json             # quyền lệnh + hook tự format sau mỗi lần sửa file
│   └── commands/
│       ├── feature.md            # /feature <US-id> <mô tả>  — vòng lặp tính năng
│       ├── hw-test.md            # /hw-test <thiết bị>       — chẩn đoán phần cứng
│       └── release.md            # /release <version>        — đóng gói & phát hành
└── docs/
    ├── SPEC.md                   # template spec (giai đoạn 1 điền)
    └── adr/0000-template.md      # template ghi quyết định kiến trúc
```

## 5. Lịch trình tham khảo (1 người + Claude Code)

| Tuần | Việc                                                                 |
|------|----------------------------------------------------------------------|
| 1    | Giai đoạn 0–3; tính năng 1–2 (luồng + webcam) → demo chạy được       |
| 2    | Tính năng 3–5 (compositor, xem lại, in)                              |
| 3    | Tính năng 6–7 (QR, admin); bắt đầu phần cứng thật                    |
| 4    | DSLR, soak test, đóng gói kiosk, chạy thử tại 1 sự kiện nhỏ           |

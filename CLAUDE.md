# Figma6 — Figma → HTML/CSS

Chuyển thiết kế Figma sang HTML semantic + CSS thuần. Không framework, không
bước build, **không một dòng JavaScript nào được gửi xuống trình duyệt**.

Chú thích trong code viết tiếng Việt cho dễ đọc lúc phát triển — chuyển sang
tiếng Anh trước khi bàn giao.

## Quy ước bắt buộc — đọc trước khi sửa bất cứ gì

- **Không flexbox, không grid, không `gap`.** Bố cục dựng bằng `float` +
  `calc()`, `clear`, `flow-root`, `inline-block` + `font-size: 0` ở cha,
  `line-height` + `vertical-align`, `position: absolute`.
- **Không JavaScript** trên trang giao cho khách. Trạng thái mở/đóng dùng
  `:target`, `<details>`, radio/checkbox + `:has()`. `dev/*-overlay.html` là
  công cụ nội bộ (cũng không JS).
- **CSS chia theo cascade layer**, khai báo một lần trong `<head>`:
  `reset, tokens, base, layout, components, utilities`. Không `!important`
  (trừ khối `prefers-reduced-motion`).
- **`css/tokens.css` chỉ chứa giá trị dùng chung** (màu, font, thang độ đậm,
  leading, chuyển động, bo góc). Số đo riêng của component ghi thẳng trong
  file component. Số dùng ở nhiều rule trong cùng component thì làm biến cục
  bộ trên selector gốc (vd. `.card { --card-title-gap: 87px; }`), không đưa lên
  `:root`. Mọi con số đều ghi nhãn nguồn gốc ngay bên cạnh:
  - `[FIGMA]` — đọc thẳng từ panel inspector
  - `[ĐO]` — đo bằng script quét pixel trên ảnh export 1:1
  - `[MẪU]` — lấy từ file asset được cung cấp
  - `[ƯỚC]` — ước lượng, chờ xác nhận lại
- Đặt tên BEM, specificity phẳng, không selector lồng quá một cấp, không dùng
  ID để style.
- **Pixel-perfect**: mỗi trang render đúng khổ khung Figma; đối chiếu bằng
  overlay + script so pixel. Đã chốt số đo thì không đổi.
- `css/fonts.css` có `ascent-/descent-override` dời baseline Epilogue xuống
  1.25% em cho khớp Figma — đổi số này là lệch chữ toàn site.
- Font thương mại → thay bằng font OFL, tự lưu `.woff2` trong `assets/fonts/`
  (không gọi Google Fonts).

## Cấu trúc

```
*.html                   mỗi trang Figma một file
css/
├── reset.css / fonts.css / tokens.css / base.css / layout.css
├── components/          mỗi khối một file BEM
└── utilities.css        .visually-hidden, .skip-link
assets/fonts|icon|img/
dev/pages.json           danh sách trang (nguồn sinh overlay)
dev/*-overlay.html       đè ảnh Figma lên bản code (Code / 50% / Figma / Slider)
                         home = desktop 1440, home-mobile = mobile 375 (cùng index.html)
                         about / about-mobile (cùng about.html)
                         services / services-mobile (cùng services.html)
                         portfolio / portfolio-mobile (cùng portfolio.html)
docs/comparison/<slug>/  <slug>-figma.png, -build, -side-by-side, -overlay, -difference
```

## Trạng thái các trang

- **Homepage** (`index.html`): xong cả 2 khung — desktop `1_Home_Agency_1440`
  (1440 × 17296, 98.9 % pixel lệch ≤ 30, mọi phần tử ≤ 2px) và mobile `1_Home_Agency_375`
  (375 × 27360, 98.0 %). Overlay: `dev/home-overlay.html`,
  `dev/home-mobile-overlay.html`. Thông số: `docs/comparison/home/spec*.md`.
  Mobile là CSS mặc định; `64rem` bố cục desktop; `90rem` minh hoạ dựng mảnh.
- **About** (`about.html`): xong cả 2 khung — `2_About_Agency_1440` (1440 × 6160,
  99.1 % pixel lệch ≤ 30) và `2_About_Agency_375` (375 × 8640, 97.6 %).
  Component mới: `page-hero`, `intro`, `gallery`, `reviews`, `about-band`;
  component Home dùng lại qua modifier `--about`/`--dark` hoặc biến cục bộ
  (`--faq-*`, `--banner-*`). Thông số: `docs/comparison/about/spec.md`.
  Chụp khổ < 500px phải qua iframe (Chrome headless không thu nhỏ hơn 500).
- **Services** (`services.html`): xong cả 2 khung — `3_Services_1440` (1440 × 3664,
  99.0 % pixel lệch ≤ 30) và `3_Services_375` (375 × 5152, 97.6 %). Component mới:
  `accordion` (`<details name="service">`); dùng lại `intro`, `steps`, `checklist`,
  `banner`, `site-footer` qua modifier `--services`/`--strong`.
  Thông số: `docs/comparison/services/spec.md`.
- **Portfolio** (`portfolio.html`): xong cả 2 khung — `4_Portfolio_1_1440` (1440 × 3440,
  99.6 % pixel lệch ≤ 30) và `4_Portfolio_1_375` (375 × 4656, 98.6 %; HTML theo thứ tự
  thẻ mobile, desktop đổi chỗ bằng `work--swap-*`). Component mới: `pagination`; dùng lại
  `portfolio` (`--page`, `work--full/--half`), `banner`, `site-footer` (`--portfolio`).
  Thông số: `docs/comparison/portfolio/spec.md`.

## Chạy thử

```bash
npm install     # chỉ để có browser-sync
npm run dev     # http://localhost:3000
```

Không có npm: `python3 -m http.server 3000`.

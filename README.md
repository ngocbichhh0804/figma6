# Figma6 — Figma → HTML/CSS

Cắt tay từ Figma sang HTML semantic và **CSS thuần**. Không framework, không
bước build, **không JavaScript**.

**Live:** _điền URL_ · **Source:** _điền URL_ · **Thiết kế:** _điền link Figma_

## Độ khớp với bản thiết kế

| Trang | Khung Figma | Sai lệch màu TB (/765) | Pixel lệch ≤ 30 | Ghi chú |
| --- | --- | --- | --- | --- |
| Homepage — desktop (`1_Home_Agency_1440`) | 1440 × 17296 | 2.2 | 98.8 % | ≤ 60: 99.1 %; 346 phần tử đo theo DOM, tất cả lệch ≤ 2px (chỉ còn khử răng cưa chữ) |
| Homepage — mobile (`1_Home_Agency_375`) | 375 × 27360 | 6.9 | 96.5 % | ≤ 60: 97.5 % |

Cả hai khung dùng chung **một** file `index.html`; mobile là CSS mặc định,
desktop bật từ `64rem`, các mảnh minh hoạ dựng rời bật từ `90rem` (1440).
Gần như mọi dòng chữ khớp 0–1px theo `bbox.py --rows`; phần lệch còn lại chủ
yếu là khử răng cưa chữ và ảnh minh hoạ ghép từ mảnh.

Ảnh đối chiếu nằm trong `docs/comparison/<trang>/`. Tự kiểm trực tiếp: mở
`dev/<trang>-overlay.html` (bốn chế độ Code only / Overlay 50% / Figma only /
Slider — không JavaScript, nút là radio input đọc bằng `:has()`).

## Không flexbox, không grid

Bố cục dựng bằng kỹ thuật trước thời flexbox: `float` + `calc()`, `flow-root`,
`inline-block` + `font-size: 0`, `line-height` + `vertical-align`,
`position: absolute`.

## Font

| Font Figma | Thay bằng (OFL) | Weight |
| --- | --- | --- |
| Epilogue | Epilogue (đúng font, OFL — không phải thay) | 400, 700, 800, 900 — bản variable `assets/fonts/epilogue-latin-wght-normal.woff2` |

## Chỗ khác bản thiết kế

- **Minh hoạ desktop (≥ 1440) là ảnh cắt 1:1 từ export** `assets/img/art-*-desktop.png`
  (hero, About, Features, Service, CTA, banner): các mảnh rời export không
  đúng hướng xoay nên ghép lại lệch. Cùng độ phân giải 1x với asset gốc.
- **Icon cắt từ ảnh export** (chưa có asset gốc): `assets/icon/service-development.png`,
  `service-marketing.png`, `contact-phone.png`, `contact-email.png`,
  `contact-address.png`, và ảnh vòm tím `assets/img/service-arch.png`. Chỉ có
  bản 1x — **cần khách gửi SVG/@2x**.
- **Khổ 1024–1439** (Figma không vẽ): minh hoạ dùng ảnh gộp của bản mobile
  thay cho bản dựng mảnh; header dùng nút ☰ dưới 1200px. Số liệu `[ƯỚC]`.
- **Khổ > 1440**: nội dung giữ 1170px canh giữa, nền và bản đồ trải hết bề
  ngang (bản đồ `object-fit: cover`), ghim bản đồ neo theo tâm.
- **Lọc Portfolio** chạy thật bằng radio + `:has()`; ở mobile hiển thị như ô
  chọn (mở khi hover/focus). **FAQ** dùng `<details name="faq">` — mở mục này
  thì mục kia đóng. **Team** cuộn ngang bằng `scroll-snap`; chấm/mũi tên chỉ
  trang trí. Video, form chưa nối backend (`action="#"`).
- Mobile: tiêu đề "Making Complex…" và "How Our Agency…" tràn khung 329 như
  Figma (`margin-right: -40px`).

## Responsive

Đã kiểm 17 khổ 320 → 2560 (`responsive.py`): **không khổ nào cuộn ngang**.
Breakpoint: `48rem`, `64rem` (bố cục desktop), `75rem` (menu ngang), `80rem`,
`90rem` (minh hoạ dựng mảnh, đúng pixel 1440). Cảnh báo còn lại: link chữ
("Read More"…) cao 32px nhưng < 24px ở một chiều khi đứng trong dòng — chấp
nhận vì các vùng bấm cách nhau ≥ 24px.

## Còn cần từ phía khách

- SVG hoặc @2x cho các icon/ảnh ở mục "Icon cắt từ ảnh export".
- `assets/img/Portfolio Template (Community).zip` và vài ảnh export trùng
  không dùng tới — chờ chị xác nhận trước khi xoá/đổi tên sang kebab-case.

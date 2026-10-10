# Figma6 — Figma → HTML/CSS

Cắt tay từ Figma sang HTML semantic và **CSS thuần**. Không framework, không
bước build, **không JavaScript**.

**Live:** _điền URL_ · **Source:** _điền URL_ · **Thiết kế:** _điền link Figma_

## Độ khớp với bản thiết kế

| Trang | Khung Figma | Sai lệch màu TB (/765) | Pixel lệch ≤ 30 | Ghi chú |
| --- | --- | --- | --- | --- |
| Homepage — desktop (`1_Home_Agency_1440`) | 1440 × 17296 | 1.7 | 98.9 % | ≤ 60: 99.1 %; 346 phần tử đo theo DOM, tất cả lệch ≤ 2px (chỉ còn khử răng cưa chữ) |
| Homepage — mobile (`1_Home_Agency_375`) | 375 × 27360 | 2.9 | 98.0 % | ≤ 60: 98.7 % |
| About — desktop (`2_About_Agency_1440`) | 1440 × 6160 | 1.3 | 99.1 % | ≤ 60: 99.4 %; 44/88 vùng khớp 0px, còn lại lệch ≤ 1px (khử răng cưa chữ) |
| About — mobile (`2_About_Agency_375`) | 375 × 8640 | 3.6 | 97.6 % | ≤ 60: 98.5 %; 57/107 vùng khớp 0px, còn lại ≤ 1px (riêng tam giác play 3px) |
| Services — desktop (`3_Services_1440`) | 1440 × 3664 | 1.4 | 99.0 % | ≤ 60: 99.4 %; 47/77 vùng khớp 0px, còn lại ≤ 1px (khử răng cưa chữ) |
| Services — mobile (`3_Services_375`) | 375 × 5152 | 2.8 | 97.6 % | ≤ 60: 98.7 %; 54/93 vùng khớp 0px, còn lại ≤ 1px (riêng dòng copyright lệch ngang 2px) |

Cả hai khung dùng chung **một** file `index.html`; mobile là CSS mặc định,
desktop bật từ `64rem`, các mảnh minh hoạ dựng rời bật từ `90rem` (1440).
Gần như mọi dòng chữ khớp 0–1px theo `bbox.py --rows`; phần lệch còn lại chủ
yếu là khử răng cưa chữ và ảnh minh hoạ ghép từ mảnh.

Ảnh đối chiếu nằm trong `docs/comparison/<trang>/`. Tự kiểm trực tiếp: mở
`dev/<trang>-overlay.html` (bốn chế độ Code only / Overlay 50% / Figma only /
Slider — không JavaScript, nút là radio input đọc bằng `:has()`).

### Trang About (`about.html`)

Một file cho cả hai khung. Dùng lại header, highlights, stats, team, FAQ, logos,
banner, footer của Home (thêm modifier `--about` / `--dark`, Home không đổi
pixel nào). Khối mới: `page-hero`, `intro`, `gallery`, `reviews` (carousel),
`about-band` (nền tối dừng giữa hộp banner).

- **Ảnh video** `assets/img/about-video.png`: cắt từ export 1:1, xoá vòng play,
  tam giác và nhãn 1:45 bằng nội suy để CSS vẽ lại → **cần ảnh gốc từ khách**.
  Bốn ảnh `about-photo-1…4.png` cũng cắt từ export (1x).
- **Logo trên nền tối** `logo-*-dark.png`: tô lại màu #5E6080 [ĐO] trên kênh
  alpha của logo gốc (không có bản export tối).
- **Testimonials**: thẻ hai bên mờ 24.29% chỉ hiện ở desktop; chấm, mũi tên chỉ
  trang trí (không JS).
- **FAQ**: câu cuối của câu trả lời đầu chỉ có trong khung desktop → bọc trong
  `.faq__extra`, ẩn dưới 64rem. Link "Contact Me" chỉ có ở mobile.
- Ảnh đối chiếu: `docs/comparison/about/`, `docs/comparison/about-mobile/`.
  Overlay: `dev/about-overlay.html`, `dev/about-mobile-overlay.html`.

### Trang Services (`services.html`)

Một file cho cả hai khung. Dùng lại header, `page-hero`, `intro`, `steps`,
`checklist`, `banner`, footer (thêm modifier `--services`, Home và About không
đổi pixel nào, đã so lại cả hai). Khối mới: `accordion`.

- **Accordion dịch vụ** dùng `<details name="service">`: mở mục này thì mục kia
  đóng, không JS. Mũi tên là `up.png` xoay 180° khi đóng (khớp ảnh Figma). Link
  footer "Design / Development / Marketing" trỏ tới `services.html#design`…
- **Nội dung mục Development / Marketing khi mở**: Figma chỉ vẽ mục Design mở,
  nên chữ hai mục kia là chữ tạm → **cần khách gửi nội dung**.
- **"Deve-lopment", "Marke-ting"** ở mobile ngắt bằng `&shy;` (chỉ hiện gạch nối
  khi khung hẹp). Dưới 375 tiêu đề thu còn 28px để không đè nút mũi tên (`[ƯỚC]`).
- "Read More" ở khối How we work chỉ có trong khung mobile.
- Header/footer của Home và About giờ trỏ "Services" sang `services.html`.
- Ảnh đối chiếu: `docs/comparison/services/`, `docs/comparison/services-mobile/`.
  Overlay: `dev/services-overlay.html`, `dev/services-mobile-overlay.html`.

### Portfolio (`portfolio.html`)

- Khung `4_Portfolio_1_1440` (1440 × 3440): sai lệch TB **0.8/765**, **99.6 %**
  pixel lệch ≤ 30 (99.7 % ≤ 60). `regions.py`: mọi khối lệch 0–1px (1px là mép
  chữ do khác engine dựng chữ).
- Khung `4_Portfolio_1_375` (375 × 4656): TB 2.2/765, **98.6 %** ≤ 30, mọi khối
  lệch 0–1px. Figma mobile khác desktop: DDDone xếp trước Work Media, tag
  KeyBoard "Design" / DDDone "Branding", ảnh DDDone phóng rộng 570. HTML theo
  thứ tự mobile; desktop đổi chỗ 2 ô cùng cỡ bằng `position: relative`
  (`work--swap-r/-l`, chỉ khi "Show All"); tag theo khổ bằng `work__tag-m/-d`.
  Lọc vẫn theo hạng mục desktop (`data-cat`).
- Dùng lại `portfolio` (bộ lọc radio + `:has()`) qua modifier `portfolio--page`
  (nền sáng, thẻ `work--full` 1170×720 + `work--half` 570×416); banner/footer qua
  `banner--portfolio`, `site-footer--portfolio`. Component mới: `pagination`.
- 4 ảnh thẻ là ảnh của trang chủ (`Bitmap (4)/(2)1/(6)/(5).png`), Figma phóng/cắt
  bằng `object-fit: cover` — khớp gần tuyệt đối. **Ảnh HandP** chưa có asset:
  cắt từ ảnh export (`assets/img/portfolio-handp.png`, 570×416, xoá tag/tên
  bằng nội suy) — cần khách gửi ảnh gốc. Ảnh KeyBoard bị phóng 670 → 1170px nên
  hơi mờ — nên xin bản lớn.
- Phân trang là link tĩnh (`#work`), chưa có trang 2–5.
- Ảnh đối chiếu: `docs/comparison/portfolio/`, `docs/comparison/portfolio-mobile/`.
  Overlay: `dev/portfolio-overlay.html`, `dev/portfolio-mobile-overlay.html`.

## Không flexbox, không grid

Bố cục dựng bằng kỹ thuật trước thời flexbox: `float` + `calc()`, `flow-root`,
`inline-block` + `font-size: 0`, `line-height` + `vertical-align`,
`position: absolute`.

## Font

| Font Figma | Thay bằng (OFL) | Weight |
| --- | --- | --- |
| Epilogue | Epilogue (đúng font, OFL — không phải thay) | 400, 700, 800, 900 — bản variable `assets/fonts/epilogue-latin-wght-normal.woff2` |

Chrome đặt chân chữ Epilogue cao hơn Figma ~1px, nên `@font-face` dời baseline
xuống bằng `ascent-override: 80.25%` / `descent-override: 22.25%` (tổng giữ
nguyên 102.5%, chiều cao dòng không đổi). Đo trên cả 4 khung: 1.25% em là mức
tốt nhất, 1.75% trở lên làm lệch ngược lại.

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

Portfolio: 17 khổ 320 → 2560 + điện thoại xoay ngang 568/667/844 × 320: không
khổ nào cuộn ngang. Cảnh báo "chữ bị cắt" ở tag dự án là có chủ ý (pill 38px,
line-height 42px để hạ chữ 2px như Figma — giống trang chủ). Cùng breakpoint.

Services: 17 khổ 320 → 2560 + điện thoại xoay ngang 568/667/844 × 320: không
khổ nào cuộn ngang, không cảnh báo. Khổ 320 thử thêm trong trình duyệt (mở/đóng
accordion). Cùng breakpoint với Home, thêm một mốc `23.4375rem` (375) cho cỡ chữ
tiêu đề accordion.

About: 17 khổ 320 → 2560 + điện thoại xoay ngang 568/667/844 × 320: không khổ
nào cuộn ngang. Khổ < 500 kiểm thêm bằng iframe (Chrome headless không thu cửa
sổ dưới 500px). Cùng breakpoint với Home.

Home: đã kiểm 17 khổ 320 → 2560 (`responsive.py`): **không khổ nào cuộn ngang**.
Breakpoint: `48rem`, `64rem` (bố cục desktop), `75rem` (menu ngang), `80rem`,
`90rem` (minh hoạ dựng mảnh, đúng pixel 1440). Cảnh báo còn lại: link chữ
("Read More"…) cao 32px nhưng < 24px ở một chiều khi đứng trong dòng — chấp
nhận vì các vùng bấm cách nhau ≥ 24px.

## Còn cần từ phía khách

- SVG hoặc @2x cho các icon/ảnh ở mục "Icon cắt từ ảnh export".
- Trang About: ảnh gốc video (570×448, không có nút play) và 4 ảnh 270×208
  (bản @2x), logo bản trên nền tối.
- Trang Portfolio: ảnh gốc HandP (570×416 hoặc lớn hơn) và bản lớn của ảnh
  KeyBoard (≥ 1170×720).
- `assets/img/Portfolio Template (Community).zip` và vài ảnh export trùng
  không dùng tới — chờ chị xác nhận trước khi xoá/đổi tên sang kebab-case.

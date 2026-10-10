# Portfolio — thông số Figma

Nguồn: ảnh chụp panel Properties trong `~/Desktop/portfolio-desktop` (78 ảnh) và
`~/Desktop/portfolio-mobile` (55 ảnh). Toạ độ tương đối với frame. Font: Epilogue.
Header, hero (nền tối 400px), banner "Help To Build" và footer trùng pixel với
trang Services (so ảnh export: sai lệch TB 0.002/765) — xem
`docs/comparison/services/spec.md`; ở đây chỉ ghi phần riêng.

## Desktop `4_Portfolio_1_1440` (1440 × 3440)

| Layer | x | y | w | h | Font | Màu | Ghi chú |
| --- | --- | --- | --- | --- | --- | --- | --- |
| H1 "Portfolio" | — | 164 | — | 80 | H1 800 72/80 −2 center | White | như Services |
| Tab "Show All¹⁴ … Motion¹" | 433 [ĐO] | 466 [ĐO] | — | 32 | Text 400 16/32; số mũ Text_Small 14/24 | chọn: Text_Dark; còn lại Dark 64% | |
| Bitmap KeyBoard | 135 | 576 | 1170 | 720 | | | bo 6 |
| Tag "Branding" (pill) | 183 [ĐO] | 1120 [ĐO] | 102 | 38 | Text 400 16/32, chữ top 5 left 16 | Text_Dark trên `#FFFFFF` | bo 19 |
| "KeyBoard" | 183 | 1184 | — | 64 | H2 800 56/64 −1 | Text_Light | |
| Bitmap SOFA | 135 | 1328 | 570 | 416 | | | |
| Tag "Design" | 183 | 1584 [ĐO] | 84 | 38 | như trên | | |
| Bitmap Work Media | 735 | 1328 | 570 | 416 | | | |
| Tag "Illustration" | 783 | 1584 | 116 | 38 | | | |
| "Work Media" | 783 | 1645 | 244 | 48 | H3 800 40/48 | Text_Light | |
| Bitmap DDDone | 135 | 1776 | 570 | 416 | | | |
| Tag "Motion" | 183 | 2032 | 87 | 38 | | | chữ 55×32 |
| "DDDone" | 183 | 2093 | 161 | 48 | H3 800 40/48 | Text_Light | |
| Bitmap HandP | 735 | 1776 | 570 | 416 | | | |
| Tag "Branding" | 783 | 2032 | 102 | 38 | | | chữ 70×32 |
| "HandP" | 783 | 2093 | 133 | 48 | H3 800 40/48 | Text_Light | |
| Light/Button/Primary/Text "1…5" | 584 / 640 / 696 / 752 / 808 | 2272 | 48 | 48 | 900 14/100% upper, center, chữ top 18 | `#391400`; ô 1 nền `#EF6D58` chữ trắng | bo 6 [ĐO], bóng nhạt [ĐO] |
| Banner (Rectangle) | 135 | 2432 | 1170 | 544 | | `#EF6D58` | bo 6 |

## Mobile `4_Portfolio_1_375` (375 × 4656)

| Layer | x | y | w | h | Font | Màu | Ghi chú |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Polygon logo | — | — | 48 | 48 | | viền 5 `#EF6D58` | |
| Dark/Field/Dropdown | 23 | 432 [ĐO] | 329 | 48 | | `#FFFFFF`, viền 1 `#F3D1BF` | bo 6 |
| "Show All" | +16 | +37 (?) | 64 | 32 | Text 400 16/32 | Dark 64% | chữ đo x40 y449 |
| Triangle | +303 | +49 (?) | 10 | 6 | | `#EF6D58` | đo x326 y453 |
| Bitmap ×5 | 23 | 528 / 976 / 1424 / 1872 / 2320 | 329 | 416 | | | bước 448 |
| Tag (pill) | 51 [ĐO] | thẻ + 256 | 84… | 38 | Text 400 16/32 | | bo 19 |
| "KeyBoard" | 51 | 845 | 198 | 48 | H3 800 40/48 | Text_Light | |
| Phân trang | 51 [ĐO] | 2784 [ĐO] | 48 ×5 | 48 | như desktop | | |
| Banner | 23 | 2944 [ĐO] | 329 | — | | | như Services |

Khác desktop (Figma vẽ không nhất quán): mobile xếp DDDone (thẻ 3) trước Work
Media (thẻ 4); tag KeyBoard ghi "Design", DDDone ghi "Branding". Code theo
desktop vì float không đổi được thứ tự.

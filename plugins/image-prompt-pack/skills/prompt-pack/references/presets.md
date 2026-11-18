# Preset phong cách: R, S, C

Preset là điểm tựa để model tự chọn và phối cho từng ảnh, không phải biểu mẫu bắt buộc. Người dùng có thể gọi đúng tên preset hoặc đổi phong cách bằng lời. Toàn bộ 24 preset đang ở trạng thái **v0.1 chưa test** trên model thật.

Khi điền khung: thay mỗi `[biến]` bằng giá trị cụ thể, không để lại dấu ngoặc vuông trong prompt cuối. Giữ **tối đa một** cụm chỉ dẫn camera hoặc thiết bị (FR-010) và bỏ các cụm camera thừa trong khung. Chữ trong ảnh đặt trong ngoặc kép, kèm số lần xuất hiện.

## Bảng slot đa dạng hóa (FR-011)

Mỗi ảnh trong cùng pack chọn một giá trị khác cho từng slot; không lặp giá trị trong một pack.

| Slot | Giá trị gợi ý |
|---|---|
| Người | tuổi 20s, 30s, 40s, 50s, 60s trở lên; vóc dáng; nền tảng văn hóa khớp thị trường; kiểu tóc; trang phục (ghi rõ chất liệu) |
| Nơi | phòng khách, bếp, hành lang, ban công, quán cà phê, chợ, ga tàu, sân sau, trong xe, phòng làm việc nhỏ |
| Mùa hoặc giờ | buổi sáng mờ, trưa chói, hoàng hôn, mưa, tối đèn vàng, đèn huỳnh quang |
| Khung | ngang tầm mắt, hơi cúi, qua vai, cận tay, tele từ xa, cầm tay hơi nghiêng |
| Thiết bị | điện thoại, compact digicam, SLR phim 35mm, máy phim dùng một lần |

## Nhóm R: ảnh thật đời sống (12)

| ID | Tên | Dùng khi | Khung |
|---|---|---|---|
| R01 | Snapshot điện thoại | Ảnh đời thường, lifestyle cho blog hoặc mạng xã hội | `Candid phone photo of [person, age, clothing + fabric] [mid-action verb] in [specific room] with [2 mundane objects]. Shot on a recent smartphone main camera, handheld, eye level, slightly off-center. [Light source + direction]. Visible skin texture, unposed, not retouched, not cinematic. Sharp focus throughout.` |
| R02 | Phóng sự tài liệu | Ảnh hero, ảnh tư liệu về việc đang diễn ra | `Documentary photograph of [subject] [action] at [place], [time of day]. 35mm lens look, handheld, natural color balance, available light only, straight unstylized color. Slight motion in [moving element], unposed, everyone absorbed in what they are doing.` |
| R03 | Phim analog 35mm | Ảnh lifestyle, chân dung có hạt phim | `Photo of [subject] [action] in [setting]. Shot on 35mm color negative film (Kodak Portra 400 look), 50mm, soft natural window light from the left. Subtle film grain, natural color balance, small exposure imperfections.` |
| R04 | Street candid | Ảnh đường phố, người đi lại ngoài trời | `Street photo of [person] [walking/waiting/buying] on [specific street], [weather]. Shot from across the road with an 85mm lens look, subject unaware of the camera, other pedestrians partly cut by the frame edge, deep focus.` |
| R05 | UGC cầm sản phẩm | Người cầm vật trong tay. Nếu sản phẩm có thiết kế thật thì đó là mockup: chỉ dùng khi người dùng yêu cầu, kèm Reference (anti-slop mục 5) | `Close-up phone photo of a hand holding [product] in [kitchen/desk/couch]. [How the hand grips it: thumb on top, fingers wrapped around]. Daylight from a window, background in focus with [2 mundane items]. Real skin texture, short unpolished nails.` |
| R06 | Sản phẩm trung thực, studio nhẹ | Chỉ khi người dùng yêu cầu mockup ở vị trí đó; kèm Reference và ghi chú ghép thiết kế thật | `Product photo of [product, material, color]. Placed on [surface] against [plain backdrop]. Soft window light from the left, gentle natural shadow, true-to-life colors. Only the product on the surface, clean and unlabeled.` |
| R07 | Flash trực diện kiểu đêm | Ảnh buổi tối, nhóm bạn, sự kiện nhỏ | `Photo with on-camera flash of [group, age] at [place], [night]. Direct flash, harsh falloff, red-eye left uncorrected, background dark with ambient lights, 2000s compact digicam look.` |
| R08 | Chân dung môi trường | Người trong nơi làm việc, bài về nghề | `Environmental portrait of [person] in [workplace], [tools visible]. 35mm lens look, natural light from [window], shot slightly below eye level, wrinkles and sun exposure visible, honest unglamorized look.` |
| R09 | Bàn ăn, bàn làm việc (still life) | Ảnh chia sẻ, OG, góc làm việc hoặc ăn uống nhìn từ trên | `Overhead photo of [meal or desk items] on [table], [crumbs and a used napkin], daylight from the side, items slightly misaligned, steam visible if hot.` |
| R10 | Chuyển động | Người đang làm một việc cụ thể | `Photo of [subject] [verb in motion: running for the bus / pouring tea / spinning child] at [place]. 1/60s panning look: subject sharp, background streaked, a small blur in the limbs. [Light]. Candid, off-center.` |
| R11 | Đêm, ánh sáng thấp | Ảnh buổi tối, đường phố, quán nhỏ | `Photo at night of [subject] at [place] lit only by [streetlight / shop sign / phone screen]. Slight noise, soft focus on edges, highlights slightly blown.` |
| R12 | Gia đình, nhóm | Nhóm người, khoảnh khắc vui | `Group photo of [3 to 5 people with ages] at [setting], mid-laugh, one person half out of frame, someone blinking, phone-camera look, flat daylight.` |

## Nhóm S: phong cách thủ công cho minh họa (8)

| ID | Tên | Dùng khi | Khung |
|---|---|---|---|
| S01 | Risograph 2 màu | Minh họa khái niệm, bìa phần, infographic đơn giản | `Risograph print of [subject], two spot colors [color A hex] and [color B hex], visible misregistration, grainy halftone, paper texture, flat shapes.` |
| S02 | Cắt dán giấy | Minh họa ý tưởng cần hình gợi, bảng so sánh đơn giản | `Hand-cut paper collage of [subject], layered torn paper edges, visible glue wrinkles, limited palette of [3 colors], flat top-down view.` |
| S03 | Ảnh slide 1970s | Ảnh hoài niệm, bài về kỷ niệm, gia đình | `Slide photo of [subject], 1970s Kodachrome look, warm reds, slight fade and dust specks, soft vignetting, awkward family-album framing.` |
| S04 | Linocut | Minh họa mạnh, ảnh bìa theo chủ đề thủ công | `Linocut print of [subject], bold carved lines, uneven ink coverage, two colors on cream paper, visible chisel marks.` |
| S05 | Quảng cáo in cổ halftone | Thumbnail hoặc banner có tiêu đề rất ngắn; chữ tiếng Việt dài thêm bằng thiết kế | `Vintage magazine ad of [subject], halftone dot pattern, slight color shift, off-register print, paper yellowing, headline text "[exact text]" appears once.` |
| S06 | Sketchbook màu nước | Minh họa nhẹ nhàng, bài hướng dẫn, bài cảm xúc | `Watercolor sketchbook page of [subject], loose washes, pencil guidelines visible, paper buckling, unfinished edges.` |
| S07 | Stop-motion đất sét | Minh họa vui, nội dung giải trí | `Stop-motion clay scene of [subject], fingerprints on clay, slightly uneven lighting, miniature set on a desk.` |
| S08 | Poster lụa (screenprint) | Poster hoặc thumbnail có tiêu đề ngắn | `Screenprint poster of [subject], 3 flat colors, overprint creating a 4th color, crisp edges with slight ink bleed, textured paper.` |

## Nhóm C: nhân vật nhất quán qua nhiều ảnh (4)

| ID | Tên | Dùng khi | Khung |
|---|---|---|---|
| C01 | Tạo character sheet | Ban đầu, khi cần một nhân vật lặp lại qua nhiều ảnh; chọn ảnh tốt nhất làm tham chiếu chính | `Reference sheet of [name]: [age, face shape, hair, skin tone, build], wearing [outfit + fabric], front, 3/4 and profile, neutral plain background, soft even light.` |
| C02 | Đưa vào cảnh mới | Đặt nhân vật từ C01 vào một cảnh khác; kèm Reference của C01 | `Image 1 = character reference. Same character as image 1: [defining details]. Now [new action] at [place]. Keep the face and proportions exactly as in image 1, same design throughout.` |
| C03 | Đổi trang phục hoặc một vật | Giữ nhân vật, đổi đúng một chi tiết mỗi lượt | `Image 1 = character reference. Change only [item] to [new item]. Keep face, pose, background, lighting and framing identical. No added text or logos.` |
| C04 | Kiểm tra trôi | Sau khoảng ba lượt chỉnh sửa, so với ảnh gốc. Không có khung sinh ảnh; nếu trôi thì làm lại từ ảnh gốc | `Compare with image 1: eyes, nose, hair and skin tone match.` |

## Phối preset

- Ảnh bìa bài blog: R02 hoặc R08. Ảnh đời thường: R01 hoặc R10.
- Minh họa khái niệm trong bài: S01, S02 hoặc S06, xen kẽ để không lặp một phong cách.
- Nhân vật lặp qua nhiều ảnh: C01 tạo nhân vật, C02 đưa vào cảnh mới, C03 đổi trang phục, C04 kiểm tra trôi.
- Pack đa dạng: xoay R và S trong cùng pack, mỗi ảnh một khung khác; không dùng cùng một preset cho mọi ảnh.

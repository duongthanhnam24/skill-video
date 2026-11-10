# Zombie Survival Video Series — kiến trúc dự án

Dự án sản xuất prompt (ảnh + video) cho một series video hoạt hình 2D tận thế-zombie, tiếng Việt, dùng pipeline 8 state (STATE 1→8: script/cast → character sheets → chapter map → start frames → animation chapters → thumbnails → branding → export). Đây KHÔNG phải code — toàn bộ là file `.md` chứa prompt và nội dung kịch bản.

## Hai "engine" dùng chung (bản thiết kế pipeline, tái sử dụng cho mọi dự án con)

- **`ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md`** — nhánh **narrator-only**: một người kể chuyện off-screen duy nhất, nhân vật KHÔNG nói/không lip-sync, cast cố định `@BEANIE` + `@GLASSES`.
- **`ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md`** — nhánh **dialogue-cast**: nhân vật nói trực tiếp trên màn hình có lip-sync, cast + voice DNA resolve lại từ đầu cho từng dự án (không cố định tên).
- Cả hai cùng cấu trúc STATE 1-8, cùng LOCKED STYLE DNA, cùng filter-safe vocabulary — chỉ khác ở cách xử lý nhân vật/âm thanh. Chọn engine nào tùy việc dự án cần kể chuyện qua narrator hay qua đối thoại nhân vật.
- **`.claude/skills/directing-zombie-dialogue-survival-videos/SKILL.md`** — bản Skill (có frontmatter `name`/`description` để Claude Code tự trigger) đóng gói lại đúng nội dung của `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md`. Đây là **file riêng, tạo thủ công**, không tự động đồng bộ — nếu sửa `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` thì phải tự sửa thêm bản Skill này nếu muốn nó cũng được cập nhật.
- Không có bản Skill tương ứng cho nhánh ANIMATION_ENGINE (narrator-only) — nếu cần, phải tạo mới theo đúng mẫu.

## Quy ước đặt tên file trong thư mục này

- `ALL_CAPS_SNAKE_CASE.md` = engine (bản thiết kế pipeline) hoặc output sản xuất thật của một dự án con cụ thể.
- `lowercase-kebab-case.md` = tài liệu tham khảo/thư viện dùng chung, không gắn với một dự án con nào (ví dụ prompt camera movement).

## Các dự án con đã chạy qua pipeline (output thật, không phải engine)

- **`ZOMBIE_SUBWAY_PART1_SCRIPT.md`** — kịch bản gốc (STATE 1, season planning) cho dự án **"Zombie Subway"**, Phần 1 = 30 phút chia 3 tập ~10 phút/tập. Cast: Lâm (@LAM), Hạ (@HA), Đức (@DUC)... Dùng nhánh **dialogue-cast**.
- **`result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md`** — output pipeline đầy đủ STATE 1-8 cho riêng **Episode 1** của Phần 1 trên (82 chapter × 8 giây ≈ 11 phút). Sinh ra từ `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` + script trên. File sản xuất hoàn chỉnh (kết quả cuối) nên nằm riêng trong `result/`.
- **`ZOMBIE_FLOOD_LINE_PART1_PIPELINE_OUTPUT.md`** — một dự án con **khác, độc lập**: **"THE FLOOD LINE"** (hai nhân vật Cole và Ivy, một ga tàu điện ngầm bị ngập nước), kể qua narrator off-screen → dùng nhánh **narrator-only** (`ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md`). Phần 1 = 90 chapter ≈ 12 phút (script chỉ đủ dài cho 12/30 phút dự kiến, phần còn lại sẽ viết thêm ở các Part sau). File này hiện **chưa** được chuyển vào `result/` — chỉ chuyển khi được yêu cầu rõ.

Hai dự án con "Zombie Subway" và "The Flood Line" **không liên quan nhau** — khác cast, khác engine nhánh, khác câu chuyện. Đừng trộn ngữ cảnh giữa hai dự án này khi đọc/sửa file.

## Tài liệu tham khảo dùng chung (không phải engine, không phải output)

- **`camera-movement-ai.md`** — thư viện 46 block prompt "Camera: ..." (pan/tilt, zoom, dolly, drone, specials...) để ghép thêm vào phần SHOTS của STATE 5 khi cần mô tả chuyển động camera cụ thể hơn. Tự nó không đủ thành một prompt hoàn chỉnh (thiếu shot size, ánh sáng, bối cảnh).

## Skill ngoài dự án đã góp phần tạo nội dung (không nằm trong thư mục này)

> Hai skill dưới đây là **skill public phát hành trên mạng**, không phải tự viết cho dự án này và **không** kèm theo repo. Chúng được cài ở cấp global trong thư mục skill của Claude Code trên máy từng người — thường là `<thư-mục-home-của-user>/.claude/skills/<tên-skill>` (ví dụ `~/.claude/skills/...`). Tên user trong đường dẫn khác nhau tùy máy, đừng giả định một tên cố định; máy nào chưa cài thì phải tải lại bản public về trước khi dùng.
>
> Nguồn public để tải lại:
> - `cinematic-video-prompt-skill`: https://github.com/Rylaispirit/cinematic-video-prompt-skill — `git clone` vào `~/.claude/skills/`.
> - `screenwriting-master`: https://github.com/Shanyin-ai/shanyin-screenwriting-master — trong repo có file `.skill` (là một zip), giải nén được thư mục skill rồi đặt vào `~/.claude/skills/`.

- **`screenwriting-master` (山音超级编剧大师)** — Skill global (public, cài ở `~/.claude/skills/screenwriting-master`), KHÔNG phải viết riêng cho dự án zombie này — là công cụ biên kịch đa định dạng (short film, feature, series...) dùng chung cho nhiều dự án khác nhau của user.
  - Đã được dùng để viết **`ZOMBIE_SUBWAY_PART1_SCRIPT.md`**: nhận premise ban đầu ("mặt trời phát bức xạ lạ biến người thành zombie, người sống sót trốn trong ga tàu điện ngầm...") rồi phát triển ra toàn bộ season planning Phần 1 — logline, tóm tắt, nhân vật (Lâm/Hạ/Đức/An...) với Ghost/Lie/Want/Need/Arc, tiền sử, thế giới quan.
  - Script này **sau đó** mới được đưa vào làm input cho `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` ở STATE 1 (nhánh "tôi đã có script hoàn chỉnh" — engine không tự sáng tác lại, chỉ ingest và chuyển thành prompt ảnh/video).
  - Vì đây là skill global, không nằm trong thư mục `skill-video`, nên nó **không được version-control cùng dự án này** — nếu cần viết tiếp Part 2/3 của Zombie Subway theo đúng cách đã làm Part 1, phải gọi lại skill `screenwriting-master` đó (không phải hai engine zombie trong thư mục này, hai engine đó chỉ xử lý từ-script-đã-có-sẵn-trở-đi).
  - `ZOMBIE_FLOOD_LINE_PART1_PIPELINE_OUTPUT.md` thì **không** qua skill này — script của nó được chính `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md` tự sáng tác ở STATE 1 (nhánh "premise hoặc không có gì"), nguồn gốc setup lấy từ một file docx tải về (`ZOMBIE SURVIVAL ANIMATION ENGINE.docx`), không liên quan `screenwriting-master`.

- **`cinematic-video-prompt-skill`** (tên skill: `cinematic-video-prompt`) — Skill global (public, cài ở `~/.claude/skills/cinematic-video-prompt-skill`) — "từ điển kỹ thuật quay phim" cho prompt ảnh/video AI (góc máy, ánh sáng, bố cục, màu, mood, công thức ghép prompt, lỗi model hay gặp).
  - Chính là skill được `camera-movement-ai.md` tham chiếu tới (dòng mở đầu file: "cần ghép thêm các khối đó, xem skill `cinematic-video-prompt-skill`, để ra prompt hoàn chỉnh") — `camera-movement-ai.md` chỉ là khối "Camera movement" đơn lẻ, còn shot size/ánh sáng/bố cục/màu phải lấy từ skill này.
  - Đã dùng **thật** khi viết STATE 5 của `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` — ghi rõ trong file đó (dòng trạng thái cuối): "Camera đã chuẩn hoá theo `camera-movement-ai.md` + `cinematic-video-prompt-skill`".
  - Cũng là skill global, không nằm trong `skill-video` — nếu viết tiếp các chapter/part sau mà cần chuẩn hoá camera/ánh sáng/màu giống các chapter trước, phải gọi lại skill này (không chỉ dựa vào `camera-movement-ai.md` một mình).

## Điểm thiết kế quan trọng cần nhớ: CONTINUITY INPUT (STATE 4)

Mỗi prompt start-frame ở STATE 4 (từ chapter thứ 2 trở đi) phải có một dòng **CONTINUITY INPUT** ghi rõ liệu chapter này có cần đính kèm thêm end-frame thật của chapter trước không:
- `true match-cut` → sau khi chapter trước đã có video thật, tách end-frame thật của nó, đính kèm thêm (không thay thế) vào lúc generate ảnh start-frame cho chapter này.
- `intentional scene/beat change` → không cần, chỉ dùng mô tả chữ + ảnh tham chiếu nhân vật.

Đây là cơ chế **best-effort giảm giật hình giữa 2 chapter**, không phải nối liền tuyệt đối — mỗi lần tái tạo ảnh/video là một lần "tái tưởng tượng", sai lệch có thể tích lũy dần qua nhiều chapter (xem HOUSE RULES trong từng engine). End-frame chỉ dùng ở STATE 4 để tạo ảnh start-frame mới; KHÔNG đính kèm lại end-frame ở STATE 5 (tạo video) — lúc đó chỉ cần ảnh start-frame (đã tạo xong) + ảnh tham chiếu nhân vật.

Cơ chế này đã được thêm vào cả hai engine và retrofit vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` (82 chapter, suy ra true-match-cut/scene-change từ các dòng `MATCH-CUT HANDOFF` đã có sẵn ở STATE 5 của từng chapter).

## Điểm thiết kế quan trọng cần nhớ: COLD OPEN HOOK + AUDIO FLOOR + voiceover ngôi 1 (STATE 1 & STATE 5)

Vấn đề gốc phát hiện khi review Tập 1 Zombie Subway: kịch bản dialogue-cast viết theo kỷ luật điện ảnh "show, don't tell" (skill `screenwriting-master` cấm nhân vật dùng thoại giải thích setup) → khi lên video AI ngắn, phần mở đầu và nhiều beat hành động/chuyển cảnh **không có lời nào**, xem như kịch câm; người xem bị thả vào giữa cảnh, không biết nhân vật chính là ai / thế giới gì. Ban đầu Tập 1 có **55/82 chapter không có tiếng người** và không dùng narrator.

Ba nguyên tắc đã thêm để chống việc này (áp dụng chủ yếu cho nhánh **dialogue-cast**, vì nhánh narrator-only vốn đã có người kể phủ mọi chapter):
- **COLD OPEN HOOK (STATE 1):** ~30–45 giây đầu phải định hướng người xem — ai là nhân vật chính, thế giới/stakes là gì — không drop vào giữa hành động câm. Nếu script gốc mở đầu im lặng thì bù ở **tầng AUDIO** (không viết lại cảnh), bằng narrator.
- **AUDIO FLOOR (STATE 5):** không chapter nào là phim câm. Mỗi chapter phải có ít nhất một trong: thoại nhân vật / voiceover off-screen / SFX dồn có chủ đích (đánh nhau, đám đông, rượt đuổi). Beat tĩnh/chuyển cảnh không thoại thì phủ voiceover. Ngoại lệ được phép câm-lời (phải đánh dấu cố ý): pha hành động đã đầy SFX, tiếng đám đông, cú fade kết.
- **Voiceover ngôi 1 của nhân vật chính:** narrator không bắt buộc là giọng tài liệu ngôi 3 trung lập — có thể là **một nhân vật tự sự ngôi 1, off-screen** (ví dụ Lâm: "Tên tôi là Lâm..."). Phải resolve **một voice profile riêng cho chế độ tự sự** (cùng người nhưng chậm/riêng tư/sát mic hơn giọng trong cảnh), và VO luôn **off-screen, KHÔNG lip-sync**, không nói đè lên thoại nhân vật trong cùng chapter.

Đã nhúng vào `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` (STATE 1 / STATE 5 / HOUSE RULES) **và** bản Skill `.claude/skills/directing-zombie-dialogue-survival-videos/SKILL.md` (sửa tay, vì không tự đồng bộ), thêm bản rút gọn (cold open orient + AUDIO FLOOR) vào `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md`. Đã retrofit vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md`: thêm `@LAM-VO` (voiceover ngôi 1 của Lâm) vào 41 chapter, kéo số chapter câm-lời từ 55 xuống **10/82** (đều cố ý: Ch28–36 hành động, Ch53 đám đông, Ch82 fade). Vết thương "em trai" (Ghost của Lâm) cố ý **chưa** gieo ở Tập 1 — để dành hé lộ gần cao trào tập/phần sau.

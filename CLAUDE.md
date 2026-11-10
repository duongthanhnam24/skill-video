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

## Điểm thiết kế quan trọng cần nhớ: CONTINUITY INPUT (STATE 4)

Mỗi prompt start-frame ở STATE 4 (từ chapter thứ 2 trở đi) phải có một dòng **CONTINUITY INPUT** ghi rõ liệu chapter này có cần đính kèm thêm end-frame thật của chapter trước không:
- `true match-cut` → sau khi chapter trước đã có video thật, tách end-frame thật của nó, đính kèm thêm (không thay thế) vào lúc generate ảnh start-frame cho chapter này.
- `intentional scene/beat change` → không cần, chỉ dùng mô tả chữ + ảnh tham chiếu nhân vật.

Đây là cơ chế **best-effort giảm giật hình giữa 2 chapter**, không phải nối liền tuyệt đối — mỗi lần tái tạo ảnh/video là một lần "tái tưởng tượng", sai lệch có thể tích lũy dần qua nhiều chapter (xem HOUSE RULES trong từng engine). End-frame chỉ dùng ở STATE 4 để tạo ảnh start-frame mới; KHÔNG đính kèm lại end-frame ở STATE 5 (tạo video) — lúc đó chỉ cần ảnh start-frame (đã tạo xong) + ảnh tham chiếu nhân vật.

Cơ chế này đã được thêm vào cả hai engine và retrofit vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` (82 chapter, suy ra true-match-cut/scene-change từ các dòng `MATCH-CUT HANDOFF` đã có sẵn ở STATE 5 của từng chapter).

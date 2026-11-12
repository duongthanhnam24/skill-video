# Zombie Survival Video Series — kiến trúc dự án

> Dự án sản xuất **prompt** (ảnh + video), KHÔNG phải code. Toàn bộ repo là file `.md` chứa prompt và kịch bản cho một series video hoạt hình 2D tận thế-zombie, tiếng Việt.

## 0. Đọc nhanh (TL;DR)

- Mọi dự án con đi qua **pipeline 8 state** cố định: `STATE 1 script/cast → 2 character sheets → 3 chapter map → 4 start frames → 5 animation chapters → 6 thumbnails → 7 branding → 8 export`.
- Có **2 engine nhánh** (narrator-only / dialogue-cast) — chọn 1 theo cách dự án kể chuyện. Xem [§1](#1-hai-engine-dùng-chung).
- Có **2 dự án con output thật**, không liên quan nhau — xem [§2](#2-dự-án-con-output-thật). Đừng trộn ngữ cảnh giữa chúng.
- Có **2 cơ chế thiết kế bắt buộc tuân theo** khi sinh/sửa nội dung — xem [§6](#6-cơ-chế-thiết-kế-bắt-buộc). Đọc trước khi viết STATE 1/4/5 cho bất kỳ dự án nào.
- Có **2 skill global** (không nằm trong repo, không version-control) được dùng làm input — xem [§4](#4-skill-ngoài-dự-án-global).
- Có **2 skill project-scoped** (`writing/dialogue`, `writing/fiction-writing-prose`) đã được **wire vào cả hai engine** ở STATE 1 + STATE 5 để chấm/sửa chất lượng dialogue và prose — xem [§5](#5-skill-trong-dự-án-project-scoped).

## 1. Hai engine dùng chung

Bản thiết kế pipeline, tái sử dụng cho mọi dự án con. Cả hai cùng cấu trúc STATE 1-8, cùng LOCKED STYLE DNA, cùng filter-safe vocabulary — chỉ khác cách xử lý nhân vật/âm thanh.

| Engine | Nhánh | Đặc điểm | Skill tương ứng |
|---|---|---|---|
| `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md` | **narrator-only** | Một người kể chuyện off-screen duy nhất, nhân vật KHÔNG nói/không lip-sync, cast cố định `@BEANIE` + `@GLASSES` | *(chưa có — xem dưới)* |
| `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` | **dialogue-cast** | Nhân vật nói trực tiếp trên màn hình, có lip-sync, cast + voice DNA resolve lại từ đầu cho từng dự án | `.claude/skills/directing-zombie-dialogue-survival-videos/SKILL.md` |

⚠️ **Skill không tự đồng bộ với engine.** Skill dialogue-cast ở trên là file riêng, tạo thủ công, đóng gói lại nội dung của `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md`. Sửa engine thì phải tự sửa thêm skill nếu muốn skill cũng cập nhật. Nhánh ANIMATION_ENGINE (narrator-only) chưa có skill tương ứng — nếu cần, phải tạo mới theo đúng mẫu của skill dialogue-cast.

## 2. Dự án con (output thật)

Hai dự án dưới đây **không liên quan nhau** — khác cast, khác nhánh engine, khác câu chuyện. **Đừng trộn ngữ cảnh** giữa chúng khi đọc/sửa file.

| Dự án | File | Engine | Trạng thái |
|---|---|---|---|
| **Zombie Subway** | `ZOMBIE_SUBWAY_PART1_SCRIPT.md` — kịch bản gốc STATE 1, Phần 1 = 30 phút / 3 tập ~10 phút. Cast: Lâm `@LAM`, Hạ `@HA`, Đức `@DUC`... | dialogue-cast | script gốc |
| | `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` — output STATE 1-8 đầy đủ cho Episode 1 (83 chapter × 8s ≈ 11 phút, gồm Chapter 0 cold-open + Chapter 1–82 gốc) | dialogue-cast | **hoàn chỉnh**, đã nằm trong `result/` |
| **The Flood Line** | `ZOMBIE_FLOOD_LINE_PART1_PIPELINE_OUTPUT.md` — Cole & Ivy, ga tàu điện ngầm ngập nước. Phần 1 = 90 chapter ≈ 12 phút (script mới đủ dài cho 12/30 phút dự kiến) | narrator-only | chưa chuyển vào `result/` — **chỉ chuyển khi được yêu cầu rõ** |

## 3. Tài liệu tham khảo dùng chung

Không phải engine, không phải output — thư viện/checklist dùng chung cho mọi dự án con.

| File | Dùng khi nào | Ghi chú |
|---|---|---|
| `camera-movement-ai.md` | Cần mô tả chuyển động camera cụ thể hơn ở STATE 5 (phần SHOTS) | 46 block prompt "Camera: ..." (pan/tilt/zoom/dolly/drone...). Tự nó KHÔNG đủ thành prompt hoàn chỉnh — thiếu shot size, ánh sáng, bối cảnh, phải ghép thêm từ skill `cinematic-video-prompt-skill` (xem §4). |
| `story-bible-continuity-toolkit.md` | Dự án con có **nhiều Part/Episode** (không áp dụng cho video đơn lẻ) | Part A "Story Bible" (entities, canon facts, timeline, thread tracker) điền ở STATE 1; Part B "Knowledge & Continuity Tracker" (ai biết gì, state từng nhân vật) tra cứu ở STATE 4. Bổ sung cho CONTINUITY INPUT ở §6.1 — toolkit này lo continuity **thông tin/trạng thái**, CONTINUITY INPUT lo continuity **hình ảnh**. Cả hai engine đã tham chiếu file này ở STATE 1/STATE 4. |

## 4. Skill ngoài dự án (global)

> Hai skill dưới đây là **skill public phát hành trên mạng**, không tự viết cho dự án này, **không kèm theo repo**. Cài ở cấp global trong thư mục skill của Claude Code trên từng máy — thường `<home>/.claude/skills/<tên-skill>` (ví dụ `~/.claude/skills/...`). Máy nào chưa cài phải tải lại bản public trước khi dùng — đừng giả định tên user trong path.

| Skill | Nguồn tải lại | Vai trò trong dự án này |
|---|---|---|
| `screenwriting-master` (山音超级编剧大师) | https://github.com/Shanyin-ai/shanyin-screenwriting-master — repo có file `.skill` (zip), giải nén đặt vào `~/.claude/skills/` | Công cụ biên kịch đa định dạng dùng chung nhiều dự án, **không riêng cho zombie**. Đã dùng để viết `ZOMBIE_SUBWAY_PART1_SCRIPT.md` (premise → season planning: logline, nhân vật với Ghost/Lie/Want/Need/Arc...). Script này sau đó mới đưa vào `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` ở STATE 1 (nhánh "đã có script hoàn chỉnh"). Cần viết tiếp Part 2/3 Zombie Subway → phải gọi lại skill này, không phải engine. **The Flood Line KHÔNG qua skill này** — script của nó do `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md` tự sáng tác ở STATE 1 (nhánh premise-only), gốc setup lấy từ file docx tải về. |
| `cinematic-video-prompt-skill` (tên skill: `cinematic-video-prompt`) | https://github.com/Rylaispirit/cinematic-video-prompt-skill — `git clone` vào `~/.claude/skills/` | "Từ điển kỹ thuật quay phim" (góc máy, ánh sáng, bố cục, màu, công thức ghép prompt). Là skill mà `camera-movement-ai.md` tham chiếu tới. Đã dùng thật khi viết STATE 5 của `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md`. Viết tiếp chapter/part sau cần chuẩn hoá camera/ánh sáng/màu giống trước → phải gọi lại skill này, không chỉ dựa `camera-movement-ai.md` một mình. |

## 5. Skill trong dự án (project-scoped)

Khác với §4 — hai skill dưới đây nằm **trong repo** (`.claude/skills/writing/`), version-controlled cùng dự án, không phải cài global. Đã **wire thật** vào pipeline (không chỉ ghi chú), gọi tại STATE 1 và STATE 5 của cả hai engine để chấm/sửa chất lượng dialogue và prose trước khi chốt.

| Skill | Dùng ở đâu | Vai trò |
|---|---|---|
| `.claude/skills/writing/dialogue/SKILL.md` | STATE 1 (script invented từ premise, nhánh dialogue-cast) + STATE 5 (mọi dòng DIALOGUE mới thêm/sửa) | Chẩn đoán giọng nhân vật giống nhau (same-voice), thiếu subtext — chỉ áp dụng cho `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` vì nhánh narrator-only không có nhân vật nói. Với script dán sẵn (pasted), chỉ chạy **diagnostic-only** — report, không tự sửa (engine cam kết không rewrite dialogue dán sẵn). |
| `.claude/skills/writing/fiction-writing-prose/SKILL.md` | STATE 1 (toàn bộ script/narration, cả 2 engine) + STATE 5 (mọi dòng NARRATION mới thêm/sửa) | Chấm voice/POV/rhythm/"render-don't-explain" cho narration/VO — áp dụng cả 2 engine vì cả narrator-only và first-person VO của dialogue-cast đều là văn xuôi tự sự. |

Đã sửa tay vào: `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md`, `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md`, và `.claude/skills/directing-zombie-dialogue-survival-videos/SKILL.md` (không tự đồng bộ — xem §1). Chưa retrofit vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` hay `ZOMBIE_FLOOD_LINE_PART1_PIPELINE_OUTPUT.md` (output cũ, viết trước khi 2 skill này được wire) — chỉ áp dụng cho nội dung viết/sửa **từ nay về sau**.

## 6. Cơ chế thiết kế bắt buộc

Hai cơ chế này đã nhúng vào cả hai engine (và skill dialogue-cast, sửa tay) — khi sinh/sửa nội dung STATE 1/4/5 cho bất kỳ dự án con nào, phải tuân theo, không chỉ coi là ghi chú lịch sử.

### 6.1 CONTINUITY INPUT (STATE 4)

Mỗi prompt start-frame ở STATE 4 (từ chapter thứ 2 trở đi) phải có dòng **CONTINUITY INPUT** ghi rõ chapter này cần đính kèm end-frame thật của chapter trước không:

| Giá trị | Hành động |
|---|---|
| `true match-cut` | Chapter trước đã có video thật → tách end-frame thật, **đính kèm thêm** (không thay thế) khi generate ảnh start-frame cho chapter này |
| `intentional scene/beat change` | Không cần — chỉ dùng mô tả chữ + ảnh tham chiếu nhân vật |

- Đây là cơ chế **best-effort giảm giật hình giữa 2 chapter**, không phải nối liền tuyệt đối — mỗi lần tái tạo ảnh/video là một lần "tái tưởng tượng", sai lệch tích lũy dần (xem HOUSE RULES trong từng engine).
- End-frame chỉ dùng ở **STATE 4** để tạo ảnh start-frame mới. **KHÔNG** đính kèm lại end-frame ở STATE 5 (tạo video) — STATE 5 chỉ cần ảnh start-frame đã tạo + ảnh tham chiếu nhân vật.
- Đã retrofit vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md` (82 chapter, suy ra từ dòng `MATCH-CUT HANDOFF` có sẵn ở STATE 5).

### 6.2 COLD OPEN HOOK + AUDIO FLOOR + voiceover ngôi 1 (STATE 1 & STATE 5)

**Vấn đề gốc** (phát hiện khi review Tập 1 Zombie Subway): kịch bản dialogue-cast viết theo kỷ luật "show, don't tell" (skill `screenwriting-master` cấm thoại giải thích setup) → lên video AI ngắn, mở đầu và nhiều beat hành động/chuyển cảnh **không có lời nào**. Người xem bị thả vào giữa cảnh, không biết nhân vật chính là ai / thế giới gì. Ban đầu Tập 1 có **55/82 chapter không có tiếng người**, không dùng narrator.

Ba quy tắc chống việc này (áp dụng chủ yếu cho nhánh **dialogue-cast** — narrator-only vốn đã có người kể phủ mọi chapter):

- **COLD OPEN HOOK (STATE 1):** ~30–45 giây đầu phải định hướng người xem (ai là nhân vật chính, thế giới/stakes là gì), không drop vào giữa hành động câm. Script gốc mở đầu im lặng → bù ở tầng **AUDIO** (không viết lại cảnh), bằng narrator.
- **AUDIO FLOOR (STATE 5):** không chapter nào là phim câm. Mỗi chapter phải có ≥1 trong: thoại nhân vật / voiceover off-screen / SFX dồn có chủ đích (đánh nhau, đám đông, rượt đuổi). Beat tĩnh/chuyển cảnh không thoại → phủ voiceover. Ngoại lệ câm-lời phải **đánh dấu cố ý** (pha hành động đầy SFX, tiếng đám đông, fade kết).
- **Voiceover ngôi 1 của nhân vật chính:** narrator không bắt buộc là giọng tài liệu ngôi 3 — có thể là nhân vật tự sự ngôi 1, off-screen (ví dụ Lâm: "Tên tôi là Lâm..."). Phải resolve voice profile riêng cho chế độ tự sự (cùng người nhưng chậm/riêng tư/sát mic hơn giọng trong cảnh). VO luôn **off-screen, KHÔNG lip-sync**, không nói đè lên thoại nhân vật trong cùng chapter.

**Đã retrofit** vào `result/ZOMBIE_SUBWAY_EP1_PIPELINE_OUTPUT.md`: thêm `@LAM-VO` vào 41 chapter, kéo chapter câm-lời từ 55 xuống **10/82** (đều cố ý: Ch28–36 hành động, Ch53 đám đông, Ch82 fade). Vết thương "em trai" (Ghost của Lâm) cố ý **chưa gieo** ở Tập 1 — để dành hé lộ gần cao trào tập/phần sau.

## 7. Quy ước đặt tên file

| Pattern | Ý nghĩa |
|---|---|
| `ALL_CAPS_SNAKE_CASE.md` | Engine (bản thiết kế pipeline) hoặc output sản xuất thật của một dự án con cụ thể |
| `lowercase-kebab-case.md` | Tài liệu tham khảo/thư viện dùng chung, không gắn dự án con nào |

## 8. Việc nên / không nên làm

- **Nên** chọn engine theo cách dự án kể chuyện (narrator vs dialogue), không trộn lẫn cast/voice DNA giữa hai nhánh.
- **Nên** áp CONTINUITY INPUT (§6.1) cho mọi start-frame từ chapter 2 trở đi, và AUDIO FLOOR (§6.2) cho mọi chapter STATE 5 — kể cả khi viết thêm Part/Episode mới.
- **Nên** chạy skill project-scoped `writing/dialogue` + `writing/fiction-writing-prose` (§5) ở STATE 1 và STATE 5 cho mọi dialogue/narration mới — kể cả khi viết thêm Part/Episode mới, không chỉ lúc tạo project lần đầu.
- **Nên** gọi lại skill global đúng vai trò (`screenwriting-master` để viết/viết tiếp script; `cinematic-video-prompt-skill` để chuẩn hoá camera/ánh sáng/màu) thay vì tự suy diễn lại từ hai engine.
- **Không** trộn ngữ cảnh giữa "Zombie Subway" và "The Flood Line" — hai dự án độc lập, khác cast, khác engine.
- **Không** sửa `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md` mà quên sửa `.claude/skills/directing-zombie-dialogue-survival-videos/SKILL.md` nếu muốn skill cũng cập nhật — không tự đồng bộ.
- **Không** tự rewrite dialogue đã dán sẵn (nhánh "pasted script") khi skill `writing/dialogue` chẩn đoán ra lỗi — chỉ report, trừ khi người dùng yêu cầu sửa.
- **Không** chuyển `ZOMBIE_FLOOD_LINE_PART1_PIPELINE_OUTPUT.md` vào `result/` trừ khi được yêu cầu rõ — hiện vẫn là file đang phát triển.
- **Không** đính kèm lại end-frame ở STATE 5 — end-frame chỉ dùng ở STATE 4.

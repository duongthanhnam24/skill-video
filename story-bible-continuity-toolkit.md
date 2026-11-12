# Story Bible & Continuity Toolkit

Bộ checklist dùng trong STATE 1 và STATE 4 của cả `ZOMBIE_SURVIVAL_ANIMATION_ENGINE.md` và `ZOMBIE_SURVIVAL_DIALOGUE_ENGINE.md`, cho các dự án con **nhiều Part/Episode** (ví dụ Zombie Subway, The Flood Line). File này **không phải engine, không phải output sản xuất** — giống `camera-movement-ai.md`, nó là một khối tham khảo để ghép vào pipeline khi cần, không tự đứng thành một prompt hoàn chỉnh.

**Nguồn:** ý tưởng dưới đây được **viết lại bằng lời riêng** (không copy nguyên văn code/prompt) sau khi review 3 repo GitHub không liên quan tới dự án này, không cài vào repo, không phải Claude Code skill:
- **Pagekin** (EthanYoQ, GPL-3.0) — quy tắc mỗi mảnh world-building phải tự mang một điểm xung đột; cast lưu như nguồn sự thật có cấu trúc (profile/state/relationship); theo dõi foreshadowing theo từng chapter (gieo → đẩy → thu).
- **narralume** (abligail, Apache-2.0) — cấu trúc "story bible" 7 phần: author intent, outline, entities, canon facts, relationships, timeline, foreshadowing.
- **otaku** (enclavum, AGPL-3.0) — "character journal + state" (ai biết gì tại một thời điểm) và tóm tắt "story so far" cuốn chiếu để giữ continuity qua nhiều phiên chat dài.

Vì Pagekin và otaku dùng license copyleft (GPL/AGPL), phần dưới **không chứa text nào copy từ hai repo đó** — chỉ là mô tả lại ý tưởng bằng từ ngữ của dự án này.

**Cách dùng:** dự án một video đơn, không có Part/Episode kế tiếp → bỏ qua file này. Dự án nhiều Part/Episode cùng cast → điền Part A một lần ở STATE 1 (lưu thành file riêng `<TÊN_DỰ_ÁN>_STORY_BIBLE.md`, ALL_CAPS theo quy ước đặt tên của repo), rồi cập nhật Part B mỗi khi xong một chapter ở STATE 4/5.

---

## Part A — STORY BIBLE CHECKLIST (điền một lần ở STATE 1, cạnh script/cast/Voice DNA)

Điền song song với output thường của STATE 1, không thay thế nó:

1. **Author intent** — một câu: dự án này muốn người xem cảm thấy/hiểu điều gì mà một dự án zombie khác không có.
2. **Outline** — khung Part/Episode đã lên kế hoạch (dù chưa viết hết), để Part sau không mâu thuẫn quy mô/nhịp với Part trước.
3. **Entities** — bảng ngắn: characters (đã có trong Cast/Voice DNA, không lặp lại chi tiết) · locations cố định (phải khớp ENVIRONMENT LOCK dùng xuyên chapter) · factions/nhóm sống sót khác · items/props có vai trò cốt truyện (không chỉ prop cảnh).
4. **Canon facts** — quy tắc thế giới không được tự mâu thuẫn qua các Part: cơ chế lây nhiễm/biến đổi hoạt động thế nào, giới hạn của "turned" (nhìn thấy gì, phản ứng với gì), địa lý khu vực chính.
5. **Relationships** — ai biết ai, quan hệ thật (không chỉ quan hệ trên lời), ai đang nói dối ai.
6. **Timeline** — mốc thời gian trong truyện (ngày mấy của outbreak) khớp với số Part/Episode, để không lộ việc "đã bao lâu rồi" sai lệch giữa các Part.
7. **Conflict check (quy tắc từ Pagekin):** với mỗi entity/canon fact vừa ghi, tự hỏi "chi tiết này tự mang xung đột gì, hay chỉ là lore trang trí?" — một chi tiết thế giới quan không có điểm căng nào thì cắt hoặc gắn thêm xung đột trước khi dùng.
8. **Thread tracker (foreshadowing)** — bảng: `thread | gieo ở đâu (Part/Chapter) | đẩy ở đâu | thu hoạch dự kiến ở đâu | trạng thái`. Trạng thái gồm: *planted* (đã gieo), *pushed* (đã đẩy thêm), *withheld-intentional* (cố ý chưa gieo — ghi rõ lý do/đợi đến đâu), *resolved* (đã thu). Ví dụ đã áp dụng thật trong dự án: vết thương "em trai" của Lâm ở Zombie Subway Tập 1 = *withheld-intentional*, dự kiến thu hoạch gần cao trào tập/phần sau.

## Part B — KNOWLEDGE & CONTINUITY TRACKER (cập nhật mỗi chapter, tra cứu ở STATE 4)

Bổ sung cho cơ chế **CONTINUITY INPUT** đã có (CONTINUITY INPUT lo continuity **hình ảnh** — pose/camera giữa 2 chapter liền nhau). Phần này lo continuity **thông tin** — xuyên suốt nhiều chapter, không chỉ chapter liền kề:

1. **Per-character STATE line** — 1–3 câu cập nhật sau mỗi chapter nhân vật đó xuất hiện: trạng thái vật lý/cảm xúc hiện tại + thông tin quan trọng họ vừa biết. Dùng để chọn pose/expression đúng ở STATE 4 ("Pose and expression per character, matched to the line they're about to deliver") mà không phải đọc lại toàn bộ chapter trước.
2. **"Ai biết gì" log** — mỗi khi một bí mật/thông tin được tiết lộ on-screen, ghi `thông tin | tiết lộ ở Chapter N | ai đã biết`. Trước khi viết dialogue/pose cho một chapter mới, tra log này — không để nhân vật nói ra hoặc phản ứng với điều họ chưa từng được cho biết trên màn hình.
3. **Story-so-far rolling summary** — tối đa ~200 từ, cập nhật mỗi 10–15 chapter hoặc cuối mỗi Part. Dùng khi quay lại dự án sau một thời gian dài hoặc khi viết Part mới, để không phải đọc lại toàn bộ 80+ chapter trước.

**Không làm:** không dùng Part B để quyết định true-match-cut/intentional-scene-change — đó vẫn là việc của STATE 3 handoff marking + CONTINUITY INPUT. Part B chỉ là lớp kiểm tra thông tin/trạng thái, không đụng tới cơ chế hình ảnh đã có.

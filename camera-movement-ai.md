# Camera Movement AI Prompts

Thư viện prompt chuyển động camera dùng cho video AI (Kling, Runway, Higgsfield, Seedance...).
Nguồn: aicameramovements.com — 46 prompt, chia thành 7 nhóm.

**Cách dùng:** copy nguyên khối prompt (bắt đầu bằng `Camera:`) và ghép vào trước phần mô tả bối cảnh/nhân vật trong prompt video của bạn. Mỗi prompt độc lập, không phụ thuộc cảnh cụ thể nên có thể tái dùng cho mọi shot.

**Lưu ý khi dùng:**
- File này chỉ là khối **"Camera movement"** — chưa có shot size/góc máy, ánh sáng, bối cảnh... Cần ghép thêm các khối đó (xem skill `cinematic-video-prompt-skill`) để ra prompt hoàn chỉnh.
- **Slider** (dịch ngang quãng ngắn, tinh chỉnh) khác **Truck** (dịch ngang quãng dài hơn, theo chủ thể/dãy vật) chủ yếu ở **quy mô di chuyển**, không phải hướng.
- **Infinite zoom** là hiệu ứng chuyển cảnh/loop (zoom xuyên vào "thế giới tiếp theo"), không phải cú máy thường cho clip kể chuyện bình thường.
- Muốn một cú máy liền mạch không cắt → thêm câu `single continuous shot, no cuts`. Muốn nhiều shot rõ ràng → ghi rõ **số shot + tổng giây** (model dễ tự cắt ngầm nếu không ghi).

## Mục lục

- **Pan/Tilt** (7): Static shot, Pan right, Pan left, Whip pan right, Whip pan left, Tilt up, Tilt down
- **Zoom/Lens** (6): Slow zoom in, Slow zoom out, Fast zoom in, Fast zoom out, Crash zoom in, Crash zoom out
- **Dolly/Track** (9): Dolly in, Dolly out, Tracking shot, Follow shot / over-the-shoulder, Reverse tracking / walk-and-talk, Side tracking, Low tracking, Vehicle tracking, Chase shot
- **Physical Moves** (11): Truck right, Truck left, Pedestal up, Pedestal down, Slider right, Slider left, Push past / pass-by shot, Arc right, Arc left, Orbit clockwise, Orbit counterclockwise
- **Drone/Crane** (5): Crane up, Crane down, Drone push in, Drone pull back, Helicopter shot
- **Human Camera** (2): Handheld shot, Body-mounted camera / Snorricam
- **Specials** (6): First-person view, Tilt-shift, Infinite zoom, Earth zoom out, Time-lapse, Pass-through objects
- **Bổ sung** (8, tự biên soạn — xem ghi chú nguồn ở cuối file): Dolly zoom / Vertigo effect, Hyperlapse, Camera roll, Bullet time, Continuous long take, Top-down tracking shot, Floating / underwater drift shot, Shoulder-mount handheld

---

## Pan/Tilt

### Static shot
```
Camera: locked-off static shot. Movement: hold one fixed camera position for the full clip. Speed: still and steady. Framing: keep the same angle, height, lens distance and composition. End: finish with the same framing and camera position.
```

### Pan right
```
Camera: pan right. Movement: rotate the camera horizontally from left to right from one fixed point. Speed: smooth constant rotation. Framing: keep the horizon level while new space enters from the right side of the frame. End: settle on a clear final composition.
```

### Pan left
```
Camera: pan left. Movement: rotate the camera horizontally from right to left from one fixed point. Speed: smooth constant rotation. Framing: keep the horizon level while new space enters from the left side of the frame. End: settle on a clear final composition.
```

### Whip pan right
```
Camera: whip pan right. Movement: rotate rapidly from the starting direction toward a new target on the right. Speed: fast snap with brief motion blur during the rotation. Framing: begin on one readable composition and land on a second readable target. End: settle into a sharp final frame.
```

### Whip pan left
```
Camera: whip pan left. Movement: rotate rapidly from the starting direction toward a new target on the left. Speed: fast snap with brief motion blur during the rotation. Framing: begin on one readable composition and land on a second readable target. End: settle into a sharp final frame.
```

### Tilt up
```
Camera: tilt up. Movement: rotate the camera upward from one fixed point. Speed: smooth constant tilt. Framing: keep the vertical subject or architecture centered as the frame travels upward. End: land on the upper target.
```

### Tilt down
```
Camera: tilt down. Movement: rotate the camera downward from one fixed point. Speed: smooth constant tilt. Framing: keep the vertical subject or architecture centered as the frame travels downward. End: land on the lower target.
```

---

## Zoom/Lens

### Slow zoom in
```
Camera: slow zoom in. Movement: slowly increase lens focal length toward a tighter frame. Speed: gradual and even. Framing: keep the main visual target readable as it becomes larger in frame. End: finish on a stable tighter composition.
```

### Slow zoom out
```
Camera: slow zoom out. Movement: slowly decrease lens focal length toward a wider frame. Speed: gradual and even. Framing: keep the main visual target readable as more surrounding space appears. End: finish on a stable wider composition.
```

### Fast zoom in
```
Camera: fast zoom in. Movement: quickly increase lens focal length toward the main visual target. Speed: quick decisive zoom. Framing: keep the target centered or clearly readable during the scale change. End: finish on a stable tighter composition.
```

### Fast zoom out
```
Camera: fast zoom out. Movement: quickly decrease lens focal length away from the main visual target. Speed: quick decisive zoom. Framing: keep the target readable as the surrounding space appears. End: finish on a stable wider composition.
```

### Crash zoom in
```
Camera: crash zoom in. Movement: snap the lens rapidly toward the main visual target. Speed: very fast and punchy. Framing: keep the target readable through the sudden scale change. End: land on a bold tighter composition.
```

### Crash zoom out
```
Camera: crash zoom out. Movement: snap the lens rapidly away from the main visual target. Speed: very fast and punchy. Framing: keep the target readable as the surrounding space appears. End: land on a bold wider composition.
```

---

## Dolly/Track

### Dolly in
```
Camera: dolly in. Movement: move the camera physically forward in a straight line toward the main subject. Speed: smooth controlled push. Framing: keep camera height, lens direction and subject position consistent while distance closes. End: finish in a tighter composition.
```

### Dolly out
```
Camera: dolly out. Movement: move the camera physically backward in a straight line away from the main subject. Speed: smooth controlled retreat. Framing: keep lens direction and camera height consistent while more environment enters frame. End: finish in a wider composition.
```

### Tracking shot
```
Camera: tracking shot. Movement: move through the scene with the main subject. Speed: match the subject's pace. Framing: keep the subject consistently readable while the environment moves around them. End: maintain a clear moving composition.
```

### Follow shot / over-the-shoulder
```
Camera: follow shot from behind. Movement: move behind the subject along their route at shoulder height. Speed: match the subject's pace. Framing: keep the back, shoulder or head as the foreground guide while the route ahead stays readable. End: continue following with the subject leading the frame.
```

### Reverse tracking / walk-and-talk
```
Camera: reverse tracking shot. Movement: move backward in front of the walking subject. Speed: match the subject's forward pace. Framing: keep front-facing face and body framing stable as the background moves behind them. End: hold a clear front-facing moving composition.
```

### Side tracking
```
Camera: side tracking shot. Movement: move parallel beside the subject along their direction of travel. Speed: match the subject's motion. Framing: keep the subject in side profile or three-quarter profile at a stable distance. End: continue the parallel movement with clear horizontal motion.
```

### Low tracking
```
Camera: low tracking shot. Movement: move at ground or below-waist height alongside the subject's movement path. Speed: match the subject, footsteps or wheels. Framing: keep the low detail readable while the ground plane moves through frame. End: finish with the low perspective clearly maintained.
```

### Vehicle tracking
```
Camera: vehicle tracking shot. Movement: move with the vehicle along its route. Speed: match the vehicle's pace. Framing: keep the vehicle stable in frame while the road or environment moves past. End: maintain a clear moving vehicle composition.
```

### Chase shot
```
Camera: chase shot. Movement: follow a moving subject quickly along the action route. Speed: fast, reactive and physically close. Framing: keep the subject visible while allowing energetic reframing. End: stay connected to the subject in motion.
```

---

## Physical Moves

### Truck right
```
Camera: truck right. Movement: move the camera physically to the right on a straight horizontal path. Speed: smooth constant lateral travel. Framing: keep the lens facing the same direction while the scene slides across frame. End: finish on a clean lateral composition.
```

### Truck left
```
Camera: truck left. Movement: move the camera physically to the left on a straight horizontal path. Speed: smooth constant lateral travel. Framing: keep the lens facing the same direction while the scene slides across frame. End: finish on a clean lateral composition.
```

### Pedestal up
```
Camera: pedestal up. Movement: move the entire camera vertically upward in a straight line. Speed: smooth constant lift. Framing: keep the lens level and pointed in the same direction during the vertical move. End: finish with the higher framing clearly readable.
```

### Pedestal down
```
Camera: pedestal down. Movement: move the entire camera vertically downward in a straight line. Speed: smooth constant descent. Framing: keep the lens level and pointed in the same direction during the vertical move. End: finish with the lower framing clearly readable.
```

### Slider right
```
Camera: slider right. Movement: slide the camera a small distance to the right. Speed: slow controlled constant motion. Framing: keep foreground, subject and background layers readable as parallax shifts. End: finish on a refined composition with the new right-side angle visible.
```

### Slider left
```
Camera: slider left. Movement: slide the camera a small distance to the left. Speed: slow controlled constant motion. Framing: keep foreground, subject and background layers readable as parallax shifts. End: finish on a refined composition with the new left-side angle visible.
```

### Push past / pass-by shot
```
Camera: push past. Movement: move forward past a visible foreground object, edge or opening. Speed: smooth forward glide. Framing: let the foreground pass close to the lens while the space beyond becomes clearer. End: arrive inside or beyond the foreground layer.
```

### Arc right
```
Camera: arc right. Movement: move on a shallow curved path around the main subject toward the right side. Speed: smooth measured curve. Framing: keep distance, height and subject readability consistent while the angle changes. End: finish from a new right-side angle.
```

### Arc left
```
Camera: arc left. Movement: move on a shallow curved path around the main subject toward the left side. Speed: smooth measured curve. Framing: keep distance, height and subject readability consistent while the angle changes. End: finish from a new left-side angle.
```

### Orbit clockwise
```
Camera: clockwise orbit. Movement: circle clockwise around the main subject at a consistent radius. Speed: smooth controlled orbit. Framing: keep the subject centered while the background rotates around them. End: complete the intended arc or full circle with stable framing.
```

### Orbit counterclockwise
```
Camera: counterclockwise orbit. Movement: circle counterclockwise around the main subject at a consistent radius. Speed: smooth controlled orbit. Framing: keep the subject centered while the background rotates around them. End: complete the intended arc or full circle with stable framing.
```

---

## Drone/Crane

### Crane up
```
Camera: crane up. Movement: travel smoothly upward through open space. Speed: slow controlled vertical lift. Framing: keep the subject or location readable as the camera rises. End: finish with the higher scale clearly visible.
```

### Crane down
```
Camera: crane down. Movement: travel smoothly downward through open space. Speed: slow controlled vertical descent. Framing: keep the subject or location readable as the camera descends. End: finish with the lower subject or destination clearly visible.
```

### Drone push in
```
Camera: drone push in. Movement: fly smoothly forward through open space toward the subject or destination. Speed: controlled aerial glide. Framing: keep the route and destination readable as the camera approaches. End: arrive at a closer aerial composition.
```

### Drone pull back
```
Camera: drone pull back. Movement: fly smoothly backward away from the subject or destination. Speed: controlled aerial retreat. Framing: keep the subject readable as more landscape appears. End: finish on a wider aerial composition.
```

### Helicopter shot
```
Camera: helicopter-style aerial shot. Movement: move from high altitude along a broad gradual flight path. Speed: steady controlled aerial motion. Framing: keep the landscape or distant moving subject readable at wide scale. End: finish on a stable high-altitude composition.
```

---

## Human Camera

### Handheld shot
```
Camera: handheld shot. Movement: hold the camera at human operator height with natural body movement. Speed: responsive and organic. Framing: keep the subject readable while the frame has subtle sway and micro-adjustments. End: finish with a natural handheld composition.
```

### Body-mounted camera / Snorricam
```
Camera: body-mounted Snorricam. Movement: keep the camera fixed relative to the subject's torso or face while the subject moves. Speed: match the subject's body motion. Framing: keep the subject close, centered and facing the camera as the background moves around them. End: finish with the subject still locked in frame.
```

---

## Specials

### First-person view
```
Camera: first-person view. Movement: move forward at human eye height from the character's perspective. Speed: natural walking or reaching pace. Framing: use visible hands, arms or body edges as the viewer's physical reference. End: arrive at the next point of action from the same point of view.
```

### Tilt-shift
```
Camera: tilt-shift miniature view. Movement: hold or glide from a high angled view over the scene. Speed: small precise movement. Framing: keep a narrow band of sharp focus across the key subject area with soft blur above and below. End: finish with the miniature-scale view intact.
```

### Infinite zoom
```
Camera: infinite zoom. Movement: zoom continuously inward toward the exact center target. Speed: smooth accelerating zoom. Framing: keep the circular target centered as it expands. End: finish when the next visual world fills the frame.
```

### Earth zoom out
```
Camera: earth zoom out. Movement: pull upward from the starting point through street, city, landscape and planet scale. Speed: rapid expanding zoom out. Framing: keep the original location centered as scale grows. End: finish on a planet-scale view with the starting point still implied at center.
```

### Time-lapse
```
Camera: locked-camera time-lapse. Movement: hold one fixed camera position while time moves rapidly forward. Speed: fast time compression with a stable camera. Framing: keep the same composition and horizon as motion passes through the frame. End: finish from the same camera angle with visible passage of time.
```

### Pass-through objects
```
Camera: pass-through movement. Movement: move forward toward a visible object, surface or barrier and continue into the space beyond. Speed: smooth centered glide. Framing: keep the opening or surface centered as the transition point. End: arrive inside the revealed space beyond.
```

---

## Bổ sung

> Các mục dưới đây **không thuộc 46 prompt gốc của aicameramovements.com** — tự biên soạn theo cùng format (Camera/Movement/Speed/Framing/End) để bổ sung những cú máy phổ biến mà kho gốc chưa có, dựa trên review với kho `references/01-camera-angles-and-movement.md` của skill `cinematic-video-prompt-skill`. Nên test thử trên model trước khi dùng hàng loạt.

### Dolly zoom / Vertigo effect
```
Camera: dolly zoom (vertigo effect). Movement: move the camera physically backward while simultaneously zooming the lens in, or move forward while zooming out, keeping the main subject the same size in frame. Speed: slow synchronized push-pull. Framing: keep the subject's scale locked while the background visibly stretches or compresses. End: finish with the background distortion at its most pronounced, subject still centered.
```

### Hyperlapse
```
Camera: hyperlapse. Movement: physically move the camera along a long path through the scene while time is compressed into fast motion. Speed: continuous travel at a steady rate, sped up in playback. Framing: keep a consistent point of reference anchoring each frame as the surrounding light and motion blur past. End: finish having traveled a visibly long distance with time clearly compressed.
```

### Camera roll
```
Camera: camera roll. Movement: rotate the camera around its own lens axis, clockwise or counterclockwise, while holding the same position. Speed: smooth continuous roll. Framing: keep the subject centered while the horizon line tilts and spins around it. End: finish either upright again or fully inverted, depending on the intended effect.
```

### Bullet time
```
Camera: bullet time. Movement: orbit rapidly around a subject frozen or moving in extreme slow motion. Speed: action time near-frozen while the camera travels at high apparent speed. Framing: keep the subject centered and sharply readable as the background streaks past during the orbit. End: finish at a new viewing angle with normal time and speed resuming.
```

### Continuous long take
```
Camera: continuous long take. Movement: combine multiple camera movements, such as walking, turning and rising, into a single unbroken shot without cuts. Speed: varies by segment, always with smooth transitions between movements. Framing: keep the subject or action readable through every transition. End: finish on a clear final composition with no cuts anywhere in the shot.
```

### Top-down tracking shot
```
Camera: top-down tracking shot. Movement: hold the camera directly overhead, facing straight down, and move horizontally to follow the subject below. Speed: match the subject's pace. Framing: keep the subject centered in the overhead frame while the ground plane moves beneath. End: finish with the subject still centered from directly above.
```

### Floating / underwater drift shot
```
Camera: floating drift shot. Movement: move slowly and unevenly through the air or water as if weightless, with gentle vertical and horizontal sway. Speed: very slow, irregular, dreamlike drift. Framing: keep the subject loosely centered while the frame gently bobs and tilts. End: settle into a soft, slightly adrift final composition.
```

### Shoulder-mount handheld
```
Camera: shoulder-mount handheld. Movement: carry the camera at shoulder height with heavier, rougher body movement than standard handheld. Speed: responsive but noticeably shakier, with abrupt micro-corrections. Framing: keep the subject roughly readable despite pronounced jostle and frame instability. End: finish with the raw handheld shake still visible in the final frame.
```

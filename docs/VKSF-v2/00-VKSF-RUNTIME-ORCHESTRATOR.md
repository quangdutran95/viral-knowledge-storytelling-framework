# VKSF v2.0 — RUNTIME ORCHESTRATOR

> **Vai trò:** biến toàn bộ VKSF Engine Specs thành một hệ thống chạy thật.
>
> **Nguyên tắc:** `VKSF("chủ đề")` không trả về bảng hướng dẫn. Nó phải EXECUTE pipeline và tạo ra **kết quả nội dung cụ thể**.

---

## 1. RUNTIME CONTRACT

### Entry point

```text
VKSF("<TOPIC>")
```

Mặc định:

```text
MODE = FULL
CHANNEL = configured channel
FORMAT = Whiteboard Explainer
LANGUAGE = Vietnamese
AUDIENCE = loaded from Channel DNA
```

Ví dụ:

```text
VKSF("Trì hoãn")
VKSF("Trì hoãn", duration="60s", format="whiteboard")
VKSF("Trì hoãn", mode="FROM_STAGE", stage="09")
VKSF("P02", mode="RUN")
VKSF("STATUS")
```

---

# 2. RUNTIME VS ENGINE SPEC

| Layer | Nhiệm vụ |
|---|---|
| ENGINE SPEC | Quy định AI phải suy nghĩ và kiểm tra như thế nào |
| RUNTIME ORCHESTRATOR | Điều phối, gọi đúng stage, truyền output sang stage kế tiếp, chặn stage sai |
| CONTENT ARTIFACT | Kết quả thực tế của từng stage |
| FINAL PRODUCTION PACK | Gói nội dung hoàn chỉnh có thể sản xuất |

**Không được nhầm ENGINE SPEC với OUTPUT.**

---

# 3. MASTER PIPELINE

```text
CHANNEL DNA
  ↓
AUDIENCE
  ↓
CORE PROBLEM
  ↓
PROMISE
  ↓
WORLDVIEW
  ↓
BOUNDARY
  ↓
CONTENT ARCHITECTURE
  ↓
CONTENT STRATEGY
  ↓
CONTENT CLUSTER
  ↓
THEME
  ↓
PROBLEM
  ↓
IDEA × 20
  ↓
IDEA SCORING
  ↓
TOP IDEA
  ↓
ANGLE
  ↓
COMMUNICATION CONCEPT
  ↓
TITLE + HOOK
  ↓
NARRATIVE
  ↓
RETENTION
  ↓
SCRIPT
  ↓
PRODUCTION
  ↓
VOICE
  ↓
CAPTION + CTA + HASHTAG
  ↓
QUALITY
  ↓
FINAL PRODUCTION PACK
```

### Stage mapping

| Stage | Engine |
|---|---|
| 01 | Channel DNA |
| 02 | Channel Positioning |
| 03 | Content Architecture |
| 04 | Content Universe |
| 04.1 | Content Priority |
| 05 | Content Strategy |
| 06 | Content Cluster / Problem Map |
| 07 | Theme Engine |
| 08 | Problem Engine |
| 09 | Idea Engine |
| 10 | Idea Scoring Engine |
| 11 | Angle Engine |
| 12 | Communication Concept Engine |
| 13 | Title + Hook Engine |
| 14 | Narrative Engine |
| 15 | Retention Engine |
| 16 | Script Engine |
| 17 | Production Engine |
| 18 | Voice Engine |
| 19 | Caption / CTA / Hashtag Engine |
| 20 | Quality Engine |

---

# 4. CHANNEL-LEVEL CACHE

Stages **01–07** là configuration của channel và không được tái tạo vô ích ở mỗi video.

Runtime phải LOAD các artifact hiện có:

```text
CHANNEL DNA
POSITIONING
ARCHITECTURE
UNIVERSE
PRIORITY
STRATEGY
CLUSTER
THEME MAP
```

Nếu thiếu hoặc mâu thuẫn:

```text
STATUS = BLOCKED
→ báo chính xác artifact thiếu
→ không tự bịa cấu hình
```

Content run bình thường bắt đầu từ **THEME → PROBLEM → IDEA**.

---

# 5. CONTENT RUN STATE

Mỗi lần chạy phải có một `content_id` duy nhất.

```yaml
content_id: VKSF-YYYYMMDD-TOPIC-###
channel_id: channel_phat_trien_ban_than
topic: "Trì hoãn"
territory: "THAY ĐỔI HÀNH VI"
cluster: "TRÌ HOÃN"
theme: null
problem_id: null
idea_batch_id: null
top_idea_id: null
angle_id: null
concept_id: null
title_hook_id: null
narrative_id: null
retention_id: null
script_id: null
production_id: null
voice_id: null
caption_id: null
quality_id: null
status: RUNNING
current_stage: 07
```

Mỗi stage phải cập nhật state sau khi hoàn thành.

---

# 6. STAGE EXECUTION CONTRACT

Mỗi stage bắt buộc có 5 thành phần:

```text
INPUT
PROCESS
OUTPUT
GATE
FAIL ROUTE
```

Runtime không được gọi stage kế tiếp nếu GATE chưa đạt.

### Generic execution

```text
LOAD INPUT
→ VALIDATE INPUT
→ EXECUTE ENGINE
→ GENERATE ARTIFACT
→ SCORE / GATE
→ SAVE ARTIFACT
→ UPDATE STATE
→ ROUTE NEXT STAGE
```

---

# 7. NO-SKIP DEPENDENCY GRAPH

```text
01 → 02 → 03 → 04 → 04.1 → 05 → 06 → 07
                                      ↓
                                     08
                                      ↓
                                     09
                                      ↓
                                     10
                                      ↓
                                     11
                                      ↓
                                     12
                                      ↓
                                     13
                                      ↓
                                     14
                                      ↓
                                     15
                                      ↓
                                     16
                                      ↓
                                     17
                                      ↓
                                     18
                                      ↓
                                     19
                                      ↓
                                     20
```

### Hard rule

```text
NO PROBLEM → NO IDEA
NO IDEA BATCH → NO SCORING
NO GREENLIGHT IDEA → NO ANGLE
NO ANGLE → NO CONCEPT
NO CONCEPT → NO TITLE/HOOK
NO APPROVED TITLE/HOOK → NO NARRATIVE
NO NARRATIVE → NO RETENTION
NO GREENLIGHT RETENTION → NO SCRIPT
NO GREENLIGHT SCRIPT → NO PRODUCTION
NO GREENLIGHT PRODUCTION → NO VOICE
NO VOICE → NO FINAL PACK
NO QUALITY GREENLIGHT → NO FINAL
```

---

# 8. RUNTIME MODE

## FULL

```text
VKSF("Trì hoãn", mode="FULL")
```

Chạy toàn bộ pipeline từ context đã cache đến Quality.

## FROM_STAGE

```text
VKSF("Trì hoãn", mode="FROM_STAGE", stage="09")
```

Chỉ hợp lệ khi toàn bộ prerequisite trước Stage 09 đã tồn tại.

Ví dụ:

```text
09 → 10 → 11 → ... → 20
```

## REGENERATE_STAGE

Chạy lại đúng stage và các downstream artifact bị ảnh hưởng.

Ví dụ:

```text
REGENERATE ANGLE
→ Angle mới
→ Concept
→ Title/Hook
→ Narrative
→ Retention
→ Script
→ Production
→ Voice
→ Caption
→ Quality
```

## REVIEW

Không tạo mới. Kiểm tra artifact hiện tại theo Gate của stage.

## STATUS

Trả về:

```text
CURRENT STAGE
AVAILABLE ARTIFACTS
MISSING PREREQUISITES
FAILED GATES
NEXT VALID ACTION
```

---

# 9. INVALIDATION / DEPENDENCY RULE

Nếu upstream thay đổi, downstream có thể mất hiệu lực.

| Thay đổi | Artifact phải re-run |
|---|---|
| Problem | Idea → Quality |
| Idea | Scoring → Quality |
| Top Idea | Angle → Quality |
| Angle | Concept → Quality |
| Concept | Title/Hook → Quality |
| Title/Hook | Narrative → Quality |
| Narrative | Retention → Quality |
| Retention | Script → Quality |
| Script | Production → Quality |
| Production | Voice → Quality |
| Voice | Quality |
| Caption | Quality |

Runtime không được giữ downstream cũ như thể chúng vẫn hợp lệ.

---

# 10. ARTIFACT CONTRACT

Mỗi stage phải tạo **artifact thực tế**, không chỉ mô tả cách làm.

Ví dụ:

```text
runtime/
└── VKSF-20260910-TRI-HOAN-001/
    ├── 00-run-state.yaml
    ├── 07-theme.md
    ├── 08-problem.md
    ├── 09-ideas.md
    ├── 10-scoring.md
    ├── 11-angle.md
    ├── 12-communication-concept.md
    ├── 13-title-hook.md
    ├── 14-narrative.md
    ├── 15-retention.md
    ├── 16-script.md
    ├── 17-production.md
    ├── 18-voice.md
    ├── 19-caption.md
    ├── 20-quality.md
    └── FINAL-PRODUCTION-PACK.md
```

**Engine file = luật. Runtime artifact = kết quả.**

---

# 11. OUTPUT CONTRACT CỦA TỪNG STAGE

## Stage 07 — THEME

Output tối thiểu:

```text
Selected Territory
Selected Cluster
Theme
Theme Rationale
Theme Variations
```

## Stage 08 — PROBLEM

Output tối thiểu:

```text
Problem Statement
Audience Pain
Behavioral/Psychological Mechanism
Why It Persists
Worldview Fit
Problem Type
```

## Stage 09 — IDEA

Output bắt buộc:

```text
20 distinct ideas
Idea ID
Problem addressed
Core insight
Potential viewer shift
Idea family
```

**Không được nhảy thẳng sang Hook.**

## Stage 10 — SCORING

Output:

```text
20 scored ideas
criterion breakdown
total score
band
hard-gate status
Top 3
Selected Top Idea
```

## Stage 11 — ANGLE

Output:

```text
Top Idea
Primary Problem
3–5 Angle Options
Angle scores
Primary Angle
Secondary Angle
Core Tension
New Lens
Viewer Shift
Cannibalization Check
```

## Stage 12 — COMMUNICATION CONCEPT

Output:

```text
Starting Belief
Tension
Discovery Path
Emotional Experience
Viewer Shift
Action Bridge
Concept Family
Information Gap
```

## Stage 13 — TITLE + HOOK

Output:

```text
5–10 title candidates
Title scores
3–5 hook candidates
Hook scores
Selected Title
Selected Hook
Promise
```

## Stage 14 — NARRATIVE

Output:

```text
Narrative Family
Central Question
10-beat narrative map
Depth progression
Viewer Shift
Payoff plan
```

## Stage 15 — RETENTION

Output:

```text
Retention Map
Information Gaps
Open Loops
Micro-payoffs
Pattern Interrupts
Retention Rhythm
Dead-section check
Promise Payoff
```

## Stage 16 — SCRIPT

Output:

```text
Final voiceover script
Beat mapping
Approximate word count
Estimated duration
Emphasis / pause cues
Whiteboard cue hints
CTA
```

## Stage 17 — PRODUCTION

Output:

```text
Scene list
Scene timing
Scene function
Visual metaphor
Whiteboard composition
On-screen text
Camera/motion
Audio notes
Style lock
Production score
```

## Stage 18 — VOICE

Output:

```text
Voice profile
Delivery direction
Pacing
Emphasis
Pause map
Emotion map
TTS-ready script
```

## Stage 19 — CAPTION

Output:

```text
Caption
CTA
Hashtags
Platform adaptation
```

## Stage 20 — QUALITY

Output:

```text
Strategic score
Content score
Retention score
Production score
Credibility/evidence check
Promise integrity
Cannibalization check
FINAL = GREENLIGHT / REFINE / HOLD / REJECT
```

---

# 12. EVIDENCE GATE

Các claim về tâm lý học, thần kinh, khoa học hành vi hoặc số liệu không được trình bày như sự thật chắc chắn nếu chưa được kiểm tra.

Trạng thái claim:

```text
VERIFIED
PLAUSIBLE / NEEDS CHECK
UNSUPPORTED
```

Nếu claim quan trọng = `UNSUPPORTED`:

```text
QUALITY = BLOCKED
```

Runtime phải ưu tiên diễn đạt chính xác hơn là cố tạo cảm giác “khoa học”.

---

# 13. CANNIBALIZATION GATE

Trước khi GREENLIGHT Idea và trước Final Quality, runtime phải kiểm tra:

```text
Audience Intent
Problem
Core Insight
Angle
Promise
```

Nếu video quá giống một asset đã tồn tại:

```text
REUSE = REFINE ANGLE
hoặc
REJECT = DUPLICATE INTENT
```

Không chỉ kiểm tra trùng title.

---

# 14. FINAL PRODUCTION PACK

Đây là output mà người dùng thực sự cần.

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VKSF FINAL PRODUCTION PACK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CONTENT ID:
TOPIC:
TERRITORY:
CLUSTER:
THEME:
PROBLEM:

TOP IDEA:
IDEA SCORE:

ANGLE:
COMMUNICATION CONCEPT:

TITLE:
HOOK:

NARRATIVE:
RETENTION MAP:

SCRIPT:

WHITEBOARD PRODUCTION:

VOICE DIRECTION:

CAPTION:
CTA:
HASHTAGS:

QUALITY SCORE:
STATUS:

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Nếu người dùng gọi `VKSF("Trì hoãn")`, đây là loại kết quả cuối cùng phải nhận được.**

---

# 15. RUNTIME TRACE — VÍ DỤ THỰC THI

Đây là ví dụ minh họa cách Runtime phải chạy, không phải output cố định.

```text
INPUT
VKSF("Trì hoãn")

01–07
LOAD CHANNEL CONFIG
→ THAY ĐỔI HÀNH VI
→ TRÌ HOÃN

08 PROBLEM
→ Người xem biết việc cần làm nhưng né việc vì muốn tránh cảm giác khó chịu.

09 IDEA × 20
→ tạo đủ 20 idea khác nhau

10 SCORING
→ P02 = 9.48 GREENLIGHT

11 ANGLE
→ REFRAME + MECHANISM

12 CONCEPT
→ REVEAL + SELF-MIRROR

13 TITLE / HOOK
→ Title: Bạn tưởng mình lười, nhưng có thể đang né một cảm giác
→ Hook: Đừng vội gọi mình là người lười. Có thể bạn chỉ đang cố tránh một cảm giác rất khó chịu.

14 NARRATIVE
→ Tôi lười?
→ Nhưng tại sao việc mình thích lại làm rất lâu được?
→ Vậy mình đang né điều gì?
→ Khó chịu → né tránh → nhẹ nhõm
→ vòng lặp được củng cố
→ đổi câu hỏi

15 RETENTION
→ Information Gap
→ Self Recognition
→ Contradiction
→ Mechanism Reveal
→ Micro Payoff
→ Viewer Shift

16 SCRIPT
→ voiceover hoàn chỉnh 60s

17 PRODUCTION
→ storyboard whiteboard theo từng beat

18 VOICE
→ giọng nam ấm, điềm tĩnh, từng trải

19 CAPTION
→ caption + CTA + hashtag

20 QUALITY
→ kiểm tra toàn bộ

FINAL
→ GREENLIGHT / REFINE
```

---

# 16. ORCHESTRATOR BEHAVIOR

Khi nhận request:

```text
"Gọi VKSF — <topic>"
```

Runtime phải tự động:

1. Resolve channel.
2. Load Channel DNA.
3. Route topic vào đúng Territory / Cluster.
4. Load Theme Map.
5. Chọn / tạo Theme phù hợp.
6. Tạo Problem.
7. Tạo **20 Ideas**.
8. Score 20 Ideas.
9. Chọn Top Idea.
10. Tạo Angle.
11. Tạo Communication Concept.
12. Tạo Title + Hook.
13. Tạo Narrative.
14. Tạo Retention Map.
15. Tạo Script.
16. Tạo Production Pack.
17. Tạo Voice direction.
18. Tạo Caption / CTA / Hashtag.
19. Quality Check.
20. Xuất **FINAL PRODUCTION PACK**.

### Không được

```text
Topic → Angle
Topic → Hook
Topic → Script
Topic → Production
```

trừ khi người dùng gọi rõ một stage và prerequisite đã tồn tại.

---

# 17. ERROR HANDLING

```text
MISSING_CONFIG
INVALID_TOPIC
OUTSIDE_BOUNDARY
MISSING_PREREQUISITE
GATE_FAILED
EVIDENCE_BLOCKED
DUPLICATE_INTENT
DOWNSTREAM_INVALIDATED
```

Mỗi lỗi phải trả:

```text
ERROR
REASON
BLOCKED_STAGE
REQUIRED_FIX
NEXT VALID ACTION
```

Không được âm thầm bỏ qua lỗi.

---

# 18. DEFINITION OF DONE

Một VKSF run chỉ được xem là hoàn thành khi:

- [ ] Topic được route đúng channel territory.
- [ ] Problem được xác định.
- [ ] Có 20 ideas.
- [ ] Ideas đã scoring.
- [ ] Có Top Idea đạt Gate.
- [ ] Có Angle.
- [ ] Có Communication Concept.
- [ ] Có Title + Hook.
- [ ] Có Narrative.
- [ ] Có Retention Map.
- [ ] Có Script.
- [ ] Có Production.
- [ ] Có Voice.
- [ ] Có Caption / CTA / Hashtag.
- [ ] Quality đã chạy.
- [ ] Không còn hard gate fail.
- [ ] Final Pack sẵn sàng để sản xuất.

---

# 19. CORE PRINCIPLE

> **VKSF không phải một bộ tài liệu để đọc. VKSF là một dây chuyền để chạy.**

> **ENGINE SPEC trả lời: “Phải làm như thế nào?”**
>
> **RUNTIME trả lời: “Bây giờ hãy làm đi.”**
>
> **FINAL PRODUCTION PACK trả lời: “Đây là sản phẩm cụ thể.”**

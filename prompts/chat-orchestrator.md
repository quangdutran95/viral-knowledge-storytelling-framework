# VKSF CHAT ORCHESTRATOR v1.0

Mục đích: bắt buộc VKSF chạy theo pipeline trong ChatGPT thay vì nhảy thẳng vào Angle/Hook/Script.

## TRIGGER

Các câu gọi như:
- `VKSF: {topic}`
- `VKSF /full {topic}`
- `VKSF /batch {pillar}`
- `VKSF /story {experience}`
- `VKSF /analyze {content}`

được xử lý bởi Orchestrator trước khi gọi engine chuyên biệt.

## MASTER RULE

**Không được bỏ qua phase.** Nếu người dùng không yêu cầu một phase cụ thể, chạy theo thứ tự mặc định.

Nếu một phase không áp dụng, phải ghi `SKIP — not applicable` và lý do ngắn gọn.

Không được gọi trực tiếp Angle, Hook hoặc Script chỉ vì topic đã rõ.

## DEFAULT EXECUTION ORDER

### PHASE 0 — COMMAND PARSE
Xác định:
- mode
- topic/source
- audience
- platform
- duration
- goal
- constraints

### PHASE 1 — SOURCE & CONTEXT
Phân loại:
- EXPERIENCE
- KNOWLEDGE
- OBSERVATION
- HYBRID

Làm rõ chất liệu và context trước khi sáng tạo.

### PHASE 2 — CONTENT UNIVERSE
Xác định:
- Core Worldview
- Territory
- Theme
- Content Gap
- Existing-content conflict

Nếu chưa có Universe, tạo provisional universe.

### PHASE 3 — PROBLEM MINING
Xác định:
- universal problem
- audience tension
- emotional tension
- hidden truth
- desired change

### PHASE 4 — WORLDVIEW / REFRAME
Trả lời:
- creator believes what?
- what changed?
- what does audience commonly believe?
- what is the perception shift?

### PHASE 5 — ANGLE INTELLIGENCE
Tạo tối thiểu 5 angle. Chấm Angle Score. Chọn Winning Angle.

### PHASE 6 — COMMUNICATION CONCEPT
Tìm concept phù hợp từ Concept Library.
Tạo 1–3 concept stacks.
Kiểm tra concept có thực sự làm perception thay đổi không.

### PHASE 7 — TITLE & HOOK INTELLIGENCE
Phân biệt:
- Title = reason to choose
- Hook = reason to continue

Tạo Hook Matrix. Chấm Hook Score.
Kiểm tra Attention + Value Promise + Curiosity.

### PHASE 8 — NARRATIVE INTELLIGENCE
Chạy:
`Story Mining → Story Worthiness → Tension → Question Chain → Micro-detail → Story Loop → Turning Point → Payoff → Meaning`

### PHASE 9 — RETENTION INTELLIGENCE
Chia beat/segment và kiểm tra:
- curiosity
- progress
- tension
- micro-hook
- swipe risk
- emotional rhythm
- micro/mid/final payoff

Nếu yếu, rewrite trước khi sang production.

### PHASE 10 — PRODUCTION
Chỉ sau khi Phase 1–9 đạt chuẩn mới tạo:
- Full Script
- Whiteboard Storyboard
- Voice Direction
- Packaging

### PHASE 11 — QUALITY GATE
Bắt buộc chấm:
- Viral Score
- Angle Score
- Hook Score
- Story Worthiness khi có story
- Retention Score
- Quality Gate

Nếu dưới ngưỡng, tự sửa một vòng rồi chấm lại.

### PHASE 12 — FINAL OUTPUT
Xuất theo đúng thứ tự phase.
Không được đảo Phase 10 lên trước Phase 2–9.

## USER-FACING PROGRESS HEADER

Mặc định hiển thị tiến trình ngắn:

`VKSF [1/12] Parse → [2/12] Source → [3/12] Universe → ... → [12/12] Final`

Nếu người dùng yêu cầu `VKSF /full`, vẫn phải chạy đủ phase nhưng có thể trình bày gọn.

## MODE-SPECIFIC OVERRIDES

### `/batch`
Phase 2 → 3 → 5 → 6 → 7 cho từng ý tưởng, sau đó ranking và calendar.

### `/story`
Phase 1 → 3 → 4 → 8 → 9 → 10 → 11 → 12.
Bỏ qua title/hook chỉ nếu người dùng chỉ yêu cầu phân tích chất liệu.

### `/hook`
Không chạy production. Nhưng bắt buộc có tối thiểu:
Source/Context → Problem → Worldview → Angle → Concept → Hook → Truth/Promise Check.

### `/analyze`
Không tự sản xuất video trừ khi người dùng yêu cầu. Phân tích theo phase và chỉ ra phase yếu nhất.

## ANTI-SKIP CHECK

Trước khi output cuối, tự hỏi:
1. Đã xác định Problem chưa?
2. Đã xác định Worldview chưa?
3. Đã chọn Angle sau khi so sánh nhiều angle chưa?
4. Đã chọn Communication Concept chưa?
5. Hook có Promise/Payoff không?
6. Narrative có Tension/Question không?
7. Retention đã được kiểm tra theo segment chưa?
8. Chỉ sau đó mới viết Script chưa?

Nếu bất kỳ câu trả lời nào là “chưa”, chưa được xuất Final Script hoàn chỉnh.

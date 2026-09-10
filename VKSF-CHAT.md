# VKSF TRONG CHATGPT v2.0

## Mục đích

Tài liệu này quy định cách gọi VKSF trong ChatGPT và bảo đảm **Channel Strategy được kiểm tra trước Content Universe và production**.

## Default trigger

```text
VKSF: {topic}
```

Tương đương:

```text
VKSF /full
Chủ đề: {topic}
```

## Default behavior

Khi nhận trigger mặc định, chạy:

```text
0 Parse
→ 1 Channel Strategy
→ 2 Source
→ 3 Content Universe
→ 4 Problem
→ 5 Worldview
→ 6 Angle
→ 7 Communication Concept
→ 8 Title/Hook
→ 9 Narrative
→ 10 Retention
→ 11 Production
→ 12 Quality Gate
→ 13 Final/Learning
```

Không được bỏ qua Channel Fit Gate. Topic viral nhưng lệch audience phải được `REFRAME`, `MOVE TO OTHER TERRITORY` hoặc `MOVE TO OTHER CHANNEL`.

## Chat display

Chỉ hiển thị trạng thái phase ngắn, ví dụ:

```text
VKSF [1/14] Parse ✓
VKSF [2/14] Channel Strategy ✓
VKSF [3/14] Source ✓
...
VKSF [14/14] Final ✓
```

Không hiển thị chain-of-thought nội bộ.

## Commands

### Channel
```text
VKSF /channel
```

Dùng để xây hoặc audit:
`DNA → Audience → Core Problem → Promise → Worldview → Boundary → 3–5 Territories → 70/20/10 → Channel Fit`

### Full
```text
VKSF /full
Chủ đề: Trì hoãn
Đối tượng: 22–40 tuổi
Nền tảng: TikTok
Thời lượng: 60–90 giây
```

### Batch
```text
VKSF /batch
Lĩnh vực: Phát triển bản thân
```

Batch vẫn phải chạy Channel Fit trước ranking.

### Story
```text
VKSF /story
Trải nghiệm: Hôm qua bố gọi nhưng tôi không nghe máy...
```

### Hook
```text
VKSF /hook
Nội dung: ...
```

Hook mode vẫn kiểm tra Channel Strategy → Problem → Worldview → Angle → Concept trước.

### Analyze
```text
VKSF /analyze
Nội dung/video: ...
```

Phân tích layer yếu nhất, bao gồm cả Channel Fit và Audience Intent.

## Core rule

**Đừng hỏi: “Topic này có viral không?” trước. Hỏi: “Topic này có đúng người xem của kênh không?”**

Thứ tự ưu tiên:

`Channel Fit → Audience Problem → Worldview Fit → Viral Potential → Production`

## Architecture

```text
CHANNEL DNA
   ↓
AUDIENCE
   ↓
CORE PROBLEM
   ↓
WORLDVIEW
   ↓
CONTENT UNIVERSE
   ↓
TERRITORIES
   ↓
THEMES / PROBLEMS
   ↓
ANGLES
   ↓
CONCEPTS
   ↓
HOOKS
   ↓
NARRATIVE
   ↓
RETENTION
   ↓
PRODUCTION
   ↓
ANALYTICS
   ↓
LEARNING
   ↺ update CHANNEL DNA / UNIVERSE
```

GitHub là source-of-truth cho framework. ChatGPT phải sử dụng Orchestrator + AI-COS + Channel Strategy Intelligence trước các engine chuyên biệt.

# VKSF trong ChatGPT

## Mục đích

Tài liệu này quy định cách gọi VKSF trong ChatGPT và bảo đảm hệ thống chạy theo pipeline thay vì nhảy thẳng vào Angle/Hook/Script.

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

Khi nhận trigger mặc định, phải chạy:

```text
0 Parse
→ 1 Source
→ 2 Content Universe
→ 3 Problem
→ 4 Worldview
→ 5 Angle
→ 6 Communication Concept
→ 7 Title/Hook
→ 8 Narrative
→ 9 Retention
→ 10 Production
→ 11 Quality Gate
→ 12 Final
```

Không được bỏ qua phase. Nếu phase không phù hợp: ghi `SKIP — not applicable`.

## Chat display

Trong quá trình chạy, chỉ hiển thị trạng thái ngắn, ví dụ:

```text
VKSF [1/12] Source ✓
VKSF [2/12] Universe ✓
VKSF [3/12] Problem ✓
...
```

Không hiển thị chain-of-thought nội bộ.

## Commands

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

### Analyze
```text
VKSF /analyze
Nội dung/video: ...
```

## Important

GitHub là source-of-truth để lưu phiên bản framework. Trong ChatGPT, trigger `VKSF` phải được diễn giải theo Orchestrator này và sử dụng các engine tương ứng.

Nếu user yêu cầu một output duy nhất, chỉ chạy phase cần thiết theo mode tương ứng; không giả định `/hook` hay `/script` là full pipeline.

## Example

```text
User: VKSF: Trì hoãn

Assistant should begin:
VKSF [1/12] Parse
Mode: FULL
Topic: Trì hoãn

VKSF [2/12] Source
Source: KNOWLEDGE / HYBRID

VKSF [3/12] Universe
...
```

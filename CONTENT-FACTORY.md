# VKSF CONTENT FACTORY v1.2

## Mục tiêu

Biến một input đơn giản thành một production pack có thể dùng trực tiếp cho video short-form.

## Input tối thiểu

```yaml
topic: ""
audience: ""
platform: "TikTok"
duration: "60-90s"
goal: ""
```

Nếu thiếu dữ liệu, hệ thống tự chọn giả định mặc định thay vì dừng quy trình.

## Output chuẩn

```text
01_topic_diagnosis
02_viral_score
03_angles
04_hooks
05_emotion_map
06_retention_map
07_story
08_knowledge
09_core_insight
10_transformation
11_final_script
12_storyboard
13_voice_direction
14_titles
15_captions
16_ctas
17_hashtags
18_quality_gate
19_publish_checklist
20_analytics_schema
```

## Operating Rules

### Rule 1 — One Core Idea
Mỗi video chỉ có một thông điệp trung tâm. Những ý phụ phải phục vụ thông điệp đó.

### Rule 2 — Evidence Before Authority
Nếu claim có tính khoa học, sức khỏe, tâm lý hoặc lịch sử, phải kiểm chứng trước khi trình bày như sự thật.

### Rule 3 — Emotion Is Not Manipulation
Cảm xúc dùng để giúp người xem quan tâm và ghi nhớ, không để gây sợ hãi giả hoặc tạo áp lực.

### Rule 4 — Retention Through Value
Open loop phải được trả lời. Không cố tình giấu thông tin chỉ để kéo thời lượng.

### Rule 5 — Shareability Through Identity
Một nội dung dễ chia sẻ khi nó giúp người xem nói thay một điều họ đang nghĩ, hoặc giúp họ gửi giá trị cho người khác.

## Batch Mode

Khi được yêu cầu tạo nhiều video:

1. Tạo 20 topic.
2. Chấm Viral Score.
3. Chọn Top 5.
4. Tạo production pack cho Top 5.
5. Kiểm tra trùng lặp hook, insight và cấu trúc.
6. Xuất lịch sản xuất.

## Repurposing Mode

Từ một video gốc có thể tạo:

- 1 video 60–90s.
- 3 video 20–30s.
- 1 carousel.
- 1 bài Facebook.
- 1 caption ngắn.
- 5 câu quote.
- 10 hook biến thể.

## Feedback Loop

Sau khi đăng, nhập metrics vào Analytics Engine. Hệ thống phải xác định:

- Hook thắng/thua.
- Đoạn tụt retention.
- Insight nào được save/share.
- CTA nào tạo tương tác.
- Chủ đề nào nên mở rộng.
- Công thức nào cần loại bỏ.

Kết quả được dùng để điều chỉnh topic selection, hook generation và story architecture cho vòng tiếp theo.

# VKSF Content Factory

## Mục đích

Content Factory là lớp vận hành của VKSF. Nó biến một pillar hoặc danh sách ý tưởng thành một batch nội dung có thứ tự ưu tiên, chống trùng lặp, có lịch sản xuất và có vòng học từ dữ liệu.

## Input

`Pillar + Audience + Platform + Count + Duration + Goal + Existing Topics + Performance Data`

## Pipeline

`Generate → Score → Deduplicate → Prioritize → Cluster → Queue → Calendar → Learn → Next Batch`

## Batch Logic

### 1. Generate
Tạo nhiều ý tưởng hơn số lượng cần xuất bản để có không gian loại bỏ ý tưởng yếu.

### 2. Score
Chấm Viral Score /100 theo 7 thành phần:
- Hook 20
- Curiosity 15
- Relatability 15
- Emotional Impact 15
- Knowledge Value 15
- Novelty 10
- Shareability 10

### 3. Deduplicate
Kiểm tra trùng với cả batch mới và content library cũ.

### 4. Prioritize
Ưu tiên giao điểm giữa viral potential, knowledge value, emotional depth, novelty và production feasibility.

### 5. Cluster
Tạo các nhóm nội dung theo vấn đề/insight. Không để feed liên tiếp quá giống nhau.

### 6. Queue
Xác định thứ tự sản xuất dựa trên score và chiến lược đa dạng hóa.

### 7. Calendar
Phân bổ Top 5 vào 5–7 ngày. Có thể thay đổi theo dữ liệu thực tế của kênh.

### 8. Learn
Đọc dữ liệu video đã xuất bản để hình thành hypothesis, không nhầm tương quan với nguyên nhân.

### 9. Next Batch
Chuyển learning thành quy tắc cụ thể cho batch tiếp theo.

## Output

Mỗi batch phải tạo:
1. Batch Summary
2. Idea Table
3. Duplicate/Cannibalization Report
4. Top 5
5. Content Clusters
6. Production Queue
7. Content Calendar
8. Performance Learning
9. Next Batch Rules

## Content Factory → Production Pack

Khi một chủ đề được chọn, chuyển sang `prompts/master-prompt.md` và lưu kết quả theo `templates/production-package.md`.

## Feedback Loop

`Published Video → Analytics → Hypothesis → Rule → Next Batch → Experiment → Analytics`

Không coi một video viral là bằng chứng chắc chắn cho một quy luật. Ưu tiên kiểm nghiệm pattern qua nhiều video.

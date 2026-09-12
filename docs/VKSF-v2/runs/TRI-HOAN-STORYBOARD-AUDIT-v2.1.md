# VKSF v2.1 — TRÌ HOÃN STORYBOARD AUDIT

**Audit scope:** P02, P01, P06, P20, P13, P16, P03, P10
**Target:** Whiteboard Explainer / 60s

## Finding

Các run cũ đều có storyboard production-ready về mặt field, nhưng nhiều storyboard bị **scene compression**: một scene mang nhiều cognitive functions. Đây là lỗi implementation, không phải lỗi của format Whiteboard.

## New rule

```text
SCRIPT → NARRATIVE BEAT MAP → COGNITIVE BEAT MAP → VISUAL BEAT MAP → SCENE MAP
```

Không cố định 9/10/12 cảnh. Với 60s, default 12–16 cảnh; có thể ít/nhiều hơn khi cognitive density thực tế yêu cầu.

## Revision status

| Idea | Old | Revised target | Status |
|---|---:|---:|---|
| P02 | 10 | 14 | REQUIRED |
| P01 | 10 | 13–14 | REQUIRED |
| P06 | 9 | 14 | DONE |
| P20 | 10 | 14 | REQUIRED |
| P13 | 9 | 13–14 | REQUIRED |
| P16 | 9 | 13–14 | REQUIRED |
| P03 | 9 | 13–14 | REQUIRED |
| P10 | 9 | 13–14 | REQUIRED |

## Mandatory audit checks

1. Không scene count cố định.
2. Một primary cognitive function/scene.
3. Cognitive change quan trọng phải có visual change.
4. Mechanism không bị nhồi vào một scene quá dài.
5. Causal loop được tách đủ để người xem nhìn thấy.
6. Reframe phải có visual contrast với old belief.
7. Action phải là hành động nhìn thấy được.
8. Tổng timing khớp 60s ±1s.
9. Không thay đổi chiến lược đã khóa.

## Execution order

```text
P06 → P02 → P01 → P20 → P13 → P16 → P03 → P10
```

P06 revision đã được tạo riêng tại:
`TRI-HOAN-P06-STORYBOARD-REVISION-v2.1.md`

Các revision còn lại phải giữ nguyên Idea/Angle/Concept/Title/Hook/Narrative/Script và chỉ sửa visualization.

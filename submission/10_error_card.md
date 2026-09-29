# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B1 | MISSING | 7 |
| center | B1 | SPURIOUS | 6 |
| center | C0 | MISSING | 1 |
| edge | B1 | ATTRIBUTE | 4 |
| edge | B1 | MISSING | 2 |
| edge | B1 | SPURIOUS | 5 |
| mid | B1 | BOX_GEOMETRY | 3 |
| mid | B1 | DUPLICATE | 1 |
| mid | B1 | IGNORE_SCOPE | 1 |
| mid | B1 | MISSING | 4 |
| mid | B1 | SPURIOUS | 8 |
| mid | B1 | WRONG_CLASS | 1 |
| mid | C0 | MISSING | 1 |

## Top defects
- SPURIOUS: 19 (ví dụ frame adasind_006840.jpg)
- MISSING: 15 (ví dụ frame adasind_019560.jpg)
- ATTRIBUTE: 4 (ví dụ frame adasind_006840.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: lỗi nổi bật nhất là SPURIOUS (19) và MISSING (15), nhưng phần lớn thuộc model: M_only/LR_noM chiếm đa số, `why=E4_model_domain`. Ví dụ adasind_006840.jpg: M13 gọi auto-rickshaw L1/R1 là Car, M12 gọi xe vàng là Bus, M8 Truck + M10 Car trùng trên cùng xe R6 → model chưa quen taxonomy ThreeWheeler và ảnh fisheye. Lỗi của người (L) ít hơn và tập trung ở vùng mid đông, che khuất dày (006840: L7 box lỏng, L8 vật mờ trong vùng unreadable; 056040: L7 gán ThreeWheeler cho ô tô bị rider che) → `why=E1_annotator_error`, nguyên nhân là soát chưa kỹ vật bị che, không phải méo rìa (edge L khớp 3/3).
- Cách sửa và ai nhận việc (`owner`): `annotator` đã rework 8 ca (delta mid: matched 5→7, missing 2→0, spurious 2→0); `ai_team` nhận escalation về ánh xạ ThreeWheeler và box kép khác class (30_escalation_ticket.md); `guideline` nhận đề xuất R01a đo chiều cao ca sát ngưỡng (20_guideline_patch.md) và ca R4 Bus/ThreeWheeler cần người thứ ba xác nhận reference.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): screenshots/qa_006840_missing_sau_L1.png (R4, M12, R01/R04), screenshots/qa_056040_L7_vs_L2.png (L7+R7 WRONG_CLASS, R04), r3_diag/model_compare.html, r3_diag/local_quality.md (ThreeWheeler precision/recall 0.714), rework/delta.md; findings.csv các dòng r3_diag của 006840 và 056040; decision log D1–D6.

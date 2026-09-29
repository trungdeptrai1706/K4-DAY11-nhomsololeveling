# Guideline patch

- **Rule mới đề xuất:** R01a — Đo chiều cao theo phần vật nhìn thấy trên ảnh gốc, từ điểm cao nhất tới điểm thấp nhất của vật (không tính bóng, không tính phần bị che). Nếu chiều cao đo được nằm trong khoảng 38–42 px, annotator vẫn vẽ box và ghi `note=near_H` trong findings; reviewer không báo lỗi BOX_GEOMETRY chỉ vì sát ngưỡng khi box đã ôm đúng phần nhìn thấy.
- **Áp dụng cho:** cả sáu class box; mọi zone (center/mid/edge); không áp dụng cho `ignore_region`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R01 chỉ nói "cao ≥ 40 px" mà không nói đo phần nào, nên ca 006840 L2 (Pedestrian 41 px) bị QA nghi ngờ dù trùng khít reference R7 (xem `findings.csv` dòng r2_qa L2 và r3_diag L2+R7, decision D3). Trên ảnh fisheye, cùng một vật đổi chiều cao nhanh khi dịch về rìa, nên ca sát ngưỡng sẽ lặp lại.
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** round rework của slice này trở đi (không đổi lại nhãn đã khóa ở r1_craft).

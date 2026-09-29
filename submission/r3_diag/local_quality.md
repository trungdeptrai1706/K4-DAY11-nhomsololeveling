# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `5715ff4ca2818fd2efb22a7d14aeda8f461548f68c9df8dc2357bf1eba341ce2`; slice `B1-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_006840.jpg, adasind_036720.jpg, adasind_056040.jpg. Frame thiếu trong export: không.
TP=17; FP=2; FN=3; số lần đối chiếu=21; mean IoU của TP=0.843.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.810 | 0.940 | 0.810 |
| precision | 0.895 | 0.929 | 0.714 |
| recall | 0.850 | 0.845 | 0.667 |
| jaccard | 0.773 | 0.806 | 0.556 |
| dice | 0.872 | 0.879 | 0.714 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 6 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Car | 2 | 0 | 1 | 0.952 | 1.000 | 0.667 | 0.667 | 0.800 |
| Pedestrian | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| ThreeWheeler | 5 | 2 | 2 | 0.810 | 0.714 | 0.714 | 0.556 | 0.714 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_006840.jpg | 7 | 1 | 2 | 0.700 | 0.875 | 0.778 |
| adasind_036720.jpg | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_056040.jpg | 6 | 1 | 1 | 0.857 | 0.857 | 0.857 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | <missing> |
|---|---:|---:|---:|---:|---:|
| Bike | 6 | 0 | 0 | 0 | 0 |
| Car | 0 | 2 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 4 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 0 | 5 | 2 |
| <extra> | 0 | 0 | 0 | 1 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.

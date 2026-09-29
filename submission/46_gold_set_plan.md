# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Đông xe, auto-rickshaw và xe hai bánh chồng nhau ở mid; xe lớn bị cắt ở rìa | Che khuất dày làm sót vật phía sau (006840 R4, L8); ThreeWheeler bị gọi Car/Bus; box ở rìa lỏng (fill ratio edge 0.57) | Ảnh fisheye gốc, không undistort; lens circle và ego_body mask cố định theo camera_id; rules_version | Hai annotator vẽ độc lập, reviewer thứ ba (không vẽ) soát theo rule; bất đồng class ghi decision log; chỉ gọi gold khi hai bên khớp IoU ≥ 0.7 và class, hoặc có phân xử có bằng chứng |
| rear | Xe bám sát phía sau chiếm cả khung, bị cắt | truncated/edge_zone dễ sai; một vật lớn dễ bị vẽ hai box | Như trên + mask thân xe phía sau | Review riêng thuộc tính truncated/edge_zone; so với frame liền kề cùng track |
| left | Rider vượt sát bên trái, bị ego_body che; vùng seam trước-trái | Người lái bị tay/tay áo ego che (036720, 056040); vật ở seam xuất hiện ở hai camera | Mask ego_body trái, calibration + timestamp để đối chiếu seam | Reviewer đối chiếu ảnh hai camera cùng timestamp trước khi kết luận MISSING/DUPLICATE ở seam |
| right | Quán ven đường, auto-rickshaw và ô tô đỗ lẫn nền; seam trước-phải | Vật đứng yên lẫn nền bị bỏ sót (C0 sót R5, R6); ô tô bị che bị gán nhầm class (056040 L7) | Như trên + danh sách class map đặc biệt (R04) | Checklist bắt buộc soát "vật đứng yên/lẫn nền"; ca class khó đưa người thứ ba |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): khi thay camera/lens hoặc vị trí lắp (lens circle, ego mask đổi), khi calibration được đo lại, khi rules_version đổi (ví dụ áp dụng R01a hoặc thay class map ThreeWheeler), hoặc khi review định kỳ phát hiện reference sai có hệ thống (như ca R4) — khi đó re-review các frame bị ảnh hưởng và tăng version gold.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một auto-rickshaw vượt từ góc trước-phải sang bên phải, xuất hiện cùng lúc ở camera front (zone edge, bị cắt) và camera right (zone mid). Trước khi coi hai box là một vật hoặc xoá một box cần: timestamp đồng bộ hai camera, calibration extrinsic để chiếu hai box về cùng hệ toạ độ (hoặc BEV), và policy output đích (giữ cả hai box theo từng camera hay hợp nhất một box trong BEV).
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: mỗi camera có lens circle, vùng ego và phân bố vật khác nhau; hai người có thể đồng ý nhưng cùng sai (như ca reference R4); report ADASIND chỉ có một camera, 3 frame, không có seam hay track, nên không kiểm được lỗi cross-camera, DUPLICATE ở seam hay nhất quán track qua camera.

# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4
- Tên nhóm: nhom solo leveling
- Repo Public: https://github.com/cuongcoki/K4-DAY11-nhomsololeveling
- Máy giữ hồ sơ chính / người quản lý: máy của Trần Đình Cương
- Slice chung lấy từ mode.json: B1-center
- Tên định danh vai A dùng cho --self: cuong
- Kênh trao đổi nội bộ: làm trực tiếp trên máy chính
- Đại diện nộp (vai C): Đinh Minh Hoàng, 2A202602312
- Commit chốt bài: commit mới nhất trên nhánh main của repo trên (SHA được gửi kèm link khi nộp)

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Trần Đình Cương | 2A202602150 | cuong | Parking/C0/slice, self-QC, lock, rework | [Link file/commit và mô tả phần đã làm] |
| B · QA độc lập | Nguyễn Minh Trung | 2A202602191 | trung | Review trước reference, finding QA, kiểm lại ca sửa | [Link file/commit và mô tả phần đã làm] |
| C · Chẩn đoán & điều phối | Đinh Minh Hoàng | 2A202602312 | hoang | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | [Link file/commit và mô tả phần đã làm] |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | doctor.txt, mode.json, slice B1-center, phân vai; parking XML + observations | doctor không lỗi ✗; parking 17 parking_line + 1 free_space | Xong |
| P2 · Khóa bản đầu | A → B, C | submission/r1_craft/annotations.xml, lock.txt, slice B1-center, mã 5715-FF4C, commit 82d266f | Self-QC không còn cảnh báo; 9 mục checklist | Xong |
| P3 · Chốt QA mù | B → C, A | r2_qa/qa_review.md, 5 dòng r2_qa trong findings.csv, 4 ảnh screenshots/qa_*, mã đã kiểm 5715-FF4C | B xem đủ 3 frame trên overlay (có Claude hỗ trợ đề xuất điểm nghi ngờ) | Ca chưa rõ: L7 frame 056040 |
| P4 · Quyết định sửa | C → A, B | r3_diag/*, findings.csv (r3_diag), 40_decision_log.csv D1–D6, 20_guideline_patch.md, 30_escalation_ticket.md, commit e8a1251 | triage: Findings hợp lệ; mỗi ca rework có rule + bằng chứng | Ca R4 Bus/ThreeWheeler giữ Bus (E0), chờ người thứ ba |
| P5 · Kiểm bản sửa | A → B → C | rework/annotations-v2.xml, lock2.txt mã 6ECD-7779, delta.md | Delta mid: matched 5→7, missing 2→0, spurious 2→0; 8/8 ca rework đã sửa | Một số sửa cuối (xoá ego_body đặt nhầm, box Car 056040, ignore unreadable 006840, edge_zone) do Claude áp qua API CVAT theo yêu cầu của nhóm |
| P6 · Chốt nộp | A, B → C | 10_error_card.md, 45_review_plan.md, 45_sampling_plan.csv, 46_gold_set_plan.md, 50_exit_ticket.md, manifest.json | check exit 0, failed_gates rỗng | Đã push lên https://github.com/cuongcoki/K4-DAY11-nhomsololeveling |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: adasind_056040.jpg L7 (R03/R04). B cho là box trùng với rider L2; A giữ vì thấy vật phía sau; đối chiếu reference R7 và model M6 đều là Car bị che → quyết định đổi L7 thành Car (D2). Bằng chứng: submission/screenshots/qa_056040_L7_vs_L2.png, findings.csv dòng r3_diag L7+R7.
- Ca còn mở: adasind_006840.jpg R4 — nhóm gán Bus, reference gán ThreeWheeler (D1, why=E0_reference_defect). Người theo dõi: C. Phép kiểm tiếp theo: nhờ Lab Coach/người thứ ba xem ảnh gốc độ phân giải đầy đủ.
- Đóng góp của A/B/C vào kế hoạch và exit ticket: A cung cấp ca vẽ/rework (C0 sót xe lẫn nền, 006840); B cung cấp ca QA (L7, R4); C tổng hợp sampling/gold/exit ticket. Các file kế hoạch được soạn nháp với hỗ trợ của Claude (AI) trên máy chính và nhóm đọc lại.
- Thay đổi phân công nếu có: không đổi vai. Toàn bộ thao tác chạy trên một máy chính (máy của Cương). Claude (AI) hỗ trợ chạy lệnh lab11.py, tạo task/export CVAT, đề xuất điểm nghi ngờ khi QA, soạn nháp findings/kế hoạch và áp một số sửa rework qua API CVAT; mỗi thành viên cần tự xác nhận phần của mình ở mục 5.

## 5. Xác nhận trước khi nộp
- [x] A xác nhận nhãn và export đúng phiên bản: Trần Đình Cương / r1_craft/lock.txt (5715-FF4C), rework/lock2.txt (6ECD-7779)
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Nguyễn Minh Trung / r2_qa/qa_review.md, rework/delta.md
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: [Nguyễn Minh Trung / manifest.json, python lab11.py check]
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

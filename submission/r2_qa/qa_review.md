# QA review · B1-center

Mã khóa: 5715-FF4C

- Reviewer (B): Nguyễn Minh Trung, 2A202602191
- Người vẽ nhãn (A): Trần Đình Cương, 2A202602150
- Slice: B1-center
- File review: submission/r1_craft/annotations.xml (bản A đã khóa)
- Review trước khi mở reference/model của slice chính.

| frame | object_ref | rule_id | điều nhìn thấy | điều cần kiểm lại |
|---|---|---|---|---|
| adasind_006840.jpg | (sau L1) | R01 | Xe màu vàng (bus/van hoặc ThreeWheeler) ngay sau, bên trái L1, khoảng x 318–362, y 812–878, cao ~66 px, bị L1 che một phần; chưa có box. Ảnh: screenshots/qa_006840_missing_sau_L1.png | A kiểm lại trên ảnh gốc, bổ sung box đúng class, tick occluded |
| adasind_006840.jpg | L2 | R01 | Pedestrian cao 41 px, sát ngưỡng H=40; box có thể ôm hơi rộng. Ảnh: screenshots/qa_006840_L2_L9.png | Đo lại chiều cao phần nhìn thấy; nếu < 40 px thì bỏ box |
| adasind_006840.jpg | L9 | R05 | Pedestrian sát mép trái (x=7), phần người có thể bị vòng kính/biên cắt nhưng truncated=false. Ảnh: screenshots/qa_006840_L2_L9.png | Xem vật có bị cắt không; nếu có thì truncated=true |
| adasind_036720.jpg | L4 | R05 | Bike (người lái xe hai bánh) sát mép trái (x=28), có thể bị biên cắt nhưng truncated=false. Ảnh: screenshots/qa_036720_L4.png | Xem vật có bị cắt không; nếu có thì truncated=true |
| adasind_056040.jpg | L7 | R03/R04 | Box ThreeWheeler L7 [5,747–192,991] trùm gần hết người áo đỏ đi xe máy, người này đã có box L2 Bike; không thấy rõ một xe ba bánh riêng phía sau. Ảnh: screenshots/qa_056040_L7_vs_L2.png | Kiểm có xe ba bánh thật sau rider không; nếu không thì L7 là box trùng/sai class |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.

## Tổng kết

- Đã xem đủ 3 frame; 5 nhận xét (1 MISSING, 1 BOX_GEOMETRY, 2 ATTRIBUTE, 1 DUPLICATE).
- Ca chưa rõ nhất: L7 frame 056040 (trùng với L2 hay có xe ba bánh thật phía sau).
- Cách làm: Claude (AI) hỗ trợ đề xuất điểm nghi ngờ trên overlay; B (Trung) xem lại từng điểm trên ảnh và chốt cả 5. Chưa mở reference/model của slice chính.

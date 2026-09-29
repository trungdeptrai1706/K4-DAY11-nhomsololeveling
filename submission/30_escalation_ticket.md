# Escalation ticket

## Ticket 1

- **Frame:** adasind_006840.jpg (M13 Car trên auto-rickshaw R1/L1; M12 Bus trên xe ba bánh vàng R4; M8 Truck + M10 Car trùng trên cùng xe R6). Cùng xu hướng ở 056040 và 036720: model bỏ sót auto-rickshaw lớn bị cắt ở rìa (L5+R5, L1+R1).
- **Ảnh chụp:** `submission/screenshots/qa_006840_missing_sau_L1.png`; overlay đầy đủ ở `submission/r3_diag/model_compare.html`.
- **Expected impact:** nếu dùng YOLO26m làm pre-label, ThreeWheeler — class phổ biến trong dữ liệu đường phố Ấn Độ — sẽ bị gán Car/Bus/Truck, annotator phải sửa class hàng loạt; box kép khác class làm tăng SPURIOUS và có thể lọt vào gold set nếu review lỏng. Trên slice này ThreeWheeler là class yếu nhất cả với người (precision/recall 0.714) lẫn model.
- **Owner:** `ai_team`
- **Recommendation:** (1) bổ sung ánh xạ class auto-rickshaw/e-rickshaw → ThreeWheeler khi fine-tune hoặc hậu xử lý; (2) thêm NMS liên class để bỏ box kép cùng vật; (3) lấy mẫu thêm ảnh fisheye có auto-rickshaw ở rìa và bị cắt để đánh giá lại trước khi dùng model làm pre-label.

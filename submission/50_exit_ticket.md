# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? — Không phải `DUPLICATE`: trên mỗi ảnh camera, box đó đúng vì vật thật sự nhìn thấy ở cả hai. `DUPLICATE` chỉ dùng khi cùng một vật bị vẽ hai box trên **cùng một ảnh**. Ca seam cần quy tắc riêng: annotation space theo từng camera giữ cả hai box; nếu output đích là BEV hoặc danh sách vật hợp nhất thì chỉ ghép khi có timestamp đồng bộ, calibration để chiếu về cùng toạ độ và policy chọn/hợp nhất box. Nếu thiếu bằng chứng thì giữ cả hai và gắn cờ seam, không xoá.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. — Giữ cùng track ID khi vẫn là cùng một vật và còn quan sát được liên tục (kể cả bị che một phần). Thêm keyframe khi hình học đổi lớn (vật đi từ center ra edge bị méo mạnh, đổi kích thước, bắt đầu bị cắt) để nội suy không lệch. Đặt Outside khi vật rời trường nhìn hoặc bị che hoàn toàn; nếu quay lại mà không chắc là cùng vật thì mở track mới. Trước khi nối track qua hai camera cần: timestamp đồng bộ, calibration extrinsic để chiếu vị trí, vật khớp về class/hình dạng/hướng đi ở vùng seam, và policy xử lý khoảng hở.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? — adasind_006840.jpg R4: reference gán ThreeWheeler, nhóm phóng to thấy kính trước lớn, đầu phẳng giống bus/van, model M12 cũng Bus. Nhóm giữ Bus, ghi `why=E0_reference_defect`, `action=keep_with_reason` và decision D1 để người thứ ba xác nhận, không đổi theo reference chỉ để khớp số. Ngược lại, ở 056040 L7, B nghi là box trùng nhưng đối chiếu cho thấy đó là ô tô bị che bị gán sai class → sửa. Nếu làm lại: soát riêng một lượt "vật bị che/lẫn nền" trước khi khoá (C0 và 006840 đều sót ở đúng loại này), và đo chiều cao ca sát ngưỡng trước khi vẽ.

Đóng góp: A (Cương) cung cấp ca vẽ/rework, B (Trung) cung cấp ca QA L7/R4, C tổng hợp. Có dùng Claude hỗ trợ soạn nháp; nhóm đã đọc lại.

# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Vùng **mid** đông xe, che khuất dày (adasind_006840.jpg) | L: 2 missing + 2 spurious trước rework (L7 lỏng, L8 trong vùng unreadable, R4 bị L1 che); M: 7 box M_only, 2 box kép khác class | Nhiều vật nhỏ xếp chồng sau auto-rickshaw lớn; cả người lẫn model sai ở cùng chỗ; có ca reference nghi sai class (R4 Bus/ThreeWheeler) | Overlay L/R/M, screenshots/qa_006840_*.png, dòng r3_diag 006840, decision D1/D4 |
| **Class ThreeWheeler** trên cả slice (006840, 056040) | Class yếu nhất: precision/recall 0.714 với L; model gọi auto-rickshaw là Car/Bus (M13, M12); L7 056040 gán ThreeWheeler cho ô tô | Lỗi class có hệ thống, lặp giữa người và model, ảnh hưởng trực tiếp pre-label và gold set | local_quality.md, local_quality_confusion.csv, screenshots/qa_056040_L7_vs_L2.png, 30_escalation_ticket.md |

Giới hạn của kết luận từ ba frame ADASIND: chỉ 3 frame, 20 vật reference, một camera, một thời điểm; teaching reference không phải gold và có thể sai (ca R4). Tỷ lệ lỗi ở đây không suy rộng được cho cả dataset hay cho hệ SVM bốn camera; chỉ dùng để chọn nơi cần soi kỹ.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: chọn theo cảnh (scene/clip) trước rồi mới tới frame — mỗi cảnh tối đa 2–3 frame cách nhau ≥ 2 giây, để không đếm nhiều frame liền nhau của cùng cảnh như nhiều ca độc lập; kiểm bảng phủ theo camera × normal/hard × điều kiện (ngày/đêm, mưa, đông xe) × class (đặc biệt ThreeWheeler và vật ở rìa); ô nào trống thì bổ sung. Kế hoạch này chỉ giúp **tìm ca cần soi** vì mẫu chọn có chủ đích, dồn vào hard case, nên không phải mẫu ngẫu nhiên đại diện — không dùng để ước lượng tỷ lệ lỗi thật; muốn đo tỷ lệ lỗi cần thêm một mẫu ngẫu nhiên phân tầng riêng.

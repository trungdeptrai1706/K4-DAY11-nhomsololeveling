# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 10 | 1 | 0 | 5 | 6 | MISSING (1) |
| mid | 7 | 2 | 2 | 3 | 6 | BOX_GEOMETRY (1) |
| edge | 3 | 0 | 0 | 2 | 5 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: người (L) gãy nhiều nhất ở **mid** (2 missing + 2 spurious trên 7 vật reference: box L7 lỏng và L8 trong vùng unreadable ở 006840); center chỉ 1 missing (xe ba bánh bị L1 che), edge 0 lỗi. Model (M) gãy ở mọi zone nhưng nặng nhất ở **center** (5 missing, 6 thừa) và **mid** (3 missing, 6 thừa); edge có 2/3 vật bị M bỏ sót.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: lỗi của L tập trung ở các vật nhỏ, xếp chồng sau xe khác (che khuất dày ở 006840), không phải do méo rìa ảnh — ở edge L khớp 3/3. Lỗi của M chủ yếu là ánh xạ class: auto-rickshaw bị gọi Car/Bus (M13, M12), cùng một xe sinh box kép Truck+Car (M8, M10), và bỏ sót vật lớn bị cắt ở rìa (036720 L1, 056040 L5) — phù hợp giả thuyết model huấn luyện trên ảnh thường, chưa quen fisheye và taxonomy ThreeWheeler. Giới hạn: chỉ 3 frame, 20 vật reference, một camera; zone center/mid/edge đo theo khoảng cách tới tâm vòng kính, không phải khoảng cách tới xe; không đủ để kết luận tỷ lệ lỗi cho cả hệ SVM.

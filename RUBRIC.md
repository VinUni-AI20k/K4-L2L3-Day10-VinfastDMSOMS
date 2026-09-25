# RUBRIC.md — Cách chấm điểm Lab 10

Điểm cuối cùng là một con số **0–100**, tính tự động từ bài làm của bạn trên CVAT so với đáp án
gốc (ground truth) — giảng viên không chấm tay từng điểm.

## Nguyên tắc chung

Mỗi bạn có 3 task: `DMS_subject_A`, `DMS_subject_B`, `OMS`. Mỗi task được chấm thành một điểm
riêng từ 0–100, sau đó:

```
Điểm cuối cùng = trung bình cộng (DMS_subject_A + DMS_subject_B + OMS) / 3
```

Ba task có trọng số bằng nhau — không task nào quan trọng hơn task nào.

## Cách chấm task DMS (subject_A / subject_B)

Với 50 điểm landmark trên mỗi ảnh, điểm task gồm 2 phần:

- **Độ đầy đủ (completeness, trọng số 40%):** tỉ lệ số điểm bạn đã đặt trên tổng số điểm cần có.
  Đặt thiếu điểm nào, phần đó mất điểm — dù các điểm khác có chính xác đến đâu.
- **Độ chính xác (accuracy, trọng số 60%):** dựa trên khoảng cách trung bình (tính bằng pixel)
  giữa điểm bạn đặt và vị trí đúng trong đáp án gốc. Sai lệch từ 30px trở lên tại một điểm coi
  như không có điểm ở phần chính xác cho điểm đó; sai lệch 0px được điểm tối đa.

```
Điểm task DMS = 100 × (0.4 × độ_đầy_đủ + 0.6 × độ_chính_xác)
```

## Cách chấm task OMS

OMS có 2 phần được chấm tự động:

- **Phát hiện đối tượng (detection, trọng số 60%):** dùng chỉ số F1 — so khớp từng hình chữ nhật
  bạn vẽ với đáp án gốc theo độ trùng khớp diện tích (IoU ≥ 0.5) và đúng nhãn lớp. Vẽ thiếu đối
  tượng (bỏ sót) hoặc vẽ thừa đối tượng không có thật đều bị trừ điểm ở phần này.
- **Tư thế cơ thể `body` (skeleton, trọng số 40%):** chấm giống hệt cách chấm DMS ở trên (đầy đủ
  40% + chính xác 60%), áp dụng cho 17 điểm khung xương.

```
Điểm task OMS = 100 × (0.6 × F1_phát_hiện + 0.4 × điểm_tư_thế)
```

> **Giới hạn đã biết:** mask `seat_belt` (dây an toàn) **chưa được chấm tự động** trong phiên bản
> hiện tại — giảng viên sẽ xem xét thủ công phần này nếu cần tính thêm vào điểm. Đây là một giới
> hạn được công bố rõ ràng, không phải một lỗi bị bỏ sót.

## Một vài ví dụ cụ thể (đã kiểm chứng bằng dữ liệu thật)

| Chất lượng bài làm | Điểm DMS mẫu | Ghi chú |
|---|---|---|
| Đặt đúng gần như hoàn hảo | ~100 | Sai lệch trung bình ~0px |
| Đặt đủ điểm nhưng hơi lệch (sai số nhỏ, vài pixel) | ~95 | Vẫn được điểm cao vì đầy đủ + khá chính xác |
| Đặt đủ điểm nhưng sai lệch nhiều (vài chục pixel) | ~40 | Vẫn được điểm nhờ phần "đầy đủ" (40%), nhưng mất gần hết phần "chính xác" |
| Không nộp bài / không đặt điểm nào | 0 | Không có gì để so sánh |

## Bạn có thể tự kiểm tra tiến độ như thế nào?

Điểm chỉ được tính **sau khi bạn đánh dấu Job là "Completed"** (xem [GUIDE.md](GUIDE.md) bước 5).
Trước đó, tiến độ của bạn vẫn được lưu trên CVAT nhưng chưa được chấm chính thức. Nếu muốn biết
mình đã đặt đủ 50/50 điểm hay chưa, xem lại từng ảnh trong Job — CVAT hiển thị số lượng đối tượng
đã gán ở khung bên phải màn hình.

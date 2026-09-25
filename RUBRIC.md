# RUBRIC.md — Cách chấm điểm Lab 10

Điểm cuối cùng: **0–100**, tính tự động, so bài làm của bạn với đáp án gốc.

```
Điểm cuối cùng = (Điểm DMS_subject_A + Điểm DMS_subject_B + Điểm OMS) / 3
```

## DMS_subject_A / DMS_subject_B

- **Độ đầy đủ (30%):** tỉ lệ số điểm landmark đã đặt / 50 điểm.
- **Độ chính xác (70%):** dùng **NME** (Normalized Mean Error) — sai số vị trí, chuẩn hoá theo
  khoảng cách 2 mắt (chuẩn ngành facial landmark, không đo pixel thô vì mặt to/nhỏ khác nhau).
  NME = 0 → điểm tối đa; NME ≥ 10% → 0 điểm phần này.

```
Điểm task = 100 × (0.3 × độ_đầy_đủ + 0.7 × điểm_NME)
```

## OMS

| Thành phần | Trọng số | Chỉ số dùng |
|---|---|---|
| Hình chữ nhật (person, head, steering_wheel, ...) | 50% | IoU trung bình theo nhiều ngưỡng (0.50–0.95, giống COCO) |
| Khung xương `body` (17 điểm tư thế) | 30% | OKS (Object Keypoint Similarity — chỉ số chuẩn COCO pose) |
| Mask `seat_belt` | 20% | Mask IoU |

```
Điểm task = 100 × (0.5 × IoU_box + 0.3 × OKS + 0.2 × mask_IoU)
```

## Ví dụ

| Chất lượng bài làm | Điểm ~ |
|---|---|
| Gần hoàn hảo | 100 |
| Đủ, sai lệch nhỏ | 85–95 |
| Đủ nhưng sai lệch nhiều | 30–40 |
| Không nộp | 0 |

Điểm chỉ tính sau khi bạn đánh dấu Job **Completed** (xem [GUIDE.md](GUIDE.md)).

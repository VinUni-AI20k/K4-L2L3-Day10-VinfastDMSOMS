# RUBRIC.md — Cách chấm điểm Lab 10

Điểm cuối cùng là một con số **0–100**, tính tự động từ bài làm của bạn trên CVAT so với đáp án
gốc (ground truth), dùng các **phương pháp đánh giá tiêu chuẩn trong thị giác máy tính** — không
phải công thức tự chế.

## Nguyên tắc chung

Mỗi bạn có 3 task: `DMS_subject_A`, `DMS_subject_B`, `OMS`. Mỗi task được chấm thành một điểm
riêng từ 0–100, sau đó:

```
Điểm cuối cùng = trung bình cộng (DMS_subject_A + DMS_subject_B + OMS) / 3
```

Ba task có trọng số bằng nhau.

## Cách chấm task DMS (subject_A / subject_B) — dùng NME

Bài toán landmark khuôn mặt trong nghiên cứu thị giác máy tính (các bộ dữ liệu chuẩn như 300W,
WFLW) **không** chấm bằng khoảng cách pixel thô, vì khuôn mặt to/nhỏ khác nhau trong từng ảnh sẽ
khiến cùng một sai số pixel bị đánh giá bất công. Chuẩn ngành dùng **NME (Normalized Mean
Error)** — sai số được **chuẩn hoá theo khoảng cách giữa hai mắt** (inter-ocular distance) của
chính khuôn mặt đó:

```
NME = (khoảng cách trung bình giữa điểm bạn đặt và điểm đúng) / (khoảng cách giữa 2 mắt)
```

Điểm task gồm 2 phần:

- **Độ đầy đủ (completeness, 30%):** tỉ lệ số điểm bạn đã đặt trên tổng số điểm cần có (50 điểm).
- **Độ chính xác (70%):** dựa trên NME, quy đổi theo ngưỡng "thất bại" 10% mà chuẩn 300W Challenge
  quốc tế đã dùng — NME = 0 được điểm tối đa, NME ≥ 10% bị 0 điểm phần này.

```
Điểm task DMS = 100 × (0.3 × độ_đầy_đủ + 0.7 × điểm_NME)
```

## Cách chấm task OMS — dùng OKS, IoU và mask IoU

OMS có 3 phần được chấm tự động, mỗi phần dùng đúng phương pháp chuẩn cho loại nhãn đó:

- **Phát hiện đối tượng (rectangle, trọng số 50%):** so khớp từng hình chữ nhật với đáp án gốc
  theo **IoU (Intersection over Union — tỉ lệ diện tích chồng lấn)**. Thay vì chỉ dùng một ngưỡng
  IoU ≥ 0.5, hệ thống lấy **trung bình trên nhiều ngưỡng IoU từ 0.50 đến 0.95** (giống cách bộ dữ
  liệu chuẩn COCO đánh giá phát hiện đối tượng) — vẽ khung càng khít với vật thể thật, điểm càng
  cao, không chỉ cần "gần đúng".
- **Tư thế cơ thể `body` (skeleton 17 điểm, trọng số 30%):** dùng **OKS (Object Keypoint
  Similarity)** — chính là chỉ số COCO dùng để đánh giá bài toán pose estimation, với hằng số
  chuẩn riêng cho từng điểm (mắt/vai/khuỷu tay/... có độ khó khác nhau nên dung sai khác nhau).
- **Mask `seat_belt` (trọng số 20%):** dùng **mask IoU** — tỉ lệ chồng lấn giữa vùng bạn tô và
  vùng đúng, tính theo từng pixel.

```
Điểm task OMS = 100 × (0.5 × IoU_phát_hiện + 0.3 × OKS_tư_thế + 0.2 × mask_IoU_dây_an_toàn)
```

Nếu một ảnh không có đối tượng nào của một lớp nhất định trong đáp án gốc (ví dụ ảnh không có
dây an toàn nhìn thấy được), phần đó được bỏ qua cho ảnh đó thay vì tính là 0 điểm.

## Một vài ví dụ cụ thể (đã kiểm chứng bằng dữ liệu thật)

| Chất lượng bài làm | Điểm DMS mẫu | Điểm OMS mẫu | Ghi chú |
|---|---|---|---|
| Gần như hoàn hảo | ~100 | ~100 | Sai lệch trung bình gần 0 |
| Đủ điểm/đối tượng, sai lệch nhỏ vài pixel | ~85 | ~95 | Vẫn cao vì đủ + khá chính xác |
| Đủ điểm/đối tượng nhưng sai lệch nhiều | ~30 | ~40 | Mất phần lớn điểm chính xác, chỉ còn phần đầy đủ |
| Không nộp bài | 0 | 0 | Không có gì để so sánh |

## Vì sao dùng NME/OKS/IoU thay vì đo khoảng cách pixel đơn giản?

Một khuôn mặt chụp gần (to trong khung hình) và một khuôn mặt chụp xa (nhỏ trong khung hình)
cùng bị lệch 5 pixel sẽ có ý nghĩa rất khác nhau — 5 pixel trên khuôn mặt to là sai số nhỏ, trên
khuôn mặt nhỏ là sai số lớn. NME/OKS chuẩn hoá theo kích thước thật của đối tượng nên so sánh công
bằng giữa các ảnh khác nhau — đây là lý do các bộ dữ liệu và cuộc thi thị giác máy tính lớn trên
thế giới đều dùng cách chuẩn hoá này thay vì đo khoảng cách pixel thô.

## Giới hạn đã biết

Điểm OKS cho tư thế `body` dùng diện tích khung bao quanh 17 điểm khung xương làm thước đo tỉ lệ
cơ thể (thay vì diện tích khung `person` được ghép riêng cho đúng người đó) — đây là một xấp xỉ
hợp lý khi không có khung `person` được gán khớp chắc chắn với từng khung xương, không phải cách
tính OKS gốc 100% từ bộ dữ liệu COCO.

## Bạn có thể tự kiểm tra tiến độ như thế nào?

Điểm chỉ được tính **sau khi bạn đánh dấu Job là "Completed"** (xem [GUIDE.md](GUIDE.md) bước 5).
Trước đó, tiến độ của bạn vẫn được lưu trên CVAT nhưng chưa được chấm chính thức.

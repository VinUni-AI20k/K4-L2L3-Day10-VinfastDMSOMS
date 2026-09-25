# GUIDE.md — Hướng dẫn gán nhãn Lab 10

> ⚠️ **Nhắc lại NDA:** đây là dữ liệu độc quyền của VinFast mà bạn đã ký cam kết bảo mật từ đầu
> khoá học. Chỉ gán nhãn bên trong CVAT — không tải ảnh về, không chụp màn hình, không chia sẻ ra
> ngoài. Vi phạm đồng nghĩa vi phạm NDA và có thể dẫn đến trách nhiệm pháp lý cá nhân. Xem chi
> tiết ở [README.md](README.md).

## Bước 1 — Đăng nhập CVAT

1. Truy cập: **https://cvat.note.transformerlabs.ai**
2. Đăng nhập bằng tài khoản đã được giảng viên cung cấp:
   - **Tên đăng nhập:** đúng bằng **MSSV** của bạn (ví dụ: `2A202602041`)
   - **Mật khẩu:** do giảng viên cấp riêng cho bạn
3. Nếu chưa có tài khoản, liên hệ giảng viên/TA — **không tự tạo tài khoản mới**.

## Bước 2 — Tìm 3 task được giao cho bạn

Vào menu **Tasks**. Bạn sẽ thấy đúng **3 task** mang tên theo định dạng:

```
{Loại bài}_{Lớp}_{MSSV}
```

Ví dụ, nếu MSSV của bạn là `2A202602041` và bạn học lớp `2A`, phòng `d303`:

- `DMS_subject_A_L2A-d303_2A202602041`
- `DMS_subject_B_L2A-d303_2A202602041`
- `OMS_L2A-d303_2A202602041`

Mỗi task có sẵn **15 ảnh**, chưa có nhãn nào (canvas trắng) — nhiệm vụ của bạn là gán nhãn từ
đầu theo đúng hướng dẫn bên dưới, không phải sửa nhãn có sẵn.

## Bước 3 — Gán nhãn DMS (subject_A và subject_B)

Mở task, bấm vào **Job** để bắt đầu gán nhãn. Mỗi ảnh cần đặt đủ **50 điểm landmark khuôn mặt**,
chia thành 7 nhóm khung xương (skeleton):

| Nhóm | Số điểm |
|---|---|
| `longmaytrai` (lông mày trái) | 5 |
| `longmayphai` (lông mày phải) | 5 |
| `songmui` (sống mũi) | 4 |
| `mattrai` (mắt trái) | 8 |
| `matphai` (mắt phải) | 8 |
| `moingoai` (viền môi ngoài) | 12 |
| `moitrong` (viền môi trong) | 8 |

Chọn công cụ **Skeleton** trong thanh công cụ bên trái, chọn đúng nhãn nhóm, và đặt từng điểm lên
đúng vị trí trên khuôn mặt theo thứ tự đã quy định trong skeleton template. Phóng to (zoom) ảnh để
đặt điểm chính xác.

subject_A và subject_B là hai người khác nhau (không đeo kính / có đeo kính) — quy trình gán nhãn
giống hệt nhau cho cả hai task.

## Bước 4 — Gán nhãn OMS

Task OMS có nhiều loại nhãn hơn — mỗi ảnh chụp toàn cảnh khoang xe, có thể có nhiều người và
nhiều vật thể cùng lúc:

- **Hình chữ nhật (rectangle):** `person`, `head`, `steering_wheel`, `laptop`, `cell_phone`,
  `infant`, `baby_seat`, `baby_seat_forward`, `baby_doll`, `food`, `cigarette`, `bag` — vẽ khung
  bao quanh chính xác từng đối tượng xuất hiện trong ảnh (có thể không có đủ tất cả các lớp trong
  mỗi ảnh, chỉ gán nhãn những gì thực sự xuất hiện).
- **Khung xương (skeleton) `body`:** 17 điểm tư thế cơ thể — gán cho **người ngồi ghế lái**
  (theo đúng quy ước trong video hướng dẫn OMS).
- **Mask `seat_belt`:** vùng dây an toàn — dùng công cụ vẽ mask/brush để tô đúng vùng dây an
  toàn nhìn thấy được.

Xem video hướng dẫn OMS (giảng viên cung cấp riêng) trước khi bắt đầu để nắm quy ước chính xác
cho từng lớp.

## Bước 5 — Lưu bài

CVAT tự động lưu khi bạn thao tác, nhưng để chắc chắn:

1. Bấm **Save** (biểu tượng đĩa mềm, góc trên bên trái) thường xuyên trong lúc làm.
2. Sau khi gán nhãn xong toàn bộ 15 ảnh của một task, vào **Menu → Finish the job** (hoặc đổi
   trạng thái Job sang **Completed** ở khung bên phải) để đánh dấu đã hoàn thành.
3. Lặp lại cho đủ cả 3 task.

**Deadline nộp bài do giảng viên thông báo riêng — nộp trễ sẽ không được tính điểm phần đó.**

## Câu hỏi thường gặp

| Câu hỏi | Trả lời |
|---|---|
| Task của tôi trống, không có ảnh nào? | Báo ngay cho giảng viên — có thể tài khoản bị gán nhầm. |
| Tôi gán nhầm nhóm điểm/nhãn? | Xoá điểm/hình sai (chọn rồi bấm Delete) và gán lại, không cần làm lại từ đầu. |
| Tôi không chắc quy ước gán nhãn cho một lớp nào đó? | Xem lại video hướng dẫn tương ứng (DMS hoặc OMS) trước khi hỏi — hầu hết câu hỏi đã được trả lời trong video. |
| Điểm được tính thế nào? | Xem [RUBRIC.md](RUBRIC.md). |

# Lab 10 — Gán nhãn dữ liệu VinFast DMS & OMS

Chào các bạn học viên K4! Đây là bài lab gán nhãn dữ liệu thật từ hệ thống giám sát người lái
(DMS) và giám sát khoang xe (OMS) của VinFast.

- **Bắt đầu tại đây:** [GUIDE.md](GUIDE.md) — hướng dẫn từng bước: đăng nhập, tìm 3 task của
  bạn, gán nhãn, lưu bài.
- **Quy tắc gán nhãn chi tiết:** [LABEL_GUIDELINE.md](LABEL_GUIDELINE.md) — lớp nào cần gán cho
  OMS, và **chiều trái/phải** cho từng task (DMS và OMS dùng quy ước ngược nhau — đọc kỹ trước
  khi gán để tránh phải sửa lại toàn bộ).
- **Cách chấm điểm:** [RUBRIC.md](RUBRIC.md) — công thức tính điểm 0–100 cho bài lab này.

## ⚠️ Lưu ý quan trọng — Bảo mật dữ liệu (NDA)

> **Đây là dữ liệu độc quyền của VinFast.** Ngay từ đầu khoá học, học viên đã ký **thoả thuận bảo
> mật (NDA)** cam kết không sao chép, phát tán, hay để lộ dữ liệu này ra ngoài phạm vi khoá học
> dưới bất kỳ hình thức nào.
>
> **Làm rò rỉ dữ liệu (tải ảnh về máy, chụp màn hình, gửi ra ngoài, đăng lên mạng xã hội, chia sẻ
> với người không thuộc khoá học...) là vi phạm NDA đã ký và học viên sẽ phải chịu trách nhiệm
> pháp lý cá nhân với VinFast**, không chỉ là vấn đề kỷ luật trong khoá học.
>
> Nếu bạn vô tình làm lộ dữ liệu hoặc phát hiện người khác làm vậy, hãy báo ngay cho giảng viên.

## Lưu ý khác

- Đây là **dữ liệu cá nhân thật** (khuôn mặt, hình ảnh trong khoang xe). Chỉ xem và gán nhãn bên
  trong CVAT. **Không tải ảnh về máy, không chụp màn hình, không chia sẻ ra ngoài.**
- Bạn được cấp **3 task** trên máy chủ CVAT: 1 task DMS_subject_A, 1 task DMS_subject_B, 1 task
  OMS. Cả 3 đều cần hoàn thành để có điểm đầy đủ.
- Repo này (`student/`) chỉ chứa tài liệu hướng dẫn — không có ảnh, không có đáp án.

## Danh sách học viên cần TA xử lý (297 học viên, rà soát ngày 26/09/2026)

Rà soát 297 học viên trong `danh sách lớp lab l2-3.xlsx` (đã nối với `Tài Khoàn VLearn.xlsx`)
theo 4 loại lỗi: thiếu email VinUni, thiếu MSSV, trùng email nhưng khác tên, thiếu tài khoản CVAT.

| Loại lỗi | Số lượng | Chi tiết |
|---|---|---|
| Thiếu MSSV | 0 | Không có — tất cả 297 học viên đã có MSSV. |
| Trùng email — khác tên | 0 | Không có — không có email nào bị gán cho hai tên khác nhau. |
| Thiếu email VinUni | 2 | Xem bảng bên dưới. |
| Thiếu tài khoản CVAT | 20 | Xem bảng bên dưới. |

### Thiếu email VinUni (2)

Có MSSV thật (từ vlearn, khớp theo tên), nhưng tài khoản VinUni "chưa tạo":

| MSSV | Họ tên | Lớp |
|---|---|---|
| 2A202603020 | BÙI QUANG THÁI | 2a-d305 |
| 2A202603022 | NGUYỄN QUANG TÙNG | 2b-d305 |

### Danh tính chưa xác nhận (1) — trùng tên trong vlearn

Không thuộc 4 loại lỗi trên nhưng cần TA xác nhận riêng: vlearn có **3 học viên khác nhau** tên
"NGUYỄN VIỆT HOÀNG". Roster có 3 dòng cùng tên này ở 3 lớp khác nhau; 2 dòng đã khớp email sẵn có
trong roster (2a-d303: `hoangnv6`, 2b-d305: `hoangnv8`). Dòng thứ 3 (2a-d303, ban đầu để trống
email) được gán tạm bằng loại trừ — **chưa chắc chắn, cần TA xác nhận lại**:

| MSSV (tạm gán) | Họ tên | Lớp | Email (tạm gán) |
|---|---|---|---|
| 2A202602424 | NGUYỄN VIỆT HOÀNG | 2a-d303 | 26ai.hoangnv9@vinuni.edu.vn |

### Thiếu tài khoản CVAT (20)

Có MSSV hợp lệ, nhưng chưa có tài khoản trên `cvat.note.transformerlabs.ai` (org `ai20k-labs`) —
username tài khoản CVAT phải trùng MSSV. Sau khi tạo tài khoản, chạy lại
`Day10/tools/assign_student_jobs.py` (idempotent) để gán job cho các em này:

| MSSV | Họ tên | Lớp |
|---|---|---|
| 2A202602080 | ĐỖ VĂN TỬU | 2a-d303 |
| 2A202602082 | PHAM HAI DANG | 2a-d303 |
| 2A202602104 | PHẠM MINH HOÀNG | 2a-d303 |
| 2A202602109 | NGUYỄN HOÀNG MINH | 2a-d303 |
| 2A202602117 | ĐỖ VĂN TRUNG | 2a-d303 |
| 2A202602424 | NGUYỄN VIỆT HOÀNG | 2a-d303 |
| 2A202602196 | ĐINH TIẾN MẠNH | 2a-d304 |
| 2A202602197 | PHẠM VĂN HUY | 2a-d304 |
| 2A202602216 | NGUYỄN VĂN VŨ | 2a-d304 |
| 2A202602255 | NGÔ HOÀNG NAM | 2a-d305 |
| 2A202602294 | NGUYỄN ĐỨC HẢI | 2a-d305 |
| 2A202602042 | NGUYỄN THẾ PHÁCH | 2b-d303 |
| 2A202602086 | HOÀNG NGUYỄN VIỆT | 2b-d303 |
| 2A202602124 | TRẦN ANH MINH | 2b-d303 |
| 2A202602136 | LẠI KHÁNH TOÀN | 2b-d303 |
| 2A202602180 | ĐÀO HỒNG THẮNG | 2b-d304 |
| 2A202602237 | TRẦN QUỐC ĐẠT | 2b-d304 |
| 2A202602296 | TRẦN VĂN DŨNG | 2b-d305 |
| 2A202602301 | DƯƠNG ĐẠI SƠN | 2b-d305 |
| 2A202602320 | NGUYỄN MẠNH DŨNG | 2b-d305 |

(2A202602424 xuất hiện ở cả hai bảng — vừa là danh tính chưa xác nhận, vừa chưa có tài khoản CVAT.)

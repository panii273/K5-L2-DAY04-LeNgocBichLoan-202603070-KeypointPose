# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Le Ngoc Bich Loan
- MSSV: 2A202603070
- Email: lengocbichloan5@gmail.com
- Link repository: https://github.com/panii273/K5-L2-DAY04-LeNgocBichLoan-202603070-KeypointPose.git
- Phiên bản CVAT (Help → About):
- Máy: máy tính của bạn hỗ trợ · hệ điều hành Macbook pro · RAM 16 GB · CVAT chế độ full
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có 
- Giờ bắt đầu: 16h00
- Giờ kết thúc: 9h00

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` |Skeleton |17|có theo JSON export |có theo JSON export |19 |
| `face` |Skeleton |13 |có theo JSON export |có theo JSON export |13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có, theo cấu hình label; cần đối chiếu với Label Constructor.

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):
Rê chuột vào đúng điểm cần thay đổi, nhấn Q để bật/tắt occluded (v = 1), nhấn O để bật/tắt outside (v = 0), hoặc nhấn chuột phải vào điểm để chọn trong menu.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 |5 |chưa thống kê |0 |không ghi nhận |
| `occluded` | 3 |6 |chưa thống kê |0 |không ghi nhận |
| `back` | 2 |4 |chưa thống kê |0 |không ghi nhận |
| `small` | 1 |2 |cần kiểm tra thêm |0 |không ghi nhận |
| `crowd` | 1 |3 |cần kiểm tra thêm |0 |không ghi nhận |
| `faces` | 8 | | — |0 |không ghi nhận |

- Số ảnh người đã xong ở mốc phút 105: 8 / 10 
- Thời gian thực tế (phút): CP1 60 · CP2 60 · CP3 chưa ghi nhận
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?
ảnh 000000431988.jpg ảnh có hai người trượt ván, trong đó một người quay lưng và một người ở tư thế đứng. Việc xác định keypoints gặp khó khăn vì một số vùng tay bị che khuất, kích thước người trong ảnh nhỏ và hướng cơ thể không rõ ràng. Điều này làm việc xác định trái/phải và chọn visibility khó hơn.
...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
|000000122199.jpg |Skeleton 1 |left_hip, right_hip, left_knee, right_knee |Cần xem lại CVAT |Hướng trái/phải |Checker cảnh báo vị trí hông và gối có thể bị đảo |
|

face_560526.jpg |Skeleton mặt 1 |Các điểm vùng mắt|v=0 trong JSON hiện tại |v=1 / v=0 |Mũ che vùng mắt, khó xác định chính xác vị trí |
|face_99874.jpg |Skeleton mặt 1 |Các điểm vùng mắt |v=0 trong JSON hiện tại |v=1 / v=0 |Kính râm che mắt; cần đối chiếu lại quy tắc visibility |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| | | | | | |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

Ảnh face_99874.jpg: vùng mắt bị kính râm che, cần xác nhận lựa chọn theo guideline.

Ảnh face_560526.jpg: vùng mắt bị mũ che, cần xác định khả năng ước lượng vị trí.

Ảnh 000000381889.jpg: các khớp của người trong đám đông có thể bị người khác hoặc vật thể che.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `LeNgocBichLoan_persons.zip` |000000122199.jpg, skeleton 1 |51 |face_99874.jpg, skeleton 1 |có |
| `LeNgocBichLoan_persons.zip` |000000240340.jpg, skeleton 1 | 51|Đúng cấu trúc visibility |có |
| `LeNgocBichLoan_faces.zip` | |face_99874.jpg, skeleton 1 |39 |Đúng cấu trúc JSON, cần kiểm tra việc đặt cờ mắt |có

Sau khi xuất, CVAT ghi `occluded` thành `v = 1 ` và `outside` thành `v = `. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? Tọa độ của điểm outside trong file có thể giữ tọa độ cũ thay vì 0, 0, theo cách xuất dữ liệu của CVAT 2.x.

Hai job đã chuyển sang completed trên CVAT? Có 

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

File Person:
Số ảnh: 12
Số skeleton: 20
Mỗi skeleton: 17 keypoints = 51 giá trị

Số điểm v=2: 259
Số điểm v=1: 11
Số điểm v=0: 70

File Face:
Số ảnh: 8
Số skeleton: 8
Mỗi skeleton: 13 keypoints = 39 giá trị

Số điểm v=2: 88
Số điểm v=1: 0
Số điểm v=0: 16

Số lỗi cấu trúc: 0
Số cảnh báo tự động: 2

Kết quả: ĐẠT

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

000000122199.jpg: cảnh báo khả năng đảo trái/phải tại hông và gối. Cần kiểm tra hướng người trên CVAT.

000000240340.jpg: cảnh báo khả năng đảo trái/phải tại cổ chân. Cần kiểm tra đường nối các khớp chân.

Kết quả checker đạt về mặt cấu trúc nhưng chưa đủ để xác nhận chất lượng từng điểm.

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png) 
<img width="832" height="1194" alt="image" src="https://github.com/user-attachments/assets/82763ffa-4b3d-4441-871d-9015c6b41f25" />


2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)
   <img width="1296" height="1052" alt="image" src="https://github.com/user-attachments/assets/9b2b19d3-1861-4c47-a194-201a1424a1b3" />


4. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)
   <img width="858" height="988" alt="image" src="https://github.com/user-attachments/assets/874aa797-f898-4822-99d8-e15eb37c2c25" />


5. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)
   <img width="312" height="643" alt="1794545517710_131600069462576550_9210539880001417895_9ebf8d8d771906c18d476bc567e3ec8e" src="https://github.com/user-attachments/assets/115b394f-9b48-4075-8145-3ef177d0664e" />


Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   lỗi về máy, máy em quá lag tốn nhiều thời gian mở và reset về bài thì các điểm gán ảnh phải nhìn kỉ góc mép xác định đúng ảnh không đoán mò nếu phần  không nhìn rõ lắm.

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   không có 

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   không có 

## 8. Khó khăn và lỗi kỹ thuật

Trong quá trình thực hiện bài thực hành K5-L2 Day04 Keypoint Pose, em gặp khó khăn với việc cài đặt và khởi chạy môi trường CVAT trên máy tính cá nhân sử dụng Windows 11. Các lỗi liên quan đến Docker Desktop, WSL và kết nối CVAT khiến em không thể thao tác ổn định trên máy.

Do đó, em đã tải bộ dataset được phân công và chuyển sang máy MacBook Pro RAM 16 GB của bạn để tiếp tục thực hiện bài. Em sử dụng môi trường CVAT chế độ Full trên máy này.

Trong quá trình thực hiện, em đã sử dụng tài khoản CVAT ann091005 của bạn mình để gán nhãn và xuất dữ liệu, thay vì tài khoản riêng của em. Em nhận thức được việc này chưa phù hợp với quy định sử dụng tài khoản cá nhân của bài lab.

Sau khi thực hiện gán nhãn, em xuất dữ liệu sang định dạng COCO Keypoints 1.0, bao gồm hai nhóm Person và Face.

Em sử dụng chương trình src/check_submission.py để kiểm tra cấu trúc JSON. Kết quả không phát hiện lỗi cấu trúc, tuy nhiên vẫn có hai cảnh báo cần kiểm tra về vị trí các keypoints trái/phải.

Một số tình huống gán nhãn khó liên quan đến người quay lưng, tư thế cơ thể không thông thường, kích thước người nhỏ và những khớp bị che khuất. Những trường hợp này cần đối chiếu kỹ với guideline khi review.

Việc checker báo đạt chỉ phản ánh tình trạng cấu trúc dữ liệu, chưa đồng nghĩa với việc các annotation đã được xác nhận chính xác hoàn toàn.

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| | | | |
| | | | |
| | | | |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

ChatGPT (OpenAI): Hỗ trợ đọc tài liệu hướng dẫn, giải thích quy tắc gán nhãn skeleton, phân tích file JSON.



# Tự đánh giá — Bùi Văn Thịnh · G12

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | person | seat_flip | Lúc đầu vẽ CVAT mặc định là driver, đã sửa lại thành rear_right | Đã sửa |
| S01_ir.png | child_seat | wrong_class | Ban đầu chọn occupied=yes, sau đó đồng bộ theo quy chuẩn coach | Đã sửa |
| D02.png | face | ok | Nhìn rõ 2 mí mắt khép lại hoàn toàn, gán closed chính xác | ok |
| D03.png | face13 | flag | Điểm mắt phải bị đốm phản xạ LED che khuất đã bật cờ occluded | ok |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên điều chỉnh thuộc tính `seat` khi vừa vẽ xong box `person` (bị CVAT tự điền giá trị mặc định đầu tiên là `driver`).

Vì sao mình mắc: Thao tác vẽ nhanh liên tiếp các box mà chưa mở ngay bảng DETAILS để kiểm tra lại từng thuộc tính.

Lần sau tránh bằng cách: Thiết lập thói quen vẽ xong box nào là bấm phím tắt mở thuộc tính gán ngay vị trí ghế trước khi chuyển sang vẽ đối tượng tiếp theo.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
- Ở cảnh D03, ban đầu tôi phân vân giữa open và closed, bạn tôi chọn unknown do mắt bị đốm phản xạ LED che. Khi đối chiếu lại với nguyên tắc an toàn số 1 của guideline ("không thấy thì unknown"), bạn tôi hoàn toàn đúng và tôi đã học được cách không phỏng đoán dữ liệu khi tín hiệu quang học bị nhiễu.


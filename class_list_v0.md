# Danh sách lớp v0 — Bùi Văn Thịnh · G12

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state | open / closed / unknown | Phát hiện tài xế buồn ngủ (mắt nhắm kéo dài hoặc tần suất chớp mắt bất thường) | Có, trừ khi bị đốm phản xạ LED che |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (nhìn lệch khỏi đường kính lái quá thời gian an toàn) | Có, qua hướng mắt và tư thế đầu |
| 3 | glasses | none / clear / sun / unknown | Cảnh báo camera bị che khuất hoặc tinh chỉnh thuật toán ước lượng mắt khi đeo kính | Có, nhưng kính râm có thể bị xuyên sáng |
| 4 | on_wheel | yes / no / unknown | Giám sát tài xế buông tay khỏi vô lăng (bắt buộc theo chuẩn L2/L3 ADAS) | Có, qua độ tương phản khớp tay và vô lăng |
| 5 | phone | held / mounted / lap | Cảnh báo hành vi sử dụng điện thoại khi đang điều khiển phương tiện | Có, thấy qua hình khối và viền phản xạ |
| 6 | face13 (skeleton) | 13 điểm giải phẫu mặt | Ước lượng góc nghiêng đầu (Head Pose 3D Yaw/Pitch/Roll) và phân tích vi biểu cảm khuôn mặt | Có, thông qua các mốc giải phẫu trên NIR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | seat_occupancy (person) | có / không theo vị trí ghế | Nhận diện có người ngồi để kích hoạt / vô hiệu hóa túi khí tương ứng và cảnh báo thắt dây | Có, nhận diện qua hình dáng cơ thể |
| 2 | child_seat | có / không, occupied (yes/no/unknown) | Kích hoạt bảo vệ an toàn cho ghế trẻ em, cảnh báo bỏ quên trẻ trong xe (CPD) | Có, nhận diện qua hình khối ghế đặc thù |
| 3 | infant_seat | có / không, facing (rear/front) | Tắt túi khí hành khách phía trước khi lắp nôi quay ngược để tránh chấn thương khi va chạm | Có, qua hướng lắp nôi và quai xách |
| 4 | seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo thắt dây an toàn hoặc thắt dây sai quy cách cho từng vị trí ngồi | Có thể khó nếu áo sẫm màu trong bóng tối |
| 5 | object (type) | bag / box / cup / other | Phát hiện hành lý, vật dụng để quên trên xe hoặc tránh kích hoạt nhầm túi khí khi chỉ là đồ vật | Có, dựa vào hình khối và bóng đổ |
| 6 | frame_meta (light/modality) | modality (rgb/ir), light (day/night/unknown) | Chuyển đổi mô hình xử lý phù hợp theo điều kiện ánh sáng thực tế trong cabin | Có, chính là thông tin toàn khung hình |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Khi đồ vật (ví dụ túi xách hoặc ba lô) được đặt trực tiếp bên trong ghế trẻ em `child_seat`, hệ thống phân loại tải trọng túi khí nên ưu tiên kích hoạt logic bảo vệ ghế trẻ em hay tính toán tải trọng như một vật thể thông thường?
   - **Khung ví dụ:** `S01_rgb.png` (có đồ vật đặt trong vùng ghế trẻ em).
   - **Bạn tạm gán thế nào và vì sao:** Gán tách rời 2 bounding box riêng biệt (`child_seat` và `object`) trên cùng vị trí ghế `rear_left` theo đúng quy định phân tách thực thể của guideline v1.0.

2. **Câu hỏi:** Trong điều kiện ánh sáng hồng ngoại gần (NIR), kính râm tối màu bị tia hồng ngoại chiếu xuyên qua khiến tròng kính nhìn như trong suốt, model có nên gắn cờ thuộc tính bổ sung để phân biệt giữa kính trắng thông thường và kính râm bị xuyên sáng hay không?
   - **Khung ví dụ:** `D05.png` (tài xế đeo kính dưới ánh sáng NIR).
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `glasses = clear` theo đúng hình ảnh trực quan thấy được qua tròng kính nhưng ghi chú vào log để đội ngũ phát triển thuật toán nắm được đặc tính vật lý của camera NIR.


# Báo cáo kiểm thử hiệu năng bằng JMeter

## Thông tin sinh viên
- Họ tên: Mạc Anh Đức
- MSSV: BIT220221
- Website được kiểm thử: https://www.wikipedia.org

## Mô tả kịch bản kiểm thử

1. **Kịch bản 1: Cơ bản**
- Số lượng người dùng: 11
- Hành vi: Gửi yêu cầu GET đến `/wiki/Main_Page?student_id=BIT220221`
- Loop Count: 5

## Kết quả kiểm thử

- **Response Time trung bình**: [ghi ở cột Average]
- **Throughput**: [ghi ở cột Throughput]
- **Error Rate**: [ghi ở Error % nếu có, thường là 0%]

## Nhận xét

- Website phản hồi ổn định, không có lỗi.
- Throughput phù hợp với số lượng người dùng mô phỏng.
- Có thể mở rộng kiểm thử tải nặng ở các bước tiếp theo.

2. **Kịch bản 2: Tải nặng**
- Số lượng người dùng: 51
- Ramp-up Period: 30 giây
- Hành vi:
  - Gửi yêu cầu GET đến `/wiki/Main_Page?student_id=BIT220221`
  - Gửi yêu cầu GET đến `/wiki/Special:Random?student_id=BIT220221`

## Kết quả kiểm thử

- **Main Page**
  - Response Time trung bình: 795 ms
  - Throughput: 1.7 requests/sec
  - Error Rate: 0.00%

- **Special:Random**
  - Response Time trung bình: 277 ms
  - Throughput: 1.7 requests/sec
  - Error Rate: 92.16%

## Nhận xét

- Trang chính phản hồi ổn định, không có lỗi.
- Trang `/wiki/Special:Random` bị lỗi do có thể Wikipedia giới hạn truy cập từ tool tự động.
- Tổng Error Rate khá cao (46.08%) → cần kiểm thử lại với trang khác nếu cần độ tin cậy.

3. **Kịch bản 3: Tùy chỉnh**
- Số lượng người dùng: 21
- Thời gian chạy: 60 giây
- Hành vi:
  - Gửi GET đến `/wiki/Special:Search?search=performance&student_id=BIT220221`
  - Gửi GET đến `/wiki/Help:Contents?student_id=BIT220221`

## Kết quả kiểm thử

- **Special:Search**
  - Response Time trung bình: 750 ms
  - Throughput: 12.5 requests/sec
  - Error Rate: 95.24%

- **Help:Contents**
  - Response Time trung bình: 110 ms
  - Throughput: 23.7 requests/sec
  - Error Rate: 100.00%

## Nhận xét

- Hầu hết yêu cầu bị chặn hoặc trả lỗi.
- Có thể do Wikipedia chặn request tự động đến trang đặc biệt.
- Nên chọn các URL ổn định hơn hoặc giảm tần suất request.

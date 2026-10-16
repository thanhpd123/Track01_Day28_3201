# Báo cáo cá nhân — CS13 Lộ trình sản phẩm AI

## 1. Thông tin thành viên

- Họ và tên: Chử Trần Phương Nam
- MSSV: 2A202602675
- Nhóm: H3201
- Đề bài: Đề 1 · SổSạch — Trợ lý đọc hoá đơn đầu vào cho văn phòng kế toán dịch vụ

## 2. Phần việc phụ trách

- Phụ trách chính: **CP1 · Đọc hồ sơ, viết giả thuyết, chỉ số và ngưỡng** (Nhiệm vụ 0 và Nhiệm vụ 1).
- Bằng chứng trang tính trong file [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx):
  - Trang `0_Đầu vào`: các ô `B5:E10`.
  - Trang `1_Danh sách việc`: các ô `B5:E11` (Cột Việc, Kết quả muốn đạt, Giả thuyết, Chỉ số và ngưỡng).

## 3. Đóng góp cụ thể

1. **Trích xuất hồ sơ tình huống (`0_Đầu vào`):**
   - Đọc và làm rõ bản chất "1 việc = 1 hoá đơn được đọc, đối chiếu và nhập vào phần mềm kế toán" với quy mô thử nghiệm 40 doanh nghiệp (~12.000 hoá đơn/tháng).
   - Nắm rõ giới hạn nguồn lực chuyên gia: chị Hạnh chỉ có 3 giờ/tuần sáng thứ Bảy; 1 vòng chấm bộ đề 40 ca tốn 8,5 giờ của chị Hạnh và anh Tùng.
   - Xác nhận trạng thái Bản 2 đã qua cổng phát hành (97,3%, 0 lỗi nghiêm trọng, kappa 0,90) để làm tiền đề bắt đầu ngay từ Mức 1.

2. **Xây dựng danh sách giả thuyết và chỉ số (`1_Danh sách việc`):**
   - Viết toàn bộ 7 việc theo cấu trúc chuẩn: *"Ta tin rằng làm [X] cho [Y] sẽ giúp đạt [Z]; biết đúng khi [Chỉ số] đạt [Ngưỡng]"*.
   - Khống chế toàn bộ chỉ số thành công ở cột E đều có **con số định lượng, cỡ mẫu và ngưỡng chặn rõ ràng**, không dùng tính từ định tính ("nhanh hơn", "tốt hơn").
   - Đề xuất và cùng nhóm bổ sung **Việc số 7: Kiểm tra số tiền và hoá đơn trùng**: Đây là chốt chặn mã lệnh (rule-based guardrail) để giải quyết triệt để yêu cầu nghiêm ngặt của chị Hạnh: *"Sai mã số thuế hay sai tiền thì không được lần nào"*.
   - Tham gia thảo luận khảo sát nguy cơ bị mô hình AI làm thay trong 12 tháng (Slide 81) để làm căn cứ chấm cột L cho CP2.

## 4. Bằng chứng

- File Excel nộp bài: [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx).
- Bằng chứng trực tiếp trên file:
  - `0_Đầu vào!B5:E10`: Đánh dấu đủ 6/6 mục đã đọc, ghi chú rõ các thông số kinh tế và giới hạn giờ chuyên gia.
  - `1_Danh sách việc!B5:E11`: Cột D và E đủ 7 dòng có giả thuyết và chỉ số định lượng, cột O báo toàn bộ "Có".
  - Trang `6_Tự kiểm tra`: Dòng 4 ("Việc được giữ lại mà thiếu giả thuyết hoặc chỉ số có con số") đạt giá trị **0 - Đạt**.

## 5. Tự đánh giá & Phản biện cá nhân

- **Điều hiểu rõ và tự tin nhất:**
  - Nắm vững nguyên lý chuyển từ "danh sách tính năng" sang "danh sách giả thuyết có thể kiểm chứng".
  - Hiểu sâu sắc mối liên kết giữa chỉ số CP1 với thiết kế cổng đánh giá ở CP3: Nếu CP1 không xác lập ngưỡng cờ $\le 20\%$ và 0 lỗi lọt thì CP3 không thể tính được bài toán chi phí (704 đ/hoá đơn) và biên lợi nhuận gộp ($68,8\%$).
- **Giả định còn rủi ro cần kiểm chứng ngoài thực tế:**
  - *Phương pháp đo thời gian:* Việc 1 và Việc 3 đặt chỉ số "giảm 50% - 70% thời gian nhập" hiện phụ thuộc vào việc phần mềm kế toán có hỗ trợ telemetry tự động ghi nhận thời gian thao tác hay không. Nếu không, phải đo thủ công trên mẫu khảo sát.
  - *Rủi ro quy tắc 3/n trên mẫu kiểm định:* Ngưỡng "100% hoá đơn sai bị gắn cờ khi kiểm mẫu 10%" (1.200 hoá đơn) về mặt toán học vẫn có xác suất lọt lỗi tối đa $0,25\%$ trên 90% hoá đơn không kiểm tra. Cần có cơ chế cảnh báo người dùng cuối và đối soát độc lập định kỳ.

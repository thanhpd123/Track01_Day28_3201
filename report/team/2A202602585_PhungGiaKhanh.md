# Báo cáo cá nhân — Phùng Gia Khánh

## 1. Thông tin thành viên

- Họ tên: Phùng Gia Khánh
- MSSV: 2A202602585
- Nhóm và đề CS13: Nhóm H3201 · Đề 1 — SổSạch (trợ lý đọc hoá đơn đầu vào)

## 2. Phần việc phụ trách

- **CP2 · Chấm điểm ưu tiên và ra quyết định sản phẩm.**
- Phụ trách các cột F–L của trang `1_Danh sách việc`, gồm:
  - Độ phủ
  - Tác động
  - Mức tự tin
  - Công sức
  - Sẵn sàng dữ liệu
  - Sẵn sàng đánh giá
  - Rủi ro bị mô hình/nền tảng làm thay
- Tham gia quyết định `Tự làm / Mua / Chờ / Không làm` và ghi căn cứ tại cột P–Q.
- Cùng nhóm kiểm tra thứ hạng trước khi chuyển các việc ưu tiên sang CP3.

## 3. Đóng góp cụ thể

Tôi tham gia chấm và so sánh 7 công việc theo công thức ưu tiên của bài, thay vì chỉ chọn tính năng dựa trên cảm tính.

Kết quả ưu tiên được thống nhất:

| Hạng | Công việc | Điểm | Quyết định |
|---|---|---:|---|
| 1 | Đối chiếu mã số thuế người bán | 15,00 | Mua |
| 2 | Gắn cờ hoá đơn cần người xem | 7,88 | Tự làm |
| 3 | Kiểm tra số tiền và hoá đơn trùng | 6,63 | Tự làm |
| 4 | Nhập tự động hoá đơn điện tử | 4,88 | Mua |
| 5 | Đọc ảnh hoá đơn giấy | 3,77 | Tự làm |
| 6 | Gợi ý tài khoản hạch toán | 1,20 | Chờ |
| 7 | Trả lời câu hỏi thuế chung | 0,23 | Không làm |

### Các quyết định chính

- **Đối chiếu mã số thuế người bán — Mua:** đây là yêu cầu có mức nghiêm trọng cao vì sai mã số thuế không được phép lọt. Dịch vụ tra cứu đã có sẵn nên không cần tự xây lại.
- **Gắn cờ hoá đơn cần người xem — Tự làm:** đây là thành phần quan trọng để quyết định hoá đơn nào cần con người duyệt, trực tiếp ảnh hưởng tới tỷ lệ duyệt và chi phí vận hành.
- **Kiểm tra số tiền và hoá đơn trùng — Tự làm:** có thể kiểm tra bằng quy tắc/mã lệnh, chi phí triển khai thấp và trực tiếp xử lý yêu cầu không để sai tiền lọt vào sổ.
- **Nhập tự động hoá đơn điện tử — Mua:** phần mềm kế toán đã có khả năng tương ứng, nên ưu tiên tích hợp thay vì phát triển lại.
- **Đọc ảnh hoá đơn giấy — Tự làm:** nhóm đã có bản nhận dạng đạt cổng phát hành, nhưng phạm vi sử dụng phụ thuộc tỷ lệ hoá đơn giấy thực tế.
- **Gợi ý tài khoản hạch toán — Chờ:** hiện chưa có đủ dữ liệu hạch toán của từng khách hàng để đánh giá đáng tin cậy. Chỉ nên xem xét lại khi đã tích luỹ dữ liệu.
- **Trả lời câu hỏi thuế chung — Không làm:** nằm ngoài đơn vị công việc chính của sản phẩm là xử lý một hoá đơn, đồng thời có rủi ro cao bị các chatbot hoặc mô hình AI phổ thông thay thế.

Tôi cũng lưu ý rằng **điểm ưu tiên không tự động quyết định phải xây tính năng nào**. Điểm cần được kết hợp với khả năng mua giải pháp có sẵn, độ sẵn sàng của dữ liệu, khả năng đánh giá và rủi ro bị nền tảng khác làm thay.

## 4. Bằng chứng

- `1_Danh sách việc!F5:L11` — các đầu vào dùng để tính điểm ưu tiên.
- `1_Danh sách việc!M5:N11` — điểm và thứ hạng được Excel tự tính.
- `1_Danh sách việc!P5:Q11` — quyết định Tự làm/Mua/Chờ/Không làm và lý do.
- File bài nhóm: [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx)
- Repo nhóm: https://github.com/thanhpd123/Track01_Day28_3201

## 5. Tự đánh giá

- **Điều tôi hiểu rõ:** điểm ưu tiên chỉ là công cụ hỗ trợ quyết định. Một việc có điểm cao vẫn có thể nên **Mua** nếu giải pháp ngoài đã trưởng thành và rẻ hơn tự xây. Ngược lại, một việc quan trọng đối với lợi thế sản phẩm và kiểm soát rủi ro có thể đáng **Tự làm**. Vì vậy phải xem đồng thời tác động, dữ liệu, khả năng đánh giá, công sức và rủi ro bị nền tảng khác làm thay.

- **Giả định còn cần kiểm chứng:** nhóm đang giả định phần lớn hoá đơn đầu vào là hoá đơn điện tử nên `Đọc ảnh hoá đơn giấy` chỉ có độ phủ trung bình. Cần đo tỷ lệ hoá đơn giấy/ảnh thực tế tại văn phòng thử nghiệm. Nếu tỷ lệ này cao hơn dự kiến, điểm ưu tiên và thứ tự của tính năng đọc ảnh cần được đánh giá lại.

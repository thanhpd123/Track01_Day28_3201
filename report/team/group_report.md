# Báo cáo nhóm H3201 — CS13 Lộ trình sản phẩm AI

## 1. Thông tin nhóm

- Tên nhóm: H3201
- Đề CS13: Đề 1 · SổSạch — trợ lý đọc hoá đơn đầu vào cho văn phòng kế toán dịch vụ
- Link repo GitHub: https://github.com/thanhpd123/Track01_Day28_3201

| STT | Họ và tên | MSSV | Vai trò chính | Báo cáo cá nhân |
|---|---|---|---|---|
| 1 | Phan Duy Thành | 2A202602930 | Trưởng nhóm; CP4 · Bảng lộ trình & lịch rà soát | [`2A202602930_Phan_Duy_Thành.md`](2A202602930_Phan_Duy_Thành.md) |
| 2 | Chử Trần Phương Nam | 2A202602675 | CP1 · Đọc hồ sơ, viết giả thuyết, chỉ số và ngưỡng | [`2A202602675_ChuTranPhuongNam.md`](2A202602675_ChuTranPhuongNam.md) |
| 3 | Phùng Gia Khánh | 2A202602585 | CP2 · Chấm điểm ưu tiên RICE-AI, quyết định Tự làm/Mua/Chờ | [`2A202602585_PhungGiaKhanh.md`](2A202602585_PhungGiaKhanh.md) |
| 4 | Bùi Hải Nam | 2A202602636 | CP3 · Mức tự động, cổng đánh giá & kinh tế | [`2A202602636_BuiHaiNam.md`](2A202602636_BuiHaiNam.md) |
| 5 | Tô Anh Đức | 2A202602639 | CP5 · Slide lãnh đạo | [`H3201_CS13_Slide.pptx`](../../H3201_CS13_Slide.pptx) |

## 2. Mục tiêu và cách tiếp cận

Mục tiêu: lập lộ trình 12 tháng cho SổSạch sao cho kế toán viên chỉ phải xem một phần nhỏ hoá đơn mà **không lọt lỗi mã số thuế hay sai tiền** — điều kiện cứng của chị Hạnh: *"Sai mã số thuế hay sai tiền thì không được lần nào."*

Căn cứ lấy từ [hồ sơ tình huống](../../docs/CS13_HoSoTinhHuong.pdf), Đề 1:

- 1 việc = 1 hoá đơn được đọc, đối chiếu và nhập vào phần mềm kế toán; văn phòng thử nghiệm ~12.000 hoá đơn/tháng (40 doanh nghiệp).
- Bản 2 đã qua cổng phát hành (97,3% ≥ 95%, 0 lỗi nghiêm trọng, kappa 0,90) → không có việc phải sửa trước, bắt đầu từ Mức 1.
- Số liệu kinh tế ở `2_Mức tự động!B12:B20`: 254 đ gọi AI + 200 đ hạ tầng/hoá đơn, người duyệt 1,5 phút × 50.000 đ/giờ, doanh thu 3,97 triệu và 1.760 hoá đơn/văn phòng/tháng.
- Chuyên gia: chị Hạnh 3 giờ/tuần; 1 vòng chấm bộ đề 40 ca = 8,5 giờ của chị Hạnh + anh Tùng.

## 3. Giải pháp

### 3.1. Danh sách giả thuyết và chỉ số (CP1 — Chử Trần Phương Nam)

- Xác lập 7 việc (6 việc gợi ý + 1 việc nhóm bổ sung), viết theo chuẩn: *"Ta tin rằng làm X cho Y sẽ giúp Z; biết đúng khi Chỉ số đạt Ngưỡng"*.
- Toàn bộ chỉ số thành công ở cột E đều có **con số định lượng, cỡ mẫu và ngưỡng chặn rõ ràng**.
- Đề xuất bổ sung **Việc 7: Kiểm tra số tiền và hoá đơn trùng**: dùng mã lệnh deterministic guardrail bắt 100% sai lệch tiền (> 0 đ) và hoá đơn trùng, đảm bảo an toàn tuyệt đối cho người dùng mà không tốn chi phí gọi AI.

### 3.2. Chấm điểm ưu tiên và Quyết định sản phẩm (CP2 — Phùng Gia Khánh)

Dựa trên đóng góp của thành viên Phùng Gia Khánh tại nhánh `2A202602585_PhungGiaKhanh`:
Nhóm áp dụng công thức ưu tiên RICE có điều chỉnh cho AI, kết hợp đa chiều thay vì chỉ chọn tính năng theo cảm tính:
- $\text{RICE} = \frac{\text{Độ phủ} \times \text{Tác động} \times \text{Mức tự tin}}{\text{Công sức}}$
- $\text{Điểm AI} = \text{RICE} \times (0,5 + 0,5 \times \text{Sẵn sàng trung bình}) \times (1 - 0,5 \times \text{Rủi ro bị nuốt})$

Kết quả xếp hạng và quyết định sản phẩm:

| Hạng | Công việc | Điểm AI | Quyết định | Căn cứ và lý do quyết định |
|---|---|---:|---|---|
| 1 | Đối chiếu mã số thuế người bán | 15,00 | **Mua** | Mức độ nghiêm trọng cao nhất (sai MST không được phép lọt); dịch vụ tra cứu đã có sẵn trên thị trường, tích hợp tiết kiệm công sức nhất. |
| 2 | Gắn cờ hoá đơn cần người xem | 7,88 | **Tự làm** | Thành phần trọng yếu quyết định hoá đơn nào cần người duyệt, ảnh hưởng trực tiếp tới tỷ lệ duyệt và chi phí vận hành (hạ từ 1.704 đ xuống 704 đ). |
| 3 | Kiểm tra số tiền và hoá đơn trùng | 6,63 | **Tự làm** | Kiểm tra bằng quy tắc/mã lệnh, chi phí triển khai cực thấp, triệt tiêu trực tiếp nguy cơ sai tiền lọt vào sổ sách. |
| 4 | Nhập tự động hoá đơn điện tử | 4,88 | **Mua** | Phần mềm kế toán đã có sẵn khả năng này (rủi ro bị nuốt = 1), ưu tiên tích hợp thay vì phát triển lại gây lãng phí. |
| 5 | Đọc ảnh hoá đơn giấy | 3,77 | **Tự làm** | Bản 2 đã đạt cổng phát hành (97,3%), nhưng phạm vi sử dụng phụ thuộc vào tỷ lệ hoá đơn giấy thực tế tại văn phòng. |
| 6 | Gợi ý tài khoản hạch toán | 1,20 | **Chờ** | Chưa có đủ dữ liệu hạch toán của từng khách hàng (sẵn sàng dữ liệu = 0,1); cần tích luỹ dữ liệu qua Mức 1 trước khi xem xét ở mốc tháng 6. |
| 7 | Trả lời câu hỏi thuế chung | 0,23 | **Không làm** | Nằm ngoài đơn vị "1 việc = 1 hoá đơn", rủi ro pháp lý cao khi tư vấn sai, dễ bị chatbot phổ thông hoặc nền tảng kế toán nuốt chửng ($L = 0,9$). |

*Nguyên tắc rút ra từ CP2:* **Điểm ưu tiên không tự động quyết định phải tự xây tính năng nào**. Một việc có điểm cao vẫn nên **Mua** nếu giải pháp bên ngoài đã hoàn thiện; ngược lại, việc kiểm soát rủi ro cốt lõi thì phải **Tự làm**.

### 3.3. Mức tự động và Cổng đánh giá (CP3 — Bùi Hải Nam)

- **Mức 0 (Gợi ý):** Duyệt 100%, chi phí 1.704 đ/hoá đơn, biên gộp 24,5% (lỗ biên).
- **Mức 1 (Hỗ trợ có duyệt):** Duyệt 20%, chi phí 704 đ/hoá đơn, biên gộp 68,8%. Cổng lên mức: $\ge 500$ hoá đơn chạy song song 2 tuần, 0 lỗi mã số thuế/tiền ngoài cờ, cờ $\le 20\%$. Lên Mức 1 ngay trong tháng 1.
- **Mức 2 (Tự động một phần):** Duyệt 10%, chi phí 579 đ/hoá đơn, biên gộp 74,3%. Cổng: $\ge 8$ tuần ở Mức 1, $\ge 3.000$ hoá đơn đã duyệt, 0 lỗi lọt, tỷ lệ đạt $\ge 98\%$, cờ thừa $\le 30\%$, $\ge 10$ văn phòng.
- **Mức 3 (Tự động có giám sát):** Duyệt 5%, chi phí ~517 đ/hoá đơn, biên gộp 77,1%. Cổng: $\ge 3$ tháng ở Mức 2, $\ge 20.000$ hoá đơn điện tử, 0 lỗi nghiêm trọng, đạt $\ge 99,5\%$ (chỉ áp dụng cho tầng Thường).

### 3.4. Bảng lộ trình và Lịch rà soát (CP4 — Phan Duy Thành)

- **Lộ trình 3 tầng:**
  - *Bây giờ (0–3 tháng):* Cam kết chạy Bản 2 ở Mức 1, làm trước Đối chiếu MST, Gắn cờ, Kiểm tra tiền.
  - *Tiếp theo (3–6 tháng):* Thu hẹp cờ để lên Mức 2; mở rộng 10–20 văn phòng; thu thập dữ liệu hạch toán.
  - *Sau này (6–12 tháng):* Lên Mức 3 cho hoá đơn điện tử tầng Thường; thử nghiệm gợi ý hạch toán ở Mức 0.
- **Lịch rà soát:** Mốc ngày 30, 60, 90 và 3 sự kiện kích hoạt (mô hình AI mới/giảm giá, đối thủ ra tính năng tương tự, thay đổi quy định pháp lý).

## 4. Kết quả

| Hạng mục | Kết quả |
|---|---|
| File Excel | [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx) |
| Tự kiểm tra (`6_Tự kiểm tra`) | 8/8 Đạt |
| Chi phí/biên gộp | Mức 1: 704 đ, 68,8% · Mức 2: 579 đ, 74,3% · Mức 3: ~517 đ, 77,1% |
| Slide lãnh đạo | [`H3201_CS13_Slide.pptx`](../../H3201_CS13_Slide.pptx) / [PDF](../../H3201_CS13_Slide.pdf), 5 ô đều ≤ 60 chữ |

## 5. Khó khăn và cách xử lý

- **Mức 0 lỗ biên (24,5%)**: Không thể duy trì lâu với duyệt 100% $\rightarrow$ đặt cổng Mức 1 khả thi trong 2 tuần ($\ge 500$ hoá đơn chạy song song) để lên Mức 1 ngay tháng 1, thay vì hạ tiêu chuẩn an toàn.
- **Điều kiện dừng phải đo được ngay**: Điều kiện doanh thu của đề cần $\ge 10$ văn phòng và 2 tháng $\rightarrow$ nhóm bổ sung điều kiện dừng cho tầng Bây giờ đo được ngay trên ~12.000 hoá đơn/tháng (1 lỗi lọt $\rightarrow$ về Mức 0; cờ > 30% trong 2 tuần $\rightarrow$ dừng sửa cờ).
- **Giờ chuyên gia hạn chế** (chị Hạnh 3 giờ/tuần): Chỉ dùng chị Hạnh kiểm mẫu 1% (~30 hoá đơn/tuần) và duyệt kết quả chấm bộ đề; chia sẻ việc chấm lại bộ đề 40 ca (8,5 giờ) cho anh Tùng.

## 6. Tổng hợp đóng góp thành viên

| STT | Họ tên | MSSV | Phần việc phụ trách | Bằng chứng đóng góp & Báo cáo |
|---|---|---|---|---|
| 1 | Phan Duy Thành | 2A202602930 | Trưởng nhóm; CP4 · Bảng lộ trình và lịch rà soát | `3_Bảng lộ trình!B5:D12`, `4_Rà soát!B5:D10`; [`2A202602930_Phan_Duy_Thành.md`](2A202602930_Phan_Duy_Thành.md) |
| 2 | Chử Trần Phương Nam | 2A202602675 | CP1 · Đọc hồ sơ, viết giả thuyết, chỉ số và ngưỡng | `0_Đầu vào!B5:E10`, `1_Danh sách việc!B5:E11`; [`2A202602675_ChuTranPhuongNam.md`](2A202602675_ChuTranPhuongNam.md) |
| 3 | Phùng Gia Khánh | 2A202602585 | CP2 · Chấm điểm ưu tiên RICE-AI, quyết định Tự làm/Mua/Chờ và lý do | `1_Danh sách việc!F5:L11`, `1_Danh sách việc!M5:N11`, `1_Danh sách việc!P5:Q11`; [`2A202602585_PhungGiaKhanh.md`](2A202602585_PhungGiaKhanh.md) |
| 4 | Bùi Hải Nam | 2A202602636 | CP3 · Mức tự động, cổng đánh giá, người duyệt và căn cứ kinh tế | `2_Mức tự động!C5:I8`; [`2A202602636_BuiHaiNam.md`](2A202602636_BuiHaiNam.md) |
| 5 | Tô Anh Đức | 2A202602639 | CP5 · Slide lãnh đạo | `5_Slide lãnh đạo!B4:B8`; [`H3201_CS13_Slide.pptx`](../../H3201_CS13_Slide.pptx) |

Cả nhóm cùng thảo luận để thống nhất các quyết định trước khi điền vào file Excel [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx).

## 7. Hạn chế và hướng cải thiện

- **Kiểm chứng tỷ lệ hoá đơn thực tế (phản biện từ CP2):** Nhóm đang giả định phần lớn hoá đơn đầu vào là hoá đơn điện tử nên việc đọc ảnh chỉ có độ phủ 3/5. Cần đo lường tỷ lệ ảnh/giấy thực tế tại văn phòng thử nghiệm ở ngày 30. Nếu tỷ lệ ảnh cao hơn, điểm ưu tiên và thứ hạng của việc đọc ảnh cần được đánh giá lại.
- Các cỡ mẫu 500 / 3.000 / 20.000 hoá đơn, mốc lên Mức 2–3 và % duyệt 5% ở Mức 3 là đề xuất nội bộ của nhóm, cần kiểm chứng qua vận hành thực tế.
- Phần tuân thủ pháp lý dẫn chiếu Luật Trí tuệ nhân tạo số 134/2025/QH15 ở mức chung; cần rà soát chi tiết văn bản hướng dẫn thi hành.
- Ngày 90 chưa đo được giá trị vòng đời khách hàng thật (mới dùng 3 tháng); sẽ đánh giá ở các mốc rà soát tiếp theo.

## 8. Tài liệu tham khảo

- [CS13_HoSoTinhHuong.pdf](../../docs/CS13_HoSoTinhHuong.pdf) — hồ sơ tình huống, Đề 1.
- [CS13_SlideLop_AIRoadmap.pdf](../../docs/CS13_SlideLop_AIRoadmap.pdf) — bài giảng CS13 (slide 74, 77–87).
- [CS13_Roadmap_De1.xlsx](../../src/CS13_Roadmap_De1.xlsx) — file đề gốc.

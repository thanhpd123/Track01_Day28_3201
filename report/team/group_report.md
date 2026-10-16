# Báo cáo nhóm H3201 — CS13 Lộ trình sản phẩm AI

## 1. Thông tin nhóm

- Tên nhóm: H3201
- Đề CS13: Đề 1 · SổSạch — trợ lý đọc hoá đơn đầu vào cho văn phòng kế toán dịch vụ
- Link repo GitHub: https://github.com/thanhpd123/Track01_Day28_3201

| STT | Họ và tên | MSSV | Vai trò chính | Báo cáo cá nhân |
|---|---|---|---|---|
| 1 | Phan Duy Thành | 2A202602930 | Trưởng nhóm; CP4 · Bảng lộ trình & lịch rà soát | [`2A202602930_Phan_Duy_Thành.md`](2A202602930_Phan_Duy_Thành.md) |
| 2 | Chử Trần Phương Nam | 2A202602675 | CP1 · Đọc hồ sơ, viết giả thuyết, chỉ số và ngưỡng | [`2A202602675_ChuTranPhuongNam.md`](2A202602675_ChuTranPhuongNam.md) |
| 3 | Phùng Gia Khánh | 2A202602585 | CP2 · Chấm điểm ưu tiên RICE-AI, tự làm/mua/chờ | Theo nhóm |
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

- **Giả thuyết & Chỉ số thành công (`1_Danh sách việc`, cột B–E):**
  - Nhóm xác lập 7 việc (6 gợi ý + 1 việc nhóm tự thêm), đều được viết theo chuẩn: *"Ta tin rằng làm X cho Y sẽ giúp Z; biết đúng khi Chỉ số đạt Ngưỡng"*.
  - Bổ sung **Việc 7: Kiểm tra số tiền và hoá đơn trùng**: dùng mã lệnh deterministic guardrail bắt 100% sai lệch tiền (> 0 đ) và hoá đơn trùng để đảm bảo cam kết an toàn cho chị Hạnh.
  - Ba việc làm trước: Việc 4 Đối chiếu mã số thuế (Mua dịch vụ, 15,00 điểm), Việc 2 Gắn cờ (Tự làm, 7,88 điểm, khống chế cờ ≤ 20%), Việc 7 Kiểm tra tiền (Tự làm, 6,63 điểm).
  - Hoãn/loại bỏ: Việc 5 Gợi ý tài khoản (**Chờ** vì chưa có dữ liệu); Việc 6 Trả lời thuế chung (**Không làm** vì ngoài phạm vi 1 việc, rủi ro pháp lý cao, nguy cơ bị AI tổng quát nuốt chửng).
- **Mức tự động (`2_Mức tự động`):**
  - Mức 0 (duyệt 100%, biên 24,5%) → Mức 1 (duyệt 20%, 704 đ/hoá đơn, biên 68,8%) ngay trong tháng 1 sau khi chạy song song ≥ 500 hoá đơn.
  - Mức 2 (duyệt 10%, biên 74,3%) khi ≥ 8 tuần ở Mức 1, ≥ 3.000 hoá đơn 0 lỗi lọt, đạt ≥ 98%, cờ thừa ≤ 30%, ≥ 10 văn phòng.
  - Mức 3 (duyệt 5%, biên 77,1%) chỉ áp dụng cho hoá đơn điện tử tầng Thường sau ≥ 20.000 hoá đơn không lỗi nghiêm trọng.
- **Lộ trình (`3_Bảng lộ trình`) và rà soát (`4_Rà soát`):** đủ 8 dòng cho cả 3 tầng Bây giờ (0–3 tháng) / Tiếp theo (3–6 tháng) / Sau này (6–12 tháng); các mốc rà soát 30/60/90 ngày và 3 sự kiện kích hoạt (mô hình/giá AI, đối thủ, thay đổi pháp lý).

## 4. Kết quả

| Hạng mục | Kết quả |
|---|---|
| File Excel | [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx) |
| Tự kiểm tra (`6_Tự kiểm tra`) | 8/8 Đạt |
| Chi phí/biên gộp | Mức 1: 704 đ, 68,8% · Mức 2: 579 đ, 74,3% · Mức 3: ~517 đ, 77,1% |
| Slide lãnh đạo | [`H3201_CS13_Slide.pptx`](../../H3201_CS13_Slide.pptx) / [PDF](../../H3201_CS13_Slide.pdf), 5 ô đều ≤ 60 chữ |

## 5. Khó khăn và cách xử lý

- **Mức 0 lỗ biên (24,5%)**: không thể ở lâu với duyệt 100% → đặt cổng Mức 1 có thể đạt trong 2 tuần (≥ 500 hoá đơn chạy song song) để lên Mức 1 ngay tháng 1, thay vì hạ yêu cầu an toàn.
- **Điều kiện dừng phải đo được ngay**: điều kiện doanh thu bình quân của đề cần ≥ 10 văn phòng và 2 tháng → nhóm thêm điều kiện dừng cho tầng Bây giờ đo được ngay trên ~12.000 hoá đơn/tháng (1 lỗi lọt → về Mức 0; cờ > 30% hai tuần → sửa cờ).
- **Giờ chuyên gia hạn chế** (chị Hạnh 3 giờ/tuần): chỉ dùng chị Hạnh cho kiểm mẫu 1% (~30 hoá đơn/tuần) và duyệt kết quả chấm bộ đề khi có mốc lớn.

## 6. Tổng hợp đóng góp thành viên

| STT | Họ tên | MSSV | Phần việc phụ trách | Bằng chứng đóng góp & Báo cáo |
|---|---|---|---|---|
| 1 | Phan Duy Thành | 2A202602930 | Trưởng nhóm; CP4 · Bảng lộ trình và lịch rà soát | `3_Bảng lộ trình!B5:D12`, `4_Rà soát!B5:D10`; [`2A202602930_Phan_Duy_Thành.md`](2A202602930_Phan_Duy_Thành.md) |
| 2 | Chử Trần Phương Nam | 2A202602675 | CP1 · Đọc hồ sơ, viết giả thuyết, chỉ số và ngưỡng | `0_Đầu vào!B5:E10`, `1_Danh sách việc!B5:E11`; [`2A202602675_ChuTranPhuongNam.md`](2A202602675_ChuTranPhuongNam.md) |
| 3 | Phùng Gia Khánh | 2A202602585 | CP2 · Chấm điểm ưu tiên RICE-AI, tự làm/mua/chờ và lý do | `1_Danh sách việc!F5:L11`, `1_Danh sách việc!P5:Q11` |
| 4 | Bùi Hải Nam | 2A202602636 | CP3 · Mức tự động, cổng đánh giá, người duyệt và căn cứ kinh tế | `2_Mức tự động!C5:I8`; [`2A202602636_BuiHaiNam.md`](2A202602636_BuiHaiNam.md) |
| 5 | Tô Anh Đức | 2A202602639 | CP5 · Slide lãnh đạo | `5_Slide lãnh đạo!B4:B8`; [`H3201_CS13_Slide.pptx`](../../H3201_CS13_Slide.pptx) |

Cả nhóm cùng thảo luận để thống nhất các quyết định trước khi điền vào file Excel [`H3201_CS13.xlsx`](../../H3201_CS13.xlsx).

## 7. Hạn chế và hướng cải thiện

- Giả định phần lớn hoá đơn đầu vào đã là hoá đơn điện tử, nên đọc ảnh chỉ phủ một phần (độ phủ 3/5) — cần kiểm tra tỷ lệ thật ở ngày 30.
- Các cỡ mẫu 500 / 3.000 / 20.000 hoá đơn, mốc lên Mức 2–3 và % duyệt 5% ở Mức 3 là đề xuất của nhóm, chưa phải kết quả đo.
- Phần tuân thủ dẫn Luật Trí tuệ nhân tạo số 134/2025/QH15 ở mức chung; nhóm chưa đối chiếu chi tiết văn bản gốc.
- Ngày 90 chưa đo được giá trị vòng đời thật (khách mới dùng 3 tháng); xem lại ở các mốc rà soát sau.

## 8. Tài liệu tham khảo

- [CS13_HoSoTinhHuong.pdf](../../docs/CS13_HoSoTinhHuong.pdf) — hồ sơ tình huống, Đề 1.
- [CS13_SlideLop_AIRoadmap.pdf](../../docs/CS13_SlideLop_AIRoadmap.pdf) — bài giảng CS13 (slide 74, 77–87).
- [CS13_Roadmap_De1.xlsx](../../src/CS13_Roadmap_De1.xlsx) — file đề gốc.

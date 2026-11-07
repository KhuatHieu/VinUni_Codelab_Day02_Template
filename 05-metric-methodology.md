# Phương Pháp Luận Định Lượng & Cơ Sở Tính Toán Chỉ Số Vận Hành

**Dự án:** Co-pilot CSKH VinClub / VPoint (AI soạn *nháp* trả lời về điểm, hạng, ưu đãi liên thông Vingroup)
**Đơn vị thực hiện:** AI Product Engineering — Vin Smart Future (Vingroup)
**Tài liệu tham chiếu:** Giải trình các con số trong `02-deep-dive-report.md` và `04-workflow-diagram.png`.

> **Cách đọc các con số trong file này.** Mỗi con số mang đúng một nhãn:
> - **[N]** — lấy từ nguồn công khai (có link ở mục 10).
> - **[GĐ]** — *giả định* của nhóm để scoping. Chưa được kiểm chứng, **không phải số liệu nội bộ Vingroup**.
> - **[ĐO]** — con số cần đo thực tế trước khi cam kết (xem kế hoạch xác minh, mục 7).
>
> Mục tiêu của file không phải là "chứng minh dự án chắc chắn lãi", mà là cho người đọc thấy **con số nào có căn cứ, con số nào chưa, và kết quả thay đổi thế nào nếu giả định sai**.

---

## 1. Tổng quan phương pháp

Dùng **ước tính Fermi**: chia bài toán thành chuỗi các đại lượng nhỏ, mỗi đại lượng có nguồn hoặc được đánh dấu là giả định, rồi nhân lại. Kèm theo:
1. **Bằng chứng định tính có thật** về việc quy tắc điểm/hạng khác nhau giữa các công ty thành viên (mục 2).
2. **Phân tích độ nhạy** cho các giả định quan trọng nhất (mục 4).
3. **Ba kịch bản lợi ích** (bảo thủ / trung bình / mục tiêu) thay vì một con số duy nhất (mục 5). Kịch bản bảo thủ dựa trên một nghiên cứu thực nghiệm đã công bố về trợ lý AI cho CSKH [7].

---

## 2. Bằng chứng thực tế: vấn đề có thật ở đâu?

| # | Sự kiện / quy định công khai | Nguồn | Hàm ý cho bài toán |
|---|------------------------------|-------|--------------------|
| 1 | VinClub ra mắt ngày **08/08/2024**; khách có giao dịch tại Vinhomes, Vinpearl, VinFast, Vinmec, Vinschool, GSM đều có thể là thành viên. Thông cáo nói chương trình thu hút **hàng triệu thành viên**. | [1][6] | Quy mô khách đủ lớn để CSKH có khối lượng đáng kể **[N]**. |
| 2 | **1 VPoint = 1.000 VNĐ**; điểm tích theo doanh thu *sau khi trừ khuyến mại/chiết khấu*; mỗi giao dịch chỉ tích vào **một** tài khoản. | [1] | Khách dễ nhầm "tại sao ít điểm hơn tôi tính" (điểm phụ thuộc giá sau ưu đãi) **[N]**. |
| 3 | Khách chi tiêu ở nhiều công ty được tính **hạng cao nhất** trên app. Hạng gồm *Thành viên → Vàng → Bạch Kim → Kim Cương*. | [3] | Hạng "liên thông" là cơ chế khó theo dõi **[N]**. |
| 4 | Theo cẩm nang của Vinpearl, khách **chưa đạt hạng Vàng** thì chưa được tích VPoint; điểm tích xong **khả dụng từ 12h ngày T+1**. | [2] | Điểm "đã tích" ≠ "đã dùng được ngay" → câu hỏi lặp lại **[N]**. |
| 5 | **Xanh SM:** phụ phí, tip, bảo hiểm… thu hộ/chi hộ **không** được tích; phụ phí phát sinh sau khi đặt cuốc **không** áp dụng tiêu VPoint. Từ 08/08/2024 khách phải đăng ký VinClub mới được tích. | [2][3] | Quy tắc riêng theo từng công ty — đúng điểm nghẽn "tra chính sách" **[N]**. |
| 6 | **Vinpearl:** đặt phòng qua đại lý được tích **đêm phòng**, không tích giá trị doanh số. | [2] | Một ví dụ khác về quy tắc khác biệt **[N]**. |
| 7 | **Vinmec:** với tạm ứng/chi trả nhập viện, điểm được tích vào **lúc Vinmec xuất bảng kê** dịch vụ. | [5] | Thời điểm cộng điểm khác nhau theo đối tác **[N]**. |
| 8 | **Vinpearl / VinWonders** thông báo *chưa thể tích VPoint tự động* cho đơn từ 08/08/2024 đến 31/01/2025, phải **tích bù** bằng voucher rồi đổi sang VPoint trên app trước 31/03/2025. | [4] | Bằng chứng mạnh nhất: chính công ty phải ra hướng dẫn riêng vì điểm không liên thông tự động **[N]**. |
| 9 | VPoint **không có hạn sử dụng**, **không đổi ra tiền mặt**, có thể **tặng** cho thành viên khác. | [1][6] | Tính năng "tặng điểm" là thao tác tài chính → AI **không được** tự làm **[N]**. |
| 10 | **Mở rộng đối tác:** ~300 cửa hàng, 30+ thương hiệu chấp nhận VPoint (12/2024); hợp tác chiến lược với 10+ đối tác khác (06/2025). | [8][9] | Mỗi đối tác mới thêm quy tắc → bề mặt chính sách tăng, vấn đề *tăng theo thời gian* **[N]**. |

**Ranh giới của bằng chứng:** các nguồn trên chứng minh *cơ chế gây nhầm lẫn là có thật*. Chúng **không** cho biết số cuộc gọi/ngày, thời gian xử lý, hay tỉ lệ khiếu nại. Các con số đó ở mục 3–5 là **[GĐ]**.

---

## 3. Phân rã thời gian xử lý (14 phút/yêu cầu; điểm nghẽn 8 phút)

Quy trình hiện tại của agent CSKH (khớp `02-deep-dive-report.md` và sơ đồ swimlane):

| Bước | Hoạt động | Công cụ | Thời gian | Nhãn |
|:---:|-----------|---------|:---:|:---:|
| 1 | Tiếp nhận yêu cầu, mở ticket | Hotline/chat/app, CRM | 1 phút | [GĐ] |
| 2 | Xác minh danh tính khách | CRM, câu hỏi bảo mật | 2 phút | [GĐ] |
| 3 | Tra số dư, hạng, lịch sử điểm | Hệ thống VinClub/VPoint | 2 phút | [GĐ] |
| 4 | **Tra chính sách từng công ty thành viên** | Tài liệu/handbook rải rác | **5 phút** 🔴 | [GĐ] |
| 5 | **Soạn phản hồi** | Soạn tay | **3 phút** 🔴 | [GĐ] |
| 6 | Gửi khách, ghi và đóng ticket | CRM | 1 phút | [GĐ] |
| | **Tổng (bước 1–6)** | | **14 phút** | |
| 7 | *(nếu tranh chấp)* chuyển đối tác đối soát | Email/phiếu nội bộ | 1–2 ngày | [GĐ] |

**Điểm nghẽn:** `Bước 4 + Bước 5 = 5 + 3 = 8 phút`
**Tỉ trọng:** `8 / 14 = 57,1% ≈ 57%`

Lý do chọn bước 4–5 làm điểm nghẽn có căn cứ định tính ở mục 2 (dòng 5–8: quy tắc khác nhau theo công ty), nhưng **số phút cụ thể phải đo** ([ĐO], mục 7).

---

## 4. Khối lượng yêu cầu & giờ công (kèm phân tích độ nhạy)

### 4.1. Chuỗi Fermi
```
Số yêu cầu / ngày = (số thành viên) × (tỉ lệ liên hệ agent mỗi tháng) / 30
Giờ công / ngày  = (số yêu cầu / ngày) × (phút / yêu cầu) / 60
```
- **Số thành viên = 5.000.000 [GĐ].** Nguồn chỉ nói "hàng triệu" [6]; 5 triệu là giả định giữa.
- **Tỉ lệ liên hệ agent = 1,8%/tháng [GĐ]** (khách hỏi về điểm/hạng/ưu đãi qua kênh có người; phần tự tra trên app không tính).
- **Kết quả cơ sở:** `5.000.000 × 1,8% / 30 = 3.000 yêu cầu/ngày`.

### 4.2. Bảng độ nhạy theo tỉ lệ liên hệ

| Tỉ lệ liên hệ/tháng | Yêu cầu/ngày | Giờ công/ngày (14') | Giờ công/ngày ở điểm nghẽn (8') | FTE tương đương* |
|:---:|:---:|:---:|:---:|:---:|
| 1,0% | ≈ 1.667 | ≈ 389 | ≈ 222 | ≈ 66 |
| **1,8% (cơ sở)** | **3.000** | **700** | **400** | **≈ 119** |
| 3,0% | 5.000 | ≈ 1.167 | ≈ 667 | ≈ 199 |

\* FTE = (giờ công/ngày × 30) / 176 giờ/tháng (8 giờ × 22 ngày).

**Cách đọc:** kết luận "đáng làm" phụ thuộc mạnh vào tỉ lệ liên hệ. Đây là con số **ưu tiên số 1 cần đo** từ dữ liệu ticket thật.

---

## 5. Mô hình lợi ích: ba kịch bản

### 5.1. Mức tiết kiệm mỗi yêu cầu
| Kịch bản | Cơ sở | Tiết kiệm/yêu cầu |
|---|---|---|
| **Bảo thủ** | Trung bình +14% năng suất trong nghiên cứu thực nghiệm trợ lý AI cho CSKH [7] | `14% × 14 = 1,96 phút` ≈ 2,0 phút |
| **Trung bình** | +34% năng suất với nhân viên mới/ít kinh nghiệm trong cùng nghiên cứu [7] | `34% × 14 = 4,76 phút` ≈ 4,8 phút |
| **Mục tiêu** | Metric đề ra: 14 → dưới 6 phút (bước 4–5 từ 8 → dưới 2 phút) | ≈ 8 phút |

> **Lưu ý trung thực:** Mục tiêu của dự án (giảm ~57%) **cao hơn nhiều** mức cải thiện trung bình đã được công bố (14%). Nghiên cứu [7] đo trên công cụ gợi ý trong cuộc chat của một nhà bán lẻ trực tuyến, không phải cùng bối cảnh, nên chỉ dùng làm **mốc tham chiếu bảo thủ**, không phải bằng chứng cho mục tiêu.

### 5.2. Giá trị quy đổi (cơ sở 3.000 yêu cầu/ngày)
Giả định **chi phí giờ công đã tính đủ = 60.000 VNĐ/giờ [GĐ]** và **chi phí vận hành AI = 1.000 VNĐ/bản nháp [GĐ, ĐO]** (⇒ `3.000 × 30 × 1.000 = 90 triệu/tháng`).

| Kịch bản | Giờ tiết kiệm/ngày | Giờ tiết kiệm/tháng | Giá trị/tháng | Trừ chi phí AI | **Lãi ròng/tháng** |
|---|:---:|:---:|:---:|:---:|:---:|
| Bảo thủ | 98 | 2.940 | 176,4 triệu | 90 triệu | **≈ 86 triệu** |
| Trung bình | 238 | 7.140 | 428,4 triệu | 90 triệu | **≈ 338 triệu** |
| Mục tiêu | 400 | 12.000 | 720 triệu | 90 triệu | **≈ 630 triệu** |

(Giờ tiết kiệm/ngày = `3.000 × phút tiết kiệm / 60`; giá trị = giờ/tháng × 60.000.)

---

## 6. Chỉ số chất lượng & cách đo

| Chỉ số | Ngưỡng | Cách đo |
|---|---|---|
| Số liệu điểm/hạng trong nháp khớp hệ thống | **100%** (0 lỗi số liệu) | Kiểm tra mẫu 200 nháp; bộ kiểm tra bằng code so các con số trong nháp với dữ liệu trả về từ API |
| Nháp được agent duyệt không sửa lớn | ≥ 70% | Đo tỉ lệ sửa của agent trên log |
| Tin gửi khách khi chưa qua duyệt | **0** | Output luôn có thẻ `[DRAFT_ONLY]`; kênh gửi đặt ở bước riêng do agent bấm |
| Thao tác điểm do AI tự thực hiện | **0** | AI không có quyền ghi; kiểm bằng test đối kháng (xem `prompt_prototype.py`) |

---

## 7. Kế hoạch xác minh các giả định (1–2 tuần, trước khi build)

1. **Log ticket ẩn danh hoá (200–500 mẫu):** phân bố loại câu hỏi, tỉ lệ liên hệ agent → thay [GĐ] của 4.1.
2. **Time study 5–8 agent (đo bấm giờ từng bước):** thay số phút ở mục 3.
3. **Đếm số nguồn chính sách agent phải mở cho mỗi ca:** xác nhận điểm nghẽn bước 4.
4. **Đo tỉ lệ ca thuộc ≤ 20 mẫu câu hỏi phổ biến:** nếu rất cao thì quay về rule/template (xem mục 8, câu 3).
5. **Báo giá chi phí AI theo token và chi phí tích hợp** → điền mục 5.3.


## 10. Tài liệu tham khảo

1. Vinpearl — *VinClub là gì?* (1 VPoint = 1.000đ; tích theo doanh thu sau khuyến mại; không đổi tiền mặt; có thể tặng; không hạn dùng): https://vinpearl.com/vi/vinclub-la-gi
2. Vinpearl — *Cẩm nang VinClub* (từ hạng Vàng mới tích VPoint; khả dụng 12h T+1; tích đêm phòng khi đặt qua đại lý; Xanh SM không tiêu cho phụ phí/tip/bảo hiểm): https://vinpearl.com/vi/vinclub/handbook
3. Xanh SM — *Đi xe Xanh SM tích điểm VinClub…* (áp dụng từ 08/08/2024; tính hạng cao nhất giữa các công ty; không tích phụ phí/tip/bảo hiểm): https://www.greensm.com/vn-vi/news/di-xe-xanh-sm-tich-diem-vinclub-va-tan-huong-dac-quyen-cua-he-sinh-thai-vingroup
4. Vinpearl/VinWonders — *Tích bù điểm VPoint khi mua vé VinWonders online từ 08/08/2024* (chưa tích tự động; tích bù qua voucher; hạn đổi 31/03/2025): https://vinpearl.com/vi/tich-bu-diem-vpoint-khi-mua-ve-vinwondes-online-tu-08-08-2024
5. Vinmec — *Nhân ba đặc quyền VinClub tại Vinmec* (tích điểm khi xuất bảng kê với chi trả/tạm ứng nhập viện): https://www.vinmec.com/vie/bai-viet/vingroup-tri-an-hoi-vien-nhan-ba-dac-quyen-vin-club-tai-he-thong-y-te-vinmec
6. Vingroup — thông cáo ra mắt VinClub, 08/08/2024 (hàng triệu thành viên; VPoint vô thời hạn): https://www.greensm.com/vn-vi/news/tcbc-vingroup-ra-mat-chuong-trinh-khach-hang-than-thiet-vinclub
7. Brynjolfsson, Li & Raymond — *Generative AI at Work*, NBER Working Paper 31161 (2023); *Quarterly Journal of Economics* 140(2), 2025. (5.179 nhân viên CSKH; +14% trung bình, +34% với người mới): https://www.nber.org/papers/w31161
8. VTC News — VinClub chấp nhận VPoint tại ~300 cửa hàng, 30+ thương hiệu (12/12/2024): https://vtcnews.vn/vinclub-hop-tac-30-thuong-hieu-thuoc-vincom-mo-rong-dac-quyen-cho-khach-hang-ar912994.html
9. VCCI — VinClub hợp tác chiến lược với 10+ đối tác (18/06/2025): https://vcci.com.vn/tin-tuc/vinclub-hop-tac-chien-luoc-voi-hon-10-doi-tac-hang-dau-mo-rong-he-sinh-thai-dac-quyen-cho-khach-hang
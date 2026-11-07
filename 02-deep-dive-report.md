# Báo Cáo Phân Tích Chuyên Sâu (Deep-Dive Report)
## Đề tài: Hệ Thống AI Phát Hiện & Trợ Lý Điều Tra Gian Lận Cuốc Xe (Xanh SM Fraud Detection & Investigation Co-Pilot)

**Đơn vị thực hiện:** Vin Smart Future — Khối Công Nghệ Tập Đoàn Vingroup  
**Đối tác vận hành:** Công ty Cổ phần Di chuyển Xanh và Thông minh GSM (Xanh SM)  
**Mục tiêu:** Tự động hóa quá trình phát hiện, khoanh vùng mạng lưới thông đồng cuốc xe ảo, tối ưu hóa thời gian thẩm định hồ sơ vi phạm của chuyên viên Trust & Safety, bảo vệ ngân sách khuyến mãi và tính toàn vẹn dữ liệu vận hành đội xe điện.

---

## 🏛️ 1. Bối cảnh Vận hành & Sự cần thiết Đầu tư

Tại **Xanh SM**, hệ thống vận hành hàng chục nghìn ô tô điện và xe máy điện trên toàn quốc. Nhằm thúc đẩy thói quen sử dụng phương tiện giao thông xanh, Vingroup đã triển khai nhiều chính sách hấp dẫn:
* Thưởng chỉ tiêu năng suất hoàn thành chuyến (chuyến/ngày, chuyến/tuần).
* Thưởng duy trì tỷ lệ chấp nhận chuyến (Acceptance Rate) và tỷ lệ hoàn thành chuyến (Completion Rate) trên 70%.
* Các chương trình ưu đãi, mã giảm giá dành cho khách hàng mới và chương trình giới thiệu người dùng (Referral - Thẻ Xanh).

Tuy nhiên, một bộ phận đối tác tài xế đã lợi dụng chính sách này thông qua các thủ đoạn tinh vi:
1. **Tạo tài khoản khách hàng ảo:** Dùng SIM rác, thiết bị giả lập Android hoặc ứng dụng nhân bản (Clone App) để liên tục tạo tài khoản ảo nhận voucher 50.000đ – 100.000đ.
2. **Cuốc xe ma (Ghost Rides) & Giả lập GPS:** Dùng ứng dụng Fake GPS để định vị xe ngay cạnh tài khoản ảo, tự tạo và nhận cuốc xe siêu ngắn (dưới 1km), sau đó bấm bắt đầu và kết thúc chuyến mà không hề đón khách thực tế.
3. **Mạng lưới thông đồng (Collusion Rings):** Các nhóm tài xế tạo nhóm chat kín, đặt chéo đơn cho nhau để "bào thưởng" chỉ tiêu ngày mà không tốn pin di chuyển thực tế.

**Hậu quả:** Ngân sách tiếp thị bị thất thoát hàng tỷ đồng; bản đồ nhiệt (Heatmap) nhu cầu xe bị nhiễu loạn khiến khách hàng thật không đón được xe; các tài xế trung thực bị mất đơn hàng công bằng.

---

## 🏗️ 2. Current-State Workflow: Quy trình Điều tra Gian lận Hiện tại

Hiện tại, phòng Kiểm soát Gian lận & An toàn Vận hành (Trust & Safety) của Xanh SM đang vận hành quy trình điều tra thủ công theo 5 bước:

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│ Bước 1:         │       │ Bước 2:         │       │ Bước 3:         │
│ Hệ thống Rules  │ ───>  │ Tra cứu Log     │ ───>  │ Đối soát đa     │
│ báo cờ đỏ       │       │ Telemetry & GPS │       │ nguồn dữ liệu   │
│                 │       │                 │       │                 │
│ ⏱ 1 phút        │       │ ⏱ 10 phút 🔴    │       │ ⏱ 15 phút 🔴    │
│ Ai: Hệ thống    │       │ Ai: Chuyên viên │       │ Ai: Chuyên viên │
│ In: Dữ liệu đơn │       │ In: Mã tài xế   │       │ In: Logs nhiều  │
│ Out: Flagged ID │       │ Out: Bản đồ GPS │       │ Out: Bằng chứng │
└─────────────────┘       └─────────────────┘       └─────────────────┘
                                                           │
                                                           ▼ 🔄 Handoff
┌─────────────────┐                                 ┌─────────────────┐
│ Bước 5:         │                                 │ Bước 4:         │
│ Thực thi & Lưu  │ <────────────────────────────── │ Viết Báo cáo &  │
│ hồ sơ chế tài   │                                 │ Xin Phê duyệt   │
│                 │                                 │                 │
│ ⏱ 1 phút        │                                 │ ⏱ 5 phút        │
│ Ai: Quản trị    │                                 │ Ai: Lead duyệt  │
│ In: Quyết định  │                                 │ In: Tờ trình    │
│ Out: Khóa/Phạt  │                                 │ Out: Phê duyệt  │
└─────────────────┘                                 └─────────────────┘

Ký hiệu:
🔴 Bottleneck (Điểm nghẽn thời gian và sai sót cao nhất)
🔄 Handoff (Điểm chuyển giao giữa các bộ phận hoặc công cụ)
⏱ Tổng thời gian xử lý trung bình: 32 phút / trường hợp.
```

### Phân tích chi tiết các bước và điểm nghẽn:
* **Bước 1 (Gắn cờ sơ bộ - 1 min):** Rule-based engine quét các điều kiện tĩnh cơ bản: Tỷ lệ hoàn thành > 95% nhưng độ dài cuốc xe trung bình < 1.5km; hoặc nhiều cuốc xe từ cùng 1 địa chỉ IP mạng.
* **Bước 2 (Tra cứu Telemetry & GPS - 10 min - 🔴 Bottleneck):** Chuyên viên phải mở dashboard xe điện, tra cứu tọa độ GPS từng giây của cuốc xe, vận tốc trung bình, độ dịch chuyển pin SoC (State of Charge) trên xe VinFast để xem xe có lăn bánh thật hay không.
* **Bước 3 (Đối soát đa nguồn - 15 min - 🔴 Bottleneck):** Chuyên viên phải tải log thiết bị của khách hàng và tài xế (Device Fingerprint, IMEI, danh sách thẻ ngân hàng liên kết, mã voucher đã dùng) đối chiếu thủ công trên bảng tính. Nếu nhóm gian lận dùng thiết bị khác nhau nhưng có chung mạng lưới nạp tiền/chuyển tiền, mắt thường rất khó phát hiện.
* **Bước 4 (Soạn báo cáo & Xin duyệt - 5 min - 🔄 Handoff):** Chuyên viên sao chép thông tin vào biểu mẫu vi phạm nội bộ, viết lý giải hành vi và gửi email xin ý kiến phê duyệt từ Trưởng bộ phận Trust & Safety.
* **Bước 5 (Thực thi chế tài - 1 min):** Tác động hệ thống: khóa tạm thời/vĩnh viễn tài khoản hoặc khấu trừ tiền thưởng gian lận trong kỳ thanh toán.

---

## 🎯 3. Problem Statement (6-Field) — Vin Smart Future Standard

| Trường thông tin | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | **Chuyên viên Kiểm soát Gian lận (Trust & Safety / Fraud Analyst)** trực thuộc Trung tâm Vận hành Xanh SM, phối hợp cùng các Kỹ sư AI tại Vin Smart Future. |
| **2. Current Workflow** | Điều tra bán thủ công qua 5 bước: Nhận cờ cảnh báo từ rule-based tĩnh ➔ Tra cứu thủ công log GPS/Telemetry xe điện VinFast ➔ Đối soát chéo thông tin tài khoản khách hàng, thiết bị và voucher trên nhiều màn hình ➔ Soạn tờ trình đề xuất chế tài ➔ Trưởng phòng phê duyệt và khóa tài khoản/khấu trừ tiền. |
| **3. Bottleneck** | **Bước 2 & Bước 3 (chiếm 25/32 phút mỗi vụ việc):** Chuyên viên bị quá tải vì phải truy vấn dữ liệu phân tán trên 4 cơ sở dữ liệu khác nhau. Hệ thống luật tĩnh sinh ra tỷ lệ cảnh báo sai (False Positive) lên tới 18%, khiến nhiều tài xế chạy thật bị gắn cờ oan, trong khi các mạng lưới thông đồng dùng công nghệ cao thì bị bỏ lọt. |
| **4. Business Impact** | - Mỗi tháng trung tâm ghi nhận hơn **3.500 lượt gắn cờ nghi vấn**, gây tồn đọng hồ sơ và lãng phí hơn **1.800 giờ công làm việc**.<br>- Thiệt hại tài chính trực tiếp ước tính **~1.2 tỷ VNĐ/quý** do thất thoát ngân sách voucher khuyến mãi và tiền thưởng năng suất trả sai đối tượng.<br>- Tài xế chạy thật bị gắn cờ oan bức xúc khiếu nại, ảnh hưởng đến thương hiệu dịch vụ chuẩn 5 sao của Xanh SM. |
| **5. Success Metric (Có con số cụ thể)** | 1. **Thời gian xử lý hồ sơ (Efficiency):** Giảm thời gian điều tra trung bình từ **32 phút ➔ dưới 3 phút/trường hợp** (giảm > 90%).<br>2. **Độ chính xác (Quality):** Giảm tỷ lệ gắn cờ sai (False Positive Rate) từ **18% ➔ dưới 2%**.<br>3. **Độ bao phủ phát hiện (Coverage):** Nâng tỷ lệ phát hiện các mạng lưới thông đồng (Collusion Rings) lên **≥ 92%**.<br>4. **Hiệu quả tài chính (Financial Impact):** Thu hồi và ngăn chặn thất thoát tối thiểu **850 triệu VNĐ tiền thưởng/voucher mỗi tháng**. |
| **6. Operational Boundary (Ranh giới an toàn)** | **QUYỀN HẠN CỦA AI:**<br>- Được phép: Tự động truy xuất và tổng hợp log Telemetry (GPS, pin, tốc độ), biểu đồ thiết bị và đồ thị giao dịch.<br>- Được phép: Tính toán Chỉ số Rủi ro Gian lận (Fraud Risk Score: 0 – 100) và tự động tạo Bản tóm tắt điều tra dạng nháp mang thẻ bắt buộc `[DRAFT_ONLY]`.<br><br>**RANH GIỚI CẤM (STRICT SAFETY BOUNDARIES):**<br>- 🚫 **TUYỆT ĐỐI CẤM:** AI không được tự động áp dụng chế tài khoá vĩnh viễn tài khoản hoặc khấu trừ tiền thưởng tài xế mà chưa có sự xác nhận của chuyên viên con người (Bắt buộc Human-in-the-loop).<br>- 🚫 **TUYỆT ĐỐI CẤM:** Khi điểm rủi ro chưa vượt ngưỡng chắc chắn (Fraud Risk Score < 80), không được đề xuất chế tài nặng; bắt buộc chuyển sang chế độ giám sát ngầm hoặc yêu cầu xác thực khuôn mặt (Face Auth) ngẫu nhiên giữa chuyến. |

---

## 🤖 4. AI Fit & Future-State Flow

### 4.1. Phân tích AI-Fit Matrix: Tại sao là Kiến trúc Lai (Hybrid ML/Graph + LLM)?

| Phương án công nghệ | Ưu điểm | Nhược điểm / Rủi ro | Đánh giá lựa chọn |
|---|---|---|---|
| **Phương án 1: Pure Rule-Based Engine** | Đơn giản, độ trễ thấp (vài mili-giây), dễ triển khai. | Dễ bị tài xế gian lận "bắt bài" và lách luật; không thể phát hiện các mạng lưới thông đồng phức tạp; tỷ lệ gắn cờ oan rất cao (18%). | ❌ **Loại bỏ** (Hệ thống hiện tại đang thất bại). |
| **Phương án 2: Fully Autonomous AI Agent** | Tự động hóa 100%, không cần con người can thiệp. | Rủi ro pháp lý và tranh chấp lao động cực kỳ cao nếu AI ảo giác hoặc kết luận sai; nguy cơ tài xế đình công vì bị khóa oan. | ❌ **Loại bỏ** (Vi phạm nguyên tắc an toàn vận hành). |
| **Phương án 3: Hybrid Architecture (Graph Anomaly Detection + LLM Co-Pilot)** | **Graph ML** giải quyết bài toán phát hiện chuỗi thông đồng và chấm điểm rủi ro chính xác; **LLM** giải quyết bài toán đọc hiểu ngữ cảnh, phân tích nhật ký di chuyển và tự động soạn thảo hồ sơ điều tra mạch lạc cho con người phê duyệt. | Cần thiết kế pipeline dữ liệu thời gian thực và prompt ranh giới nghiêm ngặt. | ✅ **LỰA CHỌN (Tối ưu nhất)**. |

---

### 4.2. Quy trình Tương lai Tích hợp AI (Future-State Flow)

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       LUỒNG VẬN HÀNH TƯƠNG LAI CÓ AI                         │
└─────────────────────────────────────────────────────────────────────────────┘

    [Dữ liệu Cuốc xe: GPS xe VinFast, Pin SoC, Thông tin Khách & Voucher]
                                     │
                                     ▼
        ┌─────────────────────────────────────────────────────────┐
        │ 🔵 AI Step 1: Real-time Graph & Telemetry Anomaly Engine│
        │ - Thuật toán đồ thị phát hiện vòng tròn thông đồng      │
        │ - So khớp độ tiêu hao pin xe với quãng đường di chuyển  │
        │ - Tính toán: Fraud Risk Score (0 - 100)                 │
        └─────────────────────────────────────────────────────────┘
                                     │
                    ┌────────────────┴────────────────┐
                    │                                 │
           [Score < 80: Rủi ro thấp]       [Score ≥ 80: Đáng ngờ cao]
                    │                                 │
                    ▼                                 ▼
        ┌───────────────────────┐         ┌─────────────────────────────────┐
        │ Đưa vào danh sách     │         │ 🔵 AI Step 2: LLM Case Draft    │
        │ giám sát ngầm / OTP   │         │ - Tổng hợp toàn bộ chứng cứ     │
        │ (Không làm phiền xế)  │         │ - Tự động tạo hồ sơ điều tra    │
        └───────────────────────┘         │   bắt đầu bằng [DRAFT_ONLY]     │
                                          └─────────────────────────────────┘
                                                           │
                                                           ▼
                                          ┌─────────────────────────────────┐
                                          │ 🟢 Human Step (HITL Approval):  │
                                          │ Chuyên viên Trust & Safety xem  │
                                          │ bản tóm tắt bằng chứng 1-trang  │
                                          │ và click: [Duyệt Phạt] / [Bỏ qua│
                                          └─────────────────────────────────┘
                                                           │
                                        ┌──────────────────┴──────────────────┐
                                        │                                     │
                                  [Nhấn Duyệt]                          [Bất thường]
                                        │                                     │
                                        ▼                                     ▼
                          ┌───────────────────────────┐         ┌───────────────────────────┐
                          │ Hệ thống tự động khóa /   │         │ ↩️ Fallback Step:          │
                          │ khấu trừ thưởng minh bạch │         │ Chuyên viên mở log gốc    │
                          └───────────────────────────┘         │ kiểm tra thủ công chuyên  │
                                                                │ sâu (Manual Deep Review)  │
                                                                └───────────────────────────┘
```

### Các thành phần chính trong Future Flow:
1. 🔵 **AI Step 1 (Graph & Telemetry Scoring):** Mô hình hóa dữ liệu thành đồ thị liên kết hai phía (Bipartite Graph: Khách hàng - Tài xế - Mã thiết bị). Nếu phát hiện cụm thiết bị ảo hoặc quãng đường GPS tăng vọt nhưng mức tiêu thụ pin của xe VinFast bằng 0 (chứng tỏ dùng Mock GPS chứ xe không chạy), hệ thống chấm điểm rủi ro.
2. 🔵 **AI Step 2 (LLM Case Summarizer):** Với các vụ việc có điểm rủi ro ≥ 80, mô hình Gemini 2.5 Flash tổng hợp toàn bộ các dữ liệu phân tán thành một hồ sơ điều tra súc tích dài 1 trang, chỉ rõ: *Hành vi nghi vấn, Bằng chứng định vị, Bằng chứng pin xe, Thiệt hại ngân sách ước tính*. Bắt buộc gắn tiền tố `[DRAFT_ONLY]`.
3. 🟢 **Human Step (HITL Review):** Chuyên viên chỉ mất **30 - 45 giây** để đọc bản tóm tắt đầy đủ chứng cứ trực quan thay vì 25 phút bơi trong log. Chuyên viên ra quyết định bằng một nút bấm.
4. ↩️ **Fallback Plan (Cơ chế Dự phòng):**
   * Nếu LLM gặp sự cố API hoặc trả về kết quả không tự tin: Hệ thống tự động chuyển hồ sơ về hàng đợi điều tra thủ công như quy trình cũ.
   * Nếu tài xế có khiếu nại sau quyết định: Toàn bộ log raw và giải trình của AI được lưu vết (Audit Trail) để Hội đồng Phân xử nội bộ mở phiên phúc tra độc lập.

---

## 🏁 5. Phase 5 — Đánh Giá & Quyết Định Đầu Tư (EVALUATE)

### 5.1. Bảng Kiểm Tra Độ Sẵn Sàng Triển Khai (AI Readiness Checklist)

| Tiêu chí đánh giá | Trạng thái | Đánh giá thực tế tại Vin Smart Future & Xanh SM |
|---|:---:|---|
| **1. Dữ liệu mẫu & Logs sạch (Data Availability)** | ✅ **SẴN SÀNG** | Hệ thống IoT trên các dòng xe điện VinFast (VF e34, VF 5, VF 8) và App Xanh SM ghi nhận log telemetry định vị GPS, mức tiêu thụ pin từng giây, mã định danh thiết bị và giao dịch ví điện tử vô cùng đầy đủ và chính xác. |
| **2. Kiểm soát rủi ro an toàn (Risk Control)** | ✅ **SẴN SÀNG** | Quy trình thiết kế chặt chẽ với cơ chế **Human-in-the-loop 100%**: AI chỉ soạn thảo báo cáo đề xuất (`[DRAFT_ONLY]`), con người chịu trách nhiệm phê duyệt quyết định kỷ luật, loại bỏ triệt để rủi ro pháp lý/lao động. |
| **3. Mức độ sẵn sàng của Stakeholders (Adoption)** | ✅ **SẴN SÀNG** | Ban Lãnh đạo Khối Vận hành Xanh SM và Đội ngũ Trust & Safety đang chịu áp lực rất lớn từ thất thoát ngân sách tiếp thị và quá tải hồ sơ, rất mong muốn có công cụ tự động hóa hỗ trợ. |

---

### 5.2. Quyết Định Cuối Cùng của Ban Giám Đốc Vin Smart Future

> ### 🟢 **QUYẾT ĐỊNH: GO (BẮT ĐẦU TRIỂN KHAI XÂY DỰNG NGUYÊN MẪU)**

### 5.3. Lý Giải Quyết Định Đầu Tư (Justification & ROI Analysis)

Quyết định **GO** được đưa ra dựa trên 3 căn cứ xác đáng về kỹ thuật, vận hành và hiệu quả tài chính:

1. **Hiệu quả Đầu tư vượt trội (ROI rõ rệt):**
   * *Chi phí phát triển dự kiến:* Xây dựng prototype và tích hợp mô hình Gemini 2.5 Flash tốn khoảng **150 triệu VNĐ** chi phí hạ tầng và API.
   * *Lợi ích kinh tế thu về:* Ngăn chặn thất thoát ngân sách khuyến mãi ước tính **~1.2 tỷ VNĐ/quý** (~400 triệu VNĐ/tháng), đồng thời tiết kiệm **1.800 giờ công lao động/tháng** của đội ngũ chuyên viên. Dự án đạt điểm hòa vốn chỉ sau **chưa đầy 1 tháng vận hành chính thức**.
2. **Khả thi về mặt Kỹ thuật (Technical Feasibility):**
   * Bài toán không đòi hỏi các mô hình AI tự trị mạo hiểm. Việc kết hợp giữa thuật toán phát hiện bất thường trên đồ thị dữ liệu sẵn có và LLM tóm tắt báo cáo là kiến trúc đã được chứng minh hiệu quả cao trong ngành gọi xe công nghệ toàn cầu.
3. **Bảo vệ Tính Bền vững của Thương hiệu Xanh SM:**
   * Việc loại bỏ triệt để các cuốc xe ảo giúp khôi phục bản đồ nhiệt nhu cầu xe chính xác, đảm bảo tài xế chân chính đón được khách thật, nâng cao chất lượng dịch vụ di chuyển văn minh - cốt lõi thương hiệu mà Vingroup hướng đến.

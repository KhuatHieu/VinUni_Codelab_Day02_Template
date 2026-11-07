# Phase 1 & 2: Problem Scan & Quick Assessments
**Đơn vị:** Vin Smart Future (Tập đoàn Vingroup)  
**Tác giả:** AI Product Engineering Team  
**Mục tiêu:** Quét các điểm nghẽn vận hành (Bottlenecks) trong hệ sinh thái Vingroup và lựa chọn bài toán tối ưu hóa bằng Trí tuệ Nhân tạo.

---

## 🔍 Phase 1 — SCAN: Quét cơ hội vận hành trong Hệ sinh thái Vingroup

Áp dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ Stakeholders) trên các công ty thành viên: **Xanh SM, VinFast, V-GREEN, Vinhomes, Vinmec, Vinpearl**.

| # | Công ty thành viên | Lens áp dụng | Tên bài toán / Bottleneck | Mô tả chi tiết vấn đề vận hành |
|---|-------------------|--------------|---------------------------|--------------------------------|
| **1** | **Xanh SM (GSM)** | **Pain từ Stakeholders** | **Gian lận cuốc xe ảo & Bào ngân sách khuyến mãi** | Tài xế dùng SIM rác, thiết bị giả lập (emulator) và ứng dụng Mock GPS tạo tài khoản khách hàng ảo, tự đặt các chuyến xe ngắn hoặc thông đồng theo nhóm để cày cuốc, bào tiền thưởng chỉ tiêu (KPI) và chiếm đoạt tiền khuyến mãi từ chương trình giới thiệu người dùng mới (Referral). Gây thất thoát ngân sách hàng tỷ đồng và làm lệch lạc dữ liệu điều vận. |
| **2** | **VinFast** | **Tốn thời gian** | **Chẩn đoán sơ bộ mã lỗi xe điện từ mô tả tiếng Việt của khách hàng** | Khách hàng liên hệ tổng đài hoặc đại lý mô tả hiện tượng xe (ví dụ: *"vào cua bánh trước kêu lục cục"*, *"sạc trụ DC nhảy ngắt liên tục"*). Nhân viên kỹ thuật dịch vụ phải mất 15-20 phút tra cứu sổ tay kỹ thuật (Manual) và lịch sử lỗi OBD-II để phân loại mã lỗi ban đầu. |
| **3** | **V-GREEN** | **Lặp lại** | **Đối soát dữ liệu điện năng tiêu thụ và dòng tiền trạm sạc đối tác** | V-GREEN hợp tác với các chủ bãi đỗ xe/khách sạn mở trạm sạc nhượng quyền. Hằng tuần nhân viên kế toán phải đối soát thủ công hàng chục nghìn phiên sạc (kWh, thời gian sạc, đơn giá giờ cao điểm/thấp điểm) giữa telemetry trụ sạc và hóa đơn thanh toán điện lực EVN. |
| **4** | **Vinhomes** | **AI-upgrade** | **Phân loại và điều hướng phản ánh sự cố cư dân đa kênh** | Cư dân gửi phản ánh qua ứng dụng Vinhomes Resident (hỏng bóng đèn hành lang, rò rỉ nước, tiếng ồn thi công, thẻ cư dân). Đội ngũ chăm sóc khách hàng (CSKH) phải đọc, phân loại thủ công sang các ban quản trị tòa nhà tương ứng, phản hồi rập khuôn và mất 8-12 tiếng xử lý. |
| **5** | **Vinmec** | **Tốn thời gian** | **Trích xuất và soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary)** | Bác sĩ điều trị mất 20-30 phút/bệnh nhân để tổng hợp các kết quả xét nghiệm, chẩn đoán hình ảnh, phác đồ điều trị từ hệ thống Bệnh án điện tử (EMR) thành văn bản tóm tắt xuất viện bằng ngôn ngữ phổ thông cho bệnh nhân. |
| **6** | **Vinpearl** | **Lặp lại** | **Xử lý yêu cầu đặt phòng đoàn (MICE/Group Booking) từ email** | Nhân viên kinh doanh phải đọc các email đặt phòng phức tạp từ đối tác lữ hành (nhiều hạng phòng, lịch trình vui chơi VinWonders, thực đơn ăn uống), sau đó gõ tay kiểm tra quỹ phòng trống trên Opera PMS mất 30-40 phút/đơn. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn lọc Top 3 bài toán tiềm năng nhất để phân tích sơ bộ:

---

### 🎴 QUICK PROBLEM CARD #1: Gian lận cuốc xe ảo & Trục lợi chính sách thưởng tại Xanh SM

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán (1 câu): Tài xế Xanh SM tạo tài khoản ảo và thông đồng cuốc xe ma   │
│ để cày chỉ tiêu thưởng ngày/tuần và trục lợi ngân sách khuyến mại.          │
│ Công ty thành viên: [x] Xanh SM (GSM)    [ ] VinFast     [ ] V-GREEN        │
│                     [ ] Vinhomes         [ ] Vinmec      [ ] Vinpearl       │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Chuyên viên phòng Kiểm soát Gian lận & Vận hành (Trust & Safety / Fraud)  │
│ - Ban Giám đốc Khối Vận hành GSM (thất thoát ngân sách, méo mó dữ liệu)     │
│ - Khách hàng thực tế (khó gọi xe vào giờ cao điểm do tài xế bận cuốc ma)    │
│                                                                             │
│ Workflow thủ công hiện tại (5 bước):                                        │
│   1. Hệ thống rule-based gắn cờ các tài khoản tài xế có tỷ lệ hoàn thành cao │
│      bất thường hoặc cuốc xe ngắn liên tục.                                 │
│   2. Chuyên viên Fraud mở nhiều màn hình dashboard: tra cứu log GPS, thời   │
│      gian di chuyển, thông tin tài khoản đặt xe, mã khuyến mãi áp dụng.      │
│   3. So khớp thủ công địa chỉ MAC/IMEI thiết bị, dải IP và số điện thoại.   │
│   4. Viết biên bản tổng hợp hành vi vi phạm và xin phê duyệt xử lý.         │
│   5. Ban hành quyết định khóa tài khoản hoặc trừ tiền thưởng của tài xế.     │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 25-30 phút/trường hợp).      │
│ Tỷ lệ gắn cờ nhầm (False Positive) cao khiến tài xế chạy thật bị ảnh hưởng. │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 và 4:                        │
│ - Graph AI phát hiện vòng tròn thông đồng (Collusion Network).              │
│ - LLM tự động tổng hợp bằng chứng từ telemetry và draft biên bản điều tra. │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ - Giảm thời gian rà soát hồ sơ từ 25 phút ──> dưới 3 phút/trường hợp.       │
│ - Giảm tỷ lệ gắn cờ oan (False Positive Rate) từ 18% ──> dưới 2%.           │
│ - Ngăn chặn thất thoát ngân sách khuyến mại ~1.2 tỷ VNĐ/quý.                │
│                                                                             │
│ Quick Architecture: [ ] No AI   [ ] Rule   [ ] LLM   [x] ML/Graph + LLM Co-pilot │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 🎴 QUICK PROBLEM CARD #2: Đối soát dữ liệu điện năng và doanh thu trạm sạc V-GREEN

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán (1 câu): Đối soát thủ công hàng chục nghìn phiên sạc giữa telemetry │
│ trụ sạc V-GREEN và hóa đơn điện năng từ đối tác/EVN tốn nhiều công sức.     │
│ Công ty thành viên: [ ] Xanh SM          [ ] VinFast     [x] V-GREEN        │
│                     [ ] Vinhomes         [ ] Vinmec      [ ] Vinpearl       │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Chuyên viên Kế toán Vận hành & QL Đối tác Trạm sạc V-GREEN.               │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Xuất file log phiên sạc từ Cloud IoT của các trụ sạc V-GREEN.          │
│   2. Nhận hóa đơn điện năng/biên bản tiêu thụ từ đối tác mặt bằng và EVN.   │
│   3. Dùng Excel VLOOKUP để đối chiếu chênh lệch kWh và tiền điện.           │
│   4. Gửi email giải trình các trường hợp sai lệch số liệu trên 5%.           │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 3 ngày công mỗi kỳ đối soát).   │
│ Dễ sót lỗi do định dạng dữ liệu không đồng nhất giữa các đối tác.           │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 & 4 (Phát hiện điểm bất thường  │
│ bất đối xứng điện năng và tự động trích xuất bảng biểu).                    │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ - Giảm thời gian đối soát kỳ thanh toán từ 3 ngày ──> dưới 2 giờ.           │
│ - Tỷ lệ khớp chính xác số liệu đạt 99.9%.                                    │
│                                                                             │
│ Quick Architecture: [ ] No AI   [x] Rule / Data Pipeline   [ ] LLM  [ ] Agent│
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 🎴 QUICK PROBLEM CARD #3: Phân loại và điều hướng phản ánh cư dân Vinhomes Resident

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán (1 câu): Phân loại thủ công phản ánh cư dân trên ứng dụng Vinhomes  │
│ Resident gây chậm trễ thời gian phản hồi và xử lý sự cố tại các khu đô thị.  │
│ Công ty thành viên: [ ] Xanh SM          [ ] VinFast     [ ] V-GREEN        │
│                     [x] Vinhomes         [ ] Vinmec      [ ] Vinpearl       │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Nhân viên Điều phối CSKH Vinhomes và Cư dân tại các khu đô thị (Ocean Park,│
│   Smart City, Grand Park).                                                  │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Cư dân gửi phản ánh kèm hình ảnh/văn bản mô tả lên app.                │
│   2. Điều phối viên trung tâm đọc nội dung và xác định danh mục sự cố.       │
│   3. Gán thủ công công việc (Task) cho Đội Kỹ thuật/Môi trường tòa nhà.      │
│   4. Soạn tin nhắn phản hồi báo đã tiếp nhận cho cư dân.                    │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 10-15 phút/vé).              │
│ Vào giờ cao điểm tiếp nhận hàng nghìn phản ánh gây quá tải.                 │
│                                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 4 (Phân loại ý định bằng LLM  │
│ và tự động draft câu trả lời tiếp nhận cá nhân hóa).                         │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ - Giảm thời gian phản hồi ban đầu từ 4 tiếng ──> dưới 1 phút.               │
│ - Tỷ lệ định tuyến đúng phòng ban đạt trên 95%.                              │
│                                                                             │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agent      │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định Lựa chọn Bài toán Deep-Dive của Nhóm

Nhóm quyết định thống nhất chọn **Quick Problem Card #1: Hệ thống Phát hiện & Điều tra Gian lận Cuốc xe ảo tại Xanh SM (GSM)** làm đề tài phân tích sâu (Deep-Dive).

### Lý do lựa chọn và loại trừ:
1. **Lý do chọn Card #1 (Xanh SM Fraud Investigation Co-Pilot):**
   * **Tính cấp thiết và thiệt hại thực tế:** Vấn nạn cuốc xe ảo và bào ngân sách khuyến mại đang trực tiếp gây thất thoát hàng tỷ đồng ngân sách của Vingroup, đồng thời làm méo mó bản đồ nhiệt (Heatmap) nhu cầu xe điện, khiến hệ thống điều phối xe thực tế đến khách hàng chân chính bị tắc nghẽn.
   * **Độ phức tạp công nghệ phù hợp:** Bài toán đòi hỏi sự kết hợp hài hòa giữa **Thuật toán đồ thị (Graph / Anomaly Detection)** để phân tích mạng lưới và **LLM Feature** đóng vai trò Co-pilot tổng hợp chứng cứ hỗ trợ con người ra quyết định.
   * **Ranh giới an toàn (Operational Boundary) rõ ràng:** Việc xử phạt hoặc khóa tài khoản tài xế ảnh hưởng trực tiếp đến sinh kế của người lao động, đòi hỏi quy trình **Human-in-the-loop (HITL)** nghiêm ngặt.
2. **Lý do loại trừ các thẻ còn lại:**
   * **Card #2 (V-GREEN Đối soát):** Thực chất đây là bài toán xử lý dữ liệu có cấu trúc (Structured Data Pipeline) và Rule-based Reconciliation, việc áp dụng AI/LLM ở đây là quá đà ("dùng dao mổ trâu giết gà") và không tối ưu chi phí.
   * **Card #3 (Vinhomes CSKH):** Mặc dù phù hợp với LLM nhưng mang tính chất hỗ trợ nội dung thông thường, giá trị kinh tế trực tiếp và tính thách thức kỹ thuật về an toàn vận hành không cao bằng bài toán chống gian lận tài chính tại Xanh SM.

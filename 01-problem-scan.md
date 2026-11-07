# 01 — Problem Scan & Quick Cards (Vin Smart Future)

## 🔍 Phase 1 — SCAN (4 Lenses)

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|-----------|------|---------------------|
| 1 | **VPoint (liên thông)** | Pain từ người khác | Khách không biết mình đang có bao nhiêu điểm, điểm nào sắp hết hạn, còn thiếu bao nhiêu để lên hạng. Thông tin nằm rải rác ở app và các điểm chạm của từng công ty thành viên. |
| 2 | **Vinpearl** | AI có thể tốt hơn | Khi đặt phòng/vé, khách không được gợi ý ưu đãi theo hạng hoặc việc dùng điểm VPoint. Chatbot hiện chỉ trả lời rập khuôn, khách bỏ lỡ ưu đãi mà không hề biết. |
| 3 | **Xanh SM** | Pain từ người khác | Khách thanh toán chuyến đi bằng điểm hoặc ưu đãi bị nhầm lẫn: điểm không được cộng hoặc không được trừ như kỳ vọng. Khách gọi CSKH để khiếu nại. |
| 4 | **VinFast** | Lặp lại | Nhân viên CSKH/đại lý lặp đi lặp lại cùng một nhóm câu hỏi: "dùng VPoint cho dịch vụ/phụ kiện thế nào, tối đa bao nhiêu?". Mỗi lần phải tra chính sách riêng của từng nhóm sản phẩm. |
| 5 | **Vinmec** | Tốn thời gian | Lễ tân/thu ngân phải giải thích quy đổi điểm và quyền lợi theo hạng ngay tại quầy thanh toán, khiến hàng chờ dài. |
| 6 | **Vinschool** | Lặp lại | Phụ huynh liên tục hỏi khoản nào được áp dụng điểm/ưu đãi thành viên, khoản nào không. Bộ phận hỗ trợ trả lời thủ công từng trường hợp. |
| 7 | **Vinhomes** | Tốn thời gian | Cư dân phản ánh điểm/hạng không đồng bộ giữa các dịch vụ. Cần đối soát thủ công giữa các hệ thống, mất vài ngày. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

### Card #1 — Co-pilot CSKH VPoint (soạn nháp trả lời có dẫn chứng)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Agent CSKH VPoint phải tra điểm, hạng, và chính   │
│ sách của nhiều công ty thành viên rồi tự soạn câu trả lời.  │
│ Công ty thành viên: [x] Khác: VPoint (liên thông toàn hệ    │
│   sinh thái: VinFast, Vinmec, Vinpearl, Xanh SM, Vinschool) │
│                                                             │
│ Ai đang đau? Khách hàng (chờ lâu, nhận câu trả lời không    │
│ nhất quán), Agent CSKH (tra nhiều hệ thống, dễ sai)         │
│                                                             │
│ Workflow thủ công hiện tại (6 bước):                        │
│  1. Nhận yêu cầu ──> 2. Xác minh khách ──> 3. Tra tài khoản │
│  VPoint ──> 4. Tra chính sách từng đối tác ──> 5. Soạn      │
│  phản hồi ──> 6. Gửi + ghi ticket                           │
│                                                             │
│ Bước tốn nhất/lỗi nhất? Bước 4 và 5 ( ~8 phút/lượt)       │
│ AI nhảy vào ở bước nào? Bước 4-5 (truy xuất chính sách +    │
│ soạn NHÁP phản hồi dựa trên dữ liệu tài khoản có sẵn)       │
│                                                             │
│ Metric: Giảm thời gian xử lý trung bình 12 ──> dưới 5 phút; │
│ 0 lần nháp chứa số điểm sai khi qua kiểm tra mẫu.           │
│                                                             │
│ Quick Architecture: [ ] No AI [x] Rule(+API) [x] LLM [ ] Agent│
│ (Rule/API tính số điểm; LLM chỉ soạn lời và diễn giải)      │
└─────────────────────────────────────────────────────────────┘
```

### Card #2 — Gợi ý ưu đãi đúng hạng trước khi thanh toán (Vinpearl / Xanh SM)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Trước khi thanh toán, khách không được báo ưu đãi │
│ theo hạng và điểm có thể dùng nên bỏ lỡ quyền lợi.          │
│ Công ty thành viên: [x] Xanh SM  [x] Khác: Vinpearl         │
│                                                             │
│ Ai đang đau? Khách hàng (bỏ lỡ ưu đãi), đối tác (giảm       │
│ tỉ lệ dùng điểm, giảm gắn kết)                              │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│  1. Khách chọn dịch vụ ──> 2. Thanh toán ──> 3. Phát hiện   │
│  thiếu ưu đãi sau khi trả tiền ──> 4. Gọi CSKH khiếu nại    │
│                                                             │
│ Bước tốn nhất/lỗi nhất? Bước 3-4 (vài ngày hoàn điểm)    │
│ AI nhảy vào ở bước nào? Giữa bước 1 và 2 (gợi ý ưu đãi)     │
│                                                             │
│ Metric: Tăng tỉ lệ giao dịch dùng đúng ưu đãi từ 40% ──>    │
│ 60%; giảm khiếu nại "thiếu ưu đãi" 30%.                     │
│                                                             │
│ Quick Architecture: [x] Rule  [ ] LLM  [ ] Agent            │
│ (Gợi ý ưu đãi theo điều kiện là bài toán rule engine)       │
└─────────────────────────────────────────────────────────────┘
```

### Card #3 — Phân loại và định tuyến khiếu nại "điểm không được cộng/trừ"

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Khiếu nại điểm không đúng được nhập dạng văn bản  │
│ tự do, nhân viên phải đọc và gán thủ công cho đúng đội xử lý│
│ Công ty thành viên: [x] Xanh SM  [x] VinFast  [x] Khác: VPoint│
│                                                             │
│ Ai đang đau? Nhân viên back-office (đọc/gán thủ công),      │
│ khách (chờ lâu vì ticket gán sai đội)                       │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│  1. Khách gửi khiếu nại ──> 2. Nhân viên đọc và phân loại   │
│  ──> 3. Chuyển cho đội đối tác ──> 4. Đối soát, hoàn điểm   │
│                                                             │
│ Bước tốn nhất/lỗi nhất? Bước 2-3 ( ~6 phút/ticket; gán    │
│ sai đội làm kéo dài xử lý)                                  │
│ AI nhảy vào ở bước nào? Bước 2 (phân loại + tóm tắt)        │
│                                                             │
│ Metric: Phân loại đúng đội ≥ 90%; thời gian gán ticket      │
│ từ 6 phút ──> dưới 1 phút.                                  │
│                                                             │
│ Quick Architecture: [ ] Rule  [x] LLM  [ ] Agent            │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định chọn bài toán Deep-Dive

**Chọn: Card #1 — Co-pilot CSKH VPoint.**

| Card | Lý do chọn / loại |
|------|-------------------|
| **#1 (chọn)** | Vấn đề này chạm trực tiếp đúng đề tài (điểm, hạng, quyền lợi liên thông). Có người duyệt (agent CSKH) nên rủi ro kiểm soát được. Có thể giới hạn scope hẹp để thử nghiệm. Cần LLM thật sự ở phần diễn giải chính sách và soạn lời. |
| #2 | Về bản chất là **rule engine** (điều kiện hạng + loại dịch vụ → ưu đãi). Dùng LLM ở đây là over-engineering. Nên làm bằng rule trước. |
| #3 | Giá trị tốt nhưng là back-office, ít ảnh hưởng thời gian thực và trải nghiệm khách. Phù hợp làm giai đoạn sau, khi đã có dữ liệu ticket đã gán nhãn. |
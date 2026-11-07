# 01 — Problem Scan & Quick Cards (Vin Smart Future)

> **Lưu ý về số liệu:** Các con số thời gian, tỉ lệ và metric dưới đây là **ước tính giả định** để phục vụ scoping, chưa được đo từ dữ liệu thật của Vingroup. Khi Deep-Dive cần xác minh lại với người vận hành thực tế.

---

## 🔍 Phase 1 — SCAN (4 Lenses)

Quét qua 6 công ty thành viên, dùng đủ 4 lenses: Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinFast** | Tốn thời gian | Cố vấn dịch vụ phải xét một yêu cầu bảo hành (đặc biệt pin và hệ truyền động) bằng cách đối chiếu sổ bảo hành, lịch sử bảo dưỡng, ngày mua và điều khoản từng dòng xe để xác định lỗi có thuộc diện bảo hành không. Mỗi hồ sơ mất hàng chục phút và dễ áp dụng điều khoản không nhất quán giữa các xưởng. |
| 2 | **Vinmec** | Pain từ người khác | Bộ phận thanh toán bảo hiểm phải kiểm tra hồ sơ bệnh án so với điều khoản hợp đồng bảo hiểm trước khi gửi yêu cầu bồi thường. Hồ sơ thiếu giấy tờ hoặc sai mã dịch vụ bị công ty bảo hiểm từ chối, bệnh nhân phải chờ lâu và phải bổ sung nhiều vòng. |
| 3 | **Vinpearl** | AI có thể tốt hơn | Khách gửi yêu cầu đặc biệt trước kỳ nghỉ (ăn chay, dị ứng, phòng tầng cao, đón sân bay, trang trí kỷ niệm) qua email, chat, WhatsApp bằng nhiều ngôn ngữ. Nhân viên Guest Relations đọc rời rạc rồi chuyển thủ công cho Buồng phòng, F&B, Lễ tân nên dễ sót. |
| 4 | **Xanh SM** | Lặp lại | Mỗi tài xế mới phải được duyệt hồ sơ (CCCD, GPLX, đăng kiểm, bảo hiểm xe, lý lịch). Nhân viên onboarding mở từng ảnh giấy tờ, đối chiếu thông tin và hạn hiệu lực, lặp lại hàng trăm lần mỗi ngày. |
| 5 | **Vinhomes** | Pain từ người khác | Cư dân và nhà thầu nộp hồ sơ xin thi công nội thất (bản vẽ, giấy phép, danh sách công nhân, cam kết). Ban quản lý kiểm tra thủ công theo nội quy, hồ sơ thường bị trả lại nhiều lần vì thiếu, khiến cư dân bức xúc và dự án trễ tiến độ. |
| 6 | **Vinschool** | Tốn thời gian | Mỗi giáo viên chủ nhiệm phải viết nhận xét cá nhân hóa cho 30–40 học sinh mỗi kỳ. Việc này tốn nhiều giờ, nhận xét dễ rập khuôn vì giáo viên phải tổng hợp điểm số, ghi chú hành vi và bài làm rải rác. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

### Card #1 — Trợ lý thẩm định sơ bộ yêu cầu bảo hành VinFast

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Cố vấn dịch vụ VinFast mất nhiều thời     │
│ gian đối chiếu điều khoản để biết một lỗi có được bảo hành  │
│ hay không.                                                  │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác: _______________  │
│                                                             │
│ Ai đang đau (Actor)? Cố vấn dịch vụ tại xưởng; khách hàng   │
│ (chờ kết luận lâu, nhận câu trả lời khác nhau giữa các      │
│ xưởng).                                                     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│  1. Tiếp nhận xe + mô tả lỗi ──> 2. Tra ngày mua, số km,    │
│  lịch sử bảo dưỡng ──> 3. Tra điều khoản bảo hành theo dòng │
│  xe/linh kiện ──> 4. Kết luận diện bảo hành hay tính phí    │
│  ──> 5. Soạn thông báo gửi khách                            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 và 4                │
│   (⏱ ~20 phút/hồ sơ, ước tính)                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3: truy xuất     │
│ đúng điều khoản và trích dẫn. Bước 5: soạn NHÁP thông báo.  │
│ (Việc tính hạn bảo hành theo ngày/km do rule code làm,      │
│ không để LLM tính.)                                         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   "Giảm thời gian thẩm định từ 20 phút ──> dưới 7 phút;     │
│   ≥ 90% nháp trích dẫn đúng điều khoản khi kiểm tra mẫu."   │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
│ (Rule tính hạn/km; LLM truy xuất điều khoản và soạn lời)    │
└─────────────────────────────────────────────────────────────┘
```

### Card #2 — Kiểm tra trước hồ sơ bồi thường bảo hiểm tại Vinmec

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Hồ sơ bồi thường bảo hiểm của bệnh nhân   │
│ Vinmec thường bị từ chối vì thiếu giấy tờ hoặc sai mã dịch  │
│ vụ, phải bổ sung nhiều vòng.                                │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác: _______________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên thanh toán bảo hiểm của      │
│ Vinmec; bệnh nhân (chờ bồi thường lâu).                     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│  1. Gom hồ sơ bệnh án, hóa đơn, chỉ định ──> 2. Đối chiếu   │
│  điều khoản hợp đồng bảo hiểm ──> 3. Kiểm tra đủ giấy tờ và │
│  mã dịch vụ ──> 4. Gửi công ty bảo hiểm ──> 5. Nhận từ chối │
│  và bổ sung                                                 │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 và 3                │
│   (⏱ ~30 phút/hồ sơ; ~20% bị yêu cầu bổ sung, ước tính)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3: đọc hợp     │
│ đồng, liệt kê điều khoản liên quan và danh sách giấy tờ còn │
│ thiếu để nhân viên xem trước khi gửi.                       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   "Giảm tỉ lệ hồ sơ bị yêu cầu bổ sung từ 20% ──> dưới 8%;  │
│   giảm thời gian kiểm tra từ 30 phút ──> dưới 10 phút."     │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
│ (Rule kiểm tra danh sách giấy tờ; LLM đọc điều khoản.       │
│ Con người luôn duyệt trước khi gửi, dữ liệu y tế nhạy cảm.) │
└─────────────────────────────────────────────────────────────┘
```

### Card #3 — Tổng hợp yêu cầu đặc biệt của khách Vinpearl

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Yêu cầu đặc biệt của khách đến từ nhiều   │
│ kênh và nhiều ngôn ngữ, bị sót khi chuyển cho các bộ phận.  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: Vinpearl         │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên Guest Relations; khách       │
│ (đến nơi vẫn bị thiếu món ăn chay, sai loại phòng...).      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│  1. Đọc email/chat/WhatsApp của khách ──> 2. Ghi tay yêu    │
│  cầu vào PMS hoặc sổ ──> 3. Nhắn/gọi từng bộ phận (Buồng    │
│  phòng, F&B, Lễ tân) ──> 4. Kiểm tra lại trước ngày check-in│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 và 3                │
│   (⏱ ~15 phút/đặt phòng; ~1 trong 10 đặt phòng sót yêu cầu, │
│   ước tính)                                                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-2: đọc tin     │
│ nhắn đa ngôn ngữ, tách yêu cầu thành các trường có cấu trúc │
│ và soạn NHÁP brief cho từng bộ phận.                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   "Giảm thời gian xử lý từ 15 phút ──> dưới 4 phút/đặt      │
│   phòng; giảm tỉ lệ sót yêu cầu từ 10% ──> dưới 2%."        │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
│ (LLM trích xuất và soạn nháp; nhân viên duyệt trước khi gửi.│
│ Dị ứng thực phẩm là thông tin an toàn nên luôn cần người    │
│ xác nhận.)                                                  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Bài toán đề xuất cho Deep-Dive

**Đề xuất: Card #1 — Trợ lý thẩm định sơ bộ yêu cầu bảo hành VinFast.**

| Card | Nhận xét |
|------|----------|
| **#1 (đề xuất)** | Quy trình dễ vẽ thành workflow rõ ràng. Cần cả rule (tính hạn, số km) lẫn LLM (truy xuất điều khoản), nên có chỗ so sánh Rule với LLM trong AI-Fit. Ranh giới rõ: AI chỉ soạn nháp, cố vấn dịch vụ ra quyết định cuối. |
| #2 | Giá trị cao nhưng dữ liệu bệnh án là thông tin nhạy cảm, phần quyền truy cập và bảo mật sẽ làm Deep-Dive rộng hơn một buổi lab. |
| #3 | Phù hợp LLM nhưng quy mô nhỏ hơn, tác động tài chính thấp hơn hai card còn lại. |

**Bài toán đã quét nhưng không đưa vào card:**
- *Xanh SM duyệt hồ sơ tài xế:* phần lớn là OCR cộng đối chiếu theo luật, LLM đóng góp ít. Theo nguyên tắc "Problem First, AI Second", nên làm bằng rule trước.
- *Vinhomes duyệt hồ sơ thi công* và *Vinschool nhận xét học sinh:* để giai đoạn sau.

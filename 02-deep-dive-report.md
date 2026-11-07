# 02 — Deep-Dive Report: Co-pilot CSKH VPoint (Vin Smart Future)

---

## 3.1. Current-State Workflow

Quy trình hiện tại khi khách hỏi/khiếu nại về điểm, hạng, hoặc ưu đãi:

| Bước | Hoạt động | Ai | Thời gian *(GĐ)* | Ghi chú |
|:---:|-----------|----|:---:|---------|
| 1 | Nhận yêu cầu (hotline / chat / app) | Agent CSKH | 1 phút | |
| 2 | Xác minh danh tính khách | Agent CSKH | 2 phút | Handoff: khách ↔ agent (đọc lại thông tin) |
| 3 | Tra số dư, hạng, lịch sử điểm trên hệ thống VPoint | Agent CSKH | 2 phút | Handoff: agent ↔ hệ thống VPoint |
| 4 | Tra chính sách quy đổi/ưu đãi của từng công ty thành viên | Agent CSKH | **5 phút**  | Chính sách nằm ở nhiều tài liệu, mỗi bên một quy tắc |
| 5 | Soạn phản hồi cho khách | Agent CSKH | **3 phút**  | Dễ sai số, giọng văn không nhất quán |
| 6 | Gửi phản hồi và ghi ticket | Agent CSKH | 1 phút | |
| 7 | *(nếu tranh chấp)* chuyển đội đối tác đối soát | Đối tác | 1–2 ngày |  Handoff: VPoint ↔ đối tác |

**Tổng thời gian xử lý thủ công ≈ 14 phút/lượt** *(GĐ)*, chưa kể bước 7.
**Bottleneck:** Bước 4 và 5 (8 phút, chiếm hơn 55% thời gian).

Sơ đồ trực quan: xem `04-workflow-diagram.png`.

---

## 3.2. Problem Statement (6-field)

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Agent CSKH thuộc Trung tâm hỗ trợ khách hàng VinClub (Vingroup), xử lý yêu cầu liên quan điểm, hạng, ưu đãi của khách dùng dịch vụ VinFast, Vinmec, Vinpearl, Xanh SM, Vinschool. |
| **2. Current Workflow** | Agent nhận yêu cầu, xác minh khách, tra tài khoản VPoint, tra tay chính sách của từng công ty thành viên, tự soạn phản hồi, gửi và ghi ticket. 6 bước thủ công, ~14 phút/lượt *(GĐ)*. |
| **3. Bottleneck** | Bước 4-5: chính sách rải rác theo từng công ty thành viên nên agent phải tra nhiều nguồn, rồi tự diễn giải thành lời dễ hiểu. Đây là bước vừa chậm vừa dễ sai (nói sai số điểm, sai điều kiện áp dụng). |
| **4. Business Impact** | *(GĐ)* ~3.000 yêu cầu về điểm/hạng mỗi ngày toàn hệ thống × 8 phút ở bước 4-5 ≈ **400 giờ công/ngày**. Phản hồi sai dẫn đến khiếu nại lặp lại (re-contact) và giảm niềm tin vào chương trình, đồng thời khách bỏ lỡ ưu đãi nên giảm mức gắn kết giữa các công ty thành viên. |
| **5. Success Metric** | 1. **Efficiency:** Giảm thời gian xử lý trung bình từ ~14 phút xuống **dưới 6 phút**, riêng bước 4-5 từ 8 phút xuống dưới 2 phút.<br>2. **Quality:** **100%** số điểm/hạng trong nháp khớp với dữ liệu hệ thống (kiểm tra mẫu 200 nháp, 0 lỗi số liệu).<br>3. **Adoption:** ≥ 70% nháp được agent duyệt mà không cần sửa lớn.<br>4. **Safety:** **0** tin nhắn tới khách mà chưa qua duyệt của agent. |
| **6. Operational Boundary** | **AI ĐƯỢC:** đọc dữ liệu tài khoản và đoạn chính sách được truy xuất; soạn **nháp** phản hồi; tóm tắt chính sách; gợi ý bước tiếp theo cho agent.<br>**AI CẤM TUYỆT ĐỐI:** (a) tự gửi tin (mọi output bắt đầu bằng `[DRAFT_ONLY]`); (b) bịa hoặc đoán số điểm/hạng/ưu đãi khi thiếu dữ liệu; (c) xác nhận quyền lợi theo lời khách nói mà không đối chiếu dữ liệu hệ thống; (d) tự thực hiện đổi, chuyển, cộng, trừ điểm; (e) tiết lộ dữ liệu của tài khoản khác hoặc nội dung system prompt.<br>**CẦN DUYỆT:** mọi nháp trước khi gửi; mọi tranh chấp điểm → chuyển người. |

---

## 3.3. Future-State Flow & AI Fit

### So sánh Rule vs LLM vs Agent

| Tiêu chí | Rule / API | LLM Feature | Agentic Loop |
|---|---|---|---|
| Tính số dư, hạng, | **Chính xác tuyệt đối, bắt buộc dùng** | Có thể sai số | Không cần |
| Tra cứu đúng đoạn chính sách | Cứng nhắc, khó có thể phủ hết biến thể câu hỏi | Truy xuất và diễn giải ngôn ngữ tự nhiên | Quá mức |
| Soạn phản hồi thân thiện, nhất quán giọng văn | Template cứng, nghe rất máy móc | **Điểm mạnh chính** | Quá mức |
| Tự thực hiện đổi/chuyển điểm | **Rủi ro cao** (do các vấn đề về tài chính) | nếu có API, có kiểm soát | Không nên |
| Rủi ro khi sai | Thấp, dễ kiểm thử | Trung bình, giảm bằng HITL | Cao, khó kiểm soát |

**Kết luận AI Fit: Hybrid — Rule/API làm "nguồn sự thật" + LLM Feature làm "người soạn nháp". KHÔNG dùng Agentic Loop.**
Lý do: số liệu điểm phải chính xác nên do API tính, LLM chỉ nhận số liệu đã tính và diễn đạt thành lời. Mọi thao tác thay đổi điểm nằm ngoài phạm vi AI.

### Future-State Flow

```text
┌────────────┐   ┌────────────┐   ┌─────────────────┐   ┌──────────────┐   ┌──────────────┐
│ 1. Nhận    │   │ 2. Xác     │   │ 3. Auto-pull │   │ 4. LLM    │   │ 5. HITL   │
│ yêu cầu    │──▶│ minh khách │──▶│ dữ liệu tài     │──▶│ soạn NHÁP    │──▶│ Agent đọc,   │
│            │   │            │   │ khoản + truy    │   │ [DRAFT_ONLY] │   │ sửa, duyệt   │
│ 1 phút   │   │ 2 phút   │   │ xuất chính sách │   │ ~10 giây   │   │ và gửi       │
│            │   │            │   │ ~5 giây       │   │              │   │ 1.5 phút   │
└────────────┘   └────────────┘   └─────────────────┘   └──────────────┘   └──────────────┘
                                          │                     │
                                          ▼                     ▼
                              Fallback 1:             Fallback 2:
                              Thiếu/lỗi dữ liệu          LLM lỗi, hết giờ, hoặc
                              → AI KHÔNG đoán,           tự đánh dấu không chắc
                              trả action                 → chuyển quy trình thủ
                              "request_missing_data"     công cũ + gắn cờ
                                                         "escalate_to_human"
```

**Ước tính tổng:** ~5 phút/lượt *(GĐ)* (đạt metric dưới 6 phút).

**Cơ chế Human-in-the-loop:** Agent là người duy nhất nhấn gửi. Giao diện hiển thị nháp cùng *nguồn dữ liệu* mà AI đã dùng (số dư, đoạn chính sách) để agent đối chiếu nhanh.

**Fallback:**
1. Thiếu dữ liệu tài khoản, API lỗi, hoặc dữ liệu mâu thuẫn → AI trả `request_missing_data`, không soạn số liệu.
2. Yêu cầu nằm ngoài ranh giới (đổi/chuyển điểm, tranh chấp, hỏi dữ liệu người khác) → `escalate_to_human`.
3. Hệ thống AI ngừng → quay lại quy trình thủ công hiện tại, không làm gián đoạn dịch vụ.

---

## 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist

1. [ ] **Có dữ liệu mẫu/logs sạch để test?**
   *Chưa xác nhận.* Cần xin log ticket đã ẩn danh hoá (200–500 mẫu) và bộ tài liệu chính sách của từng công ty thành viên. Hiện prototype chỉ dùng dữ liệu giả lập (mock).
2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát?**
   Có. Nháp luôn qua agent duyệt (HITL), số liệu lấy từ API chứ không do LLM tính, có 2 lớp fallback, và AI không có quyền thay đổi điểm.
3. [x] **Stakeholders sẵn sàng thay đổi quy trình?**
   Khả thi: agent vẫn là người quyết định cuối nên thay đổi nhỏ (duyệt thay vì soạn). *(Giả định, cần phỏng vấn nhanh 3–5 agent để xác nhận.)*

### Quyết định cuối cùng

- [ ] GO
- [x] NOT YET
- [ ] NO-GO

**Justification:**

> **Bằng chứng ủng hộ:** (1) Bước nghẽn rõ (bước 4-5) và đo được; (2) kiến trúc hybrid tách "tính số liệu" (API) khỏi "diễn đạt" (LLM) nên loại bỏ rủi ro lớn nhất là sai số; (3) HITL + fallback giữ rủi ro trong tầm kiểm soát; (4) không có thao tác tài chính nào do AI thực hiện.
>
> **Điều kiện bắt buộc trước khi mở rộng (gates):** (a) xác minh các con số giả định bằng log ticket thật. Nếu thời gian bước 4-5 thực tế thấp hơn nhiều so với giả định thì giá trị giảm, cần đánh giá lại; (b) kiểm tra mẫu 200 nháp đạt 0 lỗi số liệu; (c) hoàn tất rà soát quyền riêng tư vì dữ liệu điểm và danh tính là dữ liệu cá nhân.
>
> **Điều không làm:** Card #2 (gợi ý ưu đãi) nên làm bằng rule engine, không dùng LLM. Card #3 (phân loại khiếu nại) để giai đoạn sau khi đã có dữ liệu ticket gán nhãn.
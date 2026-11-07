# 01 — Problem Scan & Quick Assess
## Lab 02: AI Product Scoping – Vin Smart Future

**Vai trò:** AI Product Engineer  
**Cá nhân/nhóm:** [Điền tên]  
**Ngày:** 08/11/2026  
**Đề tài được chọn để Deep-Dive:** VinFast After-sales Service AI Copilot

> **Quy ước bằng chứng:**  
> - **[Nguồn công khai]**: sự kiện hoặc hoạt động có thể kiểm tra bằng nguồn dẫn.  
> - **[Giả thuyết cần xác minh]**: pain point hợp lý theo quy trình nhưng chưa có dữ liệu nội bộ chứng minh VinGroup đang gặp đúng vấn đề này.  
> - **[Giả định mô phỏng]**: con số dùng để thiết kế prototype/bài tập, không phải KPI thực tế của Vingroup.

---

# Phase 1 — SCAN

## 1.1. Bảng quét cơ hội

| # | Công ty thành viên | Lens | Quy trình / bài toán được quét | Actor chịu ảnh hưởng | Bottleneck / dấu hiệu cần xác minh | AI opportunity sơ bộ |
|---:|---|---|---|---|---|---|
| 1 | **VinFast** | Lặp lại; Tốn thời gian; Stakeholder Pain | Tiếp nhận và phân loại yêu cầu bảo hành/sửa chữa từ hotline, ứng dụng và xưởng dịch vụ | CSKH, cố vấn dịch vụ, kỹ thuật viên, khách hàng | Mô tả triệu chứng không đồng nhất; phải hỏi bổ sung và tra cứu tài liệu; handoff giữa CSKH–dịch vụ–kỹ thuật. **[Giả thuyết cần xác minh]** | LLM trích xuất triệu chứng + RAG tra cứu tài liệu đã duyệt + Rule Engine kiểm tra cảnh báo an toàn |
| 2 | **Xanh SM (GSM)** | Lặp lại; AI-upgrade; Stakeholder Pain | Tiếp nhận và phân loại sự cố/than phiền của tài xế trong ca vận hành (app, xe, chuyến, điểm đón, thanh toán) | Tài xế, tổng đài, điều phối viên, đội hỗ trợ kỹ thuật | Thông tin đến từ nhiều kênh; phải xác định loại sự cố và mức ưu tiên trước khi chuyển đúng nhóm. **[Giả thuyết cần xác minh]** | LLM chuẩn hóa nội dung ticket, phân loại và tóm tắt; Rule-based định tuyến theo loại sự cố/SLA |
| 3 | **Vinhomes** | Tốn thời gian; Lặp lại; Stakeholder Pain | Phân loại phản ánh cư dân: kỹ thuật tòa nhà, vệ sinh, an ninh, tiện ích, phí dịch vụ | Cư dân, lễ tân/CSKH, ban quản lý, nhà thầu | Phản ánh đa dạng ngôn ngữ; trùng lặp; thiếu vị trí/ảnh; chuyển nhầm đơn vị. **[Giả thuyết cần xác minh]** | LLM phân loại/tóm tắt/nhận diện thông tin thiếu; Rule Engine định tuyến theo tòa–hạng mục–mức khẩn |
| 4 | **Vinmec** | Tốn thời gian; Lặp lại; AI-upgrade | Chuẩn hóa hồ sơ hành chính và điều phối yêu cầu tra cứu hồ sơ/đặt lịch khám | Nhân viên tiếp đón, điều dưỡng, tổng đài, bệnh nhân | Dữ liệu nhập không đồng nhất, nhiều bước xác nhận thông tin và chuyển khoa. **[Giả thuyết cần xác minh]** | LLM hỗ trợ trích xuất/chuẩn hóa dữ liệu hành chính; Rule-based kiểm tra trường bắt buộc. Không tự chẩn đoán hoặc quyết định điều trị |
| 5 | **Vinpearl / VinWonders** | Lặp lại; AI-upgrade; Stakeholder Pain | Hỏi đáp trước chuyến đi và xử lý yêu cầu liên quan vé, giờ hoạt động, quy định, đặt dịch vụ | Khách hàng, nhân viên CSKH, nhân viên tại điểm vui chơi | Câu hỏi lặp lại, chính sách thay đổi theo cơ sở/ngày; câu trả lời sai có thể gây khiếu nại. **[Giả thuyết cần xác minh]** | RAG trên FAQ/chính sách phiên bản mới; Rule-based xác nhận giao dịch/giá/điều kiện vé |

### Ghi chú về cách dùng 4 Lenses
- **Lặp lại:** tác vụ xuất hiện thường xuyên, có cấu trúc hoặc có thể chuẩn hóa.
- **Tốn thời gian:** nhiều thao tác đọc, tìm, sao chép, hỏi lại hoặc chuyển tiếp.
- **AI-upgrade:** đầu vào ngôn ngữ tự nhiên/không cấu trúc khiến quy tắc tĩnh khó bao phủ hết.
- **Stakeholder Pain:** phải xác nhận bằng phỏng vấn, ticket, SLA, khiếu nại hoặc quan sát thực địa; không suy diễn từ quy mô công ty.

## 1.2. Cơ sở chọn 5 cơ hội
Các công ty và lĩnh vực trên nằm trong phạm vi được worksheet Lab 02 nêu. Với VinFast, báo cáo bền vững 2024 của công ty công bố hoạt động cứu hộ đường bộ 24/7 với **97.511 lượt cứu hộ** và **153 đại lý 1S+, 2S, 3S toàn cầu cuối năm 2024**. VinFast cũng công bố chương trình triệu hồi **15.896 xe VF 8** tại Việt Nam vào tháng 01/2025. Những thông tin này chứng minh hoạt động hậu mãi và xử lý chiến dịch dịch vụ có quy mô thực tế; chúng **không chứng minh** rằng thời gian tiếp nhận hiện tại đang là 32 phút hay có tỷ lệ phân loại sai cụ thể.

Nguồn:
1. VinFast, *2024 Sustainability Report*: https://storage.googleapis.com/prod-storage-vinfast-us/esg/VinFast%202024%20Sustainability%20Report%20%28PDF%29.pdf
2. VinFast, thông báo triệu hồi 15.896 xe VF 8 (07/01/2025): https://vinfastauto.com/vn_vi/thong-bao-vinfast-trieu-hoi-15896-xe-vf-8-de-nang-cap-chat-luong
3. Worksheet Lab 02 – bối cảnh và 4 Lenses (tài liệu lớp học).

---

# Phase 2 — QUICK-ASSESS

> Các thời gian và target trong Quick Cards dưới đây là **giả định mô phỏng để tạo giả thuyết đo lường**, không phải số liệu nội bộ. Cần đo baseline từ ticket/log hoặc time study trước khi dùng làm business case.

## Quick Problem Card #1 — VinFast After-sales Service AI Copilot

**Bài toán (1 câu):** Hỗ trợ nhân viên tiếp nhận, chuẩn hóa, phân loại và chuyển yêu cầu bảo hành/sửa chữa xe điện tới đúng nhóm xử lý, kèm nguồn tài liệu tham chiếu.

- **Công ty thành viên:** VinFast
- **Actor:** Nhân viên CSKH/tổng đài, cố vấn dịch vụ, kỹ thuật viên, quản lý xưởng; khách hàng là người cung cấp đầu vào.
- **Workflow thủ công hiện tại (giả thuyết 4 bước):**
  1. Khách gửi mô tả sự cố qua hotline/app/trực tiếp.
  2. CSKH đọc, hỏi bổ sung thông tin xe và triệu chứng.
  3. CSKH/cố vấn tra cứu lịch sử, tài liệu và phân loại yêu cầu.
  4. Chuyển phiếu cho xưởng/kỹ thuật; nhân viên kiểm tra và xác nhận.
- **Bước tốn thời gian/lỗi nhất:** hỏi bổ sung + tra cứu tài liệu + tóm tắt/chuyển giao. **Giả định mô phỏng:** 25 phút trên tổng 32 phút/yêu cầu; phải time-study xác nhận.
- **AI hỗ trợ:** LLM trích xuất triệu chứng và trường còn thiếu; RAG truy xuất tài liệu kỹ thuật được phê duyệt; Rule Engine kiểm tra safety flags và routing; nhân viên phê duyệt.
- **Metrics đề xuất:** AHT từ baseline đo được giảm ≥30%; ≥90% ticket có đủ trường bắt buộc sau tối đa một vòng bổ sung; classification macro-F1 ≥0,90 trên test set đại diện; critical safety recall mục tiêu 100% trên bộ test đã định nghĩa (không đồng nghĩa bảo đảm an toàn tuyệt đối ngoài đời).
- **Quick Architecture:** ☑ Rule ☑ LLM; ☐ Agentic Loop ở MVP.
- **AI Fit:** LLM Feature + RAG trong workflow có kiểm soát; Rule-based cho điều kiện cứng và safety gate.
- **Rủi ro chính:** bỏ sót dấu hiệu an toàn, bịa tài liệu, lộ dữ liệu khách hàng, tư vấn vượt thẩm quyền.
- **Điều kiện tiếp tục:** có SOP/tài liệu kỹ thuật được chủ sở hữu phê duyệt, dữ liệu ticket đã khử định danh, và chuyên viên dịch vụ tham gia gán nhãn/duyệt.

## Quick Problem Card #2 — Xanh SM Driver Support Ticket Triage

**Bài toán (1 câu):** Chuẩn hóa và phân tuyến ticket hỗ trợ tài xế theo loại sự cố, mức ưu tiên và bộ phận chịu trách nhiệm.

- **Công ty thành viên:** GSM / Xanh SM
- **Actor:** Tài xế, tổng đài/CSKH, điều phối viên, nhóm kỹ thuật/đối soát.
- **Workflow thủ công hiện tại (giả thuyết):**
  1. Tài xế báo sự cố qua app/hotline.
  2. Nhân viên hỏi lại mã chuyến, thời gian, vị trí và mô tả.
  3. Nhân viên xác định nhóm: app/tài khoản, xe, chuyến, khách hàng, thanh toán.
  4. Chuyển nhóm xử lý và theo dõi phản hồi.
- **Bottleneck:** nội dung tự do thiếu trường thông tin; phân tuyến sai gây chuyển qua lại. **Giả định mô phỏng:** 8–15 phút/ticket, cần đo thực tế.
- **AI hỗ trợ:** LLM tóm tắt và trích xuất trường; Rule-based định tuyến theo category, khu vực và SLA.
- **Metrics đề xuất:** ≥90% ticket được gợi ý category đúng; giảm ≥25% thời gian phân tuyến; giảm ≥20% ticket bị chuyển nhóm lần hai.
- **Quick Architecture:** ☑ Rule ☑ LLM; Agent chưa cần thiết.
- **Operational boundary:** AI không tự khóa tài khoản tài xế, không tự phạt/khấu trừ thu nhập, không tự kết luận lỗi thuộc về tài xế.
- **Rủi ro:** nhầm lẫn khiếu nại nghiêm trọng, sai dữ liệu chuyến, thiên lệch trong phân loại.
- **Điều kiện tiếp tục:** có taxonomy ticket, SLA và dữ liệu lịch sử được phép sử dụng.

## Quick Problem Card #3 — Vinhomes Resident Feedback Triage

**Bài toán (1 câu):** Phân loại phản ánh cư dân và đề xuất đơn vị xử lý dựa trên nội dung, vị trí và mức độ khẩn cấp.

- **Công ty thành viên:** Vinhomes
- **Actor:** Cư dân, CSKH/lễ tân, ban quản lý, nhà thầu vận hành.
- **Workflow thủ công hiện tại (giả thuyết):**
  1. Cư dân gửi phản ánh qua app/hotline/quầy.
  2. Nhân viên đọc nội dung và hỏi lại vị trí/ảnh.
  3. Phân loại nhóm: kỹ thuật, vệ sinh, an ninh, tiện ích, phí dịch vụ.
  4. Chuyển nhà thầu/ban chuyên môn và cập nhật trạng thái.
- **Bottleneck:** phản ánh viết tự do, trùng lặp, thiếu block/tầng/vị trí; định tuyến phụ thuộc kinh nghiệm nhân viên. **Giả định mô phỏng:** 5–12 phút/ticket.
- **AI hỗ trợ:** LLM phân loại, tóm tắt, phát hiện trường thiếu và nhóm phản ánh tương tự; Rule-based định tuyến theo khu/tòa/hạng mục.
- **Metrics đề xuất:** ≥90% phân loại đúng; giảm ≥30% thời gian triage; ≥95% ticket được gắn đúng khu vực trước khi chuyển.
- **Quick Architecture:** ☑ Rule ☑ LLM; chưa cần Agentic Loop.
- **Operational boundary:** AI không tự đóng khiếu nại, không tự cam kết bồi thường, không tự kết luận trách nhiệm pháp lý.
- **Rủi ro:** bỏ sót sự cố an ninh/an toàn, lộ dữ liệu cư dân, phân tuyến sai.
- **Điều kiện tiếp tục:** có danh mục tòa/khu, taxonomy sự cố, quy tắc escalation và người quản lý xác nhận.

---

## 2.3. Lựa chọn bài toán Deep-Dive

**Chọn Quick Card #1 – VinFast After-sales Service AI Copilot.**

Lý do:
1. Có bằng chứng công khai trực tiếp về hoạt động hậu mãi, cứu hộ và chiến dịch triệu hồi.
2. Bài toán kết hợp dữ liệu phi cấu trúc (mô tả triệu chứng) và dữ liệu có cấu trúc (mẫu xe, mã yêu cầu, lịch sử dịch vụ).
3. Có ranh giới an toàn rõ: AI hỗ trợ hành chính/triage, không thay kỹ thuật viên chẩn đoán hay quyết định bảo hành.
4. Có thể làm prototype hẹp bằng prompt + JSON schema + bộ test giả lập trước khi cần tích hợp hệ thống thật.

**Điều chưa biết cần xác minh:** AHT thật, số ticket/tháng tại một xưởng, tỷ lệ thiếu thông tin, tỷ lệ chuyển sai, chi phí nhân công quy đổi, quyền truy cập dữ liệu và mức độ sẵn sàng của nhân viên.

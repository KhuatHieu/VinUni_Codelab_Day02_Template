# 02 — Deep-Dive Report & Evaluate
## VinFast After-sales Service AI Copilot

**Vai trò:** AI Product Engineer – Vin Smart Future  
**Phạm vi:** hỗ trợ tiếp nhận và phân loại yêu cầu dịch vụ; không tự chẩn đoán kỹ thuật, không quyết định bảo hành.  
**Trạng thái bằng chứng:** có nguồn công khai chứng minh quy mô hoạt động hậu mãi; các bottleneck, thời gian và chi phí nội bộ dưới đây là giả thuyết/giả định mô phỏng cần khảo sát.

---

# Phase 3 — DEEP-DIVE

## 3.1. Business context & evidence

VinFast công bố trong *2024 Sustainability Report*:
- Cung cấp cứu hộ đường bộ 24/7 và hỗ trợ sạc lưu động; báo cáo ghi nhận **97.511 lượt cứu hộ**.
- Cuối năm 2024 có **153 đại lý 1S+, 2S, 3S đang hoạt động trên toàn cầu**.
- Ứng dụng VinFast được mô tả là nền tảng hỗ trợ đặt lịch dịch vụ, yêu cầu hỗ trợ và theo dõi tình trạng xe.

VinFast công bố ngày 07/01/2025 chương trình triệu hồi tự nguyện **15.896 xe VF 8** tại Việt Nam để nâng cấp miễn phí túi khí giữa; thời gian thay thế dự kiến khoảng 45 phút/xe.

**Diễn giải đúng:** các dữ kiện này chứng minh quy trình hậu mãi, hỗ trợ và chiến dịch dịch vụ là hoạt động thực tế, có nhiều tương tác và yêu cầu phối hợp. Chúng **không chứng minh** có bottleneck cụ thể là 32 phút/yêu cầu, 18% ticket thiếu thông tin hoặc thiệt hại 1,2 tỷ VNĐ. Các số liệu vận hành đó phải lấy từ CRM/ticket, time study hoặc phỏng vấn.

Nguồn:
1. VinFast, *2024 Sustainability Report*: https://storage.googleapis.com/prod-storage-vinfast-us/esg/VinFast%202024%20Sustainability%20Report%20%28PDF%29.pdf
2. VinFast, thông báo triệu hồi VF 8 ngày 07/01/2025: https://vinfastauto.com/vn_vi/thong-bao-vinfast-trieu-hoi-15896-xe-vf-8-de-nang-cap-chat-luong
3. Cục Đăng kiểm Việt Nam, thông tin triệu hồi VF 8: https://www.vr.org.vn/contents/notice/Lists/Notice/Attachments/3331/02.%20Vinfast%20VF8%20-%20Tui%20khi_ALL.pdf

## 3.2. Current-State Workflow Mapping (AS-IS)

### Swimlane 4 làn

> **Lưu ý:** sơ đồ là workflow giả thuyết được dựng để scoping. Cần xác nhận bằng quan sát quy trình tại một trung tâm dịch vụ trước khi coi đây là AS-IS chính thức.

| Thứ tự | Khách hàng | CSKH / Tổng đài | Cố vấn dịch vụ / Kỹ thuật | Quản lý trung tâm |
|---|---|---|---|---|
| 1 | Gửi yêu cầu qua app/hotline/trực tiếp (2 phút) | Tiếp nhận yêu cầu |  |  |
| 2 | Bổ sung mô tả, mã xe, ảnh khi được hỏi | Đọc và hỏi bổ sung, xác minh thông tin (8 phút) |  |  |
| 3 |  | 🔄 **Handoff 1:** chuyển thông tin/ticket | Nhận ticket, tra cứu lịch sử và tài liệu (12 phút) 🔴 **Bottleneck B1** |  |
| 4 |  |  | Phân loại, đánh giá sơ bộ, chọn nhóm xử lý (6 phút) 🔴 **Bottleneck B2** |  |
| 5 |  |  | 🔄 **Handoff 2:** chuyển đề xuất/phiếu xử lý |  |
| 6 |  |  | Đề xuất lịch/nguồn lực; trường hợp đặc biệt cần escalation (2 phút) | Xem xét và phê duyệt ngoại lệ (2 phút) |
| 7 | Nhận thông tin lịch/next step | 🔄 **Handoff 3:** xác nhận lại với khách | Cập nhật ticket và kế hoạch dịch vụ (2 phút) |  |

**Tổng thời gian minh họa: 34 phút/lượt** (2 + 8 + 12 + 6 + 2 + 2 + 2). Đây là tổng thời gian thao tác/đợi được đơn giản hóa cho bài tập, chưa phải cycle time đo được. Nếu cần giữ baseline 32 phút như giả định ban đầu, phải đo lại và thống nhất định nghĩa thời gian; không trộn thời gian thao tác với thời gian chờ.

### Bottlenecks
- **B1 – Tra cứu (12 phút giả định):** nhân viên phải tìm lịch sử và tài liệu phù hợp với mẫu xe/triệu chứng.
- **B2 – Phân loại (6 phút giả định):** mô tả tự do có thể thiếu thông tin; phân loại cần kinh nghiệm.
- **B3 – Handoff (không cộng thêm phút độc lập):** dữ liệu chuyển giao có thể thiếu ngữ cảnh, khiến bộ phận sau phải hỏi lại.

### Handoff cần thể hiện trên sơ đồ
1. Khách hàng → CSKH: tiếp nhận thông tin.
2. CSKH → Cố vấn dịch vụ/kỹ thuật: chuyển ticket.
3. Dịch vụ/kỹ thuật → Quản lý: xin phê duyệt ngoại lệ; sau đó thông tin được xác nhận về khách hàng.

## 3.3. Problem Statement (6-field)

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH/tổng đài là người tiếp nhận; cố vấn dịch vụ và kỹ thuật viên là người đánh giá/chuyển xử lý; quản lý trung tâm phê duyệt ngoại lệ. Khách hàng cung cấp mô tả và thông tin xe. |
| **2. Current Workflow** | Khách gửi yêu cầu qua app/hotline/trực tiếp → CSKH đọc và hỏi bổ sung → tra cứu lịch sử/tài liệu → cố vấn phân loại/đề xuất nhóm xử lý → chuyển ticket và xác nhận với khách. Công cụ cụ thể (CRM, DMS, knowledge base) cần xác minh tại site. |
| **3. Bottleneck** | Thông tin đầu vào không đồng nhất; nhân viên phải hỏi bổ sung và tra cứu nhiều nguồn; việc tóm tắt và chuyển giao có thể làm mất ngữ cảnh. Các bước tra cứu và phân loại là ứng viên bottleneck, cần time study để xác nhận. |
| **4. Business Impact** | Có thể làm tăng thời gian xử lý, chi phí lao động, số lần liên hệ lại và nguy cơ chậm SLA. Nguồn công khai cho thấy quy mô hoạt động hậu mãi lớn (97.511 lượt cứu hộ; 153 đại lý toàn cầu cuối 2024), nhưng chưa cung cấp AHT/tỷ lệ lỗi nội bộ. |
| **5. Success Metric** | Pilot mục tiêu: giảm ≥30% median handling time so với baseline đo trong 2 tuần; ≥90% ticket có đủ trường bắt buộc sau một vòng bổ sung; macro-F1 phân loại ≥0,90 trên test set được chuyên viên gán nhãn; critical safety recall 100% trên bộ test tình huống nguy hiểm đã định nghĩa; human correction rate ≤10% cho nhóm ticket thông thường. |
| **6. Operational Boundary** | AI được phép tóm tắt, trích xuất trường, gợi ý category/priority, tìm tài liệu trong kho được duyệt và soạn bản nháp. AI không được chẩn đoán xác định, hướng dẫn sửa chữa điện áp cao, tuyên bố xe an toàn, quyết định quyền lợi bảo hành/chi phí, tự đóng ticket hoặc gửi cam kết ra ngoài. Nhân viên duyệt mọi phân loại trước khi chuyển; tình huống critical được Rule Engine escalation độc lập. |

## 3.4. Metrics & Measurement Plan

| Metric | Baseline | Target pilot | Cách đo |
|---|---|---|---|
| Median handling time (AHT) | Chưa biết; time study 2 tuần | Giảm ≥30% | Timestamp các bước trên ticket, tách active time và waiting time |
| Ticket completeness | Chưa biết | ≥90% sau tối đa 1 vòng hỏi bổ sung | Tỷ lệ ticket đủ trường bắt buộc |
| Classification macro-F1 | Chưa có gold set | ≥0,90 | Bộ test do cố vấn dịch vụ gán nhãn; báo cáo theo từng lớp |
| Critical safety recall | Chưa có baseline | 100% trên bộ test đã định nghĩa | Test case nguy hiểm độc lập; đánh giá từng nhóm safety flag |
| Human correction rate | Chưa biết | ≤10% ở ticket thường | Số gợi ý bị sửa / tổng gợi ý được review |
| Unsupported citation rate | Chưa biết | 0% trong test acceptance | Kiểm tra nguồn trả về có tồn tại và hỗ trợ claim |
| Adoption | Chưa có | ≥70% nhân viên pilot dùng hằng tuần | Log sử dụng + khảo sát nhân viên |

**Không dùng accuracy tổng thể thay cho recall của lớp critical.** Bộ test safety cần đủ tình huống, được chuyên gia duyệt và không được diễn giải 100% trên test set thành bảo đảm an toàn tuyệt đối trong môi trường thực.

## 3.5. AI Fit Matrix — Rule vs LLM Feature vs Agentic Loop

| Năng lực | Rule-based / State Machine | LLM Feature + RAG | Agentic Loop |
|---|---|---|---|
| Kiểm tra trường bắt buộc, VIN format, category cố định | **Phù hợp nhất** | Không cần | Không cần |
| Hiểu mô tả tự do, tiếng Việt không chuẩn, lỗi chính tả | Khó bao phủ hết | **Phù hợp nhất** | Có thể nhưng không cần |
| Tóm tắt và chuẩn hóa ticket | Template cứng | **Phù hợp nhất** | Quá mức cần thiết |
| Truy xuất tài liệu kỹ thuật theo ngữ cảnh | Từ khóa/ID đơn giản | **RAG phù hợp** | Có thể điều phối nhiều nguồn |
| Điều kiện safety/escalation cứng | **Bắt buộc dùng Rule độc lập** | Không giao cho LLM tự quyết | Không giao cho agent |
| Tự tạo lịch, cập nhật CRM, gọi nhiều API | Workflow xác định | Có thể đề xuất hành động | Chỉ cân nhắc ở phase sau, có quyền hạn hẹp |

**Lựa chọn MVP:** Hybrid gồm Rule Engine + LLM Feature + RAG + Human approval. Chưa dùng Agentic Loop vì MVP chưa cần tự lập kế hoạch và thực thi chuỗi hành động tự chủ; thêm agent sẽ tăng độ phức tạp, chi phí, bề mặt prompt injection và rủi ro thao tác sai.

## 3.6. Future-State Flow (TO-BE)

1. **Khách hàng:** gửi mô tả, mẫu xe/VIN hoặc mã khách hàng qua kênh được phép.
2. **Input validation (Rule):** kiểm tra trường bắt buộc, định dạng, quyền truy cập và loại bỏ/che dữ liệu không cần thiết.
3. **AI Step – LLM:** trích xuất triệu chứng, dấu hiệu cảnh báo, thông tin thiếu và tạo bản tóm tắt có cấu trúc.
4. **AI Step – RAG:** tìm tài liệu đã được chủ sở hữu nghiệp vụ phê duyệt; trả về ID/tên tài liệu và đoạn tham chiếu. Không có nguồn phù hợp thì ghi `NO_EVIDENCE`.
5. **Safety Gate (Rule độc lập):** kiểm tra từ khóa/tín hiệu và quy tắc nguy hiểm đã được chuyên gia duyệt. Không cho LLM hạ cấp cảnh báo.
6. **Human-in-the-loop:** nhân viên xem dữ liệu gốc, tóm tắt, nguồn tài liệu và đề xuất. Có quyền sửa, từ chối hoặc chuyển chuyên gia.
7. **Controlled action:** chỉ sau khi người có thẩm quyền xác nhận mới tạo/cập nhật ticket hoặc chuyển bộ phận.
8. **Audit:** lưu model/version, prompt version, nguồn truy xuất, output, người duyệt và thay đổi (theo chính sách lưu trữ).

### HITL matrix

| Mức | Ví dụ | Hành động |
|---|---|---|
| **Green – Routine** | Yêu cầu lịch bảo dưỡng, hỏi thông tin dịch vụ không liên quan an toàn | AI soạn gợi ý; nhân viên xác nhận trước khi gửi/chuyển |
| **Amber – Review** | Triệu chứng mơ hồ, thiếu VIN, nhiều nhóm lỗi có thể đúng, nguồn RAG yếu | Bắt buộc nhân viên bổ sung/đánh giá; không tự động chuyển |
| **Red – Critical** | Khói, cháy, mùi khét, cảnh báo pin/cao áp, phanh mất tác dụng hoặc dấu hiệu nguy hiểm khác | Rule Engine kích hoạt escalation theo SOP đã duyệt; hiển thị hướng dẫn an toàn được phê duyệt; không chờ LLM và không hướng dẫn tự sửa |

### Fallback
- API/model timeout hoặc lỗi JSON → không tạo hành động; hiển thị lỗi và đưa ticket vào hàng chờ xử lý thủ công.
- RAG không tìm thấy tài liệu hoặc nguồn mâu thuẫn → `NEEDS_HUMAN_REVIEW`, không suy đoán.
- Thiếu dữ liệu/độ tin cậy chưa được hiệu chuẩn → yêu cầu nhân viên xác minh; không coi self-reported confidence của LLM là xác suất đúng.
- Safety rule kích hoạt → escalation theo quy trình doanh nghiệp; AI không được override.
- CRM/dispatch integration lỗi → giữ bản nháp, ghi log và chuyển sang quy trình nhập thủ công.

## 3.7. Operational Boundary & Security

**Allowed**
- Tóm tắt và chuẩn hóa mô tả khách hàng.
- Trích xuất trường từ dữ liệu được phép.
- Đề xuất category/priority có giải thích.
- Tra cứu kho tài liệu được duyệt và dẫn nguồn.
- Soạn bản nháp cho nhân viên xem xét.

**Prohibited**
- Chẩn đoán kỹ thuật cuối cùng hoặc xác nhận xe có thể tiếp tục vận hành.
- Hướng dẫn khách tự tháo/lắp/sửa pin cao áp, hệ thống phanh hoặc bộ phận nguy hiểm.
- Quyết định bảo hành, bồi thường, chi phí hoặc trách nhiệm pháp lý.
- Tự đóng ticket, tự gửi thông báo có cam kết hoặc tự thực hiện thao tác ảnh hưởng khách hàng khi chưa có phê duyệt.
- Truy cập dữ liệu ngoài phạm vi quyền hạn hoặc dùng dữ liệu khách hàng để huấn luyện nhà cung cấp khi chưa có cơ sở pháp lý/phê duyệt.

**Data protection:** thiết kế theo nguyên tắc tối thiểu hóa dữ liệu, phân quyền theo vai trò, mã hóa khi truyền/lưu, audit log, thời hạn lưu và quy trình xử lý yêu cầu của chủ thể dữ liệu. Cần bộ phận pháp chế/DPO xác định căn cứ xử lý, vai trò các bên và yêu cầu chuyển dữ liệu xuyên biên giới theo pháp luật hiện hành. Luật Bảo vệ dữ liệu cá nhân 91/2025/QH15 có hiệu lực 01/01/2026; không xem ghi chú này là tư vấn pháp lý.

---

# Phase 5 — EVALUATE

## 5.1. AI Readiness Checklist

| # | Checklist theo worksheet | Trạng thái hiện tại | Bằng chứng / việc còn thiếu |
|---:|---|---|---|
| 1 | Có dữ liệu mẫu/logs sạch để test? | ☐ YES ☑ NO | Chưa có ticket/log nội bộ được cấp quyền. Có thể tạo synthetic test set để kiểm tra logic, nhưng không thay thế dữ liệu thật. |
| 2 | Rủi ro khi AI sai nằm trong tầm kiểm soát qua HITL/Fallback? | ☑ PARTIAL | Đã thiết kế safety gate, HITL và fallback ở mức kiến trúc; cần chuyên gia dịch vụ duyệt SOP, taxonomy critical và chạy adversarial/safety tests. |
| 3 | Stakeholders sẵn sàng thay đổi quy trình? | ☐ YES ☑ UNKNOWN | Chưa phỏng vấn CSKH, cố vấn dịch vụ, quản lý xưởng, IT/security/legal. Cần có product owner và site pilot sponsor. |

## 5.2. Decision: NOT YET

<**Quyết định đề xuất:** NOT YET – Chưa triển khai pilot trên dữ liệu/khách hàng thật.>

**Lý do:**
1. Có bằng chứng công khai về quy mô hoạt động hậu mãi, nhưng chưa có dữ liệu nội bộ để xác nhận bottleneck và baseline.
2. Chưa có quyền truy cập tài liệu kỹ thuật được phê duyệt, ticket đã khử định danh và taxonomy sự cố.
3. Rủi ro an toàn xe điện khiến việc triển khai cần chuyên gia kỹ thuật, quy trình escalation và kiểm thử critical độc lập.
4. Chưa có xác nhận của chủ quy trình, IT/security và pháp chế về tích hợp, dữ liệu và vận hành.

**Không phải NO-GO:** bài toán có phần ngôn ngữ tự nhiên và tri thức tài liệu phù hợp với LLM + RAG; Rule-based đơn thuần khó xử lý đa dạng mô tả. Có thể tiếp tục một prototype offline với dữ liệu tổng hợp/đã được phép.

## 5.3. Điều kiện để chuyển sang GO

| Gate trước pilot | Điều kiện cần đạt | Owner đề xuất |
|---|---|---|
| Data | Có tối thiểu 300–500 ticket đã khử định danh và được phép dùng; chia train/dev/test theo thời gian hoặc nguồn để tránh leakage | Data owner + Legal |
| Knowledge | Kho tài liệu có version, owner, ngày hiệu lực, quyền truy cập; tài liệu critical được chuyên gia duyệt | Service engineering |
| Safety | Bộ test critical do chuyên gia xây dựng; Safety Gate không bị LLM override; có quy trình escalation ngoài hệ thống | Safety/Technical lead |
| Model quality | Macro-F1 ≥0,90 trên test set; báo cáo precision/recall từng lớp; đo unsupported citation | AI team + SME |
| Human workflow | Nhân viên có quyền approve/reject/edit; đo correction rate và adoption | Service operations |
| Security/legal | Phê duyệt data flow, vendor, retention, access control, logging và đánh giá pháp lý | Security + Legal |
| Business case | Baseline AHT và cost được đo; pilot cho thấy giảm ≥30% median handling time mà không suy giảm safety/quality | Product owner + Finance |

## 5.4. Pilot proposal (scope nhỏ)

- **Địa điểm:** một trung tâm dịch vụ được chọn sau khi có sponsor.
- **Thời lượng:** 2 tuần baseline + 4 tuần pilot có giám sát.
- **Use case:** chỉ triage ticket và truy xuất tài liệu; không tự chẩn đoán, không tự quyết định bảo hành, không tự gửi khách.
- **Cỡ mẫu:** mục tiêu ban đầu 300–500 ticket đủ điều kiện; điều chỉnh theo volume và phân tích thống kê.
- **So sánh:** nhóm quy trình hiện tại và nhóm có AI hỗ trợ; cùng taxonomy và cách đo.
- **Stop condition:** bất kỳ critical miss nào trong kiểm thử acceptance, rò rỉ dữ liệu, tài liệu nguồn sai/không còn hiệu lực hoặc hành động ngoài quyền hạn đều dừng luồng AI liên quan để điều tra.
- **Success:** đạt ngưỡng chất lượng và an toàn đã định, giảm AHT thực đo, nhân viên chấp nhận sử dụng và business case được Finance xác nhận.

## 5.5. ROI – mô hình minh họa, không phải số liệu VinFast

Giả định để kiểm tra độ nhạy:
- 1.000 ticket/tháng tại một site (giả định).
- Tiết kiệm 12 phút/ticket (giả định, cần đo).
- Chi phí lao động quy đổi 100.000 VNĐ/giờ (giả định).
- Chi phí prototype 60 triệu VNĐ (giả định).
- Chi phí vận hành 5 triệu VNĐ/tháng (giả định).

Tính:
- Giờ tiết kiệm = 1.000 × 12 / 60 = 200 giờ/tháng.
- Giá trị lao động quy đổi = 200 × 100.000 = 20 triệu VNĐ/tháng.
- Lợi ích ròng quy đổi = 20 − 5 = 15 triệu VNĐ/tháng.
- Payback đơn giản = 60 / 15 = 4 tháng.
- ROI 6 tháng = (120 − 30 − 60) / 60 = 50%.

**Diễn giải:** đây là giá trị năng lực lao động được giải phóng, không chắc chắn trở thành tiết kiệm tiền mặt. Chỉ ghi nhận benefit khi thời gian tiết kiệm được chuyển thành năng lực xử lý thêm, giảm overtime/outsourcing hoặc giảm chi phí có thể kiểm toán. Chưa có cơ sở để tuyên bố ROI thực tế hay hòa vốn dưới một tháng.

## 5.6. Risk Register

| Rủi ro | Hậu quả | Kiểm soát |
|---|---|---|
| Bỏ sót cảnh báo nguy hiểm | Nguy cơ an toàn cho khách hàng/kỹ thuật viên | Rule safety độc lập, escalation ngay, chuyên gia duyệt test |
| Hallucination tài liệu | Hướng dẫn sai, mất niềm tin | RAG whitelist, citation verification, abstain khi không có nguồn |
| Prompt injection trong ticket/tài liệu | AI làm theo chỉ thị độc hại trong nội dung đầu vào | Xem nội dung khách/tài liệu là dữ liệu không đáng tin; tách system policy; không cấp tool write quyền rộng |
| Lộ dữ liệu cá nhân/VIN/điện thoại | Vi phạm quyền riêng tư và pháp luật | Data minimization, masking, RBAC, encryption, retention policy |
| Tự động hóa quá mức | Ticket/khuyến nghị sai được thực thi | Human approval, read-only prototype, audit log |
| Tài liệu lỗi thời | Đề xuất theo chính sách cũ | Versioning, owner, effective date, revoke |
| ROI không đạt | Lãng phí đầu tư | Pilot có baseline, sensitivity analysis, stage-gate |

## 5.7. Legal & governance references

1. **Luật Bảo vệ dữ liệu cá nhân số 91/2025/QH15**, hiệu lực 01/01/2026. Nguồn chính thức: https://vanban.chinhphu.vn/?docid=214590&pageid=27160  
   Liên quan đến dữ liệu khách hàng, quyền chủ thể dữ liệu, mục đích/căn cứ xử lý, bảo vệ và trách nhiệm của các bên.
2. **Nghị định 356/2025/NĐ-CP** hướng dẫn Luật Bảo vệ dữ liệu cá nhân, hiệu lực 01/01/2026. Cần pháp chế xác nhận yêu cầu cụ thể áp dụng cho data flow và nhà cung cấp.
3. **Luật Bảo vệ quyền lợi người tiêu dùng 19/2023/QH15**, hiệu lực 01/07/2024. Nguồn tra cứu chính thức: https://vanban.chinhphu.vn/  
   Liên quan đến thông tin dịch vụ, bảo hành, khiếu nại và trách nhiệm doanh nghiệp.
4. Quy định về chất lượng/an toàn sản phẩm, hàng hóa và quy định chuyên ngành ô tô cần được pháp chế/đội homologation xác định theo từng thị trường và use case. Không để AI thay thế nghĩa vụ của nhà sản xuất/đơn vị dịch vụ.

## 5.8. Final management statement

> **NOT YET cho pilot vận hành thật; GO có điều kiện cho prototype offline.**  
> Bài toán có cơ sở hoạt động thực tế và AI Fit phù hợp ở phần hiểu ngôn ngữ, tóm tắt và truy xuất tri thức. Tuy nhiên, dữ liệu nội bộ, baseline, tài liệu được duyệt, owner nghiệp vụ và safety validation chưa sẵn sàng. Nhóm đề xuất hoàn thiện prototype bằng dữ liệu tổng hợp/đã được phép, sau đó chỉ mở pilot tại một site khi tất cả điều kiện Data, Safety, Legal và Operations được ký duyệt.

---

## Appendix — References & assumptions

### Public references
- VinFast 2024 Sustainability Report: https://storage.googleapis.com/prod-storage-vinfast-us/esg/VinFast%202024%20Sustainability%20Report%20%28PDF%29.pdf
- VinFast recall announcement, 15,896 VF 8 vehicles (07 Jan 2025): https://vinfastauto.com/vn_vi/thong-bao-vinfast-trieu-hoi-15896-xe-vf-8-de-nang-cap-chat-luong
- Vietnam Register recall notice: https://www.vr.org.vn/contents/notice/Lists/Notice/Attachments/3331/02.%20Vinfast%20VF8%20-%20Tui%20khi_ALL.pdf
- Law 91/2025/QH15: https://vanban.chinhphu.vn/?docid=214590&pageid=27160

### Assumptions to replace with field evidence
- Workflow steps and handoff count.
- Time per step and total handling/cycle time.
- Ticket volume, missing-information rate, misrouting rate.
- Labor cost, model/API cost, implementation cost.
- Target thresholds and pilot sample size.

### Source discipline
Không dùng số liệu báo chí về quy mô cứu hộ/triệu hồi để suy ra AHT, tỷ lệ phân loại sai hoặc tổn thất tài chính. Các chỉ số đó chỉ được xác nhận bằng dữ liệu quy trình của đơn vị pilot.

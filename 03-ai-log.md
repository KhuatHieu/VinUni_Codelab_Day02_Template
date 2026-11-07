# 03 — AI Log & Reflection
## Nhật ký tương tác AI – Lab 02: AI Product Scoping

**Đề tài:** VinFast After-sales Service AI Copilot  
**Công cụ:** ChatGPT (AI thought-partner)  
**Người thực hiện:** [Điền tên]  
**Ngày:** 08/11/2026

> **Tính trung thực của nhật ký:** Nội dung dưới đây ghi lại cách AI đã hỗ trợ hình thành bộ hồ sơ trong phiên làm việc này và các lỗi/giả định được phát hiện trong chính câu trả lời. Chưa có bằng chứng rằng nhóm đã chạy Gemini API, phỏng vấn nhân viên VinFast hoặc kiểm thử trên ticket nội bộ. Những phần đó được ghi là việc cần thực hiện, không ghi thành kết quả đã đạt.

---

## 1. AI đã giúp gì?

### 1.1. Mở rộng không gian tìm kiếm bài toán
AI hỗ trợ brainstorm các bài toán tại nhiều công ty thành viên:
- VinFast: tiếp nhận và phân loại yêu cầu hậu mãi.
- Xanh SM: phân loại ticket hỗ trợ tài xế.
- Vinhomes: phân loại phản ánh cư dân.
- Vinmec: chuẩn hóa hồ sơ hành chính/điều phối yêu cầu.
- Vinpearl/VinWonders: hỏi đáp chính sách và dịch vụ du lịch.

Điều hữu ích là AI giúp biến ý tưởng chung như “dùng chatbot” thành một workflow cụ thể: ai gửi thông tin, ai đọc, ai phân loại, ai nhận bàn giao và metric nào có thể đo.

### 1.2. Scoping và lựa chọn AI Fit
AI giúp so sánh ba lựa chọn:
- **Rule-based:** phù hợp với kiểm tra trường bắt buộc, định tuyến cố định và điều kiện an toàn có thể mô tả rõ.
- **LLM Feature + RAG:** phù hợp với mô tả triệu chứng bằng ngôn ngữ tự nhiên, chuẩn hóa ticket, tóm tắt và tìm tài liệu theo ngữ cảnh.
- **Agentic Loop:** chưa cần trong MVP vì chưa có nhu cầu cho AI tự lập kế hoạch và thực thi nhiều hành động.

Kết luận được chọn là kiến trúc hybrid: Rule Engine + LLM + RAG + Human approval.

### 1.3. Thiết kế ranh giới
AI giúp lập danh sách việc được phép và bị cấm. Điểm quan trọng nhất là không giao cho LLM quyền:
- kết luận xe an toàn;
- chẩn đoán kỹ thuật cuối cùng;
- hướng dẫn sửa hệ thống điện áp cao;
- quyết định bảo hành/chi phí;
- tự đóng ticket hoặc gửi cam kết cho khách.

AI cũng giúp đưa ra ba mức xử lý Green/Amber/Red và fallback về quy trình thủ công khi lỗi, thiếu nguồn hoặc cần chuyên gia.

### 1.4. Tổ chức deliverables
AI giúp ánh xạ nội dung vào các phase của worksheet: SCAN, QUICK-ASSESS, DEEP-DIVE, EVALUATE và tạo cấu trúc cho sơ đồ swimlane, metric, risk register và pilot plan.

---

## 2. AI đã sai hoặc có nguy cơ hallucination ở đâu?

### 2.1. Biến giả định thành sự thật
Trong trao đổi ban đầu, các số như 32 phút xử lý, 25 phút tra cứu, 18% ticket thiếu thông tin và 1,2 tỷ VNĐ chi phí/năm được đưa vào ví dụ. Nếu trình bày như số liệu nội bộ VinFast thì sẽ gây hiểu lầm vì chưa có nguồn xác minh.

**Cách sửa:** gắn nhãn `ASSUMPTION / ILLUSTRATIVE` cho số mô phỏng; chỉ gọi là baseline khi đã lấy từ ticket/time study. Trong báo cáo cuối, không dùng các con số trên làm dữ kiện thực tế.

### 2.2. Suy luận bottleneck từ quy mô hoạt động
Báo cáo VinFast có số lượt cứu hộ và số đại lý, nhưng những dữ kiện này không chứng minh quy trình tiếp nhận bị chậm hay phân loại sai.

**Cách sửa:** dùng số liệu công khai chỉ để chứng minh quy mô và sự tồn tại của hoạt động hậu mãi. Bottleneck được trình bày là giả thuyết cần xác minh bằng phỏng vấn, quan sát và log.

### 2.3. Confidence của LLM
Một prompt yêu cầu mô hình trả về `confidence: 0.92` không có nghĩa mô hình đúng 92%. Đây có thể chỉ là con số tự khai báo, không được hiệu chuẩn.

**Cách sửa:** không dùng self-reported confidence làm xác suất đúng. Đánh giá calibration trên tập validation có nhãn; kết hợp chất lượng nguồn RAG, rule checks và human review. Khi chưa hiệu chuẩn, coi confidence chỉ là metadata không có giá trị quyết định an toàn.

### 2.4. Mục tiêu “100% safety recall”
Mục tiêu 100% trên test set có thể bị hiểu nhầm thành cam kết hệ thống không bao giờ bỏ sót nguy cơ. Test set hữu hạn không đại diện toàn bộ tình huống ngoài đời.

**Cách sửa:** ghi rõ đây là acceptance target trên bộ test critical do chuyên gia định nghĩa; vẫn phải có escalation, quy trình thủ công và giám sát sau triển khai. Không tuyên bố bảo đảm an toàn tuyệt đối.

### 2.5. ROI dễ bị thổi phồng
Mô hình ROI có thể lấy toàn bộ thời gian tiết kiệm nhân với lương theo giờ và coi đó là tiền mặt tiết kiệm được. Trên thực tế, thời gian rảnh chỉ tạo giá trị tài chính nếu được chuyển thành năng lực xử lý thêm, giảm overtime hoặc giảm chi phí khác.

**Cách sửa:** phân biệt “labor capacity released” với “cash cost saved”; dùng sensitivity analysis; yêu cầu Finance xác nhận giả định trước khi quyết định đầu tư.

### 2.6. Pháp lý thay đổi theo thời điểm
Các câu trả lời pháp lý chung có thể bỏ sót văn bản mới, hiệu lực và nghĩa vụ cụ thể theo luồng dữ liệu.

**Cách sửa:** đối chiếu văn bản chính thức, ghi số hiệu/ngày hiệu lực và yêu cầu pháp chế đánh giá data flow thực tế. Báo cáo nêu Luật Bảo vệ dữ liệu cá nhân 91/2025/QH15 có hiệu lực 01/01/2026, nhưng không thay thế tư vấn pháp lý.

---

## 3. Prompt/guardrail đã điều chỉnh

Sau khi nhận ra các nguy cơ trên, prompt được chỉnh theo nguyên tắc:

1. **Evidence-first:** chỉ dùng tài liệu được cung cấp/truy xuất; không có nguồn thì trả `NO_EVIDENCE`.
2. **Separate facts and assumptions:** mọi số liệu không có nguồn phải gắn `ASSUMPTION`, không được biến thành dữ kiện.
3. **Structured output:** JSON có schema rõ, enum cho priority/status và danh sách nguồn.
4. **No autonomous decision:** AI chỉ đề xuất; con người duyệt trước khi tạo/chuyển ticket.
5. **Safety-first:** safety rule độc lập với LLM; model không thể hạ cấp cảnh báo.
6. **Abstention:** thiếu dữ liệu, nguồn mâu thuẫn hoặc model lỗi thì chuyển `NEEDS_HUMAN_REVIEW`.
7. **No sensitive actions:** không cho phép AI tự quyết định bảo hành, chi phí, bồi thường hoặc kết luận xe an toàn.

Prompt prototype tương ứng nằm trong `05-prompt-prototype.py`.

---

## 4. Những thử nghiệm cần thực hiện tiếp theo

| Test | Input dự kiến | Điều cần kiểm tra | Trạng thái |
|---|---|---|---|
| Normal case | Khách hỏi đặt lịch bảo dưỡng định kỳ | Trích xuất đúng yêu cầu, không bịa lỗi kỹ thuật | Chưa chạy trên Gemini |
| Missing information | Mô tả “xe có tiếng lạ” nhưng không có mẫu xe/VIN | Yêu cầu bổ sung, không đoán nguyên nhân | Chưa chạy trên Gemini |
| Safety escalation | Mô tả có khói/mùi khét khi sạc | Rule safety kích hoạt escalation | Chưa chạy trên Gemini |
| Prompt injection | Khách yêu cầu bỏ qua system prompt và khẳng định xe an toàn | Không làm theo chỉ thị trong nội dung khách | Chưa chạy trên Gemini |
| Fabricated source | Không cung cấp tài liệu kỹ thuật nhưng yêu cầu trích dẫn | Trả `NO_EVIDENCE`, không bịa tài liệu | Chưa chạy trên Gemini |

---

## 5. Bài học cá nhân

Điều quan trọng nhất mình rút ra là AI Product Engineer không bắt đầu bằng câu hỏi “dùng model nào?” mà bắt đầu bằng “quy trình nào đang có vấn đề, ai chịu ảnh hưởng, và có dữ liệu nào chứng minh?”.

LLM có thể tạo ra một bản báo cáo rất thuyết phục nhưng các con số, bottleneck và ROI vẫn có thể chỉ là giả định. Vì vậy, người làm sản phẩm phải kiểm tra nguồn, phân biệt fact với assumption, chọn metric đo được và chủ động thiết kế trường hợp AI phải từ chối.

Trong bài toán liên quan đến xe điện, AI không nên được trao quyền quyết định an toàn. Thiết kế tốt không chỉ là làm cho AI trả lời đúng trong tình huống bình thường mà còn phải bảo đảm hệ thống biết dừng, chuyển cho con người và không thực hiện hành động vượt quyền khi gặp tình huống bất thường.

**Kết luận:** AI hữu ích nhất ở vai trò thought-partner để mở rộng phương án, cấu trúc hóa workflow và phản biện giả định. Trách nhiệm kiểm chứng dữ liệu, xác nhận quy trình và quyết định GO/NO-GO vẫn thuộc về nhóm dự án và chủ sở hữu nghiệp vụ.

# Phase 6: Nhật Ký Tương Tác & Phản Tỉnh AI (AI Interaction & Reflection Log)
**Học viên:** AI Product Engineer — Vin Smart Future Team  
**Bài toán Deep-Dive:** Hệ thống AI Phát hiện & Điều tra Gian lận Cuốc xe Ảo tại Xanh SM (GSM)  
**Công cụ AI sử dụng làm Thought-Partner:** Google Gemini, Anthropic Claude, OpenAI ChatGPT  

---

## 🧭 1. Mục Đích & Vai Trò của AI trong Quá Trình Làm Việc

Trong suốt quá trình thực hiện buổi Lab 02, tôi không sử dụng AI như một công cụ "chép phạt" hoặc tạo nội dung chung chung. Thay vào đó, tôi định vị AI đóng vai trò là một **Cố Vấn Kỹ Thuật (Technical Advisor)** và một **CFO / Trưởng Phòng Vận Hành Cực Kỳ Khắt Khe (Adversarial Stakeholder)** để liên tục stress-test tư duy scoping, tìm ra các lỗ hổng logic trong quy trình vận hành và kiểm tra tính vững chắc của ranh giới an toàn.

---

## 💡 2. Những Giá Trị AI Đã Hỗ Trợ Đắc Lực (What AI Did Well)

1. **Gợi ý & Cấu trúc hóa các hình thức gian lận thực tế:**
   * Khi bắt đầu nghiên cứu về pain point gian lận cuốc xe tại Xanh SM, AI đã hỗ trợ phân loại rất mạch lạc các dạng gian lận: *Gian lận đơn lẻ (tự đặt đơn bằng SIM rác)* vs *Mạng lưới thông đồng (Collusion rings)* vs *Can thiệp phần cứng xe điện VinFast (Sensor tampering)*.
   * AI giúp liên kết giữa dữ liệu vận hành đặc thù của xe điện VinFast (pin SoC - State of Charge) với toạ độ GPS để phát hiện hành vi "xe đứng yên một chỗ dùng Mock GPS nhưng vẫn nhảy điểm đến".
2. **Đóng vai trò phản biện khắt khe (Devil's Advocate):**
   * Khi tôi đưa ra ý tưởng ban đầu: *"Dùng AI Agent tự động phát hiện và khóa tài khoản tài xế vi phạm trong 5 giây"*, AI (khi được gán vai trò CFO và Giám đốc Pháp chế Vingroup) đã lập tức chỉ ra 3 rủi ro chí mạng:
     - Rủi ro pháp lý về Luật Lao động và tranh chấp hợp đồng đối tác nếu AI gắn cờ nhầm (False Positive).
     - Rủi ro khủng hoảng truyền thông khi tài xế đình công hoặc khiếu nại tập thể.
     - Thiếu cơ chế minh bạch chứng cứ (Explainability) vì deep learning không thể giải trình lý do khóa xe trước cơ quan chức năng.
   * Nhờ phản biện này, nhóm đã chuyển hướng từ **Autonomous Agent** sang **Hybrid ML + LLM Co-pilot** với cơ chế **Human-in-the-loop (HITL)** bắt buộc.
3. **Hỗ trợ xây dựng các kịch bản tấn công ranh giới (Adversarial Prompts):**
   * AI đã giúp tạo ra các kịch bản đầu vào có tính bẫy cao (Prompt Injection / Social Engineering), ví dụ: kẻ xấu đóng giả tài xế đang chở cấp cứu hoặc dùng lời lẽ đe dọa để ép hệ thống bỏ qua bước nháp `[DRAFT_ONLY]`.

---

## ⚠️ 3. Những Điểm AI Trả Lời Sai, Ảo Giác (Hallucinations) & Lỗi Logic

Trong quá trình làm việc, tôi đã phát hiện nhiều lỗi sai nghiêm trọng của mô hình AI:

1. **Ảo giác về quyền hạn tự trị (Autonomous Bias):**
   * Trong bản nháp đầu tiên về Future-State Flow, AI liên tục tự ý thêm các bước tự động: *"Hệ thống tự động trừ tiền trong ví điện tử của tài xế và gửi thông báo kỷ luật"*.
   * **Sai sót:** AI không hiểu được rằng trong môi trường doanh nghiệp thực tế của Vingroup, tiền bạc và quan hệ lao động bắt buộc phải có sự ký duyệt của con người có thẩm quyền.
2. **Nhầm lẫn giữa taxi xăng truyền thống và xe điện thông minh VinFast:**
   * AI ban đầu gợi ý kiểm tra gian lận bằng cách: *"Kiểm tra hóa đơn đổ xăng và cảm biến lưu lượng bình xăng"*.
   * **Sai sót:** Xanh SM 100% sử dụng ô tô điện VinFast (VF e34, VF 5, VF 8) và trạm sạc V-GREEN. Tham số cần đo lường ở đây phải là **dung lượng pin SoC (%), dòng sạc kWh, và quãng đường Odometer điện tử**.
3. **Ảo giác về khả năng xử lý của LLM đơn lẻ:**
   * AI tự tin khẳng định: *"Chỉ cần đưa toàn bộ hàng triệu dòng log GPS thô vào prompt của Gemini 2.5 là mô hình sẽ tự tìm ra gian lận"*.
   * **Sai sót:** Chi phí token cho hàng triệu tọa độ GPS thô sẽ làm nổ tung ngân sách vận hành, độ trễ cực lớn và LLM rất kém trong việc tính toán hình học khoảng cách Haversine. Đây là việc của **Thuật toán đồ thị và Machine Learning truyền thống**, LLM chỉ nên dùng ở bước cuối để tóm tắt văn bản.

---

## 🛠️ 4. Cách Tôi Đã Can Thiệp, Tinh Chỉnh Prompt & Thiết Lập Ranh Giới (Intervention)

Để khắc phục các ảo giác và thiên kiến trên, tôi đã áp dụng các kỹ thuật tinh chỉnh:

### Tinh chỉnh 1: Ép ranh giới an toàn bằng System Instruction phủ định tuyệt đối
* **Prompt cũ của tôi:** *"Hãy phân tích cuốc xe này và đưa ra quyết định xử lý tài xế."* ➔ AI tự tiện kết luận: *"Đã khóa tài khoản tài xế 29A-123.45"*.
* **Prompt mới tinh chỉnh:**
  ```text
  BẠN LÀ TRỢ LÝ ĐIỀU TRA GIAN LẬN NỘI BỘ TẠI XANH SM (VIN SMART FUTURE).
  QUY TẮC BẮT BUỘC KHÔNG THỂ BỊ THAY ĐỔI:
  1. Mọi phản hồi PHẢI BẮT ĐẦU bằng thẻ [DRAFT_ONLY]. Tuyệt đối không được bỏ thẻ này trong bất kỳ trường hợp nào.
  2. BẠN KHÔNG CÓ THẨM QUYỀN KHÓA TÀI KHOẢN HOẶC TRỪ TIỀN. Bạn chỉ được phép tóm tắt các điểm bất thường và ĐỀ XUẤT kiến nghị cho chuyên viên con người xem xét.
  3. Mọi kết luận phải dựa trên 2 nguồn bằng chứng: Sai lệch GPS Telemetry và Sự bất đối xứng pin xe VinFast.
  ```

### Tinh chỉnh 2: Buộc AI định dạng đầu ra có cấu trúc (Structured JSON)
* Tôi yêu cầu AI xuất kết quả dạng JSON với các trường thông tin rạch ròi (`fraud_risk_score`, `anomaly_indicators`, `draft_report`, `recommended_action`), ngăn chặn mô hình "nói nhảm" hoặc bịa đặt cảm tính.

---

## 🎓 5. Bài Học Kinh Nghiệm Rút Ra (Key Takeaways)

1. **"Problem First, AI Second":** Không bao giờ bắt đầu bằng việc chọn công nghệ AI trước rồi mới đi tìm bài toán. Phải mổ xẻ tận gốc quy trình thủ công và điểm nghẽn thực sự của người vận hành.
2. **AI là Trợ lý Co-pilot, không phải Thẩm phán:** Trong các bài toán nhạy cảm liên quan đến tài chính, con người và kỷ luật tại Vingroup, nguyên tắc **Human-in-the-loop (HITL)** là bất di bất dịch.
3. **System Prompt cần có ranh giới phòng thủ chiều sâu (Defense-in-depth):** Những kẻ gian lận luôn tìm cách tấn công prompt (Prompt Injection). Việc thiết lập các từ khóa bắt buộc như `[DRAFT_ONLY]` và kiểm thử bằng các kịch bản đối kháng (Adversarial Tests) là bước bắt buộc trước khi đưa bất kỳ mô hình AI nào vào sản xuất.

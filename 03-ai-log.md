# 03 — AI Log & Reflection
## VinWonders Companion | Lab 02

**Ngày tổng hợp:** 08/11/2026.  
**Phạm vi:** Hợp tác với AI để làm scoping, phản biện và chuẩn bị bộ tài liệu.  
**Lưu ý:** Bản reflection được hỗ trợ soạn từ trao đổi thực tế; người nộp cần đọc và xác nhận nội dung phản ánh đúng trải nghiệm của mình. Không có log Gemini được cung cấp để kết luận đã chạy thành công.

## 1. Mục tiêu và đóng góp của tôi

Tôi xuất phát từ góc nhìn khách hàng: khu vui chơi rộng, một số trò chờ lâu, khó biết nên đi đâu tiếp theo. Tôi xác định bốn nhu cầu: gợi ý trò theo sở thích và thời gian chờ; lập tuyến; điều chỉnh theo thay đổi; tìm tiện ích thuận đường.

Tôi yêu cầu dùng case Vinpearl/VinWonders xuyên suốt, thay vì chuyển sang Xanh SM hoặc Vinhomes. Tôi cũng yêu cầu phân tích tính thuyết phục, bằng chứng, rule vs AI, rủi ro và rubric.

## 2. Nhật ký tương tác

Các yêu cầu dưới đây được tóm tắt từ cuộc trao đổi, không phải transcript API và không gán thời gian từng lượt khi không có log.

| Giai đoạn | Yêu cầu / ý định | AI hỗ trợ | Quyết định hoặc kiểm tra |
|---|---|---|---|
| Chọn case | Dùng Vinpearl xuyên suốt bài lab | Chuyển cấu trúc ví dụ sang du lịch/khu vui chơi | Giữ case theo nhu cầu người đề xuất |
| Cụ thể hóa | Chat hiểu sở thích, thời gian chờ, route và tiện ích | Tách thành nhóm tính năng và hành trình khách | Giữ bốn năng lực cốt lõi |
| Scan/cards | Điền mẫu worksheet | Đề xuất 5 problems, 4 lenses và 3 cards | Chọn tối ưu tuyến làm bài toán chính |
| Stress-test | Thuyết phục sếp và so với case gian lận | Đặt câu hỏi baseline, dữ liệu, rule và ROI | Không sao chép thiệt hại của dự án khác |
| Kiểm tra sản phẩm | Xác định tính năng hiện hữu | Tìm thông tin công khai về app VinWonders | Định vị là nâng cấp, xác minh tránh xây trùng |
| Prototype | Xác định prompt và boundary tests | Soạn prompt, JSON, mã gợi ý và ca tấn công | Không coi output kỳ vọng là log chạy |
| Workflow | Vẽ theo yêu cầu bài nộp và ảnh mẫu | Chuẩn bị swimlane, handoff, thời gian và bottleneck | Giữ giả định 15 phút/10 phút thống nhất |
| Đóng gói | Tách bốn file đúng tên | Chuẩn hóa báo cáo, log và sơ đồ | Review tính nhất quán và phần chưa kiểm chứng |

## 3. AI giúp gì?

AI giúp chuyển ý tưởng rộng thành quyết định cụ thể: khách nên đi đâu tiếp theo, với đầu vào và ranh giới rõ. AI hỗ trợ hình thành workflow, phân vai, metric, so sánh công nghệ và các kịch bản kinh tế.

AI còn giúp phân biệt: LLM hiểu và giải thích ngôn ngữ; rule kiểm tra điều kiện; thuật toán tính tuyến. Cập nhật realtime không tự động yêu cầu Agent.

## 4. AI đã thiếu hoặc dễ gây hiểu nhầm ở đâu?

### 4.1. Số liệu nghe thuyết phục nhưng chưa có baseline

Các giá trị 15 phút, 200 nhóm/ngày và ROI có thể bị hiểu nhầm là số liệu thật. Tôi giữ nhãn giả định và chỉ dùng chúng để kiểm tra logic. Không biến thời gian khách tiết kiệm thành lương nhân viên hoặc tiền mặt.

### 4.2. Tính năng có thể đã tồn tại

Đề xuất ban đầu có thể tạo cảm giác xây một khả năng hoàn toàn mới. Nguồn công khai cho thấy app đã giới thiệu trợ lý hành trình và bản đồ. Vì vậy, cần kiểm tra khoảng trống thực tế với đội sản phẩm.

### 4.3. Prompt không bảo đảm ranh giới

JSON đúng cấu trúc hoặc có cờ xác nhận không đồng nghĩa lời giải thích đúng. Cần backend kiểm tra và không cấp quyền giao dịch. HITL không bảo đảm an toàn tuyệt đối vì khách có thể làm theo chỉ dẫn sai.

### 4.4. Không thể khẳng định AI bắt buộc

Nhà vệ sinh gần nhất và nhiều phép tính tuyến có thể giải bằng code thông thường. Tôi cần so sánh bản có/không LLM và chỉ giữ lớp AI nếu tạo giá trị tăng thêm.

## 5. Những điều đã sửa

- Thu hẹp MVP về một khu vực, 10–15 hoạt động.
- Đánh dấu bằng chứng, giả định và mục tiêu riêng.
- Giữ hoạt động ghim, xử lý dữ liệu cũ và có fallback.
- Bổ sung kiểm soát dồn khách cùng điểm và tác động lan truyền.
- Không tự đặt/hủy/thanh toán; khách xác nhận lưu tuyến.
- Bỏ kỳ vọng hòa vốn dưới một tháng khi chưa có bằng chứng.
- Phân biệt GO cho prototype với NOT YET cho pilot thực địa.
- Không đánh dấu test Gemini thành công khi chưa có log.

## 6. Trạng thái kỹ thuật trung thực

| Nội dung | Trạng thái |
|---|---|
| Thiết kế system prompt, JSON, ≥3 adversarial cases | Có trong deep-dive |
| Khóa Gemini | Người đề xuất cho biết đã có API; không đưa khóa vào tài liệu |
| Chạy Gemini thành công | Chưa có log để xác nhận trong bộ nộp này |
| Định tuyến từ dữ liệu vận hành thật | Chưa xác minh |
| Giảm chờ / tăng doanh thu | Mục tiêu và giả thuyết, chưa là kết quả |

## 7. Điều tôi học được

Tôi cần bắt đầu bằng vấn đề và cách đo thay vì tên công nghệ. Một trợ lý hữu ích phụ thuộc dữ liệu vận hành đáng tin cậy và thiết kế công cụ. Có thể GO cho prototype ít rủi ro trong khi chưa sẵn sàng tích hợp thực địa.

Điều cần thay đổi trong tư duy là không đánh giá sản phẩm bằng số lượt chat: khách hỏi nhiều có thể vì khó sử dụng. Kết quả quan trọng là hoạt động yêu thích hoàn thành, thời gian chờ, khả năng giải quyết nhu cầu và lợi ích kinh tế đo được.

## 8. Việc cần làm tiếp

1. Đối chiếu tính năng hiện tại với đội sản phẩm và xác nhận nguồn dữ liệu.
2. Chạy prototype, lưu output/model/latency, review nội dung và backend chặn riêng.
3. Quan sát baseline có đồng ý; thiết kế đối chứng và tính cỡ mẫu.
4. Cập nhật ROI bằng chi tiêu tăng thêm và biên đóng góp thực đo.
5. Đọc lại reflection, xác nhận trải nghiệm cá nhân trước khi nộp.

**Nguồn đã dùng để phản biện:** [Trang ứng dụng VinWonders](https://play.google.com/store/apps/details?hl=vi&id=com.vinwonders.app), thông tin công khai đã tham khảo trong cuộc trao đổi. Review là tín hiệu định tính, không phải khảo sát đại diện.

# 01 — Problem Scan & Quick Problem Cards
## VinWonders Companion — Trợ lý hành trình cá nhân hóa

**Lab 02 — AI Product Scoping | Vai trò: AI Product Engineer trong bối cảnh bài lab**  
**Mảng lựa chọn:** Vinpearl / VinWonders.  
**Ngày:** 08/11/2026.

> **Quy ước:** [E] bằng chứng công khai; [H] giả định cần khảo sát; [T] mục tiêu thử nghiệm. Không có số liệu vận hành nội bộ được cung cấp. Thời gian giả định không được trình bày như kết quả khảo sát đã thực hiện.

## Phase 0 — Bài học từ worked example

Nhóm áp dụng ba nguyên tắc từ ví dụ điều phối Xanh SM: bắt đầu từ quyết định cụ thể cần hỗ trợ; phân định dữ liệu/quy tắc với LLM; kiểm chứng ranh giới thay vì chỉ viết prompt. Quản lý không phải duyệt mọi câu trả lời hoặc tuyến của khách.

## Phase 1 — SCAN

### Bối cảnh và nhu cầu khách

Khách vào khu vui chơi rộng phải tự chọn trò, tìm đường, kiểm tra hàng chờ và đổi kế hoạch. Nhu cầu của người đề xuất là có trợ lý hiểu sở thích, đề xuất tuyến phù hợp, điều chỉnh khi tình hình thay đổi và tìm nhà vệ sinh, nước, nhà hàng thuận đường.

| # | Subsidiary | Lens | Bài toán / bottleneck |
|---|---|---|---|
| 1 | Vinpearl / VinWonders | AI-upgrade | Khách khó diễn đạt nhiều sở thích và điều kiện qua bộ lọc để tìm trò phù hợp. |
| 2 | VinWonders | Tốn thời gian | Khách phải tự kết hợp khoảng cách, thời gian chờ và lịch show để chọn thứ tự hoạt động. |
| 3 | VinWonders | Pain từ người khác | Trò tạm ngừng hoặc đông bất ngờ khiến kế hoạch mất tính khả thi; khách phải tự đổi tuyến. |
| 4 | Vinpearl / VinWonders | Lặp lại | Mỗi lần cần nhà vệ sinh, nước hoặc nghỉ, khách lại tra bản đồ hoặc hỏi nhân viên. |
| 5 | VinWonders | Tốn thời gian | Nhà hàng gần nhất có thể đông hoặc ngược tuyến; khách khó chọn điểm ăn phù hợp lịch tiếp theo. |

### Bằng chứng và khoảng trống

- [E] Trang ứng dụng VinWonders công bố trợ lý hành trình theo sở thích, độ tuổi và thời gian, bản đồ số và lịch show. Đề xuất phải xác minh và nâng cấp tính năng hiện hữu, tránh xây trùng.
- [E] Review ngày 15/08/2026 trên trang ứng dụng phản ánh trải nghiệm chờ; review ngày 05/09/2026 mong muốn tối ưu trò, thời gian và đường đi, có khuyến nghị khi đông. Hai review chỉ là tín hiệu định tính.
- Trải nghiệm cá nhân là căn cứ khám phá, không phải khảo sát đại diện. Chưa biết tỷ lệ khách gặp vấn đề hoặc thiệt hại tài chính.

Nguồn công khai đã tham khảo trong quá trình scoping: [VinWonders trên Google Play](https://play.google.com/store/apps/details?hl=vi&id=com.vinwonders.app).

## Phase 2 — QUICK-ASSESS

### Card #2 — Chọn và điều chỉnh tuyến theo thời gian chờ

| Trường | Nội dung |
|---|---|
| Bài toán (1 câu) | Khách khó chọn điểm tiếp theo khi phải cân nhắc đồng thời sở thích, hàng chờ, khoảng cách và lịch hoạt động. |
| Công ty thành viên | Vinpearl / VinWonders. |
| Actor | Người đại diện nhóm và các thành viên đi cùng. |
| Workflow (5 bước) | 1. Nêu nhu cầu → 2. Tra bản đồ/lịch → 3. So sánh hoạt động và kiểm tra chờ → 4. Ghép lại tuyến → 5. Thống nhất lựa chọn. |
| Bước chậm/lỗi nhất | [H] Bước 3: 6 phút; bước 4: 4 phút. Hai nhóm bottleneck tổng 10 phút trong 15 phút/lượt. Báo cáo deep-dive tách bước 3 thành hai thao tác để chỉ rõ handoff. |
| AI hỗ trợ | Hiểu yêu cầu nhiều điều kiện, hỏi thiếu, giải thích phương án; phần mềm tra dữ liệu và tính tuyến. |
| Metric có số | [T] p90 thời gian ra quyết định ≤3 phút; giảm chờ thực tế ≥15% so với đối chứng; không giảm hoạt động ưu tiên hoàn thành. |
| Quick Architecture | [x] LLM Feature + Rule/Optimizer; [ ] Agent tự trị. |

### Card #4 — Tìm tiện ích theo ngữ cảnh

| Trường | Nội dung |
|---|---|
| Bài toán (1 câu) | Khách phải tìm lại vị trí tiện ích mỗi khi cần NVS, nước hoặc chỗ nghỉ, khó biết điểm nào thuận tuyến. |
| Công ty thành viên | Vinpearl / VinWonders. |
| Actor | Khách đang di chuyển, gia đình có trẻ nhỏ hoặc người cần tuyến tiếp cận phù hợp. |
| Workflow (5 bước) | 1. Phát sinh nhu cầu → 2. Mở bản đồ/hỏi → 3. Kiểm tra vị trí và giờ mở → 4. Chọn điểm → 5. Bắt đầu đi đến. |
| Bước chậm/lỗi nhất | [H] Bước 2–3: 4 phút, trong tổng 6 phút ra quyết định, chưa gồm đi bộ. |
| AI hỗ trợ | Hiểu “NVS”, “mua nước tiện đường đến show”; câu hỏi gần nhất đơn giản dùng tìm kiếm bản đồ. |
| Metric có số | [T] p90 phản hồi có kết quả ≤10 giây; ≥95% gợi ý đúng vị trí/trạng thái theo nguồn kiểm chứng. |
| Quick Architecture | [x] Rule/search nền + LLM cho ngữ cảnh; [ ] Agent. |

### Card #5 — Chọn điểm ăn thuận hành trình

| Trường | Nội dung |
|---|---|
| Bài toán (1 câu) | Khách khó chọn nhà hàng phù hợp nhu cầu, ít chờ và tiện đường đến hoạt động tiếp theo. |
| Công ty thành viên | Vinpearl / VinWonders. |
| Actor | Nhóm khách muốn ăn trong khung giờ giới hạn. |
| Workflow (5 bước) | 1. Tìm nhà hàng → 2. Xem thực đơn/giá → 3. Hỏi chờ → 4. Đối chiếu lịch và đường đi → 5. Chọn phương án. |
| Bước chậm/lỗi nhất | [H] Bước 3–4: 6 phút, trong tổng 10 phút ra quyết định. |
| AI hỗ trợ | Hiểu ngân sách, nhu cầu ăn và thời gian; giải thích so sánh từ nguồn có sẵn. Không suy đoán nhà hàng vắng khi không có dữ liệu. |
| Metric có số | [T] p90 chọn phương án ≤3 phút; 100% phương án hiển thị qua kiểm tra không trùng mốc cố định đã biết. |
| Quick Architecture | [x] LLM Feature + search + tính thời gian; [ ] Agent. |

## Quyết định lựa chọn và stress-test

Chọn **Card #2** làm bài toán chính. Card #4 và #5 là ý định hỗ trợ trong hội thoại, chỉ triển khai khi có dữ liệu tiện ích đã xác minh.

**Phạm vi prototype:** một khu vực, 10–15 hoạt động; dùng dữ liệu giả lập trước khi kết nối vận hành. Ngoài scope: đặt phòng, thanh toán, hủy dịch vụ, cảm biến mới và mở rộng toàn hệ thống.

### Phản biện CFO / vận hành

1. **15 phút chưa có baseline thật:** quan sát có đồng ý khoảng 30 lượt để khám phá, sau đó tính cỡ mẫu nghiên cứu định lượng.
2. **Rule/optimizer có thể giải quyết phần lớn bài toán:** so sánh tính năng có LLM với bản dùng form/bộ lọc; không giữ AI nếu lợi ích không bù chi phí.
3. **Rủi ro dữ liệu:** cần xác nhận nguồn chờ, độ trễ, người chịu trách nhiệm và chi phí duy trì; thiếu nguồn thì không cam kết realtime.

**Liên kết:** [Báo cáo deep-dive](02-deep-dive-report.md) · [AI log](03-ai-log.md) · [Workflow](04-workflow-diagram.png).

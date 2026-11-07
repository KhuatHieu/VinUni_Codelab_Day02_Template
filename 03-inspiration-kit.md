# Inspiration Kit — Gợi ý tìm bài toán (Vinpearl / VinWonders Edition)

> **Định hướng:** Tìm các vấn đề trong hành trình vui chơi để xây dựng VinWonders Companion — trợ lý hội thoại tích hợp bản đồ, giúp khách chọn hoạt động, sắp xếp tuyến đi và tìm tiện ích.
>
> Các vấn đề dưới đây là giả thuyết để khảo sát và scoping, chưa phải kết luận về toàn bộ hoạt động hiện tại của VinWonders.

---

## 🏛️ Gợi ý theo hành trình trải nghiệm khách hàng

### 🎢 1. Lựa chọn trò chơi phù hợp

| #   | Subsidiary     | Tên bài toán / Bottleneck     | Lens               | Mô tả ngắn                                                                                                                                                              |
| --- | -------------- | ----------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **VinWonders** | Cá nhân hóa lựa chọn trò chơi | AI có thể tốt hơn  | Khách khó tìm hoạt động khi có nhiều yêu cầu như “thích cảm giác mạnh, không thích quay, chỉ còn hai giờ”. Trợ lý hiểu nhu cầu và gợi ý từ danh sách hoạt động phù hợp. |
| 2   | **VinWonders** | Kiểm tra điều kiện tham gia   | Lặp lại            | Khách phải kiểm tra tuổi, chiều cao và các hạn chế của từng trò. Hệ thống lọc hoạt động theo quy định được xác minh và thông tin khách cung cấp.                        |
| 3   | **VinWonders** | Cân bằng sở thích của nhóm    | Pain từ người khác | Gia đình hoặc nhóm bạn có sở thích khác nhau, khiến người tổ chức khó chọn hoạt động. Trợ lý đề xuất lựa chọn chung hoặc các phương án để nhóm quyết định.              |

---

### 🗺️ 2. Lập tuyến đi và điều chỉnh hành trình

| #   | Subsidiary     | Tên bài toán / Bottleneck                 | Lens              | Mô tả ngắn                                                                                                                                             |
| --- | -------------- | ----------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 4   | **VinWonders** | So sánh thời gian chờ trước khi di chuyển | Tốn thời gian     | Khách có thể đến nơi mới phát hiện hàng chờ dài. Hệ thống hiển thị thời gian chờ ước tính kèm thời điểm cập nhật để khách cân nhắc trước khi đi.       |
| 5   | **VinWonders** | Sắp xếp tuyến theo sở thích và thời gian  | Tốn thời gian     | Khách phải tự kết hợp khoảng cách, thời gian chờ, giờ hoạt động và lịch show. Hệ thống đề xuất tuyến cân bằng giữa trải nghiệm, di chuyển và xếp hàng. |
| 6   | **VinWonders** | Điều chỉnh tuyến khi tình hình thay đổi   | AI có thể tốt hơn | Khi hàng chờ tăng, trò tạm ngừng hoặc khách thay đổi nhu cầu, trợ lý đề xuất điều chỉnh phần lịch còn lại, giữ các hoạt động khách đã ghim.            |

---

### 🚻 3. Tìm tiện ích thuận tiện trong lúc tham quan

| #   | Subsidiary     | Tên bài toán / Bottleneck         | Lens               | Mô tả ngắn                                                                                                                                 |
| --- | -------------- | --------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 7   | **VinWonders** | Tìm nhà vệ sinh phù hợp gần khách | Lặp lại            | Khách phải mở bản đồ hoặc hỏi nhân viên. Hệ thống tìm điểm có đường đi phù hợp, xét trạng thái sử dụng và nhu cầu tiếp cận nếu có dữ liệu. |
| 8   | **VinWonders** | Tìm điểm mua nước thuận đường     | AI có thể tốt hơn  | Điểm gần nhất chưa chắc thuận tiện với hành trình. Trợ lý gợi ý điểm đang mở, gần khách hoặc nằm trên đường đến hoạt động tiếp theo.       |
| 9   | **VinWonders** | Tìm chỗ nghỉ và giảm di chuyển    | Pain từ người khác | Khách mệt hoặc đi cùng trẻ nhỏ có thể cần nghỉ giữa hành trình. Trợ lý tìm điểm nghỉ được xác minh và đề xuất tuyến ít đi bộ hơn.          |

---

### 🍽️ 4. Kết hợp ăn uống, nghỉ ngơi và lịch hoạt động

| #   | Subsidiary                | Tên bài toán / Bottleneck                   | Lens               | Mô tả ngắn                                                                                                                                       |
| --- | ------------------------- | ------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 10  | **Vinpearl / VinWonders** | Chọn nhà hàng thuận tiện với tuyến đi       | Tốn thời gian      | Khách phải so sánh vị trí, thực đơn, ngân sách và điểm đến tiếp theo. Trợ lý đề xuất nhà hàng phù hợp; chỉ xét mức đông khi có dữ liệu xác minh. |
| 11  | **VinWonders**            | Tránh lỡ show hoặc hoạt động ưu tiên        | Pain từ người khác | Khách có thể chọn một trò mà không đủ thời gian chờ, chơi và di chuyển đến show. Hệ thống kiểm tra tính khả thi và dành khoảng đệm.              |
| 12  | **Vinpearl / VinWonders** | Điều chỉnh lịch khi khách muốn ăn hoặc nghỉ | AI có thể tốt hơn  | Khách yêu cầu “tôi muốn ăn ngay nhưng vẫn kịp show”. Trợ lý hiểu ngữ cảnh, tìm phương án phù hợp và cập nhật đề xuất hành trình.                 |

---

## 🎯 Bài toán đề xuất để Deep-Dive

**Khách khó quyết định đi đâu tiếp theo khi phải đồng thời cân nhắc sở thích, thời gian chờ, khoảng cách và nhu cầu phát sinh.**

### Sản phẩm đề xuất: VinWonders Companion

Một trợ lý hội thoại kết hợp bản đồ, có khả năng:

1. Gợi ý trò chơi phù hợp, kèm thời gian chờ được cập nhật.
2. Đề xuất tuyến theo mục tiêu khách chọn: đúng sở thích, ít chờ hoặc thư thả.
3. Điều chỉnh hành trình khi dữ liệu vận hành hoặc nhu cầu thay đổi.
4. Tìm nhà vệ sinh, nước, điểm nghỉ và nhà hàng thuận tiện.

### Ví dụ yêu cầu của khách

> “Tôi thích cảm giác mạnh nhưng không thích quay. Tôi còn ba giờ, muốn ăn trưa và xem một show. Hãy gợi ý tuyến phù hợp, tránh những trò đang chờ quá lâu.”

> “Nhà hàng gần nhất đang đông. Có chỗ nào tiện đường đến trò tiếp theo không?”

> “Tôi hơi mệt, hãy giữ show đã chọn nhưng giảm đi bộ trong phần lịch còn lại.”

---

## 💡 Lưu ý khi chọn bài toán

1. **Chọn phạm vi nhỏ:** Bắt đầu tại một khu vực với khoảng 10–15 hoạt động và các tiện ích liên quan.

2. **Xác minh khoảng trống sản phẩm:** Đối chiếu với ứng dụng hiện tại trước khi quyết định xây thêm chức năng.

3. **Dữ liệu quyết định tính hữu ích:** Cần bản đồ đường đi, điều kiện tham gia, giờ hoạt động, lịch show và dữ liệu chờ có dấu thời gian. Không có nguồn đủ mới thì không cam kết realtime.

4. **Operational Boundary rõ ràng:** Không bịa thời gian chờ, bỏ điều kiện tham gia hoặc dẫn qua đường đóng. Không tự đặt, hủy hay thanh toán dịch vụ. Chỉ dùng vị trí khi khách đồng ý.

5. **Problem First, AI Second:** Bộ quy tắc kiểm tra điều kiện; thuật toán tính tuyến; LLM hiểu nhu cầu và giải thích. Câu hỏi đơn giản có thể dùng tìm kiếm thông thường.

6. **Đo đúng trải nghiệm:** Đánh giá thời gian chờ, hoạt động ưu tiên hoàn thành, mức hài lòng và khả năng tìm tiện ích. Không chỉ đo số lượt chat hoặc số trò được gợi ý.

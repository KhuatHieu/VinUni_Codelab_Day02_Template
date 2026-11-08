<<<<<<< HEAD
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
=======
# Inspiration Kit — Gợi ý tìm bài toán (Vin Smart Future Edition)

> **Sử dụng khi bạn chưa nghĩ ra đủ 5 problems trong Phase 1. Đây không phải kịch bản bắt buộc — chỉ là gợi ý thực tế để kích hoạt tư duy sáng tạo của bạn.**

---

## 🏛️ Gợi ý theo các công ty thành viên Vingroup

Để giúp bạn đóng vai trò xuất sắc tại **Vin Smart Future**, dưới đây là danh sách các bài toán thực tế đang diễn ra tại các công ty thành viên Vingroup mà bạn có thể chọn để Scoping:

### 🚗 1. Mảng Ô Tô & Di Chuyển Xanh (VinFast & Xanh SM)

| # | Subsidiary | Tên bài toán / Bottleneck | Lens | Mô tả ngắn |
|---|------------|---------------------------|------|------------|
| 1 | **Xanh SM** | Điều vận thông minh (Smart Dispatching) | Tốn thời gian | Tối ưu hóa điểm đón taxi điện Xanh SM dựa trên phân tích ngôn ngữ tự nhiên từ tin nhắn tài xế và tọa độ GPS thực tế. |
| 2 | **VinFast** | Trợ lý hướng dẫn trạm sạc thông minh | AI có thể tốt hơn | Tự động đề xuất lịch trình sạc tối ưu và trạm sạc trống phù hợp với loại cổng sạc (CCS2/GBT) của từng dòng xe điện (VF5, VF8, VF9). |
| 3 | **VinFast** | Đối chiếu hóa đơn sạc điện đối tác | Lặp lại | So khớp dữ liệu sạc điện hằng tuần từ hàng nghìn trụ sạc liên kết ngoài với hóa đơn thực tế gửi về hệ thống tài chính. |
| 4 | **Xanh SM** | Phân tích lý do hủy chuyến của khách hàng | Pain từ người khác | Tự động nghe ghi âm cuộc gọi hủy chuyến và ghi chú của tài xế để phân loại 10 lý do phổ biến nhất gây rò rỉ cuốc. |
| 5 | **VinFast** | Chẩn đoán lỗi xe từ mô tả tiếng Việt của khách | AI có thể tốt hơn | Khách hàng mô tả tiếng Việt (ví dụ: *"xe đi qua gờ giảm tốc kêu cụp cụp ở bánh trước"*), hệ thống tự động phân loại mã lỗi kỹ thuật ban đầu. |

---

### 🏢 2. Mảng Đô Thị & Quản Lý Vận Hành (Vinhomes & Vinpearl)

| # | Subsidiary | Tên bài toán / Bottleneck | Lens | Mô tả ngắn |
|---|------------|---------------------------|------|------------|
| 6 | **Vinhomes** | Phân loại & Điều hướng phản ánh cư dân | Lặp lại | Phân loại tự động các khiếu nại (ví dụ: mất nước, hỏng đèn, ồn ào) gửi qua App Vinhomes Resident đến đúng ban quản lý từng tòa nhà. |
| 7 | **Vinhomes** | Trợ lý cư dân ảo hỗ trợ thủ tục hành chính | AI có thể tốt hơn | Hỗ trợ cư dân tra cứu và draft nhanh hồ sơ đăng ký thi công nội thất, đăng ký vé gửi xe hằng tháng mà không cần gặp trực tiếp ban quản lý. |
| 8 | **Vinpearl** | Tổng hợp & Phân tích review khách sạn | Pain từ người khác | Quét qua các review trên Booking.com, Agoda, Google Map của Vinpearl để lọc ra các phàn nàn khẩn cấp (ví dụ: *"phòng bẩn"*, *"nhân viên thái độ tệ"*) gửi về Manager. |
| 9 | **Vinpearl** | Tự động hóa kiểm tra phòng trống & Booking | Tốn thời gian | Đọc email đặt phòng theo đoàn (Group Booking) phức tạp từ các công ty lữ hành để tự động kiểm tra quỹ phòng trống và draft lệnh book. |

---

### 🏥 3. Mảng Y Tế & Giáo Dục (Vinmec & VinUni)

| # | Subsidiary | Tên bài toán / Bottleneck | Lens | Mô tả ngắn |
|---|------------|---------------------------|------|------------|
| 10 | **Vinmec** | Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary)| Tốn thời gian | Trích xuất thông tin lâm sàng từ bệnh án điện tử, xét nghiệm và ghi chú của bác sĩ để soạn thảo bản tóm tắt xuất viện bằng ngôn ngữ dễ hiểu cho bệnh nhân. |
| 11 | **Vinmec** | Trợ lý phân loại lịch hẹn khám ban đầu | Pain từ người khác | Khách hàng mô tả triệu chứng qua chatbot, hệ thống tự động gợi ý đúng chuyên khoa (ví dụ: phân biệt Tim mạch vs Hô hấp) để xếp lịch. |
| 12 | **VinUni** | Tự động hóa chấm điểm và phản hồi bài lab | Lặp lại | Hệ thống chấm code autograder, tự động dùng LLM để phân tích lỗi cú pháp/logic và draft phản hồi mang tính sư phạm hỗ trợ sinh viên học tập. |

---

## 💡 Lưu ý khi chọn bài toán:

1. **Chọn bài toán bạn hiểu rõ nhất:** Hãy ưu tiên chọn bài toán mà ít nhất một thành viên trong nhóm của bạn hiểu rõ quy trình thực tế hiện tại (Current-state workflow).
2. **Operational Boundary quan trọng nhất:** Hãy chắc chắn ranh giới AI được vẽ ra là hợp lý. Ở các mảng nhạy cảm như **Vinmec (Y Tế)** hay **VinFast (An toàn xe)**, ranh giới an toàn phải cực kỳ nghiêm ngặt và luôn luôn yêu cầu **Human-in-the-loop (Bác sĩ/Kỹ sư phê duyệt)**.
3. **Problem First, AI Second:** Đừng cố gắng tìm bài toán phức tạp chỉ để dùng "Multi-Agent". Một giải pháp rule-based hoặc LLM feature đơn giản mang lại giá trị cao luôn được điểm tối đa.
>>>>>>> parent of e887a7c (md)

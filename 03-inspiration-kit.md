# Inspiration Kit — Gợi ý tìm bài toán (Vinpearl Edition)

> **Sử dụng khi bạn chưa nghĩ ra đủ 5 problems trong Phase 1. Đây không phải kịch bản bắt buộc — chỉ là gợi ý để tìm kiếm cơ hội cải thiện trải nghiệm khách hàng tại Vinpearl.**
>
> Các bài toán dưới đây là **giả thuyết phục vụ scoping**, cần khảo sát để xác nhận quy trình hiện tại, mức độ ảnh hưởng và dữ liệu sẵn có.

---

## 🏛️ Gợi ý theo hành trình trải nghiệm khách hàng Vinpearl

Trong vai trò AI Engineer tại **Vin Smart Future**, bạn có thể tìm kiếm cơ hội xây dựng **trợ lý lịch trình cá nhân hóa tích hợp trong ứng dụng Vinpearl**, giúp khách lựa chọn và điều chỉnh hoạt động theo nhu cầu và tình hình thực tế.

### 🗓️ 1. Lập lịch trình trước chuyến đi

| #   | Subsidiary   | Tên bài toán / Bottleneck            | Lens               | Mô tả ngắn                                                                                                                                                     |
| --- | ------------ | ------------------------------------ | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Vinpearl** | Tổng hợp thông tin để lập lịch trình | Lặp lại            | Khách phải tự tra cứu địa điểm, giờ hoạt động, dịch vụ và lịch chương trình từ nhiều nguồn trước khi ghép thành kế hoạch du lịch.                              |
| 2   | **Vinpearl** | Cá nhân hóa lịch trình theo nhu cầu  | AI có thể tốt hơn  | Từ yêu cầu như _“Gia đình có trẻ nhỏ, thích khám phá nhưng muốn nghỉ trưa”_, hệ thống đề xuất lịch trình phù hợp với sở thích, thời gian và nhịp độ mong muốn. |
| 3   | **Vinpearl** | Dung hòa sở thích của nhóm khách     | Pain từ người khác | Người tổ chức chuyến đi khó cân bằng nhu cầu của các thành viên: người thích trò cảm giác mạnh, người muốn nghỉ dưỡng, trẻ nhỏ cần hoạt động phù hợp.          |

---

### 🎢 2. Điều chỉnh lịch trình trong ngày vui chơi

| #   | Subsidiary              | Tên bài toán / Bottleneck                    | Lens              | Mô tả ngắn                                                                                                                                                                             |
| --- | ----------------------- | -------------------------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 4   | **Vinpearl/VinWonders** | Điều chỉnh lịch trình theo thời gian chờ     | Tốn thời gian     | Khách đến hoạt động mới phát hiện hàng chờ dài và phải tự tìm phương án thay thế. Hệ thống đề xuất đổi thứ tự hoạt động dựa trên thời gian chờ được cập nhật, khoảng cách và sở thích. |
| 5   | **Vinpearl/VinWonders** | Sắp xếp lịch khi hoạt động tạm ngừng         | AI có thể tốt hơn | Khi một hoạt động đóng cửa hoặc đổi giờ, hệ thống xác định phần lịch bị ảnh hưởng và đề xuất lựa chọn thay thế phù hợp để khách xác nhận.                                              |
| 6   | **Vinpearl/VinWonders** | Hạn chế di chuyển vòng và bỏ lỡ chương trình | Tốn thời gian     | Khách phải tự đối chiếu bản đồ, thời gian di chuyển và giờ biểu diễn. Hệ thống gợi ý thứ tự tham quan khả thi, có khoảng đệm để đến đúng giờ.                                          |

---

### 👨‍👩‍👧‍👦 3. Cá nhân hóa theo đặc điểm và nhịp độ của khách

| #   | Subsidiary              | Tên bài toán / Bottleneck                       | Lens               | Mô tả ngắn                                                                                                                                                          |
| --- | ----------------------- | ----------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 7   | **Vinpearl/VinWonders** | Lọc hoạt động phù hợp với thành viên trong nhóm | Lặp lại            | Phụ huynh phải kiểm tra điều kiện tuổi, chiều cao và các hạn chế tham gia của từng hoạt động. Hệ thống lọc theo quy định được xác minh và thông tin khách cung cấp. |
| 8   | **Vinpearl**            | Bổ sung thời gian ăn uống và nghỉ ngơi          | Pain từ người khác | Lịch trình quá dày có thể khiến gia đình mệt mỏi. Hệ thống đưa giờ ăn, nghỉ và giới hạn đi bộ do khách lựa chọn vào kế hoạch.                                       |
| 9   | **Vinpearl**            | Điều chỉnh kế hoạch khi nhu cầu thay đổi        | AI có thể tốt hơn  | Khách có thể yêu cầu _“Chúng tôi hơi mệt, muốn bớt đi bộ và về khách sạn trước 17 giờ”_. Hệ thống đề xuất lịch mới, giữ các hoạt động ưu tiên và mốc đặt trước.     |

---

### 📱 4. Kết nối lịch trình với dịch vụ trong ứng dụng Vinpearl

| #   | Subsidiary   | Tên bài toán / Bottleneck                      | Lens               | Mô tả ngắn                                                                                                                                                               |
| --- | ------------ | ---------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 10  | **Vinpearl** | Tránh trùng lịch với dịch vụ đã đặt            | Lặp lại            | Khách phải tự đối chiếu lịch vui chơi với giờ đặt bàn, spa hoặc dịch vụ khác. Khi được cấp quyền truy cập, hệ thống đưa các mốc đã đặt vào lịch trình để tránh xung đột. |
| 11  | **Vinpearl** | Giải thích và so sánh các phương án lịch trình | Tốn thời gian      | Khách khó chọn giữa nhiều phương án. Trợ lý trình bày các đánh đổi như ít chờ hơn, ít đi bộ hơn hoặc trải nghiệm nhiều hoạt động yêu thích hơn.                          |
| 12  | **Vinpearl** | Hỗ trợ nhân viên tư vấn lịch trình             | Pain từ người khác | Lễ tân phải tư vấn lặp lại cho nhiều nhóm khách. Hệ thống tạo bản nháp dựa trên nhu cầu và thông tin vận hành để nhân viên kiểm tra trước khi giới thiệu.                |

---

## 💡 Lưu ý khi chọn bài toán

1. **Chọn một vấn đề chính để Deep-Dive:** Ưu tiên **#4 — Điều chỉnh lịch trình theo thời gian chờ**, dùng nhu cầu cá nhân hóa ở #2, #7 và #8 làm đầu vào. Phạm vi ban đầu có thể giới hạn trong một ngày tại một khu VinWonders.

2. **Xác minh dữ liệu trước khi cam kết tính năng:** Cần kiểm tra khả năng lấy thời gian chờ, giờ hoạt động, trạng thái đóng/mở và thời gian di chuyển. Khi dữ liệu thiếu hoặc cũ, ứng dụng phải hiển thị rõ thay vì tự tạo số liệu.

3. **Operational Boundary phải rõ:** Hệ thống được đề xuất lịch trình; khách xác nhận trước khi thay lịch đã lưu. Không tự đặt dịch vụ, thanh toán hoặc hủy đặt chỗ. Chỉ sử dụng vị trí và dữ liệu cá nhân khi được khách cho phép.

4. **Problem First, AI Second:** Dùng bộ quy tắc để kiểm tra điều kiện tham gia, bộ tối ưu để sắp xếp lịch và LLM để hiểu nhu cầu, giải thích đề xuất. Không cần Multi-Agent nếu quy trình đơn giản đã đáp ứng được bài toán.

5. **Đo hiệu quả bằng trải nghiệm thực tế:** Theo dõi thời gian lập hoặc chỉnh lịch, thời gian xếp hàng, số hoạt động ưu tiên hoàn thành và mức hài lòng. Các mục tiêu cải thiện cần được kiểm chứng qua thử nghiệm.

# 03 — AI Log & Reflection

**Đề tài:** VPoint — điểm, hạng và quyền lợi liên thông Vingroup → Co-pilot CSKH VPoint
**AI đã dùng:** Claude (scoping, viết tài liệu, viết code), Gemini 3.5 Flash (đối tượng được test trong prototype)

---

## 1. AI đã giúp gì

- **Gợi ý bài toán chính:** AI gợi ý chủ đề chính cho bài toán cụ thể
- **Brainstorm bài toán (Phase 1):** AI gợi ý các góc nhìn theo 4 lenses cho từng công ty thành viên, giúp từ một đề tài rộng rút ra 7 bài toán cụ thể.
- **Chọn bài toán (Phase 2):** AI chỉ ra Card #2 (gợi ý ưu đãi) thực chất là bài toán **rule engine**, không cần LLM. Tôi dùng nhận xét này để loại Card #2 khỏi Deep-Dive.
- **Thiết kế kiến trúc:** AI đề xuất tách "tính số liệu" (API/Rule) khỏi "diễn đạt" (LLM) để tránh LLM sai số điểm.
- **Viết prompt và test:** AI viết system prompt với 3 quy tắc (Rule 1–3) và 3 adversarial tests. Starter code chỉ có 2 tests trong khi worksheet yêu cầu **tối thiểu 3**, nên tôi thêm 1 test.
- **Gợi ý model sử dụng:** Trong quá trình gọi API, theo như đề bài là dùng gemini-2.5-flash, nhưng không cho xài sử dụng new user nên tôi dùng gemini-3.8-flash, nhưng mà tiếp tục bị lỗi do high demand, nên dùng AI để gợi ý model sử dụng

## 2. AI sai / không đáng tin ở đâu

**Những điểm đã nhận diện trong quá trình làm:**

| # | Vấn đề | Cách tôi xử lý |
|---|--------|----------------|
| 1 | Các con số (14 phút/lượt, 3.000 yêu cầu/ngày, 400 giờ công) là **ước lượng của AI**, không có nguồn từ Vingroup. Nếu nộp như sự thật thì đó là hallucination. | Đánh dấu rõ *(GĐ)* = giả định trong mọi file và đặt "xác minh bằng log thật" thành điều kiện của quyết định GO. |
| 2 | Chi tiết chương trình VPoint thật (tên hạng, tỉ lệ quy đổi, điều kiện) AI có thể nhớ sai hoặc đã lỗi thời. | Prototype chỉ dùng dữ liệu **MOCK**, ghi chú rõ trong code. Không đưa chi tiết chính sách thật vào bài. |
| 3 | Ví dụ mẫu (Xanh SM + pin < 5%) khác đề tài của tôi, nên check của starter code không dùng được nguyên xi. | Viết lại ranh giới (Rule 1–3) và các đoạn kiểm tra theo bài toán VPoint, giữ nguyên khung của starter code. |


## 3. Tôi đã sửa prompt / ranh giới như thế nào

| Vòng | Test FAIL | Nguyên nhân | Sửa gì trong SYSTEM_PROMPT | Kết quả sau sửa |
|:---:|-----------|-------------|---------------------------|-----------------|
| 1 | Nội dung gen ra không đúng với đề | AI tự sáng tạo quá đà, promt không tập trung và khá lang mang với yêu cầu | Yêu cầu tập trung vào cấu trúc bài, không được tự sáng tạo | Kết quả tập trung và đúng với yêu cầu, nhưng vẫn còn bị tình trạng AI Flob và dính nhiều icon vào bài |


## 4. Bài học rút ra

- Một số bài toán "nghe có vẻ cần AI" thực ra là rule engine (Card #2). Phân biệt sớm giúp tiết kiệm chi phí.
- Kiểm tra ranh giới bằng prompt chưa bao giờ là bảo đảm tuyệt đối. Trong hệ thống thật cần thêm lớp kiểm tra bằng code (ví dụ: validator chặn output không có `[DRAFT_ONLY]` trước khi hiển thị), ngoài ra còn có HITL.
- Con số do AI đưa ra phải được coi là giả thuyết cần kiểm chứng.
- Khi promt, nên đưa ra ngữ cảnh cụ thể, chi tiết để AI có thể hỗ trợ tốt hơn
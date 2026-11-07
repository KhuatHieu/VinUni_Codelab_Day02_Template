# 03 — AI Log & Reflection

**Đề tài Deep-Dive:** Trợ lý thẩm định sơ bộ yêu cầu bảo hành VinFast
**AI đã dùng:** Claude Code (mô hình Claude Sonnet 5.5), kèm công cụ tìm kiếm web và đọc file PDF của chính phiên làm việc đó.
**Phạm vi nhật ký:** các file `01-problem-scan.md`, `02-deep-dive-report.md`, `04-workflow-diagram.png`. Phần code `prompt_prototype.py` chưa làm tại thời điểm viết (xem mục cuối).

---

## 0. Mức độ AI tham gia (nói thẳng)

Phần lớn nội dung chữ của ba file trên do AI soạn. Vai trò của tôi là giao việc, đặt ràng buộc (kiểm tra trùng ý tưởng với các branch khác, "không bịa", phải tra nguồn thật trước khi vẽ sơ đồ) và quyết định bước tiếp theo. AI không biết vận hành thật của Vingroup, nên mọi con số vận hành trong bài là giả định, đã được đánh dấu như vậy trong từng file.

---

## 1. AI đã giúp gì

- **Hiểu repo và cách chấm điểm:** AI đọc README, worksheet và `autograder.py`, rồi giải thích file nào là đề, file nào là bài nộp, autograder chấm gì. Nhờ đó tôi biết autograder chỉ kiểm tra file có tồn tại và vài từ khóa trong code, chứ không đánh giá chất lượng nội dung.
- **Tránh trùng ý tưởng:** AI đọc `01-problem-scan.md` của hai branch đã có bài (`khuathieu`: gian lận cuốc ảo Xanh SM, chẩn đoán lỗi VinFast, đối soát V-GREEN, phân loại phản ánh Vinhomes, tóm tắt xuất viện Vinmec, đặt phòng đoàn Vinpearl; `nguyenthanhdanh`: ba card đều xoay quanh VPoint). Từ đó đề xuất 6 bài toán không trùng, dùng đủ 4 lenses. Hai branch còn lại (`nguyenthihongsan`, `thanhbinh`) lúc đó chưa có bài nên chưa so sánh được.
- **So sánh Rule với LLM với Agent:** AI chỉ ra phần tính hạn bảo hành (ngày, km) nên do rule code làm vì chính xác tuyệt đối, còn LLM chỉ đọc điều khoản và soạn nháp. Agent bị loại vì quy trình đã cố định 5 bước nên không cần tự chủ.
- **Tra cứu và đọc nguồn thật:** AI tìm sổ bảo hành chính thức của VinFast, tải file PDF về, trích văn bản và ghi lại số mục (điều kiện, loại trừ, thời hạn từng hạng mục, handoff với nhà sản xuất lốp và VinFast cho pin).
- **Dựng sơ đồ:** AI viết script vẽ `04-workflow-diagram.png` có phân làn, phân biệt rõ ô có nguồn chính thức (xanh) với ô giả định (cam, nét đứt).

---

## 2. AI sai / không đáng tin ở đâu

| # | Vấn đề | Cách phát hiện | Cách xử lý |
|---|--------|----------------|------------|
| 1 | **Tự thêm chi tiết quy trình không có nguồn.** Bản đầu của `02-deep-dive-report.md` có "DMS", "sổ bảo hành giấy/ảnh chụp", "Quản lý bảo hành, chờ vài giờ đến 1 ngày", cùng các con số 20 phút và 15 hồ sơ/ngày. Không cái nào có nguồn công khai. | Tôi yêu cầu tra quy trình thật của VinFast và "không bịa". Tra xong, AI không tìm được tài liệu công khai nào mô tả các bước nội bộ hay thời gian xử lý. | Bỏ các chi tiết không có nguồn. Phần còn lại được ghi rõ là giả định (dấu `*`, viền cam đứt nét). Chỉ giữ điều kiện, phạm vi và loại trừ lấy từ sổ bảo hành. |
| 2 | **Kết quả tìm kiếm tóm tắt sai hoặc không kiểm chứng được.** Một lượt tìm kiếm khẳng định VinFast có "quy trình chuẩn 5 bước: đặt hẹn, tiếp nhận, tư vấn, sửa chữa, bàn giao". | AI mở hai bài báo gốc (Báo Hà Tĩnh, Tạp chí Tòa án nhân dân). Cả hai đều không có câu đó. | Không đưa "5 bước" vào sơ đồ. Bài học: bản tóm tắt của công cụ tìm kiếm phải được đối chiếu với trang gốc. |
| 3 | **Nguồn chính thức khó đọc.** Các trang `vinfastauto.com` trả về lỗi 403. Công cụ đọc web báo rằng PDF "không có văn bản", dù thực tế file có lớp chữ. | AI tải file PDF về máy và dùng `pdftotext` đọc trực tiếp. | Đọc nguyên văn sổ bảo hành thay vì tin bản tóm tắt tự động. |
| 4 | **Lỗi số học và nhất quán.** Flow tương lai cộng lại khoảng 6,5 phút, nhưng Success Metric ghi "dưới 5 phút". | AI tự phát hiện khi rà lại ngay sau khi viết. | Đổi metric thành "dưới 7 phút" ở cả `02-deep-dive-report.md` và Card #1, thêm dòng cộng thời gian để người đọc kiểm được. |
| 5 | **Lỗi kỹ thuật khi dựng sơ đồ và định dạng.** Font thiếu ký hiệu đồng hồ (hiện ô vuông), dòng nguồn ở chân ảnh bị cắt, một dòng trong sơ đồ chữ dài hơn 1 ký tự làm lệch cột. Sau khi file được định dạng lại, các ngắt dòng `<br>` trong bảng bị mất nên các mục 1., 2., 3. dính liền. | Xem lại ảnh sau khi vẽ, và đọc lại file sau khi nó thay đổi trên đĩa. | Thay ký hiệu bằng chữ "Thời gian:", chỉnh lại bố cục, rút gọn dòng, đổi thành (1), (2), (3). |
| 6 | **Rủi ro bản chất:** ý tưởng và con số ban đầu là do AI đề xuất, không xuất phát từ quan sát thực tế của tôi. | Đây là giới hạn đã biết, không phải lỗi bị bắt quả tang. | Mọi con số vận hành đều có chú thích giả định, và quyết định GO được giới hạn ở pilot hẹp có điều kiện dừng. |

---

## 3. Tôi đã sửa prompt / ranh giới như thế nào

| Yêu cầu | Vấn đề | Ràng buộc tôi thêm | Kết quả |
|---------|--------|--------------------|---------|
| "Làm 01-problem-scan.md" | Chưa biết bạn cùng nhóm đã chọn gì, dễ trùng. | "Check xem ý tưởng của các branch khác đã trùng chưa, rồi đưa ý tưởng mới." | AI đọc các branch, loại những bài đã dùng, chọn 6 bài mới. |
| "Tạo 04-workflow-diagram.png" | Nếu để AI tự vẽ thì sẽ lặp lại lỗi bịa quy trình ở mục 1 bảng trên. | "Search trên mạng workflow hiện tại của VinFast. **Không bịa.** Rồi làm." | AI tra nguồn trước, sơ đồ phân biệt có nguồn với giả định, và chú thích đỏ nêu rõ số phút là ước tính. |
| "Sửa 02 cho khớp sơ đồ" | Báo cáo và sơ đồ có hai phiên bản quy trình khác nhau. | Yêu cầu đồng bộ, và thêm mục nguồn. | Bỏ chi tiết không có nguồn, thêm mục "Nguồn tham khảo" và đoạn "Mức độ kiểm chứng". |

**Quy tắc rút ra:** thay vì chỉ nói "làm cho tôi X", tôi đặt thêm hai điều kiện, (a) phải tra nguồn trước khi viết, (b) phải tách rõ "có nguồn" với "giả định" trong chính sản phẩm.

---

## 4. Điều gì vẫn chưa được kiểm chứng

- Các bước nội bộ cụ thể của cố vấn dịch vụ VinFast, đặc biệt Bước 1 và Bước 5 trong sơ đồ.
- Toàn bộ số phút (3, 5, 7, 3, 2) và tổng ~20 phút/hồ sơ, cùng khối lượng ~15 hồ sơ/ngày/xưởng.
- Việc Bước 3 và 4 thực sự là điểm nghẽn.
- Sổ bảo hành tôi dùng là của dòng **Limo Green**, file PDF có lớp chữ "DRAFT" trong metadata. Thời hạn khác nhau theo dòng xe (Limo Green: 7 năm hoặc 160.000 km; VF 9 bản Canada: 10 năm hoặc 200.000 km), nên cần đối chiếu với sổ đi kèm từng dòng xe khi triển khai thật.

---

## 5. Bài học rút ra

1. **AI viết trôi chảy cả khi đang bịa.** Bản đầu của báo cáo đọc rất thuyết phục, nhưng nhiều chi tiết trong đó không có nguồn. Độ trôi chảy không phải bằng chứng.
2. **Hãy đòi nguồn trước khi viết, không phải sau.** Yêu cầu "không bịa, tra nguồn trước" hiệu quả hơn việc rà lỗi sau khi bản nháp đã xong.
3. **Đọc nguồn gốc, đừng tin bản tóm tắt.** Công cụ tìm kiếm và công cụ đọc web đều từng cho kết quả sai hoặc không đọc được, trong khi file gốc có đủ nội dung.
4. **Con số của AI là giả thuyết.** Nên đánh dấu trong chính sản phẩm và biến việc đo baseline thật thành điều kiện của quyết định GO.
5. **Tách việc chính xác khỏi việc ngôn ngữ.** Phần tính hạn ngày/km để rule code làm, LLM chỉ đọc và soạn nháp, người luôn duyệt.

---

## 6. Phần chưa làm

- **`prompt_prototype.py`:** chưa viết `SYSTEM_PROMPT`, `evaluate_prompt()` và adversarial tests. Khi làm xong, cần bổ sung vào mục này: test nào FAIL, nguyên nhân, đã sửa prompt ra sao.
- Tôi chưa tự kiểm tra lại từng trích dẫn mục của sổ bảo hành ngoài việc đối chiếu với văn bản AI trích ra. Nếu có thời gian, nên mở file PDF và đọc lại các mục 2, 3, 6, 9, 10, 11.

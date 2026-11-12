# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603343
- Ngày / CVAT local: 11/11/2026
- Công cụ đã dùng: CVAT, OpenCV Tool trong CVAT

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ở ảnh 000000181542.jpg, đã tự vẽ mask cho label `person`
- Class và quy tắc tôi dùng để chọn biên: Class `person`: chỉ vẽ phần người nhìn thấy và đặt biên ở chỗ người giao với vật khác. Với người ngồi trên xe máy, xác định các điểm người tiếp xúc với xe (chỗ người ngồi trên xe) và lấy đó làm biên giữa người và xe.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Không áp dụng, không dùng gợi ý tự động.
- Nếu không dùng gợi ý: Không dùng. Quyết định gán nhãn: tách người đang lái xe và chiếc xe thành hai object riêng, một mask `person` và một mask `motorcycle`, không gộp người vào mask xe. Lý do: theo quy tắc instance, mỗi vật đếm được là một mask riêng; ranh giữa hai mask là chỗ người ngồi trên xe như đã nêu ở trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Ở hard_patonic, ảnh 000000350023.jpg, class `road` và `car`
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: phủ nhầm vùng của `road` lên `car`
- Bằng chứng tôi nhìn thấy: phần màu của `road` đè lên `car`
- Quy tắc và hành động sửa: chỉnh layer của `road` xuống 1 lớp
- Sau sửa đã Save và export lại chưa?: Đã save và export lại

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp3_thin`: giá treo biển xanh bên phải | (a) `pole` chỉ là cột dọc; (b) gồm cả thanh ngang nhô ra đỡ biển | Thanh ngang nối liền cột, không phải biển | Tô cột dọc và thanh ngang. Hỏi coach: có cần tô cả thanh ngang trên không? |
| 2. `cp4_curb`: phần bên phải bó vỉa | (a) `sidewalk` chỉ là lối đi dọc đường; (b) gồm cả bãi đỗ xe/sân nhà | Ranh theo chức năng và bó vỉa, bãi đỗ dùng để đỗ xe, không phải lối đi bộ | Chỉ tô lối đi bộ, bỏ bãi đỗ và dải cỏ. Hỏi coach: bãi đỗ có tính `sidewalk` không? |
| 3. `cp6_coverage`: tầng 1 tòa nhà bên phải | (a) `building` gồm mái hiên và từng cột; (b) tô kín cả tầng 1 | Chỉ tô phần nhìn thấy; giữa các cột là người, xe, cửa hàng | Tô mái hiên và các cột, để trống khoảng giữa. Hỏi coach: nhà phía sau có cần tô không? |

# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602071
- Ngày / CVAT local: 17/09/2026 / http://localhost:8080
- Công cụ đã dùng: CVAT local, Polygon, Mask/Brush, phóng to kiểm biên và gợi ý segmentation tự động có sửa thủ công

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

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

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, motorcycle lớn ở tiền cảnh.
- Class và quy tắc tôi dùng để chọn biên: Chọn `motorcycle`; chỉ lấy thân xe, bánh và các chi tiết thực sự nhìn thấy, không lấy nền nằm trong khoảng trống của bánh.
- Nếu dùng gợi ý sau đó: Gợi ý có chỗ ăn vào nền và tạo quá nhiều điểm răng cưa. Tôi phóng to, kéo biên về silhouette, bỏ điểm thừa trên đoạn thẳng và giữ thêm điểm ở góc/đường cong.
- Nếu không dùng gợi ý: Không áp dụng.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `cp6_coverage`, xe buýt lớn ở giữa ảnh và hai khe trời phía trên.
- Lỗi thuộc loại: sai lớp và phủ vùng.
- Bằng chứng tôi nhìn thấy: Xe buýt bị gợi ý nhập vào lớp `car`, trong khi `bus` không có trong class list của checkpoint; hai khe trời hẹp giữa các tòa nhà còn trống.
- Quy tắc và hành động sửa: Loại toàn bộ silhouette xe buýt khỏi `car` và các lớp semantic khác; bổ sung `sky` chỉ tại pixel trời nhìn thấy giữa các tòa nhà.
- Sau sửa đã Save và export lại chưa? Đã Save, export lại và kiểm ZIP bằng script của repo.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Đã chạy `inspect_submissions.py`; cả 9 ZIP đều báo OK về cấu trúc, chưa có điểm reference. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | `cp1_holes`, kính và khoảng trống trong bánh motorcycle | Khoét toàn bộ vùng tối hoặc giữ phần kính/chi tiết thuộc xe | Kính thuộc vật thể; chỉ bỏ nền thật sự nhìn xuyên qua và giá đỡ ngoài xe | Giữ kính thuộc motorcycle, bỏ nền trong khoảng hở và loại giá đỡ |
| 2 | `cp5_occlusion`, người lái và motorcycle ở tiền cảnh | Gộp người với xe hoặc tách thành hai instance | Person và motorcycle là hai class; chỉ vẽ phần nhìn thấy, không nối qua phần bị che | Tách person và motorcycle, đặt person ở lớp trước |
| 3 | `cp4_curb`, ranh road–sidewalk phía phải | Chọn theo màu xám hoặc theo mép bó vỉa/chức năng | Road và sidewalk có màu gần nhau; bó vỉa và chức năng đi lại là dấu hiệu chính | Theo sát mép bó vỉa, loại bồn đất và phần xe ghi hình |

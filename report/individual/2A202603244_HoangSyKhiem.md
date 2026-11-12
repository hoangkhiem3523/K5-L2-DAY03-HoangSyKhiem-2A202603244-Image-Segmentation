# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603244
- Ngày / CVAT local: 12/11/2026 — CVAT local (http://localhost:8080)
- Công cụ đã dùng: CVAT local (Polygon), có dùng gợi ý pre-annotation ban đầu rồi kiểm tra, gộp vùng và chỉnh sửa biên thủ công trên CVAT trước khi Export (`Segmentation mask 1.1` cho `easy_semantic`, `COCO 1.0` cho `medium_instance` và `hard_panoptic`).

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Hiện nộp trước 3 task chính (`easy_semantic`, `medium_instance`, `hard_panoptic`); 6 trạm checkpoint (`cp1_holes`, `cp2_slice`, `cp3_thin`, `cp4_curb`, `cp5_occlusion`, `cp6_coverage`) chưa xuất bài nộp.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: …
- Class và quy tắc tôi dùng để chọn biên: …
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: …
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `easy_semantic` — `7ee6d192-89e2408b.jpg` (lề phải cao tốc và vùng đồi cây hai bên), đồng thời chỉnh biên ở `817bca71-00000000.jpg`, `81ae7cbb-6bc63a4a.jpg`, `medium_instance` (`000000181542.jpg`, `000000373353.jpg`, `000000458325.jpg`) và `hard_panoptic` (`000000350023.jpg`, `000000460147.jpg`).
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: sai lớp (`sidewalk` giả trên lề cao tốc), thiếu vùng `vegetation` trên sườn đồi và thừa/lệch biên.
- Bằng chứng tôi nhìn thấy: Gợi ý ban đầu ở `7ee6d192-89e2408b.jpg` gán nhầm mảnh `sidewalk` (1.586 px) trên vai đường cao tốc, thiếu mảng `vegetation` sườn đồi và thừa biên `road` (350.462 px); ở `hard_panoptic/000000350023.jpg` có `traffic light` thừa (`2 → 1`).
- Quy tắc và hành động sửa: Kiểm tra và chỉnh trực tiếp trên CVAT theo quy tắc `road`–`sidewalk` và ranh vùng nhìn thấy; xóa `sidewalk` giả (`1.586 → 0` px), chỉnh `road` (`350.462 → 323.358` px), bổ sung/gộp mảng `vegetation` (`54.287 → 79.308` px), và cập nhật lại `traffic light`/`sidewalk` ở `hard_panoptic`.
- Sau sửa đã Save và export lại chưa? Đã Save trên CVAT local, export lại `easy_semantic.zip` (`Segmentation mask 1.1`), `medium_instance.zip` (`COCO 1.0`), `hard_panoptic.zip` (`COCO 1.0`) vào `submissions/`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): `python scripts/inspect_submissions.py` báo `[OK]` cho cả 3 file `easy_semantic.zip`, `medium_instance.zip` (82 polygon) và `hard_panoptic.zip` (60 polygon) / chưa có điểm (chưa phát ground truth chính thức). Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | … | … | … |
| 2 | … | … | … |
| 3 | … | … | … |

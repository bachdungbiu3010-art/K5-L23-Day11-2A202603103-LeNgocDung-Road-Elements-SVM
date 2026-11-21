# Phiếu QC 1 — Road v1.0

Lô được kiểm: **Lê Ngọc Dũng**.  
Người kiểm/lập kết quả thực tế: **Trợ lý AI theo yêu cầu Lê Ngọc Dũng**, kiểm XML và ảnh gốc.  
Người kiểm chéo xác nhận: **Nguyễn Bảo Khánh**. Nội dung do trợ lý hỗ trợ kiểm và soạn, đã được Khánh xác nhận theo thông báo của Lê Ngọc Dũng ngày 21/11/2026. Không tạo chữ ký hoặc giả lời nói của Khánh.  
Ngày kiểm: 21/11/2026. Guideline: Road v1.0.  
File: lengocdung-front.zip; lengocdung-fisheye.zip. Revision: 1 của bản chuẩn bị, chưa nộp.
Số ảnh kiểm: **6** (A01, A06, A12, B02, B03, B06), 0 ảnh thêm trong mẫu. Số nhãn đã kiểm (shape + tag): **96**.

Phương pháp: kiểm 2 ZIP toàn lô về cấu trúc; đối chiếu bằng mắt tất cả shape/tag trong 6 ảnh mẫu với ảnh gốc. Không có GT nên không xác nhận độ lệch tối đa 5 px, điểm số hoặc toàn bộ ca bị che. 0 trong bảng nghĩa là chưa ghi nhận lỗi xác định ở lần kiểm này, không có nghĩa đã chứng minh mọi nhãn đúng GT.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác định | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 16 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 16 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 16 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 16 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 24 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 16 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 32 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 16 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 37 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Đơn vị số mục kiểm: QC1-01 = 6 tag camera; QC1-02 = 8 phía L1/R1 của 3 ảnh front và B03 rear (không suy ra vạch bắt buộc khi không thấy); QC1-03–06 = lane; QC1-07 = vùng và curb; QC1-08 = đèn; QC1-09 = đèn + biển; QC1-10 = biển; QC1-11 = shape của 3 ảnh fisheye; QC1-12 = 2 ZIP. Cùng nhãn có thể được kiểm theo nhiều mã; mẫu số tính tỉ lệ chỉ đếm shape+tag một lần.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn / số thứ tự trong XML | Mức | Mô tả |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A12 | lane #10, điểm đầu (663.34,417.41) | nặng | Đường này ở bên phải R1 nhưng position=L1. Cần đối chiếu và sửa sang vị trí phía phải phù hợp (nghi R2); không được sửa mọi đường trùng position thành double. |

Số # là thứ tự shape do parser xuất ra, không phải ID hiển thị trên CVAT. Dùng loại nhãn, vị trí và ảnh minh chứng để tìm đúng đối tượng.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp hiện có |
| --- | --- | --- |
| A01 | Hai lane L2 của vạch đôi có được giữ? | Theo lời học viên truyền đạt: thầy cho vẽ 2 lane, cả hai kind=double; đã ghi nguồn hướng dẫn, không tính lỗi xác định. |
| A06 | Không thấy R1 rõ có được miễn QC1-02? | Chưa có xác nhận coach; không tự vẽ thêm vạch. |
| A12 | Crosswalk thấy rõ nhưng không có polygon; kế hoạch ảnh có yêu cầu không? | Chưa có bảng kế hoạch trong docs; ghi ca chờ xác nhận, chưa cộng lỗi bỏ sót vào tỉ lệ. |
| B03 | Quy ước position theo làn xe khi nhìn từ camera sau | Cần lead đối chiếu; chưa dùng bài học viên khác làm GT. |
| B06 | Vạch cạnh ray/đảo và vùng alternative có đúng loại không? | Cần lead xác nhận, không tự thay nhãn. |
| B02/B03 | Các edge_zone còn khác gợi ý checker | Chi tiết ở lint-dung.json; cần đối chiếu toàn ảnh, không xóa cảnh báo trong log. |
| A06 | Đèn người đi bộ có hình trắng đang sáng nhưng export vẫn off | Cần kiểm lại trên ảnh phóng to/CVAT; chưa tự quy thành lỗi màu an toàn. |

## Quyết định
Lỗi nặng xác định: **1**. Lỗi chính xác định: **0 / 96 nhãn = 0.00%**. Lỗi nhẹ xác định: **0**. Có các ca chờ lead như bảng trên.
**Kết luận của lần kiểm có trợ lý: Rework.** Có ít nhất một lỗi nặng xác định nên áp dụng Rework; không dùng Hold để thay thế khi đã có lỗi nặng. Đây là kết quả của bản trước khi sửa A12, được học viên thông báo đã có Khánh xác nhận; chưa phải điểm/kết luận của coach. Lỗi A12 đã được sửa trong bản nộp cục bộ mới. Chưa có xác nhận Khánh kiểm lại chính ZIP sau sửa, nên không tự đổi quyết định thành Release.

## Bằng chứng và phạm vi
| Ảnh | Shape | Tag | Tổng nhãn | Ghi chú |
| --- | ---: | ---: | ---: | --- |
| A01 | 10 | 4 | 14 | Đã xem XML và overlay ảnh gốc |
| A06 | 14 | 4 | 18 | Đã xem XML và overlay ảnh gốc |
| A12 | 11 | 4 | 15 | Đã xem XML và overlay ảnh gốc |
| B02 | 11 | 4 | 15 | Đã xem XML và overlay ảnh gốc |
| B03 | 17 | 4 | 21 | Đã xem XML và overlay ảnh gốc |
| B06 | 9 | 4 | 13 | Đã xem XML và overlay ảnh gốc |

Chưa thể chỉ định một ảnh "không lỗi tuyệt đối" khi chưa có GT. A01 không có lỗi xác định trong lần rà này sau khi ghi ngoại lệ vạch đôi, nhưng vẫn chưa chứng minh độ lệch 5 px.

Phần lỗi trên là kết quả tối thiểu đã xác định, không dùng số cảnh báo lint chia cho số ảnh để tính tỉ lệ. Không gửi tin, không giả chữ ký hoặc lời xác nhận của Khánh.

## Phản hồi sau sửa
A12: position của lane bắt đầu tại (663.34,417.41) đã sửa L1 → R2 trong ZIP nộp mới; giữ nguyên tọa độ. Phiếu này lưu dấu vết lỗi trước sửa, không tự ghi thành lỗi chưa sửa trong báo cáo mới. Xem nhat-ky-chot-bai.json.

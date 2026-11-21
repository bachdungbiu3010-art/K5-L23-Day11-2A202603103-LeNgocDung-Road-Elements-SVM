# Phiếu QC 1 — Road v1.0

Lô được kiểm: **Nguyễn Bảo Khánh**.  
Người kiểm/lập kết quả thực tế: **Trợ lý AI theo yêu cầu Lê Ngọc Dũng**, kiểm XML và ảnh gốc.  
Học viên phát hành: **Lê Ngọc Dũng**, có trợ lý AI hỗ trợ kiểm và soạn; phát hành theo yêu cầu nộp bài ngày 21/11/2026.  
Ngày kiểm: 21/11/2026. Guideline: Road v1.0.  
File: nguyenbaokhanh-front.zip; nguyenbaokhanh-fisheye.zip. Revision: chưa có manifest của Khánh; định danh trực tiếp bằng SHA256 bên dưới.
Số ảnh kiểm: **6** (A01, A06, A12, B02, B03, B06), 0 ảnh thêm trong mẫu. Số nhãn đã kiểm (shape + tag): **103**.

Phương pháp: kiểm 2 ZIP toàn lô về cấu trúc; đối chiếu bằng mắt tất cả shape/tag trong 6 ảnh mẫu với ảnh gốc. Không có GT nên không xác nhận độ lệch tối đa 5 px, điểm số hoặc toàn bộ ca bị che. 0 trong bảng nghĩa là chưa ghi nhận lỗi xác định ở lần kiểm này, không có nghĩa đã chứng minh mọi nhãn đúng GT.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác định | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 32 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 15 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 35 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 20 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 41 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Đơn vị số mục kiểm: QC1-01 = 6 tag camera; QC1-02 = 8 phía L1/R1 của 3 ảnh front và B03 rear (không suy ra vạch bắt buộc khi không thấy); QC1-03–06 = lane; QC1-07 = vùng và curb; QC1-08 = đèn; QC1-09 = đèn + biển; QC1-10 = biển; QC1-11 = shape của 3 ảnh fisheye; QC1-12 = 2 ZIP. Cùng nhãn có thể được kiểm theo nhiều mã; mẫu số tính tỉ lệ chỉ đếm shape+tag một lần.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn / số thứ tự trong XML | Mức | Mô tả |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A12 | lane: thiếu L1 | nặng | Ảnh thấy vạch trắng phía trái làn; XML chỉ có lane R1 (#6), chưa có L1. Không tự lấy bài Dũng làm GT. |
| 2 | QC1-06 | A06 | lane #14 | chính | Polyline đặt trên vạch sơn trắng nhưng color=yellow; cần sửa white và kiểm style theo đoạn sơn thật. |
| 3 | QC1-09 | A06 | traffic_sign #2 | chính | Biển ONE WAY đang group=supplementary; theo bảng nhóm biển trong docs phải mandatory. |

Số # là thứ tự shape do parser xuất ra, không phải ID hiển thị trên CVAT. Dùng loại nhãn, vị trí và ảnh minh chứng để tìm đúng đối tượng.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp hiện có |
| --- | --- | --- |
| A01 | Hai lane L2 của vạch đôi có được giữ? | Theo lời học viên truyền đạt: thầy cho vẽ 2 lane, cả hai kind=double; đã ghi nguồn hướng dẫn, không tính lỗi xác định. |
| A06 | Không thấy R1 rõ có được miễn QC1-02? | Chưa có xác nhận coach; không tự vẽ thêm vạch. |
| A12 | Crosswalk thấy rõ nhưng không có polygon; kế hoạch ảnh có yêu cầu không? | Chưa có bảng kế hoạch trong docs; ghi ca chờ xác nhận, chưa cộng lỗi bỏ sót vào tỉ lệ. |
| B03 | Quy ước position theo làn xe khi nhìn từ camera sau | Cần lead đối chiếu; chưa dùng bài học viên khác làm GT. |
| B06 | Vạch cạnh ray/đảo và vùng alternative có đúng loại không? | Cần lead xác nhận, không tự thay nhãn. |

## Quyết định
Lỗi nặng xác định: **1**. Lỗi chính xác định: **2 / 103 nhãn = 1.94%**. Lỗi nhẹ xác định: **0**. Có các ca chờ lead như bảng trên.
**Kết luận của lần kiểm có trợ lý: Rework.** Có ít nhất một lỗi nặng xác định nên áp dụng Rework; không dùng Hold để thay thế khi đã có lỗi nặng. Đây chưa phải quyết định chính thức của coach hoặc xác nhận của học viên kiểm chéo.

## Bằng chứng và phạm vi
| Ảnh | Shape | Tag | Tổng nhãn | Ghi chú |
| --- | ---: | ---: | ---: | --- |
| A01 | 12 | 4 | 16 | Đã xem XML và overlay ảnh gốc |
| A06 | 15 | 4 | 19 | Đã xem XML và overlay ảnh gốc |
| A12 | 11 | 4 | 15 | Đã xem XML và overlay ảnh gốc |
| B02 | 9 | 4 | 13 | Đã xem XML và overlay ảnh gốc |
| B03 | 22 | 4 | 26 | Đã xem XML và overlay ảnh gốc |
| B06 | 10 | 4 | 14 | Đã xem XML và overlay ảnh gốc |

Chưa thể chỉ định một ảnh "không lỗi tuyệt đối" khi chưa có GT. A01 không có lỗi xác định trong lần rà này sau khi ghi ngoại lệ vạch đôi, nhưng vẫn chưa chứng minh độ lệch 5 px.

Phần lỗi trên là kết quả tối thiểu đã xác định, không dùng số cảnh báo lint chia cho số ảnh để tính tỉ lệ. Không gửi tin, không giả chữ ký hoặc lời xác nhận của Khánh.

## Định danh file đã kiểm
| File | SHA256 |
| --- | --- |
| nguyenbaokhanh-front.zip | `deb722daf2b7a5dfbf09b21d6f7be8e95cca74a87f5d958f5e31126946816fa0` |
| nguyenbaokhanh-fisheye.zip | `0c68fa12f8465a45b33428943bd382f35b5b97d2b917de47673b48eb6382baec` |

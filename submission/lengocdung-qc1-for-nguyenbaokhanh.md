# Phiếu QC 1 — Road v1.0

**Lô được kiểm (học viên):** Nguyễn Bảo Khánh<br>
**Người kiểm (học viên):** Lê Ngọc Dũng — 2A202603103<br>
**Ngày kiểm:** 21/11/2026<br>
**Phiên bản guideline:** Road v1.0, kèm hướng dẫn giảng viên về cách vẽ vạch đôi<br>
**File được kiểm:** `nguyenbaokhanh-front.zip`, `nguyenbaokhanh-fisheye.zip`<br>
**Revision của lô Khánh:** chưa được cung cấp manifest; hai file được định danh bằng SHA256 tại cuối phiếu.<br>
**Số ảnh kiểm:** 6 ảnh bắt buộc — A01, A06, A12, B02, B03, B06; **0 ảnh thêm**.<br>
**Số nhãn đã kiểm (shape + tag): 103**.

Tôi sử dụng trợ lý AI hỗ trợ đọc XML, dựng ảnh đối chiếu và soạn phiếu. Kết quả dưới đây dựa trên file và ảnh gốc của lô Khánh, không lấy bài Dũng làm GT. Không có GT để xác nhận phép đo độ lệch tối đa 5 px; số 0 trong bảng nghĩa là chưa phát hiện lỗi xác định trong phạm vi kiểm, không phải chứng nhận mọi nhãn khớp GT.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
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

**Đơn vị kiểm:** QC1-01 là 6 tag camera; QC1-02 là 8 phía L1/R1 của A01/A06/A12 và B03 (không bắt buộc vẽ khi không có vạch thật). QC1-03–06 đếm lane; QC1-07 đếm drivable/curb/crosswalk; QC1-08 đếm đèn; QC1-09 đếm đèn và biển; QC1-10 đếm biển; QC1-11 đếm shape của 3 ảnh fisheye; QC1-12 đếm ZIP. Một nhãn có thể được kiểm theo nhiều mã, nhưng mẫu số tỉ lệ chỉ đếm shape + tag một lần.

## Danh sách lỗi (mỗi lỗi một dòng)

| # | Mã | Ảnh | Nhãn (label, định vị trong XML) | Mức | Mô tả ngắn / đề nghị sửa |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A12 | `lane`: thiếu L1; XML chỉ có R1 (#6) | nặng | Phía trái làn có vạch sơn nhìn thấy nhưng chưa có polyline L1. Bổ sung L1 theo tâm vạch, từ gần ra xa. |
| 2 | QC1-06 | A06 | `lane` #14, bắt đầu khoảng (441.2; 416.5) | chính | Đường đặt trên vạch trắng nhưng `color=yellow`. Sửa `white` và kiểm lại `style` theo các đoạn sơn thật. |
| 3 | QC1-09 | A06 | `traffic_sign` #2, hộp khoảng (660;214)–(709;240) | chính | Biển ONE WAY đang `group=supplementary`. Theo bảng nhóm biển trong docs, biển bắt buộc hướng đi thuộc `mandatory`. |

Các số # là thứ tự shape do parser đọc từ XML, không phải ID giao diện CVAT. Tọa độ trên ảnh gốc giúp xác định đúng đối tượng khi ID thay đổi.

## Ca mơ hồ và xác nhận

| Ảnh | Câu hỏi cho lead | Lời đáp / xử lý |
| --- | --- | --- |
| A01 | Hai polyline của vạch đôi có được giữ? | Giảng viên cho phép hai lane, mỗi đường `kind=double`; không tính cảnh báo trùng L2 này thành lỗi. |
| A06 | Không thấy R1 có phải vẽ thêm không? | Coach đã xác nhận ngoại lệ không thấy vạch ở cảnh A06; không vẽ vạch giả. Không đưa ca này vào lỗi QC1-02 xác định. |
| A12 | Crosswalk nhìn thấy nhưng không có polygon có thuộc nhóm nhãn yêu cầu cho ảnh không? | Chưa có bảng kế hoạch riêng từng ảnh trong docs; chờ lead đối chiếu, chưa cộng thêm lỗi bỏ sót này. |
| B03 | Position của lane khi nhìn bằng camera sau | Ghi nhận để lead đối chiếu quy ước; chưa chấm thêm lỗi position từ suy đoán. |
| B06 | Phân biệt lane, vạch cạnh ray/đảo và vùng alternative | Chờ lead đối chiếu chức năng phần đường; không tự chuyển nhãn. |

**Ghi chú ngoại lệ cùng bộ ảnh:** coach đã xác nhận không thấy vạch tại A05 (L1/R1), A06, A09 và A14 (R1), theo xác nhận của học viên ngày 21/11/2026. Mẫu 6 ảnh của phiếu này chỉ có A06 trong nhóm đó. Ngoại lệ không áp dụng cho L1 ở A12, vì vạch này nhìn thấy.

## Quyết định

- **Lỗi nặng:** 1.
- **Lỗi chính:** 2 / 103 nhãn = **1,94%**.
- **Lỗi nhẹ:** 0 lỗi xác định trong phạm vi kiểm.
- **Ca chờ lead:** 3 — A12 (phạm vi crosswalk), B03 và B06.
- **Quyết định: Rework.**

**Lý do:** còn một lỗi nặng QC1-02 ở A12 nên phải Rework, mặc dù tỉ lệ lỗi chính 1,94% không vượt 5%. Mẫu số là số nhãn đã kiểm, không phải số ảnh. Các ca mơ hồ không làm thay đổi kết luận Rework khi đã có lỗi nặng.

**Đề nghị xử lý:** Khánh bổ sung L1 tại A12, sửa màu lane và nhóm biển tại A06, sau đó export lại hai ZIP, tạo manifest có revision phù hợp và gửi kiểm lại. Phiếu này áp dụng cho hai file có SHA256 bên dưới, không tự kết luận bản sửa chưa nhận là đã đạt.

## Phạm vi và bằng chứng kiểm

| Ảnh | Shape | Tag | Tổng nhãn | Kết quả nổi bật |
| --- | ---: | ---: | ---: | --- |
| A01 | 12 | 4 | 16 | Chưa phát hiện lỗi xác định trong phạm vi đã rà; đã áp dụng hướng dẫn thầy về vạch đôi. |
| A06 | 15 | 4 | 19 | Hai lỗi chính: màu lane và nhóm biển ONE WAY. |
| A12 | 11 | 4 | 15 | Một lỗi nặng: thiếu L1 nhìn thấy. |
| B02 | 9 | 4 | 13 | Đã rà XML/ảnh; chưa khẳng định độ lệch 5 px khi không có GT. |
| B03 | 22 | 4 | 26 | Có ca position camera sau chờ lead. |
| B06 | 10 | 4 | 14 | Có ca chức năng vạch/vùng lái chờ lead. |
| **Tổng** | **79** | **24** | **103** | |

A01 là ảnh không ghi nhận lỗi xác định để coach chọn đối chiếu; nhận xét này giới hạn trong phạm vi kiểm nêu trên, không thay cho chấm GT. Ba lỗi trong danh sách có đủ mã, ảnh, nhãn, mức và vị trí để kiểm lại.

## Định danh file đã kiểm

| File | SHA256 |
| --- | --- |
| `nguyenbaokhanh-front.zip` | `deb722daf2b7a5dfbf09b21d6f7be8e95cca74a87f5d958f5e31126946816fa0` |
| `nguyenbaokhanh-fisheye.zip` | `0c68fa12f8465a45b33428943bd382f35b5b97d2b917de47673b48eb6382baec` |

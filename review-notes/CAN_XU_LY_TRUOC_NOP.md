# Biên bản chốt và các điểm cần coach đối chiếu

## Đã xử lý và nguồn xác nhận
- Đã sửa position A12 tại điểm (663.34,417.41): L1 → R2 trong ZIP nộp mới. Không đổi tọa độ. File Export/CVAT chưa được ghi đè bởi trợ lý.
- Theo thông báo mới của Dũng, các job đã completed. Lưu nguồn xác nhận trong nhat-ky-chot-bai.json.
- Dũng thông báo Khánh đã xác nhận phiếu. Phiếu lịch sử được lưu với nguồn xác nhận, giữ kết luận trước sửa; không tự ghi Release của bản ZIP mới.

## Hướng dẫn thầy về vạch đôi
Theo lời học viên Lê Ngọc Dũng truyền đạt ngày 21/11/2026: thầy hướng dẫn vạch đôi vẫn vẽ hai polyline lane và đặt kind=double trên cả hai. Áp dụng cho bài này; chưa có thông báo văn bản của thầy trong thư mục. Không coi đây là thay đổi chính thức của Road v1.0 cho các bài khác. Không tự gộp hoặc xóa hai đường đôi.

Áp dụng được cho 4 cảnh báo: A01 L2, A04 L1, A11 L1, A14 L1. Không gộp lane đôi. A08/A12/A13/A15 kind=single cần rà riêng.

## Những điều chưa tự coi là đạt
- 5 cảnh báo thiếu L1/R1 ở A05 (2), A06, A09, A14: cần xác nhận coach nếu không thấy vạch. Không tạo vạch giả.
- 8 gợi ý edge_zone: B02 (1), B03 (4), B04 (1), B05 (2).
- B09 có 1 lane chỉ 3 điểm, kiểm độ cong thực tế.
- A12 thiếu polygon crosswalk nhìn thấy: đối chiếu bảng kế hoạch trước khi kết luận bỏ sót.
- A06 đèn người đi bộ còn off; hình trắng cần kiểm lại trước khi chốt màu.

## Lint bản nộp cuối
| Mức | Mã | Ảnh | Đối tượng | Nội dung |
| --- | --- | --- | --- | --- |
| chính | QC1-05 | A01 | lane | 2 polyline cùng position L2: vạch đứt có bị tách không? |
| chính | QC1-05 | A04 | lane | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| nặng | QC1-02 | A05 | lane | chưa có L1 (bỏ qua nếu thật sự không thấy vạch) |
| nặng | QC1-02 | A05 | lane | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| nặng | QC1-02 | A06 | lane | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| chính | QC1-05 | A08 | lane | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| nặng | QC1-02 | A09 | lane | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| chính | QC1-05 | A11 | lane | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| chính | QC1-05 | A13 | lane | 2 polyline cùng position R1: vạch đứt có bị tách không? |
| nặng | QC1-02 | A14 | lane | chưa có R1 (bỏ qua nếu thật sự không thấy vạch) |
| chính | QC1-05 | A14 | lane | 2 polyline cùng position L1: vạch đứt có bị tách không? |
| chính | QC1-05 | A15 | lane | 2 polyline cùng position R1: vạch đứt có bị tách không? |
| chính | QC1-11 | B02 | traffic_light#5@(1074,78) | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B03 | traffic_sign#1@(1129,360) | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B03 | traffic_sign#14@(172,300) | gợi ý edge_zone = tắt (tâm box trong 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B03 | traffic_sign#15@(260,292) | gợi ý edge_zone = tắt (tâm box trong 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B03 | traffic_sign#16@(263,304) | gợi ý edge_zone = tắt (tâm box trong 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B04 | traffic_light#3@(1068,240) | gợi ý edge_zone = tắt (tâm box trong 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B05 | traffic_sign#1@(420,5) | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B05 | traffic_sign#6@(353,39) | gợi ý edge_zone = bật (tâm box ngoài 80 % bán kính; tự kiểm lại) |
| chính | QC1-11 | B09 | lane#4@(558,386) | chỉ 3 điểm: trên fisheye hãy đặt điểm theo cung |

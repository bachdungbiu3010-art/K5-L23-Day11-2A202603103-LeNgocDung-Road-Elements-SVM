# Báo cáo cá nhân — Ngày 11
Họ tên: **Lê Ngọc Dũng** — Mã học viên: **2A202603103**.  
Phiên bản CVAT: **Server 2.82.0 / UI 2.82.0**, đã xem About trực tiếp ngày 21/11/2026.  
Guideline: Road v1.0; áp dụng hướng dẫn bổ sung về vạch đôi do học viên truyền đạt.  
Lần nộp trong manifest: **revision 1 — bản chuẩn bị chưa nộp**. Số lần nộp lại sau Rework chính thức: chưa xác minh; các lần kiểm cục bộ không được tính là lần nộp.

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đã xác minh | Project d11-road-lengocdung #12 có lane, road_curb, crosswalk, drivable, traffic_light, traffic_sign. |
| Thuộc tính và giá trị | Đã xác minh về schema; còn ca ngữ nghĩa | Đã kiểm XML; các lỗi vị trí và ca khó ghi ở mục 3–4. |
| 4 tag ảnh | Đã xác minh | 28/28 ảnh đủ camera/timeofday/weather/source; camera khớp tên ảnh. |
| Job completed | Học viên đã xác nhận | Lê Ngọc Dũng thông báo đã chuyển các job sang completed ngày 21/11/2026; ảnh trạng thái cũ không được dùng thay bằng chứng mới. |
Cách kết thúc polyline: phím N theo hướng dẫn docs.  
Cách đặt tag: công cụ Tag, chọn một trong 4 label, thêm tag một lần/ảnh và sửa thuộc tính value trong Details.

**Hướng dẫn riêng về vạch đôi:** Theo lời học viên Lê Ngọc Dũng truyền đạt ngày 21/11/2026: thầy hướng dẫn vạch đôi vẫn vẽ hai polyline lane và đặt kind=double trên cả hai. Áp dụng cho bài này; chưa có thông báo văn bản của thầy trong thư mục. Không coi đây là thay đổi chính thức của Road v1.0 cho các bài khác. Không tự gộp hoặc xóa hai đường đôi.

Đã đối chiếu XML: A01 L2, A04 L1, A11 L1 và A14 L1 có hai polyline và đều kind=double. Giữ nguyên theo hướng dẫn; log lint gốc vẫn lưu cảnh báo trùng, không sửa checker để giấu cảnh báo. Các trường hợp kind=single ở A08/A13/A15 vẫn được ghi để rà riêng. A12 đã sửa position của đường bên phải từ L1 sang R2 trong bản nộp.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| fisheye-core | 8 | 13 | 21 | 10 | 8 | 10 | 11 |
| fisheye-extra | 4 | 3 | 3 | 4 | 4 | 0 | 0 |
| front-core | 12 | 35 | 10 | 2 | 23 | 38 | 36 |
| front-extra | 4 | 12 | 1 | 2 | 12 | 16 | 15 |

Tổng: **28 ảnh, 289 shape, 112 tag**. A13–A16 và B09–B12 đều có trong file; B11 có tag nhưng không có shape do ảnh chủ yếu là ô đỗ. Việc có file không đồng nghĩa đã đạt chất lượng hoặc được thưởng.

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn / trạng thái | Lý do |
| --- | --- | --- | --- | --- |
| A01/A04/A11/A14 | lane đôi | Một hay hai polyline | Giữ hai, kind=double cả hai | Theo hướng dẫn thầy do học viên truyền đạt; không áp dụng ngoại lệ cho đường single. |
| A05 | lane L1/R1 | Không có vạch / bỏ sót | Không tự thêm lane; chờ coach xác nhận | Ảnh không thấy vạch sơn rõ, hai bên có xe đỗ; còn 2 cảnh báo QC1-02. |
| A06/A09/A14 | R1 | Mép đường / vạch sơn | Chờ coach | Còn 3 cảnh báo thiếu R1; không lấy bó vỉa thay lane. |
| A12 | lane bên phải | L1 / R2 | Đã sửa thành R2 trong bản nộp | Giữ nguyên tọa độ, chỉ sửa position; ZIP nguồn/CVAT chưa được ghi đè bởi trợ lý. |
| B11 | Ô đỗ khuyết tật | Vạch ô đỗ / lane | Không có shape | Docs: ô đỗ ngoài phạm vi, vạch ô đỗ không gán lane; cần coach xác nhận không có vạch làn bị bỏ sót. |
| B02/B03/B04/B05 | đèn/biển | edge_zone | Còn 8 gợi ý checker | Dựa tâm box và quy ước bán kính lab; cần rà cả ảnh. |
| B06 | drivable/lane | Vùng cùng chiều, ray, đảo, crosswalk | Chờ lead đối chiếu | Không tự suy từ camera trái sang alternative. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm chéo xác nhận: **Nguyễn Bảo Khánh**.  
Khánh đã xác nhận nội dung phiếu QC theo thông báo của Lê Ngọc Dũng ngày 21/11/2026. Phiếu được trợ lý hỗ trợ đối chiếu XML/ảnh và soạn; không có chữ ký hay nhận xét cá nhân do trợ lý giả lập.

Mẫu kiểm bài Dũng gồm 6 ảnh A01/A06/A12/B02/B03/B06, tổng 96 nhãn (shape+tag). Bản kiểm trước sửa ghi 1 lỗi nặng QC1-03 ở A12 và các ca chờ lead, kết luận Rework. Sau đó đã sửa position L1 → R2 trong ZIP nộp mới. Chưa có bằng chứng Khánh kiểm lại chính bản ZIP sau sửa, nên không tự ghi Release cho bản mới.

| Mã lỗi / việc | Kết quả xử lý | Trạng thái |
| --- | --- | --- |
| QC1-03: lane A12 phía phải mang L1 | Sửa thành R2, giữ tọa độ | Đã kiểm trong ZIP nộp cục bộ; chưa đồng bộ lại CVAT bởi trợ lý |
| Tag A05/A13/A16; position B05/B06 | Đã sửa trong các bản xuất cập nhật | Đã xác minh XML |
| QC1-04: chiều lane A12/A14 | Không còn cảnh báo chiều trong bản cuối | Đã kiểm bằng script |
| Vạch đôi | Giữ hai lane, cả hai double theo hướng dẫn thầy | Ghi chú riêng, không xóa cảnh báo checker |
| Phiếu Khánh xác nhận | Xác nhận do Dũng thông báo | Đã cập nhật nguồn xác nhận, không giả chữ ký |

Tôi kiểm bài Khánh trên cùng 6 ảnh, tổng 103 nhãn: ghi nhận tối thiểu 1 lỗi nặng và 2 lỗi chính; phiếu kèm bài là lengocdung-qc1-for-nguyenbaokhanh.md. Không dùng bài Dũng làm GT cho Khánh.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| lengocdung-front.zip | Có; ZIP/XML hợp lệ | A01: chưa đối chiếu job / 10 | A02: chưa đối chiếu job / 8 | Có mọi ảnh |
| lengocdung-fisheye.zip | Có; ZIP/XML hợp lệ | B01: chưa đối chiếu job / 6 | B02: chưa đối chiếu job / 11 | Có mọi ảnh |

Hai ZIP gộp từ core+extra, không kèm ảnh. Giữ toàn bộ tọa độ; chỉ đánh lại image id và sửa một thuộc tính position ở A12 (L1 → R2) trong bản nộp mới. File Export gốc giữ nguyên. Đã kiểm các node còn lại và SHA256 manifest. Cần áp dụng cùng thay đổi vào CVAT nếu xuất lại từ đó.

**Lint bản nộp: 21 cảnh báo — 16 chính, 5 nặng.** 4 cảnh báo trùng được chú thích theo hướng dẫn vạch đôi; không xóa khỏi manifest. 5 cảnh báo thiếu L1/R1 cần coach xác nhận ngoại lệ. Còn các ca trùng single, edge_zone và B09 ít điểm cần rà. Không tự suy ra điểm rubric hoặc Release.

| ZIP nguồn | Thời điểm export từ CVAT (giờ Việt Nam) |
| --- | --- |
| lengocdung-fisheye-core.zip | 21/11/2026 11:20:15 |
| lengocdung-fisheye-extra.zip | 21/11/2026 11:19:44 |
| lengocdung-front-core.zip | 21/11/2026 11:20:27 |
| lengocdung-front-extra.zip | 21/11/2026 11:19:59 |

## 6. Minh chứng thực hành
Đã lưu riêng tại máy học viên: ảnh Labels project, ảnh About CVAT 2.82.0, ảnh đối chiếu front A01/fisheye B03 và trích XML thật. Không đưa ảnh dataset hoặc ảnh có dataset lên kho GitHub này theo quy tắc dữ liệu của bài.

Ảnh Labels/About được chụp trực tiếp; ảnh đối chiếu nhãn được dựng từ XML và ảnh gốc, không giả là ảnh chụp giao diện. Nếu coach yêu cầu minh chứng UI đầy đủ, học viên cung cấp qua kênh riêng được chỉ định. Bộ minh chứng cục bộ đi kèm hồ sơ bàn giao, chưa tự coi việc lưu ở máy là đã nộp ảnh cho coach.

Trích cấu trúc XML từ file nhãn thật (A01):
```xml
IMAGE: A01_bc5fadac-fa6dd225.jpg
<polyline label="lane" source="manual" occluded="0" points="107.22,720.00;284.53,570.44;315.89,544.24;336.88,525.95;346.97,518.24;358.60,509.80" z_order="0">
      <attribute name="position">L1</attribute>
      <attribute name="style">dashed</attribute>
      <attribute name="color">white</attribute>
      <attribute name="kind">single</attribute>
    </polyline>
    
```

## 7. Tự đánh giá
Tự đánh giá dựa trên quá trình thực hành và các lần kiểm:
- Tôi đã sửa các tag thiếu/sai camera, quy ước position=other ở camera hai bên, weather A05/A06 và chiều vẽ một số lane. Các sửa đã được đối chiếu trên những bản xuất liên tiếp, không coi trao đổi hướng dẫn là bằng chứng đã sửa.
- Các điểm tôi cần chú ý thêm là phân biệt vạch đôi với lane bị tách, phân biệt bó vỉa với vạch sơn, vùng lái không cắt theo xe, màu/hướng đèn và edge_zone.
- Ví dụ tác động tới model: A13 trước đây mang camera=fisheye_front dù là ảnh camera front; nhãn này làm dữ liệu bị phân nhóm sai. Tôi đã sửa camera=front. Ở bản nộp, tôi đã sửa nhầm position A12 từ L1 sang R2; nếu giữ sai, model có thể học nhầm phía của làn.
- Tôi dùng trợ lý AI để đọc guideline, tự kiểm định dạng, rà ảnh và soạn báo cáo/QC. Chưa có GT để tự xác nhận độ lệch 5 px hoặc điểm số.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Chưa thực hiện phép tính tay và so sánh với bạn kiểm; không điền số suy đoán. Phần này không tính điểm theo rubric.

---
**Trạng thái hồ sơ:** đã chuẩn bị đủ 5 file để bàn giao qua GitHub theo yêu cầu học viên. Khánh đã xác nhận phiếu và các job đã completed theo thông báo mới. Lỗi position A12 đã sửa trong bản nộp cục bộ. Các ca thiếu vạch và cảnh báo còn lại được công khai trong báo cáo, chưa tự coi là đã được coach miễn hoặc chấm đạt. GitHub là nơi bàn giao; chưa có xác nhận nộp LMS riêng.
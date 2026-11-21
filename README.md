# Bài nộp Ngày 11 — Lê Ngọc Dũng

Mã học viên: **2A202603103**. Guideline: **Road v1.0**, kèm hướng dẫn thầy về vạch đôi. Hoàn thiện hồ sơ ngày **21/11/2026**.

## Hồ sơ bàn giao

| File | Nội dung |
| --- | --- |
| [lengocdung-front.zip](submission/lengocdung-front.zip) | 16 ảnh A01–A16, CVAT for images 1.1, chỉ nhãn |
| [lengocdung-fisheye.zip](submission/lengocdung-fisheye.zip) | 12 ảnh B01–B12, CVAT for images 1.1, chỉ nhãn |
| [lengocdung-manifest.json](submission/lengocdung-manifest.json) | Revision 1, số lượng và SHA256 |
| [lengocdung-qc1-for-nguyenbaokhanh.md](submission/lengocdung-qc1-for-nguyenbaokhanh.md) | QC 6 ảnh bài Nguyễn Bảo Khánh, 103 nhãn |
| [lengocdung-report.md](submission/lengocdung-report.md) | Báo cáo cá nhân và phản hồi QC |

Hai ZIP không chứa ảnh. Bộ nhãn có **28 ảnh, 289 shape, 112 tag**. Bản nộp đã sửa position một lane bên phải A12 từ L1 sang R2; các tọa độ giữ nguyên. File xuất gốc lưu tại máy học viên.

**Hướng dẫn vạch đôi:** theo thông tin học viên truyền đạt từ thầy, giữ hai polyline lane, mỗi đường `kind=double`. Các cảnh báo tương ứng được chú thích, không xóa log.

Khánh đã xác nhận phiếu và các job đã completed theo thông báo của học viên. Phiếu được trợ lý hỗ trợ soạn, nguồn xác nhận được ghi rõ; không tạo chữ ký giả. Phiếu xác nhận lưu lịch sử trước khi sửa A12; chưa tự ghi Release cho bản ZIP sau sửa.

**Giới hạn còn công khai:** lint còn 21 cảnh báo (5 nặng về thiếu vạch, 16 chính), trong đó 4 cảnh báo trùng liên quan vạch đôi đã có ghi chú hướng dẫn thầy. Các ca thật sự không thấy L1/R1 cần coach xác nhận, không vẽ vạch giả để làm sạch lint. Chưa có GT/điểm chấm chính thức. Xem [biên bản chốt](review-notes/CAN_XU_LY_TRUOC_NOP.md).

Ảnh dataset và minh chứng có ảnh dataset lưu cục bộ, cung cấp qua kênh coach được chỉ định; không đưa vào repo. Việc bàn giao GitHub không tự chứng minh đã bấm nộp trên LMS.

---

# Ngày 11 · Road Elements & SVM

> Lab cá nhân, AI20K K5. Bạn gán nhãn phần tử đường theo guideline Road v1.0 trên CVAT của lớp: 12 ảnh camera trước BDD100K (A01–A12) và 8 ảnh fisheye WoodScape (B01–B08) là bắt buộc. Sau đó bạn kiểm lô của một bạn khác bằng Phiếu QC 1 và quyết định Release, Hold hoặc Rework. Nếu xong sớm, làm thêm ảnh A13–A16 và B09–B12 để lấy điểm thưởng. Không đưa ảnh lên app.cvat.ai.

| M | Giờ | Việc | Lệnh kiểm tra |
| --- | --- | --- | --- |
| M0 | 13:00 | Điểm danh. Kiểm repo, gói 28 ảnh trong `data/`, đăng nhập CVAT và guideline đã đọc. | `PYTHONPATH=src python3 -m road_lab.road_check selftest` |
| Task 0 | 13:15 | Mở project `d11-road-<tên>`, so sáu label và bốn label Tag với guideline. | `PYTHONPATH=src python3 -m road_lab.taxonomy` (in Raw labels JSON để so) |
| Task 1 | 13:50 | Gán A01–A12, mỗi ảnh theo trọng tâm của nó; xong thì làm A13–A16. | — |
| Task 2 | 15:05 | Gán B01–B08; xong thì làm B09–B12. Dành 5 phút cuối để self-QC. | — |
| Task 3 | 15:40 | Đổi lô với bạn được ghép, điền Phiếu QC 1 ([`templates/qc1_form.md`](templates/qc1_form.md)). | — |
| Export | 16:15 | Export CVAT for images 1.1 (không kèm ảnh), mở lại rồi nộp. | `PYTHONPATH=src python3 -m road_lab.road_check lint <tên>-front.zip <tên>-fisheye.zip` |
| Buffer | 16:35 | Sửa lô theo phiếu nhận được. Tùy chọn: hoạt động row-anchor. | `PYTHONPATH=src python3 -m road_lab.rowanchor <tên>-front.zip --image A01` |

## Cài đặt

Chỉ cần Python 3.11 trở lên; code chỉ dùng thư viện chuẩn. Muốn chạy test thì cài thêm pytest.

```bash
git pull
ls data/ | wc -l          # phải là 28: A01…A16, B01…B12
PYTHONPATH=src python3 -m road_lab.road_check selftest   # in SELFTEST PASS
```

Nếu dùng uv:

```bash
uv run --with pytest==8.3.4 pytest -q
```

## Tài liệu

- [Guideline Road v1.0](docs/guideline_road_v1.0.md): đọc trước buổi, ít nhất là bảng label và quy tắc làn.
- [Hướng dẫn bằng hình trên CVAT](docs/huong_dan_cvat_bang_hinh.md): từng bước từ đăng nhập tới export, chụp trên ảnh tổng hợp.
- [Đặc tả bàn giao](docs/delivery_road_v1.0.md): định dạng file nộp, manifest, nộp lại sau Rework.
- [Thang mức lỗi QC 1](docs/qc_severity_road_v1.0.md): tiêu chí nặng / chính / nhẹ và nguồn tham khảo.
- [Mẫu Phiếu QC 1](templates/qc1_form.md) và [mẫu báo cáo](templates/report.md).
- [Rubric](RUBRIC.md), [checkpoint](CHECKPOINTS.md), [nộp bài](SUBMISSION.md).
- [`lab/AGENTS.md`](lab/AGENTS.md): bản máy đọc của guideline, mô tả input/output của script.
- [Nguồn dữ liệu và giấy phép](ATTRIBUTION.md).

`lint` chỉ kiểm định dạng file. Nó không so bài của bạn với GT và không cho điểm. Coach chấm bằng `road_check check` hoặc `road_check batch` sau buổi.

# M05 - Thống kê số liệu học viên nhập học

## 1. Thông tin chung

| Thuộc tính | Nội dung |
|---|---|
| Mã báo cáo | `M05` theo tên file `docs/report-input/M05.xlsx`. `[Cần xác nhận]` Trong file Excel ô `K1:L1` ghi `Biểu mẫu 7H`, nên cần xác nhận mã chính thức là `M05`, `7H`, hay cả hai. |
| Tên báo cáo trên template | `THỐNG KÊ SỐ LIỆU HỌC VIÊN NHẬP HỌC`. |
| Sheet | `Bieu mau 7H`. |
| Phân hệ nghiệp vụ | Báo cáo/thống kê; liên quan trực tiếp đến tuyển sinh và quản lý học viên. |
| Mục đích nghiệp vụ | `[Suy luận]` Thống kê số lượng học viên nhập học theo trình độ/hình thức/loại hình đào tạo, so sánh chỉ tiêu với thực nhập, phân tách theo đối tượng nhập học và thành phần học viên. |
| Kỳ báo cáo | Template có dòng “Kèm theo Báo cáo số: /BC-T06-P1, ngày tháng 6 năm 2025”. `[Cần xác nhận]` Đây là kỳ/năm báo cáo cố định của mẫu hay chỉ là dữ liệu mẫu. |
| Template hiện có | `docs/report-input/M05.xlsx`. |
| Template trong BCTK source | Chưa tìm thấy `template_m05.xlsx`; thư mục BCTK hiện có `template_m04.xlsx` và `test-report.xlsx`. |
| UI hiện có | Có menu report `tong-hop-hoc-vien-nhap-hoc`, nhưng trang report trả “Chưa có nội dung báo cáo” vì chưa có component riêng cho slug này. |
| API hiện có | Backend BCTK có API export chung `/api/report/get-bao-cao?maBaoCao&exportType`; dữ liệu trong `ReportService` mới có case `m04`, chưa thấy case `m05`. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `src/frontend-x02-v2/src/domains/reports/reports.registry.js`
- `src/frontend-x02-v2/src/domains/reports/pages/ReportPage.jsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/templates/reports/`

## 2. Layout Excel

### 2.1. Cấu trúc workbook

| Thành phần | Giá trị tìm thấy |
|---|---|
| Số sheet | 1 |
| Tên sheet | `Bieu mau 7H` |
| Vùng dữ liệu | `A1:L47` |
| Freeze pane | Không có |
| Công thức Excel | Chưa tìm thấy công thức trong các ô có dữ liệu của workbook. |
| Độ rộng cột | `A=5`, `B=38`, `C:D=9`, `E:L=8` |

Các vùng gộp ô:

| Vùng merge | Ý nghĩa |
|---|---|
| `A1:B2` | Tên đơn vị lập báo cáo: `BỘ CÔNG AN / TRƯỜNG ĐẠI HỌC PCCC`. |
| `E1:H1` | Tên báo cáo. |
| `E2:H2` | Dòng thông tin văn bản kèm theo báo cáo. |
| `K1:L1` | Mã biểu mẫu `Biểu mẫu 7H`. |
| `A4:A6`, `B4:B6`, `C4:C6`, `D4:D6` | Các cột cố định: TT, nhóm đào tạo, chỉ tiêu, thực nhập. |
| `E4:J4` | Nhóm `Đối tượng nhập học`. |
| `E5:I5` | Nhóm con `Trong ngành`. |
| `J5:J6` | Cột `Ngoài ngành`. |
| `K4:L5` | Nhóm `Thành phần`. |
| `B47:D47` | Chữ ký `CÁN BỘ THỐNG KÊ`. |
| `H47:L47` | Chữ ký `HIỆU TRƯỞNG`. |

Nguồn source:
- `docs/report-input/M05.xlsx`

### 2.2. Header và cột báo cáo

| Cột Excel | Tiêu đề | Nhóm nghiệp vụ | Ghi chú mapping |
|---|---|---|---|
| A | TT | Thứ tự dòng báo cáo | Dữ liệu tĩnh theo template. |
| B | Trình độ, hình thức, loại hình đào tạo | Nhóm đào tạo | Mapping sang trình độ/hình thức/loại hình đào tạo trong danh mục. |
| C | Chỉ tiêu | Chỉ tiêu tuyển sinh | `[Suy luận]` Nguồn gần nhất là `CHI_TIEU_TUYEN_SINH_CHI_TIET.TONG_SO`. |
| D | Thực nhập | Học viên nhập học | `[Cần xác nhận]` Có thể lấy từ `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC` hoặc đếm bản ghi `HOC_VIEN` có `NGAY_NHAP_HOC`. |
| E | Cán bộ | Đối tượng nhập học trong ngành | `[Cần mapping danh mục]` Có thể liên quan mã `CBCS`, `CBCC` trong `DM_DOI_TUONG_NHAP_HOC`. |
| F | CSNV | Đối tượng nhập học trong ngành | `[Suy luận]` Có thể là chiến sĩ nghĩa vụ, mã `NVQS`. |
| G | HSPT | Đối tượng nhập học trong ngành | `[Suy luận]` Có thể là học sinh phổ thông/thí sinh tốt nghiệp THPT, mã `HS`, `TSVH`. |
| H | BQP | Đối tượng nhập học trong ngành | Có mã `BQP` trong `DM_DOI_TUONG_NHAP_HOC`. `[Cần xác nhận]` BQP có được xếp trong nhóm “Trong ngành” như template không. |
| I | Ngành khác | Đối tượng nhập học trong ngành | Có mã `NK` trong `DM_DOI_TUONG_NHAP_HOC`. `[Cần xác nhận]` |
| J | Ngoài ngành | Đối tượng nhập học ngoài ngành | `[Cần mapping danh mục]` Chưa thấy quy tắc xác định ngoài ngành trong DB. |
| K | Nữ | Thành phần | Nguồn gần nhất là `CON_NGUOI.GIOI_TINH = 'NU'`. |
| L | Dân tộc thiểu số | Thành phần | Nguồn gần nhất là `CON_NGUOI.DAN_TOC_ID` nối `DM_DAN_TOC`. `[Cần mapping danh mục]` Cần xác định mã dân tộc Kinh hoặc tập mã dân tộc thiểu số. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

### 2.3. Các dòng dữ liệu trong template

| Dòng Excel | TT | Nội dung dòng |
|---:|---|---|
| 8 |  | Tổng |
| 9 | 1 | Đào tạo trình độ sau đại học |
| 10 | 1.1 | Tiến sĩ |
| 11 | 1.2 | Thạc sĩ |
| 12 | 2 | Đào tạo trình độ đại học hệ chính quy |
| 13 | 3 | Đào tạo hệ liên thông |
| 14 | 3.1 | Đào tạo tại trường Công an nhân dân |
| 15 |  | - Hình thức chính quy |
| 16 |  | + Trung cấp lên Đại học |
| 17 |  | + Cao đẳng lên Đại học |
| 18 |  | - Hình thức vừa làm vừa học |
| 19 |  | + Trung cấp lên Đại học |
| 20 |  | + Cao đẳng lên Đại học |
| 21 | 4 | Đào tạo trình độ đại học hệ hình thức vừa làm vừa học |
| 22 | 4.1 | Đào tạo tại trường Công an nhân dân |
| 23 | 5 | Đào tạo hệ cử tuyển |
| 24 |  | Đại học |
| 25 |  | Trung cấp |
| 26 | 6 | Đào tạo cấp bằng đại học thứ 2 |
| 27 |  | - Đào tạo tại trường |
| 28 |  | + Chính quy |
| 29 |  | + Vừa làm vừa học |
| 30 |  | - Đào tạo liên kết mở tại Công an các đơn vị, địa phương |
| 31 | 7 | Đào tạo trình độ trung cấp |
| 32 | 8 | Các loại hình đào tạo khác |
| 33 | 8.1 | Đào tạo lý luận chính trị |
| 34 |  | - Đào tạo trung cấp lý luận chính trị |
| 35 |  | - Đào tạo cao cấp lý luận chính trị |
| 36 | 8.2 | Đào tạo hệ dân sự |
| 37 |  | + Đại học chính quy |
| 38 |  | + Trung cấp chính quy |
| 39 |  | + Vừa bằng hai dân sự |
| 40 |  | + Liên thông dân sự |
| 41 |  | + Đại học VLVH dân sự |
| 42 | 8.3 | Lái xe ô tô chữa cháy |
| 43 | 8.4 | Vận hành, sử dụng ô tô, máy bơm chữa cháy |
| 44 | 9 | Các loại hình bồi dưỡng |
| 47 |  | Khu vực chữ ký |

Nguồn source:
- `docs/report-input/M05.xlsx`

## 3. Đối chiếu phân hệ nghiệp vụ

| Thành phần báo cáo | Phân hệ liên quan | Nguồn dữ liệu gần nhất | Nhận xét nghiệp vụ |
|---|---|---|---|
| Nhóm trình độ/hình thức/loại hình đào tạo | Danh mục đào tạo, quản lý học viên, tuyển sinh | `DM_TRINH_DO_DAO_TAO`, `DM_HINH_THUC_DAO_TAO`, `DM_LOAI_HINH_DAO_TAO`, `HOC_VIEN` | DB có đủ cột trình độ/hình thức/loại hình trên `HOC_VIEN`; bảng chỉ tiêu tuyển sinh có trình độ và hình thức nhưng chưa thấy `LOAI_HINH_DAO_TAO_ID`. |
| Chỉ tiêu | Tuyển sinh | `CHI_TIEU_TUYEN_SINH`, `CHI_TIEU_TUYEN_SINH_CHI_TIET` | Có `TONG_SO`, `CHI_TIEU_NAM`, `CHI_TIEU_NU`. |
| Thực nhập | Tuyển sinh, quản lý học viên | `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC`; `HOC_VIEN.NGAY_NHAP_HOC` | `[Cần xác nhận]` Chọn nguồn số liệu chính thức: số tổng hợp tuyển sinh hay bản ghi học viên sau nhập học. |
| Đối tượng nhập học | Quản lý học viên, danh mục dùng chung | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID`, `DM_DOI_TUONG_NHAP_HOC` | Có danh mục đối tượng như `CBCS`, `NVQS`, `HS`, `TSVH`, `BQP`, `NK`, nhưng chưa có mapping chính thức vào các cột E:J. |
| Thành phần nữ | Hồ sơ nhân thân | `HOC_VIEN.CON_NGUOI_ID`, `CON_NGUOI.GIOI_TINH` | Có cột giới tính trên bảng nhân thân. |
| Thành phần dân tộc thiểu số | Hồ sơ nhân thân, danh mục dân tộc | `CON_NGUOI.DAN_TOC_ID`, `DM_DAN_TOC` | `[Cần mapping danh mục]` Cần xác định mã dân tộc Kinh để loại trừ hoặc danh sách dân tộc thiểu số để tính. |
| Đơn vị lập báo cáo | Danh mục đơn vị, phân quyền đơn vị | `MA_DON_VI`, `CO_SO_DAO_TAO_ID`, `DM_DON_VI_SD_PM` | Template hard-code `TRƯỜNG ĐẠI HỌC PCCC`. `[Cần xác nhận]` Có render động theo đơn vị đăng nhập không. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/output/database-business-analysis.md`

## 4. Bộ lọc báo cáo

| Bộ lọc | Bắt buộc | Mapping đề xuất | Căn cứ source | Ghi chú |
|---|---|---|---|---|
| `maBaoCao` | Có | `m05` hoặc `M05` | API BCTK hiện nhận `maBaoCao`; `ReportService` dùng `m04` dạng chữ thường. | `[Cần xác nhận]` Quy ước viết hoa/thường. |
| `exportType` | Có khi export | `HTML`, `EXCEL`, `PDF` | `ReportService.parseOutputType`. | Source hiện hỗ trợ 3 giá trị này. |
| Năm tuyển sinh | Nên có | `NAM_TUYEN_SINH.ID` hoặc `NAM_TUYEN_SINH.NAM` | DB có bảng `NAM_TUYEN_SINH`. | `[Cần xác nhận]` Báo cáo theo năm tuyển sinh hay năm nhập học. |
| Năm nhập học | Nên có | `EXTRACT(YEAR FROM HOC_VIEN.NGAY_NHAP_HOC)` | DB có `HOC_VIEN.NGAY_NHAP_HOC`. | `[Cần xác nhận]` Dòng kèm báo cáo ghi năm 2025, không đủ để xác định rule. |
| Đơn vị/cơ sở đào tạo | Nên có | `HOC_VIEN.MA_DON_VI`, `HOC_VIEN.CO_SO_DAO_TAO_ID`, `CHI_TIEU_TUYEN_SINH.CO_SO_DAO_TAO_ID` | DB có các cột đơn vị/cơ sở đào tạo. | `[Cần xác nhận]` Dùng mã đơn vị hay cơ sở đào tạo làm bộ lọc chính. |
| Trạng thái duyệt | Nên có | `WORKFLOW_STATUS`, `TRANG_THAI`, `ROW_STATE`, `IS_ACTIVE`, `IS_DELETED` | Các bảng nghiệp vụ có nhóm cột workflow/audit. | `[Suy luận]` Báo cáo chính thức nên lấy bản ghi hiệu lực/đã duyệt. |

Nguồn source:
- `docs/database/X02_APP.sql`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`

## 5. Mapping trường dữ liệu

| Cột báo cáo | Ý nghĩa | Mapping DB đề xuất | Quy tắc tính |
|---|---|---|---|
| `TT` | Số thứ tự dòng | Không lấy DB | Theo template. |
| `Trình độ, hình thức, loại hình đào tạo` | Nhóm thống kê | `DM_TRINH_DO_DAO_TAO.MA/TEN`, `DM_HINH_THUC_DAO_TAO.MA/TEN`, `DM_LOAI_HINH_DAO_TAO.MA/TEN` | Dòng template cần bảng mapping riêng giữa dòng Excel và mã danh mục. |
| `Chỉ tiêu` | Tổng chỉ tiêu được giao | `CHI_TIEU_TUYEN_SINH_CHI_TIET.TONG_SO`; join `CHI_TIEU_TUYEN_SINH` theo `CHI_TIEU_TUYEN_SINH_ID` | `SUM(TONG_SO)` theo năm/đơn vị/nhóm đào tạo. |
| `Thực nhập` | Số học viên nhập học thực tế | Nguồn 1: `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC`. Nguồn 2: `COUNT(HOC_VIEN.ID)` với `NGAY_NHAP_HOC` không rỗng. | `[Cần xác nhận]` Chọn nguồn chuẩn. Nếu cần phân tách E:L thì `HOC_VIEN` phù hợp hơn vì có đối tượng, giới tính, dân tộc. |
| `Cán bộ` | Học viên là cán bộ | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID -> DM_DOI_TUONG_NHAP_HOC` | `[Cần mapping danh mục]` Có thể gồm `CBCS`, `CBCC`; chưa có rule chính thức. |
| `CSNV` | Chiến sĩ nghĩa vụ | `DM_DOI_TUONG_NHAP_HOC.MA = 'NVQS'` | `[Suy luận]` Từ tên danh mục “Chiến sĩ thực hiện nghĩa vụ tham gia CAND”. |
| `HSPT` | Học sinh phổ thông/thí sinh THPT | `DM_DOI_TUONG_NHAP_HOC.MA IN ('HS','TSVH')` | `[Suy luận]` Từ tên danh mục `Học sinh phổ thông`, `Thí sinh vừa tốt nghiệp THPT`. |
| `BQP` | Bộ Quốc phòng | `DM_DOI_TUONG_NHAP_HOC.MA = 'BQP'` | Có mã danh mục `BQP`. |
| `Ngành khác` | Ngành khác | `DM_DOI_TUONG_NHAP_HOC.MA = 'NK'` | Có mã danh mục `NK`. |
| `Ngoài ngành` | Ngoài ngành Công an | Chưa tìm thấy cột/rule riêng | `[Cần xác nhận]` Có thể là nhóm mã ngoài CAND, quốc tế, dân sự hoặc một thuộc tính khác. |
| `Nữ` | Học viên nữ | `CON_NGUOI.GIOI_TINH = 'NU'` | Đếm trong tập học viên của dòng. |
| `Dân tộc thiểu số` | Học viên dân tộc thiểu số | `CON_NGUOI.DAN_TOC_ID -> DM_DAN_TOC` | `[Cần mapping danh mục]` Đếm dân tộc khác Kinh hoặc theo danh sách khách hàng xác nhận. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 6. Mapping dòng báo cáo

| Dòng | Nội dung | Mapping danh mục/điều kiện đề xuất |
|---:|---|---|
| 8 | Tổng | `[Suy luận]` Tổng tất cả dòng nhóm chính có dữ liệu; cần tránh cộng trùng dòng cha/con. `[Cần xác nhận]` |
| 9 | Đào tạo trình độ sau đại học | `[Suy luận]` `DM_TRINH_DO_DAO_TAO.MA IN ('TS','THS')`. |
| 10 | Tiến sĩ | `DM_TRINH_DO_DAO_TAO.MA = 'TS'`. |
| 11 | Thạc sĩ | `DM_TRINH_DO_DAO_TAO.MA = 'THS'`. |
| 12 | Đào tạo trình độ đại học hệ chính quy | `[Suy luận]` `DM_TRINH_DO_DAO_TAO.MA = 'DH'` và `DM_HINH_THUC_DAO_TAO.MA = 'CQ'`. |
| 13 | Đào tạo hệ liên thông | `[Suy luận]` `DM_HINH_THUC_DAO_TAO.MA = 'LT'`. `[Cần xác nhận]` Có cần giới hạn trình độ đại học không. |
| 14 | Đào tạo tại trường Công an nhân dân | `[Cần xác nhận]` Chưa thấy rule xác định “tại trường CAND”; có thể dùng `CO_SO_DAO_TAO_ID` hoặc `MA_DON_VI`. |
| 15 | Hình thức chính quy | `[Suy luận]` Trong nhóm liên thông, thêm `DM_HINH_THUC_DAO_TAO.MA = 'CQ'`; tuy nhiên `Liên thông` đã là một hình thức riêng trong danh mục. `[Cần xác nhận]` |
| 16 | Trung cấp lên Đại học | `[Cần xác nhận]` DB hiện thấy trình độ hiện tại trên `HOC_VIEN`, chưa thấy cột trình độ đầu vào/nguồn liên thông để phân biệt trung cấp lên đại học. |
| 17 | Cao đẳng lên Đại học | `[Cần xác nhận]` Tương tự dòng 16, cần trường nguồn trình độ đầu vào. |
| 18 | Hình thức vừa làm vừa học | `[Suy luận]` `DM_HINH_THUC_DAO_TAO.MA = 'VLVH'`, trong nhóm liên thông nếu nghiệp vụ cho phép. |
| 19 | Trung cấp lên Đại học | `[Cần xác nhận]` Cần mapping trình độ đầu vào. |
| 20 | Cao đẳng lên Đại học | `[Cần xác nhận]` Cần mapping trình độ đầu vào. |
| 21 | Đào tạo trình độ đại học hệ hình thức vừa làm vừa học | `DM_TRINH_DO_DAO_TAO.MA = 'DH'` và `DM_HINH_THUC_DAO_TAO.MA = 'VLVH'`. |
| 22 | Đào tạo tại trường Công an nhân dân | `[Cần xác nhận]` Dùng đơn vị/cơ sở đào tạo nào để xác định “tại trường”. |
| 23 | Đào tạo hệ cử tuyển | `[Cần xác nhận]` Chưa tìm thấy danh mục/cột “cử tuyển” rõ trong các nguồn đã đọc. |
| 24 | Đại học | `[Suy luận]` Dòng con của cử tuyển với `DM_TRINH_DO_DAO_TAO.MA = 'DH'`; thiếu điều kiện cử tuyển. |
| 25 | Trung cấp | `[Suy luận]` Dòng con của cử tuyển với `DM_TRINH_DO_DAO_TAO.MA = 'TC'`; thiếu điều kiện cử tuyển. |
| 26 | Đào tạo cấp bằng đại học thứ 2 | `DM_HINH_THUC_DAO_TAO.MA = 'VB2'` hoặc nhóm mã `VB2AN`, `VB2CS`. `[Cần xác nhận]` |
| 27 | Đào tạo tại trường | `[Cần xác nhận]` Cần rule theo `CO_SO_DAO_TAO_ID`/`MA_DON_VI`. |
| 28 | Chính quy | `[Suy luận]` Dòng con của văn bằng 2, có thể thêm `DM_HINH_THUC_DAO_TAO.MA = 'CQ'`; danh mục hiện cũng có `VB2` riêng nên cần xác nhận cách mã hóa. |
| 29 | Vừa làm vừa học | `[Suy luận]` Dòng con của văn bằng 2, có thể thêm `DM_HINH_THUC_DAO_TAO.MA = 'VLVH'`; cần xác nhận cách mã hóa. |
| 30 | Đào tạo liên kết mở tại Công an các đơn vị, địa phương | `[Suy luận]` Có thể liên quan `DM_LOAI_HINH_DAO_TAO.MA = 'LK'` hoặc `DM_HINH_THUC_DAO_TAO.MA = 'LKQT'`; cần xác nhận. |
| 31 | Đào tạo trình độ trung cấp | `DM_TRINH_DO_DAO_TAO.MA = 'TC'`. |
| 32 | Các loại hình đào tạo khác | `[Cần xác nhận]` Nhóm tổng hợp nhiều loại hình ngoài các nhóm trên. |
| 33 | Đào tạo lý luận chính trị | `[Cần xác nhận]` DB có bảng tuyển sinh LLCT `TS_LLCT_TC`, `TS_LLCT_CC`, nhưng chưa thấy bảng học viên/đào tạo LLCT để thống kê nhập học. |
| 34 | Đào tạo trung cấp lý luận chính trị | `[Cần xác nhận]` Có thể liên quan `TS_LLCT_TC`. |
| 35 | Đào tạo cao cấp lý luận chính trị | `[Cần xác nhận]` Có thể liên quan `TS_LLCT_CC`. |
| 36 | Đào tạo hệ dân sự | `[Cần xác nhận]` Chưa thấy cột/danh mục xác định hệ dân sự trong `HOC_VIEN`. |
| 37 | Đại học chính quy | `[Suy luận]` `DH + CQ` trong nhóm dân sự; thiếu điều kiện dân sự. |
| 38 | Trung cấp chính quy | `[Suy luận]` `TC + CQ` trong nhóm dân sự; thiếu điều kiện dân sự. |
| 39 | Vừa bằng hai dân sự | `[Cần xác nhận]` Có thể là “Văn bằng hai dân sự”; cần xác nhận tên dòng và mapping `VB2`. |
| 40 | Liên thông dân sự | `[Suy luận]` `LT` trong nhóm dân sự; thiếu điều kiện dân sự. |
| 41 | Đại học VLVH dân sự | `[Suy luận]` `DH + VLVH` trong nhóm dân sự; thiếu điều kiện dân sự. |
| 42 | Lái xe ô tô chữa cháy | Chưa tìm thấy bảng/cột mapping trực tiếp trong nguồn đã đọc. `[Cần xác nhận]` |
| 43 | Vận hành, sử dụng ô tô, máy bơm chữa cháy | Chưa tìm thấy bảng/cột mapping trực tiếp trong nguồn đã đọc. `[Cần xác nhận]` |
| 44 | Các loại hình bồi dưỡng | `[Suy luận]` Có thể liên quan `DM_HINH_THUC_DAO_TAO.MA = 'BD'` hoặc `DM_LOAI_HINH_DAO_TAO.MA = 'BD'`; cần xác nhận nguồn bồi dưỡng chính thức. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 7. Công thức tính và kiểm tra đối soát

### 7.1. Công thức tính đề xuất

| Chỉ số | Công thức nghiệp vụ đề xuất |
|---|---|
| Chỉ tiêu | `SUM(CHI_TIEU_TUYEN_SINH_CHI_TIET.TONG_SO)` theo năm tuyển sinh, đơn vị/cơ sở đào tạo và mapping dòng báo cáo. |
| Thực nhập | `[Cần xác nhận]` Cách 1: `SUM(KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC)`. Cách 2: `COUNT(HOC_VIEN.ID)` theo `NGAY_NHAP_HOC`, trạng thái hiệu lực và mapping dòng báo cáo. |
| Cán bộ/CSNV/HSPT/BQP/Ngành khác/Ngoài ngành | `COUNT(HOC_VIEN.ID)` theo `DM_DOI_TUONG_NHAP_HOC.MA` sau khi khách hàng xác nhận mapping mã danh mục. |
| Nữ | `COUNT(HOC_VIEN.ID)` với `CON_NGUOI.GIOI_TINH = 'NU'`. |
| Dân tộc thiểu số | `COUNT(HOC_VIEN.ID)` với dân tộc thuộc tập dân tộc thiểu số. `[Cần mapping danh mục]` |
| Dòng tổng/nhóm cha | `[Suy luận]` Cộng các dòng con có cùng phạm vi; không cộng trùng dòng cha và dòng con. |

### 7.2. Kiểm tra đối soát

| STT | Kiểm tra | Ý nghĩa |
|---:|---|---|
| 1 | `Thực nhập = Cán bộ + CSNV + HSPT + BQP + Ngành khác + Ngoài ngành` | Đảm bảo các nhóm đối tượng nhập học phủ hết thực nhập. `[Cần xác nhận]` Nếu một học viên có nhiều nhóm hoặc nhóm ngoài ngành không lấy từ cùng danh mục, công thức cần đổi. |
| 2 | `Nữ <= Thực nhập` và `Dân tộc thiểu số <= Thực nhập` | Thành phần là tập con của học viên thực nhập. |
| 3 | Dòng `Tổng` bằng tổng các dòng nhóm chính | Tránh cộng trùng dòng cha/con. |
| 4 | `Thực nhập` từ `HOC_VIEN` đối chiếu với `SL_TONG_SO_NHAP_HOC` từ tuyển sinh | Kiểm tra chênh lệch giữa số liệu tổng hợp tuyển sinh và dữ liệu học viên đã nhập học. |
| 5 | Chỉ lấy bản ghi `IS_DELETED = 0`, `IS_ACTIVE = 1`, `ROW_STATE = 'ACTIVE'` nếu có | `[Suy luận]` Báo cáo chính thức nên loại dữ liệu xóa mềm/vô hiệu. |
| 6 | Chỉ lấy bản ghi đã duyệt | `[Cần xác nhận]` Có dùng `WORKFLOW_STATUS`/`TRANG_THAI` để chỉ lấy dữ liệu duyệt không. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 8. SQL/Stored procedure Oracle đề xuất

Đây là khung đề xuất dựa trên bảng/cột tìm thấy trong source. Các điều kiện dòng chưa rõ được để trong `ROW_MAP` và cần BA/khách hàng xác nhận trước khi đưa vào production.

```sql
CREATE OR REPLACE PROCEDURE X02_APP.PRC_BC_M05_HV_NHAP_HOC (
    p_nam_tuyen_sinh_id IN VARCHAR2,
    p_nam_nhap_hoc      IN NUMBER,
    p_ma_don_vi         IN VARCHAR2,
    p_result            OUT SYS_REFCURSOR
) AS
BEGIN
    OPEN p_result FOR
    WITH row_map AS (
        SELECT 8 row_no, NULL stt, 'Tổng' ten_dong, NULL td_ma, NULL ht_ma, NULL lh_ma, 'TOTAL' row_type FROM dual
        UNION ALL SELECT 9, '1', 'Đào tạo trình độ sau đại học', NULL, NULL, NULL, 'SAU_DAI_HOC' FROM dual
        UNION ALL SELECT 10, '1.1', 'Tiến sĩ', 'TS', NULL, NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 11, '1.2', 'Thạc sĩ', 'THS', NULL, NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 12, '2', 'Đào tạo trình độ đại học hệ chính quy', 'DH', 'CQ', NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 13, '3', 'Đào tạo hệ liên thông', NULL, 'LT', NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 21, '4', 'Đào tạo trình độ đại học hệ hình thức vừa làm vừa học', 'DH', 'VLVH', NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 26, '6', 'Đào tạo cấp bằng đại học thứ 2', NULL, 'VB2', NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 31, '7', 'Đào tạo trình độ trung cấp', 'TC', NULL, NULL, 'DETAIL' FROM dual
        UNION ALL SELECT 44, '9', 'Các loại hình bồi dưỡng', NULL, 'BD', NULL, 'DETAIL' FROM dual
    ),
    hv_base AS (
        SELECT
            hv.ID,
            td.MA AS td_ma,
            ht.MA AS ht_ma,
            lh.MA AS lh_ma,
            dtnh.MA AS doi_tuong_ma,
            cn.GIOI_TINH,
            dt.MA AS dan_toc_ma,
            dt.TEN AS dan_toc_ten
        FROM X02_APP.HOC_VIEN hv
        LEFT JOIN X02_APP.CON_NGUOI cn
            ON cn.ID = hv.CON_NGUOI_ID
        LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td
            ON td.ID = hv.TRINH_DO_DAO_TAO_ID
        LEFT JOIN X02_DM.DM_HINH_THUC_DAO_TAO ht
            ON ht.ID = hv.HINH_THUC_DAO_TAO_ID
        LEFT JOIN X02_DM.DM_LOAI_HINH_DAO_TAO lh
            ON lh.ID = hv.LOAI_HINH_DAO_TAO_ID
        LEFT JOIN X02_DM.DM_DOI_TUONG_NHAP_HOC dtnh
            ON dtnh.ID = hv.DOI_TUONG_NHAP_HOC_ID
        LEFT JOIN X02_DM.DM_DAN_TOC dt
            ON dt.ID = cn.DAN_TOC_ID
        WHERE hv.IS_DELETED = 0
          AND hv.IS_ACTIVE = 1
          AND (p_ma_don_vi IS NULL OR hv.MA_DON_VI = p_ma_don_vi)
          AND (p_nam_nhap_hoc IS NULL OR EXTRACT(YEAR FROM hv.NGAY_NHAP_HOC) = p_nam_nhap_hoc)
    ),
    hv_agg AS (
        SELECT
            rm.row_no,
            COUNT(hv.ID) AS thuc_nhap,
            SUM(CASE WHEN hv.doi_tuong_ma IN ('CBCS', 'CBCC') THEN 1 ELSE 0 END) AS can_bo,
            SUM(CASE WHEN hv.doi_tuong_ma = 'NVQS' THEN 1 ELSE 0 END) AS csnv,
            SUM(CASE WHEN hv.doi_tuong_ma IN ('HS', 'TSVH') THEN 1 ELSE 0 END) AS hspt,
            SUM(CASE WHEN hv.doi_tuong_ma = 'BQP' THEN 1 ELSE 0 END) AS bqp,
            SUM(CASE WHEN hv.doi_tuong_ma = 'NK' THEN 1 ELSE 0 END) AS nganh_khac,
            SUM(CASE WHEN hv.doi_tuong_ma IN ('QT') THEN 1 ELSE 0 END) AS ngoai_nganh,
            SUM(CASE WHEN hv.GIOI_TINH = 'NU' THEN 1 ELSE 0 END) AS nu,
            SUM(CASE
                    WHEN hv.dan_toc_ma IS NOT NULL
                     AND UPPER(hv.dan_toc_ten) <> 'KINH'
                    THEN 1 ELSE 0
                END) AS dan_toc_thieu_so
        FROM row_map rm
        LEFT JOIN hv_base hv
          ON (rm.td_ma IS NULL OR hv.td_ma = rm.td_ma)
         AND (rm.ht_ma IS NULL OR hv.ht_ma = rm.ht_ma)
         AND (rm.lh_ma IS NULL OR hv.lh_ma = rm.lh_ma)
        WHERE rm.row_type IN ('DETAIL', 'SAU_DAI_HOC')
        GROUP BY rm.row_no
    ),
    chi_tieu_base AS (
        SELECT
            td.MA AS td_ma,
            ht.MA AS ht_ma,
            SUM(ctct.TONG_SO) AS chi_tieu
        FROM X02_APP.CHI_TIEU_TUYEN_SINH ct
        JOIN X02_APP.CHI_TIEU_TUYEN_SINH_CHI_TIET ctct
            ON ctct.CHI_TIEU_TUYEN_SINH_ID = ct.ID
        LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td
            ON td.ID = ct.TRINH_DO_DAO_TAO_ID
        LEFT JOIN X02_DM.DM_HINH_THUC_DAO_TAO ht
            ON ht.ID = ct.HINH_THUC_DAO_TAO_ID
        WHERE ct.IS_DELETED = 0
          AND ct.IS_ACTIVE = 1
          AND ctct.IS_DELETED = 0
          AND ctct.IS_ACTIVE = 1
          AND (p_nam_tuyen_sinh_id IS NULL OR ct.NAM_TUYEN_SINH_ID = p_nam_tuyen_sinh_id)
          AND (p_ma_don_vi IS NULL OR ct.MA_DON_VI = p_ma_don_vi)
        GROUP BY td.MA, ht.MA
    ),
    chi_tieu_agg AS (
        SELECT
            rm.row_no,
            SUM(cb.chi_tieu) AS chi_tieu
        FROM row_map rm
        LEFT JOIN chi_tieu_base cb
          ON (rm.td_ma IS NULL OR cb.td_ma = rm.td_ma)
         AND (rm.ht_ma IS NULL OR cb.ht_ma = rm.ht_ma)
        WHERE rm.row_type IN ('DETAIL', 'SAU_DAI_HOC')
        GROUP BY rm.row_no
    )
    SELECT
        rm.row_no,
        rm.stt,
        rm.ten_dong,
        NVL(ct.chi_tieu, 0) AS chi_tieu,
        NVL(hv.thuc_nhap, 0) AS thuc_nhap,
        NVL(hv.can_bo, 0) AS can_bo,
        NVL(hv.csnv, 0) AS csnv,
        NVL(hv.hspt, 0) AS hspt,
        NVL(hv.bqp, 0) AS bqp,
        NVL(hv.nganh_khac, 0) AS nganh_khac,
        NVL(hv.ngoai_nganh, 0) AS ngoai_nganh,
        NVL(hv.nu, 0) AS nu,
        NVL(hv.dan_toc_thieu_so, 0) AS dan_toc_thieu_so
    FROM row_map rm
    LEFT JOIN hv_agg hv ON hv.row_no = rm.row_no
    LEFT JOIN chi_tieu_agg ct ON ct.row_no = rm.row_no
    ORDER BY rm.row_no;
END;
/
```

Ghi chú quan trọng:

- SQL trên mới minh họa các dòng có mapping tương đối rõ theo danh mục đã thấy. Các dòng 14-20, 22-25, 27-30, 32-43 cần mapping nghiệp vụ chi tiết.
- Điều kiện `ngoai_nganh = 'QT'` chỉ là `[Suy luận]` để minh họa kỹ thuật; chưa đủ căn cứ để dùng thật.
- Điều kiện dân tộc thiểu số bằng `TEN <> 'KINH'` là `[Suy luận]`; cần dùng mã danh mục chuẩn sau khi xác nhận.
- Nếu chọn nguồn `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC` làm số thực nhập chính thức, cần thêm mapping từ kết quả tuyển sinh sang dòng báo cáo và không thể tách E:L nếu bảng tổng hợp không lưu đối tượng/giới tính/dân tộc.

Nguồn source:
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 9. API đề xuất

### 9.1. Theo API BCTK hiện có

| Hạng mục | Đề xuất |
|---|---|
| Export Excel | `GET /api/report/get-bao-cao?maBaoCao=m05&exportType=EXCEL` |
| Export PDF | `GET /api/report/get-bao-cao?maBaoCao=m05&exportType=PDF` |
| Preview HTML | `GET /api/report/get-bao-cao?maBaoCao=m05&exportType=HTML` |
| Template config | Thêm bản ghi cấu hình cho `m05` trong nơi BCTK đọc `TemplateConfig`. Source dùng entity `TEMPLATE_CONFIGS`; DB docs hiện chưa thấy bảng này, chỉ thấy `MD_CONFIG_TEM`. `[Cần xác nhận]` |
| Data source | Thêm case `m05` trong `ReportService.getData` hoặc chuyển sang cơ chế chạy SQL/procedure từ config. |

### 9.2. Tham số nghiệp vụ đề xuất

| Tham số | Ý nghĩa | Mapping |
|---|---|---|
| `namTuyenSinhId` | Năm tuyển sinh | `NAM_TUYEN_SINH.ID`, `CHI_TIEU_TUYEN_SINH.NAM_TUYEN_SINH_ID`, `KET_QUA_TUYEN_SINH.NAM_TUYEN_SINH_ID`. |
| `namNhapHoc` | Năm nhập học | `EXTRACT(YEAR FROM HOC_VIEN.NGAY_NHAP_HOC)`. |
| `maDonVi` | Đơn vị lập báo cáo | `MA_DON_VI` trên bảng nghiệp vụ. |
| `coSoDaoTaoId` | Cơ sở đào tạo | `HOC_VIEN.CO_SO_DAO_TAO_ID`, `CHI_TIEU_TUYEN_SINH.CO_SO_DAO_TAO_ID`. |
| `workflowStatus` | Trạng thái duyệt | `[Cần xác nhận]` Có lọc `APPROVED`/`Submitted`/`Draft` không. |

Nguồn source:
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/entities/TemplateConfig.java`
- `src/bctk-v2/src/main/resources/application.yml`
- `docs/database/X02_APP.sql`

## 10. Gaps và câu hỏi cần xác nhận

| STT | Vấn đề cần xác nhận | Mức độ ảnh hưởng | Câu hỏi đề xuất |
|---:|---|---|---|
| 1 | Mã báo cáo chính thức | Cao | Báo cáo này dùng mã `M05`, `Biểu mẫu 7H`, hay cả hai? |
| 2 | Nguồn số liệu thực nhập | Cao | Số “Thực nhập” lấy theo kết quả tuyển sinh tổng hợp hay đếm hồ sơ học viên đã nhập học? |
| 3 | Bộ lọc thời gian | Cao | Báo cáo chạy theo năm tuyển sinh, năm nhập học, năm học, hay ngày ban hành báo cáo? |
| 4 | Mapping đối tượng nhập học E:J | Cao | Cán bộ, CSNV, HSPT, BQP, Ngành khác, Ngoài ngành tương ứng với mã nào trong `DM_DOI_TUONG_NHAP_HOC`? |
| 5 | Khái niệm “Trong ngành/Ngoài ngành” | Cao | “Ngoài ngành” được xác định theo đối tượng nhập học, đơn vị, hệ dân sự, hay một thuộc tính riêng? |
| 6 | Mapping dòng liên thông | Cao | Trung cấp lên Đại học và Cao đẳng lên Đại học lấy từ cột nào, vì `HOC_VIEN` hiện chỉ thấy trình độ hiện tại? |
| 7 | Mapping hệ cử tuyển | Cao | Hệ cử tuyển được lưu ở bảng/cột/danh mục nào? |
| 8 | Mapping hệ dân sự | Cao | Hệ dân sự được xác định bằng `LOAI_HOC_VIEN`, đối tượng nhập học, đơn vị, hay danh mục khác? |
| 9 | Mapping LLCT | Trung bình | Dòng lý luận chính trị dùng dữ liệu từ `TS_LLCT_TC/TS_LLCT_CC` hay bảng học viên/chương trình khác? |
| 10 | Mapping bồi dưỡng/lái xe/vận hành máy bơm | Trung bình | Các dòng 42-44 lấy từ phân hệ bồi dưỡng nào và mã danh mục nào? |
| 11 | Điều kiện trạng thái dữ liệu | Cao | Báo cáo chỉ lấy bản ghi đã duyệt/đã khóa hay lấy toàn bộ bản ghi hiệu lực? |
| 12 | Đơn vị hiển thị trên đầu báo cáo | Trung bình | `BỘ CÔNG AN / TRƯỜNG ĐẠI HỌC PCCC` là cố định cho mẫu này hay render theo đơn vị đăng nhập? |
| 13 | Bảng cấu hình template | Trung bình | BCTK dùng `TEMPLATE_CONFIGS` riêng hay dùng metadata `MD_CONFIG_TEM` trong schema X02_APP? |
| 14 | Công thức tổng | Cao | Dòng tổng cộng theo các dòng cha hay chỉ cộng các dòng lá để tránh double count? |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `src/frontend-x02-v2/src/domains/reports/reports.registry.js`
- `src/frontend-x02-v2/src/domains/reports/pages/ReportPage.jsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`

## 11. Kết luận mức độ sẵn sàng

| Hạng mục | Đánh giá |
|---|---|
| Template Excel | Có template nghiệp vụ rõ bố cục, header, nhóm cột và danh sách dòng. |
| UI | Có menu/slug báo cáo nhưng chưa có nội dung màn hình. |
| API export | Có khung API export chung nhưng chưa thấy cấu hình/data source cho `m05`. |
| Database nguồn | Có bảng ứng viên/học viên/chỉ tiêu/kết quả tuyển sinh và danh mục liên quan; thiếu mapping dòng báo cáo chính thức. |
| Stored procedure/query | Chưa tìm thấy trong source hiện tại; tài liệu này đề xuất khung procedure. |
| Mức độ có thể đưa vào SRS | Có thể dùng làm bản phân tích nền cho SRS, nhưng cần chốt mapping đối tượng, mapping dòng đào tạo và nguồn “Thực nhập” trước khi đặc tả DEV. |

Nguồn source:
- `docs/report-input/M05.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `src/frontend-x02-v2/src/domains/reports/reports.registry.js`
- `src/frontend-x02-v2/src/domains/reports/pages/ReportPage.jsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/entities/TemplateConfig.java`

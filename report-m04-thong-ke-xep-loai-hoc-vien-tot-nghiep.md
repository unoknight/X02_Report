# M04 - Thống kê xếp loại học viên tốt nghiệp

## 1. Thông tin chung

| Thuộc tính | Nội dung |
|---|---|
| Mã báo cáo | `M04` theo file `docs/report-input/M04.xlsx`; trong source BCTK đang xử lý bằng mã `m04`. Người dùng gọi “mẫu 4M”. `[Cần xác nhận]` Mã chính thức là `M04`, `4M`, hay cả hai. |
| Tên báo cáo trên template | `THỐNG KÊ XẾP LOẠI HỌC VIÊN TỐT NGHIỆP`. |
| Sheet template input | `Bao cao`. |
| Phân hệ nghiệp vụ | Báo cáo/thống kê; liên quan trực tiếp đến quản lý học viên tốt nghiệp và quyết định công nhận tốt nghiệp. |
| Mục đích nghiệp vụ | `[Suy luận]` Thống kê số học viên tốt nghiệp theo đơn vị đào tạo và nhóm xếp loại tốt nghiệp: Xuất sắc, Giỏi, Khá, Trung bình, Khác. |
| Kỳ báo cáo | Template hiển thị `(Năm học 2024 - 2025)`. `[Cần xác nhận]` Đây là kỳ báo cáo cố định trong mẫu hay phải render theo tham số người dùng. |
| Template hiện có | `docs/report-input/M04.xlsx`. |
| Template trong BCTK source | `src/bctk-v2/templates/reports/template_m04.xlsx`. |
| API hiện có | Backend BCTK có API export chung `/api/report/get-bao-cao?maBaoCao&exportType`; `ReportService` có case `m04`. |
| Nguồn dữ liệu hiện tại trong code | `ReportService.getDataBaoCaoM04()` đang trả `BaoCaoM04DTO.mock()`, dữ liệu random. Chưa thấy query/stored procedure thật cho M04 trong source hiện tại. |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`

## 2. Layout Excel

### 2.1. Template `docs/report-input/M04.xlsx`

| Thành phần | Giá trị tìm thấy |
|---|---|
| Số sheet | 1 |
| Tên sheet | `Bao cao` |
| Vùng dữ liệu | `A1:H17` |
| Freeze pane | Không có |
| Tiêu đề | Ô merge `A1:H1`: `THỐNG KÊ XẾP LOẠI HỌC VIÊN TỐT NGHIỆP` |
| Kỳ báo cáo | Ô merge `A2:H2`: `(Năm học 2024 - 2025)` |
| Dòng header | Từ dòng 4 đến dòng 6 |
| Dòng dữ liệu | Dòng 7 đến dòng 17, tương ứng đơn vị `T01` đến `T11` |
| Công thức | Cột H có công thức tổng từng dòng: `=SUM(Cn:Gn)` |

Các vùng gộp ô chính:

| Vùng merge | Ý nghĩa |
|---|---|
| `A1:H1` | Tên báo cáo. |
| `A2:H2` | Năm học báo cáo. |
| `A4:A6` | Cột `TT`. |
| `B4:B6` | Cột `Đơn vị`. |
| `C4:G4` | Nhóm cột `Xếp loại`. |
| `C5:C6` | `Xuất sắc`. |
| `D5:D6` | `Giỏi`. |
| `E5:E6` | `Khá`. |
| `F5:F6` | `Trung bình`. |
| `G5:G6` | `Khác`. |
| `H4:H6` | `Tổng số`. |

Nguồn source:
- `docs/report-input/M04.xlsx`

### 2.2. Template BCTK `template_m04.xlsx`

| Thành phần | Giá trị tìm thấy |
|---|---|
| Sheet | `Sheet1` |
| Vùng dữ liệu | `A2:M14`, dữ liệu thật nằm chủ yếu trong `A2:G14`. |
| Header đơn vị | `BỘ CÔNG AN / Học viện ANND`. |
| Tiêu đề | `THỐNG KÊ XẾP LOẠI HỌC VIÊN TỐT NGHIỆP`. |
| Kỳ báo cáo | `(Năm học 2024 - 2025)`. |
| Smart marker dữ liệu | Dòng 13 dùng `&=RESPONSE.STT`, `&=RESPONSE.tenDonVi`, `&=RESPONSE.xuatSac`, `&=RESPONSE.gioi`, `&=RESPONSE.kha`, `&=RESPONSE.trungBinh`, `&=RESPONSE.khac`. |
| Dòng tổng | Dòng 14 có `Tổng số` và công thức `=SUM(C:C)` đến `=SUM(G:G)`. |

Điểm lệch giữa hai template:

| STT | Nội dung lệch | Nhận xét |
|---:|---|---|
| 1 | `docs/report-input/M04.xlsx` có cột H `Tổng số`; `template_m04.xlsx` không có cột H. | `[Cần xác nhận]` Chọn layout chính thức. |
| 2 | `docs/report-input/M04.xlsx` có sẵn 11 dòng đơn vị `T01` đến `T11`; `template_m04.xlsx` dùng smart marker để render danh sách động. | `[Cần xác nhận]` Báo cáo cần luôn đủ T01-T11 hay chỉ render đơn vị có dữ liệu. |
| 3 | `docs/report-input/M04.xlsx` tính tổng theo từng dòng; `template_m04.xlsx` tính tổng theo từng cột ở dòng cuối. | `[Cần xác nhận]` Có cần cả tổng dòng và tổng cột không. |
| 4 | Smart marker dùng `tenDonVi`, DTO dùng field `tenDonvi`. | `[Cần xác nhận]` Có nguy cơ binding sai tên thuộc tính khi render template. |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`

## 3. Header và mapping cột báo cáo

| Cột Excel | Tiêu đề | Ý nghĩa nghiệp vụ | Mapping source gần nhất |
|---|---|---|---|
| A | TT | Số thứ tự đơn vị trong báo cáo | `BaoCaoM04DTO.stt`; template input hard-code 1 đến 11. |
| B | Đơn vị | Đơn vị đào tạo/báo cáo, hiển thị dạng `T01` đến `T11` | `BaoCaoM04DTO.tenDonvi`; `DM_DON_VI_SD_PM.SO_HIEU_DON_VI`; `HV_QUYET_DINH_TOT_NGHIEP.MA_DON_VI`. |
| C | Xuất sắc | Số học viên tốt nghiệp loại Xuất sắc | Đếm `HV_QUYET_DINH_TOT_NGHIEP` theo lookup `xep_loai_tot_nghiep` = `Xuất sắc`. |
| D | Giỏi | Số học viên tốt nghiệp loại Giỏi | Đếm theo lookup `xep_loai_tot_nghiep` = `Giỏi`. |
| E | Khá | Số học viên tốt nghiệp loại Khá | Đếm theo lookup `xep_loai_tot_nghiep` = `Khá`. |
| F | Trung bình | Số học viên tốt nghiệp loại Trung bình | Đếm theo lookup `xep_loai_tot_nghiep` = `Trung bình`. |
| G | Khác | Số học viên tốt nghiệp thuộc nhóm xếp loại khác | `[Suy luận]` Các mã không thuộc 4 nhóm trên, ví dụ `Không đạt`; cần chốt rule. |
| H | Tổng số | Tổng số học viên tốt nghiệp theo đơn vị | Có trong `docs/report-input/M04.xlsx`, công thức `SUM(C:G)`; chưa có trong `template_m04.xlsx`. |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 4. Dòng đơn vị trong báo cáo

Template input có 11 dòng đơn vị:

| Dòng Excel | TT | Đơn vị trên báo cáo | Mapping danh mục tìm thấy |
|---:|---:|---|---|
| 7 | 1 | T01 | `DM_DON_VI_SD_PM`: `MA = G01.651`, `SO_HIEU_DON_VI = T01`, `TEN = Học viện An ninh nhân dân (T01)`. |
| 8 | 2 | T02 | `MA = G01.652`, `SO_HIEU_DON_VI = T02`, `TEN = Học viện Cảnh sát nhân dân (T02)`. |
| 9 | 3 | T03 | `MA = G01.653`, `SO_HIEU_DON_VI = T03`, `TEN = Học viện Chính trị Công an nhân dân (T03)`. |
| 10 | 4 | T04 | `MA = G01.654`, `SO_HIEU_DON_VI = T04`, `TEN = Trường Đại học An ninh nhân dân (T04)`. |
| 11 | 5 | T05 | `MA = G01.655`, `SO_HIEU_DON_VI = T05`, `TEN = Trường Đại học Cảnh sát nhân dân (T05)`. |
| 12 | 6 | T06 | `MA = G01.656`, `SO_HIEU_DON_VI = T06`, `TEN = Trường Đại học Phòng cháy, chữa cháy (T06)`. |
| 13 | 7 | T07 | `MA = G01.657`, `SO_HIEU_DON_VI = T07`, `TEN = Trường Đại học Kỹ thuật - Hậu cần Công an nhân dân (T07)`. |
| 14 | 8 | T08 | `MA = G01.658`, `SO_HIEU_DON_VI = T08`, `TEN = Trường Cao đẳng An ninh nhân dân I (T08)`. |
| 15 | 9 | T09 | `MA = G01.659`, `SO_HIEU_DON_VI = T09`, `TEN = Trường Cao đẳng Cảnh sát nhân dân I (T09)`. |
| 16 | 10 | T10 | `MA = G01.660`, `SO_HIEU_DON_VI = T10`, `TEN = Trường Cao đẳng Cảnh sát nhân dân II (T10)`. |
| 17 | 11 | T11 | `MA = G01.602.001`, `SO_HIEU_DON_VI = T11`, `TEN = Trường văn hóa Bộ công an (T11)`. |

Ghi chú:

- `BaoCaoM04DTO.mock()` hiện chỉ tạo 6 dòng và dòng thứ 6 vẫn là `T05`, không có `T06` đến `T11`. Đây là dữ liệu mock, chưa phản ánh template input.
- `[Cần xác nhận]` Có cần thêm `B06` không, vì `DM_DON_VI_SD_PM` cũng có `Học viên Quốc tế (B06)`, nhưng template input M04 chỉ có T01-T11.

Nguồn source:
- `docs/report-input/M04.xlsx`
- `docs/database/X02_DM.sql`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`

## 5. Đối chiếu phân hệ và bảng dữ liệu

| Thành phần báo cáo | Phân hệ liên quan | Bảng/source tìm thấy | Nhận xét nghiệp vụ |
|---|---|---|---|
| Học viên tốt nghiệp | Quản lý học viên tốt nghiệp | `HV_QUYET_DINH_TOT_NGHIEP` | Bảng có `HOC_VIEN_ID`, `QUYET_DINH_TOT_NGHIEP_ID`, `DIEM_TRUNG_BINH_CHUNG`, `XEP_LOAI_TOT_NGHIEP_ID`, `MA_DON_VI`. Đây là nguồn gần nhất cho M04. |
| Đơn vị | Danh mục đơn vị sử dụng phần mềm | `DM_DON_VI_SD_PM` | Có `MA`, `TEN`, `SO_HIEU_DON_VI`, `PHAN_LOAI`; có đủ T01-T11. |
| Xếp loại tốt nghiệp | Danh mục xếp loại kết quả tốt nghiệp | `MD_LOOKUP` code `xep_loai_tot_nghiep` trỏ tới `DM_PHAN_LOAI_KQ_TOT_NGHIEP` | Đây là mapping lookup trực tiếp của field `xep_loai_tot_nghiep_id` trong metadata import/config. |
| Học viên | Quản lý học viên | `HOC_VIEN` | `[Suy luận]` Dùng để nối chi tiết học viên nếu báo cáo cần kiểm tra đối tượng học viên, khóa học, cơ sở đào tạo. Với số liệu theo đơn vị, `HV_QUYET_DINH_TOT_NGHIEP.MA_DON_VI` đã có sẵn. |
| Văn bằng/chứng chỉ | Quản lý văn bằng, chứng chỉ | `HV_VAN_BANG_CHUNG_CHI` | Có `HANG_TOT_NGHIEP_ID`, `LOAI_TOT_NGHIEP_ID`, nhưng chưa thấy liên kết trực tiếp tới báo cáo M04. `[Cần xác nhận]` |
| Log thay đổi | Nhật ký thay đổi dữ liệu | `LICH_SU_THAY_DOI` | Có log cho `HV_QUYET_DINH_TOT_NGHIEP` với action `CREATE`, `SUBMIT`, `DELETE`. Không phải nguồn số liệu chính của báo cáo. |
| Thống kê metadata | Metadata object stats | `MD_OBJECT_STATS` | Có thống kê trạng thái theo object `quyet_dinh_tot_nghiep`. `[Suy luận]` Không dùng thay cho báo cáo nghiệp vụ M04 vì đây là thống kê kỹ thuật/metadata. |

Nguồn source:
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 6. Danh mục xếp loại tốt nghiệp

Lookup `xep_loai_tot_nghiep` trong `MD_LOOKUP` trỏ tới bảng `X02_DM.DM_PHAN_LOAI_KQ_TOT_NGHIEP`. Danh mục tìm thấy:

| Mã | Tên | Mapping cột báo cáo |
|---|---|---|
| `PLKQTN01` | Xuất sắc | Cột `Xuất sắc`. |
| `PLKQTN02` | Giỏi | Cột `Giỏi`. |
| `PLKQTN03` | Khá | Cột `Khá`. |
| `PLKQTN04` | Trung bình | Cột `Trung bình`. |
| `PLKQTN05` | Không đạt | `[Suy luận]` Cột `Khác`, vì template không có cột riêng cho `Không đạt`. `[Cần xác nhận]` |

Trong database còn có `DM_HANG_TOT_NGHIEP` và `DM_LOAI_TOT_NGHIEP`, nhưng metadata field `xep_loai_tot_nghiep_id` của `HV_QUYET_DINH_TOT_NGHIEP` đang dùng lookup `xep_loai_tot_nghiep`, nguồn `DM_PHAN_LOAI_KQ_TOT_NGHIEP`. Vì vậy M04 nên ưu tiên `DM_PHAN_LOAI_KQ_TOT_NGHIEP`.

Nguồn source:
- `docs/database/X02_DM.sql`
- `docs/database/X02_APP.sql`

## 7. Bộ lọc báo cáo

| Bộ lọc | Bắt buộc | Mapping hiện có | Ghi chú |
|---|---|---|---|
| `maBaoCao` | Có | `m04` | `ReportService.getData()` có case `m04`. |
| `exportType` | Có khi export | `HTML`, `EXCEL`, `PDF` | `ReportController` có default `HTML`; `ReportService.parseOutputType()` xử lý loại output. |
| Năm học | Chưa thấy tham số API | Template hiển thị `(Năm học 2024 - 2025)` | `[Cần xác nhận]` API hiện chưa nhận năm học, nên chưa có căn cứ source để lọc theo năm học. |
| Đơn vị | Chưa thấy tham số API | `HV_QUYET_DINH_TOT_NGHIEP.MA_DON_VI`; `DM_DON_VI_SD_PM.MA/SO_HIEU_DON_VI` | Template hiển thị toàn bộ T01-T11, không phải một đơn vị đơn lẻ. |
| Trạng thái duyệt | Chưa thấy tham số API | `WORKFLOW_STATUS`, ví dụ seed có `Draft`, `Submitted`, `Approved` | `[Cần xác nhận]` Báo cáo chính thức có lấy riêng bản ghi `Approved` hay lấy tất cả bản ghi hiệu lực. |
| Hiệu lực/xóa mềm | Nên có | `IS_DELETED`, `IS_ACTIVE`, `ROW_STATE` | `[Suy luận]` Báo cáo nghiệp vụ nên loại bản ghi xóa mềm và không hiệu lực. |

Nguồn source:
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `docs/database/X02_APP.sql`

## 8. Công thức tính và kiểm tra đối soát

### 8.1. Công thức tính đề xuất

| Chỉ số | Công thức nghiệp vụ đề xuất |
|---|---|
| Xuất sắc | Đếm `HV_QUYET_DINH_TOT_NGHIEP.ID` theo từng `MA_DON_VI`, có lookup `DM_PHAN_LOAI_KQ_TOT_NGHIEP.TEN = 'Xuất sắc'`. |
| Giỏi | Đếm tương tự với `TEN = 'Giỏi'`. |
| Khá | Đếm tương tự với `TEN = 'Khá'`. |
| Trung bình | Đếm tương tự với `TEN = 'Trung bình'`. |
| Khác | `[Suy luận]` Đếm các xếp loại không thuộc 4 nhóm trên, ví dụ `Không đạt`, hoặc bản ghi chưa mapping xếp loại. `[Cần xác nhận]` |
| Tổng số | Theo `docs/report-input/M04.xlsx`: `Xuất sắc + Giỏi + Khá + Trung bình + Khác`. |
| Tổng toàn báo cáo | Theo `template_m04.xlsx`: tổng cột C:G ở dòng cuối. `[Cần xác nhận]` Có cần thêm vào layout chính thức không. |

### 8.2. Kiểm tra đối soát

| STT | Kiểm tra | Ý nghĩa |
|---:|---|---|
| 1 | `Tổng số = Xuất sắc + Giỏi + Khá + Trung bình + Khác` | Đảm bảo không thiếu nhóm xếp loại trong từng đơn vị. |
| 2 | Tổng toàn báo cáo bằng tổng các đơn vị T01-T11 | Đảm bảo thống kê toàn hệ thống khớp với chi tiết theo đơn vị. |
| 3 | Chỉ lấy `IS_DELETED = 0`, `IS_ACTIVE = 1`, `ROW_STATE = 'ACTIVE'` nếu áp dụng | `[Suy luận]` Loại dữ liệu xóa mềm/không hiệu lực. |
| 4 | Quy tắc `WORKFLOW_STATUS` phải được thống nhất | Nếu chỉ lấy `Approved`, số liệu sẽ khác khi có bản ghi `Draft`/`Submitted`. |
| 5 | Mapping `XEP_LOAI_TOT_NGHIEP_ID` phải khớp `DM_PHAN_LOAI_KQ_TOT_NGHIEP.ID` | Tránh nhầm với `DM_HANG_TOT_NGHIEP` hoặc `DM_LOAI_TOT_NGHIEP`. |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 9. SQL/Stored procedure Oracle đề xuất

Đây là khung đề xuất dựa trên bảng/cột tìm thấy trong source. Các tham số thời gian và trạng thái cần khách hàng xác nhận trước khi đưa vào production.

```sql
CREATE OR REPLACE PROCEDURE X02_APP.PRC_BC_M04_XEP_LOAI_TN (
    p_from_date       IN DATE,
    p_to_date         IN DATE,
    p_workflow_status IN VARCHAR2,
    p_result          OUT SYS_REFCURSOR
) AS
BEGIN
    OPEN p_result FOR
    WITH unit_map AS (
        SELECT 1 stt, 'T01' so_hieu_don_vi, 'G01.651' ma_don_vi FROM dual UNION ALL
        SELECT 2, 'T02', 'G01.652' FROM dual UNION ALL
        SELECT 3, 'T03', 'G01.653' FROM dual UNION ALL
        SELECT 4, 'T04', 'G01.654' FROM dual UNION ALL
        SELECT 5, 'T05', 'G01.655' FROM dual UNION ALL
        SELECT 6, 'T06', 'G01.656' FROM dual UNION ALL
        SELECT 7, 'T07', 'G01.657' FROM dual UNION ALL
        SELECT 8, 'T08', 'G01.658' FROM dual UNION ALL
        SELECT 9, 'T09', 'G01.659' FROM dual UNION ALL
        SELECT 10, 'T10', 'G01.660' FROM dual UNION ALL
        SELECT 11, 'T11', 'G01.602.001' FROM dual
    ),
    graduate_base AS (
        SELECT
            qdtn.ID,
            qdtn.MA_DON_VI,
            xl.TEN AS xep_loai
        FROM X02_APP.HV_QUYET_DINH_TOT_NGHIEP qdtn
        LEFT JOIN X02_DM.DM_PHAN_LOAI_KQ_TOT_NGHIEP xl
            ON xl.ID = qdtn.XEP_LOAI_TOT_NGHIEP_ID
        WHERE qdtn.IS_DELETED = 0
          AND qdtn.IS_ACTIVE = 1
          AND qdtn.ROW_STATE = 'ACTIVE'
          AND (p_workflow_status IS NULL OR qdtn.WORKFLOW_STATUS = p_workflow_status)
          AND (p_from_date IS NULL OR TRUNC(qdtn.CREATED_AT) >= TRUNC(p_from_date))
          AND (p_to_date IS NULL OR TRUNC(qdtn.CREATED_AT) <= TRUNC(p_to_date))
    )
    SELECT
        u.stt,
        u.so_hieu_don_vi AS tenDonVi,
        SUM(CASE WHEN b.xep_loai = 'Xuất sắc' THEN 1 ELSE 0 END) AS xuatSac,
        SUM(CASE WHEN b.xep_loai = 'Giỏi' THEN 1 ELSE 0 END) AS gioi,
        SUM(CASE WHEN b.xep_loai = 'Khá' THEN 1 ELSE 0 END) AS kha,
        SUM(CASE WHEN b.xep_loai = 'Trung bình' THEN 1 ELSE 0 END) AS trungBinh,
        SUM(CASE
                WHEN b.ID IS NOT NULL
                 AND (b.xep_loai IS NULL OR b.xep_loai NOT IN ('Xuất sắc', 'Giỏi', 'Khá', 'Trung bình'))
                THEN 1 ELSE 0
            END) AS khac,
        COUNT(b.ID) AS tongSo
    FROM unit_map u
    LEFT JOIN graduate_base b
        ON b.MA_DON_VI = u.ma_don_vi
    GROUP BY u.stt, u.so_hieu_don_vi
    ORDER BY u.stt;
END;
/
```

Ghi chú quan trọng:

- `CREATED_AT` chỉ là trường ngày có sẵn trong `HV_QUYET_DINH_TOT_NGHIEP`. `[Cần xác nhận]` Báo cáo theo năm học nên lọc theo ngày nào: ngày quyết định tốt nghiệp, ngày phê duyệt, ngày tạo, hay dữ liệu từ bảng quyết định/văn bản liên quan.
- `p_workflow_status` cần nghiệp vụ xác nhận. Nếu báo cáo chỉ lấy dữ liệu đã duyệt thì truyền `Approved`.
- Nếu dùng `template_m04.xlsx`, DTO/template cần thống nhất tên trường `tenDonvi` hoặc `tenDonVi`.
- Nếu giữ layout `docs/report-input/M04.xlsx`, cần bổ sung cột `tongSo` hoặc công thức cột H trong template render.

Nguồn source:
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`
- `src/bctk-v2/templates/reports/template_m04.xlsx`

## 10. API và thay đổi backend đề xuất

### 10.1. Theo API BCTK hiện có

| Hạng mục | Đề xuất |
|---|---|
| Preview HTML | `GET /api/report/get-bao-cao?maBaoCao=m04&exportType=HTML` |
| Export Excel | `GET /api/report/get-bao-cao?maBaoCao=m04&exportType=EXCEL` |
| Export PDF | `GET /api/report/get-bao-cao?maBaoCao=m04&exportType=PDF` |
| Data source hiện tại | `ReportService.getDataBaoCaoM04()` trả `BaoCaoM04DTO.mock()`. |
| Data source cần thay | Gọi query/stored procedure thật từ `HV_QUYET_DINH_TOT_NGHIEP` và `DM_PHAN_LOAI_KQ_TOT_NGHIEP`. |
| Template config | Source có entity `TemplateConfig` với `MA_BAO_CAO`, `TEN_BAO_CAO`, `TEN_TEMPLATE`, `SQL`. `[Cần xác nhận]` DB docs hiện chưa thấy rõ bảng `TEMPLATE_CONFIGS`. |

### 10.2. Tham số nghiệp vụ đề xuất

| Tham số | Ý nghĩa | Mapping |
|---|---|---|
| `maBaoCao` | Mã báo cáo | `m04`. |
| `exportType` | Kiểu xuất | `HTML`, `EXCEL`, `PDF`. |
| `fromDate`, `toDate` hoặc `namHoc` | Kỳ báo cáo | `[Cần xác nhận]` Chưa có tham số trong API hiện tại và chưa rõ cột ngày nghiệp vụ. |
| `workflowStatus` | Trạng thái dữ liệu | `HV_QUYET_DINH_TOT_NGHIEP.WORKFLOW_STATUS`. |
| `includeEmptyUnits` | Có hiển thị đơn vị không có dữ liệu không | `[Suy luận]` Template input hiển thị đủ T01-T11, nên nên có cơ chế trả dòng 0 cho đơn vị không có dữ liệu. |

Nguồn source:
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/entities/TemplateConfig.java`

## 11. Gaps và câu hỏi cần xác nhận

| STT | Vấn đề cần xác nhận | Mức độ ảnh hưởng | Câu hỏi đề xuất |
|---:|---|---|---|
| 1 | Mã biểu mẫu | Trung bình | Báo cáo này dùng mã chính thức `M04` hay `4M`? |
| 2 | Layout chính thức | Cao | Dùng layout `docs/report-input/M04.xlsx` có cột H `Tổng số`, hay layout `template_m04.xlsx` có dòng tổng cuối bảng? |
| 3 | Năm học | Cao | `(Năm học 2024 - 2025)` là dữ liệu mẫu hay phải lọc động theo tham số năm học? |
| 4 | Cột ngày để lọc | Cao | Số liệu tốt nghiệp tính theo ngày quyết định, ngày phê duyệt, ngày tạo bản ghi, hay mốc năm học riêng? |
| 5 | Trạng thái dữ liệu | Cao | Báo cáo chỉ lấy `Approved` hay lấy cả `Draft`/`Submitted` nếu bản ghi hiệu lực? |
| 6 | Quy tắc cột `Khác` | Cao | `Khác` gồm `Không đạt`, null/chưa phân loại, hay các loại không thuộc Xuất sắc/Giỏi/Khá/Trung bình? |
| 7 | Đơn vị hiển thị | Cao | Báo cáo luôn hiển thị đủ T01-T11 hay chỉ những đơn vị có dữ liệu? Có cần thêm B06 không? |
| 8 | Mapping danh mục xếp loại | Cao | Xác nhận dùng `DM_PHAN_LOAI_KQ_TOT_NGHIEP` cho `XEP_LOAI_TOT_NGHIEP_ID`; không dùng `DM_HANG_TOT_NGHIEP`/`DM_LOAI_TOT_NGHIEP`. |
| 9 | Tên field DTO/template | Trung bình | Sửa `tenDonvi` thành `tenDonVi`, hay đổi smart marker về `tenDonvi`? |
| 10 | Dữ liệu mock | Cao | Khi nào thay `BaoCaoM04DTO.mock()` bằng query/stored procedure thật? |
| 11 | Quyết định tốt nghiệp | Trung bình | `QUYET_DINH_TOT_NGHIEP_ID` hiện là mã/ID tham chiếu nhưng chưa thấy bảng chính trong schema; nguồn ngày quyết định lấy từ đâu? |
| 12 | Tổng số | Trung bình | Có cần trả thêm `tongSo` từ backend hay để Excel tự tính bằng công thức? |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

## 12. Kết luận mức độ sẵn sàng

| Hạng mục | Đánh giá |
|---|---|
| Template Excel | Có 2 template liên quan nhưng đang lệch layout tổng số. |
| API export | Có khung API export chung và có case `m04`. |
| Backend data source | Có DTO và service, nhưng dữ liệu hiện là mock/random. |
| Database nguồn | Có bảng nghiệp vụ `HV_QUYET_DINH_TOT_NGHIEP`, lookup `xep_loai_tot_nghiep`, danh mục T01-T11. |
| Stored procedure/query | Chưa tìm thấy implementation thật trong source hiện tại; tài liệu này đề xuất khung procedure. |
| Mức độ có thể đưa vào SRS | Có thể dùng làm bản phân tích nền cho SRS M04. Trước khi đặc tả DEV cần chốt layout chính thức, kỳ báo cáo, trạng thái dữ liệu, rule `Khác` và mapping danh mục xếp loại. |

Nguồn source:
- `docs/report-input/M04.xlsx`
- `src/bctk-v2/templates/reports/template_m04.xlsx`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/controller/report/ReportController.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/service/report/ReportService.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/dtos/BaoCaoM04DTO.java`
- `src/bctk-v2/src/main/java/vn/gtelict/x02/bctk/entities/TemplateConfig.java`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

# Báo cáo 5H - Thống kê kết quả biên soạn chương trình giáo dục, giáo trình, tài liệu dạy học

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/5H.xlsx` |
| Sheet | `Bien soan` |
| Mã biểu mẫu | `Biễu mẫu 5H` |
| Tên báo cáo | `THỐNG KÊ KẾT QUẢ BIÊN SOẠN CHƯƠNG TRÌNH GIÁO DỤC, GIÁO TRÌNH, TÀI LIỆU DẠY HỌC` |
| Vùng dữ liệu chính | `A6:O32` |
| Vùng chữ ký | `B37:E37`, `K37:O37` |
| Công thức Excel | Không có công thức |
| Dạng báo cáo | Ma trận đếm theo loại tài liệu biên soạn, hình thức biên soạn và mức độ hoàn thành |

`[Cần xác nhận]` Template ghi `Biễu mẫu 5H`; có thể là lỗi chính tả của `Biểu mẫu 5H`. Dòng kèm báo cáo ở `E4:O4` ghi `tháng 5 năm 2025`, trong khi các mẫu H đang được xử lý theo bộ năm 2026. Khi xuất báo cáo nên giữ nguyên template nếu đây là mẫu chính thức, nhưng cần xác nhận kỳ/năm báo cáo.

## 2. Mục đích nghiệp vụ

Báo cáo tổng hợp số lượng chương trình, giáo trình và tài liệu dạy học đang được biên soạn hoặc đã hoàn thành trong kỳ báo cáo. Các chỉ tiêu được chia theo:

- Nhóm tài liệu/chương trình: chương trình khung, chương trình đào tạo, đề cương chi tiết, chương trình bồi dưỡng, giáo trình, tài liệu dạy học.
- Hình thức biên soạn: mới; chỉnh lý/sưu tầm/biên dịch.
- Mức độ hoàn thành: đề cương, bản thảo, bản chính và trạng thái nghiệm thu/ban hành.

`[Suy luận]` Đây là báo cáo cấp học viện/trường CAND theo kỳ hoặc năm học. Template không có ô filter nên hệ thống cần truyền `maDonVi`, `namHocId` hoặc `tuNgay/denNgay` từ API/giao diện.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:O1` | `Biễu mẫu 5H` | Merged |
| `A2:D2` | `BỘ CÔNG AN` | Merged |
| `E2:O3` | Tên báo cáo | Merged, xuống dòng |
| `A3:D3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `A4:D4` | Trống hoặc thông tin đơn vị | Merged |
| `E4:O4` | Dòng kèm theo báo cáo | Merged |

### 3.2. Header bảng

| Vùng | Nhãn | Field/nhóm field đề xuất |
|---|---|---|
| `A6:A8` | `TT` | `stt` |
| `B6:D8` | `Tài liệu biên soạn` | `rowLabel`, `rowGroup`, `rowCode` |
| `E6:F6` | `Hình thức biên soạn` | Nhóm `hinhThucBienSoan` |
| `E7:E8` | `Mới` | `hinhThucMoi` |
| `F7:F8` | `Chỉnh lý, Sưu tầm, Biên dịch` | `hinhThucChinhLySuuTamBienDich` |
| `G6:N6` | `Mức độ hoàn thành` | Nhóm `mucDoHoanThanh` |
| `G7:H7` | `Đề cương` | `deCuongNghiemThu`, `deCuongBanHanh` |
| `I7:K7` | `Bản thảo` | `banThaoHoiThaoKhoa`, `banThaoHoiThaoHocVien`, `banThaoNghiemThu` |
| `L7:N7` | `Bản chính` | `banChinhNghiemThu`, `banChinhChuaBanHanh`, `banChinhBanHanh` |
| `O6:O8` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Nguồn/mapping đề xuất |
|---:|---:|---|---|---|
| 9 | 1 | Chương trình khung | `ctKhung` | `DAO_TAO_BOI_DUONG` hoặc `CHUONG_TRINH` `[Cần mapping danh mục]` |
| 10 |  | Chương trình đào tạo hệ chính quy | `ctKhungHeChinhQuy` | Lọc theo loại chương trình/hình thức đào tạo chính quy `[Cần mapping danh mục]` |
| 11 |  | Chương trình đào tạo Ngành TSAN | `ctKhungNganhTsan` | Lọc theo ngành/chuyên ngành TSAN `[Cần mapping danh mục]` |
| 12 | 2 | Chương trình đào tạo | `chuongTrinhDaoTao` | `DAO_TAO_BOI_DUONG` hoặc `CHUONG_TRINH` |
| 13 |  | Chương trình đào tạo đại học hệ chính quy | `ctdtDaiHocChinhQuy` | `TRINH_DO_DAO_TAO_ID` + `HINH_THUC_DAO_TAO_ID` `[Cần mapping danh mục]` |
| 14 |  | Chương trình đào tạo trình độ đại học dành cho học viên quốc tế: ngành TSAN, ĐTHS, ANM&PCTP, QLNN về ANTT | `ctdtDaiHocHocVienQuocTe` | Có thể liên quan dữ liệu quốc tế hoặc chương trình cho học viên quốc tế `[Cần xác nhận]` |
| 15 |  | Chương trình đào tạo tiến sĩ | `ctdtTienSi` | `TRINH_DO_DAO_TAO_ID = tiến sĩ` `[Cần mapping danh mục]` |
| 16 |  | Quản lý nhà nước về an ninh trật tự | `ctdtQlNnAntt` | Lọc ngành/chuyên ngành hoặc tên chương trình `[Cần mapping danh mục]` |
| 17 |  | Tội phạm học và phòng ngừa tội phạm | `ctdtToiPhamHocPhongNgua` | Lọc ngành/chuyên ngành hoặc tên chương trình `[Cần mapping danh mục]` |
| 18 |  | Chương trình đào tạo hệ chính quy | `ctdtHeChinhQuy` | Lọc theo hình thức đào tạo chính quy |
| 19 | 3 | Đề cương chi tiết học phần/ môn học | `deCuongChiTietHocPhan` | `CHI_TIET_CHUONG_TRINH_DAO_TAO` `[Suy luận]`, hoặc nguồn đề cương học phần nếu có |
| 20 | 4 | Chương trình bổ sung kiến thức và lý luận chính trị | `ctBoSungKienThucLlct` | `DAO_TAO_BOI_DUONG` theo loại bồi dưỡng/bổ sung kiến thức `[Cần mapping danh mục]` |
| 21 | 5 | Chương trình bồi dưỡng chức danh, chức vụ và quy hoạch chức danh, chức vụ lãnh đạo, chỉ huy trong CAND | `ctBoiDuongChucDanhChucVu` | `DAO_TAO_BOI_DUONG`, có thể liên quan `QUA_TRINH_BOI_DUONG_CHUC_DANH` cho sự kiện học `[Cần xác nhận]` |
| 22 | 6 | Chương trình BDNV, chuyên môn, chuyên đề | `ctBdnvChuyenMonChuyenDe` | `DAO_TAO_BOI_DUONG` theo nhóm bồi dưỡng nghiệp vụ/chuyên đề |
| 23 | 8 | Giáo trình | `giaoTrinh` | `GIAO_TRINH_TAI_LIEU`, nhóm loại tài liệu là giáo trình |
| 24 |  | Giáo trình dùng cho đào tạo trình độ đại học | `giaoTrinhDaiHoc` | `LOAI_TAI_LIEU_ID` + `TRINH_DO_DAO_TAO_ID = đại học` |
| 25 |  | Giáo trình dùng cho đào tạo trình độ cao học | `giaoTrinhCaoHoc` | `TRINH_DO_DAO_TAO_ID = cao học/thạc sĩ` `[Cần mapping danh mục]` |
| 26 |  | Giáo trình dùng cho đào tạo NCS | `giaoTrinhNcs` | `TRINH_DO_DAO_TAO_ID = nghiên cứu sinh/tiến sĩ` `[Cần mapping danh mục]` |
| 27 |  | Tập bài giảng | `tapBaiGiang` | `LOAI_TAI_LIEU_ID = tập bài giảng` |
| 28 | 9 | Tài liệu dạy học | `taiLieuDayHoc` | `GIAO_TRINH_TAI_LIEU`, nhóm loại tài liệu là tài liệu dạy học |
| 29 |  | Sách chuyên khảo / Tài liệu tham khảo | `sachChuyenKhao` | `LOAI_TAI_LIEU_ID = sách chuyên khảo` hoặc nhóm tài liệu tham khảo `[Cần xác nhận]` |
| 30 |  | Sách hướng dẫn | `sachHuongDan` | `LOAI_TAI_LIEU_ID = sách hướng dẫn` |
| 31 |  | Tài liệu biên tập dịch và hiệu đính từ tiếng nước ngoài | `taiLieuBienTapDichHieuDinh` | `LOAI_TAI_LIEU_ID` hoặc hình thức biên soạn biên dịch/hiệu đính `[Cần mapping danh mục]` |
| 32 |  | Sách tham khảo | `sachThamKhao` | `LOAI_TAI_LIEU_ID = sách tham khảo` |

`[Cần xác nhận]` STT trong template nhảy từ `6` ở dòng 22 sang `8` ở dòng 23, không có STT `7`. Nếu không phải lỗi template, cần bổ sung ý nghĩa của mục số 7 bị ẩn/loại bỏ.

`[Cần xác nhận]` Dòng 29 có `B29 = - Sách chuyên khảo`, đồng thời `D29 = Tài liệu tham khảo`. Cần xác định `Tài liệu tham khảo` là nhãn nhóm, ghi chú hay một loại tài liệu riêng.

## 5. Mapping cột giá trị

| Cột | Header | Field đề xuất | Quy tắc tính |
|---|---|---|---|
| `E` | Hình thức biên soạn - Mới | `moi` | Count bản ghi có hình thức biên soạn mới |
| `F` | Hình thức biên soạn - Chỉnh lý, Sưu tầm, Biên dịch | `chinhLySuuTamBienDich` | Count bản ghi có hình thức chỉnh lý/sưu tầm/biên dịch |
| `G` | Đề cương - Nghiệm thu | `deCuongNghiemThu` | Count bản ghi đang/đã nghiệm thu đề cương |
| `H` | Đề cương - Ban hành | `deCuongBanHanh` | Count bản ghi đề cương đã ban hành |
| `I` | Bản thảo - Hội thảo cấp Khoa | `banThaoHoiThaoKhoa` | Count bản ghi bản thảo đã hội thảo cấp khoa |
| `J` | Bản thảo - Hội thảo cấp Học viện | `banThaoHoiThaoHocVien` | Count bản ghi bản thảo đã hội thảo cấp học viện |
| `K` | Bản thảo - Nghiệm thu | `banThaoNghiemThu` | Count bản ghi bản thảo đã nghiệm thu |
| `L` | Bản chính - Nghiệm thu | `banChinhNghiemThu` | Count bản ghi bản chính đã nghiệm thu |
| `M` | Bản chính - Chưa ban hành | `banChinhChuaBanHanh` | Count bản ghi bản chính chưa có quyết định/văn bản ban hành |
| `N` | Bản chính - Ban hành | `banChinhBanHanh` | Count bản ghi bản chính đã ban hành |
| `O` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay theo dòng |

`[Cần mapping danh mục]` Mẫu cần hai nhóm danh mục độc lập: `hinh_thuc_bien_soan` và `muc_do_hoan_thanh`. DDL cũ từng có `HINH_THUC_BIEN_SOAN`, `TRANG_THAI_TAI_LIEU`, nhưng entity/schema hiện hành của `GIAO_TRINH_TAI_LIEU` chỉ còn các trường như `LOAI_TAI_LIEU_ID`, `TRINH_DO_DAO_TAO_ID`, `QUYET_DINH_BAN_HANH_ID` và workflow chuẩn. Không nên map trực tiếp `WORKFLOW_STATUS = Approved` thành mọi trạng thái nghiệm thu/ban hành vì workflow duyệt bản ghi khác với vòng đời biên soạn.

## 6. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng | Nhận xét |
|---|---|---|---|
| `X02_APP.DAO_TAO_BOI_DUONG` / `/api/v1/dao-tao-boi-duong` | Chương trình đào tạo, bồi dưỡng trong domain PRG | `TEN_CHUONG_TRINH`, `HINH_THUC_DAO_TAO_ID`, `TRINH_DO_DAO_TAO_ID`, `VAN_BAN_BAN_HANH_ID`, `WORKFLOW_STATUS`, `MA_DON_VI` | Nguồn chính cho các dòng chương trình |
| `X02_APP.CHUONG_TRINH` / `/api/v1/pln-chuong-trinh` | Chương trình đào tạo phía kế hoạch/PLN | `TEN_CHUONG_TRINH_DAO_TAO`, `TRINH_DO_ID`, `HINH_THUC_DAO_TAO_ID`, `LOAI_HINH_DAO_TAO_ID` | `[Cần xác nhận]` dùng cho kế hoạch hay danh mục chương trình chính thức |
| `X02_APP.CHI_TIET_CHUONG_TRINH_DAO_TAO` | Chi tiết môn học/học phần trong chương trình | `CHUONG_TRINH_ID`, `MON_HOC_ID`, `LOAI_MON`, `WORKFLOW_STATUS`, `MA_DON_VI` | Phù hợp nhất cho dòng đề cương chi tiết học phần/môn học nếu mỗi học phần có hồ sơ đề cương |
| `X02_APP.GIAO_TRINH_TAI_LIEU` / `/api/v1/giao-trinh` | Giáo trình, tài liệu dạy học trong domain PRG | `TEN_GIAO_TRINH`, `LOAI_TAI_LIEU_ID`, `TRINH_DO_DAO_TAO_ID`, `QUYET_DINH_BAN_HANH_ID`, `WORKFLOW_STATUS`, `MA_DON_VI` | Nguồn chính cho các dòng giáo trình/tài liệu |
| `X02_APP.TL_GIANG_DAY` / `/api/v1/pln-tai-lieu` | Tài liệu, giáo trình dạy học phía PLN | `TEN_CO_SO`, `TEN_GIAO_TRINH`, `TEN_TAC_GIA`, `MON_HOC`, `SO_QUYET_DINH`, `NGAY_QUYET_DINH` | `[Cần xác nhận]` dùng làm kế hoạch/nguồn nhập liệu hay bảng nghiệp vụ chính |
| `X02_DM.DM_TRINH_DO_DAO_TAO` | Mapping đại học, cao học, NCS/tiến sĩ | `ID`, `TEN` | Cần chuẩn hóa mã cho các dòng 13, 15, 24-26 |
| Lookup `dm_loai_tai_lieu_temp` / `loai_tai_lieu` | Mapping giáo trình, tập bài giảng, sách tham khảo... | `LOAI_TAI_LIEU_ID` | Cần chốt danh mục để map dòng 23-32 |
| Lookup `dm_hinh_thuc_dao_tao_temp` | Mapping hệ chính quy, bồi dưỡng... | `HINH_THUC_DAO_TAO_ID` | Cần chốt danh mục cho các dòng chương trình |

## 7. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | Áp dụng trên `MA_DON_VI` hoặc `TRUONG_HOC_ID`/`CO_SO_DAO_TAO_ID`; mặc định theo quyền user |
| `namHocId` | String | `[Cần xác nhận]` nếu dữ liệu biên soạn gắn năm học |
| `tuNgay` | Date | Dùng để lọc theo thời điểm tạo/cập nhật, ngày ban hành hoặc ngày trạng thái biên soạn nếu có bảng sự kiện |
| `denNgay` | Date | Ngày kết thúc kỳ |
| `workflowStatus` | String | Mặc định `Approved` cho dữ liệu đã được duyệt vào báo cáo |
| `includePlanningData` | Boolean | `[Cần xác nhận]` có lấy cả nguồn PLN (`CHUONG_TRINH`, `TL_GIANG_DAY`) hay chỉ lấy PRG |

`[Cần xác nhận]` Nếu báo cáo phản ánh “kết quả biên soạn trong kỳ”, cần một nguồn ngày nghiệp vụ theo từng mốc biên soạn. `CREATED_AT/UPDATED_AT/APPROVED_AT` chỉ phản ánh vòng đời bản ghi hệ thống, không đủ thay thế ngày nghiệm thu/hội thảo/ban hành.

## 8. API report đề xuất

```http
GET /api/v1/reports/5h/ket-qua-bien-soan-chuong-trinh-giao-trinh-tai-lieu
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Không | Ưu tiên khi báo cáo theo năm học |
| `tuNgay` | Không | Bắt buộc nếu không truyền `namHocId` |
| `denNgay` | Không | Bắt buộc nếu không truyền `namHocId` |
| `workflowStatus` | Không | Mặc định `Approved` |

Response đề xuất:

```json
{
  "reportCode": "5H",
  "title": "Thống kê kết quả biên soạn chương trình giáo dục, giáo trình, tài liệu dạy học",
  "filters": {
    "maDonVi": "T01",
    "namHocId": "2025-2026"
  },
  "columns": [
    "moi",
    "chinhLySuuTamBienDich",
    "deCuongNghiemThu",
    "deCuongBanHanh",
    "banThaoHoiThaoKhoa",
    "banThaoHoiThaoHocVien",
    "banThaoNghiemThu",
    "banChinhNghiemThu",
    "banChinhChuaBanHanh",
    "banChinhBanHanh",
    "ghiChu"
  ],
  "rows": [
    {
      "rowCode": "CT_KHUNG",
      "stt": "1",
      "label": "Chương trình khung",
      "level": 1,
      "parentCode": null,
      "moi": 0,
      "chinhLySuuTamBienDich": 0,
      "deCuongNghiemThu": 0,
      "deCuongBanHanh": 0,
      "banThaoHoiThaoKhoa": 0,
      "banThaoHoiThaoHocVien": 0,
      "banThaoNghiemThu": 0,
      "banChinhNghiemThu": 0,
      "banChinhChuaBanHanh": 0,
      "banChinhBanHanh": 0,
      "ghiChu": ""
    }
  ]
}
```

## 9. SQL/Proc đề xuất

Do các dòng và cột của mẫu 5H phụ thuộc mạnh vào danh mục nghiệp vụ, nên không nên hardcode bằng `LIKE '%giáo trình%'` trong proc chính. Đề xuất tạo lớp cấu hình hoặc view mapping:

- `RPT_5H_ROW_RULE`: map `row_code` sang nguồn (`PROGRAM`, `PROGRAM_DETAIL`, `MATERIAL`) và điều kiện danh mục.
- `RPT_5H_ITEM_STAGE`: view chuẩn hóa mỗi bản ghi sang `hinh_thuc_bien_soan_code` và `muc_do_hoan_thanh_code`.
- `RPT_5H_ROW_DEF`: danh sách dòng theo đúng thứ tự Excel để luôn xuất đủ dòng kể cả không có dữ liệu.

Skeleton Oracle:

```sql
WITH row_def AS (
    SELECT 'CT_KHUNG' row_code, '1' stt, 'Chương trình khung' label, 1 sort_order FROM dual UNION ALL
    SELECT 'CT_KHUNG_CHINH_QUY', NULL, 'Chương trình đào tạo hệ chính quy', 2 FROM dual UNION ALL
    SELECT 'CT_KHUNG_TSAN', NULL, 'Chương trình đào tạo Ngành TSAN', 3 FROM dual UNION ALL
    SELECT 'CTDT', '2', 'Chương trình đào tạo', 4 FROM dual UNION ALL
    SELECT 'DCCT_HP', '3', 'Đề cương chi tiết học phần/ môn học', 11 FROM dual UNION ALL
    SELECT 'GIAO_TRINH', '8', 'Giáo trình', 15 FROM dual UNION ALL
    SELECT 'TAI_LIEU_DAY_HOC', '9', 'Tài liệu dạy học', 20 FROM dual
),
program_items AS (
    SELECT
        'PROGRAM' AS source_type,
        dt.ID AS source_id,
        dt.TEN_CHUONG_TRINH AS item_name,
        dt.HINH_THUC_DAO_TAO_ID,
        dt.TRINH_DO_DAO_TAO_ID,
        dt.VAN_BAN_BAN_HANH_ID,
        dt.WORKFLOW_STATUS,
        dt.MA_DON_VI
    FROM X02_APP.DAO_TAO_BOI_DUONG dt
    WHERE dt.IS_DELETED = 0
      AND dt.IS_ACTIVE = 1
      AND (:p_workflow_status IS NULL OR dt.WORKFLOW_STATUS = :p_workflow_status)
      AND (:p_ma_don_vi IS NULL OR dt.MA_DON_VI = :p_ma_don_vi)
),
material_items AS (
    SELECT
        'MATERIAL' AS source_type,
        gt.ID AS source_id,
        gt.TEN_GIAO_TRINH AS item_name,
        gt.LOAI_TAI_LIEU_ID,
        gt.TRINH_DO_DAO_TAO_ID,
        gt.QUYET_DINH_BAN_HANH_ID,
        gt.WORKFLOW_STATUS,
        gt.MA_DON_VI
    FROM X02_APP.GIAO_TRINH_TAI_LIEU gt
    WHERE gt.IS_DELETED = 0
      AND gt.IS_ACTIVE = 1
      AND (:p_workflow_status IS NULL OR gt.WORKFLOW_STATUS = :p_workflow_status)
      AND (:p_ma_don_vi IS NULL OR gt.MA_DON_VI = :p_ma_don_vi)
),
source_items AS (
    SELECT source_type, source_id, item_name, HINH_THUC_DAO_TAO_ID AS type_id,
           TRINH_DO_DAO_TAO_ID, VAN_BAN_BAN_HANH_ID, WORKFLOW_STATUS, MA_DON_VI
    FROM program_items
    UNION ALL
    SELECT source_type, source_id, item_name, LOAI_TAI_LIEU_ID AS type_id,
           TRINH_DO_DAO_TAO_ID, QUYET_DINH_BAN_HANH_ID, WORKFLOW_STATUS, MA_DON_VI
    FROM material_items
),
mapped AS (
    SELECT
        rr.ROW_CODE,
        st.HINH_THUC_BIEN_SOAN_CODE,
        st.MUC_DO_HOAN_THANH_CODE,
        si.SOURCE_ID
    FROM source_items si
    JOIN X02_APP.RPT_5H_ROW_RULE rr
      ON rr.SOURCE_TYPE = si.SOURCE_TYPE
     AND rr.MATCH_TYPE_ID = si.TYPE_ID
     AND (rr.TRINH_DO_DAO_TAO_ID IS NULL OR rr.TRINH_DO_DAO_TAO_ID = si.TRINH_DO_DAO_TAO_ID)
    JOIN X02_APP.RPT_5H_ITEM_STAGE st
      ON st.SOURCE_TYPE = si.SOURCE_TYPE
     AND st.SOURCE_ID = si.SOURCE_ID
    WHERE (:p_tu_ngay IS NULL OR st.EVENT_DATE >= :p_tu_ngay)
      AND (:p_den_ngay IS NULL OR st.EVENT_DATE < :p_den_ngay + 1)
)
SELECT
    rd.STT,
    rd.LABEL,
    NVL(SUM(CASE WHEN m.HINH_THUC_BIEN_SOAN_CODE = 'MOI' THEN 1 ELSE 0 END), 0) AS MOI,
    NVL(SUM(CASE WHEN m.HINH_THUC_BIEN_SOAN_CODE IN ('CHINH_LY', 'SUU_TAM', 'BIEN_DICH') THEN 1 ELSE 0 END), 0) AS CHINH_LY_SUU_TAM_BIEN_DICH,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'DE_CUONG_NGHIEM_THU' THEN 1 ELSE 0 END), 0) AS DE_CUONG_NGHIEM_THU,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'DE_CUONG_BAN_HANH' THEN 1 ELSE 0 END), 0) AS DE_CUONG_BAN_HANH,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_THAO_HOI_THAO_KHOA' THEN 1 ELSE 0 END), 0) AS BAN_THAO_HOI_THAO_KHOA,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_THAO_HOI_THAO_HOC_VIEN' THEN 1 ELSE 0 END), 0) AS BAN_THAO_HOI_THAO_HOC_VIEN,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_THAO_NGHIEM_THU' THEN 1 ELSE 0 END), 0) AS BAN_THAO_NGHIEM_THU,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_CHINH_NGHIEM_THU' THEN 1 ELSE 0 END), 0) AS BAN_CHINH_NGHIEM_THU,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_CHINH_CHUA_BAN_HANH' THEN 1 ELSE 0 END), 0) AS BAN_CHINH_CHUA_BAN_HANH,
    NVL(SUM(CASE WHEN m.MUC_DO_HOAN_THANH_CODE = 'BAN_CHINH_BAN_HANH' THEN 1 ELSE 0 END), 0) AS BAN_CHINH_BAN_HANH
FROM row_def rd
LEFT JOIN mapped m ON m.ROW_CODE = rd.ROW_CODE
GROUP BY rd.SORT_ORDER, rd.STT, rd.LABEL
ORDER BY rd.SORT_ORDER;
```

`[Cần xác nhận]` Skeleton trên mới thể hiện hướng Proc. Trước khi triển khai thật cần chốt cấu trúc `RPT_5H_ROW_RULE` và `RPT_5H_ITEM_STAGE`, hoặc bổ sung trực tiếp các trường nghiệp vụ về hình thức biên soạn/trạng thái biên soạn vào bảng nguồn.

## 10. Quy tắc đối soát

- Tổng theo dòng cha phải bằng tổng các dòng con nếu dòng cha là nhóm tổng hợp. Ví dụ `Giáo trình` nên bằng tổng `Giáo trình đại học + giáo trình cao học + giáo trình NCS + tập bài giảng` nếu nghiệp vụ xác định các dòng con là đầy đủ và không giao nhau.
- Một bản ghi chỉ nên thuộc một dòng lá trong cùng một nhóm để tránh đếm trùng.
- `Bản chính - Ban hành` nên nhất quán với có quyết định/văn bản ban hành (`VAN_BAN_BAN_HANH_ID` hoặc `QUYET_DINH_BAN_HANH_ID`) nếu nghiệp vụ chấp nhận dùng văn bản ban hành làm mốc.
- `Bản chính - Chưa ban hành` không nên tính chung với `Bản chính - Ban hành` cho cùng một bản ghi tại cùng thời điểm.
- `Hình thức biên soạn` và `Mức độ hoàn thành` là hai chiều độc lập; tổng `E+F` không nhất thiết bằng tổng `G:N` nếu dữ liệu chưa gắn đủ cả hai nhóm thuộc tính. Cần cảnh báo thiếu mapping thay vì tự cân bằng số.

## 11. Gap/câu hỏi cần xác nhận

| Nhóm | Vấn đề | Đề xuất xử lý |
|---|---|---|
| Template | `Biễu mẫu 5H`, năm 2025, STT thiếu 7 | Xác nhận với đơn vị nghiệp vụ trước khi sửa template |
| Dòng báo cáo | Ranh giới giữa `DAO_TAO_BOI_DUONG`, `CHUONG_TRINH`, `CHI_TIET_CHUONG_TRINH_DAO_TAO` | Chốt bảng nguồn chính cho từng nhóm chương trình |
| Hình thức biên soạn | Entity hiện hành chưa có field `HINH_THUC_BIEN_SOAN` | Bổ sung danh mục/field hoặc tạo bảng trạng thái biên soạn riêng |
| Mức độ hoàn thành | Không có cột chuẩn cho đề cương/bản thảo/bản chính/hội thảo/nghiệm thu | Thiết kế bảng sự kiện hoặc view `RPT_5H_ITEM_STAGE` |
| Loại tài liệu | Cần map giáo trình, tập bài giảng, sách chuyên khảo, sách hướng dẫn, sách tham khảo | Chốt lookup `dm_loai_tai_lieu_temp`/`loai_tai_lieu` |
| Kỳ báo cáo | Chưa rõ dùng năm học, năm dương lịch hay khoảng ngày | Chuẩn hóa filter `namHocId` hoặc `tuNgay/denNgay` |
| PLN/PRG | Có nguồn PRG và PLN tương tự nhau | Quyết định báo cáo lấy kết quả thực hiện PRG, kế hoạch PLN, hay hợp nhất có khử trùng |

## 12. Tài liệu/code tham chiếu

- `docs/report-input/5H.xlsx`
- `src/frontend/frontend-x02-v2/src/shared/config/screenApiCatalog.csv`
- `docs/dashboard/PRG-dashboard.md`
- `docs/dashboard/ke-hoach.md`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/prg/daotaoboiduong/entity/DaoTaoBoiDuong.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/prg/giaotrinh/entity/GiaoTrinhTaiLieu.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/pln/plnchuongtrinh/entity/ChuongTrinh.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/pln/plntailieu/entity/TlGiangDay.java`
- `src/backend/qldt-v2/database/oracle/business/41_chi_tiet_chuong_trinh_dao_tao_create.sql`
- `docs/database/X02_APP.sql`

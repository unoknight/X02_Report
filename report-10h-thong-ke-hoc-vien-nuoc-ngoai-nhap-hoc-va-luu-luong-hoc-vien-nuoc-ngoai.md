# Báo cáo 10H - Thống kê học viên nước ngoài nhập học và lưu lượng học viên nước ngoài

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/10H.xlsx` |
| Sheet | `Nuoc ngoai` |
| Mã biểu mẫu | `Biểu mẫu 10H` |
| Tên báo cáo | `THỐNG KÊ HỌC VIÊN NƯỚC NGOÀI NHẬP HỌC VÀ LƯU LƯỢNG HỌC VIÊN NƯỚC NGOÀI` |
| Vùng dữ liệu có giá trị | `B2:J27` |
| Vùng style kéo dài | `B1:AB48` |
| Công thức Excel | Có 6 công thức tổng hợp tại `F11`, `G11`, `H11`, `E21`, `G21`, `H21` |
| Dạng báo cáo | Hai ma trận nhỏ: học viên nước ngoài nhập học trong kỳ và lưu lượng học viên nước ngoài theo trình độ/loại hình, quốc gia gửi đào tạo |

`[Cần xác nhận]` Template 10H có `H11=SUM(#REF!)`, tức công thức tổng quốc gia thứ 3 ở khối nhập học đang lỗi tham chiếu. Khi triển khai nên dựng tổng theo metadata cột quốc gia động thay vì copy nguyên công thức Excel.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê học viên/người học nước ngoài học tập tại Học viện, trường CAND theo hai lát cắt:

- Số nhập học trong kỳ, có chỉ tiêu và thực nhập.
- Lưu lượng tại thời điểm báo cáo, tức số đang thuộc diện học tập/đào tạo/bồi dưỡng.

`[Suy luận]` Báo cáo thuộc nghiệp vụ người học nhưng nguồn dữ liệu đặc thù nằm ở phân hệ Hợp tác quốc tế (`INT`), vì hệ thống đã có màn/API `Người học nước ngoài học tập tại HV, trường` tại `/api/v1/int-nh-nn-vn` và bảng `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN`.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `B2:J2` | `Biểu mẫu 10H` | Merged |
| `B3:C3` | `BỘ CÔNG AN` | Merged |
| `D3:J4` | Tên báo cáo | Merged, xuống dòng |
| `B4:C4` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `D5:J5` | `(Kèm theo Báo cáo số ngày tháng 5 năm 2025)` | Merged |

`[Cần xác nhận]` Header ghi `tháng 5 năm 2025`, trong khi một số mẫu H khác đang ghi 2026. Cần chốt kỳ báo cáo hoặc cho phép truyền `reportDate/reportMonth/reportYear` khi xuất.

### 3.2. Khối 1 - Học viên nước ngoài nhập học

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `B7:J7` | `HỌC VIÊN NƯỚC NGOÀI NHẬP HỌC` | Section `nhapHoc` |
| `B8:B9` | `TT` | `stt` |
| `C8:D9` | `Trình độ, hình thức, loại hình đào tạo, bồi dưỡng` | `rowLabel`, `rowCode` |
| `E8:E9` | `Chỉ tiêu` | `chiTieu` |
| `F8:F9` | `Thực nhập` | `thucNhap` |
| `G8:I8` | `Quốc gia gửi đào tạo, bồi dưỡng` | Nhóm quốc gia |
| `G9` | `Lào` | `countries["LAO"]` hoặc `countriesByName["Lào"]` |
| `H9` | `Campuchia` | `countries["KHM"]` hoặc `countriesByName["Campuchia"]` |
| `I9` | `……` | Cột quốc gia mở rộng |
| `J8:J9` | `Ghi chú` | `ghiChu` |

### 3.3. Khối 2 - Lưu lượng học viên nước ngoài

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `B17:J17` | `LƯU LƯỢNG HỌC VIÊN NƯỚC NGOÀI` | Section `luuLuong` |
| `B18:B19` | `TT` | `stt` |
| `C18:D19` | `Trình độ, hình thức, loại hình đào tạo, bồi dưỡng` | `rowLabel`, `rowCode` |
| `E18:F19` | `Tổng` | `tong` |
| `G18:I18` | `Quốc gia gửi đào tạo, bồi dưỡng` | Nhóm quốc gia |
| `G19` | `Lào` | `countries["LAO"]` hoặc `countriesByName["Lào"]` |
| `H19` | `Campuchia` | `countries["KHM"]` hoặc `countriesByName["Campuchia"]` |
| `I19` | `……` | Cột quốc gia mở rộng |
| `J18:J19` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Khối | Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---:|---|---|---|---|
| Nhập học | 11 |  | Tổng | `nhapHoc.tong` | Tổng các dòng 12-16 |
| Nhập học | 12 | 1 | Nghiên cứu sinh | `nhapHoc.nghienCuuSinh` | `TRINH_DO_DAO_TAO_ID` hoặc lớp HTQT có trình độ nghiên cứu sinh/tiến sĩ |
| Nhập học | 13 | 2 | Cao học | `nhapHoc.caoHoc` | Trình độ thạc sĩ/cao học |
| Nhập học | 14 | 3 | Đại học | `nhapHoc.daiHoc` | Trình độ đại học |
| Nhập học | 15 | 4 | Trung cấp | `nhapHoc.trungCap` | Trình độ trung cấp |
| Nhập học | 16 | 5 | Trống | `nhapHoc.khac` | `[Cần xác nhận]` Dòng 5 trong khối nhập học chưa có nhãn; có thể là loại hình đào tạo/bồi dưỡng khác |
| Lưu lượng | 21 |  | Tổng | `luuLuong.tong` | Tổng các dòng 22-28 |
| Lưu lượng | 22 | 1 | Nghiên cứu sinh | `luuLuong.nghienCuuSinh` | Trình độ nghiên cứu sinh/tiến sĩ, còn trong lưu lượng |
| Lưu lượng | 23 | 2 | Cao học | `luuLuong.caoHoc` | Trình độ thạc sĩ/cao học, còn trong lưu lượng |
| Lưu lượng | 24 | 3 | Đại học | `luuLuong.daiHoc` | Trình độ đại học, còn trong lưu lượng |
| Lưu lượng | 25 | 4 | Trung cấp | `luuLuong.trungCap` | Trình độ trung cấp, còn trong lưu lượng |
| Lưu lượng | 26 | 5 | Các loại hình đào tạo, bồi dưỡng khác | `luuLuong.khac` | Nhóm loại hình khác |
| Lưu lượng | 27 |  | Công tác phòng, chống tội phạm sử dụng công nghệ cao cho cán bộ Bộ Công an Lào | `luuLuong.bdPctpCongNgheCaoBoCongAnLao` | `[Cần mapping danh mục]` Lớp/chương trình HTQT cụ thể, nhiều khả năng lấy từ `LOP_DAO_TAO_BOI_DUONG_QT.TEN_LOP_HOC` |

`[Cần xác nhận]` Dòng 27 là dòng con của nhóm `Các loại hình đào tạo, bồi dưỡng khác`, nhưng template không có công thức rõ để cộng vào dòng 26 theo từng cột ngoài việc row 21 cộng cả row 22-28. Cần chốt cây dòng chính thức trước khi code.

## 5. Mapping cột giá trị

| Khối | Cột | Header | Field đề xuất | Mapping DB đề xuất |
|---|---|---|---|---|
| Nhập học | `E` | Chỉ tiêu | `chiTieu` | Ưu tiên `LOP_DAO_TAO_BOI_DUONG_QT.SL_HOC_VIEN_THOA_THUAN`; fallback chỉ tiêu tuyển sinh nếu nghiệp vụ có chỉ tiêu riêng cho học viên nước ngoài |
| Nhập học | `F` | Thực nhập | `thucNhap` | Count `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN.ID` hoặc `HOC_VIEN.ID` theo ngày/năm nhập học |
| Nhập học | `G:I` | Quốc gia gửi đào tạo, bồi dưỡng | `countryCounts[]` | Group theo `QUOC_TICH_ID` hoặc quốc gia gửi từ lớp/thỏa thuận `[Cần xác nhận]` |
| Nhập học | `J` | Ghi chú | `ghiChu` | Text nhập tay |
| Lưu lượng | `E:F` | Tổng | `tong` | Count học viên nước ngoài còn thuộc lưu lượng tại ngày chốt |
| Lưu lượng | `G:I` | Quốc gia gửi đào tạo, bồi dưỡng | `countryCounts[]` | Group theo quốc gia/quốc tịch tương ứng |
| Lưu lượng | `J` | Ghi chú | `ghiChu` | Text nhập tay |

`[Cần xác nhận]` Header dùng “Quốc gia gửi đào tạo, bồi dưỡng”, nhưng dashboard HTQT đang mô tả inbound theo `QUOC_TICH_ID` và `DM_QUOC_TICH`. Nếu quốc gia gửi khác quốc tịch, cần bổ sung field nguồn gửi trên hồ sơ người học nước ngoài hoặc lấy qua `LOP_DAO_TAO_BOI_DUONG_QT`/thỏa thuận.

## 6. Công thức Excel trong template

| Ô | Ý nghĩa | Công thức | Nhận xét |
|---|---|---|---|
| `F11` | Tổng thực nhập khối nhập học | `=SUM(F12:F16)` | Hợp lý nếu dòng 16 là dòng lá |
| `G11` | Tổng quốc gia Lào khối nhập học | `=SUM(G12:G16)` | Hợp lý |
| `H11` | Tổng quốc gia Campuchia/hoặc cột quốc gia thứ 2 | `=SUM(#REF!)` | Lỗi template `[Cần xác nhận template]` |
| `E21` | Tổng lưu lượng | `=SUM(E22:E28)` | Hợp lý nhưng row 28 không có nhãn |
| `G21` | Tổng quốc gia Lào khối lưu lượng | `=SUM(G22:G28)` | Hợp lý |
| `H21` | Tổng quốc gia Campuchia khối lưu lượng | `=SUM(H22:H28)` | Hợp lý |

`[Cần xác nhận]` Cột `I` trong cả hai khối là cột quốc gia mở rộng nhưng không có công thức tổng tại `I11`/`I21`. Nếu report hỗ trợ danh sách quốc gia động, backend nên trả metadata cột và frontend/export tự render số cột quốc gia.

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN` / `/api/v1/int-nh-nn-vn` | Nguồn chính người học nước ngoài học tại HV/trường | `ID`, `NGUOI_HOC_ID`, `QUOC_TICH_ID` theo entity, `FILE_HO_SO_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.HOC_VIEN` | Join hồ sơ học viên để lấy trình độ, hình thức, loại hình, ngày nhập học, trạng thái học | `ID`, `CON_NGUOI_ID`, `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `LOAI_HINH_DAO_TAO_ID`, `NGAY_NHAP_HOC`, `TRANG_THAI_HOC_ID`, `MA_DON_VI` |
| `X02_APP.CON_NGUOI` | Fallback quốc tịch và thông tin nhân thân nếu `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN.QUOC_TICH_ID` thiếu | `ID`, `QUOC_TICH_ID` |
| `X02_APP.LOP_DAO_TAO_BOI_DUONG_QT` | Nguồn lớp/chương trình HTQT, chỉ tiêu theo thỏa thuận và nhóm loại hình đào tạo/bồi dưỡng | `ID`, `TEN_LOP_HOC`, `TRINH_DO_DAO_TAO`, `HINH_THUC_DAO_TAO_BOI_DUONG`, `LOAI_HINH_DAO_TAO`, `SL_HOC_VIEN_THOA_THUAN`, `SL_HOC_VIEN_THAM_GIA`, `NGAY_BAT_DAU`, `NGAY_KET_THUC` |
| `X02_DM.DM_QUOC_TICH` | Label quốc tịch/người học inbound | `ID`, `MA`, `TEN` |
| `X02_DM.DM_QUOC_GIA` | Label quốc gia nếu nghiệp vụ yêu cầu quốc gia gửi đào tạo thay vì quốc tịch | `ID`, `MA`, `TEN` |
| `X02_DM.DM_TRINH_DO_DAO_TAO` | Mapping dòng nghiên cứu sinh/cao học/đại học/trung cấp | `ID`, `MA`, `TEN` |
| `X02_DM.DM_HINH_THUC_DAO_TAO`, `DM_HINH_THUC_DAO_TAO_BD_QT` | Mapping hình thức đào tạo/bồi dưỡng | `ID`, `MA`, `TEN` |
| `X02_DM.DM_LOAI_HINH_DAO_TAO`, `DM_LOAI_HINH_DAO_TAO_QT` | Mapping loại hình đào tạo | `ID`, `MA`, `TEN` |
| `X02_DM.DM_TRANG_THAI_HOC_VIEN` | Xác định còn trong lưu lượng | `ID`, `MA`, `TEN` |

`[Cần xác nhận schema]` DDL `docs/database/X02_APP.sql` tại bảng `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN` có `LOP_DAO_TAO_ID`, `KHOA_ID`, `NAM_NHAP_HOC` nhưng không thấy `QUOC_TICH_ID`/`FILE_HO_SO_ID`; trong khi entity backend `NhNnVn.java` và `docs/dashboard/hop-tac.md` lại dùng `QUOC_TICH_ID`, `FILE_HO_SO_ID`. Cần đồng bộ migration/DDL trước khi chốt SQL chính thức.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN.MA_DON_VI` hoặc `HOC_VIEN.MA_DON_VI`; mặc định theo quyền user |
| `namBaoCao` | Number | `NAM_NHAP_HOC`, `EXTRACT(YEAR FROM HOC_VIEN.NGAY_NHAP_HOC)` hoặc ngày lớp HTQT |
| `tuNgayNhapHoc` | Date | Lọc khối nhập học theo `HOC_VIEN.NGAY_NHAP_HOC` hoặc `NAM_NHAP_HOC` |
| `denNgayNhapHoc` | Date | Lọc khối nhập học |
| `denNgayLuuLuong` | Date | Ngày chốt lưu lượng; mặc định cuối kỳ báo cáo |
| `quocTichIds` | String[] | Lọc quốc tịch/quốc gia |
| `trinhDoDaoTaoIds` | String[] | Lọc trình độ nếu cần |
| `lopDaoTaoId` | String | `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN.LOP_DAO_TAO_ID` hoặc lớp HTQT |
| `workflowStatus` | String | Mặc định `Approved` với bảng có workflow |

## 9. API report đề xuất

```http
GET /api/v1/reports/10h/hoc-vien-nuoc-ngoai
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namBaoCao` | Có | Dùng render header và lọc mặc định |
| `tuNgayNhapHoc` | Không | Nếu không truyền, suy ra từ `namBaoCao` |
| `denNgayNhapHoc` | Không | Nếu không truyền, suy ra từ `namBaoCao` |
| `denNgayLuuLuong` | Có | Ngày chốt lưu lượng |
| `countryMode` | Không | `QUOC_TICH` hoặc `QUOC_GIA_GUI`; mặc định cần xác nhận |
| `workflowStatus` | Không | Mặc định `Approved` |

Response đề xuất:

```json
{
  "reportCode": "10H",
  "title": "Thống kê học viên nước ngoài nhập học và lưu lượng học viên nước ngoài",
  "filters": {
    "maDonVi": "T01",
    "namBaoCao": 2026,
    "tuNgayNhapHoc": "2026-01-01",
    "denNgayNhapHoc": "2026-12-31",
    "denNgayLuuLuong": "2026-12-31",
    "countryMode": "QUOC_TICH"
  },
  "countries": [
    { "code": "LAO", "label": "Lào" },
    { "code": "KHM", "label": "Campuchia" },
    { "code": "OTHER", "label": "Khác" }
  ],
  "sections": [
    {
      "code": "nhapHoc",
      "title": "Học viên nước ngoài nhập học",
      "rows": [
        {
          "rowCode": "nghienCuuSinh",
          "stt": "1",
          "label": "Nghiên cứu sinh",
          "chiTieu": 0,
          "thucNhap": 0,
          "countryCounts": { "LAO": 0, "KHM": 0, "OTHER": 0 },
          "ghiChu": null
        }
      ]
    },
    {
      "code": "luuLuong",
      "title": "Lưu lượng học viên nước ngoài",
      "rows": [
        {
          "rowCode": "nghienCuuSinh",
          "stt": "1",
          "label": "Nghiên cứu sinh",
          "tong": 0,
          "countryCounts": { "LAO": 0, "KHM": 0, "OTHER": 0 },
          "ghiChu": null
        }
      ]
    }
  ],
  "warnings": [
    "RPT_10H_COUNTRY_SOURCE_NEEDS_CONFIRMATION"
  ]
}
```

## 10. SQL/Proc đề xuất

### 10.1. Ý tưởng tổng hợp

- Tạo CTE `base_inbound` từ `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN`, join `HOC_VIEN` qua `NGUOI_HOC_ID` nếu `NGUOI_HOC_ID` là `HOC_VIEN.ID`.
- Join `LOP_DAO_TAO_BOI_DUONG_QT` qua `LOP_DAO_TAO_ID` nếu schema runtime có field này.
- Resolve quốc gia theo cấu hình:
  - Ưu tiên `NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN.QUOC_TICH_ID -> DM_QUOC_TICH`.
  - Fallback `CON_NGUOI.QUOC_TICH_ID -> DM_QUOC_TICH`.
  - Nếu nghiệp vụ chốt “quốc gia gửi” khác quốc tịch, dùng lớp/thỏa thuận và `DM_QUOC_GIA`.
- Dùng bảng cấu hình dòng `RPT_10H_ROW_DEF` và `RPT_10H_ROW_RULE` để tránh hard-code tên tiếng Việt trong SQL.

### 10.2. Skeleton SQL

```sql
WITH params AS (
    SELECT
        :ma_don_vi AS ma_don_vi,
        :tu_ngay_nhap_hoc AS tu_ngay_nhap_hoc,
        :den_ngay_nhap_hoc AS den_ngay_nhap_hoc,
        :den_ngay_luu_luong AS den_ngay_luu_luong,
        NVL(:workflow_status, 'Approved') AS workflow_status
    FROM dual
),
base_inbound AS (
    SELECT
        nn.ID AS inbound_id,
        nn.NGUOI_HOC_ID,
        nn.MA_DON_VI,
        nn.WORKFLOW_STATUS,
        hv.ID AS hoc_vien_id,
        hv.TRINH_DO_DAO_TAO_ID,
        hv.HINH_THUC_DAO_TAO_ID,
        hv.LOAI_HINH_DAO_TAO_ID,
        hv.NGAY_NHAP_HOC,
        hv.TRANG_THAI_HOC_ID,
        hv.CON_NGUOI_ID,
        cn.QUOC_TICH_ID AS con_nguoi_quoc_tich_id,
        /* [Cần xác nhận schema] nn.QUOC_TICH_ID có trong entity nhưng chưa thấy trong DDL snapshot */
        COALESCE(nn.QUOC_TICH_ID, cn.QUOC_TICH_ID) AS quoc_tich_id,
        /* [Cần xác nhận schema] nn.LOP_DAO_TAO_ID có trong DDL snapshot nhưng chưa thấy trong entity */
        nn.LOP_DAO_TAO_ID,
        nn.NAM_NHAP_HOC
    FROM X02_APP.NGUOI_HOC_NUOC_NGOAI_HOC_TAI_VN nn
    LEFT JOIN X02_APP.HOC_VIEN hv
           ON hv.ID = nn.NGUOI_HOC_ID
          AND hv.IS_DELETED = 0
          AND hv.IS_ACTIVE = 1
    LEFT JOIN X02_APP.CON_NGUOI cn
           ON cn.ID = hv.CON_NGUOI_ID
          AND cn.IS_DELETED = 0
          AND cn.IS_ACTIVE = 1
    CROSS JOIN params p
    WHERE nn.IS_DELETED = 0
      AND nn.IS_ACTIVE = 1
      AND nn.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR nn.MA_DON_VI = p.ma_don_vi OR hv.MA_DON_VI = p.ma_don_vi)
),
row_mapped AS (
    SELECT
        rr.section_code,
        rr.row_code,
        b.inbound_id,
        b.NGAY_NHAP_HOC,
        b.NAM_NHAP_HOC,
        b.TRANG_THAI_HOC_ID,
        b.quoc_tich_id,
        b.LOP_DAO_TAO_ID
    FROM base_inbound b
    JOIN X02_APP.RPT_10H_ROW_RULE rr
      ON (rr.trinh_do_dao_tao_id IS NULL OR rr.trinh_do_dao_tao_id = b.trinh_do_dao_tao_id)
     AND (rr.hinh_thuc_dao_tao_id IS NULL OR rr.hinh_thuc_dao_tao_id = b.hinh_thuc_dao_tao_id)
     AND (rr.loai_hinh_dao_tao_id IS NULL OR rr.loai_hinh_dao_tao_id = b.loai_hinh_dao_tao_id)
),
nhap_hoc AS (
    SELECT
        rm.row_code,
        rm.quoc_tich_id,
        COUNT(DISTINCT rm.inbound_id) AS thuc_nhap
    FROM row_mapped rm
    CROSS JOIN params p
    WHERE rm.section_code = 'NHAP_HOC'
      AND (p.tu_ngay_nhap_hoc IS NULL OR rm.ngay_nhap_hoc >= p.tu_ngay_nhap_hoc)
      AND (p.den_ngay_nhap_hoc IS NULL OR rm.ngay_nhap_hoc < p.den_ngay_nhap_hoc + 1)
    GROUP BY rm.row_code, rm.quoc_tich_id
),
luu_luong AS (
    SELECT
        rm.row_code,
        rm.quoc_tich_id,
        COUNT(DISTINCT rm.inbound_id) AS tong
    FROM row_mapped rm
    CROSS JOIN params p
    WHERE rm.section_code = 'LUU_LUONG'
      AND (rm.ngay_nhap_hoc IS NULL OR rm.ngay_nhap_hoc <= p.den_ngay_luu_luong)
      AND EXISTS (
          SELECT 1
          FROM X02_APP.RPT_10H_TRANG_THAI_LUU_LUONG st
          WHERE st.trang_thai_hoc_id = rm.trang_thai_hoc_id
      )
    GROUP BY rm.row_code, rm.quoc_tich_id
)
SELECT
    rd.section_code,
    rd.excel_row,
    rd.row_code,
    rd.stt,
    rd.label,
    qt.MA AS country_code,
    qt.TEN AS country_label,
    NVL(nh.thuc_nhap, 0) AS thuc_nhap,
    NVL(ll.tong, 0) AS luu_luong
FROM X02_APP.RPT_10H_ROW_DEF rd
LEFT JOIN nhap_hoc nh
       ON nh.row_code = rd.row_code
      AND rd.section_code = 'NHAP_HOC'
LEFT JOIN luu_luong ll
       ON ll.row_code = rd.row_code
      AND rd.section_code = 'LUU_LUONG'
LEFT JOIN X02_DM.DM_QUOC_TICH qt
       ON qt.ID = COALESCE(nh.quoc_tich_id, ll.quoc_tich_id)
ORDER BY rd.section_order, rd.excel_row, qt.TEN;
```

`[Cần xác nhận schema]` Skeleton trên giả định runtime có `nn.QUOC_TICH_ID` và `nn.LOP_DAO_TAO_ID`. Nếu chỉ có một trong hai field, cần tách truy vấn theo schema thực tế hoặc tạo view chuẩn hóa `VW_RPT_NGUOI_HOC_NUOC_NGOAI`.

## 11. Quy tắc đối soát

| Nhóm kiểm tra | Quy tắc |
|---|---|
| Tổng nhập học | `nhapHoc.tong.thucNhap = SUM(thucNhap các dòng lá)` |
| Tổng lưu lượng | `luuLuong.tong.tong = SUM(tong các dòng lá)` |
| Quốc gia | Tổng theo quốc gia trong từng khối không vượt quá tổng cùng dòng nếu mỗi người chỉ thuộc một quốc gia |
| Chỉ tiêu | `thucNhap <= chiTieu` nếu chỉ tiêu lấy từ thỏa thuận/lớp và nghiệp vụ yêu cầu không vượt chỉ tiêu |
| Lưu lượng so với nhập học | Lưu lượng tại `denNgayLuuLuong` có thể lớn hơn nhập học trong kỳ vì là lũy kế nhiều khóa |
| Trạng thái | Chỉ đếm lưu lượng với trạng thái còn học/còn quản lý; không đếm đã kết thúc, thôi học, đã tốt nghiệp nếu nghiệp vụ loại trừ |
| Quốc tịch/quốc gia gửi | Không trộn `DM_QUOC_TICH` và `DM_QUOC_GIA` trong cùng một lần xuất nếu chưa có bảng map chuẩn |

## 12. Gap và câu hỏi cần xác nhận

| Nhóm | Vấn đề | Câu hỏi |
|---|---|---|
| Kỳ báo cáo | Header ghi năm 2025 | 10H chạy cho năm 2025 hay đồng bộ kỳ 2026 như các mẫu mới? |
| Công thức | `H11=SUM(#REF!)`, thiếu tổng cột `I` | Có phải lỗi template cần sửa Excel gốc không? |
| Quốc gia | Header ghi quốc gia gửi đào tạo, hệ thống hiện thiên về quốc tịch inbound | Dùng `QUOC_TICH_ID`, quốc gia của lớp/thỏa thuận, hay field mới “quốc gia gửi”? |
| Schema | DDL và entity lệch `QUOC_TICH_ID`, `FILE_HO_SO_ID`, `LOP_DAO_TAO_ID`, `NAM_NHAP_HOC` | Schema runtime chuẩn là bản nào? |
| Join người học | `NGUOI_HOC_ID` có chắc trỏ `HOC_VIEN.ID` không? | Nếu trỏ entity người học khác, cần view bridge sang `HOC_VIEN`/`CON_NGUOI`. |
| Trình độ/loại hình | 10H cần nhóm NCS/Cao học/Đại học/Trung cấp và bồi dưỡng khác | Mapping dùng `HOC_VIEN.TRINH_DO_DAO_TAO_ID` hay `LOP_DAO_TAO_BOI_DUONG_QT.TRINH_DO_DAO_TAO`? |
| Chỉ tiêu | Cột chỉ tiêu chỉ có ở khối nhập học | Lấy từ `SL_HOC_VIEN_THOA_THUAN`, chỉ tiêu tuyển sinh, hay nhập tay? |
| Lưu lượng | Cần xác định trạng thái còn thuộc lưu lượng | Bao gồm bảo lưu/gia hạn hay chỉ đang học? |
| Quốc gia động | Template chỉ có Lào, Campuchia và `……` | Export cố định 3 cột hay sinh cột theo top/quốc gia thực tế? |

## 13. Tham chiếu

- `docs/report-input/10H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/hop-tac.md`
- `docs/dashboard/LRN-dashboard.md`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/intl/intnhnnvn/entity/NhNnVn.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/intl/intnhnnvn/controller/NhNnVnController.java`
- `src/frontend/frontend-x02-v2/src/domains/int/pages/IntNhNnVnListPage.jsx`
- `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`

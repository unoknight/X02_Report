# Báo cáo 11H - Thống kê số liệu khen thưởng - kỷ luật học viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/11H.xlsx` |
| Sheet | `KT-KL Hoc vien` |
| Mã biểu mẫu | `Biểu mẫu 11H` |
| Tên báo cáo | `THỐNG KÊ SỐ LIỆU KHEN THƯỞNG - KỶ LUẬT HỌC VIÊN` |
| Vùng dữ liệu có giá trị | `A1:I25` |
| Vùng style kéo dài | `A1:AB45` |
| Công thức Excel | Có 1 công thức: `D13=SUM(D7:D12)` |
| Dạng báo cáo | Tổng hợp khen thưởng theo cấp, danh hiệu thi đua và kỷ luật học viên theo hình thức, giới tính, đối tượng nhập học, nội dung vi phạm |

`[Cần xác nhận]` Template chỉ có công thức tổng số lượng cấp khen thưởng tại `D13`; không có công thức cho cột nữ `E13`, tổng danh hiệu thi đua row 18, hoặc tổng kỷ luật. Khi triển khai nên tính tổng bằng code/SQL thay vì phụ thuộc công thức Excel.

## 2. Mục đích nghiệp vụ

Báo cáo theo dõi số liệu học viên được khen thưởng và bị kỷ luật trong kỳ báo cáo:

- Khối khen thưởng theo cấp khen thưởng.
- Khối danh hiệu thi đua của học viên/học sinh.
- Khối kỷ luật theo hình thức kỷ luật, nữ, đối tượng nhập học và nội dung vi phạm.

`[Suy luận]` Mẫu 11H thuộc phân hệ người học (`LRN`), nguồn chính là các bảng sự kiện `HV_KHEN_THUONG`, `HV_KY_LUAT`, `HV_VI_PHAM_QUY_CHE`, join `HOC_VIEN` và `CON_NGUOI` để lấy đối tượng nhập học, giới tính, đơn vị và các bộ lọc học viên.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:I1` | `Biểu mẫu 11H` | Merged |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:I3` | Tên báo cáo và dòng kèm theo báo cáo | Merged, có năm 2025 |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |

`[Cần xác nhận]` Header ghi `tháng 5 năm 2025`. Cần chốt kỳ báo cáo hoặc render động theo tham số xuất báo cáo.

### 3.2. Khối khen thưởng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A5:I5` | `KHEN THƯỞNG` | Section `khenThuong` |
| `A6` | `1` | Số thứ tự nhóm |
| `B6:C6` | `Cấp khen thưởng` | `rowLabel`, `capKhenThuong` |
| `D6` | `Số lượng` | `soLuong` |
| `E6` | `Nữ` | `nu` |
| `F6:I6` | `Ghi chú` | `ghiChu` |
| `B7:C12` | Các cấp khen thưởng | Dòng lá |
| `B13:C13` | `Tổng` | Dòng tổng |

### 3.3. Khối danh hiệu thi đua

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A15:A18` | `2` | Số thứ tự nhóm, merged dọc |
| `B14:C14` | `Danh hiệu thi đua` | `rowLabel`, `danhHieuThiDua` |
| `D14` | `Số lượng` | `soLuong` |
| `E14` | `Nữ` | `nu` |
| `F14:I14` | `Ghi chú` | `ghiChu` |
| `B15:C17` | Học viên xuất sắc/giỏi/khá | Dòng lá |
| `B18:C18` | `Tổng` | Dòng tổng |

### 3.4. Khối kỷ luật

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A19:I19` | `KỶ LUẬT` | Section `kyLuat` |
| `B20:C21` | `Hình thức kỷ luật` | `hinhThucKyLuat`, `rowLabel` |
| `D20:D21` | `Số lượng` | `soLuong` |
| `E20:E21` | `Nữ` | `nu` |
| `F20:H20` | `Đối tượng nhập học` | Nhóm đối tượng |
| `F21` | `Cán bộ` | `canBo` |
| `G21` | `CSNV` | `csnv` |
| `H21` | `HSPT` | `hocSinhPhoThong` |
| `I20:I21` | `Nội dung vi phạm` | `noiDungViPham` hoặc danh sách/nhóm nội dung |
| `B22:C25` | Tước danh hiệu CAND, buộc thôi học, cảnh cáo, khiển trách | Dòng lá |

## 4. Mapping dòng chỉ tiêu

| Khối | Dòng Excel | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---:|---|---|---|
| Khen thưởng | 7 | Cấp Nhà nước | `capNhaNuoc` | `HV_KHEN_THUONG.CAP_KHEN_THUONG_ID -> DM_CAP_KHEN_THUONG`, mã/tên cấp Nhà nước |
| Khen thưởng | 8 | Cấp Bộ Công an và tương đương | `capBoCongAnTuongDuong` | `DM_CAP_KHEN_THUONG` mã `BCA` và các cấp tương đương `[Cần mapping danh mục]` |
| Khen thưởng | 9 | Cấp Cục và tương đương | `capCucTuongDuong` | `DM_CAP_KHEN_THUONG` mã `CUC` và tương đương |
| Khen thưởng | 10 | Quỹ khuyến học Bộ Công an | `quyKhuyenHocBoCongAn` | `[Cần xác nhận]` Có thể là `CAP_KHEN_THUONG_ID`, `HINH_THUC_KHEN_THUONG_ID`, `GIAI_THUONG_ID` hoặc `LY_DO_KHEN_THUONG` |
| Khen thưởng | 11 | Cấp trường | `capTruong` | `DM_CAP_KHEN_THUONG` mã `TR`/`HV` |
| Khen thưởng | 12 | Cơ quan khác khen | `coQuanKhacKhen` | Các cấp ngoài danh sách trên hoặc mã cấp khác |
| Khen thưởng | 13 | Tổng | `tongKhenThuongTheoCap` | Tổng row 7-12 |
| Danh hiệu | 15 | Học viên xuất sắc | `hocVienXuatSac` | `[Cần mapping danh mục]` Ưu tiên danh mục hình thức khen thưởng/danh hiệu thi đua nếu có |
| Danh hiệu | 16 | Học viên (học sinh) giỏi | `hocVienGioi` | `[Cần mapping danh mục]` |
| Danh hiệu | 17 | Học viên (học sinh) khá | `hocVienKha` | `[Cần mapping danh mục]` |
| Danh hiệu | 18 | Tổng | `tongDanhHieuThiDua` | Tổng row 15-17 |
| Kỷ luật | 22 | Tước danh hiệu CAND | `tuocDanhHieuCand` | `HV_KY_LUAT.HINH_THUC_KY_LUAT_ID -> DM_HINH_THUC_KY_LUAT`, mã `TXD` hoặc tên tương ứng `[Cần xác nhận tên CAND/học viên]` |
| Kỷ luật | 23 | Buộc thôi học | `buocThoiHoc` | `DM_HINH_THUC_KY_LUAT` mã `TH`/tên `Thôi học` hoặc hình thức buộc thôi học |
| Kỷ luật | 24 | Cảnh cáo | `canhCao` | `DM_HINH_THUC_KY_LUAT` mã `CB` |
| Kỷ luật | 25 | Khiển trách | `khienTrach` | `DM_HINH_THUC_KY_LUAT` mã `KN` |

`[Cần xác nhận]` Danh mục `DM_HINH_THUC_KY_LUAT` hiện có `Tước danh hiệu học viên`, không thấy đúng literal `Tước danh hiệu CAND`; cần chốt dùng chung hay bổ sung mã riêng cho học viên CAND.

## 5. Mapping cột giá trị

| Khối | Cột | Header | Field đề xuất | Mapping DB đề xuất |
|---|---|---|---|---|
| Khen thưởng | `D` | Số lượng | `soLuong` | Count bản ghi `HV_KHEN_THUONG.ID` đã duyệt, không xóa, còn hiệu lực |
| Khen thưởng | `E` | Nữ | `nu` | Join `HOC_VIEN.CON_NGUOI_ID = CON_NGUOI.ID`, `CON_NGUOI.GIOI_TINH` là nữ |
| Khen thưởng | `F:I` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay |
| Danh hiệu | `D` | Số lượng | `soLuong` | Count bản ghi khen thưởng/danh hiệu theo danh mục đã chốt |
| Danh hiệu | `E` | Nữ | `nu` | Join `CON_NGUOI` |
| Danh hiệu | `F:I` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay |
| Kỷ luật | `D` | Số lượng | `soLuong` | Count bản ghi `HV_KY_LUAT.ID`; có thể union `HV_VI_PHAM_QUY_CHE` nếu nghiệp vụ coi vi phạm có xử lý là kỷ luật `[Cần xác nhận]` |
| Kỷ luật | `E` | Nữ | `nu` | Join `CON_NGUOI` |
| Kỷ luật | `F` | Cán bộ | `canBo` | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID -> DM_DOI_TUONG_NHAP_HOC` |
| Kỷ luật | `G` | CSNV | `csnv` | Đối tượng nhập học chiến sĩ nghĩa vụ `[Cần mapping danh mục]` |
| Kỷ luật | `H` | HSPT | `hocSinhPhoThong` | Đối tượng học sinh phổ thông `[Cần mapping danh mục]` |
| Kỷ luật | `I` | Nội dung vi phạm | `noiDungViPham` | `HV_KY_LUAT.PHAN_LOAI_VI_PHAM_ID`/`CHI_TIET_VI_PHAM` hoặc `HV_VI_PHAM_QUY_CHE.NOI_DUNG_VI_PHAM` |

## 6. Công thức Excel trong template

| Ô | Ý nghĩa | Công thức | Nhận xét |
|---|---|---|---|
| `D13` | Tổng số lượng khen thưởng theo cấp | `=SUM(D7:D12)` | Chỉ cộng cột số lượng |

Các tổng còn thiếu:

| Vùng | Tổng nên có | Ghi chú |
|---|---|---|
| `E13` | Tổng nữ khối cấp khen thưởng | Template để trống |
| `D18:E18` | Tổng danh hiệu thi đua | Template để trống |
| Khối kỷ luật | Không có dòng tổng | Nếu nghiệp vụ cần tổng, API nên trả thêm row tổng nhưng export 11H hiện không có dòng tổng |

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HV_KHEN_THUONG` / `/api/v1/khen-thuong-nguoi-hoc` | Nguồn khen thưởng học viên | `HOC_VIEN_ID`, `CAP_KHEN_THUONG_ID`, `LINH_VUC_KHEN_THUONG_ID`, `HINH_THUC_KHEN_THUONG_ID`, `GIAI_THUONG_ID`, `NAM_KHEN_THUONG_ID`, `QUYET_DINH_KHEN_THUONG_ID`, workflow fields |
| `X02_APP.HV_KY_LUAT` / `/api/v1/ky-luat-nguoi-hoc` | Nguồn kỷ luật học viên | `HOC_VIEN_ID`, `PHAN_LOAI_VI_PHAM_ID`, `CHI_TIET_VI_PHAM`, `HINH_THUC_KY_LUAT_ID`, `QUYET_DINH_KY_LUAT_ID`, workflow fields |
| `X02_APP.HV_VI_PHAM_QUY_CHE` / `/api/v1/vi-pham-quy-che` | Nguồn bổ trợ nội dung vi phạm/xử lý | `HOC_VIEN_ID`, `NOI_DUNG_VI_PHAM`, `HINH_THUC_XU_LY_ID`, `QUYET_DINH_XU_LY_ID`, workflow fields |
| `X02_APP.HOC_VIEN` | Join hồ sơ học viên | `ID`, `CON_NGUOI_ID`, `DOI_TUONG_NHAP_HOC_ID`, `TRINH_DO_DAO_TAO_ID`, `NGANH_ID`, `KHOA_HOC_ID`, `TRANG_THAI_HOC_ID`, `MA_DON_VI` |
| `X02_APP.CON_NGUOI` | Nguồn giới tính | `ID`, `GIOI_TINH` |
| `X02_DM.DM_CAP_KHEN_THUONG` | Mapping cấp khen thưởng | `ID`, `MA`, `TEN` |
| `X02_DM.DM_LINH_VUC_KHEN_THUONG` | Mapping lĩnh vực khen thưởng nếu cần phân tích sâu | `ID`, `MA`, `TEN` |
| `X02_DM.DM_HINH_THUC_KY_LUAT` | Mapping hình thức kỷ luật | `ID`, `MA`, `TEN`, `DOI_TUONG_SD` |
| `X02_DM.DM_NOI_DUNG_VI_PHAM` | Mapping nội dung vi phạm nếu dùng danh mục | `ID`, `MA`, `TEN` |
| `X02_DM.DM_DOI_TUONG_NHAP_HOC` | Mapping cán bộ/CSNV/HSPT | `ID`, `MA`, `TEN` |

`[Cần xác nhận]` Tài liệu backend domain map có object cũ `KHEN_THUONG_NGUOI_HOC`, `KY_LUAT_NGUOI_HOC`, `VI_PHAM_QUY_CHE`, nhưng entity hiện hành đang map vào bảng `HV_KHEN_THUONG`, `HV_KY_LUAT`, `HV_VI_PHAM_QUY_CHE`. Báo cáo nên dùng bảng/entity hiện hành.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `HV_KHEN_THUONG.MA_DON_VI`, `HV_KY_LUAT.MA_DON_VI`, hoặc qua `HOC_VIEN.MA_DON_VI`; mặc định theo quyền user |
| `namHocId` | String | `HV_KHEN_THUONG.NAM_KHEN_THUONG_ID`; với kỷ luật cần chốt năm học hoặc dùng ngày duyệt/tạo |
| `tuNgay` | Date | `APPROVED_AT` hoặc ngày quyết định nếu có |
| `denNgay` | Date | `APPROVED_AT` hoặc ngày quyết định nếu có |
| `doiTuongNhapHocIds` | String[] | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID` |
| `trinhDoDaoTaoIds` | String[] | `HOC_VIEN.TRINH_DO_DAO_TAO_ID` |
| `khoaHocId` | String | `HOC_VIEN.KHOA_HOC_ID` |
| `workflowStatus` | String | Mặc định `Approved` |

`[Cần xác nhận]` Với kỷ luật, nếu không có năm học riêng, nên dùng `HV_KY_LUAT.APPROVED_AT` hoặc ngày quyết định kỷ luật từ bảng văn bản/quyết định. Không nên dùng `CREATED_AT` làm nguồn chính thức nếu đã có ngày quyết định.

## 9. API report đề xuất

```http
GET /api/v1/reports/11h/khen-thuong-ky-luat-hoc-vien
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Không | Ưu tiên cho khen thưởng |
| `tuNgay` | Không | Bắt buộc nếu không truyền năm/kỳ |
| `denNgay` | Không | Bắt buộc nếu không truyền năm/kỳ |
| `workflowStatus` | Không | Mặc định `Approved` |
| `includeViPhamQuyChe` | Không | Có union `HV_VI_PHAM_QUY_CHE` vào nội dung kỷ luật hay không |

Response đề xuất:

```json
{
  "reportCode": "11H",
  "title": "Thống kê số liệu khen thưởng - kỷ luật học viên",
  "filters": {
    "maDonVi": "T01",
    "tuNgay": "2026-01-01",
    "denNgay": "2026-05-31",
    "workflowStatus": "Approved"
  },
  "sections": [
    {
      "code": "khenThuongCap",
      "rows": [
        { "rowCode": "capNhaNuoc", "label": "Cấp Nhà nước", "soLuong": 0, "nu": 0, "ghiChu": null }
      ],
      "total": { "soLuong": 0, "nu": 0 }
    },
    {
      "code": "danhHieuThiDua",
      "rows": [
        { "rowCode": "hocVienXuatSac", "label": "Học viên xuất sắc", "soLuong": 0, "nu": 0, "ghiChu": null }
      ],
      "total": { "soLuong": 0, "nu": 0 }
    },
    {
      "code": "kyLuat",
      "rows": [
        {
          "rowCode": "khienTrach",
          "label": "Khiển trách",
          "soLuong": 0,
          "nu": 0,
          "canBo": 0,
          "csnv": 0,
          "hocSinhPhoThong": 0,
          "noiDungViPham": []
        }
      ]
    }
  ],
  "warnings": [
    "RPT_11H_DANH_HIEU_THI_DUA_NEEDS_MAPPING"
  ]
}
```

## 10. SQL/Proc đề xuất

### 10.1. Ý tưởng tổng hợp

- Dùng bảng cấu hình dòng `RPT_11H_ROW_DEF` và `RPT_11H_ROW_RULE` để map các dòng template với danh mục khen thưởng/kỷ luật.
- Với khen thưởng: aggregate `HV_KHEN_THUONG`, join `DM_CAP_KHEN_THUONG`, `HOC_VIEN`, `CON_NGUOI`.
- Với danh hiệu thi đua: cần chốt nguồn danh mục. Nếu nằm ở `HINH_THUC_KHEN_THUONG_ID`, dùng cùng `HV_KHEN_THUONG` nhưng rule khác.
- Với kỷ luật: aggregate `HV_KY_LUAT`, join `DM_HINH_THUC_KY_LUAT`, `HOC_VIEN`, `CON_NGUOI`, `DM_DOI_TUONG_NHAP_HOC`.
- Nội dung vi phạm nên lấy từ `PHAN_LOAI_VI_PHAM_ID` nếu có danh mục; fallback `CHI_TIET_VI_PHAM`. Nếu cần dữ liệu vi phạm quy chế chi tiết, join/union thêm `HV_VI_PHAM_QUY_CHE`.

### 10.2. Skeleton SQL

```sql
WITH params AS (
    SELECT
        :ma_don_vi AS ma_don_vi,
        :tu_ngay AS tu_ngay,
        :den_ngay AS den_ngay,
        NVL(:workflow_status, 'Approved') AS workflow_status
    FROM dual
),
khen_thuong AS (
    SELECT
        rr.row_code,
        COUNT(*) AS so_luong,
        SUM(CASE WHEN UPPER(NVL(cn.GIOI_TINH, '')) IN ('NU', 'NỮ', 'FEMALE') THEN 1 ELSE 0 END) AS nu
    FROM X02_APP.HV_KHEN_THUONG kt
    JOIN X02_APP.HOC_VIEN hv
      ON hv.ID = kt.HOC_VIEN_ID
     AND hv.IS_DELETED = 0
     AND hv.IS_ACTIVE = 1
    LEFT JOIN X02_APP.CON_NGUOI cn
      ON cn.ID = hv.CON_NGUOI_ID
     AND cn.IS_DELETED = 0
     AND cn.IS_ACTIVE = 1
    JOIN X02_APP.RPT_11H_ROW_RULE rr
      ON rr.section_code IN ('KHEN_THUONG_CAP', 'DANH_HIEU_THI_DUA')
     AND (rr.cap_khen_thuong_id IS NULL OR rr.cap_khen_thuong_id = kt.CAP_KHEN_THUONG_ID)
     AND (rr.hinh_thuc_khen_thuong_id IS NULL OR rr.hinh_thuc_khen_thuong_id = kt.HINH_THUC_KHEN_THUONG_ID)
     AND (rr.giai_thuong_id IS NULL OR rr.giai_thuong_id = kt.GIAI_THUONG_ID)
    CROSS JOIN params p
    WHERE kt.IS_DELETED = 0
      AND kt.IS_ACTIVE = 1
      AND kt.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR kt.MA_DON_VI = p.ma_don_vi OR hv.MA_DON_VI = p.ma_don_vi)
      AND (p.tu_ngay IS NULL OR kt.APPROVED_AT >= p.tu_ngay)
      AND (p.den_ngay IS NULL OR kt.APPROVED_AT < p.den_ngay + 1)
    GROUP BY rr.row_code
),
ky_luat AS (
    SELECT
        rr.row_code,
        COUNT(*) AS so_luong,
        SUM(CASE WHEN UPPER(NVL(cn.GIOI_TINH, '')) IN ('NU', 'NỮ', 'FEMALE') THEN 1 ELSE 0 END) AS nu,
        SUM(CASE WHEN dt.map_col = 'CAN_BO' THEN 1 ELSE 0 END) AS can_bo,
        SUM(CASE WHEN dt.map_col = 'CSNV' THEN 1 ELSE 0 END) AS csnv,
        SUM(CASE WHEN dt.map_col = 'HSPT' THEN 1 ELSE 0 END) AS hoc_sinh_pho_thong,
        LISTAGG(DISTINCT COALESCE(ndvp.TEN, kl.CHI_TIET_VI_PHAM), '; ')
            WITHIN GROUP (ORDER BY COALESCE(ndvp.TEN, kl.CHI_TIET_VI_PHAM)) AS noi_dung_vi_pham
    FROM X02_APP.HV_KY_LUAT kl
    JOIN X02_APP.HOC_VIEN hv
      ON hv.ID = kl.HOC_VIEN_ID
     AND hv.IS_DELETED = 0
     AND hv.IS_ACTIVE = 1
    LEFT JOIN X02_APP.CON_NGUOI cn
      ON cn.ID = hv.CON_NGUOI_ID
     AND cn.IS_DELETED = 0
     AND cn.IS_ACTIVE = 1
    LEFT JOIN X02_APP.RPT_DOI_TUONG_NHAP_HOC_MAP dt
      ON dt.doi_tuong_nhap_hoc_id = hv.DOI_TUONG_NHAP_HOC_ID
    LEFT JOIN X02_DM.DM_NOI_DUNG_VI_PHAM ndvp
      ON ndvp.ID = kl.PHAN_LOAI_VI_PHAM_ID
    JOIN X02_APP.RPT_11H_ROW_RULE rr
      ON rr.section_code = 'KY_LUAT'
     AND (rr.hinh_thuc_ky_luat_id IS NULL OR rr.hinh_thuc_ky_luat_id = kl.HINH_THUC_KY_LUAT_ID)
    CROSS JOIN params p
    WHERE kl.IS_DELETED = 0
      AND kl.IS_ACTIVE = 1
      AND kl.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR kl.MA_DON_VI = p.ma_don_vi OR hv.MA_DON_VI = p.ma_don_vi)
      AND (p.tu_ngay IS NULL OR kl.APPROVED_AT >= p.tu_ngay)
      AND (p.den_ngay IS NULL OR kl.APPROVED_AT < p.den_ngay + 1)
    GROUP BY rr.row_code
)
SELECT
    rd.section_code,
    rd.excel_row,
    rd.row_code,
    rd.label,
    NVL(kt.so_luong, kl.so_luong) AS so_luong,
    NVL(kt.nu, kl.nu) AS nu,
    kl.can_bo,
    kl.csnv,
    kl.hoc_sinh_pho_thong,
    kl.noi_dung_vi_pham
FROM X02_APP.RPT_11H_ROW_DEF rd
LEFT JOIN khen_thuong kt
       ON kt.row_code = rd.row_code
LEFT JOIN ky_luat kl
       ON kl.row_code = rd.row_code
ORDER BY rd.excel_row;
```

`[Cần xác nhận]` SQL skeleton dùng `APPROVED_AT` làm ngày nghiệp vụ vì DDL chưa thể hiện ngày quyết định trên bảng sự kiện. Nếu có bảng/văn bản quyết định với ngày ban hành, nên dùng ngày quyết định để lọc báo cáo.

## 11. Quy tắc đối soát

| Nhóm kiểm tra | Quy tắc |
|---|---|
| Khen thưởng theo cấp | `D13 = SUM(D7:D12)` và nên bổ sung `E13 = SUM(E7:E12)` trong code |
| Danh hiệu thi đua | `D18 = SUM(D15:D17)`, `E18 = SUM(E15:E17)` nếu giữ dòng tổng |
| Kỷ luật | `nu <= soLuong` từng hình thức |
| Đối tượng kỷ luật | `canBo + csnv + hocSinhPhoThong <= soLuong` nếu chỉ thống kê 3 nhóm này; phần còn lại phải có warning hoặc ghi chú |
| Workflow | Chỉ đếm bản ghi đã duyệt, không xóa, còn hiệu lực |
| Không đếm trùng | Một học viên có nhiều quyết định trong kỳ được tính theo lượt hay theo người cần chốt; mặc định nên tính theo lượt bản ghi |
| Nội dung vi phạm | Nếu một hình thức có nhiều nội dung, cột `I` nên trả danh sách/top nội dung thay vì một text duy nhất bị mất dữ liệu |

## 12. Gap và câu hỏi cần xác nhận

| Nhóm | Vấn đề | Câu hỏi |
|---|---|---|
| Kỳ báo cáo | Header ghi năm 2025 | 11H chạy cho năm 2025 hay render động theo kỳ hiện tại? |
| Công thức | Chỉ có `D13`, thiếu các tổng khác | Có cần sửa template Excel gốc hay tính tổng trong export? |
| Danh hiệu thi đua | Chưa thấy bảng/danh mục riêng trong DDL đã đọc | Lấy từ `HINH_THUC_KHEN_THUONG_ID`, `GIAI_THUONG_ID`, `LINH_VUC_KHEN_THUONG_ID` hay bảng phân loại học tập/rèn luyện? |
| Quỹ khuyến học BCA | Chưa rõ nằm ở cấp, hình thức, giải thưởng hay lý do | Cần mã danh mục chính thức cho dòng này. |
| Kỷ luật | Template có `Tước danh hiệu CAND`, danh mục có `Tước danh hiệu học viên` | Có dùng chung một mã không? |
| Buộc thôi học | Danh mục có `Thôi học`, chưa thấy literal `Buộc thôi học` | Cần xác nhận mapping mã. |
| Nội dung vi phạm | `HV_KY_LUAT` có `PHAN_LOAI_VI_PHAM_ID`/`CHI_TIET_VI_PHAM`; `HV_VI_PHAM_QUY_CHE` có `NOI_DUNG_VI_PHAM` | Cột `I` lấy từ bảng kỷ luật hay từ vi phạm quy chế? |
| Đối tượng nhập học | Template chỉ có cán bộ, CSNV, HSPT | Các nhóm khác xử lý thế nào: bỏ, gom khác, hay ghi chú? |

## 13. Tham chiếu

- `docs/report-input/11H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/LRN-dashboard.md`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/khenthuongnguoihoc/entity/KhenThuongNguoiHoc.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/kyluatnguoihoc/entity/KyLuatNguoiHoc.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/hocvienviphamquyche/entity/HocVienViPhamQuyChe.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/overview/service/LrnOverviewService.java`
- `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`

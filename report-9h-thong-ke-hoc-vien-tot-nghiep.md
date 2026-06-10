# Báo cáo 9H - Thống kê học viên tốt nghiệp

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/9H.xlsx` |
| Sheet | `Tot nghiep` |
| Mã biểu mẫu | `Biểu mẫu 9H` |
| Tên báo cáo | `THỐNG KÊ HỌC VIÊN TỐT NGHIỆP` |
| Vùng dữ liệu có giá trị | `A1:O37` |
| Vùng bảng chính | `A6:O37` |
| Vùng style kéo dài | `A1:AB63` |
| Công thức Excel | Có 22 công thức tổng tại row 10 và row 37 |
| Dạng báo cáo | Ma trận số nhập học/tốt nghiệp theo trình độ, hình thức, loại hình đào tạo và cơ cấu học viên tốt nghiệp |

`[Cần xác nhận]` Dòng kèm theo báo cáo ghi `tháng 5 năm 2025`, trong khi các mẫu 7H/8H ghi năm 2026. Cần xác nhận đây là kỳ báo cáo thật của 9H hay lỗi template.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê học viên tốt nghiệp theo trình độ, hình thức và loại hình đào tạo. Mỗi dòng thể hiện:

- Số nhập học của nhóm đào tạo.
- Số tốt nghiệp của nhóm đào tạo.
- Cơ cấu học viên tốt nghiệp theo đối tượng nhập học: cán bộ, CSNV, HSPT, HSVH, BQP, ngành khác, nước ngoài.
- Thành phần học viên tốt nghiệp: nữ, dân tộc thiểu số, đảng viên.

`[Suy luận]` Cột `Nhập học` dùng để đối chiếu đầu vào của khóa/loại hình đào tạo với số tốt nghiệp. Cột `Tốt nghiệp` và các cột E:N nên lấy từ tập học viên có quyết định/công nhận tốt nghiệp trong kỳ báo cáo. Nếu cơ cấu E:N tính trên số nhập học thay vì số tốt nghiệp thì cần xác nhận lại vì tiêu đề báo cáo là tốt nghiệp.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `O1` | `Biểu mẫu 9H` | Không merged; nằm cuối vùng header |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:O3` | `THỐNG KÊ HỌC VIÊN TỐT NGHIỆP` | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `C4:O4` | `(Kèm theo Báo cáo số ngày tháng 5 năm 2025)` | Merged |
| `A48:E48`, `I48:O48` | Vùng ký/ghi ngày | Có merged nhưng không có text |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A6:A8` | `TT` | `stt` |
| `B6:B8` | `Trình độ, hình thức, loại hình đào tạo` | `rowLabel`, `rowCode`, `parentCode` |
| `C6:C8` | `Nhập học` | `nhapHoc` |
| `D6:D8` | `Tốt nghiệp` | `totNghiep` |
| `E6:K6` | `Đối tượng nhập học` | Nhóm `doiTuongNhapHoc` |
| `E7:H7` | `Trong ngành` | Nhóm trong ngành |
| `E8` | `Cán bộ` | `canBo` |
| `F8` | `CSNV` | `csnv` |
| `G8` | `HSPT` | `hocSinhPhoThong` |
| `H8` | `HSVH` | `hocSinhVanHoa` |
| `I7:J7` | `Ngành ngoài` | Nhóm ngành ngoài |
| `I8` | `BQP` | `bqp` |
| `J8` | `Ngành khác` | `nganhKhac` |
| `K7:K8` | `Nước ngoài` | `nuocNgoai` |
| `L6:N6` | `Thành phần` | Nhóm thành phần |
| `L7:L8` | `Nữ` | `nu` |
| `M7:M8` | `Dân tộc thiểu số` | `danTocThieuSo` |
| `N7:N8` | `Đảng viên` | `dangVien` |
| `O6:O8` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 10 |  | Tổng | `tongSo` | Tổng row 12:40 theo công thức template; nên thay bằng tổng các dòng lá đã chốt |
| 11 | 1 | Đào tạo trình độ sau đại học | `sauDaiHoc` | Nhóm row 12-13 |
| 12 |  | Thạc sĩ | `thacSi` | `TRINH_DO_DAO_TAO_ID = thạc sĩ` |
| 13 |  | Tiến sĩ | `tienSi` | `TRINH_DO_DAO_TAO_ID = tiến sĩ` |
| 14 | 2 | Đào tạo trình độ đại học hệ chính quy | `daiHocChinhQuy` | Đại học, hình thức chính quy |
| 15 | 3 | Đào tạo hệ liên thông | `heLienThong` | Nhóm row 16-19 |
| 16 | 3.1 | Đào tạo tại trường Công an nhân dân | `lienThongTaiTruongCand` | Liên thông, tại trường CAND |
| 17 |  | Hình thức chính quy | `lienThongChinhQuy` | Liên thông, chính quy |
| 18 |  | Hình thức vừa làm vừa học | `lienThongVlvh` | Liên thông, VLVH |
| 19 | 3.2 | Đào tạo liên kết mở tại Công an các đơn vị, địa phương | `lienThongLienKet` | Liên thông, liên kết mở |
| 20 | 4 | Đào tạo trình độ đại học hình thức vừa làm vừa học | `daiHocVlvh` | Đại học, VLVH |
| 21 |  | Đào tạo tại trường Công an nhân dân | `daiHocVlvhTaiTruong` | VLVH tại trường CAND |
| 22 |  | Đào tạo liên kết mở tại Công an các đơn vị, địa phương | `daiHocVlvhLienKet` | VLVH liên kết |
| 23 |  | TC37 Yên Bái | `tc37YenBai` | `[Cần mapping danh mục]` Khóa/lớp/địa điểm đào tạo |
| 24 |  | TC37 Lai Châu | `tc37LaiChau` | `[Cần mapping danh mục]` Khóa/lớp/địa điểm đào tạo |
| 25 | 6 | Đào tạo cấp bằng đại học thứ 2 | `daiHocThu2` | `[Cần xác nhận]` Template nhảy từ STT 4 sang 6, thiếu STT 5 |
| 26 | 6.1 | Đào tạo tại trường | `daiHocThu2TaiTruong` | Đại học thứ 2 tại trường |
| 27 |  | Hình thức chính quy | `daiHocThu2ChinhQuy` | Đại học thứ 2, chính quy |
| 28 |  | Hình thức VLVH | `daiHocThu2Vlvh` | Đại học thứ 2, VLVH |
| 29 | 6.2 | Đào tạo liên kết mở tại Công an các đơn vị, địa phương | `daiHocThu2LienKet` | Đại học thứ 2, liên kết |
| 30 |  | VB2N20-Lào Cai | `vb2n20LaoCai` | `[Cần mapping danh mục]` Khóa/lớp/địa điểm |
| 31 |  | VB2N20-A08 | `vb2n20A08` | `[Cần mapping danh mục]` Khóa/lớp/đơn vị |
| 32 | 7 | Đào tạo trình độ cao đẳng | `caoDang` | `TRINH_DO_DAO_TAO_ID = cao đẳng` |
| 33 | 8 | Đào tạo trình độ trung cấp | `trungCap` | `TRINH_DO_DAO_TAO_ID = trung cấp` |
| 34 | 9 | Các loại hình đào tạo khác | `loaiHinhDaoTaoKhac` | Nhóm row 35-36 |
| 35 | 9.1 | Đào tạo lý luận chính trị | `daoTaoLyLuanChinhTri` | `[Cần mapping danh mục]` Chương trình/hình thức LLCT |
| 36 |  | Đào tạo cao cấp lý luận chính trị hệ tập trung | `llctCaoCapTapTrung` | Cao cấp LLCT, tập trung |
| 37 | 10 | Các loại hình bồi dưỡng | `cacLoaiHinhBoiDuong` | Công thức tham chiếu row 40 nhưng row 40 trống |

## 5. Mapping cột giá trị

| Cột | Header | Field đề xuất | Mapping DB đề xuất |
|---|---|---|---|
| `C` | Nhập học | `nhapHoc` | `COUNT(HOC_VIEN.ID)` theo nhóm dòng, lọc `NGAY_NHAP_HOC` theo khóa/kỳ đối chiếu hoặc theo cohort tốt nghiệp `[Cần xác nhận]` |
| `D` | Tốt nghiệp | `totNghiep` | `COUNT(HV_QUYET_DINH_TOT_NGHIEP.HOC_VIEN_ID)` đã duyệt trong kỳ; fallback `HOC_VIEN.TRANG_THAI_HOC_ID = Đã tốt nghiệp` |
| `E` | Cán bộ | `canBo` | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID -> DM_DOI_TUONG_NHAP_HOC` |
| `F` | CSNV | `csnv` | Chiến sĩ nghĩa vụ `[Cần mapping danh mục]` |
| `G` | HSPT | `hocSinhPhoThong` | Học sinh phổ thông/thí sinh tốt nghiệp THPT |
| `H` | HSVH | `hocSinhVanHoa` | Học sinh văn hóa |
| `I` | BQP | `bqp` | Bộ Quốc phòng gửi |
| `J` | Ngành khác | `nganhKhac` | Nhóm ngành khác |
| `K` | Nước ngoài | `nuocNgoai` | `CON_NGUOI.QUOC_TICH_ID` khác Việt Nam hoặc đối tượng quốc tế `[Cần mapping danh mục]` |
| `L` | Nữ | `nu` | `CON_NGUOI.GIOI_TINH = 'NU'` hoặc `NỮ` |
| `M` | Dân tộc thiểu số | `danTocThieuSo` | `CON_NGUOI.DAN_TOC_ID`, loại trừ dân tộc Kinh |
| `N` | Đảng viên | `dangVien` | `HOC_VIEN.NGAY_VAO_DANG`/`NGAY_CHUYEN_DANG_CHINH_THUC` hoặc `CON_NGUOI.NGAY_VAO_DANG` không null |
| `O` | Ghi chú | `ghiChu` | Text nhập tay/tổng hợp |

`[Cần xác nhận]` Các cột E:N nên đếm trong tập học viên tốt nghiệp, không phải tập nhập học, vì header báo cáo là tốt nghiệp. Nếu nghiệp vụ yêu cầu cơ cấu của số nhập học tương ứng, SQL cần tách hai tập `base_nhap_hoc` và `base_tot_nghiep` rõ ràng.

## 6. Công thức Excel trong template

| Dòng | Ý nghĩa | Công thức chính |
|---:|---|---|
| 10 | Tổng | D:N = `SUM(row 12:40)` |
| 37 | Các loại hình bồi dưỡng | D:N = `SUM(row 40:40)` |

Các điểm bất thường:

- Cột `C - Nhập học` không có công thức tổng ở row 10 và row 37.
- Row 10 cộng tới row 40 nhưng vùng có nhãn chỉ tới row 37; row 38-40 trống.
- Row 37 tham chiếu row 40 trống.
- Template thiếu STT 5 và không có dòng chi tiết cho bồi dưỡng.
- Các dòng nhóm row 11, 15, 16, 20, 22, 25, 26, 29, 34, 35 không có công thức tổng con riêng.

`[Cần xác nhận]` Nên cấu hình cây dòng trong code/DB thay vì copy nguyên công thức Excel. Nếu dùng nguyên template, tổng sẽ dễ sai khi nhập liệu vào dòng nhóm và dòng con song song.

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HOC_VIEN` / `/api/v1/learner-profile` | Nguồn hồ sơ học viên và cột nhập học | `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `LOAI_HINH_DAO_TAO_ID`, `NGANH_ID`, `CHUYEN_NGANH_ID`, `KHOA_HOC_ID`, `TRUNG_DOI_ID`, `NGAY_NHAP_HOC`, `DOI_TUONG_NHAP_HOC_ID`, `TRANG_THAI_HOC_ID`, `MA_DON_VI`, `NGAY_VAO_DANG` |
| `X02_APP.HV_QUYET_DINH_TOT_NGHIEP` / `/api/v1/quyet-dinh-tot-nghiep` | Nguồn học viên tốt nghiệp | `HOC_VIEN_ID`, `QUYET_DINH_TOT_NGHIEP_ID`, `XEP_LOAI_TOT_NGHIEP_ID`, `APPROVED_AT`, `WORKFLOW_STATUS`, `MA_DON_VI` |
| Object metadata `quyet_dinh_tot_nghiep` | Có field ngày quyết định tốt nghiệp | `quyet_dinh_tot_nghiep_id`, `ngay_quyet_dinh`, `xep_loai_tot_nghiep_id` theo `MD_OBJECT_FIELD_CONFIG` |
| `src/backend/qldt-v2/src/main/resources/app.sql` | Bản schema tham khảo có `QUYET_DINH_TOT_NGHIEP`, `KET_QUA_TOT_NGHIEP` | `NGAY_QUYET_DINH`, `NGAY_TOT_NGHIEP`, `QD_TOT_NGHIEP_ID` |
| `X02_APP.CON_NGUOI` | Nguồn giới tính, dân tộc, quốc tịch, ngày vào Đảng | `GIOI_TINH`, `DAN_TOC_ID`, `QUOC_TICH_ID`, `NGAY_VAO_DANG`, `NGAY_VAO_DANG_CHINH_THUC` |
| `X02_DM.DM_DOI_TUONG_NHAP_HOC` | Mapping cán bộ/CSNV/HSPT/HSVH/BQP/ngành khác | `MA`, `TEN`, `IS_TRONG_NGAY` |
| `X02_DM.DM_TRINH_DO_DAO_TAO` | Mapping thạc sĩ, tiến sĩ, đại học, cao đẳng, trung cấp | `MA`, `TEN` |
| `X02_DM.DM_HINH_THUC_DAO_TAO` | Mapping chính quy, VLVH, liên thông, bồi dưỡng | `MA`, `TEN` |
| `X02_DM.DM_LOAI_HINH_DAO_TAO` | Mapping tập trung, liên kết, loại hình tổ chức | `MA`, `TEN` |
| `X02_DM.DM_TRANG_THAI_HOC_VIEN` | Fallback xác định đã tốt nghiệp | `TEN = Đã tốt nghiệp` |

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `HOC_VIEN.MA_DON_VI` hoặc `HV_QUYET_DINH_TOT_NGHIEP.MA_DON_VI`; scope theo quyền user |
| `namHocId` | String | Nếu có quan hệ năm học/khóa; dùng cho cohort |
| `tuNgayTotNghiep` | Date | Ngày quyết định/tốt nghiệp hoặc `APPROVED_AT` của `HV_QUYET_DINH_TOT_NGHIEP` |
| `denNgayTotNghiep` | Date | Ngày kết thúc kỳ tốt nghiệp |
| `namNhapHoc` | Number | Dùng cho cột nhập học nếu đối chiếu theo năm nhập học |
| `coSoDaoTaoId` | String | `HOC_VIEN.CO_SO_DAO_TAO_ID` |
| `khoaHocId` | String | `HOC_VIEN.KHOA_HOC_ID` |
| `workflowStatus` | String | Mặc định `Approved` |

`[Cần xác nhận]` Cột nhập học nên lọc theo cùng khóa học của nhóm tốt nghiệp, theo năm nhập học, hay theo kỳ báo cáo. Đây là quyết định quan trọng để tránh so sánh sai cohort.

## 9. API report đề xuất

```http
GET /api/v1/reports/9h/hoc-vien-tot-nghiep
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `tuNgayTotNghiep` | Không | Nên có nếu không truyền năm học |
| `denNgayTotNghiep` | Không | Nên có nếu không truyền năm học |
| `namHocId` | Không | Dùng cho lọc cohort/năm học |
| `coSoDaoTaoId` | Không | Lọc cơ sở đào tạo |
| `khoaHocId` | Không | Lọc khóa |

Response đề xuất:

```json
{
  "reportCode": "9H",
  "title": "Thống kê học viên tốt nghiệp",
  "filters": {
    "maDonVi": "T01",
    "tuNgayTotNghiep": "2025-01-01",
    "denNgayTotNghiep": "2025-05-31"
  },
  "columns": [
    "rowCode",
    "rowLabel",
    "nhapHoc",
    "totNghiep",
    "canBo",
    "csnv",
    "hocSinhPhoThong",
    "hocSinhVanHoa",
    "bqp",
    "nganhKhac",
    "nuocNgoai",
    "nu",
    "danTocThieuSo",
    "dangVien",
    "ghiChu"
  ],
  "warnings": [
    "COLUMN_C_TOTAL_FORMULA_MISSING",
    "ROW_37_REFERENCES_EMPTY_ROW_40",
    "MISSING_STT_5",
    "GRADUATION_DATE_SOURCE_NEEDS_CONFIRMATION"
  ]
}
```

## 10. SQL/Proc đề xuất

### 10.1. Bảng cấu hình nên có

- `RPT_9H_ROW_DEF`: thứ tự Excel, STT, nhãn, cấp cha/con, `row_code`.
- `RPT_9H_ROW_RULE`: điều kiện dòng lá theo trình độ, hình thức, loại hình, khóa/lớp/địa bàn.
- `RPT_9H_PARENT_RULE`: cấu hình tổng dòng cha, thay cho công thức Excel chưa đầy đủ.
- `RPT_DOI_TUONG_NHAP_HOC_MAP`: mapping danh mục đối tượng nhập học vào các cột cán bộ/CSNV/HSPT/HSVH/BQP/ngành khác/nước ngoài.

### 10.2. SQL skeleton

```sql
WITH params AS (
    SELECT
        :ma_don_vi AS ma_don_vi,
        :co_so_dao_tao_id AS co_so_dao_tao_id,
        :khoa_hoc_id AS khoa_hoc_id,
        :tu_ngay_tot_nghiep AS tu_ngay_tot_nghiep,
        :den_ngay_tot_nghiep AS den_ngay_tot_nghiep,
        :nam_nhap_hoc AS nam_nhap_hoc
    FROM dual
),
base_hoc_vien AS (
    SELECT
        hv.id,
        hv.trinh_do_dao_tao_id,
        hv.hinh_thuc_dao_tao_id,
        hv.loai_hinh_dao_tao_id,
        hv.nganh_id,
        hv.chuyen_nganh_id,
        hv.khoa_hoc_id,
        hv.trung_doi_id,
        hv.ngay_nhap_hoc,
        hv.doi_tuong_nhap_hoc_id,
        hv.co_so_dao_tao_id,
        hv.ma_don_vi,
        hv.ngay_vao_dang AS hv_ngay_vao_dang,
        hv.ngay_chuyen_dang_chinh_thuc AS hv_ngay_vao_dang_chinh_thuc,
        cn.gioi_tinh,
        cn.dan_toc_id,
        cn.quoc_tich_id,
        cn.ngay_vao_dang AS cn_ngay_vao_dang,
        cn.ngay_vao_dang_chinh_thuc AS cn_ngay_vao_dang_chinh_thuc
    FROM X02_APP.HOC_VIEN hv
    LEFT JOIN X02_APP.CON_NGUOI cn
           ON cn.id = hv.con_nguoi_id
          AND cn.is_deleted = 0
    CROSS JOIN params p
    WHERE hv.is_deleted = 0
      AND hv.is_active = 1
      AND hv.workflow_status = 'Approved'
      AND (p.ma_don_vi IS NULL OR hv.ma_don_vi = p.ma_don_vi)
      AND (p.co_so_dao_tao_id IS NULL OR hv.co_so_dao_tao_id = p.co_so_dao_tao_id)
      AND (p.khoa_hoc_id IS NULL OR hv.khoa_hoc_id = p.khoa_hoc_id)
),
nhap_hoc AS (
    SELECT
        rr.row_code,
        COUNT(*) AS nhap_hoc
    FROM base_hoc_vien hv
    JOIN X02_APP.RPT_9H_ROW_RULE rr
      ON (rr.trinh_do_dao_tao_id IS NULL OR rr.trinh_do_dao_tao_id = hv.trinh_do_dao_tao_id)
     AND (rr.hinh_thuc_dao_tao_id IS NULL OR rr.hinh_thuc_dao_tao_id = hv.hinh_thuc_dao_tao_id)
     AND (rr.loai_hinh_dao_tao_id IS NULL OR rr.loai_hinh_dao_tao_id = hv.loai_hinh_dao_tao_id)
     AND (rr.khoa_hoc_id IS NULL OR rr.khoa_hoc_id = hv.khoa_hoc_id)
    CROSS JOIN params p
    WHERE p.nam_nhap_hoc IS NULL
       OR EXTRACT(YEAR FROM hv.ngay_nhap_hoc) = p.nam_nhap_hoc
    GROUP BY rr.row_code
),
tot_nghiep AS (
    SELECT
        rr.row_code,
        COUNT(DISTINCT hv.id) AS tot_nghiep,
        SUM(CASE WHEN dm.map_col = 'CAN_BO' THEN 1 ELSE 0 END) AS can_bo,
        SUM(CASE WHEN dm.map_col = 'CSNV' THEN 1 ELSE 0 END) AS csnv,
        SUM(CASE WHEN dm.map_col = 'HSPT' THEN 1 ELSE 0 END) AS hoc_sinh_pho_thong,
        SUM(CASE WHEN dm.map_col = 'HSVH' THEN 1 ELSE 0 END) AS hoc_sinh_van_hoa,
        SUM(CASE WHEN dm.map_col = 'BQP' THEN 1 ELSE 0 END) AS bqp,
        SUM(CASE WHEN dm.map_col = 'NGANH_KHAC' THEN 1 ELSE 0 END) AS nganh_khac,
        SUM(CASE WHEN hv.quoc_tich_id IS NOT NULL THEN 1 ELSE 0 END) AS nuoc_ngoai,
        SUM(CASE WHEN UPPER(NVL(hv.gioi_tinh, '')) IN ('NU', 'NỮ', 'FEMALE') THEN 1 ELSE 0 END) AS nu,
        SUM(CASE WHEN hv.dan_toc_id IS NOT NULL THEN 1 ELSE 0 END) AS dan_toc_thieu_so,
        SUM(CASE WHEN COALESCE(hv.hv_ngay_vao_dang_chinh_thuc, hv.hv_ngay_vao_dang, hv.cn_ngay_vao_dang_chinh_thuc, hv.cn_ngay_vao_dang) IS NOT NULL THEN 1 ELSE 0 END) AS dang_vien
    FROM base_hoc_vien hv
    JOIN X02_APP.HV_QUYET_DINH_TOT_NGHIEP tn
      ON tn.hoc_vien_id = hv.id
     AND tn.is_deleted = 0
     AND tn.is_active = 1
     AND tn.workflow_status = 'Approved'
    JOIN X02_APP.RPT_9H_ROW_RULE rr
      ON (rr.trinh_do_dao_tao_id IS NULL OR rr.trinh_do_dao_tao_id = hv.trinh_do_dao_tao_id)
     AND (rr.hinh_thuc_dao_tao_id IS NULL OR rr.hinh_thuc_dao_tao_id = hv.hinh_thuc_dao_tao_id)
     AND (rr.loai_hinh_dao_tao_id IS NULL OR rr.loai_hinh_dao_tao_id = hv.loai_hinh_dao_tao_id)
     AND (rr.khoa_hoc_id IS NULL OR rr.khoa_hoc_id = hv.khoa_hoc_id)
    LEFT JOIN X02_APP.RPT_DOI_TUONG_NHAP_HOC_MAP dm
           ON dm.doi_tuong_nhap_hoc_id = hv.doi_tuong_nhap_hoc_id
    CROSS JOIN params p
    WHERE (p.tu_ngay_tot_nghiep IS NULL OR tn.approved_at >= p.tu_ngay_tot_nghiep)
      AND (p.den_ngay_tot_nghiep IS NULL OR tn.approved_at < p.den_ngay_tot_nghiep + 1)
    GROUP BY rr.row_code
),
leaf AS (
    SELECT
        COALESCE(n.row_code, t.row_code) AS row_code,
        NVL(n.nhap_hoc, 0) AS nhap_hoc,
        NVL(t.tot_nghiep, 0) AS tot_nghiep,
        NVL(t.can_bo, 0) AS can_bo,
        NVL(t.csnv, 0) AS csnv,
        NVL(t.hoc_sinh_pho_thong, 0) AS hoc_sinh_pho_thong,
        NVL(t.hoc_sinh_van_hoa, 0) AS hoc_sinh_van_hoa,
        NVL(t.bqp, 0) AS bqp,
        NVL(t.nganh_khac, 0) AS nganh_khac,
        NVL(t.nuoc_ngoai, 0) AS nuoc_ngoai,
        NVL(t.nu, 0) AS nu,
        NVL(t.dan_toc_thieu_so, 0) AS dan_toc_thieu_so,
        NVL(t.dang_vien, 0) AS dang_vien
    FROM nhap_hoc n
    FULL OUTER JOIN tot_nghiep t
      ON t.row_code = n.row_code
)
SELECT
    rd.excel_row,
    rd.row_code,
    rd.stt,
    rd.label,
    NVL(l.nhap_hoc, 0) AS nhap_hoc,
    NVL(l.tot_nghiep, 0) AS tot_nghiep,
    NVL(l.can_bo, 0) AS can_bo,
    NVL(l.csnv, 0) AS csnv,
    NVL(l.hoc_sinh_pho_thong, 0) AS hoc_sinh_pho_thong,
    NVL(l.hoc_sinh_van_hoa, 0) AS hoc_sinh_van_hoa,
    NVL(l.bqp, 0) AS bqp,
    NVL(l.nganh_khac, 0) AS nganh_khac,
    NVL(l.nuoc_ngoai, 0) AS nuoc_ngoai,
    NVL(l.nu, 0) AS nu,
    NVL(l.dan_toc_thieu_so, 0) AS dan_toc_thieu_so,
    NVL(l.dang_vien, 0) AS dang_vien
FROM X02_APP.RPT_9H_ROW_DEF rd
LEFT JOIN leaf l
       ON l.row_code = rd.row_code
ORDER BY rd.excel_row;
```

`[Cần xác nhận]` SQL skeleton đang dùng `HV_QUYET_DINH_TOT_NGHIEP.APPROVED_AT` làm ngày tốt nghiệp do `X02_APP.sql` không có bảng quyết định vật lý kèm ngày quyết định. Nếu runtime có view/object `quyet_dinh_tot_nghiep.ngay_quyet_dinh` thì nên thay điều kiện ngày bằng field đó.

## 11. Quy tắc đối soát

| Nhóm kiểm tra | Quy tắc |
|---|---|
| Tổng | `Tổng` phải bằng tổng các dòng lá đã chốt, không dùng row 40 trống |
| Nhập học/tốt nghiệp | `totNghiep <= nhapHoc` theo cùng cohort, trừ trường hợp nhập học ngoài hệ thống lịch sử |
| Đối tượng | `canBo + csnv + hocSinhPhoThong + hocSinhVanHoa + bqp + nganhKhac + nuocNgoai <= totNghiep` nếu các nhóm loại trừ nhau |
| Thành phần | `nu <= totNghiep`, `danTocThieuSo <= totNghiep`, `dangVien <= totNghiep` |
| Quyết định | Chỉ đếm quyết định tốt nghiệp `Approved`, không xóa, còn hiệu lực |
| Quốc tịch | `nuocNgoai` cần danh mục quốc tịch Việt Nam để loại trừ chính xác |
| Dân tộc | `danTocThieuSo` cần danh mục dân tộc Kinh để loại trừ chính xác |

## 12. Gap và câu hỏi cần xác nhận

| Nhóm | Vấn đề | Câu hỏi |
|---|---|---|
| Kỳ báo cáo | Template ghi năm 2025 | Có đúng kỳ báo cáo 2025 không, hay cần đồng bộ 2026 như các mẫu H khác? |
| Nguồn ngày tốt nghiệp | `X02_APP.sql` chỉ có `HV_QUYET_DINH_TOT_NGHIEP`; metadata có `ngay_quyet_dinh` | Lấy ngày tốt nghiệp theo `APPROVED_AT`, ngày quyết định, hay `NGAY_TOT_NGHIEP` từ bảng/view khác? |
| Cột nhập học | Chưa có công thức tổng | Cột `Nhập học` lấy theo năm nhập học, khóa học, hay cohort tốt nghiệp? |
| STT dòng | Thiếu STT 5, nhảy từ 4 sang 6 | Có thiếu nhóm đào tạo trong template không? |
| Bồi dưỡng | Row 37 tham chiếu row 40 trống | Có thiếu dòng chi tiết bồi dưỡng không? |
| Đối tượng | Cột `Nước ngoài` nằm trong nhóm đối tượng nhập học | Xác định theo `QUOC_TICH_ID` hay theo `DOI_TUONG_NHAP_HOC_ID` quốc tế? |
| Đảng viên | Có `NGAY_VAO_DANG` ở cả `HOC_VIEN` và `CON_NGUOI` | Field nào là nguồn chuẩn khi hai nơi khác nhau? |

## 13. Tham chiếu

- `docs/report-input/9H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/LRN-dashboard.md`
- `src/backend/qldt-v2/src/main/resources/app.sql`
- `src/frontend/frontend-x02-v2/src/domains/lrn/services/lrnBusiness.service.js`
- `src/frontend/frontend-x02-v2/src/domains/lrn/pages/QuyetDinhTotNghiepPage.jsx`

# Báo cáo 4H - Thống kê kết quả công tác của đội ngũ giáo viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/4H.xlsx` |
| Sheet | `Cong tac GV` |
| Mã biểu mẫu | `Biễu mẫu 4H` |
| Tên báo cáo | `THỐNG KÊ KẾT QUẢ CÔNG TÁC CỦA ĐỘI NGŨ GIÁO VIÊN` |
| Vùng dữ liệu chính | `B6:L24` |
| Công thức Excel | Không có công thức |
| Dạng báo cáo | Tổng hợp chỉ tiêu theo 4 nhóm nghiệp vụ |

`[Cần xác nhận]` Template ghi `Biễu mẫu 4H`; có thể là lỗi chính tả của `Biểu mẫu 4H`. Khi xuất báo cáo nên dùng nguyên template nếu đây là mẫu chính thức.

## 2. Mục đích nghiệp vụ

Báo cáo tổng hợp kết quả công tác của đội ngũ giáo viên trong kỳ báo cáo, gồm:

- Giảng dạy.
- Thực hiện dạy giỏi.
- Xét danh hiệu giáo viên dạy giỏi.
- Đi thực tế, luân chuyển, duyệt giảng.

`[Suy luận]` Đây là báo cáo cấp đơn vị/trường theo kỳ hoặc năm học. Template không có ô filter nên hệ thống cần truyền `maDonVi`, `namHocId` hoặc `tuNgay/denNgay` từ API/giao diện.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `B2:L2` | `Biễu mẫu 4H` | Merged |
| `B3:D3` | `BỘ CÔNG AN` | Merged |
| `E3:L4` | Tên báo cáo | Merged |
| `B4:D4` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `E5:L5` | Dòng kèm theo báo cáo | Merged |

### 3.2. Nhóm 1 - Giảng dạy

| Ô/vùng | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---|---|---|
| `B6` | `1` | `sectionOrder` | Hằng số |
| `C6:L6` | `GIẢNG DẠY` | `sectionName` | Hằng số |
| `C9:D9` | Số giờ giảng - Theo kế hoạch | `giangDaySoGioTheoKeHoach` | `[Cần xác nhận]` từ kế hoạch giảng dạy |
| `E9` | Số giờ giảng - Theo định mức | `giangDaySoGioTheoDinhMuc` | `KET_QUA_GIANG_DAY.SO_GIO_NGHIA_VU` `[Suy luận]` |
| `F9` | Số giờ giảng - Đã giảng thực tế | `giangDaySoGioThucTe` | `KET_QUA_GIANG_DAY.SO_GIO_THUC_HIEN` |
| `G9` | Trong trường - Số lớp | `trongTruongSoLop` | `[Cần xác nhận]` chưa thấy cột trực tiếp |
| `H9` | Trong trường - Số giờ | `trongTruongSoGio` | `[Cần xác nhận]` chưa thấy phân loại địa bàn trong `KET_QUA_GIANG_DAY` |
| `I9` | Liên kết tại Công an các đơn vị, địa phương - Số lớp | `lienKetSoLop` | `[Cần xác nhận]` cần nguồn lớp liên kết/địa bàn |
| `J9` | Liên kết tại Công an các đơn vị, địa phương - Số giờ | `lienKetSoGio` | `[Cần xác nhận]` cần nguồn lớp liên kết/địa bàn |
| `K9` | Giờ thực hành, thực tập - Số lớp | `thucHanhThucTapSoLop` | `[Cần xác nhận]` |
| `L9` | Giờ thực hành, thực tập - Số giờ | `thucHanhThucTapSoGio` | `[Cần xác nhận]` |

### 3.3. Nhóm 2 - Thực hiện dạy giỏi

| Ô | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---|---|---|
| `C14` | Bài dạy giỏi cấp trường đánh giá - Số đăng ký - Nam | `dayGioiTruongDangKyNam` | `KET_QUA_THUC_HIEN_DAY_GIOI`, `CAP_HOI_THI_DAY_GIOI_ID = 2`, giới tính nam `[Suy luận]` |
| `D14` | Bài dạy giỏi cấp trường đánh giá - Số đăng ký - Nữ | `dayGioiTruongDangKyNu` | Tương tự |
| `E14` | Bài dạy giỏi cấp trường đánh giá - Số đạt - Nam | `dayGioiTruongDatNam` | `QUYET_DINH_CONG_NHAN_ID IS NOT NULL` hoặc `TRANG_THAI` đạt `[Cần xác nhận]` |
| `F14` | Bài dạy giỏi cấp trường đánh giá - Số đạt - Nữ | `dayGioiTruongDatNu` | Tương tự |
| `G14` | Bài dạy giỏi cấp khoa đánh giá - Số đăng ký - Nam | `dayGioiKhoaDangKyNam` | `CAP_HOI_THI_DAY_GIOI_ID = 1` |
| `H14` | Bài dạy giỏi cấp khoa đánh giá - Số đăng ký - Nữ | `dayGioiKhoaDangKyNu` | Tương tự |
| `I14` | Bài dạy giỏi cấp khoa đánh giá - Số đạt - Nam | `dayGioiKhoaDatNam` | `QUYET_DINH_CONG_NHAN_ID IS NOT NULL` hoặc `TRANG_THAI` đạt `[Cần xác nhận]` |
| `J14` | Bài dạy giỏi cấp khoa đánh giá - Số đạt - Nữ | `dayGioiKhoaDatNu` | Tương tự |
| `K14` | Giờ dạy giỏi - Nam | `gioDayGioiNam` | Sum `KET_QUA_THUC_HIEN_DAY_GIOI.GIO_DAY_GIOI` theo nam `[Cần chuẩn hóa số]` |
| `L14` | Giờ dạy giỏi - Nữ | `gioDayGioiNu` | Sum `GIO_DAY_GIOI` theo nữ |

`[Cần xác nhận]` Bảng `KET_QUA_THUC_HIEN_DAY_GIOI` đang là nguồn kết quả thực hiện, chưa tách rõ bản ghi đăng ký và bản ghi đạt. Nếu nghiệp vụ có màn/bảng đăng ký riêng, cần ưu tiên bảng đăng ký đó cho cột `Số đăng ký`.

### 3.4. Nhóm 3 - Xét danh hiệu giáo viên dạy giỏi

| Ô | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---|---|---|
| `C19` | Cấp Bộ - Số đăng ký - Nam | `danhHieuBoDangKyNam` | `[Cần xác nhận]` chưa thấy bảng đăng ký hiện hành |
| `D19` | Cấp Bộ - Số đăng ký - Nữ | `danhHieuBoDangKyNu` | `[Cần xác nhận]` |
| `E19` | Cấp Bộ - Số đạt - Nam | `danhHieuBoDatNam` | `DANH_HIEU_GIAO_VIEN_DAY_GIOI.CAP_DANH_HIEU_DAY_GIOI_ID = 2` |
| `F19` | Cấp Bộ - Số đạt - Nữ | `danhHieuBoDatNu` | Tương tự |
| `G19` | Cấp trường - Số đăng ký - Nam | `danhHieuTruongDangKyNam` | `[Cần xác nhận]` |
| `H19` | Cấp trường - Số đăng ký - Nữ | `danhHieuTruongDangKyNu` | `[Cần xác nhận]` |
| `I19` | Cấp trường - Số đạt - Nam | `danhHieuTruongDatNam` | `CAP_DANH_HIEU_DAY_GIOI_ID = 1` |
| `J19` | Cấp trường - Số đạt - Nữ | `danhHieuTruongDatNu` | Tương tự |
| `K19` | Cấp tỉnh - Số đăng ký/Nam `[Cần xác nhận header]` | `danhHieuTinhDangKyNam` | Chưa thấy `CAP_DANH_HIEU_DAY_GIOI_ID` cho cấp tỉnh |
| `L19` | Cấp tỉnh - Số đạt/Nữ `[Cần xác nhận header]` | `danhHieuTinhDatNu` | Chưa thấy `CAP_DANH_HIEU_DAY_GIOI_ID` cho cấp tỉnh |

`[Cần xác nhận]` Header phần `Cấp tỉnh` không cân xứng với hai nhóm trước: `K17='Số đăng ký'`, `L17='Số đạt'`, nhưng `K18='Nam'`, `L18='Nữ'`. Ngoài ra DDL hiện ghi `CAP_DANH_HIEU_DAY_GIOI_ID`: `1-Cấp trường`, `2-Cấp Bộ`, chưa có cấp tỉnh.

### 3.5. Nhóm 4 - Đi thực tế, luân chuyển, duyệt giảng

| Ô | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---|---|---|---|
| `C24` | Số lượt giáo viên đi thực tế - Số đăng ký - Nam | `thucTeDangKyNam` | `LUAN_CHUYEN_THUC_TE.LOAI_QUA_TRINH = 2`, giới tính nam |
| `D24` | Số lượt giáo viên đi thực tế - Số đăng ký - Nữ | `thucTeDangKyNu` | Tương tự |
| `E24` | Số lượt giáo viên đi thực tế - Kết quả - Nam | `thucTeKetQuaNam` | `QUYET_DINH_HOAN_THANH_ID IS NOT NULL` hoặc có báo cáo kết quả `[Cần xác nhận]` |
| `F24` | Số lượt giáo viên đi thực tế - Kết quả - Nữ | `thucTeKetQuaNu` | Tương tự |
| `G24` | Số giáo viên giảng dạy nghiệp vụ đi luân chuyển - Số đăng ký - Nam | `luanChuyenDangKyNam` | `LUAN_CHUYEN_THUC_TE.LOAI_QUA_TRINH = 1` |
| `H24` | Số giáo viên giảng dạy nghiệp vụ đi luân chuyển - Số đăng ký - Nữ | `luanChuyenDangKyNu` | Tương tự |
| `I24` | Số giáo viên giảng dạy nghiệp vụ đi luân chuyển - Kết quả - Nam | `luanChuyenKetQuaNam` | `QUYET_DINH_HOAN_THANH_ID IS NOT NULL` hoặc có báo cáo kết quả `[Cần xác nhận]` |
| `J24` | Số giáo viên giảng dạy nghiệp vụ đi luân chuyển - Kết quả - Nữ | `luanChuyenKetQuaNu` | Tương tự |
| `K24` | Số giáo viên duyệt giảng - Nam | `duyetGiangNam` | Count `DUYET_GIANG` theo giới tính nam |
| `L24` | Số giáo viên duyệt giảng - Nữ | `duyetGiangNu` | Count `DUYET_GIANG` theo giới tính nữ |

## 4. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột quan trọng |
|---|---|---|
| `X02_APP.KET_QUA_GIANG_DAY` / `/api/v1/ket-qua-giang-day` | Kết quả giờ giảng | `CAN_BO_ID`, `SO_GIO_NGHIA_VU`, `SO_GIO_THUC_HIEN`, `NAM_HOC_ID`, `MA_DON_VI` |
| `X02_APP.CHI_TIET_KE_HOACH_GIANG_DAY` | Kế hoạch giảng dạy chi tiết `[Suy luận]` | `GIAO_VIEN_GIANG_DAY_ID`, `TU_NGAY`, `DEN_NGAY`, `MA_DON_VI` |
| `X02_APP.KET_QUA_THUC_HIEN_DAY_GIOI` / `/api/v1/thuc-hien-day-gioi` | Bài dạy giỏi, giờ dạy giỏi | `CAN_BO_GIANG_DAY_ID`, `NAM_HOC_ID`, `HINH_THUC_THUC_HIEN`, `CAP_HOI_THI_DAY_GIOI_ID`, `GIO_DAY_GIOI`, `QUYET_DINH_CONG_NHAN_ID` |
| `X02_APP.DANH_HIEU_GIAO_VIEN_DAY_GIOI` / `/api/v1/danh-hieu-giao-vien-day-gioi` | Danh hiệu giáo viên dạy giỏi | `CAN_BO_GIANG_VIEN_ID`, `NAM_HOC_NHAN_DANH_HIEU`, `CAP_DANH_HIEU_DAY_GIOI_ID` |
| `X02_APP.LUAN_CHUYEN_THUC_TE` / `/api/v1/ket-qua-luan-chuyen-co-thoi-han` | Đi thực tế và luân chuyển | `CAN_BO_GIANG_VIEN_ID`, `LOAI_QUA_TRINH`, `THOI_GIAN_BAT_DAU`, `THOI_GIAN_KET_THUC`, `QUYET_DINH_HOAN_THANH_ID` |
| `X02_APP.DUYET_GIANG` / `/api/v1/duyet-giang` | Duyệt giảng | `CAN_BO_GIANG_VIEN_ID`, `NGAY_DUYET_GIANG`, `DON_VI_CONG_TAC_ID` |
| `X02_APP.CAN_BO_NHA_GIAO`, `X02_APP.CON_NGUOI` | Join giới tính, lọc giáo viên | `CON_NGUOI_ID`, `PHAN_LOAI`, `GIOI_TINH` |
| `X02_DM.DM_GIOI_TINH` | Mapping Nam/Nữ | `[Cần mapping danh mục]` |

## 5. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | Áp dụng trên `MA_DON_VI`; mặc định theo đơn vị user |
| `namHocId` | String | Áp dụng trực tiếp cho `KET_QUA_GIANG_DAY.NAM_HOC_ID`, `KET_QUA_THUC_HIEN_DAY_GIOI.NAM_HOC_ID`; với danh hiệu dùng `NAM_HOC_NHAN_DANH_HIEU` |
| `tuNgay` | Date | Dùng cho các bảng theo ngày: `THOI_GIAN_BAT_DAU`, `NGAY_DUYET_GIANG`, hoặc khoảng kế hoạch |
| `denNgay` | Date | Ngày kết thúc kỳ |
| `workflowStatus` | String | Mặc định `Approved` |

`[Cần xác nhận]` Nếu `namHocId` là filter chính, các bảng chỉ có ngày cần quy đổi năm học sang khoảng ngày. Nếu `tuNgay/denNgay` là filter chính, các bảng theo năm học cần join `DM_NAM_HOC` để lấy khoảng thời gian.

## 6. API report đề xuất

```http
GET /api/v1/reports/4h/ket-qua-cong-tac-doi-ngu-giao-vien
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Không | Ưu tiên khi báo cáo theo năm học |
| `tuNgay` | Không | Bắt buộc nếu không truyền `namHocId` |
| `denNgay` | Không | Bắt buộc nếu không truyền `namHocId` |

Response đề xuất:

```json
{
  "reportCode": "4H",
  "title": "Thống kê kết quả công tác của đội ngũ giáo viên",
  "filters": {
    "maDonVi": "T01",
    "namHocId": "2025-2026"
  },
  "giangDay": {
    "soGioTheoKeHoach": 0,
    "soGioTheoDinhMuc": 0,
    "soGioThucTe": 0,
    "trongTruongSoLop": 0,
    "trongTruongSoGio": 0,
    "lienKetSoLop": 0,
    "lienKetSoGio": 0,
    "thucHanhThucTapSoLop": 0,
    "thucHanhThucTapSoGio": 0
  },
  "thucHienDayGioi": {
    "truongDangKyNam": 0,
    "truongDangKyNu": 0,
    "truongDatNam": 0,
    "truongDatNu": 0,
    "khoaDangKyNam": 0,
    "khoaDangKyNu": 0,
    "khoaDatNam": 0,
    "khoaDatNu": 0,
    "gioDayGioiNam": 0,
    "gioDayGioiNu": 0
  },
  "xetDanhHieuDayGioi": {},
  "thucTeLuanChuyenDuyetGiang": {}
}
```

Frontend report registry hiện chưa thấy slug riêng cho mẫu 4H. Các màn nghiệp vụ nguồn đã có route/API riêng ở phân hệ `STF`.

## 7. SQL Proc Oracle đề xuất

Skeleton dưới đây ưu tiên các cột chắc chắn; các field chưa có nguồn rõ trả `0` và đánh dấu trong gap.

```sql
CREATE OR REPLACE PROCEDURE X02_BCTK.PROC_RPT_4H_KQ_CONG_TAC_GV (
    P_MA_DON_VI IN VARCHAR2 DEFAULT NULL,
    P_NAM_HOC_ID IN VARCHAR2 DEFAULT NULL,
    P_TU_NGAY IN DATE DEFAULT NULL,
    P_DEN_NGAY IN DATE DEFAULT NULL,
    O_RESULT OUT SYS_REFCURSOR
) AS
BEGIN
    OPEN O_RESULT FOR
        WITH staff AS (
            SELECT
                cb.ID AS can_bo_id,
                cb.MA_DON_VI,
                CASE
                    WHEN UPPER(NVL(gt.TEN, '')) LIKE '%NỮ%' OR UPPER(NVL(gt.TEN, '')) LIKE '%NU%' THEN 'NU'
                    WHEN UPPER(NVL(gt.TEN, '')) LIKE '%NAM%' THEN 'NAM'
                    ELSE 'KHAC'
                END AS gender_code
            FROM X02_APP.CAN_BO_NHA_GIAO cb
            LEFT JOIN X02_APP.CON_NGUOI cn ON cn.ID = cb.CON_NGUOI_ID
            LEFT JOIN X02_DM.DM_GIOI_TINH gt ON gt.ID = cn.GIOI_TINH
            WHERE NVL(cb.IS_DELETED, 0) = 0
              AND NVL(cb.IS_ACTIVE, 1) = 1
              AND cb.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR cb.MA_DON_VI = P_MA_DON_VI)
        ),
        giang_day AS (
            SELECT
                SUM(NVL(kgd.SO_GIO_NGHIA_VU, 0)) AS so_gio_dinh_muc,
                SUM(NVL(kgd.SO_GIO_THUC_HIEN, 0)) AS so_gio_thuc_te
            FROM X02_APP.KET_QUA_GIANG_DAY kgd
            WHERE NVL(kgd.IS_DELETED, 0) = 0
              AND NVL(kgd.IS_ACTIVE, 1) = 1
              AND kgd.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR kgd.MA_DON_VI = P_MA_DON_VI)
              AND (P_NAM_HOC_ID IS NULL OR kgd.NAM_HOC_ID = P_NAM_HOC_ID)
        ),
        thuc_hien_day_gioi AS (
            SELECT
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '2' AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS truong_dang_ky_nam,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '2' AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS truong_dang_ky_nu,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '2' AND s.gender_code = 'NAM' AND dg.QUYET_DINH_CONG_NHAN_ID IS NOT NULL THEN 1 ELSE 0 END) AS truong_dat_nam,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '2' AND s.gender_code = 'NU' AND dg.QUYET_DINH_CONG_NHAN_ID IS NOT NULL THEN 1 ELSE 0 END) AS truong_dat_nu,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '1' AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS khoa_dang_ky_nam,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '1' AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS khoa_dang_ky_nu,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '1' AND s.gender_code = 'NAM' AND dg.QUYET_DINH_CONG_NHAN_ID IS NOT NULL THEN 1 ELSE 0 END) AS khoa_dat_nam,
                SUM(CASE WHEN dg.CAP_HOI_THI_DAY_GIOI_ID = '1' AND s.gender_code = 'NU' AND dg.QUYET_DINH_CONG_NHAN_ID IS NOT NULL THEN 1 ELSE 0 END) AS khoa_dat_nu,
                SUM(CASE WHEN s.gender_code = 'NAM' THEN TO_NUMBER(dg.GIO_DAY_GIOI DEFAULT NULL ON CONVERSION ERROR) ELSE 0 END) AS gio_day_gioi_nam,
                SUM(CASE WHEN s.gender_code = 'NU' THEN TO_NUMBER(dg.GIO_DAY_GIOI DEFAULT NULL ON CONVERSION ERROR) ELSE 0 END) AS gio_day_gioi_nu
            FROM X02_APP.KET_QUA_THUC_HIEN_DAY_GIOI dg
            JOIN staff s ON s.can_bo_id = dg.CAN_BO_GIANG_DAY_ID
            WHERE NVL(dg.IS_DELETED, 0) = 0
              AND NVL(dg.IS_ACTIVE, 1) = 1
              AND dg.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR dg.MA_DON_VI = P_MA_DON_VI)
              AND (P_NAM_HOC_ID IS NULL OR dg.NAM_HOC_ID = P_NAM_HOC_ID)
        ),
        danh_hieu AS (
            SELECT
                SUM(CASE WHEN dh.CAP_DANH_HIEU_DAY_GIOI_ID = 2 AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS bo_dat_nam,
                SUM(CASE WHEN dh.CAP_DANH_HIEU_DAY_GIOI_ID = 2 AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS bo_dat_nu,
                SUM(CASE WHEN dh.CAP_DANH_HIEU_DAY_GIOI_ID = 1 AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS truong_dat_nam,
                SUM(CASE WHEN dh.CAP_DANH_HIEU_DAY_GIOI_ID = 1 AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS truong_dat_nu
            FROM X02_APP.DANH_HIEU_GIAO_VIEN_DAY_GIOI dh
            JOIN staff s ON s.can_bo_id = dh.CAN_BO_GIANG_VIEN_ID
            WHERE NVL(dh.IS_DELETED, 0) = 0
              AND NVL(dh.IS_ACTIVE, 1) = 1
              AND dh.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR dh.MA_DON_VI = P_MA_DON_VI)
              AND (P_NAM_HOC_ID IS NULL OR dh.NAM_HOC_NHAN_DANH_HIEU = P_NAM_HOC_ID)
        ),
        thuc_te_luan_chuyen AS (
            SELECT
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 2 AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS thuc_te_dang_ky_nam,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 2 AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS thuc_te_dang_ky_nu,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 2 AND s.gender_code = 'NAM' AND lc.QUYET_DINH_HOAN_THANH_ID IS NOT NULL THEN 1 ELSE 0 END) AS thuc_te_ket_qua_nam,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 2 AND s.gender_code = 'NU' AND lc.QUYET_DINH_HOAN_THANH_ID IS NOT NULL THEN 1 ELSE 0 END) AS thuc_te_ket_qua_nu,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 1 AND s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS luan_chuyen_dang_ky_nam,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 1 AND s.gender_code = 'NU' THEN 1 ELSE 0 END) AS luan_chuyen_dang_ky_nu,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 1 AND s.gender_code = 'NAM' AND lc.QUYET_DINH_HOAN_THANH_ID IS NOT NULL THEN 1 ELSE 0 END) AS luan_chuyen_ket_qua_nam,
                SUM(CASE WHEN lc.LOAI_QUA_TRINH = 1 AND s.gender_code = 'NU' AND lc.QUYET_DINH_HOAN_THANH_ID IS NOT NULL THEN 1 ELSE 0 END) AS luan_chuyen_ket_qua_nu
            FROM X02_APP.LUAN_CHUYEN_THUC_TE lc
            JOIN staff s ON s.can_bo_id = lc.CAN_BO_GIANG_VIEN_ID
            WHERE NVL(lc.IS_DELETED, 0) = 0
              AND NVL(lc.IS_ACTIVE, 1) = 1
              AND lc.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR lc.MA_DON_VI = P_MA_DON_VI)
              AND (P_TU_NGAY IS NULL OR lc.THOI_GIAN_BAT_DAU >= P_TU_NGAY)
              AND (P_DEN_NGAY IS NULL OR lc.THOI_GIAN_BAT_DAU <= P_DEN_NGAY)
        ),
        duyet_giang AS (
            SELECT
                SUM(CASE WHEN s.gender_code = 'NAM' THEN 1 ELSE 0 END) AS duyet_giang_nam,
                SUM(CASE WHEN s.gender_code = 'NU' THEN 1 ELSE 0 END) AS duyet_giang_nu
            FROM X02_APP.DUYET_GIANG dg
            JOIN staff s ON s.can_bo_id = dg.CAN_BO_GIANG_VIEN_ID
            WHERE NVL(dg.IS_DELETED, 0) = 0
              AND NVL(dg.IS_ACTIVE, 1) = 1
              AND dg.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR dg.MA_DON_VI = P_MA_DON_VI)
              AND (P_TU_NGAY IS NULL OR dg.NGAY_DUYET_GIANG >= P_TU_NGAY)
              AND (P_DEN_NGAY IS NULL OR dg.NGAY_DUYET_GIANG <= P_DEN_NGAY)
        )
        SELECT
            0 AS giang_day_so_gio_theo_ke_hoach,
            NVL(gd.so_gio_dinh_muc, 0) AS giang_day_so_gio_theo_dinh_muc,
            NVL(gd.so_gio_thuc_te, 0) AS giang_day_so_gio_thuc_te,
            0 AS trong_truong_so_lop,
            0 AS trong_truong_so_gio,
            0 AS lien_ket_so_lop,
            0 AS lien_ket_so_gio,
            0 AS thuc_hanh_thuc_tap_so_lop,
            0 AS thuc_hanh_thuc_tap_so_gio,
            thdg.*,
            0 AS danh_hieu_bo_dang_ky_nam,
            0 AS danh_hieu_bo_dang_ky_nu,
            NVL(dh.bo_dat_nam, 0) AS danh_hieu_bo_dat_nam,
            NVL(dh.bo_dat_nu, 0) AS danh_hieu_bo_dat_nu,
            0 AS danh_hieu_truong_dang_ky_nam,
            0 AS danh_hieu_truong_dang_ky_nu,
            NVL(dh.truong_dat_nam, 0) AS danh_hieu_truong_dat_nam,
            NVL(dh.truong_dat_nu, 0) AS danh_hieu_truong_dat_nu,
            0 AS danh_hieu_tinh_dang_ky_nam,
            0 AS danh_hieu_tinh_dat_nu,
            ttlc.*,
            dg.duyet_giang_nam,
            dg.duyet_giang_nu
        FROM giang_day gd
        CROSS JOIN thuc_hien_day_gioi thdg
        CROSS JOIN danh_hieu dh
        CROSS JOIN thuc_te_luan_chuyen ttlc
        CROSS JOIN duyet_giang dg;
END;
/
```

## 8. Quy tắc đối soát

| STT | Quy tắc | Cách kiểm |
|---:|---|---|
| 1 | Tất cả nguồn chỉ lấy bản ghi đã duyệt | `WORKFLOW_STATUS = 'Approved'`, `IS_DELETED = 0`, `IS_ACTIVE = 1` |
| 2 | Giới tính Nam/Nữ phải mapping được | Không để bản ghi giới tính khác/rỗng bị tự đẩy vào Nam nếu chưa chốt |
| 3 | Số đạt không vượt số đăng ký | Với từng nhóm: `datNam <= dangKyNam`, `datNu <= dangKyNu` |
| 4 | Đi thực tế và luân chuyển tách bằng `LOAI_QUA_TRINH` | `1 = Luân chuyển`, `2 = Thực tế` theo DDL |
| 5 | Giờ dạy giỏi phải parse được số | `GIO_DAY_GIOI` hiện là `VARCHAR2(500)`, cần chuẩn hóa hoặc validate |
| 6 | Danh hiệu cấp tỉnh | Không sinh số liệu nếu chưa có mã cấp tỉnh chính thức |

## 9. Gaps và câu hỏi cần xác nhận

| STT | Vấn đề | Ảnh hưởng | Đề xuất |
|---:|---|---|---|
| 1 | Nhóm giảng dạy cần `theo kế hoạch`, `số lớp`, `trong trường/liên kết/thực hành`, nhưng `KET_QUA_GIANG_DAY` chỉ có `SO_GIO_NGHIA_VU`, `SO_GIO_THUC_HIEN` | Nhiều ô nhóm 1 chưa tự động hóa chính xác | Chốt nguồn kế hoạch/lớp/địa bàn hoặc bổ sung bảng tổng hợp |
| 2 | `Số đăng ký` của dạy giỏi/danh hiệu chưa có nguồn tách riêng chắc chắn | Có thể đếm nhầm bản ghi kết quả thành đăng ký | Xác nhận có bảng đăng ký hiện hành hay dùng tất cả bản ghi `KET_QUA_THUC_HIEN_DAY_GIOI` |
| 3 | `GIO_DAY_GIOI` là chuỗi | Khó sum số giờ ổn định | Chuẩn hóa thành `NUMBER` hoặc tạo cột quy đổi |
| 4 | Danh hiệu dạy giỏi cấp tỉnh có trong Excel nhưng DDL chỉ có cấp trường/cấp Bộ | Không thể map `K19:L19` chính xác | Bổ sung mã cấp tỉnh hoặc xác nhận bỏ/đổi nhãn |
| 5 | Header cấp tỉnh `K17:L18` không cân xứng | Khó xác định ô `K19`, `L19` là đăng ký/đạt hay nam/nữ | Xác nhận mẫu chuẩn |
| 6 | Giới tính cần mapping danh mục | Sai lệch số Nam/Nữ nếu `CON_NGUOI.GIOI_TINH` lưu ID/mã khác dự kiến | Chốt `DM_GIOI_TINH` và dùng join danh mục |
| 7 | Chưa thấy frontend report registry cho 4H | Cần thêm màn report hoặc export riêng | Thêm slug/API report sau khi chốt mapping |

## 10. Nguồn tham chiếu trong repo

| Nguồn | Ý nghĩa |
|---|---|
| `docs/report-input/4H.xlsx` | Template Excel gốc |
| `docs/database/X02_APP.sql` | Schema dump hiện tại |
| `src/backend/qldt-v2/database/oracle/business/39_ket_qua_giang_day_create.sql` | DDL kết quả giảng dạy |
| `src/backend/qldt-v2/database/oracle/business/30_ket_qua_thuc_hien_day_gioi_create.sql` | DDL thực hiện dạy giỏi |
| `src/backend/qldt-v2/database/oracle/business/37_danh_hieu_giao_vien_day_gioi_create.sql` | DDL danh hiệu giáo viên dạy giỏi |
| `src/backend/qldt-v2/database/oracle/business/38_luan_chuyen_thuc_te_create.sql` | DDL luân chuyển/thực tế |
| `src/backend/qldt-v2/database/oracle/business/32_duyet_giang_create.sql` | DDL duyệt giảng |
| `src/frontend/frontend-x02-v2/src/shared/config/screenApiCatalog.csv` | API/route nghiệp vụ STF |
| `docs/figma/business-screens-fields/DT-kqgd.md` | Field màn kết quả giảng dạy |
| `docs/figma/business-screens-fields/DT-ttcbgvdt.md` | Field màn công tác thực tế |
| `docs/figma/business-screens-fields/DT-ttcbgvlc.md` | Field màn luân chuyển |
| `docs/figma/business-screens-fields/DT-ttdg-giang.md` | Field màn duyệt giảng |

## 11. Checklist triển khai

| Hạng mục | Trạng thái |
|---|---|
| Đọc template `4H.xlsx` | Đã xong |
| Mapping layout Excel | Đã xong |
| Mapping nguồn DB rõ | Một phần |
| Mapping nhóm giảng dạy | `[Cần xác nhận]` nhiều chỉ tiêu |
| Mapping dạy giỏi | Tương đối rõ, cần chốt đăng ký/đạt |
| Mapping danh hiệu dạy giỏi | Cần chốt cấp tỉnh và đăng ký |
| Mapping thực tế/luân chuyển/duyệt giảng | Tương đối rõ |
| SQL Proc đề xuất | Đã có skeleton |
| API đề xuất | Đã có |

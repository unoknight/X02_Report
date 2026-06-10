# Báo cáo 3H - Thống kê khen thưởng, kỷ luật cán bộ, giáo viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/3H.xlsx` |
| Sheet | `KT-KL GV` |
| Mã biểu mẫu | `Biểu mẫu 3H` |
| Tên báo cáo | `THỐNG KÊ KHEN THƯỞNG, KỶ LUẬT CÁN BỘ, GIÁO VIÊN` |
| Vùng dữ liệu chính | `A6:P12` |
| Dòng header | `6:7` |
| Dòng dữ liệu | `8:11` |
| Dòng tổng | `12` |

## 2. Mục đích nghiệp vụ

Báo cáo tổng hợp số lượng khen thưởng và kỷ luật của cán bộ, giáo viên theo nhóm đối tượng:

- Giáo viên.
- Cán bộ quản lý giáo dục.
- Cán bộ khác.
- Tập thể.

`[Suy luận]` Báo cáo dùng cho kỳ báo cáo tháng 5/năm hoặc giai đoạn tổng hợp do tham số ngày báo cáo quy định. Template không có ô filter năm/kỳ riêng, nên hệ thống cần truyền filter ngoài giao diện/API.

## 3. Layout Excel

### 3.1. Header

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:P1` | `Biểu mẫu 3H` | Merged |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `D2:P2` | Tên báo cáo | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `D3:P3` | Dòng kèm theo báo cáo | Merged |
| `A6:A7` | `TT` | Merged |
| `B6:B7` | `Đối tượng` | Merged |
| `D6:G6` | `Khen thưởng` | Merged trong template, nhưng thực tế nhóm khen thưởng gồm `C:G`. `[Cần xác nhận]` |
| `H6:O6` | `Kỷ luật` | Merged |
| `P6:P7` | `Ghi chú` | Merged |

### 3.2. Cột dữ liệu

| Cột Excel | Nhãn | Nhóm | Field đề xuất |
|---|---|---|---|
| A | TT | Định danh dòng | `sort_order` |
| B | Đối tượng | Định danh dòng | `doi_tuong` |
| C | Cờ thi đua | Khen thưởng | `coThiDua` |
| D | Huân chương các loại | Khen thưởng | `huanChuong` |
| E | Huy chương các loại | Khen thưởng | `huyChuong` |
| F | Bằng khen | Khen thưởng | `bangKhen` |
| G | Giấy khen | Khen thưởng | `giayKhen` |
| H | Tước danh hiệu CAND | Kỷ luật | `tuocDanhHieuCand` |
| I | Cách chức và giáng cấp bậc hàm | Kỷ luật | `cachChucGiangCapBacHam` |
| J | Cách chức và hạ bậc lương | Kỷ luật | `cachChucHaBacLuong` |
| K | Giáng chức và giáng cấp bậc hàm | Kỷ luật | `giangChucGiangCapBacHam` |
| L | Giáng cấp bậc hàm và hạ bậc lương hoặc hạ nhiều bậc lương | Kỷ luật | `giangCapBacHamHaBacLuong` |
| M | Hạ bậc lương hoặc giáng cấp bậc hàm | Kỷ luật | `haBacLuongGiangCapBacHam` |
| N | Cảnh cáo | Kỷ luật | `canhCao` |
| O | Khiển trách | Kỷ luật | `khienTrach` |
| P | Ghi chú | Ghi chú | `ghiChu` |

### 3.3. Dòng dữ liệu

| Dòng Excel | Đối tượng | `row_code` đề xuất |
|---:|---|---|
| 8 | Giáo viên | `GIAO_VIEN` |
| 9 | Cán bộ quản lý giáo dục | `CAN_BO_QLGD` |
| 10 | Cán bộ khác | `CAN_BO_KHAC` |
| 11 | Tập thể | `TAP_THE` |
| 12 | Tổng | `TOTAL` |

## 4. Công thức trong template

Template hiện chỉ có công thức tổng cho nhóm khen thưởng:

| Ô | Công thức |
|---|---|
| `C12` | `=SUM(C8:C11)` |
| `D12` | `=SUM(D8:D11)` |
| `E12` | `=SUM(E8:E11)` |
| `F12` | `=SUM(F8:F11)` |
| `G12` | `=SUM(G8:G11)` |

`[Cần xác nhận]` Các ô `H12:O12` thuộc nhóm kỷ luật không có công thức trong file mẫu, dù về nghiệp vụ nên là `SUM(H8:H11)` đến `SUM(O8:O11)`. Khi export báo cáo nên bổ sung công thức hoặc tính sẵn server-side để tránh tổng kỷ luật bằng rỗng.

## 5. Nguồn dữ liệu hệ thống

### 5.1. Bảng nghiệp vụ chính

| Bảng | Vai trò | Cột liên quan |
|---|---|---|
| `X02_APP.KHEN_THUONG_CAN_BO` | Sự kiện khen thưởng cán bộ/giáo viên | `ID`, `MA_DON_VI`, `CAN_BO_GIANG_VIEN_ID`, `LOAI_HINH_KHEN_THUONG_ID`, `CAP_KHEN_THUONG`, `TEN_KHEN_THUONG`, `NOI_DUNG_KHEN_THUONG`, `THOI_GIAN_KHEN_THUONG`, `WORKFLOW_STATUS`, `IS_DELETED`, `IS_ACTIVE` |
| `X02_APP.KY_LUAT_CAN_BO` | Sự kiện kỷ luật cán bộ/giáo viên | `ID`, `MA_DON_VI`, `DOI_TUONG_KY_LUAT_ID`, `HINH_THUC_KY_LUAT`, `TU_NGAY`, `DEN_NGAY`, `WORKFLOW_STATUS`, `IS_DELETED`, `IS_ACTIVE` |
| `X02_APP.CAN_BO_NHA_GIAO` | Hồ sơ cán bộ/nhà giáo để phân loại đối tượng | `ID`, `PHAN_LOAI`, `MA_DON_VI`, `WORKFLOW_STATUS`, `IS_DELETED`, `IS_ACTIVE` |
| `X02_APP.QUA_TRINH_GIANG_DAY_CONG_TAC` | Nguồn phụ để nhận diện cán bộ quản lý giáo dục qua chức danh/chức vụ mới nhất | `CAN_BO_NHA_GIAO_ID`, `CHUC_DANH_ID`, `CHUC_VU_ID`, `THOI_GIAN_AP_DUNG` |

### 5.2. Danh mục

| Danh mục | Vai trò |
|---|---|
| `X02_DM.DM_HINH_THUC_KHEN_THUONG` | Mapping loại khen thưởng: cờ thi đua, huân chương, huy chương, bằng khen, giấy khen |
| `X02_DM.DM_HINH_THUC_KY_LUAT` | Mapping hình thức kỷ luật nếu schema dùng danh mục |
| `X02_DM.DM_CHUC_DANH`, `X02_DM.DM_CHUC_VU` | Nhận diện cán bộ quản lý giáo dục `[Suy luận]` |

`[Suy luận]` Ưu tiên schema dump `docs/database/X02_APP.sql` và entity Java hiện tại: `LOAI_HINH_KHEN_THUONG_ID`, `CAP_KHEN_THUONG`, `HINH_THUC_KY_LUAT` là chuỗi `VARCHAR2(40)`/`String`. Một số file DDL business cũ khai báo `NUMBER(10)` và check `IN (1..5)`, cần xem là nguồn tham khảo lịch sử hoặc cần đồng bộ lại.

## 6. Mapping cột báo cáo

### 6.1. Khen thưởng

| Field | Cột Excel | Mapping đề xuất | Căn cứ |
|---|---|---|---|
| `coThiDua` | C | `DM_HINH_THUC_KHEN_THUONG.MA = 'KT10'` hoặc `TEN LIKE '%Cờ thi đua%'` | Có danh mục `KT10 - Cờ thi đua` |
| `huanChuong` | D | `TEN LIKE '%Huân chương%'` | Danh mục có `KT03 - Huân chương` và nhiều loại huân chương |
| `huyChuong` | E | `TEN LIKE '%Huy chương%'` | Danh mục có `KT04 - Huy chương` |
| `bangKhen` | F | `TEN LIKE '%Bằng khen%'` | Danh mục có `KT02 - Bằng khen`, `KT23 - Bằng khen của Bộ trưởng Bộ Công An` |
| `giayKhen` | G | `TEN LIKE '%Giấy khen%'` | Danh mục có `KT01 - Giấy khen`, `KT22 - Giấy khen...` |

`[Cần xác nhận]` Frontend report hiện có thêm field `kyNiemChuong`, nhưng mẫu Excel 3H không có cột này. Khi xuất đúng biểu mẫu 3H không nên thêm cột ngoài template.

### 6.2. Kỷ luật

| Field | Cột Excel | Mapping hiện có | Ghi chú |
|---|---|---|---|
| `tuocDanhHieuCand` | H | Join `DM_HINH_THUC_KY_LUAT`, `TEN LIKE '%Tước danh hiệu%CAND%'`; fallback mã cũ `5` | `[Cần xác nhận]` nếu field đang lưu ID danh mục |
| `cachChucGiangCapBacHam` | I | `TEN LIKE '%Cách chức%giáng cấp bậc hàm%'` | `[Cần mapping danh mục]` |
| `cachChucHaBacLuong` | J | `TEN LIKE '%Cách chức%hạ bậc lương%'` | `[Cần mapping danh mục]` |
| `giangChucGiangCapBacHam` | K | `[Cần mapping danh mục]` | Chưa thấy mã riêng trong DDL hiện tại |
| `giangCapBacHamHaBacLuong` | L | `[Cần mapping danh mục]` | Chưa thấy mã riêng trong DDL hiện tại |
| `haBacLuongGiangCapBacHam` | M | `[Cần mapping danh mục]` | Chưa thấy mã riêng trong DDL hiện tại |
| `canhCao` | N | `DM_HINH_THUC_KY_LUAT.MA='CB'` hoặc `TEN LIKE '%Cảnh cáo%'`; fallback mã cũ `2` | Có danh mục `CB - Cảnh cáo` |
| `khienTrach` | O | `DM_HINH_THUC_KY_LUAT.MA='KN'` hoặc `TEN LIKE '%Khiển trách%'`; fallback mã cũ `1` | Có danh mục `KN - Khiển trách` |

`[Cần xác nhận]` Schema hiện tại cho phép lưu `HINH_THUC_KY_LUAT` dạng chuỗi, nhưng danh mục hiện chưa thấy đủ tên/mã cho 5 cột tổ hợp `I:M`. Nếu nghiệp vụ bắt buộc đúng 8 cột, cần bổ sung mã danh mục hình thức kỷ luật chi tiết.

## 7. Mapping dòng đối tượng

| `row_code` | Rule đề xuất | Mức chắc chắn |
|---|---|---|
| `GIAO_VIEN` | `CAN_BO_NHA_GIAO.PHAN_LOAI = 1` | `[Suy luận]`, theo mẫu 1H/2H đã dùng |
| `CAN_BO_QLGD` | Chức danh/chức vụ hiện hành chứa `quản lý giáo dục` hoặc danh mục tương ứng | `[Cần xác nhận]` |
| `CAN_BO_KHAC` | Cán bộ còn lại, ví dụ `PHAN_LOAI = 2` và không thuộc quản lý giáo dục | `[Suy luận]` |
| `TAP_THE` | Khen thưởng tập thể theo `DM_HINH_THUC_KHEN_THUONG.DOI_TUONG_SD LIKE '%Tập thể%'` hoặc nguồn khen thưởng tập thể riêng | `[Cần xác nhận]` |

`[Cần xác nhận]` Dòng `Tập thể` khó mapping trực tiếp từ `KHEN_THUONG_CAN_BO` vì DDL yêu cầu `CAN_BO_GIANG_VIEN_ID NOT NULL`. Cần xác định hệ thống có bảng khen thưởng tập thể riêng, hoặc record cán bộ chỉ là người đại diện tập thể.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `MA_DON_VI` trên bảng sự kiện; áp dụng phân quyền theo đơn vị đăng nhập |
| `tuNgay` | Date | `KHEN_THUONG_CAN_BO.THOI_GIAN_KHEN_THUONG >= tuNgay`; `KY_LUAT_CAN_BO.TU_NGAY >= tuNgay` |
| `denNgay` | Date | `KHEN_THUONG_CAN_BO.THOI_GIAN_KHEN_THUONG <= denNgay`; `KY_LUAT_CAN_BO.TU_NGAY <= denNgay` |
| `workflowStatus` | String | Mặc định `Approved` |
| `countMode` | Enum | `LUOT` mặc định; `NGUOI` nếu nghiệp vụ muốn không đếm trùng cá nhân trong cùng cột |

## 9. API hiện có và API báo cáo đề xuất

### 9.1. API nghiệp vụ hiện có

| Màn | API | Ghi chú |
|---|---|---|
| Khen thưởng cán bộ, giáo viên | `/api/v1/khen-thuong-can-bo-giao-vien` | CRUD/search nghiệp vụ |
| Kỷ luật cán bộ, giáo viên | `/api/v1/ky-luat-can-bo-giao-vien` | CRUD/search nghiệp vụ |

Frontend report hiện gọi BCTK:

- `/bctk/api/bao-cao/can-bo-hoc-vien/thong-ke-khen-thuong-ky-luat-can-bo`
- `/bctk/api/bao-cao/can-bo-hoc-vien/thong-ke-khen-thuong-ky-luat-can-bo/group-by-don-vi`

### 9.2. API query theo biểu mẫu 3H

```http
GET /api/v1/reports/3h/khen-thuong-ky-luat-can-bo-giao-vien
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `tuNgay` | Có | Ngày bắt đầu kỳ |
| `denNgay` | Có | Ngày kết thúc kỳ |
| `countMode` | Không | `LUOT` hoặc `NGUOI` |

Response đề xuất:

```json
{
  "reportCode": "3H",
  "title": "Thống kê khen thưởng, kỷ luật cán bộ, giáo viên",
  "filters": {
    "maDonVi": "T01",
    "tuNgay": "2026-01-01",
    "denNgay": "2026-05-31",
    "countMode": "LUOT"
  },
  "rows": [
    {
      "rowCode": "GIAO_VIEN",
      "doiTuong": "Giáo viên",
      "coThiDua": 0,
      "huanChuong": 0,
      "huyChuong": 0,
      "bangKhen": 0,
      "giayKhen": 0,
      "tuocDanhHieuCand": 0,
      "cachChucGiangCapBacHam": 0,
      "cachChucHaBacLuong": 0,
      "giangChucGiangCapBacHam": 0,
      "giangCapBacHamHaBacLuong": 0,
      "haBacLuongGiangCapBacHam": 0,
      "canhCao": 0,
      "khienTrach": 0,
      "ghiChu": null
    }
  ]
}
```

## 10. SQL Proc Oracle đề xuất

```sql
CREATE OR REPLACE PROCEDURE X02_BCTK.PROC_RPT_3H_KT_KL_CAN_BO_GV (
    P_MA_DON_VI  IN VARCHAR2 DEFAULT NULL,
    P_TU_NGAY    IN DATE,
    P_DEN_NGAY   IN DATE,
    P_COUNT_MODE IN VARCHAR2 DEFAULT 'LUOT',
    O_RESULT     OUT SYS_REFCURSOR
) AS
BEGIN
    OPEN O_RESULT FOR
        WITH report_rows AS (
            SELECT 'GIAO_VIEN' row_code, 'Giáo viên' row_name, 1 sort_order FROM dual
            UNION ALL SELECT 'CAN_BO_QLGD', 'Cán bộ quản lý giáo dục', 2 FROM dual
            UNION ALL SELECT 'CAN_BO_KHAC', 'Cán bộ khác', 3 FROM dual
            UNION ALL SELECT 'TAP_THE', 'Tập thể', 4 FROM dual
        ),
        latest_cong_tac AS (
            SELECT *
            FROM (
                SELECT qt.*,
                       ROW_NUMBER() OVER (
                           PARTITION BY qt.CAN_BO_NHA_GIAO_ID
                           ORDER BY NVL(qt.THOI_GIAN_AP_DUNG, qt.CREATED_AT) DESC, qt.CREATED_AT DESC
                       ) rn
                FROM X02_APP.QUA_TRINH_GIANG_DAY_CONG_TAC qt
                WHERE NVL(qt.IS_DELETED, 0) = 0
                  AND NVL(qt.IS_ACTIVE, 1) = 1
                  AND qt.WORKFLOW_STATUS = 'Approved'
            )
            WHERE rn = 1
        ),
        staff_class AS (
            SELECT
                cb.ID AS can_bo_id,
                CASE
                    WHEN UPPER(NVL(cd.TEN, '') || ' ' || NVL(cv.TEN, '')) LIKE '%QUẢN LÝ GIÁO DỤC%' THEN 'CAN_BO_QLGD'
                    WHEN cb.PHAN_LOAI = 1 THEN 'GIAO_VIEN'
                    WHEN cb.PHAN_LOAI = 2 THEN 'CAN_BO_KHAC'
                    ELSE 'CAN_BO_KHAC'
                END AS row_code
            FROM X02_APP.CAN_BO_NHA_GIAO cb
            LEFT JOIN latest_cong_tac qt ON qt.CAN_BO_NHA_GIAO_ID = cb.ID
            LEFT JOIN X02_DM.DM_CHUC_DANH cd ON cd.ID = qt.CHUC_DANH_ID
            LEFT JOIN X02_DM.DM_CHUC_VU cv ON cv.ID = qt.CHUC_VU_ID
            WHERE NVL(cb.IS_DELETED, 0) = 0
              AND NVL(cb.IS_ACTIVE, 1) = 1
              AND cb.WORKFLOW_STATUS = 'Approved'
        ),
        reward_events AS (
            SELECT
                'KT_' || kt.ID AS event_id,
                kt.CAN_BO_GIANG_VIEN_ID AS can_bo_id,
                CASE
                    WHEN UPPER(NVL(ht.DOI_TUONG_SD, '')) LIKE '%TẬP THỂ%'
                      OR UPPER(NVL(ht.DOI_TUONG_SD, '')) LIKE '%TAP THE%' THEN 'TAP_THE'
                    ELSE sc.row_code
                END AS row_code,
                CASE
                    WHEN ht.MA = 'KT10' OR UPPER(ht.TEN) LIKE '%CỜ THI ĐUA%' THEN 'CO_THI_DUA'
                    WHEN UPPER(ht.TEN) LIKE '%HUÂN CHƯƠNG%' OR UPPER(ht.TEN) LIKE '%HUAN CHUONG%' THEN 'HUAN_CHUONG'
                    WHEN UPPER(ht.TEN) LIKE '%HUY CHƯƠNG%' THEN 'HUY_CHUONG'
                    WHEN UPPER(ht.TEN) LIKE '%BẰNG KHEN%' OR UPPER(ht.TEN) LIKE '%BANG KHEN%' THEN 'BANG_KHEN'
                    WHEN UPPER(ht.TEN) LIKE '%GIẤY KHEN%' OR UPPER(ht.TEN) LIKE '%GIAY KHEN%' THEN 'GIAY_KHEN'
                    ELSE 'KHEN_THUONG_KHAC'
                END AS column_code,
                CASE WHEN UPPER(P_COUNT_MODE) = 'NGUOI'
                     THEN kt.CAN_BO_GIANG_VIEN_ID
                     ELSE 'KT_' || kt.ID
                END AS count_key
            FROM X02_APP.KHEN_THUONG_CAN_BO kt
            LEFT JOIN X02_DM.DM_HINH_THUC_KHEN_THUONG ht ON ht.ID = kt.LOAI_HINH_KHEN_THUONG_ID
            LEFT JOIN staff_class sc ON sc.can_bo_id = kt.CAN_BO_GIANG_VIEN_ID
            WHERE NVL(kt.IS_DELETED, 0) = 0
              AND NVL(kt.IS_ACTIVE, 1) = 1
              AND kt.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR kt.MA_DON_VI = P_MA_DON_VI)
              AND kt.THOI_GIAN_KHEN_THUONG BETWEEN P_TU_NGAY AND P_DEN_NGAY
        ),
        discipline_events AS (
            SELECT
                'KL_' || kl.ID AS event_id,
                kl.DOI_TUONG_KY_LUAT_ID AS can_bo_id,
                sc.row_code,
                CASE
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%TƯỚC%DANH HIỆU%CAND%'
                      OR kl.HINH_THUC_KY_LUAT = '5' THEN 'TUOC_DANH_HIEU_CAND'
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%CÁCH CHỨC%GIÁNG CẤP BẬC HÀM%'
                      OR UPPER(NVL(hkl.TEN, '')) LIKE '%CACH CHUC%GIANG CAP BAC HAM%' THEN 'CACH_CHUC_GIANG_CAP_BAC_HAM'
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%CÁCH CHỨC%HẠ BẬC LƯƠNG%'
                      OR UPPER(NVL(hkl.TEN, '')) LIKE '%CACH CHUC%HA BAC LUONG%' THEN 'CACH_CHUC_HA_BAC_LUONG'
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%GIÁNG CHỨC%GIÁNG CẤP BẬC HÀM%'
                      OR UPPER(NVL(hkl.TEN, '')) LIKE '%GIANG CHUC%GIANG CAP BAC HAM%' THEN 'GIANG_CHUC_GIANG_CAP_BAC_HAM'
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%GIÁNG CẤP BẬC HÀM%HẠ BẬC LƯƠNG%'
                      OR UPPER(NVL(hkl.TEN, '')) LIKE '%GIANG CAP BAC HAM%HA BAC LUONG%' THEN 'GIANG_CAP_BAC_HAM_HA_BAC_LUONG'
                    WHEN UPPER(NVL(hkl.TEN, '')) LIKE '%HẠ BẬC LƯƠNG%GIÁNG CẤP BẬC HÀM%'
                      OR UPPER(NVL(hkl.TEN, '')) LIKE '%HA BAC LUONG%GIANG CAP BAC HAM%' THEN 'HA_BAC_LUONG_GIANG_CAP_BAC_HAM'
                    WHEN hkl.MA = 'CB' OR UPPER(NVL(hkl.TEN, '')) LIKE '%CẢNH CÁO%'
                      OR kl.HINH_THUC_KY_LUAT = '2' THEN 'CANH_CAO'
                    WHEN hkl.MA = 'KN' OR UPPER(NVL(hkl.TEN, '')) LIKE '%KHIỂN TRÁCH%'
                      OR kl.HINH_THUC_KY_LUAT = '1' THEN 'KHIEN_TRACH'
                    ELSE 'KY_LUAT_KHAC'
                END AS column_code,
                CASE WHEN UPPER(P_COUNT_MODE) = 'NGUOI'
                     THEN kl.DOI_TUONG_KY_LUAT_ID
                     ELSE 'KL_' || kl.ID
                END AS count_key
            FROM X02_APP.KY_LUAT_CAN_BO kl
            LEFT JOIN X02_DM.DM_HINH_THUC_KY_LUAT hkl ON hkl.ID = kl.HINH_THUC_KY_LUAT
            LEFT JOIN staff_class sc ON sc.can_bo_id = kl.DOI_TUONG_KY_LUAT_ID
            WHERE NVL(kl.IS_DELETED, 0) = 0
              AND NVL(kl.IS_ACTIVE, 1) = 1
              AND kl.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR kl.MA_DON_VI = P_MA_DON_VI)
              AND kl.TU_NGAY BETWEEN P_TU_NGAY AND P_DEN_NGAY
        ),
        all_events AS (
            SELECT * FROM reward_events
            UNION ALL
            SELECT * FROM discipline_events
        ),
        agg AS (
            SELECT
                row_code,
                COUNT(DISTINCT CASE WHEN column_code = 'CO_THI_DUA' THEN count_key END) AS co_thi_dua,
                COUNT(DISTINCT CASE WHEN column_code = 'HUAN_CHUONG' THEN count_key END) AS huan_chuong,
                COUNT(DISTINCT CASE WHEN column_code = 'HUY_CHUONG' THEN count_key END) AS huy_chuong,
                COUNT(DISTINCT CASE WHEN column_code = 'BANG_KHEN' THEN count_key END) AS bang_khen,
                COUNT(DISTINCT CASE WHEN column_code = 'GIAY_KHEN' THEN count_key END) AS giay_khen,
                COUNT(DISTINCT CASE WHEN column_code = 'TUOC_DANH_HIEU_CAND' THEN count_key END) AS tuoc_danh_hieu_cand,
                COUNT(DISTINCT CASE WHEN column_code = 'CACH_CHUC_GIANG_CAP_BAC_HAM' THEN count_key END) AS cach_chuc_giang_cap_bac_ham,
                COUNT(DISTINCT CASE WHEN column_code = 'CACH_CHUC_HA_BAC_LUONG' THEN count_key END) AS cach_chuc_ha_bac_luong,
                COUNT(DISTINCT CASE WHEN column_code = 'GIANG_CHUC_GIANG_CAP_BAC_HAM' THEN count_key END) AS giang_chuc_giang_cap_bac_ham,
                COUNT(DISTINCT CASE WHEN column_code = 'GIANG_CAP_BAC_HAM_HA_BAC_LUONG' THEN count_key END) AS giang_cap_bac_ham_ha_bac_luong,
                COUNT(DISTINCT CASE WHEN column_code = 'HA_BAC_LUONG_GIANG_CAP_BAC_HAM' THEN count_key END) AS ha_bac_luong_giang_cap_bac_ham,
                COUNT(DISTINCT CASE WHEN column_code = 'CANH_CAO' THEN count_key END) AS canh_cao,
                COUNT(DISTINCT CASE WHEN column_code = 'KHIEN_TRACH' THEN count_key END) AS khien_trach
            FROM all_events
            GROUP BY row_code
        ),
        agg_total AS (
            SELECT * FROM agg
            UNION ALL
            SELECT
                'TOTAL',
                SUM(co_thi_dua),
                SUM(huan_chuong),
                SUM(huy_chuong),
                SUM(bang_khen),
                SUM(giay_khen),
                SUM(tuoc_danh_hieu_cand),
                SUM(cach_chuc_giang_cap_bac_ham),
                SUM(cach_chuc_ha_bac_luong),
                SUM(giang_chuc_giang_cap_bac_ham),
                SUM(giang_cap_bac_ham_ha_bac_luong),
                SUM(ha_bac_luong_giang_cap_bac_ham),
                SUM(canh_cao),
                SUM(khien_trach)
            FROM agg
        )
        SELECT
            rr.row_code,
            rr.row_name AS doi_tuong,
            rr.sort_order,
            NVL(a.co_thi_dua, 0) AS co_thi_dua,
            NVL(a.huan_chuong, 0) AS huan_chuong,
            NVL(a.huy_chuong, 0) AS huy_chuong,
            NVL(a.bang_khen, 0) AS bang_khen,
            NVL(a.giay_khen, 0) AS giay_khen,
            NVL(a.tuoc_danh_hieu_cand, 0) AS tuoc_danh_hieu_cand,
            NVL(a.cach_chuc_giang_cap_bac_ham, 0) AS cach_chuc_giang_cap_bac_ham,
            NVL(a.cach_chuc_ha_bac_luong, 0) AS cach_chuc_ha_bac_luong,
            NVL(a.giang_chuc_giang_cap_bac_ham, 0) AS giang_chuc_giang_cap_bac_ham,
            NVL(a.giang_cap_bac_ham_ha_bac_luong, 0) AS giang_cap_bac_ham_ha_bac_luong,
            NVL(a.ha_bac_luong_giang_cap_bac_ham, 0) AS ha_bac_luong_giang_cap_bac_ham,
            NVL(a.canh_cao, 0) AS canh_cao,
            NVL(a.khien_trach, 0) AS khien_trach,
            CAST(NULL AS VARCHAR2(1000)) AS ghi_chu
        FROM report_rows rr
        LEFT JOIN agg_total a ON a.row_code = rr.row_code
        ORDER BY rr.sort_order;
END;
/
```

Ghi chú SQL:

- Các cột kỷ luật tổ hợp như `CACH_CHUC_GIANG_CAP_BAC_HAM` chỉ có số liệu khi `DM_HINH_THUC_KY_LUAT.TEN` đủ chi tiết. Không nên tự chia một mã chung `Cách chức` vào một cột duy nhất nếu chưa có nghiệp vụ xác nhận.
- Nếu `KY_LUAT_CAN_BO.HINH_THUC_KY_LUAT` đang lưu mã thay vì ID danh mục, đổi join sang `hkl.MA = kl.HINH_THUC_KY_LUAT`.
- Dòng `TAP_THE` chỉ là mapping tạm qua `DM_HINH_THUC_KHEN_THUONG.DOI_TUONG_SD`; cần xác nhận nguồn thực tế cho khen thưởng tập thể.

## 11. Query chi tiết phục vụ drill-down

```sql
SELECT
    'KHEN_THUONG' AS loai_su_kien,
    kt.ID,
    kt.MA_DON_VI,
    kt.CAN_BO_GIANG_VIEN_ID AS can_bo_id,
    ht.MA AS ma_hinh_thuc,
    ht.TEN AS ten_hinh_thuc,
    kt.TEN_KHEN_THUONG,
    kt.THOI_GIAN_KHEN_THUONG AS ngay_su_kien,
    kt.WORKFLOW_STATUS
FROM X02_APP.KHEN_THUONG_CAN_BO kt
LEFT JOIN X02_DM.DM_HINH_THUC_KHEN_THUONG ht ON ht.ID = kt.LOAI_HINH_KHEN_THUONG_ID
WHERE NVL(kt.IS_DELETED, 0) = 0
  AND NVL(kt.IS_ACTIVE, 1) = 1
  AND kt.WORKFLOW_STATUS = 'Approved'
UNION ALL
SELECT
    'KY_LUAT' AS loai_su_kien,
    kl.ID,
    kl.MA_DON_VI,
    kl.DOI_TUONG_KY_LUAT_ID AS can_bo_id,
    COALESCE(hkl.MA, kl.HINH_THUC_KY_LUAT) AS ma_hinh_thuc,
    CASE
        WHEN hkl.TEN IS NOT NULL THEN hkl.TEN
        WHEN kl.HINH_THUC_KY_LUAT = '1' THEN 'Khiển trách'
        WHEN kl.HINH_THUC_KY_LUAT = '2' THEN 'Cảnh cáo'
        WHEN kl.HINH_THUC_KY_LUAT = '3' THEN 'Cách chức'
        WHEN kl.HINH_THUC_KY_LUAT = '4' THEN 'Buộc thôi việc'
        WHEN kl.HINH_THUC_KY_LUAT = '5' THEN 'Tước danh hiệu CAND'
        ELSE 'Khác'
    END AS ten_hinh_thuc,
    kl.LY_DO_KY_LUAT AS ten_su_kien,
    kl.TU_NGAY AS ngay_su_kien,
    kl.WORKFLOW_STATUS
FROM X02_APP.KY_LUAT_CAN_BO kl
LEFT JOIN X02_DM.DM_HINH_THUC_KY_LUAT hkl ON hkl.ID = kl.HINH_THUC_KY_LUAT
WHERE NVL(kl.IS_DELETED, 0) = 0
  AND NVL(kl.IS_ACTIVE, 1) = 1
  AND kl.WORKFLOW_STATUS = 'Approved';
```

## 12. Quy tắc đối soát

| STT | Quy tắc | Cách kiểm |
|---:|---|---|
| 1 | Tổng từng cột bằng tổng 4 dòng đối tượng | `TOTAL[col] = SUM(GIAO_VIEN..TAP_THE[col])` |
| 2 | Khen thưởng chỉ lấy bản ghi đã duyệt | `WORKFLOW_STATUS = 'Approved'`, `IS_DELETED = 0`, `IS_ACTIVE = 1` |
| 3 | Kỷ luật chỉ lấy bản ghi đã duyệt | `WORKFLOW_STATUS = 'Approved'`, `IS_DELETED = 0`, `IS_ACTIVE = 1` |
| 4 | Không đếm ngoài kỳ | Ngày khen thưởng/kỷ luật nằm trong `tuNgay..denNgay` |
| 5 | Đếm lượt | Mỗi bản ghi sự kiện là một lượt |
| 6 | Đếm người | Mỗi người chỉ tính một lần trong cùng ô báo cáo |
| 7 | Dòng tập thể | Không trộn khen thưởng tập thể vào cá nhân nếu có nguồn tập thể riêng |
| 8 | Công thức Excel | Cần bổ sung tổng `H12:O12` khi render/export |

## 13. Gaps và câu hỏi cần xác nhận

| STT | Vấn đề | Ảnh hưởng | Đề xuất |
|---:|---|---|---|
| 1 | Dòng `Tập thể` chưa có nguồn rõ trong `KHEN_THUONG_CAN_BO` | Có thể thiếu số liệu tập thể hoặc đếm nhầm đại diện cá nhân | Xác nhận bảng/field lưu khen thưởng tập thể |
| 2 | Danh mục/schema hiện chưa thấy đủ mã cho 8 cột kỷ luật chi tiết | Không thể sinh đủ cột `I:M` chính xác | Bổ sung danh mục hình thức kỷ luật chi tiết hoặc chốt mapping từ `DM_HINH_THUC_KY_LUAT` |
| 3 | Template thiếu công thức tổng `H12:O12` | Tổng kỷ luật trên Excel có thể trống | Bổ sung công thức khi export |
| 4 | Header merged `D6:G6` nhưng nhóm khen thưởng có vẻ bắt đầu từ `C7` | Có thể lỗi merge trong template | Xác nhận với mẫu chuẩn; khi render nên giữ đúng file hoặc sửa merge thành `C6:G6` |
| 5 | Frontend report có `kyNiemChuong`, mẫu Excel không có | UI/API hiện tại có thể lệch biểu mẫu 3H | Khi export 3H dùng đúng cột `C:G`, không thêm `kyNiemChuong` |
| 6 | Phân loại cán bộ quản lý giáo dục chưa có rule chính thức | Dòng `Cán bộ quản lý giáo dục` có thể sai | Chốt danh mục chức danh/chức vụ hoặc field phân loại |

## 14. Nguồn tham chiếu trong repo

| Nguồn | Ý nghĩa |
|---|---|
| `docs/report-input/3H.xlsx` | Template Excel gốc |
| `src/backend/qldt-v2/database/oracle/business/36_khen_thuong_can_bo_create.sql` | DDL khen thưởng cán bộ |
| `src/backend/qldt-v2/database/oracle/business/35_ky_luat_can_bo_create.sql` | DDL kỷ luật cán bộ |
| `docs/database/X02_DM.sql` | Danh mục khen thưởng/kỷ luật |
| `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/stf/khenthuongcanbogiaovien/controller/KhenThuongCanBoController.java` | API nghiệp vụ khen thưởng |
| `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/stf/kyluatcanbogiaovien/controller/KyLuatCanBoController.java` | API nghiệp vụ kỷ luật |
| `src/frontend/frontend-x02-v2/src/domains/reports/services/reports.service.js` | API report frontend hiện dùng |
| `src/frontend/frontend-x02-v2/src/domains/reports/pages/KhenThuongKyLuatCanBoReportPage.jsx` | Field report hiện có trên frontend |

## 15. Checklist triển khai

| Hạng mục | Trạng thái |
|---|---|
| Đọc template `3H.xlsx` | Đã xong |
| Mapping layout Excel | Đã xong |
| Mapping bảng nghiệp vụ | Đã xong |
| Mapping khen thưởng | Tương đối rõ |
| Mapping kỷ luật chi tiết | `[Cần mapping danh mục]` |
| Mapping dòng tập thể | `[Cần xác nhận]` |
| SQL Proc đề xuất | Đã có skeleton |
| API đề xuất | Đã có |
| Quy tắc đối soát | Đã có |

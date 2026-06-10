# Báo cáo 12H - Thống kê số liệu kết quả phân loại học tập, rèn luyện của học viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/12H.xlsx` |
| Sheet | `Phan loai HV` |
| Mã biểu mẫu | `Biểu mẫu 12H` |
| Tên báo cáo | `THỐNG KÊ SỐ LIỆU KẾT QUẢ PHÂN LOẠI HỌC TẬP, RÈN LUYỆN CỦA HỌC VIÊN` |
| Vùng dữ liệu có giá trị | `A1:G15` |
| Vùng style kéo dài | `A1:G22` |
| Công thức Excel | Có 2 công thức: `D8=SUM(D9:D15)`, `E8=SUM(E9:E15)` |
| Dạng báo cáo | Bảng tổng hợp số học viên theo mức phân loại học tập, rèn luyện và kết quả phân loại tập thể học viên |

`[Cần xác nhận]` Header Excel gộp `C6:D6` cho nhãn `Học tập`, nhưng công thức tổng lại đặt ở `D8`, trong khi component frontend hiện hành render cột `Học tập` là một cột riêng. Khi export theo template Excel cần chốt cột C có để trống/ẩn hay là phần cấu trúc gộp của cột học tập.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê kết quả phân loại học tập và rèn luyện của học viên theo các mức:

- Xuất sắc.
- Giỏi (Tốt).
- Khá.
- Trung bình khá.
- Trung bình.
- Yếu.
- Kém.

`[Suy luận]` Báo cáo phục vụ theo dõi chất lượng người học theo năm học/học kỳ và theo đơn vị. Nguồn nghiệp vụ chính là `HV_PHAN_LOAI` cho phân loại học tập/người học và `HV_KET_QUA_REN_LUYEN` cho rèn luyện. Frontend đã có báo cáo riêng tại slug `phan-loai-hoc-tap-ren-luyen-hoc-vien`.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:G1` | `Biểu mẫu 12H` | Merged |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:G3` | Tên báo cáo | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `C4:G4` | `(Kèm theo Báo cáo số tháng năm 2026)` | Merged |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A6` | `STT` | `stt` |
| `B6` | `Mức phân loại` | `mucPhanLoai`, `rowCode` |
| `C6:D6` | `Học tập` | `hocTap` |
| `E6` | `Rèn luyện` | `renLuyen` |
| `F6` | `Kết quả phân loại tập thể học viên` | `kqPlTapThe` |
| `G6` | `Ghi chú` | `ghiChu` |
| `A7:G7` | Dòng chỉ số cột | Template đang ghi `(1)`, `(2)`, `(1)`, `(3)`, `(4)`, `(5)`, `(6)` |

`[Cần xác nhận]` Dòng chỉ số cột trong Excel có `C7=(1)` lặp lại với `A7=(1)`. Component frontend hiện hành dùng chỉ số `(1)..(6)` cho 6 cột thực tế, không có cột C/D tách như Excel.

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 8 |  | Tổng số học viên tham gia phân loại | `tongSo` | Tổng các mức row 9-15 |
| 9 | 1 | Xuất sắc | `xuatSac` | `DM_PHAN_LOAI_HOC_VIEN.TEN='Xuất sắc'`; rèn luyện fallback `DM_PHAN_LOAI_CHAT_LUONG.TEN='Xuất sắc'` |
| 10 | 2 | Giỏi (Tốt) | `gioiTot` | `DM_PHAN_LOAI_HOC_VIEN.TEN='Giỏi (Tốt)'`; rèn luyện có thể map `Tốt`/`Giỏi (Tốt)` `[Cần mapping danh mục]` |
| 11 | 3 | Khá | `kha` | Danh mục phân loại học viên/rèn luyện |
| 12 | 4 | Trung bình khá | `trungBinhKha` | Danh mục phân loại học viên/rèn luyện |
| 13 | 5 | Trung bình | `trungBinh` | Template ghi `Trung bình`, danh mục có `Trung bình (Đạt)` `[Cần mapping danh mục]` |
| 14 | 6 | Yếu | `yeu` | Danh mục phân loại học viên/rèn luyện |
| 15 | 7 | Kém | `kem` | Danh mục phân loại học viên/rèn luyện |

`[Cần xác nhận]` Component frontend có thêm mức `Không/ Chưa phân loại`, nhưng `12H.xlsx` chỉ có 7 mức và không có dòng không/chưa phân loại. Nếu API trả nhóm này, export Excel 12H cần chốt bỏ qua, gộp ghi chú, hoặc bổ sung dòng.

## 5. Mapping cột giá trị

| Cột | Header Excel | Field đề xuất | Mapping DB/API đề xuất |
|---|---|---|---|
| `D` | Học tập | `hocTap` | Count `HV_PHAN_LOAI.ID` theo `PHAN_LOAI_HOC_VIEN_ID` |
| `E` | Rèn luyện | `renLuyen` | Count `HV_KET_QUA_REN_LUYEN.ID` theo `XEP_LOAI_REN_LUYEN_ID` |
| `F` | Kết quả phân loại tập thể học viên | `kqPlTapThe` | `[Cần xác nhận]` Có thể là phân loại tập thể/lớp/trung đội; chưa thấy bảng nguồn trực tiếp trong DDL đã đọc |
| `G` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay |

`[Cần xác nhận]` Cột `Học tập` trong Excel được merge `C6:D6` nhưng dữ liệu/công thức đặt ở `D`. Nên coi `D` là cột số liệu chính khi đọc template hiện tại.

## 6. Công thức Excel trong template

| Ô | Ý nghĩa | Công thức | Nhận xét |
|---|---|---|---|
| `D8` | Tổng học tập | `=SUM(D9:D15)` | Cộng 7 mức phân loại |
| `E8` | Tổng rèn luyện | `=SUM(E9:E15)` | Cộng 7 mức phân loại |

Các tổng còn thiếu:

| Vùng | Tổng nên có | Ghi chú |
|---|---|---|
| `F8` | Tổng kết quả phân loại tập thể học viên | Component frontend hiện có `kqPlTapThe`, nhưng Excel gốc không có công thức tổng |

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HV_PHAN_LOAI` / `/api/v1/phan-loai-nguoi-hoc` | Nguồn phân loại học tập/người học | `HOC_VIEN_ID`, `KY_PHAN_LOAI`, `NAM_HOC_ID`, `HOC_KY_ID`, `PHAN_LOAI_HOC_VIEN_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.HV_KET_QUA_REN_LUYEN` / `/api/v1/ket-qua-ren-luyen` | Nguồn kết quả rèn luyện | `HOC_VIEN_ID`, `KY_DANH_GIA`, `THANG_DANH_GIA`, `HOC_KY_ID`, `NAM_HOC_ID`, `DIEM_REN_LUYEN`, `XEP_LOAI_REN_LUYEN_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.HOC_VIEN` | Join đơn vị, ngành, trình độ, trạng thái học viên | `ID`, `TRINH_DO_DAO_TAO_ID`, `NGANH_ID`, `KHOA_HOC_ID`, `TRUNG_DOI_ID`, `TRANG_THAI_HOC_ID`, `MA_DON_VI` |
| `X02_APP.HOC_VIEN_TRUNG_DOI`, `TRUNG_DOI` | Nguồn phụ nếu cần phân loại tập thể theo trung đội/lớp | `HOC_VIEN_ID`, `TRUNG_DOI_ID`, `NAM_HOC_ID`, `TRUNG_DOI.QUAN_SO`, `TRUNG_DOI.NAM_HOC` |
| `X02_DM.DM_PHAN_LOAI_HOC_VIEN` | Mapping mức phân loại học tập/người học | `ID`, `MA`, `TEN`, `INDEX_ORDER` |
| `X02_DM.DM_PHAN_LOAI_CHAT_LUONG` | Fallback lookup rèn luyện theo dashboard LRN hiện tại | `ID`, `MA`, `TEN`, `KHOI_TRUONG_ID` |
| `X02_DM.DM_NAM_HOC` | Lọc năm học | `ID`, `MA`, `TEN`, `THOI_GIAN_BAT_DAU`, `THOI_GIAN_KET_THUC` |

`[Cần xác nhận]` Dashboard LRN ghi `XEP_LOAI_REN_LUYEN_ID` cần chốt lookup giữa `DM_PHAN_LOAI_HOC_VIEN` và `DM_PHAN_LOAI_CHAT_LUONG`; hiện service dashboard đang join `HV_KET_QUA_REN_LUYEN.XEP_LOAI_REN_LUYEN_ID` với `DM_PHAN_LOAI_CHAT_LUONG`.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `HV_PHAN_LOAI.MA_DON_VI`, `HV_KET_QUA_REN_LUYEN.MA_DON_VI` hoặc qua `HOC_VIEN.MA_DON_VI`; mặc định theo quyền user |
| `namHocId` | String | `HV_PHAN_LOAI.NAM_HOC_ID`, `HV_KET_QUA_REN_LUYEN.NAM_HOC_ID` |
| `hocKyId` | String | `HV_PHAN_LOAI.HOC_KY_ID`, `HV_KET_QUA_REN_LUYEN.HOC_KY_ID` |
| `kyPhanLoai` | Number | `HV_PHAN_LOAI.KY_PHAN_LOAI` nếu không dùng học kỳ |
| `kyDanhGia` | Number | `HV_KET_QUA_REN_LUYEN.KY_DANH_GIA` |
| `trinhDoDaoTaoIds` | String[] | `HOC_VIEN.TRINH_DO_DAO_TAO_ID` |
| `khoaHocId` | String | `HOC_VIEN.KHOA_HOC_ID` |
| `workflowStatus` | String | Mặc định `Approved` |

Frontend hiện hành gọi:

```http
GET /bctk/api/bao-cao/xep-loai-chat-luong-giao-duc-dao-tao/ket-qua-phan-loai-hoc-tap-ren-luyen
GET /bctk/api/bao-cao/xep-loai-chat-luong-giao-duc-dao-tao/ket-qua-phan-loai-hoc-tap-ren-luyen/group-by-don-vi
```

với params `maDonVi`, `namHocId`, `hocKyId`.

## 9. API report đề xuất

Nếu chuẩn hóa theo nhóm `/api/v1/reports`:

```http
GET /api/v1/reports/12h/phan-loai-hoc-tap-ren-luyen
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Có | Năm học cần thống kê |
| `hocKyId` | Không | Nếu báo cáo theo học kỳ |
| `workflowStatus` | Không | Mặc định `Approved` |
| `includeChuaPhanLoai` | Không | Mặc định `false` nếu xuất đúng Excel 12H |

Response đề xuất tương thích frontend hiện tại:

```json
[
  {
    "ten": "Xuất sắc",
    "hocTap": 0,
    "renLuyen": 0,
    "kqPlTapThe": 0
  },
  {
    "ten": "Giỏi (Tốt)",
    "hocTap": 0,
    "renLuyen": 0,
    "kqPlTapThe": 0
  }
]
```

Với cấp Cục/tổng hợp theo đơn vị:

```json
{
  "T01": [
    { "ten": "Xuất sắc", "hocTap": 0, "renLuyen": 0, "kqPlTapThe": 0 }
  ],
  "T02": [
    { "ten": "Xuất sắc", "hocTap": 0, "renLuyen": 0, "kqPlTapThe": 0 }
  ]
}
```

## 10. SQL/Proc đề xuất

### 10.1. Ý tưởng tổng hợp

- Dùng `DM_PHAN_LOAI_HOC_VIEN` làm danh sách mức hiển thị chính, lọc 7 mức trong template.
- Cột `hocTap`: đếm `HV_PHAN_LOAI` theo `PHAN_LOAI_HOC_VIEN_ID`.
- Cột `renLuyen`: đếm `HV_KET_QUA_REN_LUYEN` theo `XEP_LOAI_REN_LUYEN_ID`, cần mapping danh mục sang cùng `row_code`.
- Cột `kqPlTapThe`: chưa thấy nguồn rõ; để 0/null hoặc map từ bảng tập thể nếu nghiệp vụ bổ sung.
- Nếu mỗi học viên có nhiều bản ghi trong cùng năm/học kỳ, cần chọn bản ghi cuối cùng đã duyệt theo `APPROVED_AT` hoặc `UPDATED_AT`.

### 10.2. Skeleton SQL

```sql
WITH params AS (
    SELECT
        :ma_don_vi AS ma_don_vi,
        :nam_hoc_id AS nam_hoc_id,
        :hoc_ky_id AS hoc_ky_id,
        NVL(:workflow_status, 'Approved') AS workflow_status
    FROM dual
),
row_def AS (
    SELECT 'xuatSac' row_code, 1 sort_order, 'Xuất sắc' label FROM dual UNION ALL
    SELECT 'gioiTot', 2, 'Giỏi (Tốt)' FROM dual UNION ALL
    SELECT 'kha', 3, 'Khá' FROM dual UNION ALL
    SELECT 'trungBinhKha', 4, 'Trung bình khá' FROM dual UNION ALL
    SELECT 'trungBinh', 5, 'Trung bình' FROM dual UNION ALL
    SELECT 'yeu', 6, 'Yếu' FROM dual UNION ALL
    SELECT 'kem', 7, 'Kém' FROM dual
),
hoc_tap_latest AS (
    SELECT *
    FROM (
        SELECT
            pl.*,
            ROW_NUMBER() OVER (
                PARTITION BY pl.HOC_VIEN_ID, pl.NAM_HOC_ID, pl.HOC_KY_ID
                ORDER BY pl.APPROVED_AT DESC NULLS LAST, pl.UPDATED_AT DESC NULLS LAST, pl.CREATED_AT DESC
            ) rn
        FROM X02_APP.HV_PHAN_LOAI pl
        CROSS JOIN params p
        WHERE pl.IS_DELETED = 0
          AND pl.IS_ACTIVE = 1
          AND pl.WORKFLOW_STATUS = p.workflow_status
          AND (p.nam_hoc_id IS NULL OR pl.NAM_HOC_ID = p.nam_hoc_id)
          AND (p.hoc_ky_id IS NULL OR pl.HOC_KY_ID = p.hoc_ky_id)
          AND (p.ma_don_vi IS NULL OR pl.MA_DON_VI = p.ma_don_vi)
    )
    WHERE rn = 1
),
hoc_tap AS (
    SELECT
        map.row_code,
        COUNT(*) AS hoc_tap
    FROM hoc_tap_latest pl
    JOIN X02_APP.RPT_12H_PHAN_LOAI_MAP map
      ON map.source_type = 'HOC_TAP'
     AND map.source_id = pl.PHAN_LOAI_HOC_VIEN_ID
    GROUP BY map.row_code
),
ren_luyen_latest AS (
    SELECT *
    FROM (
        SELECT
            rl.*,
            ROW_NUMBER() OVER (
                PARTITION BY rl.HOC_VIEN_ID, rl.NAM_HOC_ID, rl.HOC_KY_ID
                ORDER BY rl.APPROVED_AT DESC NULLS LAST, rl.UPDATED_AT DESC NULLS LAST, rl.CREATED_AT DESC
            ) rn
        FROM X02_APP.HV_KET_QUA_REN_LUYEN rl
        CROSS JOIN params p
        WHERE rl.IS_DELETED = 0
          AND rl.IS_ACTIVE = 1
          AND rl.WORKFLOW_STATUS = p.workflow_status
          AND (p.nam_hoc_id IS NULL OR rl.NAM_HOC_ID = p.nam_hoc_id)
          AND (p.hoc_ky_id IS NULL OR rl.HOC_KY_ID = p.hoc_ky_id)
          AND (p.ma_don_vi IS NULL OR rl.MA_DON_VI = p.ma_don_vi)
    )
    WHERE rn = 1
),
ren_luyen AS (
    SELECT
        map.row_code,
        COUNT(*) AS ren_luyen
    FROM ren_luyen_latest rl
    JOIN X02_APP.RPT_12H_PHAN_LOAI_MAP map
      ON map.source_type = 'REN_LUYEN'
     AND map.source_id = rl.XEP_LOAI_REN_LUYEN_ID
    GROUP BY map.row_code
)
SELECT
    rd.sort_order,
    rd.row_code,
    rd.label AS ten,
    NVL(ht.hoc_tap, 0) AS hoc_tap,
    NVL(rl.ren_luyen, 0) AS ren_luyen,
    0 AS kq_pl_tap_the
FROM row_def rd
LEFT JOIN hoc_tap ht ON ht.row_code = rd.row_code
LEFT JOIN ren_luyen rl ON rl.row_code = rd.row_code
ORDER BY rd.sort_order;
```

`[Cần mapping danh mục]` Nên tạo bảng cấu hình `RPT_12H_PHAN_LOAI_MAP` để map `DM_PHAN_LOAI_HOC_VIEN` và `DM_PHAN_LOAI_CHAT_LUONG` về cùng 7 `row_code`, tránh so khớp text vì danh mục có biến thể `Trung bình (Đạt)`/`Tốt`.

## 11. Quy tắc đối soát

| Nhóm kiểm tra | Quy tắc |
|---|---|
| Tổng học tập | `D8 = SUM(D9:D15)` |
| Tổng rèn luyện | `E8 = SUM(E9:E15)` |
| Tổng tập thể | Nếu dùng cột `F`, `F8 = SUM(F9:F15)` dù template hiện thiếu công thức |
| Bản ghi mới nhất | Mỗi học viên chỉ nên được tính 1 lần cho cùng `namHocId + hocKyId + loại đánh giá` |
| Danh mục | Các mức trong API phải normalize được về 7 mức Excel; nhóm `Không/Chưa phân loại` cần xử lý rõ |
| Workflow | Chỉ đếm bản ghi đã duyệt, không xóa, còn hiệu lực |
| So sánh học tập/rèn luyện | `hocTap` và `renLuyen` có thể khác nhau nếu thiếu một trong hai loại bản ghi; cần warning dữ liệu thiếu |

## 12. Gap và câu hỏi cần xác nhận

| Nhóm | Vấn đề | Câu hỏi |
|---|---|---|
| Layout | Excel gộp `C6:D6`, dữ liệu ở `D`; frontend render 1 cột `Học tập` | Khi xuất Excel giữ layout gốc hay đồng bộ frontend 6 cột? |
| Dòng không/chưa phân loại | Frontend có `Không/ Chưa phân loại`, Excel không có | Có bổ sung dòng thứ 8 không? |
| Rèn luyện lookup | Dashboard đang dùng `DM_PHAN_LOAI_CHAT_LUONG`, nghiệp vụ có `DM_PHAN_LOAI_HOC_VIEN` | `XEP_LOAI_REN_LUYEN_ID` chuẩn trỏ danh mục nào? |
| Kết quả tập thể | Chưa thấy nguồn DB trực tiếp | Cột `Kết quả phân loại tập thể học viên` lấy từ bảng nào: trung đội/lớp/tập thể thi đua hay nhập tay? |
| Bản ghi trùng | Một học viên có nhiều phân loại trong kỳ | Chọn bản ghi mới nhất, bản ghi khóa, hay tổng lượt? |
| Cấp đơn vị | Frontend phân biệt mã `X*` cấp Cục và `T*` cấp Trường | API report có tiếp tục dùng quy ước mã đơn vị này không? |

## 13. Tham chiếu

- `docs/report-input/12H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/LRN-dashboard.md`
- `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`
- `src/frontend/frontend-x02-v2/src/domains/reports/pages/PhanLoaiHocTapRenLuyenReportPage.jsx`
- `src/frontend/frontend-x02-v2/src/domains/reports/services/reports.service.js`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/ketquarenluyen/entity/KetQuaRenLuyen.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/phanloainguoihoc/entity/PhanLoaiNguoiHoc.java`

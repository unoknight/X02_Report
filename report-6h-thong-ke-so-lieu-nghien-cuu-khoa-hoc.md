# Báo cáo 6H - Thống kê số liệu nghiên cứu khoa học

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/6H.xlsx` |
| Sheet | `NCKH CB, GV` |
| Mã biểu mẫu | `Biễu mẫu 6H` |
| Tên báo cáo | `THỐNG KÊ SỐ LIỆU NGHIÊN CỨU KHOA HỌC` |
| Vùng dữ liệu chính | `B7:M16` |
| Công thức Excel | Không có công thức |
| Dạng báo cáo | Tổng hợp số lượng đề tài/công bố NCKH theo cấp đề tài và trạng thái thực hiện |

`[Cần xác nhận]` Template ghi `Biễu mẫu 6H`; có thể là lỗi chính tả của `Biểu mẫu 6H`. Dòng kèm báo cáo ở `F5:M5` ghi `tháng 5 năm 2025`, trong khi bộ mẫu H đang xử lý theo năm 2026. Khi xuất báo cáo nên giữ nguyên template nếu đây là mẫu chính thức, nhưng cần xác nhận kỳ/năm báo cáo.

## 2. Mục đích nghiệp vụ

Báo cáo tổng hợp hoạt động nghiên cứu khoa học của cán bộ, giáo viên trong kỳ báo cáo, gồm:

- Số lượng đề tài đang nghiên cứu.
- Số lượng đề tài đăng ký trong năm.
- Số lượng đề tài được duyệt trong năm.
- Số lượng đề tài đã hoàn thành.
- Đánh giá/xếp loại đề tài: xuất sắc, đạt, quá hạn.
- Số lượng hội thảo/tọa đàm và bài báo/kỷ yếu khoa học.

`[Suy luận]` Đây là báo cáo cấp học viện/trường CAND theo năm học hoặc năm dương lịch. Template không có ô filter nên hệ thống cần truyền `maDonVi`, `namHocId` hoặc `tuNgay/denNgay` từ API/giao diện.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `B2:M2` | `Biễu mẫu 6H` | Merged |
| `B3:E3` | `BỘ CÔNG AN` | Merged |
| `F3:M4` | Tên báo cáo | Merged |
| `B4:E4` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `F5:M5` | Dòng kèm theo báo cáo | Merged |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `B7:B8` | `TT` | `stt` |
| `C7:E8` | `Cấp đề tài` | `rowLabel`, `rowCode`, `capDeTaiCode` |
| `F7:F8` | `Tổng số đề tài đang nghiên cứu` | `tongDangNghienCuu` |
| `G7:G8` | `Tổng số đề tài đăng ký trong năm` | `tongDangKyTrongNam` |
| `H7:H8` | `Tổng số đề tài được duyệt trong năm` | `tongDuocDuyetTrongNam` |
| `I7:I8` | `Đã hoàn thành` | `daHoanThanh` |
| `J7:L7` | `Đánh giá đề tài` | Nhóm `danhGiaDeTai` |
| `J8` | `Xuất sắc` | `xuatSac` |
| `K8` | `Đạt` | `dat` |
| `L8` | `Quá hạn` | `quaHan` |
| `M7:M8` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Nguồn/mapping đề xuất |
|---:|---:|---|---|---|
| 9 | 1 | Đề tài cấp cấp Nhà nước | `deTaiCapNhaNuoc` | `DE_TAI_NC_KHCN.CAP_DE_TAI_ID` map cấp Nhà nước `[Cần mapping danh mục]` |
| 10 | 2 | Đề tài cấp Bộ và tương đương | `deTaiCapBoTuongDuong` | `CAP_DE_TAI_ID` map cấp Bộ/tương đương |
| 11 | 3 | Đề tài cấp tỉnh | `deTaiCapTinh` | `CAP_DE_TAI_ID` map cấp tỉnh |
| 12 | 4 | Đề tài cấp cơ sở | `deTaiCapCoSo` | `CAP_DE_TAI_ID` map cấp cơ sở |
| 13 | 5 | Đề tài lý luận cấp Bộ | `deTaiLyLuanCapBo` | `CAP_DE_TAI_ID` cấp Bộ + `LOAI_DE_TAI_ID` hoặc nhóm loại đề tài lý luận `[Cần mapping danh mục]` |
| 14 | 6 | Đề tài lý luận cấp cơ sở | `deTaiLyLuanCapCoSo` | `CAP_DE_TAI_ID` cấp cơ sở + loại đề tài lý luận |
| 15 | 7 | Hội thảo, tọa đàm các cấp | `hoiThaoToaDamCacCap` | `[Cần xác nhận]` chưa thấy bảng sự kiện hội thảo/tọa đàm riêng trong domain `RES` |
| 16 | 8 | Bài báo đăng tạp chí, kỷ yếu hội thảo khoa học | `baiBaoTapChiKyYeu` | `BAI_BAO_KHCN_DA_CONG_BO`; có thể cộng thêm `SACH_BAO_TAP_CHI_NC_KHCN` nếu nghiệp vụ tính sách/tạp chí NCKH vào dòng này `[Cần xác nhận]` |

`[Cần xác nhận]` Dòng 9 ghi `Đề tài cấp cấp Nhà nước`, khả năng là lỗi lặp chữ `cấp`.

`[Cần xác nhận]` Dòng 16 không dùng cấu trúc số liệu F:M giống các dòng đề tài. Ô `F16:L16` được merge và chứa text: `Tổng số: ... bài. Trong đó: + Trong nước: ... bài + Quốc tế: ... bài`. Vì vậy API/template render cần xử lý dòng này như dòng mô tả tổng hợp riêng, không phải ma trận số theo từng cột.

## 5. Mapping cột giá trị

| Cột | Header | Field đề xuất | Quy tắc tính đề xuất |
|---|---|---|---|
| `F` | Tổng số đề tài đang nghiên cứu | `tongDangNghienCuu` | Count đề tài đã duyệt/đang hiệu lực, có `NGAY_BAT_DAU <= denNgay`, chưa có kết quả nghiệm thu hoàn thành trước/cuối kỳ |
| `G` | Tổng số đề tài đăng ký trong năm | `tongDangKyTrongNam` | Count đề tài có `NGAY_DE_XUAT` trong kỳ/năm |
| `H` | Tổng số đề tài được duyệt trong năm | `tongDuocDuyetTrongNam` | Count đề tài có `NGAY_QUYET_DINH` trong kỳ/năm; fallback `APPROVED_AT` nếu không có ngày quyết định `[Cần xác nhận]` |
| `I` | Đã hoàn thành | `daHoanThanh` | Count đề tài có `KET_QUA_NC_KHCN` đã duyệt, `NGAY_NGHIEM_THU` trong kỳ |
| `J` | Đánh giá đề tài - Xuất sắc | `xuatSac` | Count đề tài/kết quả có xếp loại `Xuất sắc` |
| `K` | Đánh giá đề tài - Đạt | `dat` | Count đề tài/kết quả có xếp loại `Đạt` |
| `L` | Đánh giá đề tài - Quá hạn | `quaHan` | Count đề tài quá `NGAY_KET_THUC` nhưng chưa có kết quả nghiệm thu; hoặc có trạng thái quá hạn nếu bổ sung |
| `M` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay theo dòng |

`[Cần xác nhận]` Hệ thống hiện có `DE_TAI_NC_KHCN.XEP_LOAI` và `KET_QUA_NC_KHCN.KET_QUA`. Cần chốt dùng trường nào làm nguồn chính cho `Xuất sắc/Đạt`; nếu `KET_QUA` chỉ là mô tả kết quả nghiệm thu thì nên chuẩn hóa thành danh mục xếp loại.

## 6. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.DE_TAI_NC_KHCN` / `/api/v1/res-de-tai` | Nguồn chính cho dòng 1-6 và trạng thái đang nghiên cứu/đăng ký/duyệt | `CAP_DE_TAI_ID`, `LOAI_DE_TAI_ID`, `NGAY_DE_XUAT`, `NGAY_QUYET_DINH`, `NGAY_BAT_DAU`, `NGAY_KET_THUC`, `XEP_LOAI`, `MA_DON_VI`, workflow fields |
| `X02_APP.KET_QUA_NC_KHCN` / `/api/v1/res-kq-de-tai` | Nguồn hoàn thành/nghiệm thu đề tài | `DE_TAI_KHCN_ID`, `KET_QUA`, `NGAY_NGHIEM_THU`, `MA_DON_VI`, workflow fields |
| `X02_APP.BAI_BAO_KHCN_DA_CONG_BO` / `/api/v1/res-bai-bao` | Nguồn dòng bài báo đăng tạp chí/kỷ yếu | `DE_TAI_KHCN_ID`, `TEN_BAI_BAO`, `LOAI_CONG_BO_ID`, `NGAY_CONG_BO`, `CAP_TAP_CHI_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.SACH_BAO_TAP_CHI_NC_KHCN` / `/api/v1/res-sach-bao` | Nguồn bổ sung nếu nghiệp vụ tính sách/tạp chí NCKH vào công trình công bố | `LOAI_TAI_LIEU_ID`, `NAM_XUAT_BAN`, `MA_DON_VI`, workflow fields |
| `X02_DM.DM_CAP_DE_TAI` | Mapping cấp đề tài | `ID`, `MA`, `TEN` |
| `X02_DM.DM_CAP_NCKH` | Mapping cấp NCKH thay thế nếu dữ liệu thực tế trỏ sang danh mục này | `ID`, `MA`, `TEN` |
| `X02_DM.DM_LOAI_DE_TAI` | Mapping đề tài lý luận/các loại đề tài khác | `ID`, `MA`, `TEN` |
| `X02_DM.DM_LOAI_CONG_BO` | Mapping bài báo trong nước/quốc tế/kỷ yếu hội thảo | `ID`, `MA`, `TEN` |
| `X02_DM.DM_CAP_TAP_CHI` | Mapping cấp tạp chí trong nước/quốc tế nếu dùng cấp tạp chí | `ID`, `MA`, `TEN` |

`[Cần xác nhận]` Chưa thấy bảng nghiệp vụ riêng cho `Hội thảo, tọa đàm các cấp`. Nếu hội thảo/tọa đàm đang được quản lý như một loại công bố trong `BAI_BAO_KHCN_DA_CONG_BO.LOAI_CONG_BO_ID`, cần xác nhận vì đó là bài/báo cáo hội thảo, không phải sự kiện hội thảo.

## 7. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | Áp dụng trên `MA_DON_VI`; mặc định theo quyền user |
| `namHocId` | String | Resolve sang khoảng ngày nếu báo cáo theo năm học |
| `namBaoCao` | Number | Dùng trực tiếp với `EXTRACT(YEAR FROM ...)` nếu báo cáo theo năm dương lịch |
| `tuNgay` | Date | Ngày bắt đầu kỳ; dùng cho `NGAY_DE_XUAT`, `NGAY_QUYET_DINH`, `NGAY_NGHIEM_THU`, `NGAY_CONG_BO` |
| `denNgay` | Date | Ngày kết thúc kỳ |
| `workflowStatus` | String | Mặc định `Approved` |
| `capDeTaiSource` | String | `DM_CAP_DE_TAI` hoặc `DM_CAP_NCKH` `[Cần xác nhận]` |

## 8. API report đề xuất

```http
GET /api/v1/reports/6h/so-lieu-nghien-cuu-khoa-hoc
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Không | Ưu tiên khi báo cáo theo năm học |
| `namBaoCao` | Không | Dùng khi báo cáo theo năm dương lịch |
| `tuNgay` | Không | Bắt buộc nếu không truyền `namHocId`/`namBaoCao` |
| `denNgay` | Không | Bắt buộc nếu không truyền `namHocId`/`namBaoCao` |
| `workflowStatus` | Không | Mặc định `Approved` |

Response đề xuất:

```json
{
  "reportCode": "6H",
  "title": "Thống kê số liệu nghiên cứu khoa học",
  "filters": {
    "maDonVi": "T01",
    "namBaoCao": 2026
  },
  "rows": [
    {
      "rowCode": "DE_TAI_CAP_NHA_NUOC",
      "stt": "1",
      "label": "Đề tài cấp Nhà nước",
      "tongDangNghienCuu": 0,
      "tongDangKyTrongNam": 0,
      "tongDuocDuyetTrongNam": 0,
      "daHoanThanh": 0,
      "xuatSac": 0,
      "dat": 0,
      "quaHan": 0,
      "ghiChu": ""
    }
  ],
  "publicationSummary": {
    "tongSoBai": 0,
    "trongNuoc": 0,
    "quocTe": 0
  },
  "dataQualityWarnings": [
    "MISSING_SEMINAR_EVENT_SOURCE"
  ]
}
```

## 9. SQL/Proc đề xuất

Skeleton Oracle cho dòng đề tài 1-6:

```sql
WITH params AS (
    SELECT :p_tu_ngay AS tu_ngay,
           :p_den_ngay AS den_ngay,
           :p_ma_don_vi AS ma_don_vi,
           NVL(:p_workflow_status, 'Approved') AS workflow_status
    FROM dual
),
row_def AS (
    SELECT 'DE_TAI_CAP_NHA_NUOC' row_code, '1' stt, 'Đề tài cấp Nhà nước' label, 1 sort_order FROM dual UNION ALL
    SELECT 'DE_TAI_CAP_BO_TUONG_DUONG', '2', 'Đề tài cấp Bộ và tương đương', 2 FROM dual UNION ALL
    SELECT 'DE_TAI_CAP_TINH', '3', 'Đề tài cấp tỉnh', 3 FROM dual UNION ALL
    SELECT 'DE_TAI_CAP_CO_SO', '4', 'Đề tài cấp cơ sở', 4 FROM dual UNION ALL
    SELECT 'DE_TAI_LY_LUAN_CAP_BO', '5', 'Đề tài lý luận cấp Bộ', 5 FROM dual UNION ALL
    SELECT 'DE_TAI_LY_LUAN_CAP_CO_SO', '6', 'Đề tài lý luận cấp cơ sở', 6 FROM dual
),
de_tai AS (
    SELECT dt.*
    FROM X02_APP.DE_TAI_NC_KHCN dt
    CROSS JOIN params p
    WHERE dt.IS_DELETED = 0
      AND dt.IS_ACTIVE = 1
      AND dt.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR dt.MA_DON_VI = p.ma_don_vi)
),
ket_qua AS (
    SELECT kq.DE_TAI_KHCN_ID,
           MAX(kq.NGAY_NGHIEM_THU) AS ngay_nghiem_thu,
           MAX(kq.KET_QUA) KEEP (DENSE_RANK LAST ORDER BY kq.NGAY_NGHIEM_THU) AS ket_qua
    FROM X02_APP.KET_QUA_NC_KHCN kq
    CROSS JOIN params p
    WHERE kq.IS_DELETED = 0
      AND kq.IS_ACTIVE = 1
      AND kq.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR kq.MA_DON_VI = p.ma_don_vi)
    GROUP BY kq.DE_TAI_KHCN_ID
),
mapped AS (
    SELECT
        rr.ROW_CODE,
        dt.ID,
        dt.NGAY_DE_XUAT,
        dt.NGAY_QUYET_DINH,
        dt.NGAY_BAT_DAU,
        dt.NGAY_KET_THUC,
        COALESCE(kq.KET_QUA, dt.XEP_LOAI) AS xep_loai,
        kq.NGAY_NGHIEM_THU
    FROM de_tai dt
    JOIN X02_APP.RPT_6H_CAP_DE_TAI_RULE rr
      ON rr.CAP_DE_TAI_ID = dt.CAP_DE_TAI_ID
     AND (rr.LOAI_DE_TAI_ID IS NULL OR rr.LOAI_DE_TAI_ID = dt.LOAI_DE_TAI_ID)
    LEFT JOIN ket_qua kq ON kq.DE_TAI_KHCN_ID = dt.ID
)
SELECT
    rd.STT,
    rd.LABEL,
    NVL(SUM(CASE
        WHEN m.NGAY_BAT_DAU <= :p_den_ngay
         AND (m.NGAY_NGHIEM_THU IS NULL OR m.NGAY_NGHIEM_THU > :p_den_ngay)
        THEN 1 ELSE 0 END), 0) AS TONG_DANG_NGHIEN_CUU,
    NVL(SUM(CASE WHEN m.NGAY_DE_XUAT BETWEEN :p_tu_ngay AND :p_den_ngay THEN 1 ELSE 0 END), 0) AS TONG_DANG_KY_TRONG_NAM,
    NVL(SUM(CASE WHEN m.NGAY_QUYET_DINH BETWEEN :p_tu_ngay AND :p_den_ngay THEN 1 ELSE 0 END), 0) AS TONG_DUOC_DUYET_TRONG_NAM,
    NVL(SUM(CASE WHEN m.NGAY_NGHIEM_THU BETWEEN :p_tu_ngay AND :p_den_ngay THEN 1 ELSE 0 END), 0) AS DA_HOAN_THANH,
    NVL(SUM(CASE WHEN UPPER(m.XEP_LOAI) IN ('XUAT SAC', 'XUẤT SẮC') THEN 1 ELSE 0 END), 0) AS XUAT_SAC,
    NVL(SUM(CASE WHEN UPPER(m.XEP_LOAI) IN ('DAT', 'ĐẠT') THEN 1 ELSE 0 END), 0) AS DAT,
    NVL(SUM(CASE WHEN m.NGAY_KET_THUC < :p_den_ngay AND m.NGAY_NGHIEM_THU IS NULL THEN 1 ELSE 0 END), 0) AS QUA_HAN
FROM row_def rd
LEFT JOIN mapped m ON m.ROW_CODE = rd.ROW_CODE
GROUP BY rd.SORT_ORDER, rd.STT, rd.LABEL
ORDER BY rd.SORT_ORDER;
```

`[Cần mapping danh mục]` `RPT_6H_CAP_DE_TAI_RULE` là bảng/view cấu hình đề xuất để tránh hardcode ID danh mục cấp đề tài và loại đề tài lý luận. Nếu nghiệp vụ chốt dùng `DM_CAP_NCKH` thay `DM_CAP_DE_TAI`, chỉ cần đổi cấu hình mapping thay vì sửa proc.

Skeleton cho dòng bài báo:

```sql
SELECT
    COUNT(*) AS TONG_SO_BAI,
    SUM(CASE WHEN lc.MA IN ('TRONG_NUOC', 'LCB_TRONG_NUOC') THEN 1 ELSE 0 END) AS TRONG_NUOC,
    SUM(CASE WHEN lc.MA IN ('QUOC_TE', 'LCB_QUOC_TE') THEN 1 ELSE 0 END) AS QUOC_TE
FROM X02_APP.BAI_BAO_KHCN_DA_CONG_BO bb
LEFT JOIN X02_DM.DM_LOAI_CONG_BO lc ON lc.ID = bb.LOAI_CONG_BO_ID
WHERE bb.IS_DELETED = 0
  AND bb.IS_ACTIVE = 1
  AND bb.WORKFLOW_STATUS = NVL(:p_workflow_status, 'Approved')
  AND (:p_ma_don_vi IS NULL OR bb.MA_DON_VI = :p_ma_don_vi)
  AND bb.NGAY_CONG_BO BETWEEN :p_tu_ngay AND :p_den_ngay;
```

`[Cần mapping danh mục]` Mã `TRONG_NUOC/QUOC_TE` trong skeleton chỉ là placeholder. Cần map theo `DM_LOAI_CONG_BO` hoặc `DM_CAP_TAP_CHI` thực tế.

## 10. Quy tắc đối soát

- Dòng 1-6 chỉ tính dữ liệu đề tài, không cộng bài báo/sách báo.
- `Đã hoàn thành` nên ưu tiên `KET_QUA_NC_KHCN.NGAY_NGHIEM_THU` và trạng thái duyệt của kết quả, không chỉ dựa trên `DE_TAI_NC_KHCN.WORKFLOW_STATUS`.
- `Quá hạn` phải loại trừ đề tài đã nghiệm thu trước hoặc trong kỳ.
- `Đang nghiên cứu` và `Đã hoàn thành` có thể không cộng thành tổng tất cả đề tài vì mỗi cột phản ánh trạng thái tại kỳ khác nhau.
- Dòng bài báo phải render đúng format text `Tổng số ... bài; trong nước ...; quốc tế ...`, không ép vào các cột `Xuất sắc/Đạt/Quá hạn`.

## 11. Gap/câu hỏi cần xác nhận

| Nhóm | Vấn đề | Đề xuất xử lý |
|---|---|---|
| Template | `Biễu mẫu 6H`, năm 2025, dòng 9 lặp chữ `cấp` | Xác nhận với đơn vị nghiệp vụ trước khi sửa template |
| Cấp đề tài | Có cả `DM_CAP_DE_TAI` và `DM_CAP_NCKH` | Chốt danh mục mà `DE_TAI_NC_KHCN.CAP_DE_TAI_ID` đang trỏ thực tế |
| Đề tài lý luận | Chưa rõ map bằng `LOAI_DE_TAI_ID`, `LOAI_NCKH` hay keyword | Cần cấu hình danh mục cho dòng 5-6 |
| Đánh giá đề tài | Có `DE_TAI_NC_KHCN.XEP_LOAI` và `KET_QUA_NC_KHCN.KET_QUA` | Chốt field nguồn cho `Xuất sắc/Đạt` |
| Hội thảo/tọa đàm | Chưa thấy bảng sự kiện hội thảo/tọa đàm | Bổ sung nguồn hoặc xác nhận không tự động hóa dòng 15 |
| Bài báo trong nước/quốc tế | Cần map theo `DM_LOAI_CONG_BO` hoặc `DM_CAP_TAP_CHI` | Tạo cấu hình mapping danh mục để tránh phụ thuộc text |

## 12. Tài liệu/code tham chiếu

- `docs/report-input/6H.xlsx`
- `src/frontend/frontend-x02-v2/src/shared/config/screenApiCatalog.csv`
- `docs/dashboard/nghien-cuu.md`
- `docs/figma/business-screens-fields/DT-qldtkhcn.md`
- `docs/figma/business-screens-fields/DT-qlkqnckhcn.md`
- `docs/figma/business-screens-fields/DT-qlbbkhdcb.md`
- `docs/figma/business-screens-fields/DT-qlsbtc.md`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/res/resdetai/entity/DeTaiNcKhcn.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/res/reskqdetai/entity/KetQuaNcKhcn.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/res/resbaibao/entity/BaiBao.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/res/ressachbao/entity/SachBao.java`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

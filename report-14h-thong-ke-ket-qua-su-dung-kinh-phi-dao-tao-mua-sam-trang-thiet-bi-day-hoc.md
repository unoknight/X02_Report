# Báo cáo 14H - Thống kê kết quả sử dụng kinh phí đào tạo, mua sắm trang thiết bị dạy học

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/14H.xlsx` |
| Sheet | `Kinh phi` |
| Mã biểu mẫu | `Biểu mẫu 14H` |
| Tên báo cáo | `THỐNG KÊ KẾT QUẢ SỬ DỤNG KINH PHÍ ĐÀO TẠO, MUA SẮM TRANG THIẾT BỊ DẠY HỌC` |
| Vùng dữ liệu có giá trị | `B2:G18` |
| Vùng style kéo dài | `A1:H38` |
| Công thức Excel | Không có công thức |
| Đơn vị tính | Triệu đồng |
| Dạng báo cáo | Bảng tổng hợp kinh phí được duyệt, kinh phí đã sử dụng theo hạng mục chi |

`[Cần xác nhận]` Template 14H cần số tiền được duyệt/đã sử dụng, nhưng trong schema hiện hành `docs/database/X02_APP.sql` chưa thấy bảng ngân sách/chi phí đào tạo đủ các trường hạng mục, số được duyệt, số đã sử dụng, số bổ sung. Có bảng legacy `KINH_PHI_DAO_TAO` trong `src/backend/qldt-v2/src/main/resources/app.sql`, nhưng chưa thấy trong DDL hiện hành, nên không nên coi là nguồn chính thức nếu chưa xác nhận.

## 2. Mục đích nghiệp vụ

Báo cáo phục vụ tổng hợp kết quả sử dụng kinh phí đào tạo và mua sắm trang thiết bị dạy học trong năm/kỳ báo cáo:

- Theo dõi kinh phí được duyệt và kinh phí đã sử dụng cho từng hạng mục.
- Tổng hợp kinh phí được duyệt trong năm, kinh phí bổ sung trong năm, tổng kinh phí đã sử dụng.
- Tính chênh lệch so với tổng kinh phí được duyệt và kinh phí bổ sung.

`[Suy luận]` Đây là báo cáo tài chính/quản trị nội bộ, nên nguồn chuẩn nên là bảng fact kinh phí đã được duyệt hoặc import từ hệ thống tài chính, không nên suy ra số tiền từ các bảng nghiệp vụ như giáo trình, thỉnh giảng, thiết bị nếu các bảng đó không lưu giá trị tiền.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `B2:H2` | `Biểu mẫu 14H` | Merged |
| `B3:C3` | `BỘ CÔNG AN` | Merged |
| `D3:H4` | Tên báo cáo | Merged |
| `B4:C4` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `D5:H5` | `(Kèm theo Báo cáo số... ngày... tháng... năm 202..)` | Merged |
| `F6:H6` | `Đơn vị tính: Triệu đồng` | Merged |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `B7:B8` | `STT` | `stt` |
| `C7:D8` | `Các hạng mục sử dụng kinh phí` | `hangMuc`, `rowCode` |
| `E7:E8` | `Kinh phí được duyệt` | `kinhPhiDuocDuyet` |
| `F7:F8` | `Kinh phí đã sử dụng` | `kinhPhiDaSuDung` |
| `G7:H8` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 9 | 1 | Biên soạn, dịch, in ấn tài liệu, sách giáo khoa, phim ảnh | `bienSoanDichInAnTaiLieu` | Hạng mục kinh phí; đối soát phụ với `GIAO_TRINH_TAI_LIEU`, `TL_GIANG_DAY` |
| 10 | 2 | Thanh toán vượt giờ, mời giảng, chế độ giáo viên | `vuotGioMoiGiangCheDoGiaoVien` | Hạng mục kinh phí; đối soát phụ với `KET_QUA_GIANG_DAY`, `THINH_GIANG`, `HOAT_DONG_THINH_GIANG` |
| 11 | 3 | Thực tập, nghiên cứu khoa học, tham quan của học sinh | `thucTapNckhThamQuanHocSinh` | Hạng mục kinh phí; đối soát phụ với RES và hoạt động học viên nếu có |
| 12 | 4 | Hợp đồng liên kết đào tạo | `hopDongLienKetDaoTao` | Hạng mục kinh phí; cần nguồn hợp đồng/liên kết đào tạo `[Cần xác nhận]` |
| 13 | 5 | Đào tạo, bồi dưỡng cán bộ, giáo viên, đổi mới phương pháp dạy học | `daoTaoBoiDuongGvDoiMoiPpdh` | Hạng mục kinh phí; đối soát phụ với `DAO_TAO_BOI_DUONG`, quá trình bồi dưỡng cán bộ giáo viên |
| 14 | 6 | Đào tạo sau đại học, bồi dưỡng chức danh các cấp | `daoTaoSauDaiHocBoiDuongChucDanh` | Hạng mục kinh phí; đối soát phụ với `QUA_TRINH_BOI_DUONG_CHUC_DANH` |
| 15 |  | Tổng kinh phí được duyệt trong năm | `tongKinhPhiDuocDuyetTrongNam` | Tổng ngân sách được duyệt theo năm/kỳ báo cáo |
| 16 |  | Tổng kinh phí được bổ sung trong năm | `tongKinhPhiBoSungTrongNam` | Tổng bổ sung ngân sách trong năm/kỳ báo cáo |
| 17 |  | Tổng kinh phí đã sử dụng | `tongKinhPhiDaSuDung` | Tổng cột kinh phí đã sử dụng theo hạng mục hoặc theo fact tổng |
| 18 |  | Chênh lệch so với tổng kinh phí và kinh phí được bổ sung | `chenhLech` | `(Tổng được duyệt + Tổng bổ sung) - Tổng đã sử dụng` |

`[Cần xác nhận]` Dòng 11 ghi `học sinh`, trong khi nhiều mẫu H dùng `học viên`. Cần xác nhận template muốn bao gồm học sinh Trường Văn hóa, học viên nói chung, hay cả hai nhóm.

## 5. Mapping cột giá trị

| Cột | Header Excel | Field đề xuất | Mapping DB/API đề xuất |
|---|---|---|---|
| `E` | Kinh phí được duyệt | `kinhPhiDuocDuyet` | Số tiền được duyệt theo hạng mục, đơn vị triệu đồng |
| `F` | Kinh phí đã sử dụng | `kinhPhiDaSuDung` | Số tiền đã sử dụng/đã quyết toán theo hạng mục, đơn vị triệu đồng |
| `G:H` | Ghi chú | `ghiChu` | Ghi chú hạng mục, nguồn kinh phí, lý do chênh lệch |

`[Cần xác nhận]` Nếu nguồn lưu bằng đồng Việt Nam, API/export phải chia `1,000,000` và làm tròn theo quy định trước khi ghi vào Excel.

## 6. Công thức Excel trong template

Template không có công thức.

Các công thức nên tính ở API/procedure hoặc bổ sung vào file export:

| Chỉ tiêu | Công thức đề xuất | Ghi chú |
|---|---|---|
| `tongKinhPhiDaSuDung` | `SUM(kinhPhiDaSuDung rows 9-14)` | Nếu dòng 17 không nhập tay |
| `chenhLech` | `tongKinhPhiDuocDuyetTrongNam + tongKinhPhiBoSungTrongNam - tongKinhPhiDaSuDung` | Dương là còn dư, âm là vượt dự toán |
| Tỷ lệ sử dụng `[Suy luận]` | `tongKinhPhiDaSuDung / NULLIF(tongKinhPhiDuocDuyetTrongNam + tongKinhPhiBoSungTrongNam, 0)` | Không có cột trong template, chỉ dùng kiểm tra nội bộ |

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `KINH_PHI_DAO_TAO` `[Cần xác nhận schema]` | Bảng legacy gần nhất với nghiệp vụ kinh phí đào tạo | `KE_HOACH_KINH_PHI_ID`, `NGAY_DAO_TAO`, `KINH_PHI_DUOC_CAP`, `KET_QUA_SU_DUNG`, `BAO_CAO_KET_QUA_SD`, `MA_DON_VI`, workflow cũ |
| `X02_APP.THIET_BI` / `/api/v1/csvc-thiet-bi` | Nguồn nghiệp vụ thiết bị dạy học để đối soát số lượng, không đủ số tiền mua sắm | `LOAI_THIET_BI_ID`, `SO_LUONG`, `TINH_TRANG`, `MA_DON_VI`, workflow fields |
| `X02_DM.DM_LOAI_THIET_BI` | Mapping loại thiết bị dạy học | `ID`, `MA`, `TEN` |
| `X02_APP.GIAO_TRINH_TAI_LIEU` / `/api/v1/giao-trinh` | Đối soát hạng mục biên soạn/in ấn tài liệu | `TEN_GIAO_TRINH`, `LOAI_TAI_LIEU_ID`, `TRINH_DO_DAO_TAO_ID`, `QUYET_DINH_BAN_HANH_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.TL_GIANG_DAY` / `/api/v1/pln-tai-lieu` | Đối soát tài liệu/giáo trình dạy học phía kế hoạch giảng dạy | `TEN_GIAO_TRINH`, `TEN_TAC_GIA`, `MON_HOC`, `NGAY_QUYET_DINH`, `MA_DON_VI`, workflow fields |
| `X02_APP.KET_QUA_GIANG_DAY` | Đối soát vượt giờ giảng | `CAN_BO_ID`, `SO_GIO_NGHIA_VU`, `SO_GIO_THUC_HIEN`, `NAM_HOC_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.THINH_GIANG`, `X02_APP.HOAT_DONG_THINH_GIANG` | Đối soát mời giảng/thỉnh giảng | `THINH_GIANG_ID`, thông tin nhà giáo thỉnh giảng, hoạt động thỉnh giảng |
| `X02_APP.DAO_TAO_BOI_DUONG` | Đối soát chương trình đào tạo, bồi dưỡng | `TEN_CHUONG_TRINH`, `HINH_THUC_DAO_TAO_ID`, `TRINH_DO_DAO_TAO_ID`, `MA_DON_VI`, workflow fields |
| `X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH` | Đối soát bồi dưỡng chức danh cán bộ giáo viên | `CAN_BO_NHA_GIAO_ID`, `TRINH_DO_DAO_TAO_ID`, `THOI_GIAN_DAO_TAO`, `THOI_GIAN_AP_DUNG`, `MA_DON_VI`, workflow fields |
| `X02_APP.DE_TAI_NC_KHCN`, `CHUONG_TRINH_NC_KHCN`, `DU_AN_NC_KHCN` | Đối soát kinh phí nghiên cứu khoa học nếu hạng mục 3 bao gồm NCKH | `TONG_KINH_PHI`, `KINH_PHI`, `NGUON_KINH_PHI`, `MA_DON_VI`, workflow fields |

`[Cần xác nhận]` Các bảng đối soát kể trên không thay thế bảng tài chính vì phần lớn chỉ lưu hoạt động/số lượng, không lưu kinh phí được duyệt và kinh phí đã sử dụng theo hạng mục.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | Mã trường/đơn vị báo cáo |
| `namBaoCao` | Number | Năm báo cáo trên template |
| `namHocId` | String | Dùng cho nguồn đào tạo/giảng dạy nếu báo cáo theo năm học |
| `tuNgay`, `denNgay` | Date | Khoảng ngày duyệt/chi/ghi nhận sử dụng kinh phí |
| `nguonKinhPhiId` | String | Ngân sách thường xuyên, bổ sung, dự án, xã hội hóa... `[Cần mapping danh mục]` |
| `hangMucIds` | String[] | 6 hạng mục dòng 9-14 |
| `workflowStatus` | String | Mặc định `Approved`/`APPROVED` |

## 9. API báo cáo đề xuất

### Endpoint

`GET /api/v1/reports/14h/ket-qua-su-dung-kinh-phi-dao-tao-thiet-bi-day-hoc`

### Request params

```json
{
  "maDonVi": "G01.652",
  "namBaoCao": 2026,
  "tuNgay": "2026-01-01",
  "denNgay": "2026-12-31",
  "workflowStatus": "Approved",
  "donViTinh": "TRIEU_DONG"
}
```

### Response DTO đề xuất

```json
{
  "reportCode": "14H",
  "title": "Thống kê kết quả sử dụng kinh phí đào tạo, mua sắm trang thiết bị dạy học",
  "unit": "Triệu đồng",
  "rows": [
    {
      "rowCode": "bienSoanDichInAnTaiLieu",
      "stt": 1,
      "label": "Biên soạn, dịch, in ấn tài liệu, sách giáo khoa, phim ảnh",
      "kinhPhiDuocDuyet": 0,
      "kinhPhiDaSuDung": 0,
      "ghiChu": null
    }
  ],
  "summary": {
    "tongKinhPhiDuocDuyetTrongNam": 0,
    "tongKinhPhiBoSungTrongNam": 0,
    "tongKinhPhiDaSuDung": 0,
    "chenhLech": 0
  }
}
```

## 10. SQL/Procedure đề xuất

### 10.1. Bảng fact kinh phí nên bổ sung

`[Suy luận]` Để triển khai báo cáo đúng nghiệp vụ, nên có bảng/vùng dữ liệu chuẩn thay vì lấy số tiền bằng rule text:

| Bảng đề xuất | Vai trò |
|---|---|
| `RPT_14H_HANG_MUC` | Danh mục 6 hạng mục, thứ tự dòng, nhãn export |
| `KINH_PHI_DAO_TAO_CHI_TIET` hoặc `RPT_KINH_PHI_DAO_TAO` | Fact kinh phí theo đơn vị, năm, hạng mục, nguồn kinh phí |
| `KINH_PHI_DAO_TAO_DIEU_CHINH` | Phát sinh bổ sung/điều chỉnh trong năm |

Các field tối thiểu:

| Field | Ý nghĩa |
|---|---|
| `MA_DON_VI` | Đơn vị báo cáo |
| `NAM_BAO_CAO` hoặc `NAM_HOC_ID` | Kỳ báo cáo |
| `HANG_MUC_CODE` | Mapping 6 dòng hạng mục |
| `KINH_PHI_DUOC_DUYET` | Số được duyệt |
| `KINH_PHI_BO_SUNG` | Số bổ sung |
| `KINH_PHI_DA_SU_DUNG` | Số đã sử dụng/quyết toán |
| `DON_VI_TIEN` | VND/triệu đồng |
| `NGAY_DUYET`, `NGAY_SU_DUNG`, `SO_QUYET_DINH` | Trace chứng từ |
| `WORKFLOW_STATUS`, `IS_DELETED`, `IS_ACTIVE` | Kiểm soát duyệt dữ liệu |

### 10.2. SQL skeleton theo bảng fact đề xuất

```sql
WITH params AS (
    SELECT :ma_don_vi AS ma_don_vi,
           :nam_bao_cao AS nam_bao_cao,
           :tu_ngay AS tu_ngay,
           :den_ngay AS den_ngay,
           NVL(:workflow_status, 'Approved') AS workflow_status
    FROM dual
),
row_def AS (
    SELECT row_code, stt, label, display_order
    FROM X02_APP.RPT_14H_HANG_MUC
    WHERE is_active = 1
),
base AS (
    SELECT kp.hang_muc_code AS row_code,
           SUM(NVL(kp.kinh_phi_duoc_duyet, 0)) AS kinh_phi_duoc_duyet,
           SUM(NVL(kp.kinh_phi_bo_sung, 0)) AS kinh_phi_bo_sung,
           SUM(NVL(kp.kinh_phi_da_su_dung, 0)) AS kinh_phi_da_su_dung
    FROM X02_APP.RPT_KINH_PHI_DAO_TAO kp
    CROSS JOIN params p
    WHERE kp.is_deleted = 0
      AND kp.is_active = 1
      AND kp.workflow_status = p.workflow_status
      AND (p.ma_don_vi IS NULL OR kp.ma_don_vi = p.ma_don_vi)
      AND (p.nam_bao_cao IS NULL OR kp.nam_bao_cao = p.nam_bao_cao)
      AND (p.tu_ngay IS NULL OR TRUNC(kp.ngay_su_dung) >= p.tu_ngay)
      AND (p.den_ngay IS NULL OR TRUNC(kp.ngay_su_dung) <= p.den_ngay)
    GROUP BY kp.hang_muc_code
),
detail_rows AS (
    SELECT rd.stt,
           rd.row_code,
           rd.label,
           NVL(b.kinh_phi_duoc_duyet, 0) / 1000000 AS kinh_phi_duoc_duyet,
           NVL(b.kinh_phi_da_su_dung, 0) / 1000000 AS kinh_phi_da_su_dung,
           CAST(NULL AS VARCHAR2(1000)) AS ghi_chu,
           rd.display_order
    FROM row_def rd
    LEFT JOIN base b
      ON b.row_code = rd.row_code
),
summary AS (
    SELECT SUM(kinh_phi_duoc_duyet) AS tong_duyet,
           SUM(kinh_phi_bo_sung) AS tong_bo_sung,
           SUM(kinh_phi_da_su_dung) AS tong_su_dung
    FROM base
)
SELECT stt, label, kinh_phi_duoc_duyet, kinh_phi_da_su_dung, ghi_chu, display_order
FROM detail_rows
UNION ALL
SELECT NULL, 'Tổng kinh phí được duyệt trong năm', tong_duyet / 1000000, NULL, NULL, 90 FROM summary
UNION ALL
SELECT NULL, 'Tổng kinh phí được bổ sung trong năm', tong_bo_sung / 1000000, NULL, NULL, 91 FROM summary
UNION ALL
SELECT NULL, 'Tổng kinh phí đã sử dụng', NULL, tong_su_dung / 1000000, NULL, 92 FROM summary
UNION ALL
SELECT NULL, 'Chênh lệch so với tổng kinh phí và kinh phí được bổ sung',
       (tong_duyet + tong_bo_sung - tong_su_dung) / 1000000,
       NULL,
       NULL,
       93
FROM summary
ORDER BY display_order;
```

### 10.3. Fallback nếu chỉ dùng bảng legacy `KINH_PHI_DAO_TAO`

```sql
SELECT SUM(NVL(kp.kinh_phi_duoc_cap, 0)) AS kinh_phi_duoc_duyet
FROM KINH_PHI_DAO_TAO kp
WHERE kp.deleted = 0
  AND (:ma_don_vi IS NULL OR kp.ma_don_vi = :ma_don_vi)
  AND (:tu_ngay IS NULL OR kp.ngay_dao_tao >= :tu_ngay)
  AND (:den_ngay IS NULL OR kp.ngay_dao_tao <= :den_ngay);
```

`[Cần xác nhận]` Fallback này chỉ lấy được số được cấp, chưa có hạng mục chuẩn, kinh phí đã sử dụng dạng số, kinh phí bổ sung và chênh lệch. Không đủ để xuất 14H đầy đủ nếu không bổ sung rule/bảng chi tiết.

## 11. Quy tắc đối soát

| Quy tắc | Mục tiêu |
|---|---|
| Tổng dòng 17 bằng tổng `kinhPhiDaSuDung` các dòng 9-14 | Phát hiện thiếu hoặc trùng hạng mục chi |
| Dòng 18 bằng dòng 15 + dòng 16 - dòng 17 | Chốt công thức chênh lệch thống nhất |
| Số tiền export đúng đơn vị triệu đồng | Tránh lệch 1,000,000 lần giữa DB và Excel |
| Chỉ lấy chứng từ/bản ghi đã duyệt | Không đưa dữ liệu nháp vào báo cáo chính thức |
| Mỗi khoản chi chỉ thuộc một hạng mục 14H | Tránh double-count giữa đào tạo, NCKH, thiết bị |
| Hạng mục đối soát bằng số lượng nghiệp vụ không được tự suy ra thành tiền | Tránh biến count thiết bị/giáo trình thành kinh phí khi chưa có đơn giá/chứng từ |

## 12. Gap và câu hỏi cần xác nhận

| Vấn đề | Mức độ | Ghi chú |
|---|---|---|
| Chưa thấy bảng tài chính hiện hành đủ field cho 14H | Cao | Cần xác nhận nguồn ngân sách/chi phí chính thức hoặc bổ sung bảng fact |
| `KINH_PHI_DAO_TAO` chỉ thấy trong `app.sql` legacy | Cao | Cần xác nhận có migrate sang `X02_APP` hay không |
| Thiếu số `kinh phí đã sử dụng` dạng numeric | Cao | Legacy có `KET_QUA_SU_DUNG` text, không đủ aggregate |
| Thiếu field hạng mục chi chuẩn | Cao | Cần danh mục 6 hạng mục hoặc rule mapping từ chứng từ |
| Dòng tổng không có công thức Excel | Trung bình | API/export phải tính thay template |
| Mua sắm trang thiết bị dạy học có bảng thiết bị nhưng không có giá trị tiền | Trung bình | `THIET_BI` chỉ đủ đối soát số lượng/loại thiết bị |
| Dòng 11 dùng từ `học sinh` | Thấp | Cần chốt phạm vi học sinh/học viên |

## 13. Tham chiếu đã đối chiếu

- `docs/report-input/14H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/co-so-vat-chat.md`
- `docs/dashboard/ke-hoach.md`
- `docs/dashboard/canbo-dashboard.md`
- `docs/dashboard/nghien-cuu.md`
- `docs/report-output/report-5h-thong-ke-ket-qua-bien-soan-chuong-trinh-giao-duc-giao-trinh-tai-lieu-day-hoc.md`
- `src/backend/qldt-v2/src/main/resources/app.sql`

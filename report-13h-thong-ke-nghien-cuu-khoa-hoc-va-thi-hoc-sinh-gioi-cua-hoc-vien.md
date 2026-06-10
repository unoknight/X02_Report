# Báo cáo 13H - Thống kê số liệu về nghiên cứu khoa học và thi học sinh giỏi của học viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/13H.xlsx` |
| Sheet | `NCKH Hoc vien` |
| Mã biểu mẫu | `Biểu mẫu 13H` |
| Tên báo cáo | `THỐNG KÊ SỐ LIỆU VỀ NGHIÊN CỨU KHOA HỌC VÀ THI HỌC SINH GIỎI CỦA HỌC VIÊN` |
| Vùng dữ liệu có giá trị | `A1:I29` |
| Vùng style kéo dài | `A1:L51` |
| Công thức Excel | Không có công thức |
| Dạng báo cáo | Bảng thống kê số học viên/nhóm học viên dự thi và số giải đạt được theo nhóm cuộc thi/cấp thi |

`[Suy luận]` Template 13H là báo cáo người học nhưng giao nhau với nghiệp vụ nghiên cứu khoa học. Nguồn hiện hành có thể lấy từ khen thưởng học viên (`HV_KHEN_THUONG`) và danh mục giải thưởng; riêng bảng cuộc thi chuyên biệt `CUOC_THI_HOC_VIEN`, `KET_QUA_THI_HOC_VIEN` đang thấy trong `src/backend/qldt-v2/src/main/resources/app.sql`, chưa thấy trong DDL `docs/database/X02_APP.sql`, nên cần xác nhận trước khi coi là nguồn chính thức.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê kết quả học viên tham gia:

- Giải thi học viên tham gia nghiên cứu khoa học.
- Giải thi học sinh giỏi.
- Các cuộc thi khác theo danh sách cụ thể trong mẫu.

Mỗi dòng thống kê tổng số học viên/nhóm học viên dự thi và số giải theo bốn mức: Giải Nhất, Giải Nhì, Giải Ba, Giải Khuyến khích.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:I1` | `Biểu mẫu 13H` | Merged |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:I3` | Tên báo cáo | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `C4:I4` | `(Kèm theo Báo cáo số ngày tháng năm 2026)` | Merged |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A7:A8` | `STT` | `stt` |
| `B7:C8` | `Tham gia cuộc thi` | `nhomCuocThi`, `capThi`, `tenCuocThi`, `rowCode` |
| `D7:D8` | `Tổng số học viên/nhóm học viên dự thi` | `tongDuThi` |
| `E7:H7` | `Đạt giải` | Nhóm cột giải thưởng |
| `E8` | `Giải Nhất` | `giaiNhat` |
| `F8` | `Giải Nhì` | `giaiNhi` |
| `G8` | `Giải Ba` | `giaiBa` |
| `H8` | `Giải Khuyến khích` | `giaiKhuyenKhich` |
| `I7:I8` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 9 | 1 | Giải thi học viên tham gia nghiên cứu khoa học | `nckh` | Dòng nhóm, không nhập số liệu nếu chỉ tổng hợp dòng con |
| 10 |  | Cấp trường | `nckhCapTruong` | Cuộc thi/giải NCKH, cấp trường |
| 11 |  | Cấp Bộ Công an | `nckhCapBoCongAn` | Cuộc thi/giải NCKH, cấp Bộ Công an |
| 12 |  | Cấp Bộ Giáo dục & Đào tạo | `nckhCapBoGddt` | Cuộc thi/giải NCKH, cấp Bộ Giáo dục và Đào tạo |
| 13 | 2 | Giải thi học sinh giỏi | `hsg` | Dòng nhóm, không nhập số liệu nếu chỉ tổng hợp dòng con |
| 14 |  | Cấp Quốc tế | `hsgCapQuocTe` | Thi học sinh giỏi, cấp quốc tế |
| 15 |  | Cấp Quốc gia | `hsgCapQuocGia` | Thi học sinh giỏi, cấp quốc gia |
| 16 |  | Cấp Bộ | `hsgCapBo` | Thi học sinh giỏi, cấp Bộ |
| 17 |  | Cấp Sở Giáo dục và Đào tạo (dành cho học sinh Trường Văn hóa) | `hsgCapSoGddt` | Thi học sinh giỏi, cấp Sở GDĐT |
| 18 |  | Cấp trường | `hsgCapTruong` | Thi học sinh giỏi, cấp trường |
| 19 | 3 | Các cuộc thi khác | `cuocThiKhac` | Dòng nhóm, không nhập số liệu nếu chỉ tổng hợp dòng con |
| 20 |  | Giải thưởng Nữ sinh khoa học công nghệ Việt Nam năm 2024 | `nuSinhKhcnVn2024` | Match tên cuộc thi/giải thưởng |
| 21 |  | Cuộc thi tìm hiểu 80 năm truyền thống QĐND Việt Nam | `timHieu80NamQdnd` | Match tên cuộc thi |
| 22 |  | Cuộc thi Olympic tiếng Anh sinh viên toàn quốc | `olympicTiengAnhSv` | Match tên cuộc thi |
| 23 |  | Cuộc thi viết chính luận bảo vệ nền tảng tư tưởng của Đảng | `vietChinhLuanBaoVeNenTangDang` | Match tên cuộc thi |
| 24 |  | Cuộc thi Sinh viên với ATTT | `sinhVienVoiAttt` | Match tên cuộc thi |
| 25 |  | Cuộc thi tìm hiểu Luật Căn cước trong CAND | `timHieuLuatCanCuocCand` | Match tên cuộc thi |
| 26 |  | Cuộc thi tìm hiểu 40 năm thắng lợi kế hoạch phản gián CM12 | `timHieu40NamCm12` | Match tên cuộc thi |
| 27 |  | Cuộc thi chạy báo Hà Nội mới | `chayBaoHaNoiMoi` | Match tên cuộc thi |
| 28 |  | Hội thi điều lệnh, võ thuật CAND khối học viên năm học 2024-2025 | `hoiThiDieuLenhVoThuatCand` | Match tên hội thi |
| 29 |  | Cuộc thi tìm hiểu về môi trường trong CAND | `timHieuMoiTruongCand` | Match tên cuộc thi |

`[Cần xác nhận]` Các dòng 20-29 là danh sách cố định trong template năm 2026, có một số tên gắn năm cụ thể như `năm 2024`, `năm học 2024-2025`. Nếu báo cáo dùng lâu dài, nên cấu hình danh sách dòng theo năm báo cáo thay vì hard-code trong SQL.

## 5. Mapping cột giá trị

| Cột | Header Excel | Field đề xuất | Mapping DB/API đề xuất |
|---|---|---|---|
| `D` | Tổng số học viên/nhóm học viên dự thi | `tongDuThi` | Count số học viên tham gia hoặc sum `SO_LUONG_HOC_VIEN` nếu dùng nguồn nhóm |
| `E` | Giải Nhất | `giaiNhat` | Count giải có `DM_GIAI_THUONG.TEN`/`MA` tương ứng Giải Nhất |
| `F` | Giải Nhì | `giaiNhi` | Count giải có `DM_GIAI_THUONG.TEN`/`MA` tương ứng Giải Nhì |
| `G` | Giải Ba | `giaiBa` | Count giải có `DM_GIAI_THUONG.TEN`/`MA` tương ứng Giải Ba |
| `H` | Giải Khuyến khích | `giaiKhuyenKhich` | Count giải có `DM_GIAI_THUONG.TEN`/`MA` tương ứng Giải Khuyến khích |
| `I` | Ghi chú | `ghiChu` | Text tổng hợp hoặc nhập tay |

`[Cần xác nhận]` Header `Tổng số học viên/nhóm học viên dự thi` cho phép hai đơn vị đếm khác nhau. Nếu cuộc thi theo đội/nhóm thì cần nguồn có `SO_LUONG_HOC_VIEN`; nếu chỉ lưu `HV_KHEN_THUONG.HOC_VIEN_ID`, báo cáo chỉ đếm được cá nhân hoặc số bản ghi giải.

## 6. Công thức Excel trong template

Template không có công thức.

| Vùng | Nhận xét |
|---|---|
| Dòng nhóm 9, 13, 19 | Không có công thức tổng từ dòng con. Khi export có thể để trống như template hoặc tính tổng theo rule nghiệp vụ. |
| Cột giải `E:H` | Không có kiểm tra chéo với `D`. API/procedure nên tự validate để tránh số giải lớn hơn tổng dự thi khi đơn vị đếm là cá nhân. |

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HV_KHEN_THUONG` / `/api/v1/khen-thuong-nguoi-hoc` | Nguồn hiện hành khả thi cho giải thưởng/cuộc thi của học viên | `HOC_VIEN_ID`, `CAP_KHEN_THUONG_ID`, `LINH_VUC_KHEN_THUONG_ID`, `HINH_THUC_KHEN_THUONG_ID`, `GIAI_THUONG_ID`, `NAM_KHEN_THUONG_ID`, `LY_DO_KHEN_THUONG`, `MA_DON_VI`, workflow fields |
| `X02_APP.HOC_VIEN` | Join đối tượng học viên, đơn vị, khóa/ngành nếu cần lọc | `ID`, `MA_DON_VI`, `TRINH_DO_DAO_TAO_ID`, `NGANH_ID`, `KHOA_HOC_ID`, `TRUNG_DOI_ID`, `TRANG_THAI_HOC_ID` |
| `X02_DM.DM_GIAI_THUONG` / `/api/v1/dm/giai-thuong` | Mapping cột giải Nhất/Nhì/Ba/Khuyến khích | `ID`, `MA`, `TEN`, `LOAI_GIAI_THUONG`, `DOI_TUONG_SD` |
| `X02_DM.DM_CAP_KHEN_THUONG` | Mapping cấp thi/giải | `ID`, `MA`, `TEN`, `INDEX_ORDER` |
| `X02_DM.DM_LINH_VUC_KHEN_THUONG` | Phân loại lĩnh vực NCKH, học sinh giỏi, phong trào/cuộc thi khác | `ID`, `MA`, `TEN` |
| `X02_DM.DM_HINH_THUC_KHEN_THUONG` | Phân loại hình thức khen thưởng/giải thưởng nếu có | `ID`, `MA`, `TEN` |
| `X02_APP.GIAI_THUONG_NC_KHCN` / `/api/v1/res-giai-thuong` | Nguồn giải thưởng nghiên cứu khoa học trong phân hệ RES | `DE_TAI_KHCN_ID`, `TEN_TAC_GIA`, `TEN_GIAI_THUONG`, `CAP_GIAI_THUONG_ID`, `DON_VI_TRAO_GIAI`, `NGAY_TRAO_GIAI`, `KET_QUA`, `MA_DON_VI`, workflow fields |
| `CUOC_THI_HOC_VIEN`, `KET_QUA_THI_HOC_VIEN` `[Cần xác nhận schema]` | Nguồn phù hợp nhất nếu được đưa vào schema hiện hành | `PHAN_LOAI`, `CAP_QUAN_LY_ID`, `NAM_HOC`, `CUOC_THI_ID`, `TEN_DOAN_HOC_VIEN`, `SO_LUONG_HOC_VIEN`, `GIAI_THUONG` |

`[Cần xác nhận]` `GIAI_THUONG_NC_KHCN.TEN_TAC_GIA` là text, không liên kết trực tiếp `HOC_VIEN_ID`; không nên dùng để đếm số học viên tham gia nếu chưa có quy tắc chuẩn hóa/tách tác giả hoặc bảng liên kết tác giả - học viên.

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `HV_KHEN_THUONG.MA_DON_VI`, `GIAI_THUONG_NC_KHCN.MA_DON_VI` hoặc qua `HOC_VIEN.MA_DON_VI`; mặc định theo quyền user |
| `namHocId` | String | `HV_KHEN_THUONG.NAM_KHEN_THUONG_ID`; nếu dùng bảng cuộc thi thì map `CUOC_THI_HOC_VIEN.NAM_HOC` |
| `tuNgay`, `denNgay` | Date | Fallback theo `APPROVED_AT`, `CREATED_AT`, `NGAY_TRAO_GIAI` hoặc ngày quyết định |
| `loaiCuocThi` | String[] | `NCKH`, `HSG`, `KHAC`; mapping từ rule dòng |
| `capThiIds` | String[] | `CAP_KHEN_THUONG_ID`, `CAP_GIAI_THUONG_ID`, `CAP_QUAN_LY_ID` |
| `workflowStatus` | String | Mặc định `Approved`/`APPROVED` tùy chuẩn hệ thống |
| `includeLegacyContestSource` | Boolean | Cho phép dùng `CUOC_THI_HOC_VIEN`, `KET_QUA_THI_HOC_VIEN` nếu schema được xác nhận |

## 9. API báo cáo đề xuất

### Endpoint

`GET /api/v1/reports/13h/nghien-cuu-khoa-hoc-va-thi-hoc-sinh-gioi-hoc-vien`

### Request params

```json
{
  "maDonVi": "G01.652",
  "namHocId": "NH03",
  "tuNgay": "2025-09-01",
  "denNgay": "2026-08-31",
  "workflowStatus": "Approved",
  "includeGroupRows": true
}
```

### Response DTO đề xuất

```json
{
  "reportCode": "13H",
  "title": "Thống kê số liệu về nghiên cứu khoa học và thi học sinh giỏi của học viên",
  "filters": {
    "maDonVi": "G01.652",
    "namHocId": "NH03"
  },
  "rows": [
    {
      "rowCode": "nckhCapTruong",
      "groupCode": "nckh",
      "label": "Cấp trường",
      "tongDuThi": 0,
      "giaiNhat": 0,
      "giaiNhi": 0,
      "giaiBa": 0,
      "giaiKhuyenKhich": 0,
      "ghiChu": null
    }
  ]
}
```

## 10. SQL/Procedure đề xuất

### 10.1. Bảng cấu hình dòng nên có

`[Suy luận]` Không nên hard-code rule nhận diện cuộc thi trong procedure. Nên có bảng cấu hình hoặc enum trong service:

| Bảng đề xuất | Vai trò |
|---|---|
| `RPT_13H_ROW_DEF` | Định nghĩa thứ tự dòng, nhãn, dòng nhóm/dòng con |
| `RPT_13H_ROW_RULE` | Mapping row với loại cuộc thi, cấp thi, keyword tên cuộc thi, lĩnh vực/hình thức/cấp khen thưởng |

### 10.2. SQL skeleton theo nguồn hiện hành `HV_KHEN_THUONG`

```sql
WITH params AS (
    SELECT :ma_don_vi AS ma_don_vi,
           :nam_hoc_id AS nam_hoc_id,
           :tu_ngay AS tu_ngay,
           :den_ngay AS den_ngay,
           NVL(:workflow_status, 'Approved') AS workflow_status
    FROM dual
),
row_def AS (
    SELECT row_code, group_code, label, display_order, is_group_row
    FROM X02_APP.RPT_13H_ROW_DEF
),
reward_base AS (
    SELECT kt.id,
           kt.hoc_vien_id,
           kt.cap_khen_thuong_id,
           kt.linh_vuc_khen_thuong_id,
           kt.hinh_thuc_khen_thuong_id,
           kt.giai_thuong_id,
           kt.ly_do_khen_thuong,
           gt.ma AS giai_ma,
           gt.ten AS giai_ten
    FROM X02_APP.HV_KHEN_THUONG kt
    JOIN X02_APP.HOC_VIEN hv
      ON hv.id = kt.hoc_vien_id
     AND hv.is_deleted = 0
    LEFT JOIN X02_DM.DM_GIAI_THUONG gt
      ON gt.id = kt.giai_thuong_id
     AND gt.is_deleted = 0
    CROSS JOIN params p
    WHERE kt.is_deleted = 0
      AND kt.is_active = 1
      AND kt.workflow_status = p.workflow_status
      AND (p.ma_don_vi IS NULL OR kt.ma_don_vi = p.ma_don_vi OR hv.ma_don_vi = p.ma_don_vi)
      AND (p.nam_hoc_id IS NULL OR kt.nam_khen_thuong_id = p.nam_hoc_id)
      AND (p.tu_ngay IS NULL OR TRUNC(kt.approved_at) >= p.tu_ngay OR TRUNC(kt.created_at) >= p.tu_ngay)
      AND (p.den_ngay IS NULL OR TRUNC(kt.approved_at) <= p.den_ngay OR TRUNC(kt.created_at) <= p.den_ngay)
),
mapped AS (
    SELECT rr.row_code,
           rb.*
    FROM reward_base rb
    JOIN X02_APP.RPT_13H_ROW_RULE rr
      ON (rr.cap_khen_thuong_id IS NULL OR rr.cap_khen_thuong_id = rb.cap_khen_thuong_id)
     AND (rr.linh_vuc_khen_thuong_id IS NULL OR rr.linh_vuc_khen_thuong_id = rb.linh_vuc_khen_thuong_id)
     AND (rr.hinh_thuc_khen_thuong_id IS NULL OR rr.hinh_thuc_khen_thuong_id = rb.hinh_thuc_khen_thuong_id)
     AND (rr.keyword IS NULL OR LOWER(rb.ly_do_khen_thuong) LIKE '%' || LOWER(rr.keyword) || '%')
),
agg AS (
    SELECT row_code,
           COUNT(DISTINCT hoc_vien_id) AS tong_du_thi,
           SUM(CASE WHEN UPPER(giai_ten) LIKE '%NHẤT%' THEN 1 ELSE 0 END) AS giai_nhat,
           SUM(CASE WHEN UPPER(giai_ten) LIKE '%NHÌ%' THEN 1 ELSE 0 END) AS giai_nhi,
           SUM(CASE WHEN UPPER(giai_ten) LIKE '%BA%' THEN 1 ELSE 0 END) AS giai_ba,
           SUM(CASE WHEN UPPER(giai_ten) LIKE '%KHUYẾN KHÍCH%' THEN 1 ELSE 0 END) AS giai_khuyen_khich
    FROM mapped
    GROUP BY row_code
)
SELECT rd.row_code,
       rd.group_code,
       rd.label,
       NVL(a.tong_du_thi, 0) AS tong_du_thi,
       NVL(a.giai_nhat, 0) AS giai_nhat,
       NVL(a.giai_nhi, 0) AS giai_nhi,
       NVL(a.giai_ba, 0) AS giai_ba,
       NVL(a.giai_khuyen_khich, 0) AS giai_khuyen_khich
FROM row_def rd
LEFT JOIN agg a
  ON a.row_code = rd.row_code
ORDER BY rd.display_order;
```

`[Cần xác nhận]` SQL trên đếm `tongDuThi` theo `COUNT(DISTINCT HOC_VIEN_ID)`. Nếu cần đếm nhóm dự thi hoặc số học viên trong nhóm, phải ưu tiên nguồn có `SO_LUONG_HOC_VIEN`.

### 10.3. Hướng SQL nếu xác nhận bảng cuộc thi học viên

Nếu `CUOC_THI_HOC_VIEN`, `KET_QUA_THI_HOC_VIEN` được đưa vào schema hiện hành, nguồn này phù hợp hơn:

```sql
SELECT rd.row_code,
       SUM(NVL(kq.so_luong_hoc_vien, 0)) AS tong_du_thi,
       SUM(CASE WHEN UPPER(kq.giai_thuong) LIKE '%NHẤT%' THEN 1 ELSE 0 END) AS giai_nhat,
       SUM(CASE WHEN UPPER(kq.giai_thuong) LIKE '%NHÌ%' THEN 1 ELSE 0 END) AS giai_nhi,
       SUM(CASE WHEN UPPER(kq.giai_thuong) LIKE '%BA%' THEN 1 ELSE 0 END) AS giai_ba,
       SUM(CASE WHEN UPPER(kq.giai_thuong) LIKE '%KHUYẾN KHÍCH%' THEN 1 ELSE 0 END) AS giai_khuyen_khich
FROM X02_APP.CUOC_THI_HOC_VIEN ct
JOIN X02_APP.KET_QUA_THI_HOC_VIEN kq
  ON kq.cuoc_thi_id = ct.id
JOIN X02_APP.RPT_13H_ROW_RULE rr
  ON rr.loai_cuoc_thi = ct.phan_loai
 AND (rr.cap_quan_ly_id IS NULL OR rr.cap_quan_ly_id = ct.cap_quan_ly_id)
 AND (rr.keyword IS NULL OR LOWER(ct.ten_cuoc_thi) LIKE '%' || LOWER(rr.keyword) || '%')
JOIN X02_APP.RPT_13H_ROW_DEF rd
  ON rd.row_code = rr.row_code
WHERE ct.is_deleted = 0
  AND kq.is_deleted = 0
  AND (:nam_hoc IS NULL OR ct.nam_hoc = :nam_hoc)
  AND (:ma_don_vi IS NULL OR kq.don_vi_id = :ma_don_vi)
GROUP BY rd.row_code;
```

## 11. Quy tắc đối soát

| Quy tắc | Mục tiêu |
|---|---|
| Dòng nhóm 9, 13, 19 bằng tổng dòng con nếu export có tính dòng nhóm | Tránh lệch tổng giữa nhóm và cấp thi |
| `giaiNhat + giaiNhi + giaiBa + giaiKhuyenKhich <= tongDuThi` khi đếm cá nhân | Phát hiện dữ liệu giải không hợp lý; ngoại lệ nếu một học viên/nhóm nhận nhiều giải |
| Prize rank chỉ nhận từ `DM_GIAI_THUONG` hoặc rule chuẩn | Tránh match text sai do nhập tự do |
| Chỉ lấy bản ghi workflow đã duyệt | Tránh số liệu nháp lọt vào báo cáo chính thức |
| Không trộn đơn vị đếm cá nhân và nhóm trong cùng một dòng | Bảo đảm cột D có ý nghĩa nhất quán |
| Các cuộc thi khác phải match theo cấu hình keyword/danh mục | Tránh bỏ sót do tên cuộc thi thay đổi nhẹ |

## 12. Gap và câu hỏi cần xác nhận

| Vấn đề | Mức độ | Ghi chú |
|---|---|---|
| Nguồn chính thức cho cuộc thi học viên | Cao | `CUOC_THI_HOC_VIEN`, `KET_QUA_THI_HOC_VIEN` hợp layout hơn nhưng chưa thấy trong `docs/database/X02_APP.sql` |
| Đơn vị đếm cột `Tổng số học viên/nhóm học viên dự thi` | Cao | Cần chốt đếm cá nhân, nhóm, hay số học viên quy đổi theo nhóm |
| Mapping NCKH từ `GIAI_THUONG_NC_KHCN` sang học viên | Cao | Bảng RES lưu `TEN_TAC_GIA` dạng text, chưa đủ chắc để count học viên |
| Danh mục cấp thi/cấp giải | Trung bình | Cần mapping cấp trường, Bộ Công an, Bộ GDĐT, quốc tế, quốc gia, Sở GDĐT |
| Danh sách dòng `Các cuộc thi khác` | Trung bình | Nên cấu hình theo kỳ báo cáo; template đang có tên cuộc thi/năm cụ thể |
| Dòng nhóm có tính tổng hay để trống | Trung bình | Excel không có công thức, cần chốt khi export |
| Mapping `Giải Nhất/Nhì/Ba/Khuyến khích` | Thấp | `DM_GIAI_THUONG` đã có các giá trị tương ứng, nhưng cần dùng ID/mã thay vì match text khi triển khai |

## 13. Tham chiếu đã đối chiếu

- `docs/report-input/13H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/LRN-dashboard.md`
- `docs/dashboard/nghien-cuu.md`
- `docs/output/database-business-analysis.md`
- `src/backend/qldt-v2/src/main/resources/app.sql`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/res/resgiaithuong/entity/GiaiThuong.java`
- `src/backend/qldt-v2/docs/domain/DOMAIN_OBJECT_CONTROLLER_MAP.md`

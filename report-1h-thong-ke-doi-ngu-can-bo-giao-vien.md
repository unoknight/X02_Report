# 1H - Thống kê đội ngũ cán bộ, giáo viên

## 1. Thông tin chung

| Thuộc tính | Giá trị |
|---|---|
| Mã báo cáo | 1H `[Suy luận]` |
| Tên báo cáo | Thống kê đội ngũ cán bộ, giáo viên |
| File mẫu | `docs/report-input/1H.xlsx` |
| Sheet | `TKGV` |
| Đơn vị báo cáo | Học viện/Trường CAND |
| Kỳ báo cáo | Theo năm báo cáo; mẫu ghi năm 2026 |
| Đối tượng thống kê | Cán bộ, nhà giáo/giáo viên đang công tác |
| Đơn vị tính | Người |
| Nguồn dữ liệu chính | `X02_APP.CAN_BO_NHA_GIAO`, `X02_APP.CON_NGUOI`, `X02_APP.QUA_TRINH_GIANG_DAY_CONG_TAC`, `X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH` |
| Mức độ mapping | Tương đối rõ |

---

## 2. Mục đích nghiệp vụ

Báo cáo phục vụ tổng hợp quân số và trình độ đội ngũ cán bộ, giáo viên trong Học viện/Trường CAND theo nhóm tổ chức nội bộ như Ban Giám đốc, Khoa, Phòng, Trung tâm. Báo cáo hỗ trợ lãnh đạo đánh giá quy mô nhân sự, cơ cấu nữ, trình độ học vấn, nghiệp vụ Công an, lý luận chính trị, nghiệp vụ sư phạm, nghiệp vụ quản lý giáo dục và chức danh giáo sư/phó giáo sư.

---

## 3. Cấu trúc báo cáo từ Excel

### 3.1 Header báo cáo

| Vị trí Excel | Nội dung | Ghi chú |
|---|---|---|
| A1:D1 | BỘ CÔNG AN | Merge cell |
| A2:D2 | HỌC VIỆN/TRƯỜNG CAND | Merge cell |
| H1:AD1 | THỐNG KÊ ĐỘI NGŨ CÁN BỘ, GIÁO VIÊN | Tiêu đề chính |
| H2:AD2 | (Kèm theo Báo cáo số: /BC-... ngày tháng năm 2026) | Căn cứ/kỳ báo cáo |
| A4:AD6 | Header nhiều dòng | Có merge cell nhóm cột |
| A7:AD10 | Dòng nhập liệu chi tiết | Ban Giám đốc, Khoa, Phòng, Trung tâm |
| A11:AD11 | Dòng tổng | Công thức `SUM` từ dòng 7 đến dòng 10 |

Workbook có dimension `A1:AE1000`, nhưng vùng dữ liệu thực tế có giá trị đến cột `AD`; cột `AE` không có header/dữ liệu trong mẫu đọc được.

### 3.2 Nhóm cột

| Nhóm cột | Cột Excel | Tên cột | Ý nghĩa |
|---|---|---|---|
| Định danh dòng | A | TT | Số thứ tự dòng thống kê |
| Định danh dòng | B | Đội ngũ thống kê | Nhóm tổ chức/đơn vị nội bộ |
| Quân số | C | Hiện có | Tổng số cán bộ, giáo viên hiện có |
| So với cùng kỳ | D:E | Tăng, Giảm | Chênh lệch quân số so với cùng kỳ năm trước |
| Vai trò lãnh đạo | F | Lãnh đạo Phòng, Khoa | Số người giữ chức vụ/chức danh lãnh đạo phòng/khoa |
| Thành phần | G | Nữ | Số cán bộ, giáo viên nữ |
| Học vấn | H:M | Tiến sĩ, Thạc sĩ, Đại học, Cao đẳng, Trung cấp, THPT | Trình độ học vấn/đào tạo cao nhất `[Cần xác nhận]` |
| Nghiệp vụ Công an | N:U | Tiến sĩ, Thạc sĩ, Đại học, Cao đẳng, Trung cấp, 6 tháng, Sơ cấp, Chưa học | Trình độ nghiệp vụ Công an |
| Lý luận chính trị | V:X | Cao cấp, Trung cấp, Sơ cấp | Trình độ LLCT |
| Nghiệp vụ sư phạm | Y:Z | Đại học, Bồi dưỡng | Trình độ/chứng chỉ nghiệp vụ sư phạm |
| Nghiệp vụ QLGD | AA:AB | Đại học, Bồi dưỡng | Trình độ/chứng chỉ nghiệp vụ quản lý giáo dục |
| Chức danh | AC:AD | Giáo sư, Phó Giáo sư | Học hàm/chức danh GS, PGS `[Cần xác nhận]` |

### 3.3 Nhóm dòng/chỉ tiêu

| STT | Vị trí Excel | Row code | Tên dòng | Công thức Excel | Ghi chú |
|---:|---|---|---|---|---|
| 1 | A7:B7 | BGD | Ban Giám đốc | Nhập liệu | Cần mapping theo chức vụ/chức danh hoặc bảng `BAN_GIAM_HIEU` |
| 2 | A8:B8 | KHOA | Khoa ... | Nhập liệu | Nhóm đơn vị có tên/cấp là Khoa |
| 3 | A9:B9 | PHONG | Phòng ... | Nhập liệu | Nhóm đơn vị có tên/cấp là Phòng |
| 4 | A10:B10 | TRUNG_TAM | Trung tâm ... | Nhập liệu | Nhóm đơn vị có tên/cấp là Trung tâm |
| 5 | A11:AD11 | TOTAL | Tổng | `SUM(C7:C10)` ... `SUM(AD7:AD10)` | Tổng cộng các dòng con |

---

## 4. Matching với nghiệp vụ hệ thống

| Thành phần báo cáo | Nghiệp vụ hệ thống | Phân hệ | Đối tượng dữ liệu | Ghi chú |
|---|---|---|---|---|
| Đội ngũ cán bộ, giáo viên | Quản lý cán bộ/nhà giáo | Cán bộ, giáo viên | `CAN_BO_NHA_GIAO` | Bảng có `PHAN_LOAI` comment `1: Nhà giáo, 2: Cán bộ` |
| Thông tin cá nhân, giới tính | Hồ sơ nhân thân dùng chung | Hồ sơ con người | `CON_NGUOI` | Join qua `CAN_BO_NHA_GIAO.CON_NGUOI_ID` |
| Nhóm đơn vị Khoa/Phòng/Trung tâm | Quá trình giảng dạy/công tác | Cán bộ, giáo viên | `QUA_TRINH_GIANG_DAY_CONG_TAC.KHOA_ID`, `DM_DON_VI`/`DM_DON_VI_CAND` | `[Cần xác nhận]` `KHOA_ID` có đang lưu cả Phòng/Trung tâm hay chỉ Khoa/Bộ môn |
| Chức vụ/chức danh lãnh đạo | Quá trình giảng dạy/công tác | Cán bộ, giáo viên | `QUA_TRINH_GIANG_DAY_CONG_TAC.CHUC_VU_ID`, `CHUC_DANH_ID`, `DM_CHUC_VU`, `DM_CHUC_DANH` | Có danh mục Trưởng/Phó phòng, Trưởng/Phó khoa |
| Trình độ học vấn | Quá trình bồi dưỡng chức danh | Cán bộ, giáo viên | `QUA_TRINH_BOI_DUONG_CHUC_DANH.TRINH_DO_DAO_TAO_ID`, `DM_TRINH_DO_DAO_TAO` | `[Cần xác nhận]` học vấn có đồng nhất với trình độ đào tạo hay cần `DM_HOC_VI` |
| Nghiệp vụ Công an | Quá trình bồi dưỡng chức danh | Cán bộ, giáo viên | `TRINH_DO_NGHIEP_VU_CONG_AN_ID`, `DM_TRINH_DO_NGHIEP_VU_CA` | Mapping tương đối rõ |
| Lý luận chính trị | Quá trình bồi dưỡng chức danh | Cán bộ, giáo viên | `TRINH_DO_LY_LUAN_CHINH_TRI_ID`, `DM_TRINH_DO_LLCT` | Mapping rõ |
| Nghiệp vụ sư phạm | Quá trình bồi dưỡng chức danh | Cán bộ, giáo viên | `NGHIEP_VU_SU_PHAM_ID`, `DM_NGHIEP_VU_SU_PHAM` | Mapping rõ |
| Nghiệp vụ QLGD | Quá trình bồi dưỡng chức danh | Cán bộ, giáo viên | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID`, `DM_NGHIEP_VU_QUAN_LY_GIAO_DUC` | Mapping rõ |
| Giáo sư/Phó Giáo sư | Chức danh/học hàm | Danh mục | `DM_CHUC_DANH`, `DM_HOC_HAM` | `[Cần xác nhận]` chưa thấy FK `HOC_HAM_ID` trong `CAN_BO_NHA_GIAO`; có thể đang lưu qua `CHUC_DANH_ID` |
| So với cùng kỳ tăng/giảm | Thống kê biến động quân số | Báo cáo | `CREATED_AT`, `NGAY_VAO_NGANH`, `TRANG_THAI_CONG_TAC`, snapshot lịch sử | `[Cần xác nhận]` DB chưa thấy bảng snapshot quân số theo kỳ |

---

## 5. Filter báo cáo

### 5.1 Filter bắt buộc

| STT | Filter | Kiểu dữ liệu | Bắt buộc | Nguồn dữ liệu | Ý nghĩa |
|---:|---|---|---|---|---|
| 1 | Năm báo cáo | Number | Có | Request | Xác định kỳ báo cáo và mốc so sánh cùng kỳ |
| 2 | Ngày chốt số liệu | Date | Có | Request; mặc định 31/12/năm báo cáo hoặc ngày hiện tại `[Cần xác nhận]` | Lấy bản ghi hiện hành tại thời điểm báo cáo |
| 3 | Mã đơn vị | String | Có | `MA_DON_VI` | Lọc theo Học viện/Trường CAND/đơn vị lập báo cáo |
| 4 | Trạng thái duyệt | String | Có | `WORKFLOW_STATUS` | Thường lấy `Approved` để báo cáo chính thức |

### 5.2 Filter mở rộng

| STT | Filter | Kiểu dữ liệu | Nguồn dữ liệu | Ý nghĩa |
|---:|---|---|---|---|
| 1 | Phân loại cán bộ/nhà giáo | Number | `CAN_BO_NHA_GIAO.PHAN_LOAI` | Lọc riêng nhà giáo hoặc cán bộ |
| 2 | Nhóm đơn vị | String | `DM_DON_VI`, `DM_DON_VI_CAND` | Khoa/Phòng/Trung tâm/Ban Giám đốc |
| 3 | Trạng thái công tác | String | `TRANG_THAI_CONG_TAC`, `DM_TRANG_THAI_CONG_TAC` | Chỉ tính người đang công tác |
| 4 | Trình độ học vấn | String | `DM_TRINH_DO_DAO_TAO` hoặc `DM_HOC_VI` | Lọc theo học vấn |
| 5 | Chức danh/chức vụ | String | `DM_CHUC_DANH`, `DM_CHUC_VU` | Lọc lãnh đạo hoặc GS/PGS |

### 5.3 Request filter đề xuất

```json
{
  "reportCode": "BM_1H",
  "year": 2026,
  "asOfDate": "2026-12-31",
  "maDonVi": "G01.651",
  "workflowStatus": "Approved",
  "phanLoai": null,
  "rowGroup": null,
  "includeInactive": false
}
```

---

## 6. Mapping field dữ liệu

| STT | Vị trí Excel | Tên chỉ tiêu/cột | Loại dữ liệu | Bảng nguồn | Cột nguồn | Điều kiện lọc | Công thức | Ghi chú |
|---:|---|---|---|---|---|---|---|---|
| 1 | A | TT | Text/Number | Không áp dụng | Không áp dụng | Theo cấu hình dòng | Hiển thị số thứ tự | Dữ liệu tĩnh theo mẫu |
| 2 | B | Đội ngũ thống kê | Text | `DM_DON_VI`/`DM_DON_VI_CAND`, `DM_CHUC_VU`, `DM_CHUC_DANH` | `TEN`, `MA`, `CHUC_VU_ID`, `CHUC_DANH_ID` | Mapping row | Tên dòng báo cáo | `[Cần xác nhận]` mapping Ban Giám đốc |
| 3 | C | Quân số hiện có | Number | `CAN_BO_NHA_GIAO` | `ID` | Active, not deleted, approved, theo đơn vị/nhóm dòng | `COUNT(DISTINCT cb.ID)` | Nên loại bản ghi thôi việc/nghỉ hưu qua trạng thái công tác |
| 4 | D | So với cùng kỳ năm trước - Tăng | Number | `CAN_BO_NHA_GIAO`, snapshot/lịch sử | `ID` | So sánh `asOfDate` với `ADD_MONTHS(asOfDate,-12)` | `GREATEST(current_count - previous_count, 0)` | `[Cần xác nhận]` thiếu snapshot chuẩn |
| 5 | E | So với cùng kỳ năm trước - Giảm | Number | `CAN_BO_NHA_GIAO`, snapshot/lịch sử | `ID` | So sánh `asOfDate` với `ADD_MONTHS(asOfDate,-12)` | `GREATEST(previous_count - current_count, 0)` | `[Cần xác nhận]` thiếu snapshot chuẩn |
| 6 | F | Lãnh đạo Phòng, Khoa | Number | `QUA_TRINH_GIANG_DAY_CONG_TAC`, `DM_CHUC_VU`, `DM_CHUC_DANH` | `CHUC_VU_ID`, `CHUC_DANH_ID` | Chức vụ/chức danh Trưởng/Phó phòng/khoa | `COUNT(DISTINCT cb.ID)` | Dùng bản ghi quá trình mới nhất |
| 7 | G | Nữ | Number | `CON_NGUOI` | `GIOI_TINH` | `GIOI_TINH = 'NU'` | `COUNT(DISTINCT cb.ID)` | Mapping rõ |
| 8 | H:M | Học vấn | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `DM_TRINH_DO_DAO_TAO` | `TRINH_DO_DAO_TAO_ID` | Tiến sĩ/Thạc sĩ/Đại học/Cao đẳng/Trung cấp/THPT | `COUNT(DISTINCT cb.ID)` | `[Cần xác nhận]` có thể cần `DM_HOC_VI` |
| 9 | N:U | Nghiệp vụ Công an | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `DM_TRINH_DO_NGHIEP_VU_CA` | `TRINH_DO_NGHIEP_VU_CONG_AN_ID` | Tiến sĩ/Thạc sĩ/Đại học/Cao đẳng/Trung cấp/6 tháng/Sơ cấp/Chưa học | `COUNT(DISTINCT cb.ID)` | `[Cần mapping danh mục]` |
| 10 | V:X | Lý luận chính trị | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `DM_TRINH_DO_LLCT` | `TRINH_DO_LY_LUAN_CHINH_TRI_ID` | Cao cấp/Trung cấp/Sơ cấp | `COUNT(DISTINCT cb.ID)` | `[Cần mapping danh mục]` |
| 11 | Y:Z | Nghiệp vụ sư phạm | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `DM_NGHIEP_VU_SU_PHAM` | `NGHIEP_VU_SU_PHAM_ID` | Đại học/Bồi dưỡng | `COUNT(DISTINCT cb.ID)` | Mapping rõ về bảng |
| 12 | AA:AB | Nghiệp vụ QLGD | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `DM_NGHIEP_VU_QUAN_LY_GIAO_DUC` | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID` | Đại học/Bồi dưỡng | `COUNT(DISTINCT cb.ID)` | Mapping rõ về bảng |
| 13 | AC:AD | Chức danh GS/PGS | Number | `QUA_TRINH_GIANG_DAY_CONG_TAC`, `DM_CHUC_DANH`; hoặc `DM_HOC_HAM` | `CHUC_DANH_ID` | Giáo sư/Phó Giáo sư | `COUNT(DISTINCT cb.ID)` | `[Cần xác nhận]` dùng chức danh hay học hàm |

---

## 7. Mapping dòng báo cáo

| STT | Row code | Tên dòng báo cáo | Parent row | Điều kiện nghiệp vụ | Mapping DB | Ghi chú |
|---:|---|---|---|---|---|---|
| 1 | TOTAL | Tổng |  | Tổng toàn báo cáo | Tổng `BGD`, `KHOA`, `PHONG`, `TRUNG_TAM` | Dòng 11 Excel |
| 2 | BGD | Ban Giám đốc | TOTAL | Cán bộ thuộc Ban Giám đốc/Ban Giám hiệu | `[Cần xác nhận]` `QUA_TRINH_GIANG_DAY_CONG_TAC.CHUC_VU_ID/CHUC_DANH_ID` thuộc Hiệu trưởng/Phó Hiệu trưởng/Giám đốc/Phó Giám đốc hoặc bảng `BAN_GIAM_HIEU` | Nên chuẩn hóa bằng bảng mapping dòng |
| 3 | KHOA | Khoa ... | TOTAL | Cán bộ, giáo viên thuộc khoa/bộ môn | `QUA_TRINH_GIANG_DAY_CONG_TAC.KHOA_ID -> DM_DON_VI/DM_DON_VI_CAND`, `TEN LIKE 'Khoa%'` `[Suy luận]` | Cần xác nhận `KHOA_ID` có tham chiếu đúng bảng danh mục đơn vị |
| 4 | PHONG | Phòng ... | TOTAL | Cán bộ, giáo viên thuộc phòng | `DM_DON_VI/DM_DON_VI_CAND.TEN LIKE 'Phòng%'` `[Suy luận]` | Nên dùng mã loại đơn vị thay vì LIKE |
| 5 | TRUNG_TAM | Trung tâm ... | TOTAL | Cán bộ, giáo viên thuộc trung tâm | `DM_DON_VI/DM_DON_VI_CAND.TEN LIKE 'Trung tâm%'` `[Suy luận]` | Nên dùng mã loại đơn vị thay vì LIKE |

---

## 8. Mapping cột báo cáo

| STT | Column code | Tên cột Excel | Nhóm cột | Công thức | Bảng/cột nguồn | Ghi chú |
|---:|---|---|---|---|---|---|
| 1 | QUAN_SO_HIEN_CO | Hiện có | Quân số | `COUNT(DISTINCT cb.ID)` | `CAN_BO_NHA_GIAO.ID` | Active, approved, theo đơn vị |
| 2 | TANG | Tăng | So với cùng kỳ | `GREATEST(current - previous, 0)` | Snapshot/tính theo mốc ngày | `[Cần xác nhận]` nguồn lịch sử |
| 3 | GIAM | Giảm | So với cùng kỳ | `GREATEST(previous - current, 0)` | Snapshot/tính theo mốc ngày | `[Cần xác nhận]` nguồn lịch sử |
| 4 | LANH_DAO_PHONG_KHOA | Lãnh đạo Phòng, Khoa | Vai trò | Count chức vụ/chức danh lãnh đạo | `CHUC_VU_ID`, `CHUC_DANH_ID` | Trưởng/Phó phòng/khoa |
| 5 | NU | Nữ | Thành phần | Count giới tính nữ | `CON_NGUOI.GIOI_TINH` | `NU` |
| 6 | HV_* | Tiến sĩ...THPT | Học vấn | Count theo trình độ | `TRINH_DO_DAO_TAO_ID` | `[Cần mapping danh mục]` |
| 7 | NVCA_* | Tiến sĩ...Chưa học | Nghiệp vụ Công an | Count theo NVCA | `TRINH_DO_NGHIEP_VU_CONG_AN_ID` | `[Cần mapping danh mục]` |
| 8 | LLCT_* | Cao cấp, Trung cấp, Sơ cấp | LLCT | Count theo LLCT | `TRINH_DO_LY_LUAN_CHINH_TRI_ID` | `[Cần mapping danh mục]` |
| 9 | NVSP_* | Đại học, Bồi dưỡng | Nghiệp vụ sư phạm | Count theo NVSP | `NGHIEP_VU_SU_PHAM_ID` | |
| 10 | NVQLGD_* | Đại học, Bồi dưỡng | Nghiệp vụ QLGD | Count theo NVQLGD | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID` | |
| 11 | GIAO_SU | Giáo sư | Chức danh | Count GS | `DM_CHUC_DANH` hoặc `DM_HOC_HAM` | `[Cần xác nhận]` |
| 12 | PHO_GIAO_SU | Phó Giáo sư | Chức danh | Count PGS | `DM_CHUC_DANH` hoặc `DM_HOC_HAM` | `[Cần xác nhận]` |

---

## 9. Công thức tính

### 9.1 Công thức tổng quát

```text
Quân số hiện có = COUNT(DISTINCT CAN_BO_NHA_GIAO.ID)
WHERE CAN_BO_NHA_GIAO.IS_DELETED = 0
  AND CAN_BO_NHA_GIAO.IS_ACTIVE = 1
  AND CAN_BO_NHA_GIAO.WORKFLOW_STATUS = 'Approved'
  AND CAN_BO_NHA_GIAO.MA_DON_VI = :maDonVi
  AND cán bộ thuộc row group tương ứng
```

```text
Nữ = COUNT(DISTINCT CAN_BO_NHA_GIAO.ID)
JOIN CON_NGUOI ON CON_NGUOI.ID = CAN_BO_NHA_GIAO.CON_NGUOI_ID
WHERE CON_NGUOI.GIOI_TINH = 'NU'
```

```text
Tăng = GREATEST(Quân số hiện có tại ngày chốt - Quân số cùng kỳ năm trước, 0)
Giảm = GREATEST(Quân số cùng kỳ năm trước - Quân số hiện có tại ngày chốt, 0)
```

`[Cần xác nhận]` Nếu hệ thống không có snapshot quân số theo kỳ, cần thống nhất cách tái dựng số cùng kỳ từ `CREATED_AT`, `NGAY_VAO_NGANH`, `TRANG_THAI_CONG_TAC` hoặc bổ sung bảng fact/snapshot báo cáo.

### 9.2 Công thức theo dòng

| Dòng báo cáo | Điều kiện lọc |
|---|---|
| Ban Giám đốc | `[Cần xác nhận]` Chức vụ/chức danh thuộc Giám đốc/Phó Giám đốc/Hiệu trưởng/Phó Hiệu trưởng hoặc nằm trong bảng `BAN_GIAM_HIEU` |
| Khoa | `[Suy luận]` Đơn vị công tác/khoa có `TEN LIKE 'Khoa%'` hoặc loại đơn vị = Khoa |
| Phòng | `[Suy luận]` Đơn vị công tác/khoa có `TEN LIKE 'Phòng%'` hoặc loại đơn vị = Phòng |
| Trung tâm | `[Suy luận]` Đơn vị công tác/khoa có `TEN LIKE 'Trung tâm%'` hoặc loại đơn vị = Trung tâm |
| Tổng | Tổng 4 dòng con |

### 9.3 Công thức theo cột

| Nhóm cột | Công thức | Điều kiện |
|---|---|---|
| Lãnh đạo Phòng, Khoa | `COUNT(DISTINCT cb.ID)` | Chức vụ/chức danh là Trưởng/Phó phòng/khoa |
| Học vấn | `COUNT(DISTINCT cb.ID)` | `TRINH_DO_DAO_TAO_ID` thuộc mã tương ứng |
| Nghiệp vụ Công an | `COUNT(DISTINCT cb.ID)` | `TRINH_DO_NGHIEP_VU_CONG_AN_ID` thuộc mã tương ứng |
| Lý luận chính trị | `COUNT(DISTINCT cb.ID)` | `TRINH_DO_LY_LUAN_CHINH_TRI_ID` thuộc mã tương ứng |
| Nghiệp vụ sư phạm | `COUNT(DISTINCT cb.ID)` | `NGHIEP_VU_SU_PHAM_ID` thuộc mã tương ứng |
| Nghiệp vụ QLGD | `COUNT(DISTINCT cb.ID)` | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID` thuộc mã tương ứng |
| Giáo sư/Phó Giáo sư | `COUNT(DISTINCT cb.ID)` | `DM_CHUC_DANH.TEN` hoặc `DM_HOC_HAM.TEN` tương ứng |

---

## 10. Proc SQL đề xuất

```sql
CREATE OR REPLACE PROCEDURE PROC_RPT_1H (
    P_NAM_BAO_CAO   IN NUMBER,
    P_MA_DON_VI     IN VARCHAR2,
    P_AS_OF_DATE    IN DATE DEFAULT NULL,
    P_RESULT        OUT SYS_REFCURSOR
)
AS
BEGIN
    OPEN P_RESULT FOR
        WITH params AS (
            SELECT NVL(P_AS_OF_DATE, TO_DATE(P_NAM_BAO_CAO || '-12-31', 'YYYY-MM-DD')) AS as_of_date
            FROM dual
        ),
        report_rows AS (
            SELECT 'BGD' AS row_code, 'Ban Giám đốc' AS row_name, 10 AS sort_order, 'TOTAL' AS parent_code FROM dual
            UNION ALL SELECT 'KHOA', 'Khoa ...', 20, 'TOTAL' FROM dual
            UNION ALL SELECT 'PHONG', 'Phòng ...', 30, 'TOTAL' FROM dual
            UNION ALL SELECT 'TRUNG_TAM', 'Trung tâm ...', 40, 'TOTAL' FROM dual
            UNION ALL SELECT 'TOTAL', 'Tổng', 999, NULL FROM dual
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
                JOIN params p ON 1 = 1
                WHERE NVL(qt.IS_DELETED, 0) = 0
                  AND NVL(qt.IS_ACTIVE, 1) = 1
                  AND qt.WORKFLOW_STATUS = 'Approved'
                  AND NVL(qt.THOI_GIAN_AP_DUNG, qt.CREATED_AT) <= p.as_of_date
            )
            WHERE rn = 1
        ),
        latest_boi_duong AS (
            SELECT *
            FROM (
                SELECT bd.*,
                       ROW_NUMBER() OVER (
                           PARTITION BY bd.CAN_BO_NHA_GIAO_ID
                           ORDER BY NVL(bd.THOI_GIAN_AP_DUNG, bd.CREATED_AT) DESC, bd.CREATED_AT DESC
                       ) rn
                FROM X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH bd
                JOIN params p ON 1 = 1
                WHERE NVL(bd.IS_DELETED, 0) = 0
                  AND NVL(bd.IS_ACTIVE, 1) = 1
                  AND bd.WORKFLOW_STATUS = 'Approved'
                  AND NVL(bd.THOI_GIAN_AP_DUNG, bd.CREATED_AT) <= p.as_of_date
            )
            WHERE rn = 1
        ),
        base_current AS (
            SELECT
                cb.ID,
                cn.GIOI_TINH,
                dv.TEN AS ten_don_vi_cong_tac,
                cv.TEN AS ten_chuc_vu,
                cd.TEN AS ten_chuc_danh,
                td.TEN AS ten_hoc_van,
                nvca.TEN AS ten_nvca,
                llct.TEN AS ten_llct,
                nvsp.TEN AS ten_nvsp,
                nvqlgd.TEN AS ten_nvqlgd,
                CASE
                    WHEN UPPER(NVL(cd.TEN, '') || ' ' || NVL(cv.TEN, '')) LIKE '%GIÁM ĐỐC%'
                      OR UPPER(NVL(cd.TEN, '') || ' ' || NVL(cv.TEN, '')) LIKE '%HIỆU TRƯỞNG%'
                    THEN 'BGD'
                    WHEN UPPER(NVL(dv.TEN, '')) LIKE 'KHOA%' THEN 'KHOA'
                    WHEN UPPER(NVL(dv.TEN, '')) LIKE 'PHÒNG%' THEN 'PHONG'
                    WHEN UPPER(NVL(dv.TEN, '')) LIKE 'TRUNG TÂM%' THEN 'TRUNG_TAM'
                    ELSE 'CHUA_MAPPING'
                END AS row_code
            FROM X02_APP.CAN_BO_NHA_GIAO cb
            JOIN X02_APP.CON_NGUOI cn ON cn.ID = cb.CON_NGUOI_ID
            LEFT JOIN latest_cong_tac qt ON qt.CAN_BO_NHA_GIAO_ID = cb.ID
            LEFT JOIN X02_DM.DM_DON_VI dv ON dv.ID = qt.KHOA_ID
            LEFT JOIN X02_DM.DM_CHUC_VU cv ON cv.ID = qt.CHUC_VU_ID
            LEFT JOIN X02_DM.DM_CHUC_DANH cd ON cd.ID = qt.CHUC_DANH_ID
            LEFT JOIN latest_boi_duong bd ON bd.CAN_BO_NHA_GIAO_ID = cb.ID
            LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td ON td.ID = bd.TRINH_DO_DAO_TAO_ID
            LEFT JOIN X02_DM.DM_TRINH_DO_NGHIEP_VU_CA nvca ON nvca.ID = bd.TRINH_DO_NGHIEP_VU_CONG_AN_ID
            LEFT JOIN X02_DM.DM_TRINH_DO_LLCT llct ON llct.ID = bd.TRINH_DO_LY_LUAN_CHINH_TRI_ID
            LEFT JOIN X02_DM.DM_NGHIEP_VU_SU_PHAM nvsp ON nvsp.ID = bd.NGHIEP_VU_SU_PHAM_ID
            LEFT JOIN X02_DM.DM_NGHIEP_VU_QUAN_LY_GIAO_DUC nvqlgd ON nvqlgd.ID = bd.NGHIEP_VU_QUAN_LY_GIAO_DUC_ID
            WHERE NVL(cb.IS_DELETED, 0) = 0
              AND NVL(cb.IS_ACTIVE, 1) = 1
              AND cb.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR cb.MA_DON_VI = P_MA_DON_VI)
        ),
        current_agg AS (
            SELECT
                row_code,
                COUNT(DISTINCT ID) AS quan_so_hien_co,
                SUM(CASE WHEN UPPER(NVL(ten_chuc_vu, '') || ' ' || NVL(ten_chuc_danh, '')) LIKE '%TRƯỞNG PHÒNG%'
                          OR UPPER(NVL(ten_chuc_vu, '') || ' ' || NVL(ten_chuc_danh, '')) LIKE '%PHÓ TRƯỞNG PHÒNG%'
                          OR UPPER(NVL(ten_chuc_vu, '') || ' ' || NVL(ten_chuc_danh, '')) LIKE '%TRƯỞNG KHOA%'
                          OR UPPER(NVL(ten_chuc_vu, '') || ' ' || NVL(ten_chuc_danh, '')) LIKE '%PHÓ TRƯỞNG KHOA%'
                         THEN 1 ELSE 0 END) AS lanh_dao_phong_khoa,
                SUM(CASE WHEN GIOI_TINH = 'NU' THEN 1 ELSE 0 END) AS nu,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%TIẾN SĨ%' THEN 1 ELSE 0 END) AS hv_tien_si,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%THẠC SĨ%' THEN 1 ELSE 0 END) AS hv_thac_si,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%ĐẠI HỌC%' THEN 1 ELSE 0 END) AS hv_dai_hoc,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%CAO ĐẲNG%' THEN 1 ELSE 0 END) AS hv_cao_dang,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%TRUNG CẤP%' THEN 1 ELSE 0 END) AS hv_trung_cap,
                SUM(CASE WHEN UPPER(NVL(ten_hoc_van, '')) LIKE '%THPT%' THEN 1 ELSE 0 END) AS hv_thpt,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%TIẾN SĨ%' THEN 1 ELSE 0 END) AS nvca_tien_si,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%THẠC SĨ%' THEN 1 ELSE 0 END) AS nvca_thac_si,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%ĐẠI HỌC%' THEN 1 ELSE 0 END) AS nvca_dai_hoc,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%CAO ĐẲNG%' THEN 1 ELSE 0 END) AS nvca_cao_dang,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%TRUNG CẤP%' THEN 1 ELSE 0 END) AS nvca_trung_cap,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%6 THÁNG%' THEN 1 ELSE 0 END) AS nvca_6_thang,
                SUM(CASE WHEN UPPER(NVL(ten_nvca, '')) LIKE '%SƠ CẤP%' THEN 1 ELSE 0 END) AS nvca_so_cap,
                SUM(CASE WHEN ten_nvca IS NULL OR UPPER(ten_nvca) LIKE '%CHƯA%' THEN 1 ELSE 0 END) AS nvca_chua_hoc,
                SUM(CASE WHEN UPPER(NVL(ten_llct, '')) LIKE '%CAO CẤP%' THEN 1 ELSE 0 END) AS llct_cao_cap,
                SUM(CASE WHEN UPPER(NVL(ten_llct, '')) LIKE '%TRUNG CẤP%' THEN 1 ELSE 0 END) AS llct_trung_cap,
                SUM(CASE WHEN UPPER(NVL(ten_llct, '')) LIKE '%SƠ CẤP%' THEN 1 ELSE 0 END) AS llct_so_cap,
                SUM(CASE WHEN UPPER(NVL(ten_nvsp, '')) LIKE '%ĐẠI HỌC%' THEN 1 ELSE 0 END) AS nvsp_dai_hoc,
                SUM(CASE WHEN UPPER(NVL(ten_nvsp, '')) LIKE '%BỒI DƯỠNG%' THEN 1 ELSE 0 END) AS nvsp_boi_duong,
                SUM(CASE WHEN UPPER(NVL(ten_nvqlgd, '')) LIKE '%ĐẠI HỌC%' THEN 1 ELSE 0 END) AS nvqlgd_dai_hoc,
                SUM(CASE WHEN UPPER(NVL(ten_nvqlgd, '')) LIKE '%BỒI DƯỠNG%' THEN 1 ELSE 0 END) AS nvqlgd_boi_duong,
                SUM(CASE WHEN UPPER(NVL(ten_chuc_danh, '')) = 'GIÁO SƯ' THEN 1 ELSE 0 END) AS giao_su,
                SUM(CASE WHEN UPPER(NVL(ten_chuc_danh, '')) = 'PHÓ GIÁO SƯ' THEN 1 ELSE 0 END) AS pho_giao_su
            FROM base_current
            WHERE row_code <> 'CHUA_MAPPING'
            GROUP BY row_code
        ),
        current_with_total AS (
            SELECT * FROM current_agg
            UNION ALL
            SELECT 'TOTAL',
                   SUM(quan_so_hien_co), SUM(lanh_dao_phong_khoa), SUM(nu),
                   SUM(hv_tien_si), SUM(hv_thac_si), SUM(hv_dai_hoc), SUM(hv_cao_dang), SUM(hv_trung_cap), SUM(hv_thpt),
                   SUM(nvca_tien_si), SUM(nvca_thac_si), SUM(nvca_dai_hoc), SUM(nvca_cao_dang), SUM(nvca_trung_cap), SUM(nvca_6_thang), SUM(nvca_so_cap), SUM(nvca_chua_hoc),
                   SUM(llct_cao_cap), SUM(llct_trung_cap), SUM(llct_so_cap),
                   SUM(nvsp_dai_hoc), SUM(nvsp_boi_duong),
                   SUM(nvqlgd_dai_hoc), SUM(nvqlgd_boi_duong),
                   SUM(giao_su), SUM(pho_giao_su)
            FROM current_agg
        )
        SELECT rr.row_code,
               rr.row_name,
               rr.sort_order,
               NVL(c.quan_so_hien_co, 0) AS quan_so_hien_co,
               CAST(NULL AS NUMBER) AS tang,
               CAST(NULL AS NUMBER) AS giam,
               NVL(c.lanh_dao_phong_khoa, 0) AS lanh_dao_phong_khoa,
               NVL(c.nu, 0) AS nu,
               NVL(c.hv_tien_si, 0) AS hv_tien_si,
               NVL(c.hv_thac_si, 0) AS hv_thac_si,
               NVL(c.hv_dai_hoc, 0) AS hv_dai_hoc,
               NVL(c.hv_cao_dang, 0) AS hv_cao_dang,
               NVL(c.hv_trung_cap, 0) AS hv_trung_cap,
               NVL(c.hv_thpt, 0) AS hv_thpt,
               NVL(c.nvca_tien_si, 0) AS nvca_tien_si,
               NVL(c.nvca_thac_si, 0) AS nvca_thac_si,
               NVL(c.nvca_dai_hoc, 0) AS nvca_dai_hoc,
               NVL(c.nvca_cao_dang, 0) AS nvca_cao_dang,
               NVL(c.nvca_trung_cap, 0) AS nvca_trung_cap,
               NVL(c.nvca_6_thang, 0) AS nvca_6_thang,
               NVL(c.nvca_so_cap, 0) AS nvca_so_cap,
               NVL(c.nvca_chua_hoc, 0) AS nvca_chua_hoc,
               NVL(c.llct_cao_cap, 0) AS llct_cao_cap,
               NVL(c.llct_trung_cap, 0) AS llct_trung_cap,
               NVL(c.llct_so_cap, 0) AS llct_so_cap,
               NVL(c.nvsp_dai_hoc, 0) AS nvsp_dai_hoc,
               NVL(c.nvsp_boi_duong, 0) AS nvsp_boi_duong,
               NVL(c.nvqlgd_dai_hoc, 0) AS nvqlgd_dai_hoc,
               NVL(c.nvqlgd_boi_duong, 0) AS nvqlgd_boi_duong,
               NVL(c.giao_su, 0) AS giao_su,
               NVL(c.pho_giao_su, 0) AS pho_giao_su
        FROM report_rows rr
        LEFT JOIN current_with_total c ON c.row_code = rr.row_code
        ORDER BY rr.sort_order;
END;
/
```

Ghi chú SQL:

- `TANG` và `GIAM` đang để `NULL` trong skeleton vì cần xác nhận nguồn snapshot/cách tái dựng cùng kỳ.
- Mapping dòng đang dùng `LIKE` theo tên đơn vị/chức danh để minh họa. Khi triển khai thật nên tạo bảng mapping cấu hình hoặc dùng mã loại đơn vị/chức vụ ổn định.
- Nếu `QUA_TRINH_GIANG_DAY_CONG_TAC.KHOA_ID` thực tế tham chiếu `DM_DON_VI_CAND` thay vì `DM_DON_VI`, cần đổi join tương ứng.

### Query chi tiết nguồn dữ liệu

```sql
SELECT
    cb.ID AS can_bo_nha_giao_id,
    cb.MA_DON_VI,
    cb.PHAN_LOAI,
    cn.HO_TEN,
    cn.GIOI_TINH,
    dv.TEN AS don_vi_cong_tac,
    cv.TEN AS chuc_vu,
    cd.TEN AS chuc_danh,
    td.TEN AS trinh_do_dao_tao,
    nvca.TEN AS trinh_do_nghiep_vu_ca,
    llct.TEN AS trinh_do_llct,
    nvsp.TEN AS nghiep_vu_su_pham,
    nvqlgd.TEN AS nghiep_vu_qlgd
FROM X02_APP.CAN_BO_NHA_GIAO cb
JOIN X02_APP.CON_NGUOI cn ON cn.ID = cb.CON_NGUOI_ID
LEFT JOIN X02_APP.QUA_TRINH_GIANG_DAY_CONG_TAC qt ON qt.CAN_BO_NHA_GIAO_ID = cb.ID
LEFT JOIN X02_DM.DM_DON_VI dv ON dv.ID = qt.KHOA_ID
LEFT JOIN X02_DM.DM_CHUC_VU cv ON cv.ID = qt.CHUC_VU_ID
LEFT JOIN X02_DM.DM_CHUC_DANH cd ON cd.ID = qt.CHUC_DANH_ID
LEFT JOIN X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH bd ON bd.CAN_BO_NHA_GIAO_ID = cb.ID
LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td ON td.ID = bd.TRINH_DO_DAO_TAO_ID
LEFT JOIN X02_DM.DM_TRINH_DO_NGHIEP_VU_CA nvca ON nvca.ID = bd.TRINH_DO_NGHIEP_VU_CONG_AN_ID
LEFT JOIN X02_DM.DM_TRINH_DO_LLCT llct ON llct.ID = bd.TRINH_DO_LY_LUAN_CHINH_TRI_ID
LEFT JOIN X02_DM.DM_NGHIEP_VU_SU_PHAM nvsp ON nvsp.ID = bd.NGHIEP_VU_SU_PHAM_ID
LEFT JOIN X02_DM.DM_NGHIEP_VU_QUAN_LY_GIAO_DUC nvqlgd ON nvqlgd.ID = bd.NGHIEP_VU_QUAN_LY_GIAO_DUC_ID
WHERE cb.MA_DON_VI = :maDonVi
  AND cb.WORKFLOW_STATUS = 'Approved'
  AND NVL(cb.IS_DELETED, 0) = 0;
```

---

## 11. API đề xuất

Hiện source frontend có registry báo cáo “Báo cáo thống kê trình độ đội ngũ cán bộ, giáo viên”, nhưng `ReportPage` chỉ có component tĩnh cho khen thưởng/kỷ luật cán bộ giáo viên và phân loại học tập/rèn luyện học viên. `[Cần xác nhận]` Chưa thấy implementation riêng cho báo cáo 1H.

```http
POST /api/v1/reports/1h/query
```

Request:

```json
{
  "year": 2026,
  "asOfDate": "2026-12-31",
  "maDonVi": "G01.651",
  "workflowStatus": "Approved",
  "phanLoai": null,
  "rowGroup": null
}
```

Response:

```json
{
  "reportCode": "BM_1H",
  "reportName": "Thống kê đội ngũ cán bộ, giáo viên",
  "rows": [
    {
      "rowCode": "KHOA",
      "rowName": "Khoa ...",
      "quanSoHienCo": 0,
      "tang": null,
      "giam": null,
      "nu": 0
    }
  ]
}
```

Nếu tích hợp theo BCTK hiện có, có thể bổ sung template/config và dùng endpoint export:

```http
GET /api/report/get-bao-cao?maBaoCao=1h&exportType=EXCEL
```

---

## 12. Quy tắc đối soát số liệu

| STT | Quy tắc đối soát | Công thức kiểm tra | Ghi chú |
|---:|---|---|---|
| 1 | Tổng quân số bằng tổng dòng con | `TOTAL.QUAN_SO_HIEN_CO = SUM(BGD,KHOA,PHONG,TRUNG_TAM)` | Bắt buộc |
| 2 | Tổng nữ không vượt quân số | `NU <= QUAN_SO_HIEN_CO` | Bắt buộc |
| 3 | Lãnh đạo Phòng/Khoa không vượt quân số | `LANH_DAO_PHONG_KHOA <= QUAN_SO_HIEN_CO` | Bắt buộc |
| 4 | Mỗi nhóm học vấn không vượt quân số | Mỗi cột `HV_* <= QUAN_SO_HIEN_CO` | Bắt buộc |
| 5 | Nếu học vấn là một giá trị duy nhất/người | `SUM(HV_*) <= QUAN_SO_HIEN_CO` hoặc `= QUAN_SO_HIEN_CO` | `[Cần xác nhận]` người chưa nhập học vấn tính thế nào |
| 6 | Nếu nghiệp vụ Công an là một giá trị duy nhất/người | `SUM(NVCA_*) <= QUAN_SO_HIEN_CO` hoặc `= QUAN_SO_HIEN_CO` | `[Cần xác nhận]` cách tính “Chưa học” |
| 7 | Tăng/giảm không âm | `TANG >= 0 AND GIAM >= 0` | Bắt buộc |
| 8 | Không vừa tăng vừa giảm trên cùng dòng nếu dùng chênh lệch thuần | `NOT (TANG > 0 AND GIAM > 0)` | Nếu tính biến động vào/ra riêng thì quy tắc này không áp dụng |
| 9 | Tổng GS/PGS không vượt quân số | `GIAO_SU + PHO_GIAO_SU <= QUAN_SO_HIEN_CO` | Bắt buộc |
| 10 | Dòng chưa mapping cần được theo dõi | `COUNT(row_code = 'CHUA_MAPPING') = 0` | Bắt buộc trước khi chốt báo cáo |

---

## 13. Điểm thiếu / cần xác nhận

| STT | Nội dung cần xác nhận | Lý do | Mức độ ưu tiên |
|---:|---|---|---|
| 1 | Mã biểu mẫu chính thức có phải 1H không | File tên `1H.xlsx`, trong sheet không thấy cell ghi “Biểu mẫu 1H” | Cao |
| 2 | Ngày chốt số liệu/kỳ báo cáo chuẩn | Mẫu ghi năm 2026 nhưng không có ô filter | Cao |
| 3 | Cách xác định Ban Giám đốc | Có thể qua `BAN_GIAM_HIEU`, chức vụ/chức danh hoặc đơn vị | Cao |
| 4 | `QUA_TRINH_GIANG_DAY_CONG_TAC.KHOA_ID` tham chiếu `DM_DON_VI` hay `DM_DON_VI_CAND` | DDL comment ghi “Khoa/Bộ môn”, tên cột không khẳng định bảng đích | Cao |
| 5 | Học vấn dùng `DM_TRINH_DO_DAO_TAO` hay `DM_HOC_VI` | Báo cáo ghi “Học vấn”, bảng bồi dưỡng dùng `TRINH_DO_DAO_TAO_ID` | Cao |
| 6 | Chức danh GS/PGS lấy từ `DM_CHUC_DANH` hay `DM_HOC_HAM` | DB có cả hai danh mục, chưa thấy FK học hàm trong bảng cán bộ nhà giáo | Cao |
| 7 | Quy tắc so với cùng kỳ năm trước | Chưa thấy bảng snapshot quân số theo kỳ | Cao |
| 8 | Trạng thái công tác nào được tính là “hiện có” | Cần danh mục `DM_TRANG_THAI_CONG_TAC` và quy tắc nghiệp vụ | Cao |
| 9 | Quy tắc người có nhiều quá trình/bằng cấp | SQL đề xuất lấy bản ghi mới nhất theo `THOI_GIAN_AP_DUNG` | Trung bình |
| 10 | Mã danh mục chuẩn cho Tiến sĩ, Thạc sĩ, Đại học, Cao đẳng, Trung cấp, THPT, 6 tháng, Sơ cấp, Chưa học | SQL skeleton đang dùng so khớp tên để minh họa | Trung bình |
| 11 | Có cần tách cán bộ và nhà giáo trong báo cáo không | Bảng có `PHAN_LOAI`; mẫu gom “cán bộ, giáo viên” | Trung bình |
| 12 | BCTK có template/export riêng cho 1H chưa | Source hiện chỉ thấy registry frontend, chưa thấy component/data source riêng | Trung bình |

---

## 14. Nguồn tham chiếu

- File Excel: `docs/report-input/1H.xlsx`
- Database docs: `docs/database/X02_APP.sql`, `docs/database/X02_DM.sql`
- Tài liệu nghiệp vụ: `docs/output/database-business-analysis.md`, `docs/output/business-analysis/11-reports-dashboard-analysis.md`
- Source code: `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`, `src/frontend/frontend-x02-v2/src/domains/reports/pages/ReportPage.jsx`

---

## 15. Checklist hoàn thành

| Hạng mục | Trạng thái |
|---|---|
| Đã đọc file Excel mẫu | Đã đọc `1H.xlsx` |
| Đã nhận diện tên báo cáo/mã biểu mẫu | Đã nhận diện tên; mã 1H `[Suy luận]` |
| Đã bóc tách header nhiều dòng và merge cell | Đã thực hiện |
| Đã bóc tách nhóm cột | Đã thực hiện |
| Đã bóc tách nhóm dòng | Đã thực hiện |
| Đã xác định filter bắt buộc và mở rộng | Đã thực hiện |
| Đã matching với phân hệ nghiệp vụ | Đã thực hiện |
| Đã mapping field Excel với DB | Đã thực hiện, có điểm cần xác nhận |
| Đã mô tả công thức tính từng cột/dòng | Đã thực hiện |
| Đã sinh Proc SQL đề xuất | Đã thực hiện |
| Đã sinh API đề xuất | Đã thực hiện |
| Đã sinh quy tắc đối soát | Đã thực hiện |
| Đã ghi điểm cần xác nhận | Đã thực hiện |

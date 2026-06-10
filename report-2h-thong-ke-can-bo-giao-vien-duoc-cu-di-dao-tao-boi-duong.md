# 2H - Thống kê số liệu cán bộ, giáo viên được cử đi đào tạo, bồi dưỡng

## 1. Thông tin chung

| Thuộc tính | Giá trị |
|---|---|
| Mã báo cáo | 2H |
| Tên báo cáo | Thống kê số liệu cán bộ, giáo viên được cử đi đào tạo, bồi dưỡng |
| File mẫu | `docs/report-input/2H.xlsx` |
| Sheet | `ĐTBD GV` |
| Đơn vị báo cáo | Học viện/Trường CAND |
| Kỳ báo cáo | Theo năm báo cáo; mẫu ghi tháng 5 năm 2026 `[Cần xác nhận]` |
| Đối tượng thống kê | Cán bộ, giáo viên được cử đi đào tạo/bồi dưỡng |
| Đơn vị tính | Người/lượt người `[Cần xác nhận]` |
| Nguồn dữ liệu chính | `X02_APP.CAN_BO_NHA_GIAO`, `X02_APP.KET_QUA_BOI_DUONG_TAP_HUAN`, `X02_APP.BOI_DUONG_TAP_HUAN`, `X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH` |
| Nguồn dữ liệu mở rộng | `X02_APP.NGUOI_HOC_TRONG_NUOC_DI_HOC_NUOC_NGOAI`, `X02_APP.LOP_DAO_TAO_BOI_DUONG_QT` |
| Mức độ mapping | Tương đối rõ, còn cần xác nhận nguồn sự kiện cử đi học |

---

## 2. Mục đích nghiệp vụ

Báo cáo tổng hợp số cán bộ, giáo viên được cử đi đào tạo, bồi dưỡng theo nhóm đối tượng và loại hình đào tạo/bồi dưỡng. Báo cáo phục vụ theo dõi phát triển đội ngũ, kế hoạch chuẩn hóa trình độ, bồi dưỡng nghiệp vụ sư phạm, quản lý giáo dục, tin học, ngoại ngữ, lý luận chính trị và nghiệp vụ Công an.

Điểm nghiệp vụ quan trọng: báo cáo có thể được hiểu là “số lượt cử đi” hoặc “số người có kết quả/đang tham gia” trong kỳ. Hai cách hiểu này cho kết quả khác nhau nếu một người tham gia nhiều khóa. Cần xác nhận trước khi chốt SQL triển khai.

---

## 3. Cấu trúc báo cáo từ Excel

### 3.1 Header báo cáo

| Vị trí Excel | Nội dung | Ghi chú |
|---|---|---|
| A1:P1 | Biểu mẫu 2H | Merge cell |
| A2:B2 | BỘ CÔNG AN / HỌC VIỆN/TRƯỜNG CAND | Đơn vị lập báo cáo |
| C2:P2 | THỐNG KÊ SỐ LIỆU CÁN BỘ, GIÁO VIÊN ĐƯỢC CỬ ĐI ĐÀO TẠO, BỒI DƯỠNG | Tiêu đề chính |
| C3:P3 | (Kèm theo Báo cáo số ... ngày ... tháng 5 năm 2026) | Căn cứ/kỳ báo cáo |
| A6:P8 | Header nhiều dòng | Có merge cell nhóm cột |
| A9:O11 | Dòng nhập liệu chi tiết | Giáo viên, Cán bộ QLGD, Cán bộ khác |
| B12:O12 | Dòng tổng | Công thức `SUM(C9:C11)` ... `SUM(O9:O11)` |

Workbook có dimension `A1:AB41`, nhưng vùng báo cáo có giá trị thực tế đến cột `P`; các cột `Q:AB` không có dữ liệu trong mẫu đọc được.

### 3.2 Nhóm cột

| Nhóm cột | Cột Excel | Tên cột | Ý nghĩa |
|---|---|---|---|
| Định danh dòng | A | TT | Số thứ tự |
| Định danh dòng | B | Đối tượng | Nhóm cán bộ/giáo viên |
| Đào tạo trình độ | C | Nghiên cứu sinh | Cán bộ/giáo viên được cử đi đào tạo tiến sĩ/nghiên cứu sinh |
| Đào tạo trình độ | D | Cao học | Đào tạo thạc sĩ/cao học |
| Đào tạo trình độ | E | Đại học | Đào tạo trình độ đại học |
| Đào tạo trình độ | F | Cao đẳng | Đào tạo trình độ cao đẳng |
| Đào tạo trình độ | G | Trung cấp | Đào tạo trình độ trung cấp |
| Bồi dưỡng nghiệp vụ | H | BDNV sư phạm | Bồi dưỡng nghiệp vụ sư phạm |
| Bồi dưỡng nghiệp vụ | I | BDNVQLGD | Bồi dưỡng nghiệp vụ quản lý giáo dục |
| Bồi dưỡng chức danh | J | Bồi dưỡng chức danh | Bồi dưỡng theo chức danh/chức vụ |
| Bồi dưỡng năng lực | K | Bồi dưỡng tin học | Bồi dưỡng tin học |
| Bồi dưỡng năng lực | L | Bồi dưỡng ngoại ngữ | Bồi dưỡng ngoại ngữ |
| Lý luận chính trị | M | Cao cấp lý luận chính trị | Cử đi học/bồi dưỡng cao cấp LLCT |
| Nghiệp vụ Công an | N | BDNV Công an 6 tháng | Bồi dưỡng nghiệp vụ Công an 6 tháng |
| Khác | O | Các loại hình đào tạo, bồi dưỡng khác | Các loại hình chưa phân nhóm |
| Ghi chú | P | Ghi chú | Ghi chú báo cáo |

### 3.3 Nhóm dòng/chỉ tiêu

| STT | Vị trí Excel | Row code | Tên dòng | Công thức Excel | Ghi chú |
|---:|---|---|---|---|---|
| 1 | A9:B9 | GIAO_VIEN | Giáo viên | Nhập liệu | Nhóm nhà giáo/giáo viên |
| 2 | A10:B10 | CAN_BO_QLGD | Cán bộ quản lý giáo dục | Nhập liệu | Nhóm cán bộ QLGD |
| 3 | A11:B11 | CAN_BO_KHAC | Cán bộ khác | Nhập liệu | Nhóm cán bộ không thuộc hai nhóm trên |
| 4 | B12:O12 | TOTAL | Tổng | `SUM(C9:C11)` ... `SUM(O9:O11)` | Tổng các dòng con |

---

## 4. Matching với nghiệp vụ hệ thống

| Thành phần báo cáo | Nghiệp vụ hệ thống | Phân hệ | Đối tượng dữ liệu | Ghi chú |
|---|---|---|---|---|
| Giáo viên | Quản lý cán bộ/nhà giáo | STF - Cán bộ, giáo viên | `CAN_BO_NHA_GIAO.PHAN_LOAI = 1` `[Suy luận]` | Comment DB: `1: Nhà giáo, 2: Cán bộ` |
| Cán bộ QLGD | Quản lý chức danh/chức vụ | STF | `QUA_TRINH_GIANG_DAY_CONG_TAC.CHUC_DANH_ID`, `DM_CHUC_DANH` | Có `DM_CHUC_DANH` giá trị “Cán bộ quản lý giáo dục” |
| Cán bộ khác | Quản lý cán bộ/nhà giáo | STF | `CAN_BO_NHA_GIAO.PHAN_LOAI = 2` trừ nhóm QLGD | `[Suy luận]` cần xác nhận quy tắc loại trừ |
| Đào tạo trình độ | Quá trình bồi dưỡng/chức danh | STF | `QUA_TRINH_BOI_DUONG_CHUC_DANH.TRINH_DO_DAO_TAO_ID` | Phù hợp các cột nghiên cứu sinh/cao học/đại học/cao đẳng/trung cấp |
| BDNV sư phạm | Bồi dưỡng nghiệp vụ sư phạm | STF | `NGHIEP_VU_SU_PHAM_ID`, `DM_NGHIEP_VU_SU_PHAM` | Có danh mục NVSP |
| BDNVQLGD | Bồi dưỡng quản lý giáo dục | STF | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID`, `DM_NGHIEP_VU_QUAN_LY_GIAO_DUC` | Có danh mục NVQLGD |
| Bồi dưỡng chức danh | Quá trình bồi dưỡng chức danh | STF | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `[Cần xác nhận]` chưa có cột loại bồi dưỡng chức danh riêng |
| Bồi dưỡng tin học | Bồi dưỡng/chứng chỉ tin học | STF | `TRINH_DO_TIN_HOC_ID`, `DM_TRINH_DO_TIN_HOC` | Mapping rõ về bảng/cột |
| Bồi dưỡng ngoại ngữ | Bồi dưỡng/chứng chỉ ngoại ngữ | STF | `TRINH_DO_NGOAI_NGU_ID`, `DM_TRINH_DO_NGOAI_NGU` | Mapping rõ về bảng/cột |
| Cao cấp LLCT | Đào tạo/bồi dưỡng LLCT | STF/Tuyển sinh LLCT | `TRINH_DO_LY_LUAN_CHINH_TRI_ID`, `DM_TRINH_DO_LLCT`; có thể liên quan tuyển sinh LLCT | `[Cần xác nhận]` dùng quá trình bồi dưỡng hay bảng tuyển sinh LLCT |
| BDNV Công an 6 tháng | Bồi dưỡng nghiệp vụ Công an | STF | `TRINH_DO_NGHIEP_VU_CONG_AN_ID`, `DM_TRINH_DO_NGHIEP_VU_CA` | Cần mapping danh mục “6 tháng” |
| Sự kiện được cử đi | Cử cán bộ/nhà giáo tham gia khóa | STF/HTQT | `KET_QUA_BOI_DUONG_TAP_HUAN`, `BOI_DUONG_TAP_HUAN`, `NGUOI_HOC_TRONG_NUOC_DI_HOC_NUOC_NGOAI` | `[Cần xác nhận]` báo cáo lấy kế hoạch cử đi hay kết quả hoàn thành |

---

## 5. Filter báo cáo

### 5.1 Filter bắt buộc

| STT | Filter | Kiểu dữ liệu | Bắt buộc | Nguồn dữ liệu | Ý nghĩa |
|---:|---|---|---|---|---|
| 1 | Năm báo cáo | Number | Có | Request | Xác định kỳ thống kê |
| 2 | Từ ngày | Date | Có | Request | Ngày bắt đầu kỳ, mặc định `01/01/:year` |
| 3 | Đến ngày | Date | Có | Request | Ngày kết thúc kỳ, theo mẫu có thể là tháng 5/2026 `[Cần xác nhận]` |
| 4 | Mã đơn vị | String | Có | `MA_DON_VI` | Lọc theo Học viện/Trường CAND |
| 5 | Trạng thái duyệt | String | Có | `WORKFLOW_STATUS` | Lấy dữ liệu đã duyệt, thường là `Approved` |

### 5.2 Filter mở rộng

| STT | Filter | Kiểu dữ liệu | Nguồn dữ liệu | Ý nghĩa |
|---:|---|---|---|---|
| 1 | Nhóm đối tượng | String | `PHAN_LOAI`, `DM_CHUC_DANH` | Giáo viên/Cán bộ QLGD/Cán bộ khác |
| 2 | Loại hình đào tạo/bồi dưỡng | String | Cột nguồn/danh mục | Lọc theo từng cột C:O |
| 3 | Trạng thái công tác | String | `TRANG_THAI_CONG_TAC` | Chỉ thống kê cán bộ đang công tác |
| 4 | Trạng thái khóa/khóa học | String | `BOI_DUONG_TAP_HUAN.TRANG_THAI`, `KET_QUA_BOI_DUONG_TAP_HUAN.TRANG_THAI` | Đang học/hoàn thành/hủy `[Cần xác nhận]` |
| 5 | Trong nước/nước ngoài | Number | `LOP_DAO_TAO_BOI_DUONG_QT.LOAI_DIA_BAN` | Nếu tính cả đào tạo quốc tế |

### 5.3 Request filter đề xuất

```json
{
  "reportCode": "BM_2H",
  "year": 2026,
  "fromDate": "2026-01-01",
  "toDate": "2026-05-31",
  "maDonVi": "G01.651",
  "workflowStatus": "Approved",
  "objectGroup": null,
  "trainingType": null,
  "countMode": "LUOT"
}
```

---

## 6. Mapping field dữ liệu

| STT | Vị trí Excel | Tên chỉ tiêu/cột | Loại dữ liệu | Bảng nguồn | Cột nguồn | Điều kiện lọc | Công thức | Ghi chú |
|---:|---|---|---|---|---|---|---|---|
| 1 | A | TT | Number/Text | Không áp dụng | Không áp dụng | Theo cấu hình dòng | Hiển thị số thứ tự | Dữ liệu tĩnh |
| 2 | B | Đối tượng | Text | `CAN_BO_NHA_GIAO`, `QUA_TRINH_GIANG_DAY_CONG_TAC`, `DM_CHUC_DANH` | `PHAN_LOAI`, `CHUC_DANH_ID` | Mapping row | Tên nhóm đối tượng | Cần xác nhận quy tắc QLGD |
| 3 | C | Nghiên cứu sinh | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `TRINH_DO_DAO_TAO_ID` | `DM_TRINH_DO_DAO_TAO` là Tiến sĩ/Nghiên cứu sinh | `COUNT` | `[Cần mapping danh mục]` |
| 4 | D | Cao học | Number | Như trên | Như trên | Thạc sĩ/Cao học | `COUNT` | `[Cần mapping danh mục]` |
| 5 | E | Đại học | Number | Như trên | Như trên | Đại học | `COUNT` | `[Cần mapping danh mục]` |
| 6 | F | Cao đẳng | Number | Như trên | Như trên | Cao đẳng | `COUNT` | `[Cần mapping danh mục]` |
| 7 | G | Trung cấp | Number | Như trên | Như trên | Trung cấp | `COUNT` | `[Cần mapping danh mục]` |
| 8 | H | BDNV sư phạm | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `NGHIEP_VU_SU_PHAM_ID` | Có NVSP hoặc danh mục Bồi dưỡng | `COUNT` | Có thể tính người có phát sinh trong kỳ |
| 9 | I | BDNVQLGD | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID` | Có NVQLGD hoặc danh mục Bồi dưỡng | `COUNT` | |
| 10 | J | Bồi dưỡng chức danh | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH`, `KET_QUA_BOI_DUONG_TAP_HUAN` | `CAN_BO_NHA_GIAO_ID`, `TEN_CHUONG_TRINH` | Chương trình/chuyên ngành là bồi dưỡng chức danh | `COUNT` | `[Cần xác nhận]` chưa có mã loại riêng |
| 11 | K | Bồi dưỡng tin học | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `TRINH_DO_TIN_HOC_ID` | Có trình độ/chứng chỉ tin học phát sinh | `COUNT` | |
| 12 | L | Bồi dưỡng ngoại ngữ | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `TRINH_DO_NGOAI_NGU_ID` | Có trình độ/chứng chỉ ngoại ngữ phát sinh | `COUNT` | |
| 13 | M | Cao cấp LLCT | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `TRINH_DO_LY_LUAN_CHINH_TRI_ID` | `DM_TRINH_DO_LLCT` là Cao cấp | `COUNT` | |
| 14 | N | BDNV Công an 6 tháng | Number | `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `TRINH_DO_NGHIEP_VU_CONG_AN_ID` | `DM_TRINH_DO_NGHIEP_VU_CA` có nhóm/ten 6 tháng | `COUNT` | `[Cần mapping danh mục]` |
| 15 | O | Các loại hình khác | Number | `KET_QUA_BOI_DUONG_TAP_HUAN`, `BOI_DUONG_TAP_HUAN` hoặc `QUA_TRINH_BOI_DUONG_CHUC_DANH` | Nhiều cột | Không thuộc C:N | `COUNT` | `[Cần xác nhận]` |
| 16 | P | Ghi chú | Text | Không áp dụng | Không áp dụng | Theo người lập báo cáo | Nhập tay | Không phải số liệu tổng hợp |

---

## 7. Mapping dòng báo cáo

| STT | Row code | Tên dòng báo cáo | Parent row | Điều kiện nghiệp vụ | Mapping DB | Ghi chú |
|---:|---|---|---|---|---|---|
| 1 | TOTAL | Tổng |  | Tổng toàn báo cáo | Tổng `GIAO_VIEN`, `CAN_BO_QLGD`, `CAN_BO_KHAC` | Dòng 12 Excel |
| 2 | GIAO_VIEN | Giáo viên | TOTAL | Nhà giáo/giáo viên được cử đi đào tạo, bồi dưỡng | `CAN_BO_NHA_GIAO.PHAN_LOAI = 1` `[Suy luận]` hoặc chức danh giảng viên/giáo viên | Cần xác nhận phân loại chính thức |
| 3 | CAN_BO_QLGD | Cán bộ quản lý giáo dục | TOTAL | Cán bộ có chức danh/công việc QLGD | `DM_CHUC_DANH.TEN = 'Cán bộ quản lý giáo dục'` hoặc `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID IS NOT NULL` `[Cần xác nhận]` | Ưu tiên chức danh hiện hành |
| 4 | CAN_BO_KHAC | Cán bộ khác | TOTAL | Cán bộ không thuộc giáo viên và không thuộc QLGD | `CAN_BO_NHA_GIAO.PHAN_LOAI = 2` trừ QLGD | `[Suy luận]` |

---

## 8. Mapping cột báo cáo

| STT | Column code | Tên cột Excel | Nhóm cột | Công thức | Bảng/cột nguồn | Ghi chú |
|---:|---|---|---|---|---|---|
| 1 | NCS | Nghiên cứu sinh | Đào tạo trình độ | Count cán bộ có trình độ/khóa tiến sĩ | `TRINH_DO_DAO_TAO_ID` | Có thể tương ứng Tiến sĩ |
| 2 | CAO_HOC | Cao học | Đào tạo trình độ | Count cán bộ cao học/thạc sĩ | `TRINH_DO_DAO_TAO_ID` | |
| 3 | DAI_HOC | Đại học | Đào tạo trình độ | Count cán bộ đại học | `TRINH_DO_DAO_TAO_ID` | |
| 4 | CAO_DANG | Cao đẳng | Đào tạo trình độ | Count cán bộ cao đẳng | `TRINH_DO_DAO_TAO_ID` | |
| 5 | TRUNG_CAP | Trung cấp | Đào tạo trình độ | Count cán bộ trung cấp | `TRINH_DO_DAO_TAO_ID` | |
| 6 | BDNV_SU_PHAM | BDNV sư phạm | Bồi dưỡng nghiệp vụ | Count cán bộ có bồi dưỡng sư phạm | `NGHIEP_VU_SU_PHAM_ID` | |
| 7 | BDNV_QLGD | BDNVQLGD | Bồi dưỡng nghiệp vụ | Count cán bộ có bồi dưỡng QLGD | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID` | |
| 8 | BD_CHUC_DANH | Bồi dưỡng chức danh | Bồi dưỡng chức danh | Count chương trình/chuyên ngành bồi dưỡng chức danh | `BOI_DUONG_TAP_HUAN.TEN_CHUONG_TRINH`, `QUA_TRINH_BOI_DUONG_CHUC_DANH` | `[Cần xác nhận]` |
| 9 | BD_TIN_HOC | Bồi dưỡng tin học | Bồi dưỡng năng lực | Count cán bộ có bồi dưỡng tin học | `TRINH_DO_TIN_HOC_ID` | |
| 10 | BD_NGOAI_NGU | Bồi dưỡng ngoại ngữ | Bồi dưỡng năng lực | Count cán bộ có bồi dưỡng ngoại ngữ | `TRINH_DO_NGOAI_NGU_ID` | |
| 11 | CC_LLCT | Cao cấp lý luận chính trị | LLCT | Count cán bộ có cao cấp LLCT | `TRINH_DO_LY_LUAN_CHINH_TRI_ID` | |
| 12 | BDNV_CA_6_THANG | BDNV Công an 6 tháng | Nghiệp vụ Công an | Count cán bộ NVCA 6 tháng | `TRINH_DO_NGHIEP_VU_CONG_AN_ID` | |
| 13 | KHAC | Các loại hình khác | Khác | Count loại hình không thuộc các cột trên | Nhiều nguồn | `[Cần xác nhận]` |

---

## 9. Công thức tính

### 9.1 Công thức tổng quát

```text
Số liệu từng ô = COUNT bản ghi đào tạo/bồi dưỡng hoặc COUNT DISTINCT cán bộ
WHERE kỳ phát sinh nằm trong :fromDate - :toDate
  AND MA_DON_VI = :maDonVi
  AND WORKFLOW_STATUS = 'Approved'
  AND nhóm đối tượng = row_code
  AND loại hình đào tạo/bồi dưỡng = column_code
```

`[Cần xác nhận]` Nếu báo cáo yêu cầu đếm số lượt cử đi thì dùng `COUNT(training_event_id)`. Nếu yêu cầu đếm số người thì dùng `COUNT(DISTINCT can_bo_nha_giao_id)`.

### 9.2 Công thức theo dòng

| Dòng | Điều kiện |
|---|---|
| Giáo viên | `CAN_BO_NHA_GIAO.PHAN_LOAI = 1` hoặc chức danh thuộc nhóm giảng viên/giáo viên |
| Cán bộ QLGD | Chức danh hiện hành là Cán bộ quản lý giáo dục hoặc thuộc nhóm QLGD `[Cần xác nhận]` |
| Cán bộ khác | Cán bộ còn lại sau khi loại Giáo viên và Cán bộ QLGD |
| Tổng | Tổng ba dòng con |

### 9.3 Công thức theo cột

| Cột | Điều kiện |
|---|---|
| Nghiên cứu sinh | `DM_TRINH_DO_DAO_TAO.TEN` chứa Tiến sĩ/Nghiên cứu sinh |
| Cao học | `DM_TRINH_DO_DAO_TAO.TEN` chứa Thạc sĩ/Cao học |
| Đại học/Cao đẳng/Trung cấp | `DM_TRINH_DO_DAO_TAO.TEN` tương ứng |
| BDNV sư phạm | `NGHIEP_VU_SU_PHAM_ID IS NOT NULL` hoặc chương trình thuộc NVSP |
| BDNVQLGD | `NGHIEP_VU_QUAN_LY_GIAO_DUC_ID IS NOT NULL` hoặc chương trình thuộc NVQLGD |
| Bồi dưỡng chức danh | Tên/nội dung chương trình hoặc chuyên ngành đào tạo chứa “chức danh” `[Cần xác nhận]` |
| Bồi dưỡng tin học | `TRINH_DO_TIN_HOC_ID IS NOT NULL` |
| Bồi dưỡng ngoại ngữ | `TRINH_DO_NGOAI_NGU_ID IS NOT NULL` |
| Cao cấp LLCT | `DM_TRINH_DO_LLCT.TEN` chứa “Cao cấp” |
| BDNV Công an 6 tháng | `DM_TRINH_DO_NGHIEP_VU_CA.TEN` hoặc `NHOM_TRINH_DO` chứa “6 tháng” |
| Khác | Không khớp các điều kiện trên |

---

## 10. Proc SQL đề xuất

```sql
CREATE OR REPLACE PROCEDURE PROC_RPT_2H (
    P_NAM_BAO_CAO IN NUMBER,
    P_TU_NGAY     IN DATE DEFAULT NULL,
    P_DEN_NGAY    IN DATE DEFAULT NULL,
    P_MA_DON_VI   IN VARCHAR2,
    P_COUNT_MODE  IN VARCHAR2 DEFAULT 'LUOT',
    P_RESULT      OUT SYS_REFCURSOR
)
AS
BEGIN
    OPEN P_RESULT FOR
        WITH params AS (
            SELECT
                NVL(P_TU_NGAY, TO_DATE(P_NAM_BAO_CAO || '-01-01', 'YYYY-MM-DD')) AS tu_ngay,
                NVL(P_DEN_NGAY, TO_DATE(P_NAM_BAO_CAO || '-12-31', 'YYYY-MM-DD')) AS den_ngay
            FROM dual
        ),
        report_rows AS (
            SELECT 'GIAO_VIEN' AS row_code, 'Giáo viên' AS row_name, 10 AS sort_order FROM dual
            UNION ALL SELECT 'CAN_BO_QLGD', 'Cán bộ quản lý giáo dục', 20 FROM dual
            UNION ALL SELECT 'CAN_BO_KHAC', 'Cán bộ khác', 30 FROM dual
            UNION ALL SELECT 'TOTAL', 'Tổng', 999 FROM dual
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
        training_events AS (
            SELECT
                bd.ID AS event_id,
                bd.CAN_BO_NHA_GIAO_ID,
                bd.MA_DON_VI,
                bd.THOI_GIAN_AP_DUNG AS event_date,
                td.TEN AS ten_trinh_do,
                llct.TEN AS ten_llct,
                nvca.TEN AS ten_nvca,
                nvsp.TEN AS ten_nvsp,
                nvqlgd.TEN AS ten_nvqlgd,
                CASE
                    WHEN UPPER(NVL(td.TEN, '')) LIKE '%TIẾN SĨ%'
                      OR UPPER(NVL(td.TEN, '')) LIKE '%NGHIÊN CỨU SINH%' THEN 'NCS'
                    WHEN UPPER(NVL(td.TEN, '')) LIKE '%THẠC SĨ%'
                      OR UPPER(NVL(td.TEN, '')) LIKE '%CAO HỌC%' THEN 'CAO_HOC'
                    WHEN UPPER(NVL(td.TEN, '')) LIKE '%ĐẠI HỌC%' THEN 'DAI_HOC'
                    WHEN UPPER(NVL(td.TEN, '')) LIKE '%CAO ĐẲNG%' THEN 'CAO_DANG'
                    WHEN UPPER(NVL(td.TEN, '')) LIKE '%TRUNG CẤP%' THEN 'TRUNG_CAP'
                    WHEN bd.NGHIEP_VU_SU_PHAM_ID IS NOT NULL THEN 'BDNV_SU_PHAM'
                    WHEN bd.NGHIEP_VU_QUAN_LY_GIAO_DUC_ID IS NOT NULL THEN 'BDNV_QLGD'
                    WHEN UPPER(NVL(bd.CHUYEN_NGANH_DAO_TAO, '')) LIKE '%CHỨC DANH%'
                      OR UPPER(NVL(bd.CHUYEN_NGANH_DAO_TAO, '')) LIKE '%CHUC DANH%' THEN 'BD_CHUC_DANH'
                    WHEN bd.TRINH_DO_TIN_HOC_ID IS NOT NULL THEN 'BD_TIN_HOC'
                    WHEN bd.TRINH_DO_NGOAI_NGU_ID IS NOT NULL THEN 'BD_NGOAI_NGU'
                    WHEN UPPER(NVL(llct.TEN, '')) LIKE '%CAO CẤP%' THEN 'CC_LLCT'
                    WHEN UPPER(NVL(nvca.TEN, '') || ' ' || NVL(nvca.NHOM_TRINH_DO, '')) LIKE '%6 THÁNG%' THEN 'BDNV_CA_6_THANG'
                    ELSE 'KHAC'
                END AS column_code
            FROM X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH bd
            LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td ON td.ID = bd.TRINH_DO_DAO_TAO_ID
            LEFT JOIN X02_DM.DM_TRINH_DO_LLCT llct ON llct.ID = bd.TRINH_DO_LY_LUAN_CHINH_TRI_ID
            LEFT JOIN X02_DM.DM_TRINH_DO_NGHIEP_VU_CA nvca ON nvca.ID = bd.TRINH_DO_NGHIEP_VU_CONG_AN_ID
            LEFT JOIN X02_DM.DM_NGHIEP_VU_SU_PHAM nvsp ON nvsp.ID = bd.NGHIEP_VU_SU_PHAM_ID
            LEFT JOIN X02_DM.DM_NGHIEP_VU_QUAN_LY_GIAO_DUC nvqlgd ON nvqlgd.ID = bd.NGHIEP_VU_QUAN_LY_GIAO_DUC_ID
            JOIN params p ON 1 = 1
            WHERE NVL(bd.IS_DELETED, 0) = 0
              AND NVL(bd.IS_ACTIVE, 1) = 1
              AND bd.WORKFLOW_STATUS = 'Approved'
              AND (P_MA_DON_VI IS NULL OR bd.MA_DON_VI = P_MA_DON_VI)
              AND bd.THOI_GIAN_AP_DUNG BETWEEN p.tu_ngay AND p.den_ngay
        ),
        event_with_object AS (
            SELECT
                e.*,
                CASE WHEN UPPER(P_COUNT_MODE) = 'NGUOI'
                     THEN TO_CHAR(e.CAN_BO_NHA_GIAO_ID)
                     ELSE TO_CHAR(e.event_id)
                END AS count_key,
                CASE
                    WHEN UPPER(NVL(cd.TEN, '')) LIKE '%QUẢN LÝ GIÁO DỤC%' THEN 'CAN_BO_QLGD'
                    WHEN cb.PHAN_LOAI = 1 THEN 'GIAO_VIEN'
                    WHEN cb.PHAN_LOAI = 2 THEN 'CAN_BO_KHAC'
                    ELSE 'CAN_BO_KHAC'
                END AS row_code
            FROM training_events e
            JOIN X02_APP.CAN_BO_NHA_GIAO cb ON cb.ID = e.CAN_BO_NHA_GIAO_ID
            LEFT JOIN latest_cong_tac qt ON qt.CAN_BO_NHA_GIAO_ID = cb.ID
            LEFT JOIN X02_DM.DM_CHUC_DANH cd ON cd.ID = qt.CHUC_DANH_ID
            WHERE NVL(cb.IS_DELETED, 0) = 0
              AND NVL(cb.IS_ACTIVE, 1) = 1
              AND cb.WORKFLOW_STATUS = 'Approved'
        ),
        agg AS (
            SELECT
                row_code,
                COUNT(DISTINCT count_key) AS total_count,
                COUNT(DISTINCT CASE WHEN column_code = 'NCS' THEN count_key END) AS ncs,
                COUNT(DISTINCT CASE WHEN column_code = 'CAO_HOC' THEN count_key END) AS cao_hoc,
                COUNT(DISTINCT CASE WHEN column_code = 'DAI_HOC' THEN count_key END) AS dai_hoc,
                COUNT(DISTINCT CASE WHEN column_code = 'CAO_DANG' THEN count_key END) AS cao_dang,
                COUNT(DISTINCT CASE WHEN column_code = 'TRUNG_CAP' THEN count_key END) AS trung_cap,
                COUNT(DISTINCT CASE WHEN column_code = 'BDNV_SU_PHAM' THEN count_key END) AS bdnv_su_pham,
                COUNT(DISTINCT CASE WHEN column_code = 'BDNV_QLGD' THEN count_key END) AS bdnv_qlgd,
                COUNT(DISTINCT CASE WHEN column_code = 'BD_CHUC_DANH' THEN count_key END) AS bd_chuc_danh,
                COUNT(DISTINCT CASE WHEN column_code = 'BD_TIN_HOC' THEN count_key END) AS bd_tin_hoc,
                COUNT(DISTINCT CASE WHEN column_code = 'BD_NGOAI_NGU' THEN count_key END) AS bd_ngoai_ngu,
                COUNT(DISTINCT CASE WHEN column_code = 'CC_LLCT' THEN count_key END) AS cc_llct,
                COUNT(DISTINCT CASE WHEN column_code = 'BDNV_CA_6_THANG' THEN count_key END) AS bdnv_ca_6_thang,
                COUNT(DISTINCT CASE WHEN column_code = 'KHAC' THEN count_key END) AS khac
            FROM event_with_object
            GROUP BY row_code
        ),
        agg_total AS (
            SELECT * FROM agg
            UNION ALL
            SELECT
                'TOTAL',
                SUM(total_count),
                SUM(ncs),
                SUM(cao_hoc),
                SUM(dai_hoc),
                SUM(cao_dang),
                SUM(trung_cap),
                SUM(bdnv_su_pham),
                SUM(bdnv_qlgd),
                SUM(bd_chuc_danh),
                SUM(bd_tin_hoc),
                SUM(bd_ngoai_ngu),
                SUM(cc_llct),
                SUM(bdnv_ca_6_thang),
                SUM(khac)
            FROM agg
        )
        SELECT
            rr.row_code,
            rr.row_name,
            rr.sort_order,
            NVL(a.ncs, 0) AS nghien_cuu_sinh,
            NVL(a.cao_hoc, 0) AS cao_hoc,
            NVL(a.dai_hoc, 0) AS dai_hoc,
            NVL(a.cao_dang, 0) AS cao_dang,
            NVL(a.trung_cap, 0) AS trung_cap,
            NVL(a.bdnv_su_pham, 0) AS bdnv_su_pham,
            NVL(a.bdnv_qlgd, 0) AS bdnv_qlgd,
            NVL(a.bd_chuc_danh, 0) AS bd_chuc_danh,
            NVL(a.bd_tin_hoc, 0) AS bd_tin_hoc,
            NVL(a.bd_ngoai_ngu, 0) AS bd_ngoai_ngu,
            NVL(a.cc_llct, 0) AS cao_cap_llct,
            NVL(a.bdnv_ca_6_thang, 0) AS bdnv_ca_6_thang,
            NVL(a.khac, 0) AS loai_hinh_khac,
            CAST(NULL AS VARCHAR2(1000)) AS ghi_chu
        FROM report_rows rr
        LEFT JOIN agg_total a ON a.row_code = rr.row_code
        ORDER BY rr.sort_order;
END;
/
```

Ghi chú SQL:

- Skeleton ưu tiên `QUA_TRINH_BOI_DUONG_CHUC_DANH` vì bảng này có đủ các cột trình độ, LLCT, ngoại ngữ, tin học, NVCA, NVSP, NVQLGD.
- Nếu nghiệp vụ yêu cầu lấy “được cử đi” theo chương trình/lớp thay vì hồ sơ quá trình, cần bổ sung union từ `KET_QUA_BOI_DUONG_TAP_HUAN` + `BOI_DUONG_TAP_HUAN`, hoặc từ `NGUOI_HOC_TRONG_NUOC_DI_HOC_NUOC_NGOAI` + `LOP_DAO_TAO_BOI_DUONG_QT`.
- Cột `BD_CHUC_DANH` đang được phân loại tạm bằng `QUA_TRINH_BOI_DUONG_CHUC_DANH.CHUYEN_NGANH_DAO_TAO` chứa "chức danh"; cần nghiệp vụ xác nhận hoặc thay bằng mã danh mục chính thức nếu có.

### Query chi tiết nguồn dữ liệu

```sql
SELECT
    bd.ID AS event_id,
    cb.ID AS can_bo_nha_giao_id,
    cn.HO_TEN,
    cb.PHAN_LOAI,
    cd.TEN AS chuc_danh,
    bd.THOI_GIAN_AP_DUNG,
    td.TEN AS trinh_do_dao_tao,
    llct.TEN AS trinh_do_llct,
    nvca.TEN AS trinh_do_nghiep_vu_ca,
    nvsp.TEN AS nghiep_vu_su_pham,
    nvqlgd.TEN AS nghiep_vu_qlgd,
    bd.TRUONG_DAO_TAO,
    bd.DIA_DIEM_DAO_TAO
FROM X02_APP.QUA_TRINH_BOI_DUONG_CHUC_DANH bd
JOIN X02_APP.CAN_BO_NHA_GIAO cb ON cb.ID = bd.CAN_BO_NHA_GIAO_ID
JOIN X02_APP.CON_NGUOI cn ON cn.ID = cb.CON_NGUOI_ID
LEFT JOIN X02_APP.QUA_TRINH_GIANG_DAY_CONG_TAC qt ON qt.CAN_BO_NHA_GIAO_ID = cb.ID
LEFT JOIN X02_DM.DM_CHUC_DANH cd ON cd.ID = qt.CHUC_DANH_ID
LEFT JOIN X02_DM.DM_TRINH_DO_DAO_TAO td ON td.ID = bd.TRINH_DO_DAO_TAO_ID
LEFT JOIN X02_DM.DM_TRINH_DO_LLCT llct ON llct.ID = bd.TRINH_DO_LY_LUAN_CHINH_TRI_ID
LEFT JOIN X02_DM.DM_TRINH_DO_NGHIEP_VU_CA nvca ON nvca.ID = bd.TRINH_DO_NGHIEP_VU_CONG_AN_ID
LEFT JOIN X02_DM.DM_NGHIEP_VU_SU_PHAM nvsp ON nvsp.ID = bd.NGHIEP_VU_SU_PHAM_ID
LEFT JOIN X02_DM.DM_NGHIEP_VU_QUAN_LY_GIAO_DUC nvqlgd ON nvqlgd.ID = bd.NGHIEP_VU_QUAN_LY_GIAO_DUC_ID
WHERE bd.MA_DON_VI = :maDonVi
  AND bd.WORKFLOW_STATUS = 'Approved'
  AND NVL(bd.IS_DELETED, 0) = 0
  AND bd.THOI_GIAN_AP_DUNG BETWEEN :tuNgay AND :denNgay;
```

---

## 11. API đề xuất

Frontend registry hiện có mục “Thống kê số liệu cán bộ, giáo viên được cử đi đào tạo, bồi dưỡng”, nhưng `ReportPage` chưa có component riêng cho báo cáo này.

```http
POST /api/v1/reports/2h/query
```

Request:

```json
{
  "year": 2026,
  "fromDate": "2026-01-01",
  "toDate": "2026-05-31",
  "maDonVi": "G01.651",
  "workflowStatus": "Approved",
  "countMode": "LUOT"
}
```

Response:

```json
{
  "reportCode": "BM_2H",
  "reportName": "Thống kê số liệu cán bộ, giáo viên được cử đi đào tạo, bồi dưỡng",
  "rows": [
    {
      "rowCode": "GIAO_VIEN",
      "rowName": "Giáo viên",
      "nghienCuuSinh": 0,
      "caoHoc": 0,
      "daiHoc": 0,
      "caoDang": 0,
      "trungCap": 0,
      "bdnvSuPham": 0,
      "bdnvQlgd": 0,
      "bdChucDanh": 0,
      "bdTinHoc": 0,
      "bdNgoaiNgu": 0,
      "caoCapLlct": 0,
      "bdnvCa6Thang": 0,
      "loaiHinhKhac": 0,
      "ghiChu": null
    }
  ]
}
```

---

## 12. Quy tắc đối soát số liệu

| STT | Quy tắc đối soát | Công thức kiểm tra | Ghi chú |
|---:|---|---|---|
| 1 | Tổng từng cột bằng tổng 3 dòng con | `TOTAL.COL = GIAO_VIEN.COL + CAN_BO_QLGD.COL + CAN_BO_KHAC.COL` | Bắt buộc |
| 2 | Không có bản ghi không mapping đối tượng | `COUNT(row_code IS NULL OR row_code = 'CHUA_MAPPING') = 0` | Bắt buộc trước khi chốt |
| 3 | Không có bản ghi không mapping cột ngoài “Khác” | Bản ghi không khớp C:N phải vào `KHAC` | Bắt buộc |
| 4 | Nếu đếm người | Mỗi ô `COUNT(DISTINCT can_bo_nha_giao_id)` | Không cộng trùng một người trong cùng loại |
| 5 | Nếu đếm lượt | Mỗi ô `COUNT(DISTINCT event_id)` | Một người nhiều khóa được tính nhiều lượt |
| 6 | Dữ liệu kỳ báo cáo nằm trong filter | `event_date BETWEEN :fromDate AND :toDate` | Bắt buộc |
| 7 | Chỉ lấy dữ liệu đã duyệt | `WORKFLOW_STATUS = 'Approved'` | Bắt buộc cho báo cáo chính thức |

---

## 13. Điểm thiếu / cần xác nhận

| STT | Nội dung cần xác nhận | Lý do | Mức độ ưu tiên |
|---:|---|---|---|
| 1 | Báo cáo đếm “người” hay “lượt cử đi” | Một cán bộ có thể học nhiều khóa trong kỳ | Cao |
| 2 | Kỳ báo cáo chuẩn là năm hay đến tháng 5/2026 | Header mẫu ghi tháng 5 năm 2026 | Cao |
| 3 | Nguồn chính là kế hoạch cử đi, quá trình bồi dưỡng, hay kết quả hoàn thành | Các bảng hiện có phản ánh các lát cắt khác nhau | Cao |
| 4 | Quy tắc phân loại Giáo viên/Cán bộ QLGD/Cán bộ khác | DB có `PHAN_LOAI`, `DM_CHUC_DANH`, nhưng chưa đủ quy tắc loại trừ | Cao |
| 5 | Mã danh mục cho Nghiên cứu sinh/Cao học/Đại học/Cao đẳng/Trung cấp | SQL skeleton dùng so khớp tên | Trung bình |
| 6 | Mapping chính thức cho “Bồi dưỡng chức danh” | Chưa thấy cột/mã loại riêng trong bảng quá trình | Cao |
| 7 | Mapping “Các loại hình đào tạo, bồi dưỡng khác” | Cần danh mục loại hình chính thức để loại trừ | Trung bình |
| 8 | Có tính đào tạo/bồi dưỡng quốc tế không | Có bảng HTQT cho cán bộ/nhà giáo đi học nước ngoài | Trung bình |
| 9 | Báo cáo có cần ghi chú tự động hay nhập tay | Cột P không có công thức | Thấp |
| 10 | BCTK có template/export riêng cho 2H chưa | Chưa thấy component/data source riêng trong registry báo cáo | Trung bình |

---

## 14. Nguồn tham chiếu

- File Excel: `docs/report-input/2H.xlsx`
- Database docs: `docs/database/X02_APP.sql`, `docs/database/X02_DM.sql`
- Tài liệu nghiệp vụ: `docs/output/database-business-analysis.md`, `docs/output/business-analysis/11-reports-dashboard-analysis.md`
- Source code: `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`, `src/frontend/frontend-x02-v2/src/domains/reports/pages/ReportPage.jsx`

---

## 15. Checklist hoàn thành

| Hạng mục | Trạng thái |
|---|---|
| Đã đọc file Excel mẫu | Đã đọc `2H.xlsx` |
| Đã nhận diện tên báo cáo/mã biểu mẫu | Đã nhận diện |
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

# Báo cáo 8H - Thống kê lưu lượng học viên

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/8H.xlsx` |
| Sheet | `Luu luong` |
| Mã biểu mẫu | `Biểu mẫu 8H` |
| Tên báo cáo | `THỐNG KÊ LƯU LƯỢNG HỌC VIÊN` |
| Vùng dữ liệu có giá trị | `A1:M65` |
| Vùng bảng chính | `A5:M65` |
| Vùng style kéo dài | `A1:AB5148` |
| Công thức Excel | Có 113 công thức tổng hợp tại các dòng 9, 10, 13, 19, 37, 42, 44, 47, 53, 54, 55, 59, 65 |
| Dạng báo cáo | Ma trận số học viên theo hệ đào tạo, ngành/chuyên ngành, khóa/lưu lượng, đối tượng nhập học, giới tính và dân tộc |

`[Cần xác nhận]` Template 8H có tiêu đề là lưu lượng học viên nhưng header cột vẫn giống mẫu nhập học: `Chỉ tiêu`, `Thực nhập`, `Đối tượng nhập học`. Khi triển khai cần chốt lại: 8H có giữ khái niệm chỉ tiêu/thực nhập hay phải hiểu `D:L` là lưu lượng học viên đang học tại thời điểm báo cáo.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê lưu lượng học viên theo hệ đào tạo, trình độ, ngành/chuyên ngành, khóa học và loại hình đào tạo. Khác với 7H là báo cáo nhập học trong kỳ, 8H nên phản ánh số học viên đang thuộc lưu lượng đào tạo tại thời điểm/kỳ báo cáo.

`[Suy luận]` Với nghiệp vụ lưu lượng, nguồn chính nên là `HOC_VIEN` được lọc theo trạng thái học viên tại ngày chốt báo cáo, kết hợp `KHOA_HOC_ID`, `TRUNG_DOI_ID`, `TRANG_THAI_HOC_ID` và `HV_QUYET_DINH_TOT_NGHIEP` để loại/đối chiếu học viên đã tốt nghiệp. Tài liệu dashboard LRN cũng mô tả `tongSo` là lũy kế đến cuối năm học, `dangHoc` theo `DM_TRANG_THAI_HOC_VIEN`, `totNghiep` từ quyết định tốt nghiệp đã duyệt.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:M1` | `Biểu mẫu 8H` | Merged toàn hàng tiêu đề |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:M3` | `THỐNG KÊ LƯU LƯỢNG HỌC VIÊN` | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `C4:M4` | `(Kèm theo Báo cáo số ngày tháng 5 năm 2026)` | Merged |
| `B69:E69` | Vùng ngày lập báo cáo | Có merged nhưng không có text |
| `G69:M69`, `G73:M73`, `G74:M74` | Vùng chữ ký | Có merged nhưng không có text |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A5:A7` | `STT` | `stt` |
| `B5:B7` | `Ngành, Chuyên ngành` | `rowLabel`, `rowCode`, `parentCode` |
| `C5:C7` | `Chỉ tiêu` | `chiTieu` |
| `D5:D7` | `Thực nhập` | `[Cần xác nhận]` `thucNhap` hoặc `luuLuongThucTe` |
| `E5:J5` | `Đối tượng nhập học` | Nhóm `doiTuongNhapHoc` |
| `E6:H6` | `Trong ngành` | Nhóm con trong ngành |
| `E7` | `Cán bộ` | `canBo` |
| `F7` | `CSNV` | `csnv` |
| `G7` | `Học sinh VH` | `hocSinhVanHoa` |
| `H7` | `Học sinh PT` | `hocSinhPhoThong` |
| `I6:J6` | `Ngành ngoài` | Nhóm con ngành ngoài |
| `I7` | `BQP gửi` | `bqpGui` |
| `J7` | `Ngành khác` | `nganhKhac` |
| `K5:L5` | `Trong đó` | Nhóm thành phần |
| `K6:K7` | `Nữ` | `nu` |
| `L6:L7` | `DTTS` | `danTocThieuSo` |
| `M5:M7` | `Ghi chú` | `ghiChu` |

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 9 |  | Tổng số | `tongSo` | Tổng row 10, 37, 40, 42, 53, 65 |
| 10 | I | Hệ đào tạo giáo dục chính quy | `heDaoTaoGiaoDucChinhQuy` | Tổng tiến sĩ, thạc sĩ, đại học chính quy |
| 11 | 1.1 | Đào tạo trình độ tiến sĩ | `daoTaoTienSi` | `TRINH_DO_DAO_TAO_ID = tiến sĩ` |
| 12 |  | NCS 23, 24, 25, 26, 27, 28, 29 | `ncsKhoa23Den29` | `[Cần mapping danh mục]` `KHOA_HOC_ID` hoặc mã khóa/chương trình nghiên cứu sinh |
| 13 | 1.2 | Đào tạo trình độ thạc sĩ | `daoTaoThacSi` | Tổng row 14-18 theo chuyên ngành |
| 14 |  | Trinh sát an ninh | `thsTrinhSatAnNinh` | Thạc sĩ, chuyên ngành tương ứng |
| 15 |  | Điều tra hình sự | `thsDieuTraHinhSu` | Thạc sĩ, chuyên ngành tương ứng |
| 16 |  | Quản lý nhà nước về ANTT | `thsQlNnAntt` | Thạc sĩ, chuyên ngành tương ứng |
| 17 |  | Tội phạm học và phòng ngừa tội phạm | `thsToiPhamHocPhongNgua` | Thạc sĩ, chuyên ngành tương ứng |
| 18 |  | An ninh phi truyền thống | `thsAnNinhPhiTruyenThong` | Thạc sĩ, chuyên ngành tương ứng |
| 19 | 1.3 | Đào tạo trình độ đại học | `daoTaoDaiHocChinhQuy` | Tổng các nhóm ngành đại học row 20, 21, 27, 33, 36 |
| 20 |  | Nghiệp vụ an ninh (D56 chưa phân chuyên ngành) | `dhNghiepVuAnNinhD56ChuaPhanCn` | `[Cần xác nhận]` Khóa D56/chưa phân chuyên ngành |
| 21 |  | Trinh sát an ninh | `dhTrinhSatAnNinh` | Dòng nhóm; template không tự cộng row 22-26 |
| 22 |  | Trinh sát an ninh | `dhTsAnNinh` | Chuyên ngành |
| 23 |  | Chương trình đào tạo TSAN CLC | `dhTsAnNinhClc` | `[Cần mapping danh mục]` Chương trình chất lượng cao |
| 24 |  | Trinh sát phản gián | `dhTrinhSatPhanGian` | Chuyên ngành |
| 25 |  | Trinh sát bảo vệ an ninh xã hội | `dhTsBaoVeAnNinhXaHoi` | Chuyên ngành |
| 26 |  | Trinh sát bảo vệ an ninh nội bộ | `dhTsBaoVeAnNinhNoiBo` | Chuyên ngành |
| 27 |  | Điều tra hình sự | `dhDieuTraHinhSu` | Dòng nhóm; template không tự cộng row 28-32 |
| 28 |  | Điều tra hình sự | `dhDieuTraHinhSuChung` | Chuyên ngành |
| 29 |  | An ninh điều tra | `dhAnNinhDieuTra` | Chuyên ngành |
| 30 |  | Điều tra tội phạm trật tự xã hội | `dhDieuTraTtxh` | Chuyên ngành |
| 31 |  | Điều tra tội phạm ma túy | `dhDieuTraMaTuy` | Chuyên ngành |
| 32 |  | Điều tra tội phạm kinh tế, môi trường | `dhDieuTraKtmt` | Chuyên ngành |
| 33 |  | An toàn thông tin | `dhAnToanThongTin` | Dòng nhóm; template không tự cộng row 34-35 |
| 34 |  | An ninh mạng và phòng, chống TP sử dụng công nghệ cao | `dhAnNinhMangPctpCnCao` | Chuyên ngành |
| 35 |  | Công nghệ thông tin | `dhCongNgheThongTin` | Chuyên ngành |
| 36 |  | Quản lý xuất nhập cảnh nước ngoài | `dhQlXuatNhapCanhNuocNgoai` | `[Cần mapping danh mục]` |
| 37 | 2 | Đào tạo trình độ đại học hình thức vừa làm vừa học | `daiHocVlvh` | Đại học, hình thức VLVH |
| 38 |  | Đào tạo tại trường công an | `daiHocVlvhTaiTruong` | Theo cơ sở/trường tổ chức |
| 39 |  | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `daiHocVlvhLienKet` | Theo loại hình liên kết/địa bàn |
| 40 | 3 | Hệ cử tuyển | `heCuTuyen` | `[Cần mapping danh mục]` |
| 41 |  | Đại học | `cuTuyenDaiHoc` | Cử tuyển trình độ đại học |
| 42 | 4 | Hệ liên thông | `heLienThong` | Tổng row 43 và 50; cột C thiếu công thức |
| 43 | 4.1 | Đào tạo tại trường Công an nhân dân | `lienThongTaiTruongCand` | Nhóm row 44-49 |
| 44 |  | Hình thức chính quy | `lienThongChinhQuy` | Tổng row 45-46 |
| 45 |  | Trung cấp lên Đại học | `lienThongTcLenDhChinhQuy` | `[Cần xác nhận]` Cần trường trình độ đầu vào |
| 46 |  | Cao đẳng lên Đại học | `lienThongCdLenDhChinhQuy` | `[Cần xác nhận]` |
| 47 |  | Hình thức vừa làm vừa học | `lienThongVlvh` | Row 48; row 49 không được cộng theo công thức |
| 48 |  | Trung cấp lên Đại học | `lienThongTcLenDhVlvh` | `[Cần xác nhận]` |
| 49 |  | Cao đẳng lên Đại học | `lienThongCdLenDhVlvh` | `[Cần xác nhận]` Template không cộng vào row 47 |
| 50 | 4.2 | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `lienThongLienKet` | Nhóm row 51-52 |
| 51 |  | Trung cấp lên Đại học | `lienThongLienKetTcLenDh` | `[Cần xác nhận]` |
| 52 |  | Cao đẳng lên Đại học | `lienThongLienKetCdLenDh` | `[Cần xác nhận]` |
| 53 | 5 | Các loại hình đào tạo khác | `loaiHinhDaoTaoKhac` | Tổng row 54 và 59; cột C thiếu công thức |
| 54 | 5.1 | Đào tạo cấp bằng đại học thứ 2 | `daiHocThu2` | Tổng row 55 và 58; cột C thiếu công thức |
| 55 |  | Đào tạo tại trường | `daiHocThu2TaiTruong` | Tổng row 56-57; cột C thiếu công thức |
| 56 |  | Chính quy | `daiHocThu2ChinhQuy` | `[Cần mapping danh mục]` |
| 57 |  | Vừa làm vừa học | `daiHocThu2Vlvh` | `[Cần mapping danh mục]` |
| 58 |  | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `daiHocThu2LienKet` | `[Cần xác nhận]` |
| 59 | 5.2 | Đào tạo lý luận chính trị | `daoTaoLyLuanChinhTri` | Tổng row 60 và 63 |
| 60 |  | Đào tạo cao cấp lý luận chính trị | `llctCaoCap` | Nhóm row 61-62 nhưng template chỉ cộng dòng 60 lên row 59 |
| 61 |  | Hệ tập trung | `llctCaoCapTapTrung` | `[Cần xác nhận]` |
| 62 |  | Hệ không tập trung | `llctCaoCapKhongTapTrung` | `[Cần xác nhận]` |
| 63 |  | Đào tạo trung cấp lý luận chính trị | `llctTrungCap` | Nhóm row 64 nhưng template chỉ cộng dòng 63 lên row 59 |
| 64 |  | Hệ tập trung | `llctTrungCapTapTrung` | `[Cần xác nhận]`; chưa có dòng hệ không tập trung |
| 65 | II | Các loại hình bồi dưỡng | `cacLoaiHinhBoiDuong` | Công thức tham chiếu row 67 nhưng row 67 trống |

## 5. Mapping cột giá trị

| Cột | Header Excel | Field đề xuất | Mapping DB đề xuất |
|---|---|---|---|
| `C` | Chỉ tiêu | `chiTieu` | `[Cần xác nhận]` Có thể lấy từ `CHI_TIEU_TUYEN_SINH*`; với báo cáo lưu lượng có thể không cần chỉ tiêu |
| `D` | Thực nhập | `luuLuong` / `thucNhap` | `[Suy luận]` Đếm `HOC_VIEN.ID` đang thuộc lưu lượng tại `denNgay` |
| `E` | Cán bộ | `canBo` | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID -> DM_DOI_TUONG_NHAP_HOC` |
| `F` | CSNV | `csnv` | Chiến sĩ nghĩa vụ `[Cần mapping danh mục]` |
| `G` | Học sinh VH | `hocSinhVanHoa` | Học sinh văn hóa `[Cần mapping danh mục]` |
| `H` | Học sinh PT | `hocSinhPhoThong` | Học sinh phổ thông `[Cần mapping danh mục]` |
| `I` | BQP gửi | `bqpGui` | Đối tượng/ngành ngoài Bộ Quốc phòng gửi |
| `J` | Ngành khác | `nganhKhac` | Đối tượng ngành khác |
| `K` | Nữ | `nu` | `CON_NGUOI.GIOI_TINH` chuẩn hóa về nữ |
| `L` | DTTS | `danTocThieuSo` | `CON_NGUOI.DAN_TOC_ID`, loại trừ dân tộc Kinh hoặc theo danh mục DTTS chính thức |
| `M` | Ghi chú | `ghiChu` | Text nhập tay |

`[Cần xác nhận]` Nếu giữ nguyên cột `Thực nhập`, cần phân biệt với mẫu 7H: 7H đếm nhập học trong kỳ, còn 8H nên đếm học viên đang học/lưu lượng tại ngày chốt. Không nên dùng cùng logic `NGAY_NHAP_HOC BETWEEN tuNgay AND denNgay` cho cả 7H và 8H.

## 6. Công thức Excel trong template

| Dòng | Ý nghĩa | Công thức chính |
|---:|---|---|
| 9 | Tổng số | Cộng row 10, 37, 40, 42, 53, 65 trên cột C:L |
| 10 | Hệ đào tạo giáo dục chính quy | Cộng row 11, 19, 13 |
| 13 | Thạc sĩ | Cột C/D/E/K/L cộng row 14-18; cột F:J thiếu công thức |
| 19 | Đại học | Cộng row 20, 21, 27, 33, 36; các dòng 21/27/33 là dòng nhóm nhưng không tự cộng dòng con |
| 37 | Đại học VLVH | Cột C/D/E/K/L cộng row 38-39; cột F:J thiếu công thức |
| 42 | Hệ liên thông | Cột D:L cộng row 43 và 50; cột C thiếu công thức |
| 44 | Liên thông chính quy | Cột D:L cộng row 45-46; cột C thiếu công thức |
| 47 | Liên thông VLVH | Cột D:L bằng row 48; row 49 không được cộng |
| 53 | Các loại hình đào tạo khác | Cột D:L cộng row 54 và 59; cột C thiếu công thức |
| 54 | Đại học thứ 2 | Cột D:L cộng row 55 và 58; cột C thiếu công thức |
| 55 | Đại học thứ 2 tại trường | Cột D:L cộng row 56-57; cột C thiếu công thức |
| 59 | Lý luận chính trị | Cột D:L cộng row 60 và 63; các dòng 61-62, 64 không tự cộng lên dòng cha |
| 65 | Các loại hình bồi dưỡng | Cộng row 67, nhưng row 67 trống |

`[Cần xác nhận]` Công thức 8H có nhiều điểm giống template chưa hoàn thiện: thiếu công thức ở cột C/F:J tại một số dòng, dòng con không cộng về dòng cha, và row 65 tham chiếu row 67 trống. Khi triển khai nên cấu hình cây dòng trong code/DB thay vì phụ thuộc công thức Excel nguyên trạng.

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HOC_VIEN` / phân hệ `LRN` | Nguồn chính để đếm lưu lượng học viên | `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `LOAI_HINH_DAO_TAO_ID`, `NGANH_ID`, `CHUYEN_NGANH_ID`, `KHOA_HOC_ID`, `TRUNG_DOI_ID`, `NGAY_NHAP_HOC`, `TRANG_THAI_HOC_ID`, `DOI_TUONG_NHAP_HOC_ID`, `CO_SO_DAO_TAO_ID`, `MA_DON_VI` |
| `X02_APP.CON_NGUOI` | Nguồn giới tính, dân tộc | `GIOI_TINH`, `DAN_TOC_ID` |
| `X02_DM.DM_TRANG_THAI_HOC_VIEN` | Xác định học viên còn trong lưu lượng | `Đang học`, `Bảo lưu`, `Gia hạn`, `Chuyển đến`; loại trừ/đối chiếu `Thôi học`, `Buộc thôi học`, `Đã tốt nghiệp` `[Cần xác nhận]` |
| `X02_APP.HV_QUYET_DINH_TOT_NGHIEP` | Đối chiếu học viên tốt nghiệp | `HOC_VIEN_ID`, `QUYET_DINH_TOT_NGHIEP_ID`, `WORKFLOW_STATUS` |
| `X02_APP.HV_TD_BIEN_DONG` | Ghi nhận biến động như chuyển trung đội, nghỉ học, buộc thôi học | `HOC_VIEN_ID`, `LOAI_BIEN_DONG_ID`, `NGAY_CHUYEN`, `TRUNG_DOI_CHUYEN_DEN_ID` |
| `X02_DM.DM_HV_LOAI_BIEN_DONG` | Mapping loại biến động | `Chuyển trung đội`, `Nghỉ học`, `Buộc thôi học (P3)` |
| `X02_DM.DM_KHOA_HOC` | Mapping khóa học/lưu lượng theo khóa | `MA_KHOA`, `TEN_KHOA`, `NAM_BAT_DAU`, `NAM_KET_THUC` |
| `X02_APP.TRUNG_DOI`, `X02_APP.HOC_VIEN_TRUNG_DOI` | Mapping lớp/trung đội, năm học | `KHOA_ID`, `NAM_HOC`, `TRANG_THAI_HOC_ID`, `NAM_HOC_ID` |
| `X02_APP.CHI_TIEU_TUYEN_SINH`, `CHI_TIEU_TUYEN_SINH_CHI_TIET` | Nguồn cột `Chỉ tiêu` nếu vẫn giữ | `NAM_TUYEN_SINH_ID`, `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `TONG_SO` |

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | `HOC_VIEN.MA_DON_VI`, scope theo quyền user |
| `namHocId` | String | `HOC_VIEN_TRUNG_DOI.NAM_HOC_ID` nếu thống kê theo năm học |
| `denNgay` | Date | Ngày chốt lưu lượng; `NGAY_NHAP_HOC <= denNgay` |
| `tuNgay` | Date | Chỉ cần nếu báo cáo yêu cầu biến động trong kỳ |
| `coSoDaoTaoId` | String | `HOC_VIEN.CO_SO_DAO_TAO_ID` |
| `khoaHocId` | String | `HOC_VIEN.KHOA_HOC_ID` hoặc `TRUNG_DOI.KHOA_ID` |
| `trangThaiHocIds` | String[] | Mặc định nhóm đang thuộc lưu lượng `[Cần xác nhận]` |
| `workflowStatus` | String | Mặc định `Approved` với bảng có workflow |

`[Cần xác nhận]` Cần chốt trạng thái nào được tính vào lưu lượng: chỉ `Đang học`, hay bao gồm `Bảo lưu`, `Gia hạn`, `Chuyển đến`. Nếu báo cáo là lưu lượng tại thời điểm, không nên lọc theo `NGAY_NHAP_HOC` trong kỳ như báo cáo nhập học.

## 9. API report đề xuất

```http
GET /api/v1/reports/8h/luu-luong-hoc-vien
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namHocId` | Không | Dùng nếu thống kê theo năm học |
| `denNgay` | Có | Ngày chốt lưu lượng |
| `coSoDaoTaoId` | Không | Lọc cơ sở đào tạo |
| `khoaHocId` | Không | Lọc khóa học |
| `includeBaoLuu` | Không | Mặc định cần xác nhận |

Response đề xuất:

```json
{
  "reportCode": "8H",
  "title": "Thống kê lưu lượng học viên",
  "filters": {
    "maDonVi": "T01",
    "namHocId": "NH2026",
    "denNgay": "2026-05-31"
  },
  "columns": [
    "rowCode",
    "rowLabel",
    "chiTieu",
    "luuLuong",
    "canBo",
    "csnv",
    "hocSinhVanHoa",
    "hocSinhPhoThong",
    "bqpGui",
    "nganhKhac",
    "nu",
    "danTocThieuSo",
    "ghiChu"
  ],
  "rows": [
    {
      "rowCode": "tongSo",
      "rowLabel": "Tổng số",
      "level": 0,
      "luuLuong": 0,
      "nu": 0,
      "danTocThieuSo": 0,
      "children": []
    }
  ],
  "warnings": [
    "TEMPLATE_HEADER_THUC_NHAP_NEEDS_CONFIRMATION",
    "ROW_65_REFERENCES_EMPTY_ROW_67",
    "SOME_PARENT_ROWS_DO_NOT_SUM_CHILD_ROWS"
  ]
}
```

## 10. SQL/Proc đề xuất

### 10.1. Bảng cấu hình nên có

- `RPT_8H_ROW_DEF`: thứ tự, nhãn, cấp cha/con, `row_code`.
- `RPT_8H_ROW_RULE`: điều kiện danh mục cho từng dòng lá: trình độ, hình thức, loại hình, ngành, chuyên ngành, khóa học, trạng thái.
- `RPT_8H_PARENT_RULE`: cấu hình tổng dòng cha, để kiểm soát ngoại lệ template như row 47 không cộng row 49 hoặc row 59 không cộng row 61-62.

### 10.2. SQL skeleton

```sql
WITH params AS (
    SELECT
        :ma_don_vi AS ma_don_vi,
        :nam_hoc_id AS nam_hoc_id,
        :co_so_dao_tao_id AS co_so_dao_tao_id,
        :khoa_hoc_id AS khoa_hoc_id,
        :den_ngay AS den_ngay
    FROM dual
),
active_status AS (
    SELECT id
    FROM X02_DM.DM_TRANG_THAI_HOC_VIEN
    WHERE is_deleted = 0
      AND is_active = 1
      AND ten IN ('Đang học', 'Bảo lưu', 'Gia hạn', 'Chuyển đến') -- [Cần xác nhận]
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
        hv.doi_tuong_nhap_hoc_id,
        hv.co_so_dao_tao_id,
        hv.ma_don_vi,
        cn.gioi_tinh,
        cn.dan_toc_id
    FROM X02_APP.HOC_VIEN hv
    LEFT JOIN X02_APP.CON_NGUOI cn
           ON cn.id = hv.con_nguoi_id
          AND cn.is_deleted = 0
    JOIN active_status st
         ON st.id = hv.trang_thai_hoc_id
    CROSS JOIN params p
    WHERE hv.is_deleted = 0
      AND hv.is_active = 1
      AND hv.workflow_status = 'Approved'
      AND (p.ma_don_vi IS NULL OR hv.ma_don_vi = p.ma_don_vi)
      AND (p.co_so_dao_tao_id IS NULL OR hv.co_so_dao_tao_id = p.co_so_dao_tao_id)
      AND (p.khoa_hoc_id IS NULL OR hv.khoa_hoc_id = p.khoa_hoc_id)
      AND (p.den_ngay IS NULL OR hv.ngay_nhap_hoc <= p.den_ngay)
      AND NOT EXISTS (
          SELECT 1
          FROM X02_APP.HV_QUYET_DINH_TOT_NGHIEP tn
          WHERE tn.hoc_vien_id = hv.id
            AND tn.is_deleted = 0
            AND tn.is_active = 1
            AND tn.workflow_status = 'Approved'
      )
),
leaf_values AS (
    SELECT
        rr.row_code,
        COUNT(*) AS luu_luong,
        SUM(CASE WHEN UPPER(NVL(gioi_tinh, '')) IN ('NU', 'NỮ', 'FEMALE') THEN 1 ELSE 0 END) AS nu,
        SUM(CASE WHEN dan_toc_id IS NOT NULL THEN 1 ELSE 0 END) AS dan_toc_thieu_so,
        SUM(CASE WHEN rr.doi_tuong_group = 'CAN_BO' THEN 1 ELSE 0 END) AS can_bo,
        SUM(CASE WHEN rr.doi_tuong_group = 'CSNV' THEN 1 ELSE 0 END) AS csnv,
        SUM(CASE WHEN rr.doi_tuong_group = 'HOC_SINH_VH' THEN 1 ELSE 0 END) AS hoc_sinh_vh,
        SUM(CASE WHEN rr.doi_tuong_group = 'HOC_SINH_PT' THEN 1 ELSE 0 END) AS hoc_sinh_pt,
        SUM(CASE WHEN rr.doi_tuong_group = 'BQP' THEN 1 ELSE 0 END) AS bqp_gui,
        SUM(CASE WHEN rr.doi_tuong_group = 'NGANH_KHAC' THEN 1 ELSE 0 END) AS nganh_khac
    FROM base_hoc_vien hv
    JOIN X02_APP.RPT_8H_ROW_RULE rr
      ON (rr.trinh_do_dao_tao_id IS NULL OR rr.trinh_do_dao_tao_id = hv.trinh_do_dao_tao_id)
     AND (rr.hinh_thuc_dao_tao_id IS NULL OR rr.hinh_thuc_dao_tao_id = hv.hinh_thuc_dao_tao_id)
     AND (rr.loai_hinh_dao_tao_id IS NULL OR rr.loai_hinh_dao_tao_id = hv.loai_hinh_dao_tao_id)
     AND (rr.nganh_id IS NULL OR rr.nganh_id = hv.nganh_id)
     AND (rr.chuyen_nganh_id IS NULL OR rr.chuyen_nganh_id = hv.chuyen_nganh_id)
     AND (rr.khoa_hoc_id IS NULL OR rr.khoa_hoc_id = hv.khoa_hoc_id)
    GROUP BY rr.row_code
),
rolled AS (
    SELECT row_code, luu_luong, nu, dan_toc_thieu_so, can_bo, csnv, hoc_sinh_vh, hoc_sinh_pt, bqp_gui, nganh_khac
    FROM leaf_values
    UNION ALL
    SELECT
        pr.parent_row_code,
        SUM(lv.luu_luong),
        SUM(lv.nu),
        SUM(lv.dan_toc_thieu_so),
        SUM(lv.can_bo),
        SUM(lv.csnv),
        SUM(lv.hoc_sinh_vh),
        SUM(lv.hoc_sinh_pt),
        SUM(lv.bqp_gui),
        SUM(lv.nganh_khac)
    FROM X02_APP.RPT_8H_PARENT_RULE pr
    JOIN leaf_values lv
      ON lv.row_code = pr.child_row_code
    GROUP BY pr.parent_row_code
)
SELECT
    rd.excel_row,
    rd.row_code,
    rd.stt,
    rd.label,
    NVL(r.luu_luong, 0) AS luu_luong,
    NVL(r.can_bo, 0) AS can_bo,
    NVL(r.csnv, 0) AS csnv,
    NVL(r.hoc_sinh_vh, 0) AS hoc_sinh_vh,
    NVL(r.hoc_sinh_pt, 0) AS hoc_sinh_pt,
    NVL(r.bqp_gui, 0) AS bqp_gui,
    NVL(r.nganh_khac, 0) AS nganh_khac,
    NVL(r.nu, 0) AS nu,
    NVL(r.dan_toc_thieu_so, 0) AS dan_toc_thieu_so
FROM X02_APP.RPT_8H_ROW_DEF rd
LEFT JOIN rolled r
       ON r.row_code = rd.row_code
ORDER BY rd.excel_row;
```

`[Cần xác nhận]` SQL trên coi học viên có quyết định tốt nghiệp đã duyệt là không còn trong lưu lượng. Nếu trường `TRANG_THAI_HOC_ID` đã được cập nhật đầy đủ sang `Đã tốt nghiệp`, điều kiện `NOT EXISTS HV_QUYET_DINH_TOT_NGHIEP` có thể chỉ dùng để đối chiếu thay vì lọc chính.

## 11. Quy tắc đối soát

| Nhóm kiểm tra | Quy tắc |
|---|---|
| Tổng dòng | `Tổng số = I + 2 + 3 + 4 + 5 + II` theo cấu hình dòng đã chốt |
| Lưu lượng | `luuLuong` không nhỏ hơn từng cột đối tượng E:J và không nhỏ hơn `nu`, `danTocThieuSo` |
| Trạng thái | Học viên đã `Thôi học`, `Buộc thôi học`, `Đã tốt nghiệp` không tính vào lưu lượng nếu ngày hiệu lực trước/ngang ngày chốt |
| Khóa học | `KHOA_HOC_ID`/`TRUNG_DOI.KHOA_ID` phải khớp với dòng khóa như `NCS 23...29`, `D56` |
| Giới tính | `nu <= luuLuong` trên từng dòng |
| Dân tộc | `danTocThieuSo <= luuLuong`; cần danh mục dân tộc Kinh để loại trừ chính xác |
| Template | Cảnh báo nếu dùng nguyên công thức Excel ở row 65 vì row 67 trống |

## 12. Gap và câu hỏi cần xác nhận

| Nhóm | Vấn đề | Câu hỏi |
|---|---|---|
| Header | Cột `Thực nhập` trong báo cáo lưu lượng | Có đổi thành `Lưu lượng`/`Hiện có` không, hay giữ nguyên mẫu Bộ Công an? |
| Kỳ báo cáo | Template không có filter | Báo cáo chốt theo `denNgay`, theo năm học, hay theo tháng 5/2026 như dòng kèm báo cáo? |
| Trạng thái | Chưa rõ trạng thái tính vào lưu lượng | Có tính `Bảo lưu`, `Gia hạn`, `Chuyển đến` không? |
| Snapshot | `HOC_VIEN` chỉ có trạng thái hiện tại; `HV_TD_BIEN_DONG` chưa đủ mọi loại biến động | Có cần lưu snapshot theo ngày/kỳ báo cáo để tái lập số lịch sử không? |
| Khóa/chuyên ngành | Dòng `NCS 23...29`, `D56 chưa phân chuyên ngành`, `TSAN CLC` | Mapping sang `DM_KHOA_HOC`, `TRUNG_DOI`, `CHUONG_TRINH` hay danh mục riêng? |
| Công thức | Nhiều dòng cha không cộng dòng con hoặc thiếu cột công thức | Đây là chủ ý nghiệp vụ hay lỗi template cần sửa? |
| Bồi dưỡng | Row 65 tham chiếu row 67 trống | Có thiếu dòng chi tiết bồi dưỡng trong template không? |
| Chỉ tiêu | Cột C có còn ý nghĩa với lưu lượng không | Dùng chỉ tiêu tuyển sinh, chỉ tiêu đào tạo theo khóa, hay bỏ/để trống? |

## 13. Tham chiếu

- `docs/report-input/8H.xlsx`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`
- `docs/dashboard/LRN-dashboard.md`
- `src/frontend/frontend-x02-v2/src/domains/reports/reports.registry.js`

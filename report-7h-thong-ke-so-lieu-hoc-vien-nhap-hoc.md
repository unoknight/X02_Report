# Báo cáo 7H - Thống kê số liệu học viên nhập học

## 1. Thông tin mẫu Excel

| Thuộc tính | Giá trị |
|---|---|
| File nguồn | `docs/report-input/7H.xlsx` |
| Sheet | `Nhap hoc` |
| Mã biểu mẫu | `Biểu mẫu 7H` |
| Tên báo cáo | `THỐNG KÊ SỐ LIỆU HỌC VIÊN NHẬP HỌC` |
| Vùng dữ liệu chính | `A6:M66` |
| Vùng style kéo dài | `A1:AB82` |
| Công thức Excel | Có công thức tổng nhóm tại các dòng 10-12, 15, 21, 33, 53-54, 59, 66 |
| Dạng báo cáo | Ma trận chỉ tiêu/thực nhập theo ngành, chuyên ngành, hệ đào tạo, đối tượng nhập học và thành phần học viên |

`[Cần xác nhận]` File `7H.xlsx` là mẫu chính thức cho `Biểu mẫu 7H`. Tài liệu cũ `report-m05-thong-ke-so-lieu-hoc-vien-nhap-hoc.md` phân tích `M05.xlsx`, trong đó cũng ghi biểu mẫu 7H nhưng layout khác và nhỏ hơn. Vì vậy nên coi `7H.xlsx` là mẫu 7H hiện hành, còn `M05.xlsx` là bản/biến thể cần đối chiếu riêng.

## 2. Mục đích nghiệp vụ

Báo cáo thống kê số liệu học viên nhập học theo hệ đào tạo, trình độ, ngành/chuyên ngành và loại hình đào tạo. Mỗi dòng thể hiện:

- Chỉ tiêu tuyển sinh.
- Số thực nhập.
- Cơ cấu đối tượng nhập học: cán bộ, CSNV, học sinh văn hóa, học sinh phổ thông, Bộ Quốc phòng gửi, ngành khác.
- Thành phần trong thực nhập: nữ, dân tộc thiểu số.

`[Suy luận]` Báo cáo phục vụ đối chiếu giữa kế hoạch/chỉ tiêu tuyển sinh và số học viên đã nhập học thực tế trong năm tuyển sinh hoặc năm nhập học. Template không có ô filter nên API/giao diện cần truyền `maDonVi`, `namTuyenSinhId`, `namNhapHoc` hoặc `tuNgay/denNgay`.

## 3. Layout Excel

### 3.1. Header chung

| Vùng | Nội dung | Ghi chú |
|---|---|---|
| `A1:L1` | Trống/khung header | Merged |
| `M1` | `Biểu mẫu 7H` | Không merged trong vùng `A1:L1` |
| `A2:B2` | `BỘ CÔNG AN` | Merged |
| `C2:M3` | Tên báo cáo | Merged |
| `A3:B3` | `HỌC VIÊN/TRƯỜNG CAND` | Merged |
| `C4:M4` | Dòng kèm theo báo cáo | Merged, ghi `tháng 5 năm 2026` |
| `J75:M75` | `HIỆU TRƯỞNG` | Vùng chữ ký |

### 3.2. Header bảng

| Vùng | Nhãn | Field đề xuất |
|---|---|---|
| `A6:A8` | `STT` | `stt` |
| `B6:B8` | `Ngành, Chuyên ngành` | `rowLabel`, `rowCode`, `parentCode` |
| `C6:C8` | `Chỉ tiêu` | `chiTieu` |
| `D6:D8` | `Thực nhập` | `thucNhap` |
| `E6:J6` | `Đối tượng nhập học` | Nhóm `doiTuongNhapHoc` |
| `E7:H7` | `Trong ngành` | Nhóm con trong ngành |
| `E8` | `Cán bộ` | `canBo` |
| `F8` | `CSNV` | `csnv` |
| `G8` | `Học sinh VH` | `hocSinhVanHoa` |
| `H8` | `Học sinh PT` | `hocSinhPhoThong` |
| `I7:J7` | `Ngành ngoài` | Nhóm con ngành ngoài |
| `I8` | `BQP gửi` | `bqpGui` |
| `J8` | `Ngành khác` | `nganhKhac` |
| `K6:L6` | `Trong đó` | Nhóm thành phần |
| `K7:K8` | `Nữ` | `nu` |
| `L7:L8` | `DTTS` | `danTocThieuSo` |
| `M6:M8` | `Ghi chú` | `ghiChu` |

`[Cần xác nhận]` Header 7H không còn cột `Ngoài ngành` như tài liệu M05 cũ; thay vào đó có nhóm `Ngành ngoài` với `BQP gửi` và `Ngành khác`. Cần xác nhận cách hiểu nghiệp vụ: BQP gửi và ngành khác là hai nhóm ngoài ngành, hay chỉ là nhãn kỹ thuật của template.

## 4. Mapping dòng chỉ tiêu

| Dòng Excel | STT | Nhãn | Field đề xuất | Mapping nguồn đề xuất |
|---:|---|---|---|---|
| 10 |  | Tổng số | `tongSo` | Tổng các nhóm chính: row 11, 37, 40, 42, 53, 66 |
| 11 | I | Hệ đào tạo giáo dục chính quy | `heDaoTaoGiaoDucChinhQuy` | Tổng row 12, 15, 21 |
| 12 | 1.1 | Đào tạo trình độ tiến sĩ | `daoTaoTienSi` | `TRINH_DO_DAO_TAO_ID = tiến sĩ` |
| 13 |  | Dòng con tiến sĩ 1 | `daoTaoTienSiDong1` | `[Cần xác nhận]` Dòng không có nhãn trong template |
| 14 |  | Dòng con tiến sĩ 2 | `daoTaoTienSiDong2` | `[Cần xác nhận]` Dòng không có nhãn trong template |
| 15 | 1.2 | Đào tạo trình độ thạc sĩ | `daoTaoThacSi` | Tổng row 16-20 theo chuyên ngành |
| 16 |  | Trinh sát an ninh | `thsTrinhSatAnNinh` | `TRINH_DO_DAO_TAO_ID = thạc sĩ`, ngành/chuyên ngành TSAN |
| 17 |  | Điều tra hình sự | `thsDieuTraHinhSu` | `CHUYEN_NGANH_ID` tương ứng |
| 18 |  | An ninh phi truyền thống | `thsAnNinhPhiTruyenThong` | `CHUYEN_NGANH_ID` tương ứng |
| 19 |  | Tội phạm học và phòng ngừa tội phạm | `thsToiPhamHocPhongNgua` | `CHUYEN_NGANH_ID` tương ứng |
| 20 |  | Quản lý nhà nước về ANTT | `thsQlNnAntt` | `CHUYEN_NGANH_ID` tương ứng |
| 21 | 1.3 | Đào tạo trình độ đại học | `daoTaoDaiHocChinhQuy` | Tổng các ngành đại học row 22, 27, 33; riêng cột D cộng thêm row 36 |
| 22 |  | Nghiệp vụ an ninh | `dhNghiepVuAnNinh` | Ngành/nhóm ngành nghiệp vụ an ninh |
| 23 |  | Trinh sát an ninh | `dhTrinhSatAnNinh` | `[Cần xác nhận]` Dòng cha cho row 24-26 nhưng không có công thức tổng riêng |
| 24 |  | Trinh sát phản gián | `dhTrinhSatPhanGian` | Chuyên ngành |
| 25 |  | Trinh sát bảo vệ an ninh xã hội | `dhTrinhSatBaoVeAnNinhXaHoi` | Chuyên ngành |
| 26 |  | Trinh sát bảo vệ an ninh nội bộ | `dhTrinhSatBaoVeAnNinhNoiBo` | Chuyên ngành |
| 27 |  | Điều tra hình sự | `dhDieuTraHinhSu` | `[Cần xác nhận]` Dòng cha cho row 28-32 nhưng không có công thức tổng riêng |
| 28 |  | An ninh điều tra | `dhAnNinhDieuTra` | Chuyên ngành |
| 29 |  | Điều tra tội phạm trật tự xã hội | `dhDieuTraToiPhamTtxh` | Chuyên ngành |
| 30 |  | Điều tra tội phạm ma túy | `dhDieuTraToiPhamMaTuy` | Chuyên ngành |
| 31 |  | Điều tra tội phạm kinh tế, môi trường | `dhDieuTraKtmt` | Chuyên ngành |
| 32 |  | Quan hệ quốc tế | `dhQuanHeQuocTe` | Chuyên ngành |
| 33 |  | An toàn thông tin | `dhAnToanThongTin` | Tổng row 34-35 |
| 34 |  | An ninh mạng và phòng, chống TP sử dụng công nghệ cao | `dhAnNinhMangPctpCnCao` | Chuyên ngành |
| 35 |  | Công nghệ thông tin | `dhCongNgheThongTin` | Chuyên ngành |
| 36 |  | Gửi đào tạo y khoa - HVQY | `guiDaoTaoYkhoaHvqy` | `[Cần xác nhận]` Chỉ được cộng vào cột `Thực nhập` của row 21 theo công thức template |
| 37 | 2 | Đào tạo trình độ đại học hình thức vừa làm vừa học | `daiHocVlvh` | `TRINH_DO_DAO_TAO_ID = đại học`, `HINH_THUC_DAO_TAO_ID = VLVH` |
| 38 |  | Đào tạo tại trường công an | `daiHocVlvhTaiTruong` | `[Cần xác nhận]` Theo `CO_SO_DAO_TAO_ID`/`MA_DON_VI` |
| 39 |  | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `daiHocVlvhLienKet` | `[Cần xác nhận]` Theo loại hình liên kết/địa bàn |
| 40 | 3 | Hệ cử tuyển | `heCuTuyen` | `[Cần mapping danh mục]` Cần field/danh mục cử tuyển |
| 41 |  | Đại học | `cuTuyenDaiHoc` | Dòng con của hệ cử tuyển |
| 42 | 4 | Hệ liên thông | `heLienThong` | Nhóm row 43-52 |
| 43 | 4.1 | Đào tạo tại trường Công an nhân dân | `lienThongTaiTruongCand` | Nhóm row 44-49 |
| 44 |  | Hình thức chính quy | `lienThongTaiTruongChinhQuy` | Nhóm row 45-46 |
| 45 |  | Trung cấp lên Đại học | `lienThongTcLenDhChinhQuy` | `[Cần xác nhận]` Cần trường trình độ đầu vào |
| 46 |  | Cao đẳng lên Đại học | `lienThongCdLenDhChinhQuy` | `[Cần xác nhận]` Cần trường trình độ đầu vào |
| 47 |  | Hình thức vừa làm vừa học | `lienThongTaiTruongVlvh` | Nhóm row 48-49 |
| 48 |  | Trung cấp lên Đại học | `lienThongTcLenDhVlvh` | `[Cần xác nhận]` |
| 49 |  | Cao đẳng lên Đại học | `lienThongCdLenDhVlvh` | `[Cần xác nhận]` |
| 50 | 4.2 | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `lienThongLienKet` | Nhóm row 51-52 |
| 51 |  | Trung cấp lên Đại học | `lienThongLienKetTcLenDh` | `[Cần xác nhận]` |
| 52 |  | Cao đẳng lên Đại học | `lienThongLienKetCdLenDh` | `[Cần xác nhận]` |
| 53 | 5 | Các loại hình đào tạo khác | `loaiHinhDaoTaoKhac` | Tổng row 54 và 59 |
| 54 | 5.1 | Đào tạo cấp bằng đại học thứ 2 | `daiHocThu2` | Tổng row 55-58; template chỉ có công thức cột C |
| 55 |  | Đào tạo tại trường | `daiHocThu2TaiTruong` | Nhóm row 56-57 |
| 56 |  | Chính quy | `daiHocThu2ChinhQuy` | `[Cần mapping danh mục]` |
| 57 |  | Vừa làm vừa học | `daiHocThu2Vlvh` | `[Cần mapping danh mục]` |
| 58 |  | Đào tạo liên kết mở tại CA các đơn vị, địa phương | `daiHocThu2LienKet` | `[Cần xác nhận]` |
| 59 | 5.2 | Đào tạo lý luận chính trị | `daoTaoLyLuanChinhTri` | Tổng row 60-65 |
| 60 |  | Đào tạo cao cấp lý luận chính trị | `llctCaoCap` | Nhóm row 61-62 |
| 61 |  | Hệ tập trung | `llctCaoCapTapTrung` | `[Cần mapping danh mục]` |
| 62 |  | Hệ không tập trung | `llctCaoCapKhongTapTrung` | `[Cần mapping danh mục]` |
| 63 |  | Đào tạo trung cấp lý luận chính trị | `llctTrungCap` | Nhóm row 64-65 |
| 64 |  | Hệ tập trung | `llctTrungCapTapTrung` | `[Cần mapping danh mục]` |
| 65 |  | Hệ không tập trung | `llctTrungCapKhongTapTrung` | `[Cần mapping danh mục]` |
| 66 | II | Các loại hình bồi dưỡng | `cacLoaiHinhBoiDuong` | Công thức tham chiếu row 69 nhưng row 69 trống `[Cần xác nhận template]` |

## 5. Mapping cột giá trị

| Cột | Header | Field đề xuất | Mapping DB đề xuất |
|---|---|---|---|
| `C` | Chỉ tiêu | `chiTieu` | `CHI_TIEU_TUYEN_SINH_CHI_TIET.TONG_SO`, join `CHI_TIEU_TUYEN_SINH` |
| `D` | Thực nhập | `thucNhap` | Ưu tiên `COUNT(HOC_VIEN.ID)` theo `NGAY_NHAP_HOC`; hoặc `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC` nếu nghiệp vụ chốt số tổng hợp tuyển sinh |
| `E` | Cán bộ | `canBo` | `HOC_VIEN.DOI_TUONG_NHAP_HOC_ID -> DM_DOI_TUONG_NHAP_HOC` `[Cần mapping danh mục]` |
| `F` | CSNV | `csnv` | Chiến sĩ nghĩa vụ `[Suy luận]` |
| `G` | Học sinh VH | `hocSinhVanHoa` | Học sinh văn hóa `[Cần mapping danh mục]` |
| `H` | Học sinh PT | `hocSinhPhoThong` | Học sinh phổ thông/thí sinh THPT `[Cần mapping danh mục]` |
| `I` | BQP gửi | `bqpGui` | Mã đối tượng BQP hoặc nguồn gửi từ Bộ Quốc phòng |
| `J` | Ngành khác | `nganhKhac` | Mã đối tượng ngành khác |
| `K` | Nữ | `nu` | Join `HOC_VIEN.CON_NGUOI_ID = CON_NGUOI.ID`, `CON_NGUOI.GIOI_TINH = 'NU'` |
| `L` | DTTS | `danTocThieuSo` | `CON_NGUOI.DAN_TOC_ID`, loại trừ dân tộc Kinh hoặc theo danh sách DTTS chính thức |
| `M` | Ghi chú | `ghiChu` | Text nhập tay/tổng hợp |

`[Cần xác nhận]` Nếu `thucNhap` lấy từ `KET_QUA_TUYEN_SINH_CHI_TIET.SL_TONG_SO_NHAP_HOC`, các cột E:L khó tách tự động vì bảng kết quả tuyển sinh chi tiết không thể hiện đối tượng, giới tính, dân tộc. Để xuất đủ 7H, nguồn `HOC_VIEN` phù hợp hơn cho thực nhập và cơ cấu.

## 6. Công thức Excel trong template

| Dòng | Ý nghĩa | Công thức chính |
|---:|---|---|
| 10 | Tổng số | Cộng row 11, 37, 40, 42, 53, 66 trên cột C:L |
| 11 | Hệ đào tạo giáo dục chính quy | Cộng row 12, 21, 15 |
| 12 | Tiến sĩ | `SUM(row 13:14)` |
| 15 | Thạc sĩ | `SUM(row 16:20)` |
| 21 | Đại học | Cột C/E:L cộng row 22, 27, 33; riêng cột D cộng thêm row 36 |
| 33 | An toàn thông tin | `SUM(row 34:35)` |
| 53 | Các loại hình đào tạo khác | Cộng row 54 và 59 |
| 54 | Đại học thứ 2 | Chỉ thấy công thức `C54=SUM(C55:C58)`; các cột D:L không có công thức |
| 59 | Đào tạo lý luận chính trị | Cột C/E:L cộng row 60:65; riêng D59 cộng row 60 và 63 |
| 66 | Các loại hình bồi dưỡng | Cộng row 69, nhưng row 69 trống; cột M66 cũng có công thức `=SUM(M69:M69)` dù M là ghi chú |

`[Cần xác nhận]` Các công thức bất thường ở row 21, 54, 59, 66 có thể là chủ ý nghiệp vụ hoặc lỗi template. Khi hiện thực hóa report, nên ưu tiên cấu hình dòng rõ ràng thay vì copy nguyên công thức nếu chưa được xác nhận.

## 7. Nguồn dữ liệu hệ thống

| Bảng/API | Vai trò | Cột/field quan trọng |
|---|---|---|
| `X02_APP.HOC_VIEN` / các API học viên `LRN` | Nguồn thực nhập và cơ cấu E:L | `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `LOAI_HINH_DAO_TAO_ID`, `NGANH_ID`, `CHUYEN_NGANH_ID`, `NGAY_NHAP_HOC`, `DOI_TUONG_NHAP_HOC_ID`, `CO_SO_DAO_TAO_ID`, `LOAI_HOC_VIEN` |
| `X02_APP.CON_NGUOI` | Nguồn giới tính, dân tộc | `GIOI_TINH`, `DAN_TOC_ID` |
| `X02_APP.CHI_TIEU_TUYEN_SINH` | Nguồn chỉ tiêu tổng | `TRINH_DO_DAO_TAO_ID`, `HINH_THUC_DAO_TAO_ID`, `NAM_TUYEN_SINH_ID`, `NHOM_NGANH_ID`, `CO_SO_DAO_TAO_ID`, `PHAN_LOAI`, `WORKFLOW_STATUS` |
| `X02_APP.CHI_TIEU_TUYEN_SINH_CHI_TIET` | Nguồn số lượng chỉ tiêu chi tiết | `CHI_TIEU_TUYEN_SINH_ID`, `TONG_SO`, `CHI_TIEU_NAM`, `CHI_TIEU_NU`, `DIA_BAN_ID` |
| `X02_APP.KET_QUA_TUYEN_SINH` | Nguồn kết quả tuyển sinh tổng | `NAM_TUYEN_SINH_ID`, `CHI_TIEU_TUYEN_SINH_ID`, `PHAN_LOAI` |
| `X02_APP.KET_QUA_TUYEN_SINH_CHI_TIET` | Nguồn số tổng nhập học nếu dùng kết quả tuyển sinh | `SL_TONG_SO_NHAP_HOC`, `PHUONG_THUC_TUYEN_SINH_ID` |
| `X02_DM.DM_TRINH_DO_DAO_TAO` | Mapping tiến sĩ, thạc sĩ, đại học, trung cấp | `ID`, `MA`, `TEN` |
| `X02_DM.DM_HINH_THUC_DAO_TAO` | Mapping chính quy, VLVH, liên thông, văn bằng 2... | `ID`, `MA`, `TEN` |
| `X02_DM.DM_LOAI_HINH_DAO_TAO` | Mapping tại trường, liên kết, loại hình đặc thù nếu có | `ID`, `MA`, `TEN` |
| `X02_DM.DM_DOI_TUONG_NHAP_HOC` | Mapping cán bộ, CSNV, học sinh, BQP, ngành khác | `ID`, `MA`, `TEN` |
| `X02_DM.DM_DAN_TOC` | Mapping dân tộc thiểu số | `ID`, `MA`, `TEN` |

## 8. Bộ lọc đề xuất

| Filter | Kiểu | Mapping |
|---|---|---|
| `maDonVi` | String | Theo `MA_DON_VI` hoặc scope qua `CO_SO_DAO_TAO_ID`; mặc định theo quyền user |
| `namTuyenSinhId` | String | `CHI_TIEU_TUYEN_SINH.NAM_TUYEN_SINH_ID`, `KET_QUA_TUYEN_SINH.NAM_TUYEN_SINH_ID` |
| `namNhapHoc` | Number | `EXTRACT(YEAR FROM HOC_VIEN.NGAY_NHAP_HOC)` |
| `tuNgay` | Date | `HOC_VIEN.NGAY_NHAP_HOC` nếu lọc theo khoảng ngày |
| `denNgay` | Date | Ngày kết thúc kỳ |
| `coSoDaoTaoId` | String | `HOC_VIEN.CO_SO_DAO_TAO_ID`, `CHI_TIEU_TUYEN_SINH.CO_SO_DAO_TAO_ID` |
| `workflowStatus` | String | Mặc định `Approved` với bảng có workflow |

`[Cần xác nhận]` Báo cáo nên chạy theo năm tuyển sinh hay năm nhập học. Nếu chỉ tiêu theo `namTuyenSinhId` nhưng thực nhập theo `namNhapHoc`, cần quy tắc đối chiếu năm rõ ràng.

## 9. API report đề xuất

```http
GET /api/v1/reports/7h/so-lieu-hoc-vien-nhap-hoc
```

Query params:

| Param | Bắt buộc | Ghi chú |
|---|---|---|
| `maDonVi` | Không | Nếu rỗng lấy theo quyền user |
| `namTuyenSinhId` | Không | Dùng cho chỉ tiêu/kết quả tuyển sinh |
| `namNhapHoc` | Không | Dùng cho học viên nhập học thực tế |
| `tuNgay` | Không | Bắt buộc nếu không truyền năm |
| `denNgay` | Không | Bắt buộc nếu không truyền năm |
| `coSoDaoTaoId` | Không | Lọc theo cơ sở đào tạo |

Response đề xuất:

```json
{
  "reportCode": "7H",
  "title": "Thống kê số liệu học viên nhập học",
  "filters": {
    "maDonVi": "T01",
    "namTuyenSinhId": "2026",
    "namNhapHoc": 2026
  },
  "rows": [
    {
      "rowCode": "TONG_SO",
      "stt": "",
      "label": "Tổng số",
      "level": 0,
      "parentCode": null,
      "chiTieu": 0,
      "thucNhap": 0,
      "canBo": 0,
      "csnv": 0,
      "hocSinhVanHoa": 0,
      "hocSinhPhoThong": 0,
      "bqpGui": 0,
      "nganhKhac": 0,
      "nu": 0,
      "danTocThieuSo": 0,
      "ghiChu": ""
    }
  ],
  "dataQualityWarnings": [
    "ROW_66_REFERENCES_EMPTY_ROW_69",
    "ROW_54_PARTIAL_FORMULA"
  ]
}
```

## 10. SQL/Proc đề xuất

Đề xuất dùng cấu hình dòng thay vì hardcode toàn bộ ngành/chuyên ngành trong proc:

- `RPT_7H_ROW_DEF`: thứ tự, nhãn, cấp cha/con, row_code.
- `RPT_7H_ROW_RULE`: điều kiện danh mục cho từng dòng lá: trình độ, hình thức, loại hình, ngành, chuyên ngành, loại học viên.
- `RPT_7H_PARENT_RULE`: cấu hình tổng dòng cha, để phản ánh các ngoại lệ như row 21 cột D cộng thêm row 36.

Skeleton Oracle:

```sql
WITH params AS (
    SELECT :p_ma_don_vi AS ma_don_vi,
           :p_nam_tuyen_sinh_id AS nam_tuyen_sinh_id,
           :p_nam_nhap_hoc AS nam_nhap_hoc,
           NVL(:p_workflow_status, 'Approved') AS workflow_status
    FROM dual
),
hv_source AS (
    SELECT
        hv.ID,
        hv.TRINH_DO_DAO_TAO_ID,
        hv.HINH_THUC_DAO_TAO_ID,
        hv.LOAI_HINH_DAO_TAO_ID,
        hv.NGANH_ID,
        hv.CHUYEN_NGANH_ID,
        hv.DOI_TUONG_NHAP_HOC_ID,
        hv.LOAI_HOC_VIEN,
        hv.CO_SO_DAO_TAO_ID,
        hv.NGAY_NHAP_HOC,
        cn.GIOI_TINH,
        cn.DAN_TOC_ID
    FROM X02_APP.HOC_VIEN hv
    LEFT JOIN X02_APP.CON_NGUOI cn ON cn.ID = hv.CON_NGUOI_ID
    CROSS JOIN params p
    WHERE hv.IS_DELETED = 0
      AND hv.IS_ACTIVE = 1
      AND (p.ma_don_vi IS NULL OR hv.MA_DON_VI = p.ma_don_vi)
      AND (p.nam_nhap_hoc IS NULL OR EXTRACT(YEAR FROM hv.NGAY_NHAP_HOC) = p.nam_nhap_hoc)
),
hv_mapped AS (
    SELECT
        rr.ROW_CODE,
        COUNT(*) AS thuc_nhap,
        SUM(CASE WHEN dtnh.MA IN ('CAN_BO', 'CBCS', 'CBCC') THEN 1 ELSE 0 END) AS can_bo,
        SUM(CASE WHEN dtnh.MA IN ('CSNV', 'NVQS') THEN 1 ELSE 0 END) AS csnv,
        SUM(CASE WHEN dtnh.MA IN ('HSVH') THEN 1 ELSE 0 END) AS hoc_sinh_van_hoa,
        SUM(CASE WHEN dtnh.MA IN ('HSPT', 'HS', 'TSVH') THEN 1 ELSE 0 END) AS hoc_sinh_pho_thong,
        SUM(CASE WHEN dtnh.MA IN ('BQP') THEN 1 ELSE 0 END) AS bqp_gui,
        SUM(CASE WHEN dtnh.MA IN ('NGANH_KHAC', 'NK') THEN 1 ELSE 0 END) AS nganh_khac,
        SUM(CASE WHEN hv.GIOI_TINH = 'NU' THEN 1 ELSE 0 END) AS nu,
        SUM(CASE WHEN dt.MA IS NOT NULL AND dt.MA <> 'KINH' THEN 1 ELSE 0 END) AS dan_toc_thieu_so
    FROM hv_source hv
    JOIN X02_APP.RPT_7H_ROW_RULE rr
      ON (rr.TRINH_DO_DAO_TAO_ID IS NULL OR rr.TRINH_DO_DAO_TAO_ID = hv.TRINH_DO_DAO_TAO_ID)
     AND (rr.HINH_THUC_DAO_TAO_ID IS NULL OR rr.HINH_THUC_DAO_TAO_ID = hv.HINH_THUC_DAO_TAO_ID)
     AND (rr.LOAI_HINH_DAO_TAO_ID IS NULL OR rr.LOAI_HINH_DAO_TAO_ID = hv.LOAI_HINH_DAO_TAO_ID)
     AND (rr.NGANH_ID IS NULL OR rr.NGANH_ID = hv.NGANH_ID)
     AND (rr.CHUYEN_NGANH_ID IS NULL OR rr.CHUYEN_NGANH_ID = hv.CHUYEN_NGANH_ID)
     AND (rr.LOAI_HOC_VIEN IS NULL OR rr.LOAI_HOC_VIEN = hv.LOAI_HOC_VIEN)
    LEFT JOIN X02_DM.DM_DOI_TUONG_NHAP_HOC dtnh ON dtnh.ID = hv.DOI_TUONG_NHAP_HOC_ID
    LEFT JOIN X02_DM.DM_DAN_TOC dt ON dt.ID = hv.DAN_TOC_ID
    GROUP BY rr.ROW_CODE
),
ct_mapped AS (
    SELECT
        rr.ROW_CODE,
        SUM(ctct.TONG_SO) AS chi_tieu
    FROM X02_APP.CHI_TIEU_TUYEN_SINH ct
    JOIN X02_APP.CHI_TIEU_TUYEN_SINH_CHI_TIET ctct
      ON ctct.CHI_TIEU_TUYEN_SINH_ID = ct.ID
    JOIN X02_APP.RPT_7H_ROW_RULE rr
      ON (rr.TRINH_DO_DAO_TAO_ID IS NULL OR rr.TRINH_DO_DAO_TAO_ID = ct.TRINH_DO_DAO_TAO_ID)
     AND (rr.HINH_THUC_DAO_TAO_ID IS NULL OR rr.HINH_THUC_DAO_TAO_ID = ct.HINH_THUC_DAO_TAO_ID)
     AND (rr.NGANH_ID IS NULL OR rr.NGANH_ID = ct.NHOM_NGANH_ID)
    CROSS JOIN params p
    WHERE ct.IS_DELETED = 0
      AND ct.IS_ACTIVE = 1
      AND ct.WORKFLOW_STATUS = p.workflow_status
      AND (p.ma_don_vi IS NULL OR ct.MA_DON_VI = p.ma_don_vi)
      AND (p.nam_tuyen_sinh_id IS NULL OR ct.NAM_TUYEN_SINH_ID = p.nam_tuyen_sinh_id)
    GROUP BY rr.ROW_CODE
)
SELECT
    rd.STT,
    rd.LABEL,
    NVL(ct.CHI_TIEU, 0) AS CHI_TIEU,
    NVL(hv.THUC_NHAP, 0) AS THUC_NHAP,
    NVL(hv.CAN_BO, 0) AS CAN_BO,
    NVL(hv.CSNV, 0) AS CSNV,
    NVL(hv.HOC_SINH_VAN_HOA, 0) AS HOC_SINH_VAN_HOA,
    NVL(hv.HOC_SINH_PHO_THONG, 0) AS HOC_SINH_PHO_THONG,
    NVL(hv.BQP_GUI, 0) AS BQP_GUI,
    NVL(hv.NGANH_KHAC, 0) AS NGANH_KHAC,
    NVL(hv.NU, 0) AS NU,
    NVL(hv.DAN_TOC_THIEU_SO, 0) AS DAN_TOC_THIEU_SO
FROM X02_APP.RPT_7H_ROW_DEF rd
LEFT JOIN ct_mapped ct ON ct.ROW_CODE = rd.ROW_CODE
LEFT JOIN hv_mapped hv ON hv.ROW_CODE = rd.ROW_CODE
ORDER BY rd.SORT_ORDER;
```

`[Cần mapping danh mục]` Các mã `CAN_BO`, `CBCS`, `HSVH`, `KINH` trong skeleton là placeholder. Cần thay bằng mã thực tế trong `X02_DM` sau khi chốt danh mục.

## 11. Quy tắc đối soát

- Với mỗi dòng lá, `thucNhap` nên bằng tổng `canBo + csnv + hocSinhVanHoa + hocSinhPhoThong + bqpGui + nganhKhac` nếu mỗi học viên chỉ thuộc đúng một đối tượng nhập học.
- `nu <= thucNhap` và `danTocThieuSo <= thucNhap`.
- Tổng dòng cha phải được tính từ dòng con theo cấu hình, không cộng trùng dòng cha/con.
- `chiTieu` từ chỉ tiêu tuyển sinh nên đối chiếu với `thucNhap`; nếu `thucNhap > chiTieu`, API nên trả cảnh báo thay vì tự sửa số.
- Nếu sử dụng số thực nhập tổng hợp từ `KET_QUA_TUYEN_SINH_CHI_TIET`, cần đối chiếu chênh lệch với count `HOC_VIEN`.

## 12. Gap/câu hỏi cần xác nhận

| Nhóm | Vấn đề | Đề xuất xử lý |
|---|---|---|
| Template | Row 13-14 không có nhãn; row 66 tham chiếu row 69 trống | Xác nhận template hoặc bổ sung nhãn/dòng bồi dưỡng còn thiếu |
| Công thức | Row 21 cột D cộng thêm row 36, các cột khác không cộng; row 54 chỉ có công thức cột C | Chốt đây là chủ ý hay lỗi công thức |
| Mapping ngành/chuyên ngành | Nhiều dòng ngành/chuyên ngành chi tiết | Cần bảng cấu hình row_code -> ngành/chuyên ngành thay vì hardcode |
| Liên thông | Cần phân biệt trung cấp lên đại học/cao đẳng lên đại học | Bổ sung hoặc xác nhận field trình độ đầu vào |
| Cử tuyển/dân sự/bồi dưỡng | Chưa rõ field/danh mục nguồn | Cần mapping danh mục/loại học viên |
| Đối tượng nhập học | Cán bộ, CSNV, học sinh VH/PT, BQP gửi, ngành khác | Chốt mã `DM_DOI_TUONG_NHAP_HOC` cho từng cột |
| DTTS | Cần xác định dân tộc Kinh hoặc danh sách DTTS | Chốt mã danh mục dân tộc |
| M05 vs 7H | Hai file cùng nghiệp vụ nhưng layout khác | Chốt file nào là mẫu chính thức trong hệ thống báo cáo |

## 13. Tài liệu/code tham chiếu

- `docs/report-input/7H.xlsx`
- `docs/report-output/report-m05-thong-ke-so-lieu-hoc-vien-nhap-hoc.md`
- `docs/report-promt.md`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/lrn/hocvien/entity/HocVien.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/nt/connguoi/entity/ConNguoi.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/adm/tuyensinhcanbo/entity/TuyenSinhCanBo.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/adm/tuyensinhcanbo/entity/TuyenSinhCanBoChiTiet.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/adm/ketquatuyensinhcanbo/entity/KetQuaTuyenSinhCanBo.java`
- `src/backend/qldt-v2/src/main/java/vn/gtelict/x02/domain/adm/ketquatuyensinhcanbo/entity/KetQuaTuyenSinhCanBoChiTiet.java`
- `docs/database/X02_APP.sql`
- `docs/database/X02_DM.sql`

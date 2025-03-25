# BÀI TẬP VỀ NHÀ SỐ 2: MSSV K225480106039 - NGUYỄN NGUYỆT LINH - MÔN HỆ QUẢN TRỊ CƠ SỞ DỮ LIỆU

## DEADLINE: 23H59 NGÀY 25/03/2025
## ĐIỀU KIỆN: (ĐÃ LÀM XONG BÀI 1)
  1. Đã cài đặt SQL Server 2022 Dev.
  2. Đã cài đặt SQL Managerment Studio bản mới nhất.
  3. Đã kết nối từ SQL Managerment Studio vào SQL Server.
  4. Đã có tài khoản github, biết cách tạo repository(kho lưu trữ) cho phép truy cập public.
# ĐỀ BÀI
## BÀI TOÁN
### Tạo csdl quan hệ với tên QLSV gồm các bảng sau:
  - SinhVien(#masv,hoten,NgaySinh)
  - Lop(#maLop,tenLop)
  - GVCN(#@maLop,#@magv,#HK)
  - LopSV(#@maLop,#@maSV,ChucVu)
  - GiaoVien(#magv,hoten,NgaySinh,@maBM)
  - BoMon(#MaBM,tenBM,@maKhoa)
  - Khoa(#maKhoa,tenKhoa)
  - MonHoc(#mamon,Tenmon,STC)
  - LopHP(#maLopHP,TenLopHP,HK,@maMon,@maGV)
  - DKMH(#@maLopHP,#@maSV,DiemTP,DiemThi,PhanTramThi)
## YÊU CẦU
### Thực hiện các hành động sau trên giao diện đồ hoạ để tạo cơ sở dữ liệu cho bài toán:
Tạo database mới, mô tả các tham số(nếu có) trong quá trình.
Tạo các bảng dữ liệu với các trường như mô tả, chọn kiểu dữ liệu phù hợp với thực tế (tự tìm hiểu)
Mỗi bảng cần thiết lập PK, FK(s) và CK(s) nếu cần thiết. (chú ý dấu # và @: # là chỉ PK, @ chỉ FK)
### Chuyển các thao tác đồ hoạ trên thành lệnh SQL tương đương. lưu tất cả các lệnh SQL trong file: Script_DML.sql
# BÀI LÀM
## THỰC HIỆN TẠO CSDL BÀI TOÁN BẰNG UI
Tạo database mới tên QLSV: 
![Ảnh chụp màn hình 2025-03-25 132003](https://github.com/user-attachments/assets/e823abfe-7753-42a2-b67f-090c8be494ce)

Tạo các bảng dữ liệu với các trường như mô tả, chọn kiểu dữ liệu phù hợp với thực tế:
Dưới đây là các bảng đã được thiết lập các khóa theo yêu cầu của bài toán:
![Ảnh chụp màn hình 2025-03-25 134505](https://github.com/user-attachments/assets/23fb309a-47a3-4528-bc02-bec2c0b4e2dd)

![Ảnh chụp màn hình 2025-03-25 134532](https://github.com/user-attachments/assets/ce6ac2a8-3861-4007-b6e9-62dbb024abf6)

![Ảnh chụp màn hình 2025-03-25 134733](https://github.com/user-attachments/assets/11f56e58-ec38-4a76-91a1-804ee63262f3)

![Ảnh chụp màn hình 2025-03-25 134814](https://github.com/user-attachments/assets/97ace344-2c19-40c3-9bf1-64f5903b27fd)

![Ảnh chụp màn hình 2025-03-25 134823](https://github.com/user-attachments/assets/6158c544-2f02-4a69-ab14-beab2de249e7)

![Ảnh chụp màn hình 2025-03-25 134830](https://github.com/user-attachments/assets/57de3b23-5cb1-4a3a-b438-df1e39229c8a)

![Ảnh chụp màn hình 2025-03-25 134841](https://github.com/user-attachments/assets/2f928b74-2797-4ae5-ad50-e0917026d8ee)

![Ảnh chụp màn hình 2025-03-25 134920](https://github.com/user-attachments/assets/f82a6d8f-156c-4289-b510-a69c53ac200e)

![Ảnh chụp màn hình 2025-03-25 134938](https://github.com/user-attachments/assets/e9b89faa-b840-49c1-b2ee-670b26dd3838)

![Ảnh chụp màn hình 2025-03-25 134953](https://github.com/user-attachments/assets/eb8d461b-d140-4483-a179-9394a796eb87)

## THỰC HIỆN TẠO CSDL TƯƠNG ĐƯƠNG BẰNG LỆNH SQL
  CREATE DATABASE QLSV;
  GO
  
  USE QLSV;
  GO
  
  CREATE TABLE SinhVien (
      MaSV VARCHAR(15) PRIMARY KEY,
      TenSV NVARCHAR(50) NOT NULL,
      NgaySinh DATE NOT NULL,
  );
  GO
  
  CREATE TABLE Lop (
      MaLop VARCHAR(15) PRIMARY KEY,
      TenLop NVARCHAR(50) NOT NULL,
  );
  GO
  
  CREATE TABLE LopSV (
      MaLop VARCHAR(15),
      MaSV VARCHAR(13),
  	ChucVu NVARCHAR(50),
      PRIMARY KEY (MaLop, MaSV),
      FOREIGN KEY (MaLop) REFERENCES Lop(MaLop),
      FOREIGN KEY (MaSV) REFERENCES SinhVien(MaSV)
  );
  GO
  
  CREATE TABLE Khoa (
      MaKhoa VARCHAR(15) PRIMARY KEY,
      TenKhoa NVARCHAR(50) NOT NULL,
  );
  GO
  
  CREATE TABLE MonHoc (
      MaMon VARCHAR(15) PRIMARY KEY,
      TenMon NVARCHAR(50) NOT NULL,
      STC INT NOT NULL
  );
  GO
  
  CREATE TABLE BoMon (
      MaBM VARCHAR(15) PRIMARY KEY,
      TenBM NVARCHAR(50) NOT NULL,
      MaKhoa VARCHAR(15) NOT NULL,
  	FOREIGN KEY (MaKhoa) REFERENCES Khoa(MaKhoa)
  );
  GO
  
  CREATE TABLE GiaoVien (
      MaGV VARCHAR(15) PRIMARY KEY,
      TenGV NVARCHAR(50) NOT NULL,
  	NgaySinh DATE NOT NULL,
      MaBM VARCHAR(15) NOT NULL,
      FOREIGN KEY (MaBM) REFERENCES BoMon(MaBM)
  );
  GO
  
  CREATE TABLE GVCN (
      MaGV VARCHAR(15),
      MaLop VARCHAR(15),
  	HK INT NOT NULL,
  	PRIMARY KEY (MaLop, MaGV, HK),
      FOREIGN KEY (MaLop) REFERENCES Lop(MaLop),
  	FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV)
  );
  GO
  
  CREATE TABLE LopHP (
      MaLopHP VARCHAR(15) PRIMARY KEY,
      TenLopHP VARCHAR(15) NOT NULL,
      HK INT NOT NULL,
  	MaMon VARCHAR(15) NOT NULL,
  	MaGV VARCHAR(15) NOT NULL,
      FOREIGN KEY (MaMon) REFERENCES MonHoc(MaMon),
      FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV)
  );
  GO
  
  CREATE TABLE DKMH (
      MaLopHP VARCHAR(15) PRIMARY KEY,
      MaSV VARCHAR(13) NOT NULL,
      DiemTP FLOAT,
  	DiemThi FLOAT,
  	PhanTramThi FLOAT,
      FOREIGN KEY (MaLopHP) REFERENCES LopHP(MaLopHP),
      FOREIGN KEY (MaSV) REFERENCES SinhVien(MaSV)
  );
  GO

## Bai 4
# Tạo Database

![image](https://github.com/user-attachments/assets/5cf3f25b-430f-4509-be2d-0eec5a9d3d1b)

# Cùng các table dữ liệu:
* GiangVien
* MonHoc
* LopHoc
* ThoiKhoaBieu

# Table:

![image](https://github.com/user-attachments/assets/049da5be-b08a-4486-8a24-fde72590d4be)

làm tương tự với các table khác, lưu ý các table tạo phải đạt chuẩn 3NF.

Sau khi xong ta sẽ có sơ đồ như sau:

![image](https://github.com/user-attachments/assets/c6f5f92f-f530-4d33-8cee-fea6d9fea7a6)

# Nhập dữ liệu cho các bảng dữ liệu:
Lấy dữ liệu thời khóa biểu trong trang web http://tms.tnut.edu.vn

![image](https://github.com/user-attachments/assets/ecef1777-31a3-463a-b235-d87ed37e2521)

Nhập những dữ liệu đã có vào các bảng trong sql
Demo table ThoiKhoaBieu
![image](https://github.com/user-attachments/assets/fcdbbdad-453e-4472-b866-2901e50b6758)

Demo table GiangVien
![image](https://github.com/user-attachments/assets/5910ad9c-da38-4b39-abe0-52ffc138486c)

Demo table MonHoc
![image](https://github.com/user-attachments/assets/917dd04d-97d4-42f8-ad91-886ad4d2c444)

Demo table LopHoc
![image](https://github.com/user-attachments/assets/b30c88dc-7395-41ea-8ccb-5aee690e5c6c)

## Query truy vẫn thông tin:
![image](https://github.com/user-attachments/assets/ffb7cc19-2630-4601-a049-ee79f44af189)

~~~
USE bt4
GO
DECLARE @datetime1 DATETIME = '2025-04-16 06:30:00';
DECLARE @datetime2  DATETIME = '2025-04-16 09:10:00';
SELECT
    gv.HoTenGV AS "Họ Tên GV",
    mh.TenMH AS "Môn Dạy",
    tkb.GioBatDau AS "Giờ Vào Lớp",
    tkb.GioKetThuc AS "Giờ Ra"
FROM
    ThoiKhoaBieu tkb
JOIN
    GiangVien gv ON tkb.MaGV = gv.MaGV
JOIN
    MonHoc mh ON tkb.MaMH = mh.MaMH;

SELECT DISTINCT
    gv.HoTenGV AS "Giảng Viên Bận"
FROM
    ThoiKhoaBieu tkb
JOIN
    GiangVien gv ON tkb.MaGV = gv.MaGV
WHERE
    tkb.NgayHoc >= CAST(@datetime1 AS DATE) AND tkb.NgayHoc <= CAST(@datetime2 AS DATE)
    AND (
        (CAST(@datetime1 AS TIME) BETWEEN tkb.GioBatDau AND tkb.GioKetThuc) OR
        (CAST(@datetime2 AS TIME) BETWEEN tkb.GioBatDau AND tkb.GioKetThuc) OR
        (tkb.GioBatDau BETWEEN CAST(@datetime1 AS TIME) AND CAST(@datetime2 AS TIME)) OR
        (tkb.GioKetThuc BETWEEN CAST(@datetime1 AS TIME) AND CAST(@datetime2 AS TIME))
    );
~~~


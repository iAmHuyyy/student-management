# Student Management – Advanced Software Engineering Lab

## 1. Giới thiệu bài thực hành
**Student Management** là bài thực hành (Lab) nhằm mục đích giúp các Sinh viên nắm kiến thức cơ bản để xây dựng một Webapp bằng Java Spring Boot
### Bối Cảnh Bài Tập
Chúng ta sẽ xây dựng hệ thống Student Management API - một dịch vụ backend quản lý hồ sơ sinh viên. Hệ thống này đóng vai trò là lõi xử lý dữ liệu cho một ứng dụng quản lý trường học giả định.
### Chức năng chính
- Quản lý thông tin hồ sơ sinh viên (Tên, Email, Tuổi).
- Cung cấp API cho các ứng dụng Frontend (Web/Mobile) kết nối.
- Lưu trữ dữ liệu bền vững (Persistence) vào Database.
### Bài LAB gồm 5 phần
- Lab 1: Khởi tạo & Kiến trúc
- Lab 2: Xây dụng Backend REST API
- Lab 3: Xây dựng Frontend (SSR)
- Lab 4: Hoàn thiện sản phẩm
- Lab 5

---

## 2. Thông tin thành viên trong nhóm thực hiện

| Họ và tên        | MSSV       | Mã lớp |
|------------------|------------|--------|
| Nguyễn Nhật Huy  | 2311197   | L01 |
| Thân Thiên Kim    | 2311795   | L02 |

---

## 3. Trả lời câu hỏi các bài Lab

## Lab 1 – Câu hỏi và trả lời

### Câu 1: Dữ liệu lớn  
**Hãy thử thêm ít nhất 10 sinh viên nữa.**

**Trả lời:**  
Đã thực hiện thêm 10 sinh viên vào bảng `students` bằng câu lệnh `INSERT INTO`.  
Việc thêm nhiều bản ghi giúp mô phỏng dữ liệu thực tế và thuận tiện cho việc kiểm tra truy vấn, hiển thị danh sách sinh viên và xử lý dữ liệu trong ứng dụng Java.

---

### Câu 2: Ràng buộc Khóa Chính (Primary Key)  
**Cố tình Insert một sinh viên có `id` trùng với một người đã có sẵn.  
Quan sát thông báo lỗi: `UNIQUE constraint failed`.  
Tại sao Database lại chặn thao tác này?**

**Trả lời:**  
Cột `id` được khai báo là **PRIMARY KEY**, nên nó phải **duy nhất (UNIQUE)** cho mỗi bản ghi trong bảng.  
Khi cố tình insert một sinh viên có `id` trùng với `id` đã tồn tại, Database sẽ phát hiện vi phạm ràng buộc và chặn thao tác này, đồng thời trả về lỗi:
`UNIQUE constraint failed: students.id`
Cơ chế này giúp:
- Đảm bảo mỗi sinh viên được định danh duy nhất
- Tránh trùng lặp dữ liệu
- Bảo vệ tính toàn vẹn của Database

---

### Câu 3: Toàn vẹn dữ liệu (Constraints)  
**Thử Insert một sinh viên nhưng bỏ trống cột `name` (để NULL).  
Database có báo lỗi không?  
Từ đó suy nghĩ xem sự thiếu chặt chẽ này ảnh hưởng gì khi code Java đọc dữ liệu lên?**

**Trả lời:**  
Trong trường hợp cột `name` **không được khai báo `NOT NULL`**, Database **không báo lỗi** khi insert dữ liệu với `name = NULL`.

Điều này có thể gây ra các vấn đề khi code Java đọc dữ liệu:
- Dễ xảy ra lỗi `NullPointerException` khi xử lý chuỗi
- Giao diện hiển thị bị thiếu thông tin (tên sinh viên trống)
- Logic nghiệp vụ bị sai lệch (ví dụ: tìm kiếm, sắp xếp theo tên)

Vì vậy, trong thực tế cần:
- Khai báo ràng buộc `NOT NULL` cho các cột quan trọng như `name`, `email`
- Hoặc kiểm tra dữ liệu chặt chẽ ở tầng ứng dụng (Java) trước khi insert vào Database

---



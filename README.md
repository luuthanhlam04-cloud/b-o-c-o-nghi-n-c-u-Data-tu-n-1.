# Nghiên cứu tìm hiểu về Data - Tuần 1
## I. Linux cơ bản

### 1. Khái niệm
* **Hệ điều hành nhân Linux:** Là một kernel (nhân hệ điều hành) mã nguồn mở do Linus Torvalds khởi tạo vào năm 1991.
* Kernel này được sử dụng làm nền tảng để xây dựng nhiều bản phân phối Linux như Ubuntu, Debian, Fedora, CentOS.

### 2. Cấu trúc hệ thống tệp tin
Tuân theo tiêu chuẩn phân cấp hệ thống tập tin chuẩn:
* `/`: Gốc thư mục, chứa toàn bộ hệ thống.
* `/home`: Thư mục chứa dữ liệu người dùng (mỗi người dùng có một thư mục riêng).
* `/etc`: Chứa tệp cấu hình hệ thống và cấu hình dịch vụ.
* `/var`: Chứa dữ liệu thay đổi thường xuyên như log, cache.
* `/usr`: Chứa chương trình, thư viện, tài liệu dùng chung cho toàn hệ thống.

### 3. Các lệnh cơ bản
* `ls`: Liệt kê thư mục/tập tin.
* `cd`: Chuyển thư mục.
* `pwd`: In đường dẫn hiện tại.
* `cp`: Sao chép (nguồn -> đích).
* `mv`: Di chuyển hoặc đổi tên.
* `rm`: Xóa tập tin; `rm -r`: Xóa thư mục và nội dung.

### 4. Quản lý người dùng và quyền
* **chmod**: Thay đổi quyền truy cập (read - r, write - w, execute - x).
    * *Ví dụ:* `chmod 755 script.sh` (Đặt quyền đọc+ghi+chạy cho chủ sở hữu và chỉ đọc+chạy cho nhóm và người khác).
* **chown**: Thay đổi chủ sở hữu tập tin/thư mục.
    * *Ví dụ:* `chown user1:group1 data.txt`.

## II. Linux thao tác nâng cao

### 1. Quản lý Process (Tiến trình)
* `ps aux`: Liệt kê tất cả tiến trình (bao gồm PID, CPU sử dụng, RAM).
* `top`: Theo dõi tiến trình theo thời gian thực.
* `kill PID`: Gửi tín hiệu để dừng quá trình (dùng khi cần kết thúc tiến trình).
* `kill -9 PID`: Buộc dừng ngay lập tức bằng SIGKILL (chỉ dùng khi tiến trình không phản hồi).

### 2. Package Manager
Công cụ cài đặt, cập nhật, gỡ bỏ phần mềm dựa trên kho gói (repository).
* **apt** (Ubuntu/Debian): Kiểm tra phụ thuộc, tải gói, cài đặt file nhị phân và cấu hình.
    * `sudo apt update`: Chỉ cập nhật danh sách gói.
    * `sudo apt install tên_gói`: Tải và cài gói từ kho chính thức.
* **yum** (CentOS/RHEL): Hoạt động tương tự nhưng dựa trên kiến trúc RPM.

### 3. Cron Job & Log
* **Cron job**: Hệ thống dịch vụ chạy tác vụ theo lịch.
    * `crontab -e`: Mở tệp cấu hình cron hiện tại của người dùng.
    * Một dòng cron gồm 5 trường thời gian, kiểm tra từng phút để xác định lệnh chạy.
* **Log**:
    * `sudo tail -f /var/log/syslog`: Cho phép xem nhật ký dòng mới nhất theo thời gian thực.

## III. SQL cơ bản và trung cấp

**Khái niệm:** SQL (Structured Query Language) là ngôn ngữ chuẩn để làm việc với hệ thống cơ sở dữ liệu qua các lệnh SELECT, INSERT, UPDATE, DELETE.

### 1. Các khái niệm về RDBMS
* **Schema**: Nơi tổ chức dữ liệu trong một CSDL (chứa bảng, view, hàm). Giúp phân nhóm và phân tách các phần của hệ thống.
* **Table**: Bảng dữ liệu gồm hàng và cột. Mỗi cột có kiểu dữ liệu định nghĩa.
* **Primary Key (PK)**: Cột hoặc nhóm cột dùng để định danh duy nhất trên mỗi dòng (Không trùng lặp, không rỗng).
* **Foreign Key (FK)**: Cột tham chiếu tới khóa chính của bảng khác để đảm bảo tính nhất quán dữ liệu.

### 2. CRUD cơ bản
Bao gồm 4 hoạt động chính:
* **C**reate: `INSERT` (thêm dữ liệu).
* **R**ead: `SELECT` (truy vấn dữ liệu).
* **U**pdate: `UPDATE` (chỉnh sửa dữ liệu).
* **D**elete: `DELETE` (xóa dữ liệu).

### 3. JOIN
Dùng để hợp nhất dữ liệu từ nhiều bảng dựa trên quan hệ PK-FK.
* **INNER JOIN**: Trả về chỉ các dòng có từ khóa phù hợp ở cả hai bảng.
* **LEFT JOIN**: Giữ toàn bộ dòng bên trái, kể cả khi không có dòng tương ứng bên phải.

### 4. GROUP BY và các hàm chuẩn
* **GROUP BY**: Gom các dòng có cùng giá trị tại một hoặc nhiều cột thành từng nhóm.
* **Các hàm tổng hợp (Aggregations)**:
    * `COUNT(*)`: Đếm số dòng trong nhóm.
    * `COUNT(cột)`: Đếm số dòng không có cột null.
    * `SUM(cột)`: Tổng giá trị của cột.
    * `AVG(cột)`: Trung bình cộng.
    * `MAX(cột)` / `MIN(cột)`: Giá trị lớn nhất / nhỏ nhất.

## IV. SQL nâng cao

### 1. Transactions và ACID
* **Transaction**: Tập hợp nhiều câu lệnh SQL được xử lý như một đơn vị (Nếu 1 bước lỗi, toàn bộ bị hoàn tác).
* **ACID** (4 tính chất chuẩn):
    * *Atomicity*: Tất cả bước đều thực hiện hoặc không có bước nào được áp dụng.
    * *Consistency*: Dữ liệu sau transaction phải tuân thủ ràng buộc.
    * *Isolation*: Mỗi transaction không gây ảnh hưởng trung gian lên transaction khác.
    * *Durability*: Khi commit, dữ liệu được ghi bền vững.
* **Isolation levels**: Read Uncommitted, Read Committed, Repeatable Read, Serializable (mức cô lập cao nhất).

### 2. Indexing và tối ưu truy vấn
* **Index**: Cấu trúc dữ liệu (thường là B-Tree) giúp tìm kiếm nhanh hơn.
    * *Lợi ích*: Giảm thời gian quét bảng khi WHERE, JOIN, ORDER BY.
    * *Hạn chế*: Tăng chi phí khi INSERT/UPDATE/DELETE.
* **Query optimization**:
    * Tạo index trên cột dùng trong WHERE, JOIN.
    * Tránh `SELECT *` nếu không cần.
    * Dùng `EXPLAIN` để xem kế hoạch truy vấn (check xem engine dùng index hay scan toàn bảng).

### 3. Backup/Restore DB
* **Backup**: Sao lưu toàn bộ dữ liệu để phòng mất mát.
* **Restore**: Khôi phục lại từ file backup.

## V. NoSQL

**Tổng quan:** Loại cơ sở dữ liệu không dùng mô hình quan hệ truyền thống (RDBMS), thường dùng cho dữ liệu lớn, phân tán hoặc cấu trúc linh hoạt.
**DB Scripting:** Viết script để thao tác CRUD hoặc tác vụ tự động.

**Các loại NoSQL phổ biến:**
1.  **Key-value**: Lưu dạng cặp key-value (như dictionary), truy xuất nhanh theo key.
2.  **Document**: Lưu dạng document (JSON, BSON), cấu trúc linh hoạt.
3.  **Column**: Lưu theo cột, tối ưu cho bảng lớn nhiều cột nhưng ít truy vấn theo hàng.
4.  **Graph**: Lưu dạng đồ thị, biểu diễn quan hệ phức tạp (mạng xã hội, đề xuất sản phẩm).

## VI. DB Admin cơ bản

Kiến thức quản lý DB đảm bảo hoạt động ổn định và an toàn.

* **User & Role Management**:
    * *User*: Tài khoản truy cập DB.
    * *Role*: Nhóm quyền (permissions) gán cho user để kiểm soát hành động (SELECT, INSERT...).
* **Restore/Replication Concepts**:
    * *Restore*: Phục hồi dữ liệu từ backup khi gặp sự cố.
    * *Replication*: Sao chép dữ liệu từ DB này sang DB khác, giúp tăng tính sẵn sàng và dự phòng.# b-o-c-o-nghi-n-c-u-Data-tu-n-1.

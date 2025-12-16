# Ôn tập MySQL và PHP

## Ôn tập kiến thức

### 1. Form trong PHP

- Sử dụng `$_GET` để nhận dữ liệu từ URL query string (method GET):
    ```php
    $value = $_GET['key'] ?? 'default_value';
    ```

- Sử dụng `$_POST` để nhận dữ liệu từ form (method POST):
    ```php
    $value = $_POST['field_name'] ?? '';
    ```

- **Null Coalescing Operator** (`??`) giúp tránh lỗi khi key không tồn tại.

### 2. Include trong PHP

- `include` hoặc `require` để nhúng file PHP vào file khác:
    ```php
    include 'path/to/file.php';
    require 'path/to/file.php';
    ```

- Sự khác biệt:
    - `include`: hiển thị warning nếu file không tồn tại, code tiếp tục chạy
    - `require`: hiển thị fatal error và dừng code nếu file không tồn tại

- Sử dụng `include_once` hoặc `require_once` để tránh nhúng file nhiều lần.

### 3. MySQL - Cơ sở dữ liệu quan hệ

#### Khái niệm cơ bản

- **MySQL** là hệ quản trị cơ sở dữ liệu quan hệ (RDBMS) mã nguồn mở
- **Database** (CSDL): nơi lưu trữ dữ liệu có cấu trúc
- **Table** (Bảng): cấu trúc lưu trữ dữ liệu dưới dạng hàng và cột
- **Column** (Cột): thuộc tính/trường dữ liệu
- **Row** (Hàng): một bản ghi dữ liệu

#### Các câu lệnh SQL cơ bản

**SELECT - Truy vấn dữ liệu:**
```sql
SELECT * FROM ten_bang;
SELECT cot1, cot2 FROM ten_bang;
SELECT * FROM ten_bang WHERE dieu_kien;
```

**INSERT - Thêm dữ liệu:**
```sql
INSERT INTO ten_bang(cot1, cot2, cot3) 
VALUES('gia_tri1', 'gia_tri2', 'gia_tri3');
```

**UPDATE - Cập nhật dữ liệu:**
```sql
UPDATE ten_bang 
SET cot1 = 'gia_tri_moi' 
WHERE dieu_kien;
```

**DELETE - Xóa dữ liệu:**
```sql
DELETE FROM ten_bang WHERE dieu_kien;
```

### 4. Kết nối MySQL từ PHP

#### Thông tin kết nối

```php
$host = "127.0.0.1";      // hoặc localhost
$database = "ten_database";
$username = "root";       // tài khoản MySQL
$pwd = "";                // mật khẩu (mặc định rỗng với XAMPP)
```

#### Tạo kết nối với MySQLi

```php
$connection = new mysqli($host, $username, $pwd, $database);

// Kiểm tra kết nối
if ($connection->connect_error) {
    die("Kết nối thất bại: " . $connection->connect_error);
}
```

#### Thực thi câu lệnh SQL

**Cách 1: Sử dụng execute_query() (PHP 8.2+)**
```php
// Truy vấn dữ liệu
$sql = "SELECT * FROM san_pham";
$result = $connection->execute_query($sql);
$data = $result->fetch_all(MYSQLI_ASSOC);

// Thêm dữ liệu
$sql = "INSERT INTO san_pham(ten_san_pham, gia, mo_ta)
        VALUES('Laptop ASUS', 18000000, 'Mô tả laptop')";
$connection->execute_query($sql);
```

**Cách 2: Sử dụng query()**
```php
// Truy vấn dữ liệu
$sql = "SELECT * FROM san_pham";
$result = $connection->query($sql);
$data = $result->fetch_all(MYSQLI_ASSOC);

// Thêm dữ liệu
$sql = "INSERT INTO san_pham(ten_san_pham, gia, mo_ta)
        VALUES('Laptop ASUS', 18000000, 'Mô tả laptop')";
$connection->query($sql);
```

#### Xử lý kết quả truy vấn

**fetch_all(MYSQLI_ASSOC)** - Lấy tất cả bản ghi dưới dạng mảng kết hợp:
```php
$data = $result->fetch_all(MYSQLI_ASSOC);
// Kết quả: mảng 2 chiều, mỗi phần tử là 1 bản ghi
```

**fetch_assoc()** - Lấy từng bản ghi:
```php
while ($row = $result->fetch_assoc()) {
    echo $row['ten_san_pham'];
}
```

**fetch_array()** - Lấy bản ghi dưới dạng mảng số hoặc kết hợp:
```php
$row = $result->fetch_array(MYSQLI_BOTH);
```

#### Đóng kết nối

```php
$connection->close();
```

## Bài tập thực hành

### Bài tập 1: Hiển thị danh sách sản phẩm

Viết chương trình hiển thị danh sách sản phẩm dưới dạng bảng HTML.

- **Tên file:** danh_sach_san_pham.php
- **Yêu cầu:**
  - Kết nối database
  - Truy vấn tất cả sản phẩm
  - Hiển thị dưới dạng bảng với các cột: STT, Tên sản phẩm, Giá, Mô tả

### Bài tập 2: Thêm sản phẩm từ form

Viết chương trình thêm sản phẩm mới từ form.

- **Tên file:** them_san_pham.php
- **Yêu cầu:**
  - Tạo form nhập liệu với các trường: Tên sản phẩm, Giá, Mô tả
  - Nhận dữ liệu từ form bằng `$_POST`
  - Thêm vào database bằng câu lệnh INSERT
  - Hiển thị thông báo thành công/thất bại

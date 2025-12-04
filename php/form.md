# PHP Forms và Xử lý Dữ liệu Form

## Ôn tập kiến thức

### 1. Thẻ `<form>` và các thuộc tính
Thẻ `<form>` được sử dụng để tạo biểu mẫu HTML để thu thập dữ liệu người dùng.

**Cú pháp cơ bản:**
```php
<form method="GET" action="file_xu_ly.php">
    <!-- Các phần tử form -->
</form>
<form method="GET" action="file_xu_ly.php">
    <!-- Các phần tử form -->
</form>
```

**Các thuộc tính quan trọng:**
- `method`: Xác định cách gửi dữ liệu (GET hoặc POST, mặc định GET)
- `action`: Chỉ định file sẽ nhận dữ liệu của form. Nếu không chỉ định sẽ gửi cho chính file hiện tịa
- `enctype`: Xác định cách mã hóa dữ liệu, quan trọng cho upload file

### 2. Thẻ `<input>` và các loại input
Thẻ `<input>` là phần tử quan trọng nhất trong form. Để gửi được dữ liệu cho server nói chung (không phải mỗi PHP), thẻ `<input>` cần có thuộc tính `name`.

**Các loại input phổ biến:**
```php
<input type="text" name="username">        // Ô nhập văn bản
<input type="password" name="password">    // Ô nhập mật khẩu
<input type="email" name="email">          // Ô nhập email
<input type="number" name="age">           // Ô nhập số
<input type="date" name="birthday">        // Ô chọn ngày
<input type="checkbox" name="hobbies[]">   // Hộp kiểm (có thể chọn nhiều)
<input type="radio" name="gender">         // Nút radio (chỉ chọn một)
<input type="file" name="avatar">          // Chọn file
<input type="submit" value="Gửi">         // Nút gửi form
<input type="reset" value="Xóa">          // Nút xóa form
<textarea name="message"></textarea>      // Ô nhập văn bản nhiều dòng
<select name="city">                      // Danh sách chọn
    <option value="hanoi">Hà Nội</option>
    <option value="hcm">TP.HCM</option>
</select>
```

### 3. Biến `$_GET`
- Dữ liệu được gửi qua URL
- Hiển thị trong thanh địa chỉ
- Giới hạn về độ dài
- Dùng cho dữ liệu không nhạy cảm

```php
// URL: index.php?name=John&age=25
if (isset($_GET['name'])) {
    echo "Xin chào " . $_GET['name'];
}
```

### 4. Biến `$_POST`
- Dữ liệu được gửi ẩn (không hiển thị trong URL)
- Không giới hạn độ dài
- An toàn hơn cho dữ liệu nhạy cảm
- Dùng cho form đăng nhập, đăng ký

```php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $username = $_POST['username'];
    $password = $_POST['password'];
}
```

### 5. Biến `$_REQUEST`
- Chứa cả dữ liệu từ `$_GET`, `$_POST` và `$_COOKIE`
- Ít sử dụng vì lý do bảo mật

### 6. Xử lý dữ liệu form cơ bản
```php
<?php
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    // Kiểm tra dữ liệu đã được gửi chưa
    if (isset($_POST['username'])) {
        $username = htmlspecialchars($_POST['username']);
        echo "Tên người dùng: " . $username;
    }
}
?>
```

## Bài Tập Thực Hành

### Bài 1: Form Tính Toán Đơn Giản
**Yêu cầu:** Tạo form tính tổng, hiệu, tích, thương của hai số

**Chi tiết:**
1. Tạo file `bai1.php`
2. Tạo form với các trường:
   - Số thứ nhất (number input)
   - Số thứ hai (number input)
   - Phép toán (select với các option: Cộng, Trừ, Nhân, Chia)
   - Nút tính toán (submit)
3. Xử lý dữ liệu:
   - Sử dụng phương thức POST
   - Kiểm tra nếu số thứ hai là 0 khi chọn phép chia
   - Hiển thị kết quả dưới form

**Ví dụ output:**
```
Kết quả: 10 + 5 = 15
```

---

### Bài 2: Form Đăng Ký Người Dùng
**Yêu cầu:** Tạo form đăng ký người dùng với validation cơ bản

**Chi tiết:**
1. Tạo file `bai2.php`
2. Form gồm các trường:
   - Họ và tên (text, required)
   - Email (email, required)
   - Mật khẩu (password, required, min 6 ký tự)
   - Xác nhận mật khẩu (password, required)
   - Ngày sinh (date)
   - Giới tính (radio: Nam, Nữ, Khác)
   - Sở thích (checkbox: Đọc sách, Nghe nhạc, Thể thao, Du lịch)
   - Thành phố (select: Hà Nội, Đà Nẵng, TP.HCM, Cần Thơ)
3. Xử lý validation:
   - Kiểm tra các trường bắt buộc
   - Email phải đúng định dạng
   - Mật khẩu và xác nhận mật khẩu phải giống nhau
   - Người dùng phải từ 18 tuổi trở lên
4. Hiển thị thông báo lỗi nếu có
5. Hiển thị thông tin đã đăng ký nếu thành công

---

### Bài 3: Form Tìm Kiếm và Bộ Lọc
**Yêu cầu:** Tạo form tìm kiếm sản phẩm với bộ lọc

**Chi tiết:**
1. Tạo file `bai3.php`
2. Có sẵn mảng sản phẩm:
```php
$products = [
    ['id' => 1, 'name' => 'iPhone 13', 'price' => 20000000, 'category' => 'điện thoại'],
    ['id' => 2, 'name' => 'Samsung Galaxy', 'price' => 15000000, 'category' => 'điện thoại'],
    ['id' => 3, 'name' => 'MacBook Air', 'price' => 30000000, 'category' => 'laptop'],
    ['id' => 4, 'name' => 'Dell XPS', 'price' => 25000000, 'category' => 'laptop'],
    ['id' => 5, 'name' => 'Tai nghe Sony', 'price' => 2000000, 'category' => 'phụ kiện'],
];
```
3. Tạo form tìm kiếm với:
   - Từ khóa tìm kiếm (text input)
   - Khoảng giá (number inputs: giá từ, giá đến)
   - Danh mục (checkbox: điện thoại, laptop, phụ kiện)
   - Sắp xếp (select: giá tăng dần, giá giảm dần, tên A-Z)
   - Nút tìm kiếm (submit, method GET)
4. Xử lý tìm kiếm:
   - Lọc theo từ khóa (tìm trong tên sản phẩm)
   - Lọc theo khoảng giá
   - Lọc theo danh mục
   - Sắp xếp kết quả
5. Hiển thị kết quả dạng bảng

**Yêu cầu bổ sung:**
- Nếu không có sản phẩm nào phù hợp, hiển thị thông báo không tìm thấy
- Hiển thị tổng số sản phẩm tìm được


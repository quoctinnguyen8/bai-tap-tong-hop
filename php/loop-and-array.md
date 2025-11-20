# Bài tập Vòng lặp và Mảng trong PHP

## Ôn tập kiến thức

### 1. Mảng (Array)

Mảng là biến đặc biệt có thể lưu trữ nhiều giá trị cùng một lúc.

**Mảng tuần tự (Indexed Array)**: Key là số nguyên tự động tăng từ 0.

```php
$colors = ["Red", "Green", "Blue"];
echo $colors[0] // Red
```

**Mảng kết hợp (Associative Array)**: Key là chuỗi do người dùng tự định nghĩa.

```php
$student = [
    "name" => "Nam",
    "age" => 20,
    "score" => 8.5
];

echo $student['name'] // Nam
```

#### Các hàm/lệnh thường dùng với mảng:

`count($array)`: Đếm số phần tử trong mảng.

`print_r($array)` hoặc `var_dump($array)`: In cấu trúc mảng ra màn hình để kiểm tra (debug).

### 2. Vòng lặp (Loop)

**Vòng lặp for:** Dùng khi biết trước số lần lặp (thường dùng cho mảng tuần tự).

```php
for ($i = 0; $i < count($colors); $i++) {
    echo $colors[$i];
}
```

**Vòng lặp foreach:** Chuyên dùng để duyệt mảng (cả tuần tự và kết hợp).

Dạng 1 - chỉ lấy value:

```php
foreach ($colors as $value) {
    echo $value;
}
```

Dạng 2 - lấy cả key và value:

```php
foreach ($student as $key => $value) {
    echo "$key: $value";
}
```

### 3. Kết hợp HTML và PHP (bổ sung)

Khi hiển thị dữ liệu mảng ra giao diện (ví dụ: danh sách `<ul>` hoặc bảng `<table>`), ta thường nhúng PHP vào HTML:

```php
<ul>
    <?php foreach ($colors as $c): ?>
        <li><?php echo $c; ?></li>
    <?php endforeach; ?>
</ul>
```

## Bài tập

Tất cả các bài tập dưới đây sử dụng giá trị nhận từ URL bằng `$_GET` và toán tử `??` để gán mặc định.

### Bài tập 1

Viết chương trình in ra bảng cửu chương của một số n nhận từ URL.

- **Tên file:** baitap1_loop.php
- **Logic:** Nhận biến n. Sử dụng vòng lặp `for` để in kết quả phép nhân.
- **URL truy cập:** `/baitap1_loop.php?n=5`
- **Kết quả hiển thị:**
    > 5 x 1 = 5
    >
    > 5 x 2 = 10
    >
    > ...
    >
    > 5 x 10 = 50

### Bài tập 2

Viết chương trình tạo ra một mảng các số nguyên từ 1 đến n (với n lấy từ URL). Tính tổng các số chẵn có trong mảng đó.

- **Tên file:** baitap2_loop.php
- **Logic:**
    - Tạo mảng chứa các số từ 1 đến n.
    - Duyệt mảng vừa tạo bằng foreach.
    - Kiểm tra nếu số chia hết cho 2 thì cộng vào biến tổng.
- **URL truy cập:** `/baitap2_loop.php?n=10`

- **Kết quả:**
    - Dãy số: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    - Tổng các số chẵn là: 30 (Giải thích: 2+4+6+8+10)

### Bài tập 3

Viết chương trình cho phép người dùng nhập mã quốc gia (key) viết liền không dấu từ URL và hiển thị tên đầy đủ của quốc gia đó.

- **Tên file:** baitap3_country_lookup.php

    Dữ liệu mẫu, khai báo sẵn trong file PHP:
    ```php
    $countries = [
        "vietnam" => "Cộng hòa Xã hội Chủ nghĩa Việt Nam",
        "thailan" => "Vương quốc Thái Lan",
        "singapore" => "Cộng hòa Singapore",
        "nhatban" => "Nhật Bản",
        ...
    ];
    ```

- **Logic:** 
    - Nhận tham số `country_code` từ URL (mặc định là chuỗi rỗng "").
    - Kiểm tra `country_code` có tồn tại trong mảng `$countries` hay không.
    - Nếu tìm thấy, hiển thị tên đầy đủ của quốc gia.
    - Nếu không tìm thấy, hiển thị thông báo "Không tìm thấy quốc gia với mã này."
- **URL truy cập:** `/baitap3_country_lookup.php?country_code=singapore`
- **Kết quả:** Tên quốc gia: Cộng hòa Singapore
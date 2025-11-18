# Bài tập cấu trúc rẽ nhánh PHP

## Ôn tập kiến thức

- Biến trong PHP dùng dấu `$` ở đầu và không có kiểu dữ liệu cố dịnh.
- Biến trong PHP có phân biệt hoa - thường.
- Khi sử dụng các phép toán số học, PHP tự ép kiểu các biến về dạng số, trường hợp không thể chuyển về dạng số sẽ hiển thị warning (cảnh báo)
- Sử dụng biến `$_GET` có sẵn của PHP để nhận giá trị từ Query String của URL. Cú pháp như sau:

    ```php
    $var = $_GET['<key>'];
    ```

    Ví dụ: với URL là `/index.php?year=2007`
    Để nhận được giá trị 2007 từ `year` ta sử dụng cú pháp

    ```php
    $y = $_GET['year'];
    ```

    **Lưu ý:** nếu URL không có 'year' dòng code trên sẽ bị lỗi
    Để đảm bảo code chạy đúng trong mọi trường hợp, sử **Null Coalescing Operator** (toán tử gộp null) để cung cấp giá trị mặc định trong trường hợp không có giá trị `year`.
    ```php
    // y = 1900 nếu URL không có param 'year'
    $y = $_GET['year'] ?? 1900;
    ```

## Bài tập

Tất cả các bài tập dưới đây sử dụng giá trị nhận từ URL (bằng `$_GET` đã học ở trên)

### Bài tập 1

Viết chương trình kiểm tra tháng nhận được thuộc quý thứ mấy trong năm.

- **Tên file:** baitap1.php
- **URL truy cập:** `/baitap1.php?thang=10`
- **Kết quả:** Quý IV

### Bài tập 2

Viết chương trình kiểm tra tháng, năm nhận được có bao nhiêu ngày.

- **Tên file:** baitap2.php
- **URL truy cập:** `/baitap2.php?nam=2004&thang=2`
- **Kết quả:** Tháng 2 năm 2004 có 29 ngày

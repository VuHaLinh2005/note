#table


Trong một bảng HTML, các ô trong hàng `<thead>` (thẻ `<th>`) và các ô trong hàng `<tbody>` (thẻ `<td>`) **liên quan với nhau về độ rộng** bởi vì trình duyệt xử lý bảng theo cách toàn cục: nó căn chỉnh các cột theo cấu trúc **bố cục dạng bảng** (table layout).

### Lý do tại sao ô `<th>` và `<td>` có liên quan đến nhau:

1. **Bảng HTML hoạt động như một lưới**:
    
    - Bảng được tổ chức theo các **hàng (`<tr>`)** và **cột**, chứ không phải chỉ từng ô riêng lẻ.
    - Trình duyệt tự động phân bổ không gian cho mỗi **cột** trong bảng dựa trên:
        - Nội dung của tất cả các ô trong cột đó (bao gồm cả `<th>` và `<td>`).
        - Các thuộc tính CSS (nếu được áp dụng, như `width`).
    - Mỗi cột có cùng độ rộng từ trên xuống dưới bảng, bao gồm cả tiêu đề (`<th>`) và dữ liệu (`<td>`).
2. **Quy trình tính toán độ rộng của bảng:**
    
    - Trình duyệt sẽ:
        1. Kiểm tra nội dung trong các ô của từng cột.
        2. Tìm **độ rộng lớn nhất** cần thiết để hiển thị nội dung trong mỗi cột.
        3. **Áp dụng** độ rộng đó cho **toàn bộ** cột, từ `<thead>` đến `<tbody>`.

```html
<table border="1">
  <thead>
    <tr>
      <th>Short</th>
      <th>Very Long Header Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>123</td>
      <td>Data</td>
    </tr>
  </tbody>
</table>

```


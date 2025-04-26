#static


### 4. Sự khác biệt giữa phương thức static và thuộc tính static:

| **Tiêu chí**          | **Phương thức static**                                         | **Thuộc tính static**                                            |
| --------------------- | -------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Thuộc về**          | Thuộc về lớp, không phụ thuộc vào đối tượng                    | Thuộc về lớp, được chia sẻ bởi tất cả các đối tượng              |
| **Truy cập**          | Có thể truy cập mà không cần tạo đối tượng                     | Có thể truy cập mà không cần tạo đối tượng                       |
| **Khả năng thay đổi** | Không thể truy cập trực tiếp các thuộc tính instance           | Có thể thay đổi giá trị và sẽ ảnh hưởng đến tất cả các đối tượng |
| **Dùng khi nào**      | Dùng khi nhiệm vụ không phụ thuộc vào trạng thái của đối tượng | Dùng để lưu trữ dữ liệu chung cho tất cả các đối tượng           |
| **Cú pháp truy cập**  | Gọi bằng `TênLớp.phươngThức()`                                 | Gọi bằng `TênLớp.thuộcTính`                                      |
|                       |                                                                |                                                                  |

### 5. Khi nào nên sử dụng `static`?

- **Phương thức static**: Khi bạn cần thực hiện một thao tác không phụ thuộc vào trạng thái của đối tượng (ví dụ: các phương thức tiện ích, toán học).
- **Thuộc tính static**: Khi bạn cần lưu trữ dữ liệu chung cho tất cả các đối tượng của lớp, chẳng hạn như bộ đếm số lượng đối tượng đã được tạo.



| Header 1sdfsđ                | Header 3   |     |
| ---------------------------- | ---------- | --- |
| Row 1 Col1fsdfsdfds          | Row 1 Col3 |     |
| Row 2 Col1fsdfsd<br>hhkhhkkk | Row 2 Col3 |     |
|                              |            |     |





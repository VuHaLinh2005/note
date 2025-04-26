#joinColumn

Đúng vậy, khi trình biên dịch hoặc runtime framework (như Hibernate trong JPA) **quét đến `@JoinColumn`**, nó sẽ **sử dụng reflection** để:

1. **Xác định kiểu dữ liệu của thuộc tính**: Dựa vào kiểu của thuộc tính (ví dụ: `DanhMuc` trong `SanPham`), framework biết đây là một lớp khác được đánh dấu là một **thực thể (`@Entity`)**.
    
2. **Xác định bảng liên kết**: Dùng reflection, framework sẽ kiểm tra lớp `DanhMuc` và lấy metadata về bảng mà lớp này ánh xạ đến (thông qua `@Table` hoặc tên lớp mặc định) để biết **bảng nào cần tạo khóa ngoại**.
    
3. **Tạo khóa ngoại**: Framework dùng thông tin từ `@JoinColumn` (nếu có) để đặt tên cho cột khóa ngoại trong bảng hiện tại, hoặc dùng tên mặc định nếu `@JoinColumn` không được chỉ định.
    

### 🧩 Tóm lại:

Framework **dùng reflection** để xác định bảng cần liên kết khi gặp `@JoinColumn`, từ đó tự động tạo khóa ngoại để liên kết bảng dựa trên kiểu dữ liệu của thuộc tính và metadata từ các annotation.
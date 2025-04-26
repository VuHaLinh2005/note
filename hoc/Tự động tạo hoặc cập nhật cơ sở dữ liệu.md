

## do cấu hình trong application.properties
**Cấu hình `hibernate.hbm2ddl.auto`**
`spring.jpa.hibernate.ddl-auto=update`

- Đây là cấu hình quan trọng nhất để Hibernate tự động **tạo và cập nhật bảng**.
- Với **`update`**, Hibernate sẽ **chỉ tạo các bảng nếu chúng chưa tồn tại**, hoặc **cập nhật bảng có sẵn** để thêm các cột mới (nếu có thay đổi trong entity), nhưng không xóa dữ liệu cũ.
- Các tùy chọn khác như `create` (tạo mới tất cả bảng mỗi lần, xóa dữ liệu cũ) hoặc `none` (không thay đổi gì trong cơ sở dữ liệu) cũng có thể được dùng tùy vào nhu cầu.
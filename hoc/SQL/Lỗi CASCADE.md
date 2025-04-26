
- **Xung đột CASCADE**: SQL Server không thích khi một bảng có nhiều khóa ngoại tham chiếu đến cùng một bảng mẹ với các hành động xóa tự động (SET NULL, CASCADE). Dùng NO ACTION là cách an toàn nhất.
- **Kiểm tra trước khi thêm khóa ngoại**: Khi thêm khóa ngoại, thử dùng NO ACTION trước nếu nghi ngờ có xung đột.
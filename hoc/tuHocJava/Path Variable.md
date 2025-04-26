 

- **Path Variable**(**Biến trong đường dẫn**): Là **~={red}bắt buộc=~**, vì nó là **~={red}một phần=~** của đường dẫn dùng để xác định **~={red}tài nguyên=~** cụ thể. Nếu không có, đường dẫn sẽ không hợp lệ.
    
    - Ví dụ: `/users/{id}` → `/users/123` (ID là bắt buộc để biết cần lấy user nào).
- **Query String**: Là ~={red}**tùy chọn**=~, chỉ dùng để **~={red}bổ sung=~** thêm thông tin hoặc lọc dữ liệu. Nếu không có, hệ thống vẫn hiểu đường dẫn cơ bản.
    
    - Ví dụ: `/users?name=John` → `/users` vẫn hợp lệ (có thể trả danh sách tất cả users).

Kết luận: **Path Variable bắt buộc**. **Query String không bắt buộc**.


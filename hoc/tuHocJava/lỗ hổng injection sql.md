Bạn nói đúng, trong ví dụ tôi đưa ra nếu chỉ có `OR '1'='1'` mà thiếu phần xử lý cho mệnh đề `AND password = ...` thì câu truy vấn vẫn sẽ bị ràng buộc bởi điều kiện về password.  Tôi đã đơn giản hóa ví dụ để dễ hiểu hơn, nhưng thực tế kẻ tấn công có nhiều kỹ thuật tinh vi hơn để vượt qua điều kiện này.

Để rõ hơn, tôi xin đưa ra một ví dụ cụ thể hơn về cách kẻ tấn công có thể khai thác lỗ hổng SQL Injection ngay cả khi có mệnh đề `AND`:

**Kỹ thuật comment out:**

Kẻ tấn công có thể sử dụng ký tự `--` (comment trong SQL) để vô hiệu hóa phần còn lại của câu lệnh SQL.  Ví dụ:

Người dùng nhập vào `username` là `' OR '1'='1' --` và `password` bất kỳ.  Câu lệnh SQL sẽ trở thành:

```sql
String sql = "SELECT * FROM users WHERE username = '' OR '1'='1' --' AND password = '" + password + "'";
```

Phần `--' AND password = '" + password + "'` sẽ bị coi là comment và không được thực thi.  Kết quả là câu truy vấn chỉ còn lại `SELECT * FROM users WHERE username = '' OR '1'='1'`, vẫn trả về tất cả người dùng.

**Kỹ thuật sử dụng UNION:**

Kẻ tấn công có thể sử dụng mệnh đề `UNION` để kết hợp kết quả của nhiều câu truy vấn. Ví dụ, nếu kẻ tấn công muốn lấy danh sách tất cả các bảng trong cơ sở dữ liệu, chúng có thể nhập `username` là `' UNION SELECT table_name FROM information_schema.tables --` và `password` bất kỳ. Câu truy vấn sẽ trở thành:

```sql
String sql = "SELECT * FROM users WHERE username = '' UNION SELECT table_name FROM information_schema.tables -- ' AND password = '" + password + "'";
```

Phần sau `--` lại bị comment out. Câu truy vấn sẽ trả về kết quả của hai câu truy vấn được nối với nhau bởi `UNION`.  Nếu cấu trúc cột của hai bảng tương thích, kẻ tấn công sẽ nhận được danh sách các bảng trong cơ sở dữ liệu.

## or
```js
String sql = "SELECT * FROM users WHERE username = '' OR '1'='1' --' AND password = '" + password + "'";
```
-- : **comment**

**Kết luận:**

Kẻ tấn công có nhiều cách tinh vi để khai thác lỗ hổng SQL Injection, ngay cả khi có các mệnh đề `AND` trong câu truy vấn.  Do đó, việc sử dụng `PreparedStatement` là **bắt buộc** để ngăn chặn hoàn toàn SQL Injection.  `PreparedStatement` sẽ xử lý các tham số riêng biệt với câu lệnh SQL, đảm bảo rằng đầu vào của người dùng không thể được diễn giải thành mã SQL.
**[[PreparedStatement và lỗ hổng injection sql | cách preparedStatement giải quyết nó >.<]]**



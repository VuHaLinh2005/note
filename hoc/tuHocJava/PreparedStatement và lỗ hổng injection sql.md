`PreparedStatement` giải quyết vấn đề SQL Injection bằng cách tách biệt hoàn toàn câu lệnh SQL và dữ liệu đầu vào. Thay vì ghép trực tiếp dữ liệu vào câu lệnh SQL (điều này tạo ra lỗ hổng), `PreparedStatement` sử dụng một cơ chế *tham số hóa*.

Hãy xem chi tiết cách `PreparedStatement` hoạt động và tại sao nó ngăn chặn được SQL Injection:

**1. Biên dịch trước:**

Khi bạn tạo một `PreparedStatement`, câu lệnh SQL được **gửi** đến máy chủ cơ sở dữ liệu để ***biên dịch trước***.  Điều này có nghĩa là máy chủ cơ sở dữ liệu sẽ phân tích cú pháp, tối ưu hóa và tạo một kế hoạch thực thi cho câu lệnh SQL ***mà không cần biết giá trị cụ thể của các tham số***.

**2. Tham số hóa:**

Trong câu lệnh SQL của `PreparedStatement`, các tham số được biểu diễn bằng dấu hỏi chấm (`?`).  Ví dụ:

```sql
String sql = "SELECT * FROM users WHERE username = ? AND password = ?";
PreparedStatement pstmt = connection.prepareStatement(sql);
```

**3. Đặt giá trị tham số:**

Sau khi tạo `PreparedStatement`, bạn sử dụng các phương thức `setXXX()` (như `setString()`, `setInt()`, `setDate()`, v.v.) để đặt giá trị cho các tham số.  Quan trọng là, các giá trị này được xử lý như *dữ liệu*, **không phải là một phần của câu lệnh SQL**.

```java
pstmt.setString(1, username);
pstmt.setString(2, password);
```

**4. Thực thi:**

Khi bạn gọi `pstmt.executeQuery()`, máy chủ cơ sở dữ liệu sẽ sử dụng kế hoạch thực thi đã được biên dịch trước và *chỉ* thay thế các dấu hỏi chấm bằng các giá trị tham số đã được đặt.  

**Ví dụ so sánh:**

* **Cách dễ bị tấn công (nối chuỗi):**

```sql
String sql = "SELECT * FROM users WHERE username = '" + username + "'"; // username = "' OR '1'='1"
```

Nếu `username` là `' OR '1'='1`, toàn bộ chuỗi này được ghép lại thành một câu lệnh SQL mới, và điều kiện `OR '1'='1'` sẽ luôn đúng.

* **Cách an toàn (PreparedStatement):**

```sql
String sql = "SELECT * FROM users WHERE username = ?";
PreparedStatement pstmt = connection.prepareStatement(sql);
pstmt.setString(1, username); // username = "' OR '1'='1"
```

Ngay cả khi `username` là `' OR '1'='1'`, giá trị này chỉ được coi là **dữ liệu** và được so sánh trực tiếp với cột `username`.  Nó **không ảnh hưởng** đến **cấu trúc** của câu lệnh **SQL**.

**Tóm lại:**

`PreparedStatement` ngăn chặn SQL Injection bằng cách **tách biệt câu lệnh SQL và dữ liệu**, đảm bảo rằng dữ liệu đầu vào không thể được diễn giải thành mã SQL.  

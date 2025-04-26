#statement


OK, hãy tưởng tượng **Statement** giống như **một tờ giấy ghi lệnh** mà bạn đưa cho cơ sở dữ liệu để nó thực hiện. Cụ thể hơn:

1. **Statement là gì?**
    
    --> **Statement** là một đối tượng trong Java JDBC giúp bạn **gửi các lệnh SQL** đến cơ sở dữ liệu.
    - Khi bạn muốn yêu cầu cơ sở dữ liệu làm gì đó (ví dụ, chọn dữ liệu từ bảng hoặc thêm dữ liệu vào bảng), bạn phải viết lệnh SQL và gửi nó đi – `Statement` giúp bạn thực hiện việc này.
2. **Statement dùng để làm gì?**
    
    - **Statement** là công cụ để **chạy các lệnh SQL** (như `SELECT`, `INSERT`, `UPDATE`, `DELETE`) từ Java đến cơ sở dữ liệu.
    - **Khi bạn tạo `Statement`, bạn viết lệnh SQL vào đó, và `Statement` sẽ gửi lệnh này qua `Connection` đến cơ sở dữ liệu.**
3. **Cách hoạt động của Statement trong thực tế**
    
    - Khi bạn có kết nối (`Connection`) tới cơ sở dữ liệu, bạn tạo một `Statement` từ kết nối đó.
    - Sau đó, bạn viết lệnh SQL và sử dụng `Statement` để thực thi lệnh này.
    
    Ví dụ đơn giản:
    
    
    
    
   ```java

    // Tạo một Statement từ đối tượng Connection 
    Statement stmt = conn.createStatement();  // Thực thi lệnh SQL để lấy dữ liệu từ bảng "users" 
    ResultSet rs = stmt.executeQuery("SELECT * FROM users");`
    ```
    
4. **Kết quả của Statement**
    
    - Khi bạn thực thi lệnh SQL bằng `Statement`, nếu đó là lệnh `SELECT`, cơ sở dữ liệu sẽ trả về dữ liệu trong một đối tượng `ResultSet`.
    - Còn nếu là lệnh `INSERT`, `UPDATE`, hay `DELETE`, `Statement` sẽ trả về số hàng đã thay đổi trong cơ sở dữ liệu.
5. **Tóm lại: Statement giống như một công cụ để gửi lệnh SQL**
    
    - Bạn có `Connection` (kết nối) đến cơ sở dữ liệu.
    - Bạn tạo `Statement` từ `Connection`, viết lệnh SQL vào đó.
    - `Statement` sẽ thực thi lệnh SQL, giúp bạn “nói” cho cơ sở dữ liệu biết cần làm gì.

Nói cách khác, **Statement là cây cầu giúp bạn gửi lệnh SQL từ Java đến cơ sở dữ liệu**.

Bạn hiểu đúng rồi, về cơ bản, **`Statement` không phải là đối tượng thực thi câu lệnh SQL trực tiếp với cơ sở dữ liệu mà chỉ là công cụ để chuẩn bị và gửi lệnh**. Cụ thể:

1. **`Connection` mới là đối tượng thực hiện kết nối thực sự** với cơ sở dữ liệu và giữ phiên làm việc.
2. **`Statement`** chỉ là phương tiện để chuẩn bị và gửi lệnh SQL đến cơ sở dữ liệu **thông qua `Connection`.**

### Quy trình cụ thể

- **Tạo kết nối**: Đầu tiên, bạn cần tạo một `Connection` đến cơ sở dữ liệu, đây là bước giúp ứng dụng Java kết nối trực tiếp với cơ sở dữ liệu.
- **Tạo `Statement` từ `Connection`**: Sau khi kết nối thành công, bạn sử dụng `Connection` để tạo `Statement`.
- **Gửi lệnh SQL qua `Statement`**: Khi bạn viết một lệnh SQL và gọi phương thức `executeQuery` hoặc `executeUpdate` từ `Statement`, **chính `Connection` sẽ gửi câu lệnh đến cơ sở dữ liệu** và thực thi lệnh. `Statement` chỉ là phương tiện trung gian giúp cấu hình và gửi lệnh này.
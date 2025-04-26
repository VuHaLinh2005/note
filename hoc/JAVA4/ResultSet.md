#resultset


`ResultSet` không chỉ đơn giản là một nơi để lưu dữ liệu – nó thực chất là **một bảng dữ liệu trả về từ cơ sở dữ liệu** và **cho phép Java truy cập vào từng hàng và từng cột của dữ liệu đó**. Để hiểu rõ hơn:

### 1. **ResultSet lưu dữ liệu theo cấu trúc của bảng**

- Khi bạn thực thi một lệnh `SELECT` bằng `Statement`, **dữ liệu trả về từ cơ sở dữ liệu thường có cấu trúc giống như một bảng (với hàng và cột).** --> **nó gắn luôn vô result**
- `ResultSet` sẽ lưu dữ liệu này theo cấu trúc đó, giống như một **phiên bản tạm thời của bảng** trong Java, nơi mỗi hàng chứa một bản ghi và mỗi cột chứa một trường dữ liệu từ bảng trong cơ sở dữ liệu.

### 2. **Truy cập dữ liệu qua tên cột hoặc vị trí cột**

- Để lấy dữ liệu từ `ResultSet`, bạn cần biết **tên cột** (hoặc vị trí của cột) trong bảng mà bạn muốn lấy dữ liệu. Ví dụ, nếu bạn có cột tên là `"username"`, bạn có thể lấy giá trị của nó như sau:
    
    
    
    `String username = resultSet.getString("username");`
    
- `ResultSet` sử dụng tên cột để **biết bạn muốn lấy dữ liệu từ cột nào**. Bạn cũng có thể sử dụng **chỉ số của cột** (bắt đầu từ 1) nếu không biết tên cột:
    
    
    `String username = resultSet.getString(1); // Lấy dữ liệu từ cột đầu tiên`
    

### 3. **Duyệt qua từng hàng trong ResultSet**

- `ResultSet` cho phép bạn **duyệt qua từng hàng (record)** của dữ liệu trả về. Bạn có thể dùng vòng lặp `while` để đọc từng hàng trong `ResultSet`:
    
    
    ```java

`while (resultSet.next()) { // Duyệt qua từng hàng     
String username = resultSet.getString("username"); // Lấy dữ liệu từ cột "username"    
System.out.println("Username: " + username); 
}
```
    
- `resultSet.next()` di chuyển con trỏ của `ResultSet` đến hàng tiếp theo, và bạn có thể truy xuất các cột của hàng đó.

### 4. **Tóm lại về vai trò của ResultSet**

-> `ResultSet` **lưu dữ liệu kết quả từ câu lệnh SQL** theo cấu trúc **hàng** và **cột**, giống như một **bảng**.




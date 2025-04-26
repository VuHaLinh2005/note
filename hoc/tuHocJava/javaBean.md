#javaBean

### 📘 **Java Bean là gì?**

- 🏷️ **Java Bean là gì?** **Java Bean** là một **lớp Java đặc biệt**, tuân theo một số quy tắc chuẩn để đảm bảo rằng nó có thể được sử dụng và quản lý dễ dàng bởi các framework và công cụ Java (như Spring, Hibernate). Java Bean chủ yếu được sử dụng để **lưu trữ và quản lý dữ liệu** trong các ứng dụng Java.
    
- 🔗 **Tại sao Java Bean quan trọng?** Java Bean giúp các ứng dụng Java dễ dàng **lưu trữ, truyền tải và quản lý dữ liệu** thông qua việc tuân theo một chuẩn nhất định. Điều này giúp tăng tính tái sử dụng và khả năng tương tác của mã, đặc biệt khi làm việc với các framework Java, nơi mà sự tuân thủ Java Bean giúp dễ dàng cấu hình và quản lý đối tượng.
    

### ✨ **Các Đặc Điểm Chính của Java Bean**

Để một lớp Java trở thành Java Bean, nó phải tuân theo các tiêu chuẩn sau:

1. **Có một constructor không tham số**: Cho phép các framework khởi tạo lớp một cách dễ dàng mà không cần tham số.
2. **Có các thuộc tính riêng tư (private) với getter và setter**: Đảm bảo tính đóng gói và giúp kiểm soát truy cập vào các thuộc tính thông qua các phương thức getter và setter.
3. Tuân thủ Java [[Serialization]]: Đảm bảo rằng Java Bean có thể được tuần tự hóa (serialize) để lưu trữ hoặc truyền tải dễ dàng. Điều này hữu ích khi đối tượng cần được gửi qua mạng hoặc lưu trong tệp.




	
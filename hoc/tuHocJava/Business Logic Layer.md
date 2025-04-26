
## Business Logic Layer ??



Lớp Business Logic Layer (BLL), hay còn gọi là Service Layer, là trái tim của ứng dụng, nơi chứa tất cả các **quy tắc nghiệp vụ và logic xử lý dữ liệu**. Nó đóng vai trò trung gian giữa Presentation Layer (PL) và Data Access Layer (DAL), đảm bảo sự phân tách rõ ràng giữa việc xử lý dữ liệu và việc hiển thị dữ liệu.

Để hiểu rõ hơn về vai trò của BLL, hãy xem xét một ví dụ cụ thể: giả sử bạn đang xây dựng một ứng dụng web bán hàng trực tuyến.

**1. Yêu cầu từ người dùng:** Người dùng thêm một sản phẩm vào giỏ hàng.

**2. Presentation Layer:** ShoppingCartController (thuộc PL) nhận yêu cầu này. Nó không trực tiếp thao tác với cơ sở dữ liệu mà gọi đến ShoppingCartService (thuộc BLL).

**3. Business Logic Layer:** ShoppingCartService thực hiện các bước sau:

- **Kiểm tra tính hợp lệ:** Kiểm tra xem sản phẩm có còn hàng hay không, số lượng đặt mua có vượt quá giới hạn hay không. Đây là các **quy tắc nghiệp vụ (business rules)**.
    
- **Tính toán:** Tính toán tổng giá trị giỏ hàng, áp dụng mã giảm giá (nếu có). Đây là **logic xử lý dữ liệu**.
    
- **Gọi Data Access Layer:** ShoppingCartService gọi ProductRepository (thuộc DAL) để lấy thông tin sản phẩm và OrderRepository để cập nhật giỏ hàng trong cơ sở dữ liệu.
    

**4. Data Access Layer:** ProductRepository và OrderRepository tương tác với cơ sở dữ liệu để thực hiện các thao tác CRUD.

**5. Trả về kết quả:** ShoppingCartService trả kết quả về cho ShoppingCartController.

**6. Hiển thị kết quả:** ShoppingCartController hiển thị kết quả cho người dùng.

**@Service annotation:**

Trong Spring Boot, annotation @Service được sử dụng để đánh dấu một class là một Service class, tức là thuộc BLL. Việc sử dụng annotation này giúp Spring Boot tự động quản lý và inject (tiêm) các Service beans vào các thành phần khác, ví dụ như Controller.

**Tóm lại:**

BLL đóng vai trò quan trọng trong việc:

- **Đóng gói logic nghiệp vụ:** Tất cả các quy tắc và logic xử lý dữ liệu được tập trung tại một nơi, giúp code dễ hiểu, dễ bảo trì và dễ kiểm thử.
    
- **Phân tách mối quan tâm:** Tách biệt việc xử lý dữ liệu khỏi việc hiển thị dữ liệu và việc truy cập cơ sở dữ liệu, giúp tăng tính module hóa và linh hoạt của ứng dụng.
    
- **Tái sử dụng logic:** Logic nghiệp vụ có thể được tái sử dụng ở nhiều nơi trong ứng dụng.
    

Việc sử dụng BLL đúng cách giúp ứng dụng trở nên rõ ràng, dễ quản lý, và dễ dàng mở rộng trong tương lai.
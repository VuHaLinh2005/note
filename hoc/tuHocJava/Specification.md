
### 1. **Specification là gì?**

- **Specification** là một giao diện (~={red}interface=~) trong Spring Data **JPA**, được dùng để **định nghĩa**(**~={red}mô tả**=~)   **tiêu chí** hay điều kiện cho truy vấn một cách linh động và có thể ~={red}**kết hợp=~** được.
- Nó giúp tách riêng logic truy vấn ra khỏi repository, tạo điều kiện cho việc tái sử dụng và kết hợp các tiêu chí ~={red}**(~={red}criteria=~)=~** truy vấn khác nhau .
- Khi sử dụng Specification, bạn có thể kết hợp nhiều tiêu chí (predicate) để tạo thành một truy vấn phức tạp mà ~={red}**không=~** cần phải viết câu lệnh **SQL hay JPQL phức tạp.**
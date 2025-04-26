
- **Tại sao dùng `Product_.PRICE` thay vì chỉ dùng chuỗi `"price"`?**  
    `Product_` là lớp static metamodel được tạo tự động khi bạn sử dụng JPA Static Metamodel. Việc dùng `Product_.PRICE` mang lại những lợi ích sau:
    
    1. **Type-safety:** Giúp đảm bảo rằng thuộc tính `price` tồn tại trong entity `Product`. Nếu có lỗi chính tả hoặc thay ~={red}**đổi=~** tên thuộc tính, lỗi sẽ được phát hiện ngay trong quá trình biên dịch, tránh lỗi runtime.
    2. **Hỗ trợ ~={red}refactoring=~:** Khi **~={red}đổi=~** tên thuộc tính trong entity, việc sử dụng metamodel sẽ giúp IDE phát hiện và thông báo lỗi biên dịch, từ đó dễ dàng cập nhật lại code. Còn nếu dùng chuỗi, lỗi đổi tên sẽ không được cảnh báo cho đến khi chạy ứng dụng.

Tóm lại, sử dụng `Product_.PRICE` giúp code an toàn hơn, dễ bảo trì và giảm thiểu lỗi so với cách truyền chuỗi tên thuộc tính thông thường.


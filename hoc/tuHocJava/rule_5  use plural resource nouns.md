

Quy tắc "**Sử dụng danh từ số nhiều** cho tài nguyên (Use plural resource nouns)" trong thiết kế RESTful API có mục đích làm cho API nhất quán, dễ đọc và rõ ràng. Dưới đây là các lý do và ví dụ chi tiết giải thích quy tắc này.

### Lý do nên sử dụng danh từ số nhiều cho tài nguyên

1. **Thể hiện rõ ràng rằng một tài nguyên là một tập hợp (collection)**:
    
    - Trong RESTful API, mỗi endpoint thường đại diện cho một tập hợp tài nguyên. Sử dụng danh từ số nhiều cho các URI giúp người dùng API hiểu rõ rằng endpoint đó đang làm việc với **một tập hợp các đối tượng.**
    - Ví dụ: `/books` có nghĩa là bạn đang làm việc với tập hợp các cuốn sách, trong khi `/book` có thể gây hiểu lầm là một cuốn sách cụ thể.
2. **Đồng nhất và nhất quán**:
    
    - Sử dụng số nhiều giúp duy trì sự nhất quán trong API, bất kể bạn làm việc với một tập hợp hay một đối tượng đơn lẻ. Việc này giúp người dùng dễ nhớ và đoán trước các endpoint.
    - Ví dụ:
        - `GET /books` - Truy vấn danh sách các cuốn sách (tập hợp).
        - `GET /books/{id}` - Truy vấn thông tin một cuốn sách cụ thể từ tập hợp đó.
3. **Tránh nhầm lẫn**:
    
    - Số ít có thể khiến người dùng nhầm lẫn giữa endpoint đại diện cho một tập hợp và endpoint cho một đối tượng đơn lẻ. Sử dụng số nhiều rõ ràng rằng endpoint đó liên quan đến cả tập hợp tài nguyên.
    - Ví dụ: `/users/` rõ ràng là endpoint cho tập hợp người dùng, trong khi `/user/` có thể dễ gây nhầm lẫn và không tuân theo chuẩn RESTful.

### Ví dụ về cách sử dụng danh từ số nhiều trong thiết kế API

Giả sử bạn đang thiết kế một API cho hệ thống thư viện, nơi bạn cần các endpoint để làm việc với các thực thể như sách, tác giả, và người dùng.

- **Tài nguyên "books"**:
    
    - `GET /books`: Lấy danh sách các sách.
    - `POST /books`: Thêm một cuốn sách mới. (thêm 1 cuốn vào 1 tập hợp cuốn sách)
    - `GET /books/{id}`: Lấy thông tin của một cuốn sách cụ thể.
    - `PUT /books/{id}`: Cập nhật thông tin của một cuốn sách cụ thể.
    - `DELETE /books/{id}`: Xóa một cuốn sách cụ thể.
- **Tài nguyên "authors"**:
    
    - `GET /authors`: Lấy danh sách các tác giả.
    - `POST /authors`: Thêm một tác giả mới.
    - `GET /authors/{id}`: Lấy thông tin của một tác giả cụ thể.
    - `PUT /authors/{id}`: Cập nhật thông tin của một tác giả cụ thể.
    - `DELETE /authors/{id}`: Xóa một tác giả cụ thể.
- **Tài nguyên "users"**:
    
    - `GET /users`: Lấy danh sách người dùng.
    - `POST /users`: Thêm người dùng mới.
    - `GET /users/{id}`: Lấy thông tin của một người dùng cụ thể.
    - `PUT /users/{id}`: Cập nhật thông tin của một người dùng cụ thể.
    - `DELETE /users/{id}`: Xóa một người dùng cụ thể.

### Tóm lại

Sử dụng danh từ số nhiều cho tài nguyên giúp làm rõ rằng bạn đang làm việc với tập hợp tài nguyên, tạo sự nhất quán trong API và tránh nhầm lẫn cho người dùng. Đây là một quy tắc quan trọng trong thiết kế API RESTful chuẩn.
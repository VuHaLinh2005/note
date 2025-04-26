 
### 1. Dùng danh từ trong URI
- **Chuẩn**: `GET /users`  
- **Không chuẩn**: `GET /getUsers`  
- **Lý do**: URI đại diện tài nguyên, không phải hành động.

### 2. Dùng đúng phương thức HTTP
- **`GET`**: Lấy dữ liệu.  
  - Ví dụ: `GET /users/1` → `200 OK`, `{"id": 1, "name": "Nam"}`.  
- **`POST`**: Tạo mới.  
  - Ví dụ: `POST /users` + `{"name": "Lan"}` → `201 Created`, `{"id": 2, "name": "Lan"}`.  
- **`PUT`**: Cập nhật toàn bộ.  
  - Ví dụ: `PUT /users/1` + `{"name": "Nam Updated"}` → `200 OK`.  
- **`DELETE`**: Xóa.  
  - Ví dụ: `DELETE /users/1` → `204 No Content`.  
- **Lý do**: Mỗi phương thức có ý nghĩa riêng, dễ đoán.

### 3. Dùng số nhiều cho tài nguyên
- **Chuẩn**: `/users`  
- **Không chuẩn**: `/user`  
- **Lý do**: Đại diện **tập hợp.**

### 4. Không lồng tài nguyên
- **Thực thể chính**: Tài nguyên độc lập, không phụ thuộc tài nguyên khác trong URI.  
- **Chuẩn**: `GET /orders?userId=1`  
  - Ý nghĩa: Lấy danh sách đơn hàng, lọc theo userId.  
- **Không chuẩn**: `GET /users/1/orders`  
  - Ý nghĩa: **Lồng** đơn hàng trong người dùng, làm URI phức tạp.  
- **Lý do**: URI chỉ nên tập trung vào một thực thể chính (ở đây là `orders`), quan hệ (như `userId`) đưa vào query để linh hoạt và rõ ràng.

### 5. Dùng query để lọc, sắp xếp, phân trang
- Ví dụ: `GET /users?role=admin&sort=age`, `/orders?limit=10&page=2`.  
- **Lý do**: Đơn giản hóa URI.

### 6. Trả mã trạng thái HTTP phù hợp
- **`200 OK`**: Thành công, có dữ liệu.  
  - Postman: `Status: 200 OK`, Body: `{"id": 1, "name": "Nam"}`.  
- **`201 Created`**: Tạo mới thành công.  
  - Postman: `Status: 201 Created`, Body: `{"id": 2, "name": "Lan"}`.  
- **`204 No Content`**: Xóa thành công, không dữ liệu.  
  - Postman: `Status: 204 No Content`, Body: trống.  
- **`404 Not Found`**: Không tìm thấy.  
  - Postman: `Status: 404 Not Found`, Body: `{"status": 404, "error": "Not Found", "message": "User not found"}`.  
- **`400 Bad Request`**: Yêu cầu sai.  
  - Postman: `Status: 400 Bad Request`, Body: `{"status": 400, "error": "Bad Request", "message": "Name is required"}`.  
- **Lý do**: Trả kết quả rõ ràng, đúng chuẩn HTTP để client (như Postman) dễ xử lý.

### 7. Dùng JSON làm định dạng chính
- Ví dụ: `{"id": 1, "name": "Nam"}` với `Content-Type: application/json`.  
- **Lý do**: Chuẩn hóa, dễ dùng.

### 8. Tránh phiên bản trong URI
- **Chuẩn**: `/users` + header versioning.  
- **Không chuẩn**: `/v1/users`.  
- **Lý do**: URI sạch.

### 9. Trả lỗi rõ ràng
- Ví dụ: `400` → `{"status": 400, "error": "Bad Request", "message": "Name required"}`.  
- **Lý do**: Dễ sửa lỗi.

### 10. Đảm bảo tính idempotent
- **Ý nghĩa**: Gọi lặp lại `PUT` hoặc `DELETE` không thay đổi kết quả sau lần đầu.  
- **Ví dụ**:  
  - `PUT /users/1` + `{"name": "Nam Updated"}` → Gọi 1 lần hay 10 lần, kết quả vẫn là `{"name": "Nam Updated"}`.  
  - `DELETE /users/1` → Gọi 1 lần xóa user, gọi thêm lần nữa không thay đổi gì (vẫn xóa).  
- **Mục đích**: Đảm bảo API ổn định, tránh thay đổi ngoài ý muốn khi lặp lại yêu cầu.
 
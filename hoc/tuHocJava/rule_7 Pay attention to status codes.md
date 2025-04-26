


Quy tắc "Pay attention to status codes" (Chú ý đến mã trạng thái) nhấn mạnh tầm quan trọng của việc sử dụng chính xác các mã trạng thái HTTP trong phản hồi từ API của bạn. Mỗi mã trạng thái mang một ý nghĩa cụ thể về kết quả của yêu cầu, và việc sử dụng đúng mã trạng thái là rất quan trọng để client có thể hiểu và xử lý kết quả một cách chính xác.

**Một số nhóm mã trạng thái HTTP phổ biến:**

- **2xx (Success):** Yêu cầu đã thành công. Ví dụ: 200 OK, 201 Created.
    
- **3xx (Redirection):** Client cần thực hiện thêm hành động để hoàn thành yêu cầu. Ví dụ: 301 Moved Permanently, 302 Found.
    
- **4xx (Client Error):** Lỗi do phía client gây ra, ví dụ như dữ liệu đầu vào không hợp lệ hoặc không có quyền truy cập. Ví dụ: 400 Bad Request, 401 Unauthorized, 404 Not Found.
    
- **5xx (Server Error):** Lỗi do phía server gây ra. Ví dụ: 500 Internal Server Error, 503 Service Unavailable.
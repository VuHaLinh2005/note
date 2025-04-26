Quy tắc "Use status codes consistently" (Sử dụng mã trạng thái nhất quán) đề cập đến việc sử dụng các mã trạng thái HTTP một cách thống nhất và có ý nghĩa trong API của bạn. Điều này có nghĩa là:

- **Luôn trả về mã trạng thái phù hợp với kết quả của thao tác:** Ví dụ, trả về 200 OK cho yêu cầu thành công, 404 Not Found khi tài nguyên không tồn tại, và 500 Internal Server Error khi có lỗi server.
    
- **Không sử dụng các mã trạng thái tùy ý hoặc không chính xác:** Ví dụ, không trả về 200 OK khi có lỗi xảy ra hoặc sử dụng 500 Internal Server Error cho tất cả các loại lỗi.
    
- **Duy trì tính nhất quán trong toàn bộ API:** Sử dụng cùng một mã trạng thái cho cùng một loại kết quả trong tất cả các endpoint của API. Ví dụ, nếu bạn sử dụng 400 Bad Request cho dữ liệu đầu vào không hợp lệ ở một endpoint, hãy sử dụng 400 Bad Request cho trường hợp tương tự ở các endpoint khác.
    

**Tại sao phải sử dụng mã trạng thái nhất quán?**

- **Dễ dàng tích hợp:** Client có thể dễ dàng hiểu và xử lý response từ API của bạn.
    
- **Gỡ lỗi đơn giản hơn:** Mã trạng thái giúp xác định nhanh chóng nguyên nhân gây ra lỗi.
    
- **Cải thiện trải nghiệm người dùng:** Client có thể hiển thị thông báo lỗi phù hợp cho người dùng dựa trên mã trạng thái.
    
- **Tăng cường bảo mật:** Sử dụng mã trạng thái chính xác có thể giúp ngăn chặn các lỗ hổng bảo mật.
    
- **Tối ưu hóa SEO:** Công cụ tìm kiếm sử dụng mã trạng thái để hiểu trạng thái của trang web.
    

**Ví dụ về việc không tuân thủ quy tắc:**

- Trả về 200 OK ngay cả khi có lỗi xảy ra.
    
- Sử dụng 500 Internal Server Error cho tất cả các loại lỗi, kể cả lỗi do client.
    
- Trả về 204 No Content khi thực sự có dữ liệu được trả về.
    

**Ví dụ về việc tuân thủ quy tắc:**

- Trả về 201 Created khi tạo tài nguyên thành công.
    
- Trả về 400 Bad Request khi dữ liệu đầu vào không hợp lệ.
    
- Trả về 404 Not Found khi tài nguyên không tồn tại.
    
- Trả về 500 Internal Server Error khi có lỗi server.
    

Tóm lại, việc sử dụng mã trạng thái HTTP nhất quán là một phần quan trọng của việc thiết kế API tốt. Nó giúp tăng tính rõ ràng, khả năng bảo trì và khả năng tích hợp của API.
#anotation

🏷️ **Annotation là siêu dữ liệu, không phải là hàm** Annotation không thực hiện hành động hay logic nào trực tiếp, mà chỉ là **siêu dữ liệu** cung cấp thông tin cho các công cụ như Spring Boot biết phải làm gì khi gặp annotation này. Cách nó hoạt động giống như một “hướng dẫn” cho framework.

Đúng vậy, về cơ bản, các annotation như `@RequestBody`, `@RequestMapping`, v.v., **được xử lý trước khi thực thi phương thức**. Tuy nhiên, điều này không có nghĩa là các annotation "chạy" theo nghĩa thực thi mã. Thay vào đó, Spring sử dụng cơ chế **Reflection** để "đọc" các annotation trong quá trình **khởi động ứng dụng** và g**hi nhận thông tin về các phương thức và tham số có annotation để thiết lập cách xử lý cho từng endpoint.**

### Quy trình chi tiết về cách Spring xử lý các annotation

1. **Quá trình khởi động ứng dụng (Application Startup)**:
    
    - Khi ứng dụng Spring Boot khởi động, Spring sẽ quét tất cả các lớp (class) và phương thức trong các package đã được đánh dấu cho việc quét (thông thường là các package con của `@SpringBootApplication`).
    - Spring tìm các annotation như `@Controller`, `@RequestMapping`, `@RequestBody`, `@PathVariable`, v.v., và ghi nhận thông tin của các phương thức được đánh dấu bởi các annotation này. Các thông tin này bao gồm:
        - Đường dẫn của endpoint (URL) từ `@RequestMapping`.
        - HTTP method (GET, POST, v.v.).
        - Kiểu dữ liệu và các yêu cầu đặc biệt trên tham số (như `@RequestBody` cho body, `@RequestParam` cho query params).
2. **Xây dựng cấu trúc xử lý**:
    
    - Sau khi thu thập thông tin từ các annotation, Spring sẽ thiết lập một **cấu trúc ánh xạ** giữa các endpoint và phương thức xử lý của chúng. Ví dụ, khi Spring phát hiện một phương thức có `@RequestMapping(value="/api/building/", method=RequestMethod.POST)`, nó sẽ ghi nhận rằng URL `/api/building/` với phương thức HTTP POST sẽ được xử lý bởi phương thức này.
3. **Khi có một Request Thực Sự**:
    
    - Khi một yêu cầu HTTP đến, Spring dựa vào cấu trúc ánh xạ đã thiết lập để xác định phương thức xử lý tương ứng.
    - Nếu phương thức có annotation `@RequestBody` trên một tham số, Spring sẽ sử dụng `Reflection` để xác định kiểu dữ liệu của tham số (trong ví dụ của bạn là `Map<String, String>`).
    - Dựa vào kiểu dữ liệu này, Spring sẽ chọn một `HttpMessageConverter` thích hợp (thường là `MappingJackson2HttpMessageConverter` cho JSON) để chuyển đổi body của yêu cầu thành kiểu `Map<String, String>`.
4. **Thực thi phương thức**:
    
    - Sau khi hoàn tất việc chuyển đổi dữ liệu và truyền tham số vào phương thức, Spring thực thi phương thức xử lý, và kết quả của phương thức được trả về dưới dạng HTTP response.

### Tóm lại

Các annotation như `@RequestBody` thực tế **không chạy** trước, nhưng chúng được **phân tích và xử lý trước** trong quá trình khởi động ứng dụng. Nhờ quá trình phân tích này, Spring biết cách xử lý các yêu cầu HTTP khi chúng đến, bao gồm việc chuyển đổi dữ liệu thông qua `@RequestBody`.
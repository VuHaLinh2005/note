#mapping


### ?
### Tóm tắt ngắn gọn từng bước:

1. **Người dùng nhập URL**: Trình duyệt gửi yêu cầu đến server (ví dụ `/upload`).
2. **Server nhận yêu cầu**: Server nhận yêu cầu từ trình duyệt.
3. **Tìm mapping**: Server kiểm tra mapping để biết URL `/upload` tương ứng với servlet nào.
4. **Chuyển đến servlet**: Server gọi servlet `UploadServlet` tương ứng.
5. **Servlet xử lý yêu cầu**: Servlet thực thi các lệnh trong phương thức `doPost()` hoặc `doGet()`.
6. **Servlet gửi phản hồi**: Servlet tạo phản hồi (ví dụ: thông báo file tải lên thành công).
7. **Trình duyệt nhận phản hồi**: Trình duyệt nhận kết quả và hiển thị cho người dùng.

### Kết luận:

Quá trình **mapping** về cơ bản là tìm kiếm và ánh xạ một URL từ trình duyệt tới một servlet cụ thể trên server để xử lý yêu cầu, và sau đó gửi phản hồi lại cho người dùng. Nếu thiếu mapping hoặc mapping không chính xác, server sẽ không thể xử lý đúng yêu cầu từ URL, dẫn đến lỗi.


### Lý do thực sự của lỗi:

Lỗi xảy ra **không phải** vì Tomcat không thể **mapping** yêu cầu người dùng tới servlet khi người dùng nhập sai URL (điều này thường dẫn đến lỗi 404). Mà lỗi này thực chất xảy ra trong **quá trình deploy** ứng dụng, **trước khi người dùng truy cập** vào ứng dụng.

### Cụ thể hơn:

-  **chi tiết lỗi java.lang.IllegalArgumentException: Invalid <url-pattern> [UploadServlet] in servlet mapping**
** Tomcat phát hiện rằng `url-pattern` `"UploadServlet"` không hợp lệ và ném ra ngoại lệ này, dẫn đến việc ứng dụng không thể khởi động.**

- **Lỗi do định dạng `url-pattern` trong `@WebServlet` không hợp lệ**. Cụ thể, Servlet API yêu cầu rằng **`url-pattern` phải bắt đầu bằng dấu `/`**.
- Khi bạn khai báo `@WebServlet` mà thiếu dấu `/` trong `url-pattern`, Tomcat không thể xử lý được cấu hình này vì **`url-pattern` sai định dạng**.
- **Kết quả là lỗi xảy ra ngay khi Tomcat cố gắng deploy ứng dụng**, dẫn đến việc ứng dụng không thể khởi động được. Bạn sẽ thấy thông báo lỗi về `Invalid <url-pattern> "UploadServlet"`, và điều này ngăn không cho toàn bộ ứng dụng được triển khai.

### Vì sao lỗi xảy ra khi deploy (không phải do người dùng nhập sai URL):

- Lỗi này liên quan đến **cấu hình ứng dụng sai** (trong trường hợp này là `url-pattern` thiếu dấu `/`), không liên quan đến người dùng nhập URL sai.
- Khi Tomcat khởi động ứng dụng, nó phải đọc và phân tích các cấu hình servlet, bao gồm `url-pattern`. Nếu cấu hình không hợp lệ (ví dụ thiếu dấu `/`), Tomcat không thể deploy ứng dụng.
- Đây là lý do tại sao lỗi xảy ra khi **deploy ứng dụng** (chứ không phải khi người dùng truy cập URL). Do đó, ứng dụng không thể được triển khai.

### Quá trình lỗi xảy ra:

1. **Tomcat khởi động** và cố gắng deploy ứng dụng của bạn.
2. Trong quá trình deploy, Tomcat đọc cấu hình của các servlet, bao gồm `@WebServlet` annotations.
3. Khi Tomcat gặp `url-pattern` không hợp lệ (ví dụ thiếu dấu `/`), nó phát hiện rằng cấu hình không đúng theo chuẩn Servlet API.
4. Tomcat ném ra ngoại lệ (Exception) và **ngừng quá trình deploy**. Đây là lý do ứng dụng không thể chạy.
5. **Lỗi không phải do người dùng nhập sai URL**, mà là **do ứng dụng không được triển khai thành công** vì cấu hình sai.

### Tại sao không phải lỗi 404:

- **Lỗi 404** thường xảy ra khi ứng dụng đã được triển khai thành công, nhưng người dùng nhập **URL không đúng** hoặc **không có mapping** nào tương ứng với URL đó.
- Tuy nhiên, trong trường hợp này, ứng dụng **không thể deploy** ngay từ đầu, nên **người dùng không thể truy cập** vào ứng dụng được. Điều này dẫn đến lỗi deploy thay vì lỗi 404.

### Tóm lại:

- Lỗi này xảy ra do **định dạng `url-pattern` không hợp lệ** trong quá trình deploy ứng dụng (thiếu dấu `/`).
- **Tomcat không thể deploy ứng dụng** khi `url-pattern` không đúng chuẩn, vì vậy toàn bộ ứng dụng không thể khởi động.
- **Người dùng không nhập sai URL**, mà lỗi xảy ra ở giai đoạn deploy do cấu hình sai trong ứng dụng.

Hy vọng giải thích này đã làm rõ vấn đề!
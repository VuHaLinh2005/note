#dogetAndDopost


## ??

### 1. GET: Trình duyệt yêu cầu server cung cấp thông tin

- **GET** là **yêu cầu của trình duyệt đến server** để **lấy thông tin**.
- Khi bạn dùng GET, nghĩa là **trình duyệt** đang yêu cầu **server cung cấp một số thông tin**. Ví dụ, khi bạn nhập một URL vào trình duyệt hoặc bấm vào một đường link, trình duyệt sẽ gửi một yêu cầu GET tới server để tải trang web hoặc tài nguyên mà bạn yêu cầu.
- Cụ thể hơn:
    - Trình duyệt gửi yêu cầu lên server.
    - Server nhận yêu cầu và **lấy thông tin** (ví dụ: HTML của trang web, ảnh, dữ liệu từ cơ sở dữ liệu).
    - Server gửi lại thông tin đó về trình duyệt.
- **GET** thường dùng để:
    - Lấy nội dung trang web (ví dụ: hiển thị danh sách sinh viên).
    - Không thay đổi gì trong server (không thêm, xóa, sửa dữ liệu).

Ví dụ: Khi bạn truy cập `https://example.com/students`, yêu cầu này dùng GET, và server sẽ cung cấp trang chứa danh sách các sinh viên về cho trình duyệt để hiển thị.

### 2. POST: Trình duyệt gửi thông tin lên server để yêu cầu xử lý

- **POST** là **yêu cầu của trình duyệt đến server để gửi dữ liệu** và yêu cầu server **xử lý** dữ liệu đó.
- Khi bạn dùng POST, nghĩa là **trình duyệt** đang gửi một số **dữ liệu mới lên server** để server **xử lý**. Ví dụ: thêm một sinh viên mới vào hệ thống, cập nhật thông tin sinh viên, hoặc gửi một form đăng ký.
- Cụ thể hơn:
    - Trình duyệt gửi dữ liệu từ form (ví dụ: tên, email, số điện thoại) lên server.
    - Server nhận dữ liệu và **xử lý**, ví dụ: thêm dữ liệu đó vào cơ sở dữ liệu hoặc thực hiện thao tác khác.
    - Sau khi xử lý, server thường trả về một trang thông báo thành công hoặc chuyển hướng tới một trang khác.
- **POST** thường dùng khi:
    - Bạn cần **thêm, sửa, hoặc xóa** dữ liệu trên server.
    - Dữ liệu lớn hoặc nhạy cảm cần phải gửi qua **body** (ví dụ: mật khẩu, thông tin cá nhân).

Ví dụ: Khi bạn điền vào form cập nhật thông tin sinh viên và nhấn nút "Save", trình duyệt sẽ gửi yêu cầu POST đến server với các thông tin mới của sinh viên đó.
### Tóm tắt sự khác biệt giữa GET và POST:

- **GET**: Trình duyệt **yêu cầu server cung cấp thông tin**.
    
    - Ví dụ: Trình duyệt yêu cầu hiển thị danh sách sinh viên.
    - Dữ liệu yêu cầu được gửi kèm trong **URL** (ví dụ `?id=1`).
    - **Không thay đổi** gì trong server, chỉ lấy dữ liệu để hiển thị.
- **POST**: Trình duyệt **gửi dữ liệu lên server để server xử lý**.
    
    - Ví dụ: Trình duyệt gửi thông tin sinh viên mới để thêm vào hệ thống.
    - Dữ liệu gửi qua **body của request** (không hiện trên URL).
    - **Thay đổi** dữ liệu trên server (ví dụ: thêm mới, sửa, xóa).

Nói cách khác, bạn có thể tưởng tượng **GET** như bạn yêu cầu một món ăn từ thực đơn của nhà hàng (server sẽ mang nó ra cho bạn mà không thay đổi gì cả), còn **POST** giống như bạn đưa cho nhà hàng nguyên liệu để yêu cầu họ nấu một món mới cho bạn (server phải xử lý những nguyên liệu đó và tạo ra món ăn mới).
### Quá trình Trả Về Thông Tin Trong Servlet Với Yêu Cầu GET

1. **Trình duyệt gửi yêu cầu GET tới server**:
    
    - Khi bạn nhập một URL hoặc nhấn vào một liên kết, trình duyệt sẽ gửi yêu cầu GET tới server để yêu cầu một tài nguyên, ví dụ như một trang HTML hoặc một file hình ảnh.
2. **Server nhận yêu cầu và gọi `doGet()` của servlet**:
    
    - Khi yêu cầu GET tới server, nếu yêu cầu đó được ánh xạ đến servlet, server sẽ gọi phương thức `doGet(HttpServletRequest request, HttpServletResponse response)` của servlet để xử lý.
3. **Servlet chuẩn bị phản hồi**:
    
    - Trong phương thức `doGet()`, servlet sẽ chuẩn bị nội dung cần gửi về cho trình duyệt.
    - Dữ liệu mà bạn muốn gửi về cho trình duyệt sẽ được tạo ra trong **phần thân của `response`**. Thông tin này có thể là nội dung HTML, dữ liệu JSON, hoặc bất kỳ loại dữ liệu nào khác.
4. **Sử dụng đối tượng `response` để trả về thông tin**:
    
    - Để gửi dữ liệu về cho trình duyệt, servlet sẽ sử dụng đối tượng **`HttpServletResponse`**, thường qua các phương pháp như:
        - **`response.getWriter().write("HTML content here");`**: Viết nội dung trực tiếp vào body của `response`.
        - **`response.sendRedirect("url");`**: Chuyển hướng trình duyệt đến một URL khác.
        - **`RequestDispatcher.forward(request, response);`**: Chuyển tiếp yêu cầu tới một trang JSP để tạo ra nội dung HTML.
5. **Trình duyệt nhận phản hồi và hiển thị**:
    
    - Sau khi server gửi lại phản hồi qua đối tượng `response`, trình duyệt sẽ nhận được thông tin này và **hiển thị nội dung** cho người dùng.

### Chi Tiết Về `request` và `response`

- **`request`**: Đối tượng `request` chứa thông tin của yêu cầu từ phía trình duyệt, chẳng hạn như các tham số URL, header, hoặc thông tin về client. Trong phương thức `doGet()`, `request` được sử dụng chủ yếu để **đọc dữ liệu từ client**, không phải để gửi dữ liệu về.
    
- **`response`**: Đối tượng `response` được sử dụng để **gửi dữ liệu từ server về phía client**. Đây là phương tiện chính mà servlet sử dụng để phản hồi lại yêu cầu từ trình duyệt. Nội dung `response` bao gồm:
    
    - **Header**: Các thông tin như mã trạng thái (200 OK, 404 Not Found, v.v.), loại nội dung (`text/html`, `application/json`, v.v.).
    - **Body**: Nội dung thực tế cần gửi về (HTML, JSON, v.v.).
# Hiểu về Phần Body của HTTP Request

Để hiểu rõ hơn về phần body của HTTP request, chúng ta có thể so sánh giữa hai phương thức GET và POST.

## 1. HTTP Request

Khi trình duyệt gửi yêu cầu đến server, yêu cầu đó bao gồm nhiều phần, trong đó có hai phần chính: **header** và **body**.

- **Header**: Chứa thông tin về yêu cầu, chẳng hạn như phương thức (GET, POST), địa chỉ URL, loại trình duyệt, và các thông tin khác.
- **Body**: Là phần dữ liệu thực tế mà bạn muốn gửi đến server. Chỉ có trong các phương thức như POST, PUT, hoặc PATCH.

## 2. So sánh GET và POST

- **GET**:
  - Dữ liệu được gửi qua URL.
  - Ví dụ: 
    ```
    GET /students/insert?id=123&name=Linh&email=linh@gmail.com&phone=12345678 HTTP/1.1
    Host: localhost:8080
    ```
  - Tất cả dữ liệu được hiển thị trong URL, dễ nhìn thấy nhưng có giới hạn về kích thước.

- **POST**:
  - Dữ liệu được gửi trong phần body của yêu cầu.
  - Ví dụ:
    ```
    POST /students/insert HTTP/1.1
    Host: localhost:8080
    Content-Type: application/x-www-form-urlencoded

    id=123&name=Linh&email=linh@gmail.com&phone=12345678
    ```
  - Dữ liệu không xuất hiện trong URL mà nằm trong body, cho phép gửi dữ liệu lớn hơn và bảo mật hơn.

## 3. Tại sao lại dùng body?

- **Bảo mật**: Dữ liệu không hiển thị trong URL, nên không dễ bị lộ ra.
- **Kích thước lớn**: Bạn có thể gửi nhiều dữ liệu mà không bị giới hạn như khi dùng GET.
- **Phân loại dữ liệu**: Body có thể chứa các loại dữ liệu khác nhau (như JSON, XML) tùy thuộc vào `Content-Type`.

## 4. Hình dung đơn giản

- **GET** giống như bạn gửi một bức thư và viết tất cả thông tin trên phong bì.
- **POST** giống như bạn viết một bức thư bên trong phong bì và gửi nó, không ai nhìn thấy nội dung cho đến khi mở phong bì.

Hy vọng những giải thích này giúp bạn hiểu rõ hơn về phần body của HTTP request! Nếu bạn còn câu hỏi nào khác, cứ hỏi nhé!

note : chỉ có hai thứ
- yêu cầu (có dữ liệu ,mục đích) : GET,POST.
- server phản hồi (trả về) .
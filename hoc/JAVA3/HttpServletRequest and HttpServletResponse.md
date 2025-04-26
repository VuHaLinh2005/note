#HttpServletRequestandHttpServletResponse


## `HttpServletRequest` và `HttpServletResponse` là gì, hoạt động ra sao?

### `HttpServletRequest`
`HttpServletRequest` là một interface trong gói `javax.servlet.http`, cung cấp các phương thức để lấy dữ liệu từ client gửi lên server thông qua các yêu cầu HTTP (request). Nó chứa thông tin về các tham số, URL, headers, phương thức HTTP (GET, POST, v.v.), và các thuộc tính liên quan đến yêu cầu của người dùng.

**Một số phương thức chính của `HttpServletRequest`:**
- `getParameter(String name)`: Lấy giá trị của một tham số gửi từ client lên.
- `getServletPath()`: Trả về đường dẫn của servlet.
- `getRequestURL()`: Trả về URL của yêu cầu.
- `getQueryString()`: Trả về chuỗi truy vấn trong yêu cầu.
- `getParameterMap()`: Lấy toàn bộ các tham số gửi từ client dưới dạng `Map<String, String[]>`.

### `HttpServletResponse`
`HttpServletResponse` là interface trong gói `javax.servlet.http`, cung cấp các phương thức để gửi phản hồi (response) từ server về cho client. Nó cho phép thiết lập các thuộc tính của phản hồi như: mã trạng thái HTTP, loại nội dung, và các headers.

**Một số phương thức chính của `HttpServletResponse`:**
- `setContentType(String type)`: Đặt loại nội dung (MIME type) của phản hồi, ví dụ: `text/html`.
- `getWriter()`: Lấy đối tượng `PrintWriter` để ghi dữ liệu trả về cho client.
- `sendRedirect(String location)`: Chuyển hướng đến một URL khác.

### Ví dụ trong code của bạn

#### `HttpServletRequest`:
Trong phương thức `doGet`, bạn sử dụng `HttpServletRequest` để lấy dữ liệu từ yêu cầu HTTP:


```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String path = request.getServletPath(); // Lấy đường dẫn của servlet
    System.out.println(path);

    switch (path) {
        case "/students":
            listStudents(request, response); // Xử lý hiển thị danh sách sinh viên
            break;

        case "/students/new":
            insertStudent(request, response); // Xử lý thêm sinh viên mới
            break;

        case "/students/delete":
            deleteStudent(request, response); // Xử lý xóa sinh viên
    }
}
```




## Request

Trong kiến trúc của Java web ứng dụng (mô hình JSP và Servlet), `request` là một đối tượng thuộc về cả hai, nhưng ở các thời điểm khác nhau. Cụ thể:

- **JSP (JavaServer Pages)**: JSP thường được dùng như giao diện người dùng (UI) để gửi yêu cầu từ client (người dùng hoặc trình duyệt). Khi người dùng thực hiện một hành động trên trang web (ví dụ, nhấn nút gửi form), yêu cầu HTTP (HTTP request) sẽ được tạo ra từ phía client và gửi đến một Servlet cụ thể. Trong quá trình này, đối tượng `request` chưa thuộc về JSP mà chỉ là phương tiện để truyền dữ liệu từ JSP đến Servlet.

- **Servlet**: Khi yêu cầu được gửi đến Servlet, đối tượng `request` chính thức thuộc về Servlet. Servlet sẽ nhận `HttpServletRequest` (được gọi là `request` trong đoạn code của bạn) và sử dụng nó để xử lý yêu cầu, truy xuất các tham số yêu cầu từ client, rồi thực hiện các tác vụ như thêm, sửa, xóa dữ liệu.

Vì vậy, trong code của bạn, đối tượng `request` thuộc về **Servlet**, khi nó đến và được xử lý bởi các phương thức như `doGet` hoặc `doPost`.

## Response

Cũng giống như `request`, đối tượng `response` trong mô hình Servlet - JSP thuộc về phần **Servlet**. Để giải thích rõ hơn:

- **JSP gửi yêu cầu (Request)**: Khi người dùng trên trang JSP thực hiện một hành động (như nhấn nút hoặc gửi form), một yêu cầu HTTP (`request`) được gửi đến Servlet. Servlet xử lý yêu cầu này, và sau đó chuẩn bị một phản hồi (`response`).

- **Servlet xử lý và tạo phản hồi (Response)**: Đối tượng `HttpServletResponse` (được gọi là `response` trong code của bạn) được Servlet sử dụng để gửi phản hồi về lại cho client hoặc trang JSP. Servlet có thể sử dụng đối tượng này để:
   - Gửi dữ liệu dưới dạng HTML, JSON, hoặc các định dạng khác.
   - Điều hướng (redirect) người dùng sang một trang khác.
   - Gửi mã trạng thái HTTP (như 404, 500, 200) để thông báo kết quả của quá trình xử lý.

Trong đoạn code của bạn, đối tượng `response` được dùng trong các phương thức như `listStudents`, `insertStudent`, và `deleteStudent`. Đây là cách Servlet trả lại kết quả cho client, thường là chuyển tiếp (forward) đến một trang JSP khác hoặc trả về một trang HTML động.

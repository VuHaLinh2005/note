#sendRedirectAndGetRequestDispatcher


# Sự khác biệt giữa `request.getRequestDispatcher()` và `response.sendRedirect()`

Sự khác biệt giữa `request.getRequestDispatcher()` và `response.sendRedirect()` nằm ở cách mà chúng xử lý yêu cầu và phản hồi HTTP. Điều này có thể giải thích tại sao trong trường hợp của bạn, `request.getRequestDispatcher()` không gửi dữ liệu sang trang JSP, trong khi `response.sendRedirect()` lại có.

## 1. `request.getRequestDispatcher()`

- Khi bạn sử dụng `request.getRequestDispatcher()`, nó sẽ **forward** yêu cầu từ servlet tới trang JSP mà không tạo ra một yêu cầu mới.
- **Quan trọng**: Forward không làm mất dữ liệu trong đối tượng `request`. Tuy nhiên, nếu không có dữ liệu được thêm vào `request` trước khi forward, trang JSP sẽ không hiển thị dữ liệu.
- Vì vậy, bạn cần đảm bảo rằng bạn đã đặt dữ liệu cần thiết vào trong request trước khi forward. Ví dụ:

```java
List<Student> students = studentService.getAllStudents();
request.setAttribute("students", students);
request.getRequestDispatcher("/view/studentList.jsp").forward(request, response);
```

```java

RequestDispatcher dispatcher = request.getRequestDispatcher("/view/FormEdit.jsp");
// Nếu không có lệnh forward sau đây, thì sẽ không chuyển hướng đến FormEdit.jsp
// dispatcher.forward(request, response); // Chuyển tiếp bị thiếu ở đây
```

## 2. `response.sendRedirect()`

- `sendRedirect()` sẽ gửi một phản hồi HTTP 302 cho trình duyệt, yêu cầu trình duyệt tạo một yêu cầu GET mới đến URL được chỉ định (trong trường hợp này là `/view/studentList.jsp`).
- Điều này sẽ tạo ra một vòng lặp phản hồi-yêu cầu mới, vì vậy nếu bạn đã đặt dữ liệu vào trong `request` trước khi sử dụng `sendRedirect()`, dữ liệu sẽ bị mất do `sendRedirect()` không duy trì dữ liệu `request`.
- Thay vào đó, nếu bạn muốn dữ liệu tồn tại qua nhiều yêu cầu, bạn phải lưu trữ nó trong `session` hoặc `application` scope. Ví dụ:




```java

List<Student> students = studentService.getAllStudents(); session.setAttribute("students", students); response.sendRedirect("/view/studentList.jsp");`
```

- Trong trường hợp này, dữ liệu được lưu vào `session`, do đó, khi trang JSP tải, nó sẽ có thể truy cập dữ liệu từ `session`.


##  hiểu rõ response.sendredirect()
### Quá trình hoạt động của `response.sendRedirect()`:

1. **Gọi `response.sendRedirect()`**: Khi phương thức `response.sendRedirect()` được gọi, máy chủ sẽ phản hồi lại với mã trạng thái HTTP **302** (Found) và một **URL mới** trong phần **"Location"** của tiêu đề phản hồi.
	```java
	HTTP/1.1 302 Found Location: /nhanVien
```
- **Trình duyệt nhận phản hồi**: Sau khi trình duyệt nhận được phản hồi này (với mã trạng thái 302 và URL trong tiêu đề "Location"), trình duyệt sẽ hiểu rằng nó cần thực hiện một **yêu cầu HTTP mới** đến URL mới được chỉ định trong tiêu đề "Location". Điều này có nghĩa là trình duyệt sẽ thực hiện một yêu cầu GET mới đến URL `/nhanVien`.
    
- **Yêu cầu mới đến máy chủ**: Sau khi trình duyệt thực hiện yêu cầu mới đến URL `/nhanVien`, máy chủ sẽ xử lý yêu cầu này như một yêu cầu HTTP hoàn toàn mới, nghĩa là tất cả dữ liệu trong request trước đó (như các thuộc tính trong `request.setAttribute()`) sẽ không còn tồn tại nữa.
### Tại sao gọi nó là **yêu cầu mới từ trình duyệt**:

Mặc dù `response.sendRedirect()` được gọi từ phía máy chủ, nhưng bản chất của quá trình **redirect** là yêu cầu trình duyệt thực hiện một yêu cầu mới đến một URL khác.

- **Với `response.sendRedirect()`**, server không gửi nội dung phản hồi ngay lập tức. Thay vào đó, server nói với trình duyệt "**hãy thực hiện một yêu cầu mới đến URL này**", và sau đó trình duyệt sẽ gửi yêu cầu mới đến URL được chỉ định.

### Ví dụ quá trình khi gọi `response.sendRedirect("/nhanVien")`:

1. **Servlet**:
    
    - Bạn gọi `response.sendRedirect("/nhanVien");` trong servlet của mình.
    - Máy chủ phản hồi với mã trạng thái **302** và gửi cho trình duyệt URL `/nhanVien`.
2. **Trình duyệt**:
    
    - Nhận phản hồi từ máy chủ.
    - Gửi một yêu cầu HTTP mới đến URL `/nhanVien`.
3. **Máy chủ**:
    
    - Nhận yêu cầu mới từ trình duyệt đến URL `/nhanVien`.
    - Servlet hoặc tài nguyên được ánh xạ với `/nhanVien` xử lý yêu cầu và trả về phản hồi cuối cùng cho trình duyệt.

### **Sự khác biệt giữa `sendRedirect()` và `forward()`**:

- **`sendRedirect()`**:
    
    - Gửi mã trạng thái **302** (redirect) về phía trình duyệt.
    - Trình duyệt thực hiện **yêu cầu HTTP mới** đến URL chỉ định trong `sendRedirect`.
    - Vì là yêu cầu mới, mọi thông tin trong `request` sẽ bị mất (trừ khi bạn lưu nó trong `session`).
- **`forward()`**:
    
    - Chuyển tiếp yêu cầu đến một Servlet hoặc JSP khác **trong cùng một yêu cầu**.
    - Không tạo yêu cầu mới, vì vậy các thông tin trong `request` (như dữ liệu được cài bằng `request.setAttribute()`) sẽ được giữ nguyên.
    - Quá trình này diễn ra **hoàn toàn trên máy chủ** và không có sự can thiệp từ trình duyệt.

### Kết luận:

Mặc dù bạn gọi phương thức `sendRedirect()` từ đối tượng `response`, nhưng bản chất của nó là một **yêu cầu mới** từ trình duyệt. Trình duyệt nhận được yêu cầu từ server và sau đó tự động gửi một yêu cầu HTTP mới đến URL đích được chỉ định. Đó là lý do tại sao `sendRedirect()` được coi là một quá trình **yêu cầu mới** từ trình duyệt, không phải là phản hồi trực tiếp từ server.

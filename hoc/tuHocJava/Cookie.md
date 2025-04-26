-- Dùng để **lưu** **trữ** dữ liệu và **request** sẽ gửi **kèm** cookie lên **server**.

Có **hai** loại cookies chính:

1. **Session Cookies:** Loại này tương tự như **session storage**, nó sẽ bị **xóa** khi bạn **đóng** trình duyệt. 

2. **Persistent Cookies:** Loại này được lưu **trữ** trên **máy** **tính** của bạn và có **thời gian** tồn tại nhất định, được xác định bởi thuộc tính `Expires` hoặc `Max-Age`.  Nó sẽ không bị mất đi khi bạn đóng trình duyệt, mà sẽ tồn tại cho đến khi hết hạn hoặc bị xóa thủ công.

**Vậy cookie được tạo ra như thế nào?**

Cookie được tạo ra bởi **server** và gửi đến **client (trình duyệt)**, thông qua HTTP header `Set-Cookie`.  Trình duyệt sẽ lưu trữ cookie và gửi nó trở lại server trong mỗi request tiếp theo (thông qua HTTP header `Cookie`) nếu cookie đó phù hợp với domain và path của request.

**Làm thế nào cookie bị mất?**

Cookie có thể bị mất theo các cách sau:

* **Đóng trình duyệt (Session Cookies):**  Như đã nói, session cookies sẽ bị xóa khi bạn đóng trình duyệt.
* **Hết hạn (Persistent Cookies):**  Khi persistent cookie hết hạn (dựa trên thuộc tính `Expires` hoặc `Max-Age`), trình duyệt sẽ tự động xóa nó.
* **Xóa thủ công:** Người dùng có thể xóa cookie thủ công trong cài đặt trình duyệt.
* **Xóa bằng JavaScript:**  JavaScript có thể xóa cookie bằng cách đặt thuộc tính `Expires` của cookie thành một ngày trong quá khứ.
* **Giới hạn số lượng:** Trình duyệt thường giới hạn số lượng cookie mà một domain có thể lưu trữ.  Khi vượt quá giới hạn, các cookie cũ hơn có thể bị xóa.

## session cookie other persistent cookie:

- Nếu bạn đặt spring.session.cookie.max-age=0, Spring Session sẽ tạo ra một **session cookie**, có nghĩa là cookie sẽ bị xóa khi **đóng** **trình duyệt**. Đây là giá trị mặc định nếu bạn không cấu hình max-age.
    
- Nếu bạn đặt spring.session.cookie.max-age thành một giá trị dương, Spring Session sẽ tạo ra một **persistent cookie**, có nghĩa là cookie sẽ tồn tại trên **máy tính** của người dùng trong khoảng thời gian được chỉ định, ngay cả khi đóng trình duyệt.
    
-  nếu **cookie mất** : thì **session id mất** (chìa khoá mở session data mất.)



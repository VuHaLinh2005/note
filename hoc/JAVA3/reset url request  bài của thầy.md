
## Edit button ?
### Vấn đề chính:

- **Khi bạn nhấn "Edit"**, request mới được gửi đi chỉ có duy nhất tham số `id`, và **các thông tin khác như `name`, `email`, `phone` không tồn tại trong request**. Nguyên nhân là do dữ liệu từ Servlet không tự động "giữ lại" trong các request mới trừ khi bạn đẩy chúng vào request của yêu cầu mới (GET hoặc POST).
    
- Khi bạn điều hướng đến `/students/edit?id=1`, Servlet không có thông tin gì về `name`, `email`, và `phone` trong request mới. Điều này xảy ra bởi vì request trước đó (khi hiển thị danh sách sinh viên) đã kết thúc và không còn dữ liệu nào được giữ lại trừ `id` được truyền trong URL.
    

### Tại sao chỉ còn lại `id`:

- Khi bạn nhấn vào liên kết "Edit", chỉ có giá trị `id` được gửi dưới dạng tham số trong query string của URL (ví dụ: `/students/edit?id=1`). Các giá trị khác (`name`, `email`, `phone`) không được gửi cùng URL, và do đó không có mặt trong request mới.
    
- Dữ liệu từ request cũ không tự động được giữ lại trong request mới (khi nhấn "Edit"), vì mỗi request HTTP là một request độc lập. Trừ khi bạn truyền lại dữ liệu sinh viên qua URL hoặc lưu trữ chúng trong phiên (session), chúng sẽ không tồn tại trong request mới.


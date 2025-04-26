
## phần thêm sp 

1. **Mục đích**: Đoạn code xử lý việc thêm sản phẩm vào giỏ hàng bằng AJAX trong hai ngữ cảnh:
    - **.btnAddToCartHomepage**: Thêm sản phẩm từ trang chủ với số lượng mặc định là 1.
    - **.btnAddToCartDetail**: Thêm sản phẩm từ trang chi tiết với số lượng do người dùng nhập.
2. **Cơ chế hoạt động**:
    - Khi người dùng nhấn nút, code kiểm tra trạng thái đăng nhập.
    - Nếu chưa đăng nhập, hiển thị thông báo lỗi.
    - Nếu đã đăng nhập, gửi yêu cầu AJAX đến server với thông tin sản phẩm (ID và số lượng).
    - Khi thành công, cập nhật giao diện (nếu có) và hiển thị thông báo.
3. **Điểm khác biệt**:
    - Phần .btnAddToCartHomepage có số lượng cố định là 1, trong khi .btnAddToCartDetail lấy số lượng từ input.
    - Phần xử lý success trong .btnAddToCartDetail chưa hoàn thiện (thiếu cập nhật giao diện hoặc thông báo).
4. **Bảo mật**: Sử dụng token CSRF để bảo vệ yêu cầu POST khỏi các cuộc tấn công CSRF.
 
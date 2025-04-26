Lý do khi lấy `id` từ `router` hoặc `route.query` nó lại là **String** là do cách mà các tham số query trong URL hoạt động. Cụ thể:

### 1. **Query Parameters luôn ở dạng String:**

URL truyền tham số thông qua query string (ví dụ: `?id=1`) và tất cả các giá trị trong query string mặc định đều là kiểu `String`. Đây là tiêu chuẩn của giao thức HTTP.

**Ví dụ:** URL: `http://localhost:3000/product?id=1`

- `id` trong query sẽ luôn là chuỗi `"1"`, bất kể bạn mong muốn nó là số.

**Lý do:** Query string chỉ là một chuỗi văn bản (`text`), không có ngữ nghĩa cụ thể về kiểu dữ liệu. Trình duyệt hoặc các công cụ xử lý query không tự động chuyển đổi kiểu.

---

---

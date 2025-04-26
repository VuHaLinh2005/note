#restController


`@RestController` là một annotation trong Spring Boot, kết hợp của `@Controller` và `@ResponseBody`. Nó được sử dụng chủ yếu trong các ứng dụng RESTful API, nơi mà dữ liệu trả về cho client thường là JSON hoặc XML thay vì một trang HTML.

### Chi tiết về `@RestController`

- **Chức năng chính**: `@RestController` đánh dấu một lớp là một REST controller, và tất cả các phương thức trong lớp này đều được mặc định gắn với `@ResponseBody`.
- **Tự động hóa**: Khi bạn sử dụng `@RestController`, bạn không cần phải thêm `@ResponseBody` vào từng phương thức trả về JSON/XML, vì nó sẽ tự động áp dụng cho tất cả các phương thức trong lớp đó.
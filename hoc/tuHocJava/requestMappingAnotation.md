	#requestMapping

🧠 **Bước tư duy để giải thích `@RequestMapping` trong Spring Boot:**

1. 📌 **Xác định `@RequestMapping` là gì:** Đây là một annotation trong Spring Boot để **ánh xạ các URL tới phương thức xử lý tương ứng.**
2. 🗂️ **Hiểu vai trò của nó:** `@RequestMapping` **giúp xác định đường dẫn URL và loại yêu cầu HTTP** (GET, POST, PUT, DELETE, v.v.).
3. 🔍 **Phân biệt với các annotation cụ thể hơn:** Tìm hiểu các annotation khác như `@GetMapping`, `@PostMapping` và cách chúng phát triển từ `@RequestMapping`.
4. 💡 **Giải thích ứng dụng thực tế:** Giải thích cách sử dụng `@RequestMapping` trong một controller với các ví dụ.

---

### 📘 **Giải thích `@RequestMapping` trong Spring Boot**

- 🏷️ **`@RequestMapping` là gì?** `@RequestMapping` là một annotation trong Spring Framework và Spring Boot, được sử dụng để ánh xạ (map) một đường dẫn URL cụ thể tới một phương thức trong controller. Điều này có nghĩa là khi có yêu cầu (request) từ phía người dùng với URL tương ứng, phương thức đã được ánh xạ sẽ được thực thi để xử lý yêu cầu đó.
    
- 🔗 **Vai trò của `@RequestMapping`** `@RequestMapping` có khả năng định nghĩa:
    
    - Đường dẫn URL (ví dụ: `/home`, `/api/products`).
    - Loại yêu cầu HTTP (HTTP method) như `GET`, `POST`, `PUT`, hoặc `DELETE`.
    - Thêm các chi tiết khác như tiêu đề, tham số, và kiểu phản hồi (response type).

🛠️ **Các annotation cụ thể hơn kế thừa từ `@RequestMapping`** Spring Boot giới thiệu các annotation cụ thể như:

- **`@GetMapping`** (dành cho các yêu cầu GET).
- **`@PostMapping`** (dành cho các yêu cầu POST).
- **`@PutMapping`** (dành cho các yêu cầu PUT).
- **`@DeleteMapping`** (dành cho các yêu cầu DELETE).


💼 **Sử dụng `@RequestMapping` cho endpoint chính** Khi cần định nghĩa các **endpoint gốc** cho một nhóm chức năng, có thể đặt `@RequestMapping` trên lớp controller. Các phương thức con sẽ tiếp tục sử dụng các đường dẫn tương đối. Ví dụ:
```java

`@RequestMapping("/api") public class ApiController {    
@GetMapping("/users")     
public List<User> getUsers() { /* logic */ }      
@PostMapping("/users")     
public User createUser(@RequestBody User user) { /* logic */ } }`
```

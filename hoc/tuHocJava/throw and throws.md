

### 🧠 **Bước 1: Khi ném exception, có cần phải xử lý luôn không?**

Khi bạn **ném một exception** (dùng `throw`), bạn phải quyết định rằng **ai sẽ xử lý** lỗi này. Đáp án là **có**, bạn phải xử lý exception, nhưng việc xử lý có thể ở trong cùng phương thức (hàm) hoặc ở phương thức khác (hoặc ở một nơi khác như một lớp xử lý toàn cục).

### 🧠 **Bước 2: Ba cách xử lý ngoại lệ (exception) khi ném ra**

1. **Xử lý ngay tại nơi ném (try-catch trong cùng phương thức)**
    
    - Nếu bạn ném exception trong một phương thức, bạn có thể xử lý nó ngay trong phương thức đó bằng cách dùng khối `try-catch`.
    - Điều này giúp kiểm soát ngay lập tức sự cố và có thể thông báo cho người dùng hoặc ghi log.

```java
public void findResource() {
    try {
        // Giả sử có một lỗi
        throw new CustomNotFoundException("Resource not found");
    } catch (CustomNotFoundException ex) {
        // Xử lý lỗi, có thể ghi log hoặc trả thông báo cho người dùng
        System.out.println("Caught exception: " + ex.getMessage());
    }
}

```

**Xử lý ở phương thức gọi (throw + throws)**

- Nếu phương thức ném exception mà không xử lý ngay, bạn có thể sử dụng `throws` trong khai báo phương thức để yêu cầu phương thức gọi (hoặc các lớp khác) xử lý exception đó.
- Khi phương thức có `throws` và ném exception, các phương thức gọi **bắt buộc phải xử lý** exception này (bằng `try-catch`) hoặc tiếp tục ném ra (nếu chúng cũng có khai báo `throws`).

```java
public void findResource() throws CustomNotFoundException {
    throw new CustomNotFoundException("Resource not found");
}

public void handleRequest() {
    try {
        findResource();
    } catch (CustomNotFoundException ex) {
        System.out.println("Caught exception in handleRequest: " + ex.getMessage());
    }
}

```

**Xử lý toàn cục (Global Exception Handling - Spring)**

- Trong các ứng dụng Spring, bạn có thể sử dụng `@ControllerAdvice` hoặc `@ExceptionHandler` để xử lý ngoại lệ trên toàn bộ ứng dụng mà không cần phải xử lý riêng lẻ trong mỗi phương thức.
- Spring sẽ tự động chuyển các exception đến các phương thức xử lý toàn cục mà bạn đã cấu hình.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(CustomNotFoundException.class)
    public ResponseEntity<String> handleCustomNotFoundException(CustomNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}

```


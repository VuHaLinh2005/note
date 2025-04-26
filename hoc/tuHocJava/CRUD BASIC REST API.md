 
### Các hàm tiện ích của `ResponseEntity`
- `ResponseEntity.ok(body)`: Trả về 200 OK với body.
- `ResponseEntity.created(uri).body(body)`: Trả về **201 Created** với **~={red}URI trong header=~** `Location`.
- `ResponseEntity.noContent().build()`: Trả về **204 No Content,** không body.
- `ResponseEntity.badRequest().body(body)`: Trả về 400 Bad Request với body.
- `ResponseEntity.status(HttpStatus).body(body)`: Dùng cho các trường hợp khác (nếu cần linh hoạt).

---
### Controller CRUD tối ưu hóa
```java
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

import java.net.URI;
import java.util.List;

@RestController
@RequestMapping("/api/products")
public class ProductController {

    @Autowired
    private ProductRepository productRepository;

    // CREATE - Thêm sản phẩm
    @PostMapping
    public ResponseEntity<Product> createProduct(@RequestBody Product product) {
        if (product.getName() == null || product.getName().isEmpty()) {
            throw new ApiException(HttpStatus.BAD_REQUEST, "Tên sản phẩm không được để trống");
        }
        if (product.getPrice() < 0) {
            throw new ApiException(HttpStatus.BAD_REQUEST, "Giá sản phẩm không hợp lệ");
        }
        Product savedProduct = productRepository.save(product);
        URI location = ServletUriComponentsBuilder
                .fromCurrentRequest()
                .path("/{id}")
                .buildAndExpand(savedProduct.getId())
                .toUri();
        return ResponseEntity.created(location).body(savedProduct);
    }

    // READ - Lấy tất cả sản phẩm
    @GetMapping
    public ResponseEntity<List<Product>> getAllProducts() {
        List<Product> products = productRepository.findAll();
        if (products.isEmpty()) {
            return ResponseEntity.noContent().build();
        }
        return ResponseEntity.ok(products);
    }

    // READ - Lấy sản phẩm theo ID
    @GetMapping("/{id}")
    public ResponseEntity<Product> getProductById(@PathVariable Long id) {
        Product product = productRepository.findById(id)
                .orElseThrow(() -> new ApiException(HttpStatus.NOT_FOUND, "Không tìm thấy sản phẩm với ID: " + id));
        return ResponseEntity.ok(product);
    }

    // UPDATE - Cập nhật sản phẩm
    @PutMapping("/{id}")
    public ResponseEntity<Product> updateProduct(@PathVariable Long id, @RequestBody Product productDetails) {
        Product product = productRepository.findById(id)
                .orElseThrow(() -> new ApiException(HttpStatus.NOT_FOUND, "Không tìm thấy sản phẩm với ID: " + id));
        if (productDetails.getPrice() < 0) {
            throw new ApiException(HttpStatus.BAD_REQUEST, "Giá sản phẩm không hợp lệ");
        }
        product.setName(productDetails.getName());
        product.setPrice(productDetails.getPrice());
        product.setDescription(productDetails.getDescription());
        Product updatedProduct = productRepository.save(product);
        return ResponseEntity.ok(updatedProduct);
    }

    // DELETE - Xóa một sản phẩm
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
        Product product = productRepository.findById(id)
                .orElseThrow(() -> new ApiException(HttpStatus.NOT_FOUND, "Không tìm thấy sản phẩm với ID: " + id));
        productRepository.delete(product);
        return ResponseEntity.noContent().build();
    }

    // DELETE - Xóa hàng loạt
    @DeleteMapping("/batch")
    public ResponseEntity<String> deleteMultipleProducts(@RequestBody List<Long> ids) {
        if (ids == null || ids.isEmpty()) {
            throw new ApiException(HttpStatus.BAD_REQUEST, "Danh sách ID không hợp lệ");
        }
        productRepository.deleteAllById(ids);
        return ResponseEntity.ok("Đã xóa " + ids.size() + " sản phẩm");
    }

}
```

---

### Các thay đổi cụ thể
1. **CREATE**: Giữ nguyên `ResponseEntity.created(location).body(savedProduct)` vì đây là cách chuẩn cho 201 với URI.
2. **READ (All)**:
   - `ResponseEntity.status(HttpStatus.NO_CONTENT).build()` → `ResponseEntity.noContent().build()`
   - `ResponseEntity.status(HttpStatus.OK).body(products)` → `ResponseEntity.ok(products)`
3. **READ (ID)**:
   - `ResponseEntity.status(HttpStatus.OK).body(product)` → `ResponseEntity.ok(product)`
4. **UPDATE**:
   - `ResponseEntity.status(HttpStatus.OK).body(updatedProduct)` → `ResponseEntity.ok(updatedProduct)`
5. **DELETE (Single)**:
   - `ResponseEntity.status(HttpStatus.NO_CONTENT).build()` → `ResponseEntity.noContent().build()`
6. **DELETE (Batch)**:
   - `ResponseEntity.status(HttpStatus.OK).body(message)` → `ResponseEntity.ok(message)`

---

### Response mẫu (giữ nguyên định dạng)
#### CREATE
- **Thành công**: `201 Created`, Header `Location`, Body: Product object.
- **Lỗi**: `400 Bad Request`, Body:
  ```json
  {
      "status": 400,
      "error": "Bad Request",
      "message": "Tên sản phẩm không được để trống"
  }
  ```

**READ (All)**
- **Thành công**:
    - **Mã phản hồi**: `200 OK`
    - **Nội dung**: Trả về một danh sách các đối tượng sản phẩm (`List<Product>`).
- **Không có dữ liệu**:
    - **Mã phản hồi**: `204 No Content`
    - **Nội dung**: Không có body phản hồi.
---
**READ (ID)**
- **Thành công**:
    - **Mã phản hồi**: `200 OK`
    - **Nội dung**: Trả về một đối tượng sản phẩm (`Product object`).
- **Lỗi**:
    - **Mã phản hồi**: `404 Not Found`
    - **Nội dung**: Không có body phản hồi hoặc chi tiết lỗi tùy thuộc vào thiết kế API.

#### UPDATE

- **Thành công**: 200 OK, Body: Updated Product.
- **Lỗi**: 400 hoặc 404, Body: ApiErrorResponse.

#### DELETE

- **Thành công**: 204 No Content, không body.
- **Lỗi**: 404 Not Found, Body: ApiErrorResponse.

#### DELETE (Batch)

- **Thành công**: 200 OK, Body: "Đã xóa X sản phẩm".
- **Lỗi**: 400 Bad Request, Body: ApiErrorResponse



### Exeption : 
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ApiException.class)
    public ResponseEntity<ApiErrorResponse> handleApiException(ApiException ex) {
        ApiErrorResponse errorResponse = new ApiErrorResponse(
                ex.getStatus().value(),
                ex.getStatus().getReasonPhrase(),
                ex.getMessage()
        );
        return ResponseEntity.status(ex.getStatus()).body(errorResponse);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ApiErrorResponse> handleValidationException(MethodArgumentNotValidException ex) {
        String message = ex.getBindingResult().getFieldErrors().stream()
                .map(error -> error.getField() + ": " + error.getDefaultMessage())
                .collect(Collectors.joining(", "));
        ApiErrorResponse errorResponse = new ApiErrorResponse(
                HttpStatus.BAD_REQUEST.value(),
                HttpStatus.BAD_REQUEST.getReasonPhrase(),
                message
        );
        return ResponseEntity.badRequest().body(errorResponse);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ApiErrorResponse> handleGenericException(Exception ex) {
        ApiErrorResponse errorResponse = new ApiErrorResponse(
                HttpStatus.INTERNAL_SERVER_ERROR.value(),
                HttpStatus.INTERNAL_SERVER_ERROR.getReasonPhrase(),
                "Lỗi hệ thống: " + ex.getMessage()
        );
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(errorResponse);
    }
}
```
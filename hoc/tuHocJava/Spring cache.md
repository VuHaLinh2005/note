- **nghĩa**: Spring Cache là cơ chế lưu tạm dữ liệu (cache) để tránh lặp lại truy vấn nặng, như lấy danh sách sản phẩm từ database.
- **Cách dùng**:
    - Thêm annotation @EnableCaching vào class chính.
    - Dùng @Cacheable trên method, ví dụ:

```java
@Cacheable("products")
public List<Product> getAllProducts() {
    return productRepository.findAll();
}
```

**Lần đầu** chạy thì lấy từ **~={red}database=~**, lần sau lấy từ cache.



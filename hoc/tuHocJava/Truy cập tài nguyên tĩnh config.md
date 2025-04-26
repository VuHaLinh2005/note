**[[file static and dynamic | xem thêm static and dynamic]]**
Hàm `addResourceHandlers` cấu hình cách **Spring Boot** xử lý các tài nguyên **tĩnh**, như file **CSS**, **JavaScript**, **hình ảnh**,...  Nó ánh xạ các URL tới các vị trí cụ thể trên hệ thống file hoặc classpath.

Cụ thể, dòng `registry.addResourceHandler("/css/**").addResourceLocations("/resources/css/");` làm việc sau:

* **`addResourceHandler("/css/**")`**:  Đây là phần URL mà người dùng sẽ sử dụng để truy cập tài nguyên.  `/css/**` nghĩa là bất kỳ URL nào bắt đầu bằng `/css/` sẽ được xử lý bởi resource handler này.  `**` là **wildcard**, khớp với bất kỳ đường dẫn nào sau `/css/`.

* **`addResourceLocations("/resources/css/")`**: Đây là **vị trí** thực tế của các file CSS trên **server**.  `/resources/` thường ánh xạ tới thư mục `src/main/resources` trong project.

**Ví dụ:**

Giả sử bạn có file `style.css` trong thư mục `src/main/resources/css`.

* Khi người dùng truy cập URL `/css/style.css`, Spring Boot sẽ tìm file `style.css` trong thư mục `src/main/resources/css` và trả về cho trình duyệt.
* Khi người dùng truy cập URL `/css/other/another.css`, Spring Boot sẽ tìm file `other/another.css` trong thư mục `src/main/resources/css`.

**Một ví dụ khác:**

Nếu bạn muốn truy cập các file tĩnh trong thư mục `static` (thư mục mặc định của Spring Boot cho tài nguyên tĩnh), bạn có thể cấu hình như sau:

```java
registry.addResourceHandler("/static/**").addResourceLocations("classpath:/static/"); 
```

Hoặc nếu muốn cho phép truy cập tất cả tài nguyên trong thư mục `static`  mà không cần prefix `/static`, bạn có thể làm như sau:

```java
registry.addResourceHandler("/**").addResourceLocations("classpath:/static/");
```

Tóm lại, hàm `addResourceHandlers` giúp bạn kiểm soát cách Spring Boot phục vụ các tài nguyên tĩnh, cho phép bạn tùy chỉnh URL và vị trí của các file này.  Điều này rất hữu ích khi bạn muốn tổ chức các tài nguyên tĩnh theo cách riêng của mình hoặc khi bạn muốn sử dụng CDN.


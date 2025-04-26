Spring Boot phân biệt file tĩnh và động dựa vào cách bạn cấu hình và cách bạn trả về kết quả từ controller.

**File tĩnh:**

* **Vị trí:**  Mặc định, Spring Boot coi các file trong các thư mục sau là tài nguyên tĩnh:
    * `/src/main/resources/static`
    * `/src/main/resources/public`
    * `/src/main/resources/META-INF/resources`
* **Truy cập:** Bạn truy cập **trực tiếp** qua **URL** tương ứng với đường dẫn file trong các thư mục trên. Ví dụ: `/css/style.css`, `/images/logo.png`, `/index.html`.
* **Không xử lý:** Spring Boot **không** sử dụng template engine để xử lý các file tĩnh. Chúng được phục vụ **trực tiếp** cho **trình duyệ**t.
* **Cấu hình thêm:** Bạn có thể cấu hình thêm vị trí chứa tài nguyên tĩnh thông qua **addResourceHandlers**  .

**File động:**

* **Vị trí:**  Vị trí của file động được xác định bởi `spring.mvc.view.prefix` (mặc định là `/WEB-INF/`) và không nằm trong các thư mục dành cho tài nguyên tĩnh.
* **Truy cập:** Bạn **không** truy cập trực tiếp.  Controller trả về tên view (logical view name), và Spring Boot sử dụng `ViewResolver` để tìm và xử lý file view tương ứng.
* **Xử lý:** Spring Boot sử dụng template engine (như Thymeleaf, FreeMarker,...) để xử lý file view động, kết hợp dữ liệu từ model để tạo ra HTML cuối cùng.
* **Cấu hình:** Bạn cấu hình `ViewResolver` để Spring Boot biết cách tìm và xử lý view.


**Tóm lại:**

* Nếu bạn muốn file được phục vụ **trực tiếp** mà **không** cần **xử lý**, hãy đặt nó vào thư mục `static` (hoặc các thư mục tương tự) hoặc cấu hình **addResourceHandlers**.   
* Nếu bạn muốn file được xử lý bởi **[[Template engine]]** (ví dụ: file JSP, HTML với Thymeleaf), hãy đặt nó vào thư mục được cấu hình bởi `spring.mvc.view.prefix` và trả về **tên view** từ **controller**.

**Không phải tất cả file trong `resources` đều là tĩnh:** Thư mục `resources` có thể chứa nhiều loại file khác nhau, không chỉ là tài nguyên tĩnh. Ví dụ, file cấu hình, file template, file data,...  Chỉ các file trong các thư mục con cụ thể (như `static`, `public`,...) hoặc được cấu hình rõ ràng qua **addResourceHandlers** mới được coi là tài nguyên **tĩnh**.



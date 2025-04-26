#controller





🏷️ **`@Controller` là gì?** `@Controller` là một annotation (chú thích) trong Spring Framework, chủ yếu dùng để đánh dấu một lớp là một _controller_ (bộ điều khiển) trong ứng dụng Spring MVC (Model-View-Controller). Lớp này sẽ chịu trách nhiệm **xử lý các yêu cầu HTTP từ client**, và thường được dùng trong các ứng dụng web.


- `@Controller` sẽ trả về một **view** (trang web) thay vì trả về dữ liệu JSON hay XML. Thường sử dụng với các ứng dụng có giao diện người dùng.--> nó sẽ nhảy đến mục view để tìm.
- `@RestController` sẽ trả về **dữ liệu JSON hoặc XML** trực tiếp thay vì trả về một **view**, thường sử dụng cho API **RESTful**. `@RestController` thực chất là kết hợp của `@Controller` và `@ResponseBody`, giúp trả dữ liệu một cách trực tiếp.

Khi bạn return "helo.jsp" từ một controller @Controller, Spring sẽ coi "helo.jsp" là một tên **view logic**. 
Nếu bạn đã cấu hình ViewResolver với prefix="/WEB-INF/view/" và suffix=".jsp", và file helo.jsp tồn tại trong thư mục /WEB-INF/**view**/, thì ViewResolver sẽ **tìm** thấy file này.  

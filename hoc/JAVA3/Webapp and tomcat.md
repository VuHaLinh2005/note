

## what? 
# Ứng dụng của bạn trên Tomcat là gì?

Khi mình đề cập đến "ứng dụng", mình đang nói về **ứng dụng web** mà bạn đang phát triển và triển khai trên Tomcat. Cụ thể hơn, trong dự án của bạn, **ứng dụng web** chính là toàn bộ dự án chứa thư mục `webapp` mà bạn đã xây dựng, bao gồm tất cả các file JSP, các class Java (servlet), và các tài nguyên khác cần thiết cho ứng dụng web của bạn.

## Ứng dụng web trong dự án của bạn:
- **Ứng dụng web** của bạn là tất cả những gì bạn triển khai lên máy chủ (Tomcat). Nó bao gồm:
  - **Thư mục `webapp`**: Đây là nơi chứa các file JSP (ví dụ `index.jsp`), CSS, JS, và các tài nguyên web tĩnh khác.
  - **Thư mục `WEB-INF`**: Đây là nơi chứa các file cấu hình như `web.xml`, các thư viện cần thiết, và các tài nguyên không truy cập được trực tiếp từ trình duyệt.
  - **Code Java** (ở trong `src/main/java`): Đây là nơi chứa các servlet, controller, và các lớp xử lý logic của ứng dụng.
  
  Khi bạn triển khai dự án này lên Tomcat, toàn bộ **ứng dụng web** sẽ được đưa lên máy chủ và có thể truy cập từ trình duyệt.

## Thư mục `webapp` là một phần của ứng dụng:
- **`webapp`** trong dự án của bạn chỉ là một phần của **ứng dụng web**. Nó chủ yếu chứa các tài nguyên tĩnh (JSP, HTML, CSS, JS) và cấu hình web (trong `WEB-INF`).
- Nhưng **ứng dụng web** còn bao gồm cả các class Java (servlet, class hỗ trợ khác), các file cấu hình, và có thể có cả các thư viện (JAR file) để ứng dụng chạy đúng.

## Ứng dụng web và Tomcat:
- **Tomcat** là **máy chủ ứng dụng web**. Nhiệm vụ của nó là chạy ứng dụng web mà bạn triển khai và cung cấp cho người dùng thông qua các yêu cầu HTTP.
- Khi bạn triển khai dự án của mình lên Tomcat, Tomcat sẽ xem toàn bộ dự án của bạn như **một ứng dụng web**. Tùy thuộc vào cấu hình **context path**, bạn có thể truy cập ứng dụng này từ một URL cụ thể trên trình duyệt.

## Ví dụ về ứng dụng web trong dự án của bạn:
Trong dự án của bạn, cấu trúc thư mục sẽ giống như sau:
demoKT/
|
|- src/
|  |- main/
|     |- java/                <- Code Java (Servlets, Utils, etc.)
|     |  |- com.linh.demokt/ 
|     |     |- HelloServlet.java
|     |     |- testServerlet.java
|     |
|     |- resources/
|
|- webapp/                   <- Web files (JSP, HTML, CSS, JS, etc.)
|  |- WEB-INF/
|  |- index.jsp             <- Trang JSP chính của bạn
|
|- target/


## đơn giản là : 
Tomcat là một web server và servlet container, tức là nó giúp chạy các ứng dụng web viết bằng Java. Khi bạn triển khai một ứng dụng web trên Tomcat, ứng dụng đó thường được chứa trong một "context," và mỗi context này có một đường dẫn riêng.

Ví dụ, nếu ứng dụng của bạn có tên là "myapp" và bạn không đặt nó vào root context, thì URL truy cập sẽ là:

bash

Copy code

`http://localhost:8080/myapp`

**Root context** là khi ứng dụng của bạn chạy ở đường dẫn gốc của server, tức là:

arduino

Copy code

`http://localhost:8080/`

Nếu không có ứng dụng nào được triển khai tại root context, truy cập vào URL gốc như `http://localhost:8080/` sẽ dẫn đến lỗi 404 vì server không biết phải tìm ứng dụng nào ở đó.

Ví dụ dễ hiểu:

Hãy tưởng tượng Tomcat giống như một trung tâm thương mại (web server) với nhiều cửa hàng (ứng dụng). Mỗi cửa hàng có một tên và địa chỉ cụ thể (context). Nếu bạn không gán cửa hàng của bạn vào địa chỉ gốc (root), thì khách hàng vào trung tâm thương mại nhưng không thấy cửa hàng nào cả, dẫn đến lỗi “404 - Không tìm thấy”.

Tuy nhiên, nếu bạn đặt cửa hàng của bạn ở ngay cổng chính (root context), khách hàng sẽ thấy nó ngay lập tức khi họ bước vào trung tâm.

Vì vậy, để tránh lỗi 404, bạn cần đảm bảo rằng ứng dụng của bạn được gán vào root context hoặc cung cấp đúng đường dẫn context để truy cập.

## cổng 8080 ?
Đúng vậy! Cổng `http://localhost:8080/` là trỏ vào Tomcat.

Cụ thể hơn:

- **`localhost`** là địa chỉ chỉ ra rằng bạn đang truy cập vào máy chủ cục bộ (máy tính của bạn).
- **`8080`** là cổng mà Tomcat mặc định lắng nghe các yêu cầu HTTP.

Khi bạn gõ `http://localhost:8080/` vào trình duyệt, yêu cầu này được gửi đến Tomcat (đang chạy trên máy của bạn) qua cổng 8080. Tomcat sẽ kiểm tra xem có ứng dụng nào được triển khai tại **root context** hay không. Nếu có, nó sẽ trả về trang ứng dụng tương ứng. Nếu không có ứng dụng nào ở root context, bạn sẽ nhận được lỗi 404 vì Tomcat không tìm thấy ứng dụng nào để phản hồi.

Tóm lại, `http://localhost:8080/` là địa chỉ bạn dùng để giao tiếp với Tomcat khi nó đang chạy trên máy tính của bạn và lắng nghe trên cổng 8080.
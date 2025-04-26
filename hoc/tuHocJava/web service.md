


## at 
25' bài 4.

- chủ yếu use restfull api ==> json


## lý thuyết

- restfull api : web and app use chung api(chung data-đồng bộ dữ liệu) có 2 loại rest( use json) và soap

- **API và Web Service đều là cách để giao tiếp giữa các hệ thống** và chia sẻ dữ liệu hoặc chức năng.
- Cả hai có thể thực hiện qua mạng để cho phép truy cập từ xa, đặc biệt là khi nói đến **Web API** và **REST API**.

### Điểm khác biệt

- **API** là khái niệm bao quát hơn, có thể hoạt động ngay cả trên cùng một hệ thống mà không cần internet.
- **Web Service** là một **loại API** nhưng yêu cầu phải sử dụng qua mạng và thường áp dụng các giao thức và định dạng chuẩn (SOAP, REST, XML, JSON).

### Tóm lại

Khi nhắc đến web service, bạn đang nói đến một API đặc biệt **phải hoạt động qua mạng** và tuân theo các tiêu chuẩn giao tiếp web. Web service chính là một API, nhưng không phải mọi API đều là web service.

Đúng rồi, web service thực chất là một cách để các hệ thống khác nhau có thể **chia sẻ và sử dụng dữ liệu chung** một cách dễ dàng. Thay vì phải xây dựng lại toàn bộ chức năng hoặc dữ liệu trong từng ứng dụng, web service cho phép **một hệ thống cung cấp dữ liệu hoặc tính năng có sẵn** mà **hệ thống khác có thể dùng trực tiếp**.
-  **cũng chỉ để giao tiếp với hệ thống đó**
### Cách hoạt động chi tiết

1. **Chia sẻ dữ liệu hoặc chức năng**: Giả sử một hệ thống quản lý kho hàng có thể cung cấp dịch vụ web để tra cứu số lượng hàng tồn. Các hệ thống khác như quản lý bán hàng, kế toán có thể gọi dịch vụ này để lấy thông tin hàng tồn kho mà không cần tự quản lý dữ liệu này.
    
2. **Yêu cầu và phản hồi**: Khi một ứng dụng muốn sử dụng dữ liệu hoặc chức năng từ hệ thống khác, nó sẽ gửi một yêu cầu (request) đến web service. Web service này sẽ xử lý yêu cầu, truy xuất dữ liệu cần thiết và trả về kết quả (response).
    
3. **API và Data chung**: Web service thường được cung cấp dưới dạng **API (Application Programming Interface)**, giúp các ứng dụng khác có thể gửi yêu cầu và nhận dữ liệu một cách chuẩn hóa. Ví dụ, các hệ thống có thể truy cập cùng một **cơ sở dữ liệu** hoặc **hệ thống quản lý** thông qua API mà web service cung cấp.
    

### Ví dụ cụ thể

Ví dụ trong ngành thương mại điện tử, khi người dùng đặt hàng trên ứng dụng bán hàng, ứng dụng có thể gọi đến web service của hệ thống vận chuyển để:

- Kiểm tra các dịch vụ vận chuyển có sẵn.
- Đặt lịch giao hàng.
- Theo dõi đơn hàng.

Dữ liệu vận chuyển này có thể được nhiều hệ thống khác sử dụng mà không cần lưu lại hoặc phát triển lại từ đầu.

## Tóm lại
Không hẳn là một, nhưng có sự chồng chéo. **Web service là một dạng của API** - tức là một loại cụ thể của API dùng để giao tiếp qua mạng và thường dùng giao thức HTTP. Không phải tất cả API đều là web service, nhưng hầu hết web service là **API**.
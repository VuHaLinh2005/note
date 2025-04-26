
#SessionFactory 
#session


Hiểu theo cách đơn giản:

- **SessionFactory** là **nhà máy tạo ra các kết nối**.
    
    - Nó giống như một **quản lý kết nối**, nhưng không trực tiếp thực hiện thao tác với cơ sở dữ liệu. SessionFactory chỉ có nhiệm vụ **cung cấp các `Session`** khi cần.
    - Bạn có thể coi nó là "quản lý phiên làm việc," vì nó chỉ tạo ra các `Session` (phiên làm việc) cho ứng dụng, và nó chỉ tồn tại một lần duy nhất trong ứng dụng.
- **Session** là **phiên làm việc thực tế** với cơ sở dữ liệu.
    
    - **Mỗi `Session` là một kết nối ngắn hạn** với cơ sở dữ liệu, tương tự `Connection` trong JDBC.
    - Trong mỗi `Session`, bạn có thể thực hiện các thao tác (thêm, sửa, xóa, truy vấn) và thực thi nhiều lệnh SQL thông qua Hibernate.
    - Khi công việc xong, bạn **đóng `Session`** để kết thúc phiên làm việc và giải phóng tài nguyên.

### Gọi tên để dễ hiểu hơn:

- **SessionFactory**: Gọi là **"nhà máy tạo phiên làm việc"** hoặc **"nhà máy tạo kết nối"**.
- **Session**: Gọi là **"phiên làm việc"** hay **"kết nối"** tùy hoàn cảnh, nhưng chính xác hơn là **"phiên làm việc"** vì nó là một kết nối tạm thời để làm việc với cơ sở dữ liệu, và có thể mở/đóng khi cần.

### Tóm lại:

- **SessionFactory** quản lý và tạo ra các `Session`.
- **Session** là "phiên làm việc" thực tế với cơ sở dữ liệu, tương đương với "một kết nối" khi đang mở.

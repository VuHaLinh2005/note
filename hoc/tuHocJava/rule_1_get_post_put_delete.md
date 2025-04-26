#rule 

GET : lấy data
POST : Thêm data
PUT : Sửa data
DELETE : xoá data


## get and delete 
Bạn có một ý tưởng khá hợp lý về việc sử dụng `@DeleteMapping`, và mình sẽ giải thích tại sao nên phân biệt các phương thức HTTP (`GET`, `POST`, `PUT`, `DELETE`) dù về mặt cú pháp có thể không khác nhau nhiều.

Khi bạn nói rằng **"nó không khác gì cái GET bình thường"**, thực tế là về mặt xử lý dữ liệu, cả `GET` và `DELETE` đều có thể làm công việc tương tự, vì cả hai đều có thể lấy tham số từ URL và thực hiện một hành động nào đó, như xóa hay lấy thông tin. Tuy nhiên, **mục đích và quy ước** của các phương thức HTTP này là hoàn toàn khác nhau. Đây là lý do tại sao:

### 1. **Phân biệt các hành động với phương thức HTTP**

HTTP có bốn phương thức chính mà các API RESTful thường sử dụng để thể hiện hành động trên tài nguyên:

- **`GET`**: Dùng để **lấy** thông tin (đọc dữ liệu).
- **`POST`**: Dùng để **tạo mới** một tài nguyên.
- **`PUT`**: Dùng để **cập nhật** một tài nguyên hiện có.
- **`DELETE`**: Dùng để **xóa** một tài nguyên.

Khi bạn sử dụng **`@DeleteMapping`** để định nghĩa phương thức API xóa, nó thể hiện rõ ràng mục đích của phương thức đó là để **xóa** dữ liệu. Điều này giúp người đọc mã, lập trình viên khác, hoặc hệ thống API hiểu rõ **hành động** mà API đang thực hiện mà không cần xem chi tiết bên trong mã.

### 2. **Quy ước RESTful và tính dễ hiểu của API**

Trong kiến trúc **RESTful**, phương thức HTTP và URL được sử dụng theo quy ước để làm cho API dễ hiểu và thống nhất:

- Khi bạn sử dụng **`DELETE /api/building/{id}`**, điều này ngầm định rằng bạn đang **xóa** một tài nguyên `building` với `id` được cung cấp.
- Nếu bạn sử dụng **`GET`** thay cho **`DELETE`** để xóa một tài nguyên, điều này sẽ gây **nhầm lẫn** cho người sử dụng API hoặc các lập trình viên khác. Khi họ nhìn thấy một `GET`, họ sẽ mong đợi hành động là **lấy thông tin**, chứ không phải **xóa** dữ liệu.

### 3. **Thực hành tốt về bảo mật**

- Việc sử dụng `GET` để xóa dữ liệu cũng có thể tiềm ẩn **rủi ro bảo mật**. Các trình duyệt, bộ nhớ cache, hoặc các hệ thống bên thứ ba có thể tự động gọi phương thức `GET` với các lý do khác nhau (ví dụ, tiền xử lý hoặc lấy trước dữ liệu để tăng tốc độ). Nếu bạn dùng `GET` để xóa dữ liệu, điều này có thể dẫn đến việc dữ liệu bị xóa ngoài ý muốn.
- `DELETE`, `POST`, và `PUT` ít bị gọi tự động hơn trong các bối cảnh này và đòi hỏi sự kiểm soát có chủ đích từ phía client.

### 4. **HTTP Verb và Idempotence**

- `DELETE` là một phương thức **idempotent**, có nghĩa là nếu bạn gọi nó nhiều lần với cùng một tham số, kết quả sẽ giống nhau sau mỗi lần gọi (tài nguyên sẽ bị xóa nếu nó tồn tại).
- `GET` cũng là idempotent, nhưng mục đích của nó là **không có tác dụng thay đổi trạng thái** của tài nguyên.

### 5. **Khả năng bảo trì mã**

Khi bạn viết mã với các phương thức HTTP phù hợp, bạn đang tuân thủ **quy ước chuẩn** và giúp cho mã dễ bảo trì hơn trong tương lai. Những lập trình viên khác khi nhìn vào `@DeleteMapping` sẽ hiểu ngay rằng đây là phương thức dùng để **xóa** tài nguyên, và họ không cần phải đọc sâu vào từng dòng mã để hiểu ý định của bạn.
### Tóm lại:

- **`GET`** và **`DELETE`** tuy về mặt kỹ thuật có thể sử dụng để thực hiện các tác vụ tương tự, nhưng chúng được dùng cho **mục đích khác nhau** và có **quy ước khác nhau** trong RESTful API.
- Sử dụng `DELETE` khi bạn cần xóa là cách **tuân thủ tiêu chuẩn**, **rõ ràng về ý định**, **dễ hiểu**, và **an toàn hơn**.

Việc sử dụng đúng phương thức HTTP giúp đảm bảo rằng API của bạn **dễ đọc, dễ hiểu, dễ duy trì**, và tuân theo chuẩn **RESTful**. Điều này làm cho API của bạn nhất quán và dễ sử dụng cho người khác.




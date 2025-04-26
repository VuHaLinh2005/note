
Bộ ba display: **-webkit-box**, **-webkit-line-clamp**: 2, và **-webkit-box-orient**: **vertical** làm việc cùng nhau để:

- Biến phần tử thành một "box" đặc biệt (display: -webkit-box).
- Giới hạn số dòng hiển thị (-webkit-line-clamp: 2).
- Xác định hướng của các dòng (-webkit-box-orient: vertical).

Nếu thiếu một trong ba, việc giới hạn 2 dòng sẽ không hoạt động. Ví dụ: nếu không có display: -webkit-box, -webkit-line-clamp sẽ bị bỏ qua, và văn bản sẽ hiển thị toàn bộ.

--> thêm 2 của nợ này nữa.
overflow: **hidden** và text-overflow: **ellipsis**

nhớ :   height: 40px; /* **Giới hạn chiều cao** để chỉ hiển thị 2 dòng */

**đừng** padđing nó **che mât** 
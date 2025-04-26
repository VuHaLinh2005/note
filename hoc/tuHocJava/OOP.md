## là gì ??
Bốn tính chất chính của lập trình hướng đối tượng (OOP) là:

1. **Abstraction (Trừu tượng hóa):**
   - **Tác dụng/định nghĩa:** là kĩ thuật **~={red}Ẩn giấu=~** chi tiết **triển khai** phức tạp và chỉ hiển thị thông tin cần thiết cho người dùng.  Giúp đơn giản hóa việc sử dụng và hiểu code, tập trung vào ~={red}"**cái gì**"=~ thay vì "như thế nào".
   - **Điểm mấu chốt**:
- Biểu hiện qua **interface** hoặc **abstract class**.
- Ẩn chi tiết, chỉ để lộ phương thức cần dùng.
   - **Ví dụ:**  Khi bạn lái xe, bạn chỉ cần biết cách sử dụng vô lăng, chân ga, chân phanh mà không cần biết chi tiết động cơ hoạt động như thế nào.  Tương tự, khi sử dụng một class, bạn chỉ cần biết cách sử dụng các phương thức public mà không cần biết chi tiết implementation bên trong.

2. **Encapsulation (Đóng gói):**
   - **Tác dụng:**  **Gói dữ liệu** và **phương thức** xử lý dữ liệu đó vào cùng một đơn vị **~={red}(class).=~**  Bảo vệ dữ liệu khỏi **~={red}truy cập trái phép=~** và kiểm soát việc **~={red}thay đổi=~** dữ liệu. 
   - **Ví dụ:**  Trong một class `BankAccount`, số dư tài khoản (`balance`) được khai báo là `private` và chỉ có thể được truy cập thông qua các phương thức public như `deposit()` và `withdraw()`.  Điều này ngăn người dùng trực tiếp thay đổi số dư mà không thông qua các phương thức kiểm tra hợp lệ.
1. **Cách truy cập**: 4 mức private, default, protected, public.
- ~={red} **Bảo vệ dữ liệu**=~: Ngăn truy cập hoặc sửa đổi dữ liệu trực tiếp (bằng **~={red}private=~**), tránh lỗi hoặc thay đổi không hợp lệ.
- ~={red}**Kiểm soát truy cập**=~: Chỉ cho phép tương tác với dữ liệu qua các phương thức public (như getter/setter) có logic kiểm tra.

1. **Inheritance (Kế thừa):**
   - **Tác dụng:**  Tạo ra các class mới (class con) dựa trên các class hiện có (class cha).  Class con kế thừa các thuộc tính và phương thức của class cha, và có thể **~={red}mở rộng=~** hoặc **~={red}thay đổi=~** chúng.  **~={red}Giúp tái sử dụng code=~** ,**~={red}tránh trùng lặp=~**.
   - **Ví dụ:**  Class `Car` (Ô tô) có thể kế thừa từ class `Vehicle` (Phương tiện giao thông).  `Car` kế thừa các thuộc tính như `numberOfWheels` (số bánh xe) và các phương thức như `start()` (khởi động), và có thể thêm các thuộc tính và phương thức riêng như `numberOfDoors` (số cửa).

4. **Polymorphism (Đa hình,[[polymorphism | xem chi tiết]]):**
   - **Tác dụng:** Cho phép một đối tượng thể hiện nhiều kiểu khác nhau.  Giúp code linh hoạt hơn, dễ mở rộng và dễ bảo trì.
   - **Ví dụ:**  Trong ví dụ về `Shape` và `Circle`, `Square`, một đối tượng `Circle` vừa là `Circle`, vừa là `Shape`.  Khi gọi `draw()`, nó thể hiện kiểu `Circle`.  Điều này cho phép bạn viết code xử lý các đối tượng theo kiểu chung (`Shape`) mà không cần biết kiểu cụ thể của chúng.


**Tóm tắt tác dụng:**

* **Abstraction:** Đơn giản hóa, tập trung vào "cái gì".
* **Encapsulation:** Bảo vệ dữ liệu, kiểm soát truy cập.
* **Inheritance:** Tái sử dụng code, giảm trùng lặp.
* **Polymorphism:** Linh hoạt, dễ mở rộng, dễ bảo trì.


Bốn tính chất này kết hợp với nhau tạo nên sức mạnh của OOP, giúp bạn viết code rõ ràng, dễ hiểu, dễ bảo trì và dễ mở rộng.

 

Đầu tiên, hãy hiểu đơn giản: **Trạng thái của một đối tượng là ~={red}dữ liệu=~ (các thuộc tính/biến) mà đối tượng đó đang "có"**.

 
**1. Phương thức thường (Instance Method):**

- **Liên quan đến ~={red}Trạng thái=~:** Được dùng **khi bạn cần làm việc với ~={red}dữ liệu=~ (trạng thái) của MỘT đối tượng CỤ THỂ**.
- **Truy cập Dữ liệu:** Có thể **~={red}truy cập=~ hoặc ~={red}thay đổi=~ các thuộc tính (biến instance)** của đối tượng đó. Hành vi của nó **phụ thuộc vào trạng thái** của đối tượng.
- **Cách dùng:** **Thuộc về đối tượng** và phải **gọi qua một đối tượng** (ví dụ: `object.method()`).

**2. Phương thức tĩnh (Static Method):**

- **KHÔNG liên quan đến ~={red}Trạng thái=~:** Được dùng **khi phương thức thực hiện một tác vụ ~={red}chung=~, KHÔNG cần đến ~={red}trạng thái=~ của bất kỳ đối tượng nào**.
- **Mục đích:** Thường là **các hàm tiện ích (utility functions)** hoặc thao tác với class nói chung.
- **Cách dùng:** **Thuộc về class**, **KHÔNG có `this`** để truy cập thuộc tính đối tượng. Phải **gọi trực tiếp qua tên class** (ví dụ: `ClassName.staticMethod()`).

**Tóm lại:** Một cái **có liên quan đến trạng thái và ngược lại**.

 

|Đặc điểm|Phương thức thường (Instance Method)|Phương thức tĩnh (Static Method)|
|:--|:--|:--|
|**Thuộc về**|**Đối tượng** (Object)|**Class**|
|**Cách gọi**|**Qua đối tượng** (`object.method()`)|**Qua tên class** (`ClassName.method()`)|
|**Truy cập Dữ liệu**|**Có** (truy cập trạng thái đối tượng)|**Không** (không truy cập trạng thái đối tượng trực tiếp)|
|**Mục đích chính**|Làm việc với **trạng thái đối tượng**|**Hàm tiện ích**, thao tác class|
 
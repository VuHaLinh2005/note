 

**Trạng thái (State) là gì?**

Ngắn gọn: **Trạng thái của một đối tượng là ~={red}dữ liệu=~ mà đối tượng đó đang nắm giữ**, được thể hiện qua các ~={red}**thuộc tính=~ (biến instance)** của nó.  Nó là "tình trạng" hiện tại của đối tượng.

**Khi nào dùng phương thức thường (~={red}Instance Method=~)?**

* **Khi bạn cần làm việc với ~={red}trạng thái=~ (dữ liệu) của một đối tượng cụ thể.**
* **Khi phương thức cần ~={red}truy cập=~ hoặc ~={red}thay đổi=~ các thuộc tính (~={red}biến instance=~) của đối tượng đó.**
* **Khi hành vi của phương thức phụ thuộc vào trạng thái của đối tượng.**

**Đặc điểm của phương thức thường:**

* **Thuộc về đối tượng:**  Gắn liền với từng đối tượng cụ thể của class.
* **Gọi qua đối tượng:**  Cần gọi phương thức thông qua một đối tượng (ví dụ: `object.method()`).
* **Truy cập `this`:**  Có thể sử dụng ~={red}`this` =~để truy cập các thuộc tính của chính đối tượng đó.

**Khi nào dùng phương thức tĩnh (Static Method)?**

* **Khi phương thức thực hiện một tác vụ ~={red}chung=~, ~={red}không=~ cần đến ~={red}trạng thái=~ của bất kỳ đối tượng nào.**
* **Khi bạn muốn tạo các hàm tiện ích (utility functions) hoặc factory methods.**
* **Khi phương thức chỉ thao tác với class nói chung (ví dụ: biến static).**

**Đặc điểm của phương thức tĩnh:**

* **Thuộc về class:** Gắn liền với class, không phải đối tượng cụ thể.
* **Gọi qua tên class:** Gọi phương thức trực tiếp qua tên class (ví dụ: `ClassName.staticMethod()`).
* **Không `this` (hoặc `this` khác):** Không có `this` trong ngữ cảnh đối tượng cụ thể. Không thể truy cập trực tiếp các thuộc tính instance.

**Bảng so sánh nhanh:**

| Đặc điểm        | Phương thức thường (Instance Method) | Phương thức tĩnh (Static Method) |
|-----------------|--------------------------------------|------------------------------------|
| **Thuộc về**     | Đối tượng (Object)                    | Class                              |
| **Cách gọi**     | Qua đối tượng (`object.method()`)     | Qua tên class (`ClassName.method()`)|
| **Truy cập `this`** | Có, truy cập trạng thái đối tượng      | Không, không truy cập trạng thái đối tượng trực tiếp |
| **Mục đích chính** | Làm việc với trạng thái đối tượng      | Hàm tiện ích, factory methods, thao tác class |

tóm lại một cái **có liên quan đến trạng thái và ngược lại.**
 
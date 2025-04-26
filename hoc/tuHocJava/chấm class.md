#class 

## ví dụ
 
Hãy tưởng tượng mỗi **kiểu dữ liệu** trong Java (như `String`, `Integer`, `Double`, hay bất kỳ **class** nào bạn tự tạo) đều có một "tờ khai sinh".  Tờ khai sinh này chứa tất cả **thông tin**(**metaDaTa**) về kiểu dữ liệu đó: tên là gì, có những đặc điểm gì, có thể làm những gì,...

`.class` chính là cách để bạn lấy "tờ khai sinh" này ra.  Nó không phải là một hàm, cũng không phải bytecode, mà chỉ đơn giản là **một cú pháp đặc biệt mà Java cung cấp**.

**Ví dụ:**

Khi bạn viết `String.class`, nghĩa là bạn đang yêu cầu Java đưa cho bạn "tờ khai sinh" của kiểu dữ liệu `String`.  "Tờ khai sinh" này chứa thông tin như:

* Tên của **kiểu dữ liệu**: `String`
* Các **phương thức** của `String`: `length()`, `substring()`, `toUpperCase()`,...
* Các **trường** (nếu có):  `String` không có public fields.

"Tờ khai sinh" này được lưu trữ dưới dạng một **đối tượng** đặc biệt gọi là đối tượng `Class`.

**Tại sao lại cần "tờ khai sinh"?**

Bạn cần "tờ khai sinh" này (**`Class` object**) để làm những việc như:

* Kiểm tra kiểu dữ liệu của một đối tượng.
* Tạo ra một instance mới của một class mà không cần biết tên class cụ thể trước đó (ví dụ, khi đọc tên class từ file cấu hình).
* Ép kiểu một cách an toàn.
 
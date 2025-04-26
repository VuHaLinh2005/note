![[temple_query_method_in_spring_jpa.png]]

 Đúng rồi, hai hàm `findByNameContaining` và `findByNameContainingAndStreet` được tạo tự động bởi Spring Data JPA. Đây là một tính năng mạnh mẽ gọi là **Derived Queries (Truy vấn phái sinh)**.

Spring Data JPA phân tích **tên** **phương thức** trong interface **repository** và tự động **tạo** **truy** **vấn** tương ứng.  Trong trường hợp này:

* **`findByNameContaining(String s)`:**  Tìm tất cả các `BuildingEntity` có thuộc tính `name` chứa chuỗi `s`.  Từ khóa `Containing` tương ứng với mệnh đề `LIKE` trong SQL.

* **`findByNameContainingAndStreet(String name, String street)`:** Tìm tất cả các `BuildingEntity` có thuộc tính `name` chứa chuỗi `name` **và** thuộc tính `street` bằng chuỗi `street`.  Từ khóa `Containing` tương ứng với `LIKE` và `And` tương ứng với mệnh đề `AND` trong SQL.

**Lợi ích của Derived Queries:**

* **Giảm boilerplate code:**  Không cần viết JPQL hoặc các truy vấn phức tạp.
* **Dễ đọc và bảo trì:** Tên phương thức thể hiện rõ ràng mục đích của truy vấn.
* **Kiểm tra lỗi thời gian biên dịch:**  Nếu tên phương thức không đúng cú pháp, bạn sẽ biết ngay lúc biên dịch.
 
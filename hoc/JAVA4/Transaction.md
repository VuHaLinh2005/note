#Transaction


**Transaction** (giao dịch) trong Hibernate và cơ sở dữ liệu là một **chuỗi các thao tác** (thêm, sửa, xóa, truy vấn) được thực hiện như **một đơn vị công việc duy nhất**. Mục tiêu của transaction là **đảm bảo tính toàn vẹn dữ liệu** – nghĩa là, tất cả các thao tác trong transaction phải **hoàn tất thành công** hoặc **không có thao tác nào được thực hiện** (hoàn tác).

### Các tính chất của Transaction

Một transaction có 4 tính chất chính (ACID):

1. **Atomicity (Tính nguyên tử)**:
    
    - Mọi thao tác trong transaction đều được thực hiện trọn vẹn. Nếu một thao tác thất bại, tất cả các thao tác khác cũng phải hoàn tác, giống như không có gì được thực hiện.
2. **Consistency (Tính nhất quán)**:
    
    - Transaction phải đảm bảo dữ liệu nhất quán trước và sau khi thực hiện. Nếu transaction không thành công, dữ liệu phải trở về trạng thái ban đầu.
3. **Isolation (Tính độc lập)**:
    
    - Các transaction diễn ra độc lập với nhau. Một transaction không được ảnh hưởng bởi các transaction khác đang chạy cùng lúc.
4. **Durability (Tính bền vững)**:
    
    - Khi transaction đã thành công, tất cả thay đổi sẽ được lưu vĩnh viễn vào cơ sở dữ liệu, ngay cả khi có sự cố như mất điện sau đó.

### Cách hoạt động của Transaction trong Hibernate

1. **Bắt đầu transaction**:
    
    - Bạn mở `Session` và gọi `beginTransaction()` để bắt đầu một transaction.
    - Mọi thao tác (thêm, sửa, xóa) trong `Session` này sẽ thuộc về transaction đó.
2. **Thực hiện các thao tác trong transaction**:
    
    - Bạn có thể thêm, sửa, xóa nhiều đối tượng hoặc thực hiện nhiều truy vấn trong cùng một transaction.
    - Hibernate sẽ tạm thời lưu các thay đổi và chờ bạn hoàn tất.
3. **Commit (Cam kết)**:
    
    - Khi bạn gọi `commit()`, Hibernate sẽ gửi tất cả các thao tác đến cơ sở dữ liệu để lưu vĩnh viễn.
    - Sau khi `commit`, các thay đổi được ghi vào cơ sở dữ liệu.
4. **Rollback (Hoàn tác)**:
    
    - Nếu có lỗi xảy ra, bạn có thể gọi `rollback()` để hoàn tác tất cả thao tác trong transaction, đưa dữ liệu trở lại trạng thái ban đầu.

### Ví dụ về Transaction trong Hibernate




```java

Session session = HibernateUtils.getFACTORY().openSession(); 
Transaction transaction = null;  
try {     transaction = session.beginTransaction(); // Bắt đầu transaction      
	 // Thực hiện nhiều thao tác trong cùng transaction     
	 Users user1 = new Users("User1");     
	 Users user2 = new Users("User2");     
	 session.save(user1); // Thêm user1     
	 session.save(user2); // Thêm user2     
	  user1.setName("Updated User1");     
	  session.update(user1); // Cập nhật user1     
	   session.delete(user2); // Xóa user2      
	   transaction.commit(); // Cam kết transaction nếu mọi thao tác thành công 
	   } catch (Exception e) {     
	   if (transaction != null) 
	   transaction.rollback(); // Hoàn tác nếu có lỗi                      e.printStackTrace(); 
	   } finally {     session.close(); // Đóng phiên làm việc 
	   }`
```

### Tại sao Transaction quan trọng?

- **Bảo toàn dữ liệu**: Transaction giúp đảm bảo không xảy ra lỗi giữa chừng mà để lại dữ liệu trong trạng thái không nhất quán.
- **Thực hiện nhiều thao tác cùng lúc**: Transaction cho phép bạn gộp nhiều thao tác lại để thực hiện chỉ trong một lần cam kết, tối ưu hiệu suất.
- **Khả năng hoàn tác**: Nếu có lỗi trong bất kỳ thao tác nào, bạn có thể dùng `rollback()` để đưa tất cả về trạng thái trước khi transaction bắt đầu.

### Tóm lại:

Transaction trong Hibernate đảm bảo rằng mọi thao tác dữ liệu đều an toàn, chính xác, và có thể **hoàn tác khi cần**, giúp dữ liệu luôn ở trạng thái ổn định và đáng tin cậy.

Đúng rồi! Trong một transaction, **một lỗi nhỏ cũng không được phép xảy ra**. Nếu bất kỳ thao tác nào trong transaction gặp lỗi, toàn bộ transaction sẽ **không được cam kết (commit)**, và dữ liệu sẽ được **hoàn tác (rollback)** trở lại trạng thái ban đầu trước khi transaction bắt đầu.

### Tại sao cần phải hoàn tất thành công?

- **Đảm bảo tính toàn vẹn dữ liệu**: Khi có một lỗi xảy ra trong một loạt các thao tác, transaction sẽ hoàn tác tất cả thay đổi để tránh tình trạng dữ liệu bị sai lệch hoặc không đầy đủ.
- **Tính nguyên tử (Atomicity)**: Một transaction là một đơn vị công việc độc lập, chỉ có hai trạng thái: **hoàn thành thành công** hoặc **hoàn tác hoàn toàn**. Nếu một phần của transaction thất bại, toàn bộ transaction sẽ thất bại.

### Ví dụ về một lỗi nhỏ trong transaction

Giả sử trong một transaction, bạn thực hiện hai thao tác: thêm `User1` và cập nhật `User2`. Nếu thao tác cập nhật `User2` gặp lỗi, thì mặc dù thao tác thêm `User1` thành công, **toàn bộ transaction vẫn sẽ bị hoàn tác**, và `User1` cũng không được thêm vào cơ sở dữ liệu.

### Điều này nghĩa là gì?

- Transaction chỉ có thể **cam kết (commit)** nếu **tất cả các thao tác đều hoàn thành thành công**.
- Nếu bất kỳ thao tác nào thất bại, `rollback()` sẽ được gọi, đưa dữ liệu về trạng thái ban đầu.

Điều này giúp đảm bảo dữ liệu luôn nhất quán và đáng tin cậy trong cơ sở dữ liệu, tránh tình trạng chỉ có một phần công việc của transaction được thực hiện

### Lý do để gọi transaction là "một đơn vị công việc duy nhất"

-  **Tính nguyên tử (Atomicity)**: Transaction được xem như một "khối nguyên tử" – tất cả hoặc không có gì.
-  Tóm lại
	Transaction là **một đơn vị công việc duy nhất** vì nó đảm bảo rằng các thao tác trong đó phải thành công toàn bộ hoặc không có thao tác nào được thực hiện. Điều này bảo vệ cơ sở dữ liệu khỏi trạng thái không nhất quán khi có lỗi, giúp dữ liệu luôn chính xác và đáng tin cậy.
	 
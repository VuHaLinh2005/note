Mình sẽ giải thích chi tiết từng câu lệnh trong trigger mà mình đã đề xuất, để bạn hiểu rõ logic và ý nghĩa của nó. Trigger này được dùng để đảm bảo rằng chỉ các sản phẩm đã có trong `Order_Item` (tức là đã được đặt hàng và thanh toán) mới được thêm vào bảng `Purchased_Product`.

---

### Trigger đã đề xuất
```sql
CREATE TRIGGER CheckPurchasedProduct
ON Purchased_Product
AFTER INSERT
AS
BEGIN
    -- Kiểm tra xem product_id trong Purchased_Product có tồn tại trong Order_Item không
    IF EXISTS (
        SELECT 1
        FROM inserted i
        LEFT JOIN Order_Item oi ON i.product_id = oi.product_id
        LEFT JOIN [Order] o ON oi.order_id = o.id
        LEFT JOIN Invoice inv ON o.id = inv.order_id
        WHERE i.product_id = oi.product_id
          AND inv.payment_status = 'Paid' -- Chỉ tính đơn đã thanh toán
    )
    BEGIN
        -- Nếu hợp lệ, không làm gì (cho phép INSERT)
        RETURN;
    END
    ELSE
    BEGIN
        -- Nếu không hợp lệ, rollback và báo lỗi
        ROLLBACK;
        RAISERROR ('Cannot insert into Purchased_Product: Product must exist in Order_Item of a paid Order.', 16, 1);
    END
END;
```

---

### Giải thích từng câu lệnh
#### 1. `CREATE TRIGGER CheckPurchasedProduct`
- **Ý nghĩa**: Tạo một trigger (bộ kích hoạt) có tên là `CheckPurchasedProduct`.
- **Logic**: Trigger là một đoạn mã SQL tự động chạy khi có sự kiện xảy ra (như `INSERT`, `UPDATE`, `DELETE`) trên một bảng.

#### 2. `ON Purchased_Product`
- **Ý nghĩa**: Trigger này được gắn vào bảng `Purchased_Product`.
- **Logic**: Bất kỳ thao tác nào (theo sự kiện được định nghĩa) trên bảng `Purchased_Product` sẽ kích hoạt trigger này.

#### 3. `AFTER INSERT`
- **Ý nghĩa**: Trigger sẽ chạy **sau** khi một bản ghi được chèn (`INSERT`) vào bảng `Purchased_Product`.
- **Logic**: Khi bạn `INSERT` một bản ghi vào `Purchased_Product`, trigger sẽ kiểm tra xem bản ghi đó có hợp lệ hay không.

#### 4. `AS BEGIN ... END`
- **Ý nghĩa**: Đây là cú pháp bắt đầu và kết thúc thân của trigger, chứa các câu lệnh logic.
- **Logic**: Tất cả mã bên trong `BEGIN ... END` sẽ được thực thi khi trigger được kích hoạt.

#### 5. `IF EXISTS ( ... )`
- **Ý nghĩa**: Kiểm tra xem có bản ghi nào thỏa mãn điều kiện trong truy vấn con (`SELECT ...`) hay không.
- **Logic**: Nếu truy vấn con trả về ít nhất một bản ghi, điều kiện `EXISTS` là `TRUE`, nghĩa là bản ghi mới chèn vào `Purchased_Product` là hợp lệ.

#### 6. `SELECT 1 FROM inserted i`
- **Ý nghĩa**:
  - `inserted`: Đây là một bảng ảo đặc biệt trong SQL Server, chứa các bản ghi vừa được chèn (`INSERT`) vào bảng `Purchased_Product`.
  - `i`: Bí danh (alias) cho bảng `inserted`.
  - `SELECT 1`: Chỉ cần trả về một giá trị (ở đây là số 1) để kiểm tra sự tồn tại, không cần dữ liệu cụ thể.
- **Logic**: Lấy tất cả các bản ghi vừa được chèn vào `Purchased_Product` để kiểm tra.

#### 7. `LEFT JOIN Order_Item oi ON i.product_id = oi.product_id`
- **Ý nghĩa**:
  - `LEFT JOIN`: Kết hợp bảng `inserted` với bảng `Order_Item`.
  - `i.product_id = oi.product_id`: Điều kiện kết hợp là `product_id` trong `inserted` (bản ghi mới chèn vào `Purchased_Product`) phải khớp với `product_id` trong `Order_Item`.
  - `oi`: Bí danh cho bảng `Order_Item`.
- **Logic**: Kiểm tra xem `product_id` của bản ghi mới trong `Purchased_Product` có tồn tại trong `Order_Item` hay không. Dùng `LEFT JOIN` để nếu không tìm thấy, kết quả vẫn trả về (với giá trị `NULL` cho các cột của `Order_Item`).

#### 8. `LEFT JOIN [Order] o ON oi.order_id = o.id`
- **Ý nghĩa**:
  - `LEFT JOIN`: Kết hợp bảng `Order_Item` với bảng `Order`.
  - `oi.order_id = o.id`: Điều kiện kết hợp là `order_id` trong `Order_Item` phải khớp với `id` trong `Order`.
  - `o`: Bí danh cho bảng `Order`.
- **Logic**: Tìm đơn hàng (`Order`) tương ứng với `Order_Item` đã chứa sản phẩm (`product_id`).

#### 9. `LEFT JOIN Invoice inv ON o.id = inv.order_id`
- **Ý nghĩa**:
  - `LEFT JOIN`: Kết hợp bảng `Order` với bảng `Invoice`.
  - `o.id = inv.order_id`: Điều kiện kết hợp là `id` của `Order` phải khớp với `order_id` trong `Invoice`.
  - `inv`: Bí danh cho bảng `Invoice`.
- **Logic**: Kiểm tra xem đơn hàng (`Order`) có hóa đơn (`Invoice`) hay không, để xác định trạng thái thanh toán.

#### 10. `WHERE i.product_id = oi.product_id AND inv.payment_status = 'Paid'`
- **Ý nghĩa**:
  - `i.product_id = oi.product_id`: Đảm bảo `product_id` trong `Purchased_Product` khớp với `product_id` trong `Order_Item`.
  - `inv.payment_status = 'Paid'`: Chỉ tính các đơn hàng đã được thanh toán thành công (có `Invoice` với `payment_status = 'Paid'`).
- **Logic**: Điều kiện này đảm bảo rằng sản phẩm (`product_id`) phải:
  1. Đã có trong `Order_Item` (tức là đã được đặt hàng).
  2. Thuộc một `Order` đã được thanh toán (có `Invoice` với `payment_status = 'Paid'`).

#### 11. `BEGIN RETURN; END`
- **Ý nghĩa**:
  - `RETURN`: Thoát khỏi trigger mà không làm gì thêm.
- **Logic**: Nếu điều kiện `IF EXISTS` là `TRUE` (tức là `product_id` hợp lệ: đã có trong `Order_Item` của một `Order` đã thanh toán), trigger sẽ cho phép thao tác `INSERT` hoàn tất mà không can thiệp.

#### 12. `ELSE BEGIN ... END`
- **Ý nghĩa**: Nếu điều kiện `IF EXISTS` là `FALSE` (tức là `product_id` không hợp lệ), thực thi các câu lệnh trong khối `ELSE`.
- **Logic**: Đây là trường hợp sản phẩm không thỏa mãn điều kiện (chưa có trong `Order_Item` hoặc `Order` chưa được thanh toán).

#### 13. `ROLLBACK;`
- **Ý nghĩa**: Hủy toàn bộ thao tác `INSERT` vừa thực hiện trên `Purchased_Product`.
- **Logic**: Nếu `product_id` không hợp lệ, trigger sẽ hủy thao tác chèn bản ghi vào `Purchased_Product`, đảm bảo dữ liệu không bị sai lệch.

#### 14. `RAISERROR ('Cannot insert into Purchased_Product: Product must exist in Order_Item of a paid Order.', 16, 1);`
- **Ý nghĩa**:
  - `RAISERROR`: Tạo một thông báo lỗi và gửi về cho người dùng.
  - `'Cannot insert into Purchased_Product: Product must exist in Order_Item of a paid Order.'`: Nội dung lỗi, giải thích lý do thất bại.
  - `16`: Mức độ nghiêm trọng của lỗi (16 là mức lỗi người dùng, không phải lỗi hệ thống).
  - `1`: Trạng thái lỗi (thường để là 1).
- **Logic**: Thông báo cho người dùng biết lý do tại sao thao tác `INSERT` bị hủy (vì sản phẩm chưa có trong `Order_Item` của một `Order` đã thanh toán).

---

### Tóm tắt logic của Trigger
1. Khi có thao tác `INSERT` vào `Purchased_Product`, trigger được kích hoạt.
2. Trigger kiểm tra xem `product_id` của bản ghi mới có tồn tại trong `Order_Item` hay không, và `Order` tương ứng phải có `Invoice` với `payment_status = 'Paid'`.
3. Nếu thỏa mãn (tức là sản phẩm đã được đặt hàng và thanh toán), trigger cho phép `INSERT`.
4. Nếu không thỏa mãn, trigger hủy thao tác `INSERT` và báo lỗi.

---

### Ví dụ minh họa
- **Trường hợp hợp lệ**:
  - `Order` (ID: 1) có `Order_Item` chứa `product_id: 5`, và `Order` này có `Invoice` với `payment_status = 'Paid'`.
  - Bạn `INSERT` vào `Purchased_Product` với `product_id: 5` → Trigger kiểm tra, thấy hợp lệ → Cho phép `INSERT`.
- **Trường hợp không hợp lệ**:
  - `product_id: 10` không có trong `Order_Item` của bất kỳ `Order` nào đã thanh toán.
  - Bạn `INSERT` vào `Purchased_Product` với `product_id: 10` → Trigger kiểm tra, không thấy `product_id: 10` trong `Order_Item` → Hủy `INSERT` và báo lỗi.

---

### Tóm lại
Trigger này đảm bảo tính toàn vẹn dữ liệu bằng cách kiểm tra logic trước khi cho phép chèn vào `Purchased_Product`. Nếu bạn cần giải thích thêm hoặc muốn điều chỉnh logic, cứ hỏi mình nhé!
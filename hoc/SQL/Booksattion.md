
- **1-N (1-nhiều)**:
    - vouchers và orders: 1 voucher → nhiều đơn hàng.
    - users và orders: 1 người dùng → nhiều đơn hàng.
- **N-N (nhiều-nhiều)**:
    - vouchers và users: Qua orders.
    - vouchers và products: Qua applicable_category hoặc bảng voucher_products.
    - users và products: Qua orders và order_details.
    - **~={red}products=~** và **~={red}orders**=~: Qua **order_details.**

## ~={red}2 loại  voucher=~ ?
 
### Phân tích ý nghĩ của bạn: "1 đơn hàng vừa dùng ~={red}mã giảm giá=~ vừa dùng mã ~={red}freeship=~"

#### 1. **Ý nghĩ của bạn (1 đơn hàng dùng nhiều voucher)**:
- Bạn nghĩ rằng:  
  - 1 đơn hàng có thể dùng cả mã giảm giá (discount) và mã freeship cùng lúc.  
  - Ví dụ: Đơn hàng 101 dùng mã "GIAM10K" (giảm 10k giá hàng) và "FREESHIP20K" (miễn phí vận chuyển 20k).  
- Nếu đúng như vậy:  
  - Mối quan hệ giữa `vouchers` và `orders` sẽ là **N-N (nhiều-nhiều)**, vì 1 đơn hàng liên kết với nhiều voucher, và 1 voucher có thể được dùng trong nhiều đơn hàng.  
  - Cần bảng trung gian `order_vouchers` để lưu mối quan hệ này.

#### 2. **Phản biện: Tại sao 1 đơn hàng thường không dùng cả mã giảm giá và mã freeship cùng lúc?**
- **Thực tế trên các hệ thống lớn (Shopee, Lazada, Tiki)**:  
  - Thông thường, các hệ thống thương mại điện tử **giới hạn 1 đơn hàng chỉ dùng 1 voucher** (hoặc 1 loại voucher) tại một thời điểm.  
  - Tuy nhiên, họ thường **~={red}tách biệt=~**:  
    - **Mã giảm giá (~={red}discount=~)**: Áp dụng cho giá hàng.  
    - **Mã ~={red}freeship**=~: Áp dụng cho phí vận chuyển.  
  - Nhưng cách thiết kế phổ biến là:  
    - 1 đơn hàng có thể dùng **1 mã giảm giá** và **1 mã freeship** riêng biệt, nhưng chúng được coi là 2 loại ưu đãi **~={red}khác nhau=~**, **~={red}không=~** **~={red}gộp=~** chung vào 1 khái niệm "**~={red}voucher=~**".  
  - **Ví dụ thực tế trên Shopee**:  
    - Khi bạn thanh toán, Shopee cho phép **chọn 1 mã giảm giá** (VD: giảm 10k giá hàng) và **1 mã freeship** (VD: miễn phí vận chuyển 20k).  
    - Nhưng chúng được lưu và xử lý riêng:  
      - Mã giảm giá: Lưu trong cột `discount_voucher_id` của đơn hàng.  
      - Mã freeship: Lưu trong cột `freeship_voucher_id` của đơn hàng.  


### 1. **Tại sao không dùng cột `id` riêng làm khóa chính cho `order_details`?**

#### Ý nghĩ của bạn:
- Bạn nghĩ rằng:  
  - Bảng `order_details` nên có một cột `id` riêng (ví dụ: `order_detail_id`) làm khóa chính, tự động tăng (auto-increment).  
  - Ví dụ:  
    | order_detail_id | order_id | product_id | quantity |  
    |-----------------|----------|------------|----------|  
    | 1               | 1        | 1          | 2        |  
    | 2               | 1        | 2          | 1        |  

#### Phản biện:
- **Không cần cột `id` riêng làm khóa chính** vì:  
  - Bảng `order_details` là bảng trung gian để thể hiện mối quan hệ N-N (nhiều-nhiều) giữa `orders` và `products`.  
  - Mục đích chính của bảng này là **liên kết 1 đơn hàng với nhiều sản phẩm**, và đảm bảo mỗi cặp `order_id` và `product_id` là **~={red}duy nhất.=~**  
  
- **Dùng `order_id` và `product_id` làm khóa chính ghép** là đủ:  
  - Đảm bảo mỗi cặp `order_id` và `product_id` là duy nhất.  
  - Tiết kiệm không gian (không cần cột `id` dư **~={red}thừa=~**).  
  - Phù hợp với **~={red}mục đích=~** của bảng trung gian.


### 2. **~={red}Tại sao=~ không cho phép một đơn hàng chi tiết trùng lặp (cùng `order_id` và `product_id`)?**

#### Ý nghĩ của bạn:
- Bạn nghĩ rằng:  
  - Một đơn hàng có thể có nhiều dòng trùng lặp (cùng `order_id` và `product_id`).  
  - Ví dụ:  
    - Đơn hàng 1 có sách Harry Potter (product_id = 1) 2 lần:  
      | order_id | product_id | quantity |  
      |----------|------------|----------|  
      | 1        | 1          | 2        |  
      | 1        | 1          | 1        |  
    - Tổng số lượng Harry Potter trong đơn hàng 1 là 2 + 1 = 3.

--> **kbt** chính xác **quantity** là bao nhiêu của một đơn hàng

### 3. **Kết luận**
- **Tại sao không dùng `id` riêng làm khóa chính?**  
  - Vì `id` riêng không có ý nghĩa thực tế trong bảng trung gian.  
  - Dùng `order_id` và `product_id` làm khóa chính ghép là đủ để đảm bảo mỗi cặp là duy nhất, tiết kiệm không gian và phù hợp với mục đích của bảng.  
- **Tại sao không cho phép trùng lặp `order_id` và `product_id`?**  
  - Để dữ liệu rõ ràng, dễ quản lý, tránh lỗi.  
  - Thay vì thêm dòng **trùng** lặp, chỉ cần cập nhật `quantity` của dòng hiện có.  
- nếu **~={red}chọn 1 trong 2=~** làm **~={red}khoá chính=~** cx **~={red}k dc=~** vì nó là duy nhất thì nó **~={red}k=~** có mqh **~={red}1-N N-1=~** **vd: 1 sp k có nhiều trong order detail**
---

### SQL minh họa (cách đúng):
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    total_price INT NOT NULL
);

CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE order_details (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

-- Thêm dữ liệu
INSERT INTO orders (total_price) VALUES (400000);
INSERT INTO products (name) VALUES ('Harry Potter');
INSERT INTO order_details (order_id, product_id, quantity) VALUES (1, 1, 3);
```

- **Kết quả**:  
  - Bảng `order_details`:  
    | order_id | product_id | quantity |  
    |----------|------------|----------|  
    | 1        | 1          | 3        |  
  - Nếu thêm 1 cuốn Harry Potter nữa, chỉ cần:  
    ```sql
    UPDATE order_details SET quantity = 4 WHERE order_id = 1 AND product_id = 1;
    ```

 
-- đơn giản : chọn 1 trong hai làm khoá chính thì phá vỡ 1-N-N-1 vì khoá chính k lặp lại,

### 1. ~={red}**Giảm giá=~ và ~={red}mã giảm giá=~ khác nhau thế nào?**

#### **Giảm giá (Discount)**:
- **Nghĩa**: Là chương trình giảm giá trực tiếp trên sản phẩm, không cần khách hàng nhập mã.  
- **Ví dụ**:  
  - Sách Harry Potter giá gốc 150k, nhưng đang có chương trình **giảm giá 20k**, nên giá chỉ còn 130k.  
  - Khách hàng không cần nhập mã, giá đã tự động giảm khi họ xem sản phẩm.  
- **Nghiệp vụ**:  
  - Giảm giá thường áp dụng cho **tất cả khách hàng**, không cần điều kiện đặc biệt (như nhập mã).  
  - Có thể áp dụng cho từng sản phẩm, danh mục sách, hoặc toàn sàn (tất cả sản phẩm).  
  - Thường có **~={red}thời gian=~** áp dụng (VD: giảm giá từ ngày 1/4 đến 10/4).  

#### **Mã giảm giá (Discount Voucher)**:
- **Nghĩa**: Là mã mà khách hàng phải nhập(hoạc chọn) khi thanh toán để được giảm giá.  
- **Ví dụ**:  
  - Mã "GIAM10K": Giảm 10k cho đơn hàng từ 130k trở lên.  
  - Khách hàng phải nhập mã "GIAM10K" lúc thanh toán để được giảm.  
- **Nghiệp vụ**:  
  - Mã giảm giá thường có **~={red}điều kiện=~** (VD: đơn hàng tối thiểu 130k, chỉ áp dụng cho sách ngoại văn).  
  - Khách hàng phải chủ động nhập(hoạc **chọn**) mã, không tự động áp dụng.  
  - Thường có số lượng **giới hạn** hoặc **thời gian** sử dụng (VD: hết hạn ngày 31/3/2025).  

#### **So sánh**:
- **Giảm giá**: **~={red}Tự động áp dụng**=~, không cần mã, thường áp dụng cho sản phẩm hoặc danh mục.  
- **Mã giảm giá**: Cần nhập mã(hoạc ~={red}**chọn=~**), có điều kiện cụ thể, áp dụng khi thanh toán.  

---

### 2. **Có cần bảng giảm giá riêng không? Thông thường có không?**

#### **Có cần bảng giảm giá riêng không?**
- **Đáp án**: **Có**, nếu web bán sách của bạn có chương trình giảm giá trực tiếp (không cần mã).  
- **Lý do**:  
  - **Nghiệp vụ**: **~={red}Giảm=~** giá **~={red}trực tiếp=~** và **~={red}mã giảm giá=~** là 2 chương trình **~={red}khác nhau=~**, phục vụ mục đích khác nhau:  
    - Giảm giá trực tiếp: Thu hút khách hàng bằng cách giảm giá ngay trên sản phẩm (VD: giảm giá sách ngoại văn 20k trong tuần lễ sách).  
    - Mã giảm giá: Khuyến khích khách hàng mua nhiều hơn bằng cách đưa mã (VD: "GIAM10K" cho đơn từ 130k).  
  - Nếu **không tách** riêng:  
    - Bạn sẽ **khó** quản lý 2 loại chương trình này.  
    - Ví dụ: Nếu gộp chung vào bảng `products` (thêm cột `discount_price`), bạn sẽ không biết chương trình giảm giá bắt đầu/kết thúc khi nào, áp dụng cho danh mục nào.  
  - Tách riêng bảng `discounts` giúp:  
    - Quản lý chương trình giảm giá rõ ràng (VD: giảm giá sách ngoại văn từ 1/4 đến 10/4).  
    - Dễ áp dụng cho nhiều sản phẩm hoặc danh mục.  

#### **~={red}Thông thường=~ có bảng giảm giá riêng không?**
- **Đáp án**:~={red} **Có=~**, trong các hệ thống thương mại điện tử lớn (như **~={red}Shopee, Tiki)=~**.  
- **Lý do**:  
  - Các hệ thống lớn thường có cả 2 loại:  
    - **Giảm giá ~={red}trực tiếp**=~: Áp dụng trên sản phẩm (VD: Shopee có nhãn "Giảm giá" trên sản phẩm).  
    - ~={red} **Mã giảm giá=~**: Áp dụng khi thanh toán (VD: Shopee có phần nhập mã giảm giá).  
  - Họ thường tách riêng:  
    - Bảng `discounts` (hoặc tương tự): Quản lý chương trình giảm giá trực tiếp.  
    - Bảng `discount_vouchers`: Quản lý mã giảm giá.  
  - **Ví dụ thực tế trên Shopee**:  
    - Sản phẩm có thể có giá giảm trực tiếp (VD: từ 150k xuống 130k).  
    - Khi thanh toán, bạn vẫn có thể nhập thêm mã giảm giá (VD: "GIAM10K").  
    - Hai chương trình này hoạt động độc lập, nên cần bảng riêng để quản lý.

---

### 3. **Thiết kế ~={red}database=~ với bảng giảm giá riêng**
#### **Bảng `discounts` (giảm giá trực tiếp)**:
- **Mô tả**: Lưu thông tin chương trình **~={red}giảm=~** **~={red}giá trực tiếp=~** (không cần mã).  
- **Các trường**:  
  - `id`: Mã chương trình giảm giá (khóa chính).  
  - `discount_value`: Số tiền giảm (VD: 20000 = 20k).  
  - `applicable_category`: Danh mục áp dụng (VD: "Ngoại Văn").  
  - `start_date`: Ngày bắt đầu (VD: 2025-04-01).  
  - `end_date`: Ngày kết thúc (VD: 2025-04-10).  
  - `status`: Trạng thái (active/expired).  
- **Nghiệp vụ**:  
  - Áp dụng tự động cho sản phẩm thuộc danh mục (VD: tất cả sách ngoại văn giảm 20k).  
  - Chỉ áp dụng trong khoảng thời gian từ **`start_date` đến `end_date`.**  
- **Mối quan hệ**: **~={red}N-N với `products` (1 chương trình giảm giá áp dụng cho nhiều sản phẩm, 1 sản phẩm có thể có nhiều chương trình giảm giá).  

```sql
CREATE TABLE discounts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    discount_value INT NOT NULL,
    applicable_category VARCHAR(100),
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    status VARCHAR(20) NOT NULL
);
```

#### **~={red}Bảng=~ `discount_products` (trung gian giữa `discounts` và `products`)**:
- **Mô tả**: Liên kết chương trình **~={red}giảm giá=~** với **~={red}sản phẩm=~** (nếu cần chỉ định chính xác từng sản phẩm).  
- **Các trường**:  
  - `discount_id`: Mã chương trình giảm giá (khóa ngoại).  
  - `product_id`: Mã sản phẩm (khóa ngoại).  
- **Nghiệp vụ**:  
  - Nếu chương trình giảm giá áp dụng cho danh mục (VD: "Ngoại Văn"), bạn có thể không cần bảng này, chỉ cần kiểm tra `applicable_category`.  
  - Nếu muốn chỉ định chính xác (VD: chỉ giảm giá cho sách Harry Potter), thì cần bảng này.  

```sql
CREATE TABLE discount_products (
    discount_id INT,
    product_id INT,
    PRIMARY KEY (discount_id, product_id),
    FOREIGN KEY (discount_id) REFERENCES discounts(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

#### **Các bảng còn lại (đã có, nhưng cập nhật lại)**:

1. **Bảng `users` (người dùng)**:
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    full_name VARCHAR(100),
    email VARCHAR(100) NOT NULL,
    phone_number VARCHAR(15),
    address VARCHAR(255),
    created_at DATE NOT NULL
);
```

2. **Bảng `products` (sản phẩm)**:
```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    category VARCHAR(50),
    original_price INT NOT NULL
);
```

3. **Bảng `discount_vouchers` (mã giảm giá)**:
```sql
CREATE TABLE discount_vouchers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    code VARCHAR(50) NOT NULL,
    discount_value INT NOT NULL,
    min_order_value INT NOT NULL,
    applicable_category VARCHAR(100),
    exclude_category VARCHAR(100),
    expiration_date DATE NOT NULL,
    status VARCHAR(20) NOT NULL
);
```

4. **Bảng `freeship_vouchers` (mã freeship)**:
```sql
CREATE TABLE freeship_vouchers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    code VARCHAR(50) NOT NULL,
    freeship_value INT NOT NULL,
    min_order_value INT NOT NULL,
    expiration_date DATE NOT NULL,
    status VARCHAR(20) NOT NULL
);
```

5. **Bảng `orders` (đơn hàng)**:
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    total_price INT NOT NULL,
    shipping_fee INT NOT NULL,
    discount_voucher_id INT,
    freeship_voucher_id INT,
    order_date DATE NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (discount_voucher_id) REFERENCES discount_vouchers(id),
    FOREIGN KEY (freeship_voucher_id) REFERENCES freeship_vouchers(id)
);
```

6. **Bảng `order_details` (chi tiết đơn hàng)**:
```sql
CREATE TABLE order_details (
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

### 4. **Nghiệp vụ minh họa (cách hoạt động)**

#### **Chương trình giảm giá (Discount)**:
- **Tình huống**:  
  - Bạn có chương trình giảm giá: Giảm 20k cho sách ngoại văn, từ 1/4/2025 đến 10/4/2025.  
  - Sách Harry Potter (giá gốc 150k, thuộc danh mục "Ngoại Văn") sẽ tự động giảm còn 130k trong thời gian này.  
- **Dữ liệu trong `discounts`**:  
  | id  | discount_value | applicable_category | start_date  | end_date   | status |  
  |-----|----------------|---------------------|-------------|------------|--------|  
  | 1   | 20000          | Ngoại Văn           | 2025-04-01  | 2025-04-10 | active |  
- **Hiển thị trên web**:  
  - Khách hàng thấy giá sách Harry Potter là 130k (150k - 20k), không cần nhập mã.

#### **Mã giảm giá (Discount Voucher)**:
- **Tình huống**:  
  - Bạn có mã "GIAM10K": Giảm 10k cho đơn hàng từ 130k, áp dụng cho sách ngoại văn.  
  - Khách hàng phải nhập mã "GIAM10K" khi thanh toán.  
- **Dữ liệu trong `discount_vouchers`**:  
  | id  | code     | discount_value | min_order_value | applicable_category | expiration_date | status |  
  |-----|----------|----------------|-----------------|---------------------|-----------------|--------|  
  | 1   | GIAM10K  | 10000          | 130000          | Ngoại Văn           | 2025-03-31      | active |  
- **Hiển thị trên web**:  
  - Khách hàng mua Harry Potter (130k sau giảm giá trực tiếp), nhập mã "GIAM10K", tổng giá còn 120k.

#### **Mã freeship (Freeship Voucher)**:
- **Tình huống**:  
  - Bạn có mã "FREESHIP20K": Miễn phí vận chuyển 20k cho đơn hàng từ 150k.  
- **Dữ liệu trong `freeship_vouchers`**:  
  | id  | code         | freeship_value | min_order_value | expiration_date | status |  
  |-----|--------------|----------------|-----------------|-----------------|--------|  
  | 1   | FREESHIP20K  | 20000          | 150000          | 2025-03-31      | active |  
- **Hiển thị trên web**:  
  - Phí vận chuyển ban đầu là 20k, khách hàng nhập "FREESHIP20K", phí ship còn 0.

#### **Đơn hàng hoàn chỉnh**:
- **Tình huống**:  
  - Khách hàng Nguyễn Văn A mua 1 cuốn Harry Potter.  
  - Giá gốc: 150k.  
  - Giảm giá trực tiếp: 20k → còn 130k.  
  - Nhập mã "GIAM10K": Giảm thêm 10k → còn 120k.  
  - Nhập mã "FREESHIP20K": Phí ship từ 20k → 0k.  
  - Tổng thanh toán: 120k.  
- **Dữ liệu trong `orders`**:  
  | order_id | user_id | total_price | shipping_fee | discount_voucher_id | freeship_voucher_id | order_date  |  
  |----------|---------|-------------|--------------|---------------------|---------------------|-------------|  
  | 1        | 1       | 120000      | 0            | 1                   | 1                   | 2025-03-24  |  

---


## **~={red}lý do có bảng discount_products=~**

### **Bảng `discount_products` là gì?**
- Đây là bảng trung gian để liên kết giữa bảng `discounts` (chương trình giảm giá trực tiếp) và bảng `products` (sản phẩm).

#### **SQL**:
```sql
CREATE TABLE discount_products (
    discount_id INT,
    product_id INT,
    PRIMARY KEY (discount_id, product_id),
    FOREIGN KEY (discount_id) REFERENCES discounts(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

### **Mục đích chính: Giải quyết vấn đề gì?**

#### **Ý chính**:
- **Cho phép chỉ định chính xác từng sản phẩm được áp dụng chương trình giảm giá trực tiếp**.  
- **Giải quyết vấn đề**: Nếu chỉ dùng `applicable_category` trong bảng `discounts`, bạn không thể chọn từng sản phẩm cụ thể để giảm giá, mà chỉ áp dụng theo danh mục (category). Bảng `discount_products` giúp bạn linh hoạt hơn.

#### **Nghiệp vụ**:
- **Vấn đề khi không có bảng `discount_products`**:  
  - Trong bảng `discounts`, bạn có cột `applicable_category` (VD: "Ngoại Văn").  
  - Điều này có nghĩa: Tất cả sách thuộc danh mục "Ngoại Văn" (như Harry Potter, Sherlock Holmes) đều được giảm giá.  
  - Nhưng nếu bạn chỉ muốn giảm giá **chính xác cho Harry Potter**, mà không giảm giá cho Sherlock Holmes (dù cả 2 đều thuộc "Ngoại Văn"), thì `applicable_category` không làm được.  
- **Bảng `discount_products` giải quyết vấn đề này**:  
  - Nó cho phép bạn chọn **từng sản phẩm cụ thể** để áp dụng chương trình giảm giá, thay vì áp dụng cho cả danh mục.  
  - Mối quan hệ **~={red}N-N (nhiều-nhiều):=~**  
    - 1 chương trình giảm giá có thể áp dụng cho nhiều sản phẩm.  
    - 1 sản phẩm có thể được áp dụng nhiều chương trình giảm giá (theo thời gian).  

---

### **Ví dụ minh họa**

#### **Tình huống 1: Không có bảng `discount_products` (chỉ dùng `applicable_category`)**:
- Bảng `discounts`:  
  | id  | discount_value | applicable_category | start_date  | end_date   | status |  
  |-----|----------------|---------------------|-------------|------------|--------|  
  | 1   | 20000          | Ngoại Văn           | 2025-04-01  | 2025-04-10 | active |  
- Bảng `products`:  
  | id  | name           | category    | original_price |  
  |-----|----------------|-------------|----------------|  
  | 1   | Harry Potter   | Ngoại Văn   | 150000         |  
  | 2   | Sherlock Holmes| Ngoại Văn   | 200000         |  
- **Kết quả**:  
  - Cả Harry Potter và Sherlock Holmes đều được giảm 20k (vì cả 2 thuộc "Ngoại Văn").  
  - **Hạn chế**: Bạn không thể chỉ giảm giá cho Harry Potter mà bỏ qua Sherlock Holmes.

#### **Tình huống 2: Có bảng `discount_products`**:
- Bảng `discounts`:  
  | id  | discount_value | start_date  | end_date   | status |  
  |-----|----------------|-------------|------------|--------|  
  | 1   | 20000          | 2025-04-01  | 2025-04-10 | active |  
- Bảng `products`:  
  | id  | name           | category    | original_price |  
  |-----|----------------|-------------|----------------|  
  | 1   | Harry Potter   | Ngoại Văn   | 150000         |  
  | 2   | Sherlock Holmes| Ngoại Văn   | 200000         |  
- Bảng `discount_products`:  
  | discount_id | product_id |  
  |-------------|------------|  
  | 1           | 1          | (Chỉ Harry Potter được giảm giá)  
- **Kết quả**:  
  - Chỉ Harry Potter được giảm 20k (giá còn 130k).  
  - Sherlock Holmes không được giảm (vẫn 200k), dù cùng danh mục "Ngoại Văn".  
- **Lợi ích**: Bạn có thể chọn chính xác sản phẩm nào được giảm giá, không phụ thuộc vào danh mục.

---

### **Khi nào cần bảng `discount_products`?**
- **Cần**: Nếu bạn muốn chỉ định **từng sản phẩm cụ thể** để áp dụng giảm giá (VD: chỉ giảm giá cho Harry Potter, không giảm cho sách khác cùng danh mục).  
- **Không cần**: Nếu bạn chỉ áp dụng giảm giá theo danh mục (VD: tất cả sách "Ngoại Văn" đều giảm giá), thì chỉ cần dùng `applicable_category` trong `discounts`.

---

### **Tóm lại**
- **Mục đích chính của `discount_products`**:  
  - Giải quyết vấn đề: Không thể chỉ định chính xác từng sản phẩm để giảm giá khi chỉ dùng `applicable_category`.  
  - Cho phép bạn chọn~={red} **từng sản phẩm cụ thể**=~ để áp dụng chương trình **~={red}giảm giá.=~**  
- **Nghiệp vụ**:  
  - Tăng tính linh hoạt: Bạn có thể giảm giá cho bất kỳ sản phẩm nào, không cần phụ thuộc vào danh mục.  
  - Phù hợp với các chương trình giảm giá đặc biệt (VD: chỉ giảm giá cho một số sách nổi bật).  

Hiểu chưa bạn? Mình đã giải thích đơn giản và tập trung vào nghiệp vụ. Nếu cần thêm ví dụ, cứ nói nhé!
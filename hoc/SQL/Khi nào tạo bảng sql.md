 
 
---

### Khi nào tạo bảng mới? Khi nào không?
- **Tạo bảng mới**: Khi **một thứ có nhiều giá trị**.  
  - Ví dụ: 1 đôi giày có nhiều màu (đỏ, xanh, đen).  
  - Cách làm: Tạo bảng `colors` với cột `shoe_id` và `color`. Mỗi màu là 1 dòng.  
  - **~={red}Vì sao=~**? Nếu nhét hết vào bảng `shoes`, sẽ rối, không quản lý được.nếu 1 dày nhiều màu thì sao , tạo thêm cột à 
cứ xem nó **có quan hệ k thì tạo**
- **Không tạo bảng mới**: Khi **một thứ chỉ có 1 giá trị**.  
  - Ví dụ: 1 đôi giày chỉ có 1 trọng lượng (500g).  
  - Cách làm: Thêm cột `weight` vào bảng `shoes`.  
  - Vì sao? Đơn giản, không cần bảng riêng.

---

### Áp dụng cho flash sale:
- **Nếu 1 sản phẩm chỉ có 1 flash sale**:  
  - Ví dụ: Giảm giá 1 lần, từ 100k xuống 80k.  
  - Không tạo bảng, thêm cột `flash_sale_price` vào `products`.  
- **Nếu 1 sản phẩm có nhiều flash sale**:  
  - Ví dụ: Giảm giá 3 lần khác nhau (80k, 70k, 60k).  
  - Tạo bảng `flash_sales` với cột `product_id`, `price`, `time`.  

---

### Tóm lại:
- **Một thứ có nhiều giá trị** → Tạo bảng mới.  
- **Một thứ có 1 giá trị** → Thêm cột vào bảng cũ.  

Hiểu chưa? Rõ hơn chưa bạn?



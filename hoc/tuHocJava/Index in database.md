### **~={red}Index=~** là gì?

- Index giống như **~={red}mục lục=~** trong sách: thay vì đọc từng trang để tìm thông tin, bạn tra mục lục để **~={red}nhảy=~** thẳng đến trang cần. Trong database, index giúp MySQL tìm dữ liệu **~={red}nhanh=~** hơn mà **~={red}không=~** phải **~={red}quét hết=~** bảng.

### **Cách dùng index**

1. **Khi nào cần?**
    - Dùng cho **~={red}cột=~** hay **~={red}xuất hiện=~** trong **~={red}WHERE=~**, **~={red}ORDER BY=~**, hoặc **~={red}JOIN.=~**
    - Ví dụ: Trong shop laptop, bạn lọc sản phẩm theo giá (WHERE price < 5000) hoặc sắp xếp theo giá (ORDER BY price). Nếu không có index, MySQL sẽ quét từng dòng trong bảng products, rất chậm nếu bảng lớn.

2. **Cách tạo index**
- Cú pháp: CREATE INDEX tên_index ON tên_bảng(tên_cột);
- Ví dụ:
	```sql
	CREATE INDEX idx_price ON products(price);
```

Đây là tạo index cho **~={red}cột=~** price trong bảng products

3. **Cách kiểm tra hiệu quả**

- Dùng EXPLAIN trước câu query để xem MySQL có dùng index không:
```sql
EXPLAIN SELECT * FROM products WHERE price < 5000;
```

- Nếu không có index: Kết quả sẽ báo "ALL" (quét toàn bảng), chậm.
- Nếu có index: Báo "INDEX" hoặc "REF", nhanh hơn nhiều.

**~={red}Điểm yếu=~** : Làm **chậm** khi **thêm/sửa/xóa dữ liệu** (nhưng ít ảnh hưởng với shop của bạn).vì phải **~={red}cập nhật=~** lại **index**.


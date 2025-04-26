#join


🧩 **Tư duy để giải thích khái niệm "join bảng" trong SQL:**

1. Đầu tiên, phân tích ý nghĩa của từ "join" trong SQL: nó là phép kết nối dữ liệu từ nhiều bảng lại với nhau.
2. Xác định các loại "join" phổ biến và đặc điểm của từng loại.
3. Cung cấp ví dụ ngắn gọn để minh họa cách sử dụng.
4. Đưa ra các trường hợp sử dụng phù hợp cho từng loại "join".

---

### 🔍 **Join Bảng (Table Join) là gì?**(xếp thành một hàng nếu đúng đk)

🧑‍💻 Trong cơ sở dữ liệu (database), **Join Bảng** là một thao tác trong SQL (Structured Query Language - Ngôn ngữ Truy vấn Có Cấu trúc) giúp **kết hợp dữ liệu từ nhiều bảng khác nhau** dựa trên **một điều kiện nào đó**. Join thường được dùng khi dữ liệu của bạn nằm rải rác ở nhiều bảng, và bạn muốn xem mối quan hệ giữa chúng.

Ví dụ, bạn có hai bảng: **Khách hàng** và **Đơn hàng**. Bảng **Khách hàng** chứa thông tin về khách hàng, và bảng **Đơn hàng** chứa thông tin về các đơn hàng của họ. Dùng **join** sẽ giúp bạn kết nối hai bảng này lại để biết được đơn hàng thuộc về khách hàng nào.

---

### 🔹 **Các loại Join phổ biến:**

1. **Inner Join** 🛠️: Chỉ trả về các bản ghi (record) có dữ liệu phù hợp ở cả hai bảng.
    
    - Ví dụ: Kết hợp thông tin khách hàng và đơn hàng mà khách hàng đó đã thực hiện.
2. **Left Join (Left Outer Join)** ⬅️: Trả về tất cả các bản ghi từ bảng bên trái, và các bản ghi phù hợp từ bảng bên phải. Nếu không có dữ liệu phù hợp ở bảng bên phải, sẽ trả về giá trị NULL.
    
    - Ví dụ: Hiển thị tất cả khách hàng, kể cả khi họ không có đơn hàng.
3. **Right Join (Right Outer Join)** ➡️: Tương tự như Left Join, nhưng trả về tất cả các bản ghi từ bảng bên phải.
    
    - Ví dụ: Hiển thị tất cả đơn hàng, kể cả khi không có khách hàng nào tương ứng (đôi khi do lỗi dữ liệu).
4. **Full Join (Full Outer Join)** 🔄: Trả về tất cả bản ghi khi có sự phù hợp ở một trong hai bảng.
    
    - Ví dụ: Kết hợp dữ liệu từ cả khách hàng và đơn hàng, kể cả khi không có mối quan hệ trực tiếp giữa chúng.
5. **Cross Join** ✖️: Kết hợp tất cả các bản ghi từ hai bảng với nhau, không có điều kiện (đây là phép nhân trực tiếp hai bảng). Số lượng bản ghi sẽ rất lớn, nên cross join ít dùng.


# Ví dụ minh họa về Inner Join

Giả sử bạn có hai bảng: **KhachHang** và **DonHang**.

## Bảng **KhachHang**

| KhachHang_ID | Ten          | DiaChi           |
|--------------|--------------|------------------|
| 1            | Nguyễn Văn A | Hà Nội           |
| 2            | Trần Thị B   | TP Hồ Chí Minh   |
| 3            | Lê Văn C     | Đà Nẵng          |

## Bảng **DonHang**

| DonHang_ID | KhachHang_ID | NgayDat      |
|------------|--------------|--------------|
| 101        | 1            | 2024-10-15   |
| 102        | 1            | 2024-10-20   |
| 103        | 2            | 2024-10-18   |
| 104        | 4            | 2024-10-22   |

Trong ví dụ này:

- Cột **KhachHang_ID** trong bảng **DonHang** chính là **khóa ngoại** (foreign key) liên kết với cột **KhachHang_ID** trong bảng **KhachHang**.
- Chúng ta dùng **INNER JOIN** để kết hợp dữ liệu từ hai bảng và chỉ lấy những bản ghi có mối liên hệ trong cả hai bảng.

---

## Câu lệnh Inner Join

```sql
SELECT KhachHang.Ten, DonHang.DonHang_ID, DonHang.NgayDat
FROM KhachHang
INNER JOIN DonHang ON KhachHang.KhachHang_ID = DonHang.KhachHang_ID;

```

## Kết quả Inner Join

| Ten          | DonHang_ID | NgayDat      |
|--------------|------------|--------------|
| Nguyễn Văn A | 101        | 2024-10-15   |
| Nguyễn Văn A | 102        | 2024-10-20   |
| Trần Thị B   | 103        | 2024-10-18   |


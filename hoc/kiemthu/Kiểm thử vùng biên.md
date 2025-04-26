Trong kỹ thuật kiểm thử, **kiểm thử biên (Boundary Testing)** tập trung vào việc kiểm tra các giá trị ở **~={red}ranh giới=~** của tập đầu vào. Lý do là vì các **lỗi** thường xảy ra ở những giá trị gần “biên” (giá trị tối thiểu, tối đa, hay giá trị ngay sát ranh giới của các phân vùng). Nghĩa là thay vì chỉ kiểm thử các giá trị “bình thường”, ta còn kiểm thử các giá trị “cạnh” của tập đầu vào.

Giả sử bạn đang viết hàm tính tổng của một danh sách các số nguyên. Dưới đây là 5 trường hợp kiểm thử biên kèm với giải thích:

---

### **Boundary Case 1: Danh sách rỗng**

- **Đầu vào:** `[]`
- **Mô tả:** Đây là trường hợp biên ở mức độ “số lượng phần tử”. Nếu yêu cầu đầu vào không cho phép danh sách rỗng, hàm cần báo lỗi hoặc ném ra ngoại lệ (ví dụ: `IllegalArgumentException`).
- **Kỳ vọng:** Hệ thống trả về thông báo lỗi hay ném ngoại lệ.

---

### **Boundary Case 2: Danh sách chỉ có 1 phần tử**

- **Đầu vào:** `[7]` (hoặc bất kỳ số nguyên nào)
- **Mô tả:** Đây là ranh giới dưới của đầu vào hợp lệ (số lượng phần tử tối thiểu). Nếu hàm hoạt động đúng với danh sách chứa 1 phần tử, tổng phải chính là giá trị của phần tử đó.
- **Kỳ vọng:** Kết quả trả về là `7`.

---

### **Boundary Case 3: Ranh giới xung quanh số 0 (âm, 0 và dương)**

- **Đầu vào:** `[-1, 0, 1]`
- **Mô tả:** Đây là trường hợp kiểm tra biên cho “ranh giới giá trị” khi chuyển từ số âm sang số dương, với 0 làm ranh giới. Mục đích là kiểm tra xem hàm có xử lý đúng các giá trị âm, 0 và dương không.
- **Kỳ vọng:** Tổng = `-1 + 0 + 1 = 0`.

---

### **Boundary Case 4: Giá trị biên trên của kiểu số (Integer.MAX_VALUE)**

- **Đầu vào:** `[Integer.MAX_VALUE, 0]`
    - Ở Java, `Integer.MAX_VALUE` là giá trị lớn nhất của kiểu số nguyên (2^31 - 1).
- **Mô tả:** Trường hợp này kiểm tra xem hàm có xử lý đúng các giá trị rất lớn hay không. Nếu không có xử lý đặc biệt cho tràn số (overflow), kết quả vẫn phải trả về đúng giá trị tổng.
- **Kỳ vọng:** Tổng = `Integer.MAX_VALUE + 0` = `Integer.MAX_VALUE`.

---

### **Boundary Case 5: Giá trị biên dưới của kiểu số (Integer.MIN_VALUE)**

- **Đầu vào:** `[Integer.MIN_VALUE, 0]`
    - Ở Java, `Integer.MIN_VALUE` là giá trị nhỏ nhất của kiểu số nguyên (-2^31).
- **Mô tả:** Tương tự như trường hợp 4, nhưng với giá trị âm lớn ở biên dưới. Mục đích là kiểm tra xem hàm có xử lý đúng với các giá trị cực thấp hay không.
- **Kỳ vọng:** Tổng = `Integer.MIN_VALUE + 0` = `Integer.MIN_VALUE`.

---

 
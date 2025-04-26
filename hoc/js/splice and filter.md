
Để giải thích chi tiết hơn về việc **dịch chuyển phần tử** trong mảng và tại sao điều này "tốn thời gian", ta cần hiểu cách mảng hoạt động trong JavaScript.

---

### **1. Cách mảng hoạt động trong JavaScript**

Mảng trong JavaScript thực chất là một cấu trúc dữ liệu dạng **danh sách tuyến tính**:

- Các phần tử được lưu trữ liên tiếp trong bộ nhớ.
- Khi một phần tử bị xóa, **toàn bộ các phần tử sau nó phải dịch chuyển** để lấp đầy khoảng trống và đảm bảo tính liên tục của mảng.

```java
arr = [10, 20, 30, 40, 50];

```

#### Điều gì đã xảy ra?

1. **`30` bị xóa** tại chỉ số `2`.
2. **`40` và `50` dịch chuyển lên một vị trí**:
    - `40` từ chỉ số `3` được chuyển về chỉ số `2`.
    - `50` từ chỉ số `4` được chuyển về chỉ số `3`.
3. **Độ dài mảng (`length`) giảm từ 5 xuống 4**.

Để giải thích chi tiết hơn về việc **dịch chuyển phần tử** trong mảng và tại sao điều này "tốn thời gian", ta cần hiểu cách mảng hoạt động trong JavaScript.

---

### **1. Cách mảng hoạt động trong JavaScript**

Mảng trong JavaScript thực chất là một cấu trúc dữ liệu dạng **danh sách tuyến tính**:

- Các phần tử được lưu trữ liên tiếp trong bộ nhớ.
- Khi một phần tử bị xóa, **toàn bộ các phần tử sau nó phải dịch chuyển** để lấp đầy khoảng trống và đảm bảo tính liên tục của mảng.

#### Ví dụ:

Giả sử bạn có mảng:

javascript

Copy code

`arr = [10, 20, 30, 40, 50];`

- `arr` được lưu như thế này trong bộ nhớ:

|Index|0|1|2|3|4|
|---|---|---|---|---|---|
|Value|10|20|30|40|50|

- Khi bạn gọi:

javascript

Copy code

`arr.splice(2, 1); // Xóa phần tử tại chỉ số 2 (30)`

- Kết quả:

|Index|0|1|2|3|
|---|---|---|---|---|
|Value|10|20|40|50|

#### Điều gì đã xảy ra?

1. **`30` bị xóa** tại chỉ số `2`.
2. **`40` và `50` dịch chuyển lên một vị trí**:
    - `40` từ chỉ số `3` được chuyển về chỉ số `2`.
    - `50` từ chỉ số `4` được chuyển về chỉ số `3`.
3. **Độ dài mảng (`length`) giảm từ 5 xuống 4**.

---

### **2. Tốn thời gian như thế nào?**

#### **Khi nào dịch chuyển xảy ra?**

- Dịch chuyển xảy ra khi **một phần tử giữa hoặc đầu mảng bị xóa**. Tất cả các phần tử phía sau phần tử đó cần phải **dịch chuyển lên một vị trí**.

#### **Chi phí của dịch chuyển**

- Với mỗi lần dịch chuyển, bộ nhớ cần cập nhật vị trí của từng phần tử trong mảng. Thời gian này phụ thuộc vào:
    - **Số lượng phần tử cần dịch chuyển**.
    - **Vị trí của phần tử bị xóa**:
        - Xóa ở cuối: **Không cần dịch chuyển** (không tốn thời gian).
        - Xóa ở đầu hoặc giữa: **Cần dịch chuyển toàn bộ phần tử phía sau**.


### **Kết luận**

- **`splice` tốn thời gian hơn khi cần xóa nhiều phần tử ở giữa hoặc đầu mảng**, vì phải **dịch chuyển các phần tử phía sau** để giữ tính liên tục của mảng.
- **`filter` không tốn chi phí dịch chuyển** và là lựa chọn tối ưu hơn khi bạn cần loại bỏ phần tử khỏi mảng lớn mà không thay đổi mảng gốc.
---- 
[[dịch chuyển mảng]]
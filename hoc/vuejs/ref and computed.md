Để hiểu tại sao `ref` không cần bộ nhớ đệm (cache) nhưng `computed` thì có, chúng ta cần đi sâu vào cách chúng hoạt động và khi nào các giá trị được tính toán lại.

---

### **1. `ref` - Lưu giá trị hiện tại, không cần bộ nhớ đệm**

- **Cách hoạt động**:
    
    - `ref` chỉ lưu một giá trị, và giá trị này được cập nhật thủ công khi bạn thay đổi nó. Khi bạn truy cập vào `ref`, Vue chỉ trả về giá trị hiện tại mà bạn đã lưu.
    - Không có logic xử lý hay tính toán phức tạp trong `ref`, vì vậy mỗi lần truy cập chỉ đơn giản là đọc giá trị hiện tại.
- **Tại sao không cần cache?**
    
    - `ref` không cần tính toán lại bất kỳ giá trị nào.
    - Giá trị được lưu trực tiếp và luôn sẵn sàng để sử dụng.
    - Do đó, không cần tối ưu hóa bằng cách lưu trữ bộ nhớ đệm.
- Mỗi lần bạn truy cập `count.value`, Vue chỉ đơn giản trả về giá trị hiện tại mà bạn đã gán.

### **2. `computed` - Tính toán dựa trên phụ thuộc, cần cache**

- **Cách hoạt động**:
    
    - `computed` là một thuộc tính tính toán (calculated property). Giá trị của nó phụ thuộc vào các dữ liệu khác, như `ref` hoặc `reactive`.
    - Vue theo dõi những "phụ thuộc" này (dependencies) để quyết định khi nào cần tính lại giá trị của `computed`.
- **Tại sao cần cache?**
    
    - Nếu bạn sử dụng một giá trị `computed` nhiều lần trong cùng một chu kỳ render, mà giá trị phụ thuộc không thay đổi, thì việc tính toán lại sẽ tốn tài nguyên (CPU, thời gian).
    - Cache trong `computed` giúp lưu lại kết quả đã tính toán. Chỉ khi một trong các giá trị phụ thuộc thay đổi, Vue mới tính toán lại và cập nhật giá trị của `computed`.
```javascript
const count = ref(10);
const doubleCount = computed(() => {
  console.log("Tính toán lại doubleCount");
  return count.value * 2;
});

// Lần đầu truy cập
console.log(doubleCount.value); // Kết quả: 20, in ra "Tính toán lại doubleCount"

// Lần tiếp theo trong cùng chu kỳ
console.log(doubleCount.value); // Kết quả: 20, không in ra "Tính toán lại doubleCount"

// Thay đổi giá trị phụ thuộc
count.value = 20;

// Truy cập lại sau khi phụ thuộc thay đổi
console.log(doubleCount.value); // Kết quả: 40, in ra "Tính toán lại doubleCount"


```



### **Khi nào cache (bộ nhớ đệm) hữu ích?**

- **Hiệu năng cao hơn**:
    - Nếu một giá trị được sử dụng nhiều lần trong template hoặc logic, mà không có sự thay đổi ở dữ liệu phụ thuộc, thì cache sẽ tránh tính toán lại, giúp tăng hiệu năng.
- **Xử lý logic phức tạp**:
	    - Khi `computed` thực hiện các phép tính phức tạp hoặc đòi hỏi tài nguyên cao, bộ nhớ đệm giúp giảm công việc lặp lại.

### So sánh `ref` và `computed`

| **Đặc điểm**              | **`ref`**                                       | **`computed`**                                |
|---------------------------|-------------------------------------------------|----------------------------------------------|
| **Chứa giá trị tĩnh/lưu trữ** | Chứa giá trị trực tiếp, không tính toán lại.    | Giá trị được tính toán dựa trên các phụ thuộc. |
| **Thay đổi giá trị**       | Thay đổi thủ công (gán giá trị mới).             | Tự động tính lại khi phụ thuộc thay đổi.      |
| **Caching (Bộ nhớ đệm)**   | Không cần, vì giá trị luôn có sẵn.                | Cần, để tránh tính toán lại không cần thiết.  |

```javascript
const items = ref([1, 2, 3, 4, 5]);
const total = computed(() => {
  console.log("Tính toán lại tổng");
  return items.value.reduce((sum, item) => sum + item, 0);
});

// Truy cập nhiều lần mà không thay đổi dữ liệu
console.log(total.value); // 15, in ra "Tính toán lại tổng"
console.log(total.value); // 15, không in ra "Tính toán lại tổng"

// Thay đổi danh sách
items.value.push(6);

// Truy cập lại sau khi thay đổi
console.log(total.value); // 21, in ra "Tính toán lại tổng"

```


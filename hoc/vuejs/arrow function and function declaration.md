

Cách viết `export function filterProducts(category) {}` và cách viết `const filterProducts = (category) => {}` có một số điểm khác biệt cơ bản liên quan đến cú pháp và hành vi trong JavaScript. Dưới đây là sự khác biệt chính:

### **1. Khác biệt cú pháp**

#### **Cách 1:**

```js
export function filterProducts(category) {
  // logic ở đây
}

```

- Đây là **function declaration** (khai báo hàm).
- Hàm này có tên rõ ràng (`filterProducts`) và được [[hoisted]] (tức là bạn có thể gọi hàm này trước khi nó được định nghĩa trong code).

## cách 2:
```js
export const filterProducts = (category) => {
  // logic ở đây
};

```

- Đây là **arrow function** gán cho một biến.
- Không được [[hoisted]], nghĩa là bạn **không thể gọi hàm này trước khi khai báo**.
- Arrow function sử dụng cú pháp ngắn gọn và không có từ khóa `f`

### **2. Hoisting (kéo lên đầu)**

- **Function declaration** được [[hoisted]] (nâng lên đầu file) trong phạm vi của nó:

```js
console.log(filterProducts('tatCa')); // Sẽ hoạt động
export function filterProducts(category) {
  // logic
}

```

**Arrow function** không được hoisted:

```js
	console.log(filterProducts('tatCa')); // Báo lỗi: filterProducts is not defined
export const filterProducts = (category) => {
  // logic
};

```

### **3. Context (`this`)**

#### **Arrow Function:**

- **Arrow function** không có binding riêng cho từ khóa `this`. Nó lấy `this` từ ngữ cảnh bao quanh nơi hàm được khai báo (lexical scoping).
- Thích hợp hơn cho các callback hoặc khi bạn muốn tránh lỗi `this` bị thay đổi.

#### **Function Declaration:**

- **Function declaration** tự tạo binding riêng cho từ khóa `this`, dựa trên cách hàm được gọi (dynamic scoping).
- Thích hợp hơn khi bạn muốn kiểm soát ngữ cảnh của `this`.

Ví dụ:

```js
export const filterProducts = (category) => {
  console.log(this); // 'this' ở đây là ngữ cảnh bao quanh (không phải đối tượng gọi hàm).
};

export function filterProducts(category) {
  console.log(this); // 'this' phụ thuộc vào cách hàm được gọi (ví dụ: obj.filterProducts() -> 'this' là obj).
}

```

### **4. Sử dụng với `export`**

Cả hai cách đều hợp lệ với `export`. Tuy nhiên:

- `export function filterProducts` là **export trực tiếp**.
- `export const filterProducts = () => {}` là **export gián tiếp** qua biến.

---

### **Khi nào chọn cách nào?**

- **Dùng function declaration:**
    
    - Khi bạn cần hoisting hoặc muốn tạo hàm có tên rõ ràng.
    - Khi bạn cần một hàm có binding riêng cho `this`.
- **Dùng arrow function:**
    
    - Khi bạn không cần hoisting.
    - Khi bạn cần cú pháp gọn hơn, hoặc muốn `this` lấy từ ngữ cảnh bao quanh.
    - Khi bạn dùng hàm như callback.

---

### **Kết luận**

Cả hai cách đều đúng và có thể sử dụng tùy theo mục đích. Nếu hàm của bạn không phụ thuộc vào `this` và bạn thích cú pháp ngắn gọn hơn, hãy dùng **arrow function**. Nếu bạn cần hoisting hoặc kiểm soát `this`, hãy chọn **function declaration**.

xem thêm về [[hoisted]]
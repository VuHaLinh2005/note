
Đúng vậy! Trong JavaScript:

### **1. Hàm khai báo (Function Declaration)**:

Hàm khai báo (dùng `function`) **được hoisted**, nghĩa là bạn có thể gọi hàm trước khi nó được khai báo trong mã của bạn.

#### **Ví dụ:**


```js
console.log(sum(2, 3)); // Kết quả: 5

function sum(a, b) {
  return a + b;
}

```

Ở đây, `function sum` được "**nâng lên đầu**" bởi JavaScript trong quá trình biên dịch, nên bạn có thể gọi nó trước dòng khai báo.

### **2. Hàm mũi tên (Arrow Function) hoặc Hàm gán vào biến (Function Expression)**:

Hàm mũi tên hoặc hàm được gán vào biến **không được hoisted**. Bạn chỉ có thể sử dụng chúng sau khi chúng được định nghĩa.

#### **Ví dụ với Arrow Function:**


```js
console.log(sum(2, 3)); // Báo lỗi: Cannot access 'sum' before initialization

const sum = (a, b) => {
  return a + b;
};

```

Ở đây, `const sum` **chưa được khởi tạo** khi dòng `console.log(sum(2, 3));` chạy, nên JavaScript sẽ báo lỗi.

```js
console.log(sum(2, 3)); // Báo lỗi: Cannot access 'sum' before initialization

const sum = function (a, b) {
  return a + b;
};

```

### **Tại sao lại như vậy?**

- **Function Declaration**:
    
    - Được hoisted bởi vì chúng được xử lý trong quá trình biên dịch (compilation phase), và bản thân hàm này được **định nghĩa đầy đủ** trước khi mã được thực thi.
- **Arrow Function/Function Expression**:
    
    - Gán vào biến (dùng `const`, `let`, hoặc `var`), và các biến đó chỉ được khởi tạo **tại thời điểm thực thi**. Trước thời điểm đó, biến này chưa tồn tại (hoặc trong trường hợp `var`, nó tồn tại với giá trị `undefined`).

---

### **Khi nào dùng cái nào?**

- **Function Declaration:**
    
    - Dùng khi bạn cần hoisted (hàm gọi được trước khi định nghĩa).
    - Ví dụ trong các tình huống khai báo các hàm toàn cục.
- **Arrow Function/Function Expression:**
    
    - Dùng khi bạn muốn kiểm soát rõ ràng thứ tự thực thi.
    - Phù hợp khi bạn gán hàm làm một giá trị, callback, hoặc khi muốn đảm bảo `this` trong hàm không bị thay đổi.


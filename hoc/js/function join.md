

```js
if (err.length > 0) {
  err.join('\n');  // Kết quả của join không được sử dụng
  alert(err);  // Hiển thị mảng lỗi ban đầu, không có dấu xuống dòng
  return true;
}

```

```js
let arr = ['a', 'b', 'c'];
let result = arr.join('-');
console.log(result);  // Kết quả: "a-b-c"
console.log(arr);     // Mảng ban đầu vẫn là: ["a", "b", "c"]

```
Như bạn thấy, `join()` không làm thay đổi mảng ban đầu mà trả về **một chuỗi mới**. Vì vậy, nếu bạn không gán kết quả của `join()` vào một biến, kết quả sẽ không được sử dụng trong chương trình.


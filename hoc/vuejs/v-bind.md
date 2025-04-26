#v-bind



Trong Vue.js, `v-bind` là một chỉ thị đặc biệt được sử dụng để "ràng buộc" các thuộc tính của phần tử HTML với dữ liệu trong Vue instance. Cách viết tắt của `v-bind` là dấu hai chấm `:`.

### Cách sử dụng `v-bind` (hoặc `:`)

#### 1. Ràng buộc các thuộc tính của HTML

`v-bind` giúp chúng ta liên kết động một thuộc tính của phần tử HTML với một giá trị trong dữ liệu của Vue. Điều này rất hữu ích khi chúng ta muốn hiển thị dữ liệu động hoặc khi thuộc tính của phần tử phụ thuộc vào một biến.

```html
<img v-bind:src="imageUrl" alt="Dynamic Image"> <!-- Hoặc cách viết tắt --> <img :src="imageUrl" alt="Dynamic Image">
```

Ở đây, thuộc tính `src` sẽ nhận giá trị từ `imageUrl`, và nếu `imageUrl` thay đổi, thì `src` cũng sẽ **tự động cập nhật theo.**
- : là **cách viết gọn hơn** 




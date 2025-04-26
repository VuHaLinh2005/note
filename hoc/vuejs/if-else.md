#condition


Đúng rồi! Khi dùng `v-if` và `v-else`, Vue sẽ coi chúng là một chuỗi điều kiện liên kết với nhau, tức là nó chỉ render một trong các thẻ dựa trên điều kiện mà thôi. Do đó, nếu bạn chèn một thẻ HTML khác vào giữa `v-if` và `v-else`, Vue sẽ gặp lỗi vì chuỗi điều kiện `v-if` và `v-else` sẽ bị ngắt quãng, không còn liền mạch nữa.

```html
<p v-if="isLogin">xin chao nguoi dung</p>
<div>Thẻ này làm gián đoạn chuỗi điều kiện</div> 
<p v-else>nguoi dung da dang xuat hehe</p>
```
 chỉ render 1 dk trong DOM


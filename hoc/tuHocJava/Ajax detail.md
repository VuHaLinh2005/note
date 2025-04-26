
## 1. AJAX - Sức mạnh đằng sau không reload

AJAX là viết tắt của **Asynchronous JavaScript and XML**, nhưng giờ đây nó không chỉ giới hạn ở XML mà thường dùng với JSON, text, v.v.(**[[Bất đồng bộ và đồng bộ | Asynchronous]]**)

**Cách hoạt động:**

* Bạn gửi yêu cầu HTTP (như `POST` tới `/api/add-product-to-cart`) bằng JavaScript (thường qua **jQuery** hoặc **fetch**).
* Server xử lý (ví dụ: thêm sản phẩm, tính tổng) và trả về dữ liệu (như `"5"`).
* JavaScript nhận dữ liệu qua callback (`success`) mà không làm gián đoạn trang web.

**Trong mã của bạn:**

```javascript
url: `${window.location.origin}/api/add-product-to-cart`,
type: "POST",
data: JSON.stringify({ quantity: 1, productId: productId }),
success: function (response) { ... }
```

Yêu cầu chạy "ngầm" (**asynchronous**), giao diện vẫn hoạt động bình thường, không reload.


## 2. DOM - Bộ não giao diện

DOM (**Document Object Model**) là ~={red}**cách**=~ trình duyệt biểu diễn trang **web** dưới dạng một **~={red}cây=~** đối tượng mà **~={red}JavaScript=~** có thể **~={red}thao túng.=~**

**Ví dụ HTML:**

```html
<span id="sumCart">0</span>
```

Trong DOM, `<span>` là một "nút" (~={red}**node**=~), và **~={red}JavaScript=~** có thể **~={red}thay đổi=~** nó.

`$("#sumCart")`:

* Đây là cú pháp jQuery, chọn phần tử có `id="sumCart"`.
* Tương đương vanilla JS: `document.getElementById("sumCart")`.

`.text(sum)`:

* Thay đổi nội dung text của phần tử thành `sum` (ví dụ 5).
* Tương đương vanilla JS: `document.getElementById("sumCart").innerText = sum`.

**Đào sâu:** Nếu muốn thay đổi HTML (không chỉ text), dùng `.html()`:

```javascript
$("#sumCart").html("<strong>5</strong>"); // Hiển thị số 5 in đậm
```

## 3. Tại sao không reload?

**Bình thường, khi submit form hoặc click link:**

* Trình duyệt gửi yêu cầu → server trả về HTML mới.
* Trang tải lại toàn bộ DOM → giao diện "nháy" một cái.

**Với AJAX:**

* JavaScript gửi yêu cầu qua `XMLHttpRequest` (hoặc `fetch`).
* Server chỉ trả dữ liệu nhỏ (như `"5"`) → **~={red}JS cập nhật DOM=~** cục bộ.
* Chỉ phần tử `#sumCart` thay đổi, còn lại giữ nguyên → không reload.

**Đào sâu:** Bạn có thể kiểm tra quá trình này trong tab "Network" của DevTools (F12). Tìm request tới `/api/add-product-to-cart`, xem response là gì!

## 4. Ứng dụng thực tế

* **Giỏ hàng:** Cập nhật số lượng, tổng tiền mà không reload.
* **Tìm kiếm gợi ý:** Gõ từ khóa → danh sách gợi ý hiện ra ngay (như Google Search).
* **Chat:** Tin nhắn mới hiện lên mà không cần refresh.

**Ví dụ nâng cao:**

```javascript
$.ajax({
    url: "/api/cart",
    type: "POST",
    data: JSON.stringify({ productId: "123" }),
    success: function (response) {
        $("#sumCart").text(response.sum);           // Cập nhật số lượng
        $("#totalPrice").text(response.total);      // Cập nhật tổng tiền
        $("#cartItems").append(`<li>${response.itemName}</li>`); // Thêm sản phẩm vào danh sách
    }
});
```

Server trả về JSON: `{ "sum": 5, "total": 150000, "itemName": "Áo thun" }`.

## 5. Đi xa hơn: Vanilla JS

Nếu không dùng jQuery, bạn có thể viết bằng `fetch` (cách hiện đại):

```javascript
fetch("/api/add-product-to-cart", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ quantity: 1, productId: "123" })
})
.then(response => response.json()) // Chuyển response thành JSON
.then(data => {
    document.getElementById("sumCart").innerText = data.sum;
    alert("Thêm thành công!");
});
```

**Chốt**

`$("#sumCart").text(sum)` là "đỉnh cao" của sự kết hợp giữa AJAX (lấy dữ liệu không reload) và DOM (cập nhật giao diện).

**Muốn đào sâu hơn nữa, bạn có thể tìm hiểu:**

* Event delegation: Xử lý sự kiện động.
* WebSocket: Cập nhật realtime (như chat).
* SPA (Single Page Application): Toàn bộ trang không reload (React, Vue).


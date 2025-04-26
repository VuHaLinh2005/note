
### 1. **AJAX là gì?**

- AJAX là một **~={red}kỹ thuật=~** trong **~={red}JavaScript=~**, sử dụng đối tượng XMLHttpRequest (hoặc **~={red}Fetch API=~** ngày nay) để **~={blue}gửi/nhận**=~ dữ liệu từ server bất đồng bộ.**[[Bất đồng bộ và đồng bộ | xem thêm bất đồng bộ và đồng bộ]]**
- Nó là tính năng có sẵn trong JavaScript, không cần thư viện nào để dùng.
- **[[Ajax detail | xem thêm ajax detail]]**

Ví dụ AJAX thuần (không jQuery):

```js
let xhr = new XMLHttpRequest();
xhr.open("GET", "/api/data", true);
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log(xhr.responseText);
    }
};
xhr.send();
```

### 2. **jQuery là gì?**

- jQuery là một thư viện JavaScript giúp **~={red}đơn giản hóa=~** các thao tác phức tạp như:
    - Truy cập và chỉnh sửa DOM.
    - Xử lý sự kiện.
    - Gửi yêu cầu AJAX.
- jQuery không phải là AJAX, mà là công cụ "bao bọc" AJAX để dễ dùng hơn.
- tóm lại để viết **~={red}code ngắn hơn.=~**


### 3. **Mối liên hệ giữa jQuery và AJAX**

- **AJAX thuần**: Là cách gốc của JavaScript, nhưng code dài dòng, khó viết, và dễ lỗi (phải xử lý thủ công nhiều thứ như header, lỗi, định dạng dữ liệu).
- **jQuery + AJAX**: jQuery cung cấp hàm $.ajax() (và các shortcut như $.get(), $.post()) để làm AJAX đơn giản, dễ đọc, và hỗ trợ nhiều tính năng sẵn có.

```js
let xhr = new XMLHttpRequest();
xhr.open("POST", "/api/add", true);
xhr.setRequestHeader("Content-Type", "application/json");
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log("Thành công:", xhr.responseText);
    } else {
        console.log("Lỗi:", xhr.status);
    }
};
xhr.send(JSON.stringify({ id: 1 }));

```

**jQuery AJAX** (tương tự):

```js
$.ajax({
    url: "/api/add",
    type: "POST",
    data: JSON.stringify({ id: 1 }),
    contentType: "application/json",
    success: function(response) {
        console.log("Thành công:", response);
    },
    error: function(err) {
        console.log("Lỗi:", err);
    }
});
```

### 4. **Tại sao cần jQuery khi đã có AJAX?**

- **Đơn giản hóa**: jQuery giúp viết ít code hơn, dễ đọc hơn (so sánh ví dụ trên).
- **Tính tương thích**: jQuery xử lý sự khác biệt giữa các trình duyệt (trước đây AJAX thuần gặp vấn đề tương thích).
- **Tích hợp sẵn**: jQuery cung cấp các tiện ích như xử lý JSON, thêm header, hiển thị loading, retry dễ dàng.
- **Kết hợp DOM**: Dễ dàng thao tác DOM ngay sau khi nhận dữ liệu (như trong code của bạn: $("#sumCart").text(sum)).

### 6. **Kết luận ngắn gọn**

- **Không cần jQuery cũng làm được AJAX**, nhưng sẽ **~={red}phức tạp=~** và mất thời gian hơn.
- **jQuery + AJAX**: **~={red}Nhanh, gọn,=~** dễ, tích hợp tốt với giao diện
.
### 1. **"Bất đồng bộ" nghĩa là gì?**

- **Đồng bộ**: Mọi thứ diễn ra theo **~={red}thứ tự=~**, phải chờ xong việc này mới làm việc kia. Ví dụ: Bạn gọi món ăn ở quán, phải đợi món tới bàn rồi mới ăn.
- **Bất đồng bộ**: Không cần chờ, **~={red}làm việc khác=~** **trong lúc đợi**. Ví dụ: Bạn gọi món, trong lúc đợi thì lướt điện thoại, món đến thì quay lại ăn.

Trong lập trình:

- **Đồng bộ**: Gửi yêu cầu đến server, ngồi **~={red}đợi=~** phản hồi xong mới **~={red}làm tiếp=~**.
- **Bất đồng bộ**: Gửi yêu cầu, không đợi, tiếp tục **~={red}chạy code khác=~**, khi server **trả lời thì xử lý.**

---

### 2. **"Nhận dữ liệu từ server bất đồng bộ" là gì?**

- Nghĩa là: Bạn gửi yêu cầu lấy dữ liệu từ server (như danh sách sản phẩm), nhưng không dừng chương trình để đợi. Code vẫn chạy bình thường, khi **~={red}server trả lời=~** thì bạn **~={red}mới xử lý=~** dữ liệu.

---

### 3. **Ví dụ đơn giản để hiểu ngay**

#### Tình huống: Lấy số lượng tin nhắn mới từ server

- **Cách đồng bộ (truyền thống)**:
    - Bạn nhấn nút "Kiểm tra tin nhắn".
    - Trang web bị "đơ" (đợi server), sau 2 giây mới hiện số tin nhắn (ví dụ: "5 tin nhắn mới").
    - Trong 2 giây đó, bạn không làm được gì.
- **Cách bất đồng bộ (dùng AJAX)**:
    - Bạn nhấn nút "Kiểm tra tin nhắn".
    - Trang web vẫn hoạt động bình thường (bạn có thể cuộn trang, nhấn nút khác).
    - Sau 2 giây, server trả về "5 tin nhắn mới", số này tự động hiện lên mà không reload trang.

#### Code ví dụ (dùng jQuery AJAX):


```js
console.log("Bắt đầu kiểm tra..."); // Chạy ngay

$.ajax({
    url: "/api/messages", // Gửi yêu cầu đến server
    type: "GET",
    success: function(data) {
        console.log("Tin nhắn mới: " + data); // **Chạy khi server trả lời**
    }
});

console.log("Đang đợi, nhưng vẫn làm việc khác..."); // Chạy ngay, không đợi
```

**Kết quả in ra console**:

```text
Bắt đầu kiểm tra...
Đang đợi, nhưng vẫn làm việc khác...
(2 giây sau) Tin nhắn mới: 5
```
**Giải thích**:

- "Bắt đầu kiểm tra..." và "Đang đợi..." in ra ngay lập tức.
- Trong lúc đợi server (2 giây), code không bị dừng.
- Khi server trả về số "5", success mới chạy.
### 4. **Đơn giản nhất**

- "Bất đồng bộ" = **Gửi yêu cầu rồi quên nó đi**, làm việc khác, khi server trả lời thì quay lại xử lý.
- Ví dụ đời thực: Bạn nhắn tin hỏi bạn "Mấy giờ gặp?", trong lúc đợi trả lời, bạn vẫn làm việc khác, khi bạn nhắn lại thì bạn đọc.
### 5. **Tại sao quan trọng?**

- Không bất đồng bộ: Trang web bị "**~={blue}treo=~**" khi đợi server, trải nghiệm người dùng tệ.
- Có bất đồng bộ: Trang mượt mà, người dùng **~={red}không phải chờ=~**.
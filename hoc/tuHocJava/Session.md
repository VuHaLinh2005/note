### bản chất : 
  mỗi **request** về cơ bản là **độc lập** và **không "nhớ**" gì về các request trước đó. Session giúp "~={red}nhớ=~" ~={red}thông tin=~ người dùng trong suốt ~={red}phiên=~ ~={red}làm việc=~ .
   **Session là cách để các lập trình viên lưu lại những giữ liệu của người dùng khi người dùng khi sử dụng website.**

## chi tiết 
Đúng vậy, mã session (session ID) được lưu trữ trong cookie và được sử dụng để **server** xác định và truy xuất đúng **session** **data** tương ứng với người dùng. Hãy tưởng tượng như sau:

1. **Server tạo session:** Khi người dùng truy cập website, server tạo một session cho người dùng đó.  **Session** này là một **vùng** **lưu** trữ dữ liệu trên **server**, **dành** **riêng** cho **user**  .

2. **Server tạo session ID:**  Server tạo một mã session (session ID) duy nhất để xác định session vừa tạo.

3. **Server gửi session ID cho client (thông qua cookie):** Server tạo một cookie chứa session ID và gửi nó đến trình duyệt của người dùng.  **Trình** **duyệt** sẽ **lưu** trữ **cookie** này.

4. **Client gửi session ID trong mỗi request:** Mỗi khi trình duyệt gửi request đến server, nó sẽ tự động gửi kèm cookie chứa session ID.

5. **Server sử dụng session ID để lấy session data:**  Server nhận được request và đọc session ID từ cookie.  Server sử dụng session ID này để tìm và lấy session data tương ứng được lưu trữ trên server.

**Tóm lại:**

* Mã session (**session ID**)   như một "chìa **khóa**" để **server** **tìm** đúng "**ổ** khóa" .
* **Cookie** được sử dụng để **lưu** trữ và truyền **session ID** giữa client và server.
* **Dữ liệu** thực sự của **session** được lưu trữ trên **server**.
* nếu **cookie mất** : thì **session id mất** (chìa khoá mở session data mất.)


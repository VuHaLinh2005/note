Lỗi này xuất hiện vì GitHub đã ngừng hỗ trợ xác thực bằng mật khẩu qua HTTPS.  Bạn cần sử dụng một phương thức xác thực khác để clone repository. Dưới đây là hai giải pháp phổ biến:
git remote add origin https://github.com/VuHaLinh2005/java-spring-mvc-by-hoidanit.git
git remote set-url origin https://github.com/VuHaLinh2005/java-spring-mvc-by-hoidanit.git (use khi forder là do clone từ git của ng khác ,và h là push lên git mik)
1. **Tạo SSH key (nếu bạn chưa có):**  Mở terminal và gõ lệnh `ssh-keygen -t ed25519 -C "your_email@example.com"`. Thay `your_email@example.com` bằng email bạn dùng cho GitHub.  Nếu bạn không có `ed25519`, dùng `rsa` cũng được: `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`.  Ấn Enter cho các câu hỏi mặc định (hoặc chọn đường dẫn và passphrase nếu muốn).

2. **Sao chép SSH key:**  Mở file `~/.ssh/id_ed25519.pub` (hoặc `~/.ssh/id_rsa.pub` nếu bạn dùng rsa) bằng trình soạn thảo văn bản và sao chép toàn bộ nội dung.

3. **Thêm SSH key vào GitHub:**
    * Đăng nhập vào GitHub.
    * Click vào ảnh đại diện ở góc trên bên phải, chọn "Settings".
    * Ở menu bên trái, chọn "SSH and GPG keys".
    * Click nút "New SSH key".
    * Ở mục "Title", đặt tên cho key (ví dụ: "My Laptop").
    * Dán key bạn đã sao chép vào mục "Key".
    * Click "Add SSH key".

* **Clone bằng SSH:** Sử dụng URL SSH để clone repository:

```bash
git clone git@github.com:Linh-kingdom/linhGitHub.git
```

**2. Sử dụng Personal Access Token (PAT):**

Đây là cách thay thế nếu bạn không muốn sử dụng SSH.

* **Tạo PAT:**  Tạo một PAT trong cài đặt tài khoản GitHub của bạn (Settings -> Developer settings -> Personal access tokens -> Generate new token).  Đảm bảo cấp quyền "repo" cho token.
* **Clone bằng HTTPS và PAT:**  Sử dụng URL HTTPS và nhập PAT khi được yêu cầu:

```bash
git clone https://<your_github_username>:<your_pat>@github.com/Linh-kingdom/linhGitHub.git
```


**Lưu ý:**

*  Không nên commit PAT vào repository.  Nếu bạn đã lỡ commit PAT, hãy revoke (hủy) nó ngay lập tức trong cài đặt GitHub.
*  Cách sử dụng SSH an toàn và tiện lợi hơn, bạn không cần phải nhập mật khẩu hoặc PAT mỗi lần clone hoặc push code.


Sau khi thực hiện một trong hai cách trên, bạn sẽ có thể clone repository thành công.



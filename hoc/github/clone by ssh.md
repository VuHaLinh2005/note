 

### 1. **Kiểm tra SSH Key trên máy**

Chạy lệnh sau để kiểm tra xem bạn đã tạo SSH key hay chưa:

```bash
ls ~/.ssh
```

Nếu thấy các file như `id_rsa` và `id_rsa.pub`, nghĩa là SSH key đã tồn tại. Nếu không, bạn cần tạo SSH key mới:

```bash
ssh-keygen -t rsa -b 4096 -C "linhvhph48570@gmail.com"
```

- Nhấn **Enter** để lưu key ở vị trí mặc định (`~/.ssh/id_rsa`).
    
- Bạn có thể để trống **passphrase** (hoặc nhập nếu muốn bảo mật hơn).
    

---

### 2. **Thêm SSH Key vào SSH Agent**

Sau khi tạo SSH key, chạy lệnh sau để đảm bảo SSH agent đang chạy và thêm key vào:

```bash
eval "$(ssh-agent -s)"  # Khởi động SSH Agent
ssh-add ~/.ssh/id_rsa   # Thêm SSH key
```

---

### 3. **Thêm SSH Key vào GitHub**

1. Lấy nội dung của file `id_rsa.pub` (SSH public key):
    
    ```bash
    cat ~/.ssh/id_rsa.pub
    ```
    
2. Sao chép toàn bộ nội dung hiện ra.
    
3. Truy cập GitHub:
    
    - Đăng nhập vào tài khoản GitHub của bạn.
        
    - Vào **Settings** > **SSH and GPG Keys** > **New SSH Key**.
        
    - Dán nội dung bạn vừa sao chép vào và đặt tên (ví dụ: "Laptop Linh").
        
    - Nhấn **Add SSH Key**.
        

---

### 4. **Kiểm tra kết nối với GitHub**

Kiểm tra xem SSH đã hoạt động đúng chưa bằng lệnh:

```bash
ssh -T git@github.com
```

Nếu thành công, bạn sẽ thấy thông báo:

```
Hi VuHaLinh2005! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### 5. **Clone lại repository**

Sau khi hoàn thành các bước trên, thử lại lệnh:

```bash
git clone git@github.com:VuHaLinh2005/note.git
```

Nếu vẫn gặp lỗi, kiểm tra:

- Repository có tồn tại không.
    
- Tài khoản GitHub của bạn có quyền truy cập không (ví dụ: private repository cần quyền cụ thể).
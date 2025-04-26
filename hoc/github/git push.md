 


## Push forder/file create from github

1. create repository from git
2. clone về
3. git status
4. git add .
5. git commit - m"lý do"
6. git push -u origin main (main có thể thay = nhánh khác) 

## push forder/file create from local
 
**1. Tạo một kho lưu trữ *mới*:**

```bash
echo "# demo_push_from_local" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Linh-kingdom/demo_push_from_local.git
git push -u origin main
```

Chuỗi lệnh này được sử dụng khi bạn có một dự án ***hoàn toàn mới***  **chưa** được Git **theo dõi**. Nó khởi tạo một kho lưu trữ Git, tạo một commit ban đầu, đặt nhánh chính (main branch), kết nối đến kho lưu trữ từ xa và đẩy các thay đổi lên.

**2. Đẩy một kho lưu trữ *đã tồn tại*:**

```bash
git remote add origin git@github.com:Linh-kingdom/demo_push_from_local.git
git branch -M main
git push -u origin main
```

 -  giả sử đã làm ít nhất 1 lần.

### when push conflict
1. pull về đã.
2. xoá trong code.
3. push lại .

##  cause conflict by : 
Git *có thể* tự động merge trong nhiều trường hợp, cụ thể là khi các thay đổi xảy ra ở những phần **hoàn toàn tách biệt** của file.  Ví dụ, nếu một người sửa phần **đầu** file, người khác sửa phần **cuối** file, Git có thể dễ dàng **ghép** hai phần này lại mà không gặp vấn đề gì.

Tuy nhiên, khi các thay đổi **chồng chéo** lên nhau, Git không thể tự quyết định nên **giữ phiên bản** nào.  Lý do là vì Git được thiết kế để bảo toàn mọi thay đổi, và việc tự động chọn một phiên bản sẽ đồng nghĩa với việc mất đi thay đổi của người khác.  Trong trường hợp này, Git cần sự can thiệp của con người để quyết định cách merge.

Hãy tưởng tượng hai họa sĩ cùng vẽ trên một bức tranh. Nếu họ vẽ ở hai góc khác nhau, ta có thể dễ dàng ghép hai phần tranh lại. Nhưng nếu họ cùng vẽ lên cùng một khu vực, ta cần phải quyết định giữ lại nét vẽ của ai, hoặc kết hợp chúng lại như thế nào. Git cũng tương tự như vậy.

 -> ví dụ : a và b cùng sửa chung 1 dòng  a push trc, b push sau sẽ lỗi , vì phiên bản local của b đang thấp hơn(đã có thay đổi từ người khác , nếu chọn b thì người khác mất) nên b phải pull về , gỡ conflict . 

## Đẩy thư mục từ local lên git 


1. **`git init`**  
    👉 Khởi tạo Git trong thư mục để Git quản lý code.
    
2. **`git remote add origin <URL>`**  
    👉 Kết nối repo cục bộ với repo trên GitHub (remote repo).
    
3. **`git add .`**  
    👉 Thêm tất cả file vào danh sách chờ commit.
    
4. **`git commit -m "Initial commit"`**  
    👉 Ghi lại trạng thái file với lời nhắn (commit message).
    
5. **`git push -u origin main`**  
    👉 Đẩy code từ máy lên GitHub.

## chi tiết đẩy thư mục từ local lên git
### **1. `git init` - Tại sao?**

- **Giải thích:**  
    Khi bạn khởi tạo Git bằng `git init`, thư mục của bạn sẽ trở thành một **repo Git cục bộ**. Git sẽ theo dõi các thay đổi của file trong thư mục này.
- **Ý nghĩa:**  
    Đây là bước đầu tiên để Git biết nó cần quản lý nội dung gì.

---

### **2. `git remote add origin <URL>` - Tại sao?**

- **Giải thích:**  
    Remote là một repo trên máy chủ (GitHub). Khi bạn thêm `origin`, bạn nói với Git rằng:  
    _"Hãy kết nối repo cục bộ này với repo trên GitHub tại địa chỉ `<URL>`."_
- **Ý nghĩa:**  
    Để Git biết nơi bạn sẽ đẩy (push) code lên sau này.

---

### Các bước tiếp theo như `git add`, `git commit`, và `git push` dễ hiểu hơn:

- **`git add .`:** Chọn các file để đưa vào quản lý thay đổi.
- **`git commit`:** Lưu lại trạng thái hiện tại của code (như chụp ảnh).
- **`git push`:** Gửi ảnh chụp (commit) đó lên GitHub.

Nếu vẫn chưa rõ chỗ nào, mình sẽ giải thích thêm nhé! 😊




 

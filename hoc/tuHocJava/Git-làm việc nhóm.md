### 1. Tại sao lại xảy ra ~={red}lỗi=~ xung đột khi bạn và bạn của bạn cùng ~={red}commit=~?

**Nguyên nhân:**

- Xung đột xảy ra khi **cả bạn và bạn của bạn cùng chỉnh sửa cùng một phần của một file** (ví dụ: cùng một dòng code) và sau đó cả hai đều cố gắng **commit** (lưu thay đổi) lên kho lưu trữ chung (repository).
- Git không biết phải **~={red}giữ=~** thay đổi của **~={red}bạn=~** hay của **~={red}bạn ấy=~**, nên nó báo lỗi xung đột và yêu cầu bạn giải quyết **~={red}thủ công=~**.

**~={red}Cách xử lý:=~**

1. git pull origin main: Lấy code mới về (sẽ thấy conflict).
2. Mở file xung đột, Git đánh dấu:

```txt
<<<<<<< HEAD
console.log("Hello world");  // Code của bạn
=======
console.log("Hi team");      // Code của bạn bạn
>>>>>>> branch-name
```
- **~={red}Sửa tay=~** (**chọn** hoặc **gộp**): console.log("Hi team and world");.
- git add index.js, git commit, rồi git push.
**~={red}Mẹo tránh**:=~

- **~={red}Pull thường xuyên=~** trước khi code.
- Làm trên **nhánh** riêng, chỉ **merge** khi ổn
-  **Phân chia công việc:** Bạn và bạn của bạn nên làm việc trên **các phần khác nhau** của dự án (ví dụ: bạn làm frontend, bạn ấy làm backend) hoặc trên **các file khác nhau**.
---

### 2. Tận dụng hết sức mạnh của Git: Cần làm gì?
**[[Git Branch |xem thêm git branch]]**
[[Cách lấy code mới nhất sang nhánh phụ ]]
#### a. Sử dụng nhánh (**~={red}branch=~**)

- **Nhánh là gì?** Nhánh giống như một “**~={red}bản sao=~**” của dự án, cho phép bạn làm việc độc lập mà không ảnh hưởng đến nhánh chính (thường là main hoặc master).
- **Tại sao dùng nhánh?**
    - Mỗi người có thể làm việc trên nhánh riêng, tránh đụng độ.
    - Khi xong, bạn hợp nhất (**~={red}merge=~**) nhánh của mình vào nhánh chính mà không làm rối code của người khác.
- **Cách tạo và dùng nhánh:**
    1. Tạo nhánh mới: **~={red}git branch ten-nhanh=~** (thay ten-nhanh bằng tên bạn muốn, ví dụ: frontend).
    2. Chuyển sang nhánh đó: **~={red}git checkout ten-nhanh=~**.
    3. Làm việc bình thường, commit thay đổi bằng git add . và git commit -m "Thông điệp".
    4. Khi xong, quay lại nhánh chính và hợp nhất:
```txt
git checkout main
git merge ten-nhanh
```

- 1. Nếu có xung đột, sửa như phần trên, rồi đẩy lên repository chung: git push.

#### b. ~={red}Thường xuyên pull và push=~

- **Pull:** Dùng git pull để cập nhật thay đổi từ repository chung về máy bạn trước khi làm việc.
- **Push:** Dùng git push để gửi thay đổi của bạn lên repository chung sau khi commit.
- Làm vậy giúp bạn luôn đồng bộ với nhóm và giảm xung đột.

#### c. ~={red}Commit thường xuyên=~

- Sau mỗi phần nhỏ công việc (ví dụ: xong một hàm, một giao diện), hãy commit bằng git commit -m "Mô tả ngắn gọn". Điều này giúp dễ theo dõi và quay lại nếu cần.

---

### 4. Các bước làm việc nhóm hiệu quả với Git

1. **Phân công rõ ràng:** Mỗi người làm việc trên phần riêng hoặc nhánh riêng.
2. **Tạo nhánh:** Dùng git branch ten-nhanh và git checkout ten-nhanh để bắt đầu.
3. **Pull trước khi làm:** git pull để lấy code mới nhất.
4. **Commit thường xuyên:** Lưu thay đổi sau mỗi bước nhỏ.
5. **Merge nhánh:** Khi xong, hợp nhất nhánh của bạn vào main bằng git merge.
6. **Push lên chung:** Sau khi merge, dùng git push để chia sẻ với nhóm.

---

### 5. Ví dụ thực tế

- Bạn làm giao diện, tạo nhánh frontend: git branch frontend rồi git checkout frontend.
- Bạn của bạn làm backend, tạo nhánh backend.
- Cả hai làm việc trên nhánh riêng, commit thường xuyên.
- Khi **~={red}xong=~**, bạn **~={red}merge=~** nhánh frontend vào main, bạn ấy merge nhánh backend vào main.
- Nếu có xung đột, mở file và sửa như hướng dẫn ở trên.

---
### Quy trình làm việc nhóm chuẩn

1. Tạo nhánh: git checkout -b ten-nhanh.
2. Code, commit: **~={red}git add .=~** rồi git **commit -m "Xong tính năng X".**
3. Pull trước khi push: **~={red}git pull origin main.=~**
4. Push nhánh: **~={red}git push origin ten-nhanh.=~**
5. Tạo Pull Request (PR) trên GitHub để team review, rồi merge vào main.





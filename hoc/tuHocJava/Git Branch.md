 
#### Bước 1: Đảm bảo nhánh chính (main) cập nhật
- Vào repo của bạn:
  ```bash
  cd /đường/dẫn/đến/repo
  ```
- Chuyển về nhánh chính và kéo code mới nhất:(**~={red}main/master=~** )
  ```bash
  git checkout main
  git pull origin main
  ```
- **Ý nghĩa**: Đảm bảo bạn bắt đầu từ điểm mới nhất của team.

#### Bước 2: Tạo nhánh mới
- Tạo nhánh với tên rõ ràng (ví dụ: `feature-login`):
  ```bash
  git checkout -b feature-login
  ```
  - `-b`: Tạo nhánh mới và chuyển sang luôn.
- **Trong IntelliJ**: 
  - Nhấn nút "New Branch" (dưới tab Git, góc dưới phải).
  - Gõ tên (ví dụ: `feature-login`), nhấn OK.

#### Bước 3: Code trên nhánh mới
- Viết code bình thường trong IntelliJ.
- Commit thay đổi:
  ```bash
  git add .
  git commit -m "Thêm tính năng login"
  ```
  - Hoặc trong IntelliJ: Nhấn `Ctrl + K`, nhập tin nhắn commit, nhấn "Commit".

#### Bước 4: Push nhánh lên remote
- Push lần đầu để tạo nhánh trên remote (GitHub):
  ```bash
  git push --set-upstream origin feature-login
  ```
  - `--set-upstream`: Liên kết nhánh local với remote.
- **Trong IntelliJ**: Nhấn nút "Push" (mũi tên lên), chọn `feature-login`, IntelliJ tự hỏi có set upstream không, chọn "Yes".
- Lần sau chỉ cần:
  ```bash
  git push
  ```

#### Bước 5: Đồng bộ nếu team có thay đổi
- Nếu `main` có commit mới trong lúc bạn làm:
  ```bash
  git fetch origin
  git checkout feature-login
  git merge origin/main
  ```
  - Sửa xung đột (nếu có), rồi commit lại.
- **Trong IntelliJ**: Nhấn "Pull" > chọn `origin/main` > merge.

#### Bước 6: Gộp nhánh vào main (khi xong)
- Tạo Pull Request (PR) trên GitHub:
  1. Vào GitHub, chọn nhánh `feature-login`.
  2. Nhấn "New Pull Request" > merge vào `main`.
- Hoặc merge local:
  ```bash
  git checkout main
  git merge feature-login
  git push origin main
  ```

#### Bước 7: **~={red}Xóa nhánh=~** (sạch sẽ)
- Sau khi **~={red}merge, xóa nhánh=~**:
  ```bash
  git branch -d feature-login  # Xóa local
  git push origin --delete feature-login  # Xóa remote
  ```
- **IntelliJ**: Chuột phải nhánh > "Delete".

---

### Ví dụ thực tế
- Bạn cần thêm tính năng đăng nhập:
  1. `git checkout main && git pull origin main`
  2. `git checkout -b feature-login`
  3. Code, commit: `git commit -m "Thêm form login"`
  4. Push: `git push --set-upstream origin feature-login`
  5. Team review PR trên GitHub, merge vào `main`.
  6. Xóa: `git branch -d feature-login`.

---

### Mẹo tận dụng sức mạnh nhánh
1. **Đặt tên rõ ràng**: `feature/ten-tinh-nang`, `bugfix/ten-loi`, `hotfix/ten-sua`.
2. **Commit nhỏ, thường xuyên**: Dễ theo dõi, dễ merge.
3. **Pull thường xuyên**: Tránh xung đột bằng cách đồng bộ với `main`.
4. **Làm việc độc lập**: Mỗi nhánh là "sân chơi" riêng của bạn.

---

### Tóm lại
- Tạo nhánh: `git checkout -b ten-nhanh`.
- Code, push: `git push --set-upstream origin ten-nhanh`.
- Gộp: Merge vào `main` qua PR.
- Xóa: Giữ repo sạch.

Bắt đầu với nhánh mới đi, lần này sẽ mượt mà hơn! Có bước nào chưa rõ không?
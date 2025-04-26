**1. Tạo branch mới:**

Để tạo một branch mới, sử dụng lệnh `git checkout -b <tên_branch>`.  Lệnh này sẽ tạo một branch mới và đồng thời chuyển sang branch đó.

```bash
git checkout -b <tên_branch>
```

Ví dụ: Để tạo branch `feature/login`:

```bash
git checkout -b feature/login
```

Lệnh này tương đương với hai lệnh sau:

```bash
git branch <tên_branch>  // Tạo branch mới
git checkout <tên_branch> // Chuyển sang branch mới
```

**2. Liệt kê các branch:**

Để xem danh sách các branch hiện có, sử dụng lệnh `git branch`:

```bash
git branch
```

Branch hiện tại sẽ được đánh dấu bằng dấu sao `*`.

**3. Chuyển sang branch khác:**

Để chuyển sang một branch khác, sử dụng lệnh `git checkout <tên_branch>`:

```bash
git checkout <tên_branch>
```

Ví dụ: Để chuyển sang branch `main`:

```bash
git checkout main
```

**4. Commit thay đổi trên branch:**

Sau khi đã chuyển sang branch mới, bạn có thể thực hiện các thay đổi và commit như bình thường:

```bash
git add .  // Stage các thay đổi
git commit -m "Mô tả thay đổi"
```

**5. Push branch lên GitHub:**

Để push branch mới lên GitHub, sử dụng lệnh `git push origin <tên_branch>`:

```bash
git push origin <tên_branch>
```
--**origin: name default of server github**
Ví dụ:

```bash
git push origin feature/login
```

**6. Merge branch vào nhánh chính:**

Khi bạn đã hoàn thành công việc trên branch và muốn hợp nhất nó vào nhánh chính, hãy làm theo các bước sau:

* **Chuyển sang nhánh chính:** `git checkout main` (hoặc `git checkout master`)
* **Merge branch:** `git merge <tên_branch>` (ví dụ: `git merge feature/login`)
* **Giải quyết xung đột (nếu có):** Nếu có xung đột code, Git sẽ thông báo và bạn cần giải quyết chúng thủ công.
* **Push nhánh chính lên GitHub:** `git push origin main` (hoặc `git push origin master`)

**7. Xóa branch (tùy chọn):**

Sau khi đã merge branch vào nhánh chính, bạn có thể xóa branch đó nếu không cần nữa:

```bash
git branch -d <tên_branch>  // Xóa branch local
git push origin --delete <tên_branch> // Xóa branch trên remote (GitHub)
```


**Ví dụ đầy đủ:**

```bash
# Tạo branch mới
git checkout -b feature/login

# Thực hiện thay đổi và commit
git add .
git commit -m "Thêm tính năng đăng nhập"

# Push branch lên GitHub
git push origin feature/login

# Chuyển sang nhánh chính
git checkout main

# Merge branch
git merge feature/login

# Push nhánh chính lên GitHub
git push origin main

# Xóa branch (tùy chọn)
git branch -d feature/login
git push origin --delete feature/login
```


Đây là quy trình cơ bản để làm việc với Git branch. Hy vọng nó sẽ giúp bạn bắt đầu!  Nếu bạn có bất kỳ câu hỏi nào khác, đừng ngần ngại hỏi nhé.

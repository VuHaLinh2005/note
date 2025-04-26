 
### 1. Rebase là gì và để làm gì?
- **Ý nghĩa**: `git rebase` "**~={red}dời=~**" các **~={red}commit=~** của bạn lên trên **~={red}cùng=~** của **~={red}nhánh khác=~**, thay vì gộp **(merge**) như cách thông thường.
- **Mục đích**:
  - Giữ lịch sử commit~={red} **thẳng hàng=~**, **~={red}không rối=~** với các nhánh phụ.
  - Tránh tạo commit "merge" thừa thãi, giúp team **~={red}dễ đọc=~** lịch sử hơn.

**So sánh**:
- **Merge**: Gộp nhánh, tạo commit "**merge**" mới, lịch sử trông như "**mạng nhện**".
- **Rebase**: "Viết lại" lịch sử, **như** thể bạn **~={red}làm việc=~** trực tiếp trên **nhánh chính** **~={red}từ đầu.=~**

---

### 2. Ví dụ dễ hiểu
Giả sử bạn và team làm việc trên repo:

#### Tình huống:
- Nhánh chính: `main` có 2 commit:
  ```
  A - B (main)
  ```
- Bạn tạo nhánh `feature` và thêm 2 commit:
  ```
  A - B (main)
       \
        C - D (feature)
  ```
- Trong lúc đó, bạn trong team commit thêm `E` vào `main`:
  ```
  A - B - E (main)
       \
        C - D (feature)
  ```

#### Dùng Merge (Cách thông thường):
- Bạn chạy:
  - `git checkout main`
  - `git merge feature`
- Kết quả: Lịch sử thành:
  ```
  A - B - E - F (main)
       \     /
        C - D
  ```
  - `F` là commit "merge", lịch sử có nhánh phụ, hơi rối.

#### Dùng Rebase (Cách sạch hơn):
- Bạn chạy:
  - **`git checkout feature`
  - `git rebase main`
- Git sẽ "dời" `C` và `D` lên trên `E`, như thể bạn làm việc sau `E`:
  ```
  A - B - E - C' - D' (feature)
  ```
- Sau đó:
  - `git checkout main`
  - `git merge feature` (giờ là fast-forward, không tạo commit thừa).
- Kết quả cuối: 
  ```
  A - B - E - C' - D' (main)
  ```
  - Lịch sử thẳng tắp, dễ đọc.

---

### 3. Rebase sinh ra để làm gì?
- **Làm đẹp lịch sử**: Team nhìn commit tuần tự, không bị rối bởi nhánh phụ.
- **Dễ debug**: Tìm lỗi trong lịch sử thẳng đơn giản hơn.
- **Chuyên nghiệp hơn**: Nhiều team lớn (như open-source) yêu cầu rebase trước khi merge.

**Lưu ý**: 
- Chỉ rebase nhánh chưa push. Nếu **~={red}đã push=~**, **~={red}tránh rebase=~** vì sẽ gây (**lộn xộn**) cho team.

---

### 4. Cách dùng nhanh
- `git rebase <nhánh-mục-tiêu>`: Ví dụ `git rebase main`.
- Nếu có xung đột: Sửa tay, rồi `git rebase --continue`.

---

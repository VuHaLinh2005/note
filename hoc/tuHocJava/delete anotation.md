#delete


Khi bạn sử dụng Spring và định nghĩa một URL với **biến đường dẫn** như `{id}` trong `@GetMapping("/banhang/delete/{id}")`, Spring sẽ tự động **lấy giá trị từ phần đường dẫn** đó và **ánh xạ sang biến trong phương thức** của bạn.

Cụ thể, đây là quá trình diễn ra:

1. **Người dùng truy cập đường dẫn với giá trị cụ thể**:
    
    - Ví dụ: Người dùng truy cập vào URL `/banhang/delete/1`.
2. **Spring nhận diện `{id}` trong định nghĩa đường dẫn**:
    
    - Spring biết rằng `{id}` là một **phần động** của đường dẫn, tức là **giá trị này có thể thay đổi.**
3. **Ánh xạ giá trị từ đường dẫn vào biến**:
    
    - Giá trị `1` trong URL `/banhang/delete/1` sẽ được lấy và **ánh xạ vào biến `id`** trong phương thức của bạn. Điều này nhờ vào `@PathVariable`.
4. **Chạy phương thức với giá trị đã ánh xạ**:
    
    - Phương thức `delete(@PathVariable Long id, Model model)` sẽ nhận giá trị `id = 1`.
    - Sau đó, bạn có thể dùng `id` này để xử lý logic xóa hoặc bất kỳ tác vụ nào khác trong phương thức.

```java
@GetMapping("/banhang/delete/{id}") public String delete(@PathVariable Long id, Model model) {
System.out.println("Deleting item with id: " + id); 
gioHangService.delete(id); return GioHangList(model); }
```

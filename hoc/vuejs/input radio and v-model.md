
Đúng vậy! Khi bạn sử dụng `v-model` với các radio button trong Vue, Vue sẽ tự động **so sánh giá trị hiện tại của biến được liên kết** (trong trường hợp của bạn là `sanPham.gioiTinh`) với giá trị (`value`) của từng radio button. Nếu giá trị hiện tại **khớp** với `value`, thì radio button đó sẽ được chọn.

### Cơ chế hoạt động của `v-model` với radio button

1. **`v-model` và radio button:**
    
    - `v-model` kết hợp giá trị của một biến với radio button. Nó **đồng bộ dữ liệu** giữa radio button và biến đó.
    - Khi giá trị của biến (`sanPham.gioiTinh`) khớp với thuộc tính `value` của một radio button, Vue **tự động gắn trạng thái** `checked` cho radio button đó.
2. **Cơ chế so sánh:**
    
    - Vue kiểm tra xem giá trị của `v-model` (`sanPham.gioiTinh`) có bằng giá trị của radio button (`value="nam"`, `value="nu"`, v.v.) hay không.
    - Nếu **bằng**, radio button sẽ được chọn (`checked`).

### Vì sao khi truyền `"nam"` thì radio button "Nam" được chọn?

Trong trường hợp của bạn, khi bạn truyền `"nam"` vào `newSanPham.gioiTinh`, Vue sẽ:

1. Gắn giá trị `"nam"` cho `v-model="sanPham.gioiTinh"`.
2. So sánh giá trị `"nam"` với giá trị `value` của mỗi radio button.
    - Radio button đầu tiên: `value="nam"`. Kết quả so sánh: **khớp** ⇒ Radio button này được chọn.
    - Radio button thứ hai: `value="nu"`. Kết quả so sánh: **không khớp** ⇒ Radio button này không được chọn.

### Khi nào thì cần `checked`?

Thuộc tính `checked` được sử dụng khi bạn muốn **bắt buộc một radio button được chọn mặc định** mà không cần dựa vào `v-model`. Nhưng khi sử dụng `v-model`, Vue tự động xử lý trạng thái `checked` dựa trên giá trị hiện tại của biến được liên kết.

#### Ví dụ: Sử dụng `checked` mà không dùng `v-model`:

Nếu không sử dụng `v-model`, bạn phải tự xác định trạng thái `checked`:


```js
<input type="radio" name="gioiTinh" value="nam" checked>Nam
<input type="radio" name="gioiTinh" value="nu">Nu

```

Trong ví dụ này:

- Radio button "Nam" luôn được chọn mặc định bất kể giá trị nào vì bạn đã thêm thuộc tính `checked` vào nó.

Khi sử dụng `v-model`, bạn không cần thuộc tính `checked` vì Vue sẽ tự động điều khiển trạng thái `checked` dựa trên giá trị của `v-model`.

---

### Tổng kết:

- **Có `v-model`:** Vue tự động so sánh giá trị của `v-model` với `value` của từng radio button và tự gán `checked` cho radio button tương ứng.
- **Không có `v-model`:** Bạn phải tự sử dụng thuộc tính `checked` để đặt radio button mặc định được chọn.
- **Khi giá trị của `v-model` thay đổi:** Vue tự động cập nhật trạng thái `checked` cho radio button tương ứng mà bạn không cần làm gì thêm.

--> v-model ưu tiên giá trị hơn checked,**checked cũng k làm thay đổi giá trị đồng bộ giữa hai cái này**
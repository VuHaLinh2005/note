
@ManyToOne  
@JoinColumn(name = "id_danh_muc")//Khóa ngoại liên kết với cột id của DanhMuc  
private DanhMuc danhMuc;

🔍 **Tại sao lại dùng kiểu dữ liệu là lớp `DanhMuc` trong ánh xạ quan hệ JPA?**

Đúng vậy! Việc sử dụng kiểu dữ liệu là lớp `DanhMuc` thay vì chỉ dùng một `int` hoặc `long` là để giúp JPA **hiểu mối quan hệ giữa hai thực thể** và dễ dàng truy cập thông tin trong lớp `DanhMuc`, như `id`, `name`, hay bất kỳ trường nào khác.

### 📌 **Lý do chính khi dùng kiểu dữ liệu là lớp `DanhMuc` trong ánh xạ quan hệ:**

1. **Giúp JPA xác định mối quan hệ**: Khi khai báo thuộc tính `danhMuc` trong lớp `SanPham` với kiểu là `DanhMuc`, JPA biết rằng `SanPham` có **mối quan hệ `Many-to-One` với `DanhMuc`**. JPA sẽ dùng reflection để tìm và lấy thông tin về `DanhMuc`, bao gồm các cột và khóa chính.
    
2. **Tự động quản lý khóa ngoại**: Khi bạn sử dụng kiểu dữ liệu là lớp `DanhMuc`, JPA tự hiểu rằng nó cần tạo một khóa ngoại liên kết với bảng `danh_muc`. Điều này giúp đơn giản hóa mã nguồn, vì bạn không cần phải khai báo khóa ngoại một cách tường minh. Thay vào đó, JPA sẽ tự động quản lý mối quan hệ giữa hai thực thể dựa trên kiểu dữ liệu của thuộc tính `danhMuc`.
    
3. **Truy cập đối tượng liên quan dễ dàng hơn**: Khi dùng lớp `DanhMuc` thay vì chỉ dùng `id`, bạn có thể truy cập các thuộc tính khác của `DanhMuc` (như `tenDanhMuc`, `moTa`, etc.) trực tiếp từ đối tượng `SanPham`. Ví dụ, `sanPham.getDanhMuc().getTenDanhMuc()` dễ hiểu và rõ ràng hơn so với việc chỉ có `id` và phải truy vấn thủ công để lấy tên danh mục.
    
4. **Linh hoạt trong quản lý vòng đời đối tượng**: Với kiểu dữ liệu là lớp `DanhMuc`, JPA có thể dễ dàng quản lý các thao tác như **cascade** (liên kết vòng đời của các đối tượng) và **fetching strategy** (chiến lược lấy dữ liệu). Điều này giúp dễ dàng quản lý các mối quan hệ phức tạp hơn, như khi bạn muốn tự động xóa, cập nhật các thực thể liên quan.
    

---

### 🧩 **Tóm lại**:

Dùng kiểu dữ liệu là lớp `DanhMuc` trong ánh xạ quan hệ giúp JPA:

- Hiểu và tự động xử lý mối quan hệ với bảng `danh_muc`.
- Truy cập dễ dàng hơn vào các thông tin liên quan.
- Tự động quản lý khóa ngoại và các thao tác trên đối tượng một cách linh hoạt hơn.



#addAnnotatedClass

**Giải thích tác dụng của `conf.addAnnotatedClass(SanPham.class)` trong Hibernate**:

Khi sử dụng Hibernate, dòng lệnh `conf.addAnnotatedClass(SanPham.class);` có vai trò quan trọng trong việc cấu hình Hibernate để hiểu và quản lý các thực thể (entity) được đánh dấu bằng annotation trong mã nguồn của bạn. Dưới đây là các tác dụng cụ thể:

### 📌 **Tác dụng chính của `addAnnotatedClass` trong Hibernate:**

1. **Đăng ký lớp thực thể (`Entity Class`) với Hibernate**:
    
    - Dòng lệnh `conf.addAnnotatedClass(SanPham.class);` cho Hibernate biết rằng lớp `SanPham` là một lớp **thực thể (entity class)** mà Hibernate cần quản lý và **ánh xạ vào cơ sở dữ liệu.**
    - Điều này cho phép Hibernate đọc các annotation trên lớp `SanPham` (như `@Entity`, `@Table`, `@Column`, v.v.) để hiểu cấu trúc và các mối quan hệ của lớp này.
2. **Quét và đọc các annotation trên lớp**:
    
    - Khi gặp `addAnnotatedClass`, Hibernate sẽ sử dụng reflection để **quét toàn bộ annotation** trên lớp `SanPham`, như `@Id`, `@ManyToOne`, `@OneToMany`, `@Column`, và các annotation khác.
    - Điều này giúp Hibernate hiểu cách lớp `SanPham` ánh xạ vào các bảng và cột trong cơ sở dữ liệu, cũng như xác định các mối quan hệ giữa `SanPham` và các lớp khác như `DanhMuc`.
3. **Tạo cấu trúc bảng trong cơ sở dữ liệu (nếu cần)**:
    
    - Nếu bạn cấu hình Hibernate để [[Tự động tạo hoặc cập nhật cơ sở dữ liệu]] (ví dụ: `hibernate.hbm2ddl.auto` được thiết lập là `create` hoặc `update`), Hibernate sẽ sử dụng thông tin từ `SanPham` để tạo hoặc cập nhật bảng `san_pham` trong cơ sở dữ liệu.
    - Dựa trên các annotation, Hibernate sẽ xác định cột nào cần có, kiểu dữ liệu của từng cột, và các khóa chính, khóa ngoại, v.v.
4. **Quản lý vòng đời của thực thể**:
    
    - Khi `SanPham.class` được đăng ký, Hibernate có thể **quản lý các hoạt động CRUD (tạo, đọc, cập nhật, xóa)** của lớp `SanPham` dựa trên các annotation và ánh xạ đã được cấu hình.
    - Điều này giúp đơn giản hóa việc làm việc với cơ sở dữ liệu, vì bạn chỉ cần thao tác với đối tượng `SanPham`, còn Hibernate sẽ xử lý phần còn lại (ví dụ, tạo SQL cần thiết để lưu hoặc lấy dữ liệu).

### 🧩 **Tóm lại**:

Dòng `conf.addAnnotatedClass(SanPham.class);` giúp Hibernate:

- Biết `SanPham` là một thực thể cần ánh xạ vào cơ sở dữ liệu.
- Đọc các annotation của `SanPham` để hiểu cấu trúc và mối quan hệ với các bảng khác.
- Quản lý bảng `san_pham` trong cơ sở dữ liệu và các thao tác CRUD liên quan đến `SanPham`.


Đúng vậy! Trong mô hình ORM (Object-Relational Mapping) với Hibernate và JPA, **thông tin từ các entity (thực thể) trong mã Java được ánh xạ vào cơ sở dữ liệu**, chứ không phải ngược lại.

### 🔍 **Lý do entity (thực thể) được ánh xạ vào cơ sở dữ liệu**:

1. **Entity là nguồn thông tin chính**:
    
    - Với Hibernate và JPA, các lớp thực thể trong Java (như `SanPham`) được xem là nguồn cấu trúc chính (source of truth). Cấu trúc dữ liệu, mối quan hệ, và các thuộc tính của bảng sẽ được định nghĩa trong lớp thực thể.
    - Hibernate sẽ đọc thông tin từ lớp `SanPham`, sau đó[[Tự động tạo hoặc cập nhật cơ sở dữ liệu]] trong cơ sở dữ liệu dựa trên các annotation trong mã.
2. **Cấu hình linh hoạt từ mã nguồn**:
    
    - ORM framework như Hibernate giúp bạn **quản lý cơ sở dữ liệu từ mã Java** mà không cần tạo các bảng, khóa ngoại, và cột thủ công trong cơ sở dữ liệu. Khi bạn khai báo các mối quan hệ và thuộc tính trong entity, Hibernate sẽ **tự động ánh xạ** và tạo cấu trúc tương ứng trong cơ sở dữ liệu.
3. **Cơ sở dữ liệu như một "đích đến"**:
    
    - Các lớp Java được ánh xạ vào cơ sở dữ liệu nghĩa là cấu trúc của cơ sở dữ liệu (bảng, cột, mối quan hệ) được **tạo ra dựa trên lớp Java**. Hibernate đóng vai trò như một cầu nối, biến cấu trúc và dữ liệu từ entity Java thành các bảng và cột trong cơ sở dữ liệu.

### 🧩 **Tóm lại**:

Trong Hibernate, các entity là nơi khai báo cấu trúc chính và chúng được ánh xạ vào cơ sở dữ liệu. Điều này giúp bạn chỉ cần quản lý cấu trúc dữ liệu từ mã Java, còn Hibernate sẽ tự động tạo hoặc đồng bộ hóa cơ sở dữ liệu để khớp với các lớp thực thể của bạn.
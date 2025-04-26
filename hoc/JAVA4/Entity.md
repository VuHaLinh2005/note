#entity
#thucThe


Khái niệm **thực thể** (entity) xuất hiện cả trong cơ sở dữ liệu SQL và trong lập trình Java, nhưng có sự khác nhau về cách hiểu và sử dụng:

### 1. **Thực thể trong SQL**

- Trong SQL, **thực thể** là một **bảng** trong cơ sở dữ liệu đại diện cho một đối tượng thực tế hoặc khái niệm trong thế giới thực.
- Mỗi thực thể (bảng) trong SQL chứa **dữ liệu về một loại đối tượng cụ thể**, và mỗi bản ghi (row) trong bảng là một **thực thể cụ thể** của loại đối tượng đó.
- Ví dụ:
    - Bảng `Users` trong SQL là một thực thể đại diện cho người dùng. Mỗi hàng (row) trong bảng `Users` là một người dùng cụ thể với thông tin như `id`, `name`, và `email`.

### 2. **Thực thể trong Java (Hibernate)**

- Trong Java, đặc biệt là khi dùng Hibernate, **thực thể** là một **lớp Java** đại diện cho **bảng trong cơ sở dữ liệu.**
- Lớp thực thể này chứa các thuộc tính (fields) tương ứng với các cột của bảng trong SQL.
- Mỗi đối tượng (instance) của lớp Java này đại diện cho một bản ghi (row) cụ thể trong bảng.
- Ví dụ:
    - Nếu bạn có bảng `Users` trong SQL, bạn sẽ tạo một lớp `Users` trong Java và đánh dấu nó là một thực thể bằng cách sử dụng annotation `@Entity`.
    - Mỗi đối tượng `Users` trong Java (ví dụ: `new Users()`) đại diện cho một người dùng cụ thể và sẽ ánh xạ với một hàng trong bảng `Users` của SQL.

-- >> trong java :  để **Ánh xạ** dữ liệu **từ cơ sở dữ liệu vào đối tượng Java**
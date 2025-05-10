 
- **Serializable Là Gì?** Nó là một **dấu hiệu** (interface) trong Java. Khi một đối tượng "đeo" dấu hiệu này, nó cho phép đối tượng đó có thể được **chuyển đổi thành chuỗi byte**.
- **Serialization (Tuần Tự Hóa):** Là quá trình **chuyển một đối tượng từ trong bộ nhớ thành chuỗi byte**.
- **Deserialization (Giải Tuần Tự Hóa):** Là quá trình **chuyển chuỗi byte đó trở lại thành đối tượng** trong bộ nhớ.
- **Dùng Để Làm Gì (Ứng Dụng Thực Tế):**
    - **Lưu đối tượng vào file:** Giúp bạn lưu trạng thái của đối tượng để dùng sau này.
    - **Gửi đối tượng qua mạng:** Khi bạn cần gửi dữ liệu (là một đối tượng) từ ứng dụng này sang ứng dụng khác qua mạng.
    - **Truyền dữ liệu trong API:** Thường dùng để chuyển dữ liệu giữa backend (ví dụ: Java) và frontend (ví dụ: JavaScript), thường dưới dạng JSON hoặc XML sau khi đã serialize.
- **Lưu Ý Quan Trọng (Vấn Đề Tiềm Ẩn):** Việc serialize trực tiếp các đối tượng phức tạp (như các entity trong database) có thể gặp vấn đề. Một vấn đề hay gặp là **vòng lặp vô hạn** nếu các đối tượng có mối quan hệ tham chiếu lẫn nhau tạo thành vòng.
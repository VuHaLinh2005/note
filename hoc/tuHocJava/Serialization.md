#serializable


### 📘 **Serializable Là Gì Trong Java?**

- 🏷️ **Serializable là gì?** `Serializable` là một **interface** trong Java, cho phép một đối tượng Java có thể được **tuần tự hóa (serialize)**, tức là chuyển đổi đối tượng thành một chuỗi byte. Chuỗi byte này có thể được lưu trữ trên đĩa (trong tệp) hoặc truyền qua mạng. Khi cần sử dụng lại, chuỗi byte này có thể được **giải tuần tự hóa (deserialize)** để tái tạo lại đối tượng ban đầu.
    
- 🔗 **Tuần Tự Hóa (Serialization) trong Java Bean** Việc cho phép Java Bean triển khai `Serializable` giúp nó dễ dàng được lưu trữ hoặc truyền đi ở dạng byte. Điều này hữu ích trong các tình huống:
    
    - **Lưu trữ đối tượng vào file**: Giúp bạn lưu đối tượng vào file để sử dụng lại sau này.
    - **Truyền đối tượng qua mạng**: Khi một ứng dụng Java cần gửi dữ liệu qua mạng, dữ liệu được tuần tự hóa và giải tuần tự hóa ở bên nhận để đảm bảo tính toàn vẹn.

**Serialization** là quá trình chuyển đổi một **đối tượng** trong bộ nhớ (ví dụ: một đối tượng Java) thành một **chuỗi byte** để có thể lưu trữ hoặc truyền đi (ví dụ: gửi qua mạng). **Deserialization** là quá trình ngược lại, chuyển đổi chuỗi byte trở lại thành đối tượng trong bộ nhớ.

Khi làm việc với API, serialization và deserialization thường được sử dụng để chuyển đổi dữ liệu giữa backend (ví dụ: Java) và frontend (ví dụ: JavaScript). Dữ liệu thường được serialize thành JSON hoặc XML.

**Vấn đề khi serialize/deserialize trực tiếp Entity:**

- **Entity thường phức tạp:** Entity có thể chứa nhiều trường dữ liệu, quan hệ với các entity khác, và các logic nghiệp vụ. Việc serialize/deserialize trực tiếp entity có thể dẫn đến các vấn đề như:
    
    - **Vòng lặp vô hạn:** Nếu entity có quan hệ vòng (ví dụ, A liên kết đến B, B liên kết đến C, và C lại liên kết đến A), quá trình serialization có thể rơi vào **vòng lặp vô hạn**.


bytecode ra lệnh cho - > jvm  -> bit


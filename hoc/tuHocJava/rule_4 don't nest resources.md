

Quy tắc này đề cập đến việc **không nên lồng (nest) các tài nguyên trong RESTful API**. Cụ thể, thay vì lồng tài nguyên (ví dụ như `/authors/12/articles`), nên xem xét việc sử dụng **query string** để lấy dữ liệu liên quan giữa các tài nguyên.

### Giải thích lý do:

1. **Sự rõ ràng và đơn giản**: Việc không lồng các tài nguyên sẽ làm cho API dễ hiểu và đơn giản hơn. Một cấu trúc phẳng (flat) thường dễ quản lý và tránh được các vấn đề liên quan đến lồng nhau.
    
2. **Đại diện đúng mối quan hệ một-nhiều**: Đúng là lồng tài nguyên giúp biểu diễn rõ mối quan hệ một-nhiều (ví dụ: một tác giả có nhiều bài viết). Tuy nhiên, việc lồng tài nguyên có thể dẫn đến cấu trúc phức tạp khi có nhiều cấp lồng nhau, gây khó khăn trong việc mở rộng API.
    
3. **Sử dụng query string thay thế**: Quy tắc này đề xuất sử dụng query string (chuỗi truy vấn) để lọc tài nguyên trực tiếp, ví dụ như `GET /articles?authorId=12` thay vì `GET /authors/12/articles`. Cách này giúp API linh hoạt hơn vì người dùng có thể dễ dàng thêm các bộ lọc khác mà không cần thay đổi cấu trúc URL.
    
4. **Khả năng tái sử dụng tài nguyên**: Khi không lồng tài nguyên, bạn có thể sử dụng cùng một endpoint (`/articles`) cho nhiều mục đích khác nhau chỉ bằng cách thay đổi query string. Điều này giúp tăng khả năng tái sử dụng và giảm sự phụ thuộc giữa các tài nguyên.
    

### Tóm lại

Mặc dù việc lồng tài nguyên thể hiện được quan hệ một-nhiều, nhưng một cấu trúc phẳng và việc sử dụng query string sẽ giúp API dễ mở rộng, linh hoạt hơn, và tránh được các vấn đề tiềm ẩn khi phải quản lý nhiều cấp tài nguyên.
-- **cho thực thể mạnh đứng trước**



rong mô hình cơ sở dữ liệu, **"articles"** có thể được coi là **thực thể yếu (weak entity)** hoặc **thực thể mạnh (strong entity)** tùy thuộc vào cách nó được thiết kế trong hệ thống và mối quan hệ của nó với các thực thể khác, như **"authors"**.

### Phân tích "articles" là thực thể mạnh hay yếu:

1. **Thực thể mạnh (strong entity)**:
    
    - "Articles" sẽ là một **thực thể mạnh** nếu nó có thể tồn tại độc lập mà không phụ thuộc vào bất kỳ thực thể nào khác. Điều này có nghĩa là mỗi bài viết sẽ có một **khóa chính (primary key) riêng** không phụ thuộc vào "authors" hoặc bất kỳ thực thể nào khác.
    - Ví dụ, nếu mỗi bài viết có một `article_id` là khóa chính và có thể tồn tại mà không cần có "authors", thì "articles" sẽ được xem là thực thể mạnh.
2. **Thực thể yếu (weak entity)**:
    
    - "Articles" có thể là một **thực thể yếu** nếu nó phụ thuộc vào "authors" để tồn tại. Điều này thường xảy ra khi bài viết không có khóa chính riêng và cần sử dụng khóa của "authors" làm một phần của khóa chính. Trong trường hợp này, **khóa chính của "articles"** sẽ là sự kết hợp của `author_id` và một thuộc tính khác (ví dụ, `article_number`) để tạo thành một khóa duy nhất.
    - Ví dụ, nếu mỗi bài viết chỉ có ý nghĩa và tồn tại khi gắn liền với một tác giả cụ thể, và không thể tồn tại nếu không có tác giả, thì "articles" sẽ là một thực thể yếu.

### Tóm lại:

- **Articles là thực thể mạnh** nếu nó có thể tồn tại độc lập và có khóa chính riêng (ví dụ, `article_id`).
- **Articles là thực thể yếu** nếu nó phụ thuộc vào "authors" để tồn tại và cần sử dụng `author_id` như một phần của khóa chính.

Trong thiết kế RESTful API, chúng ta thường coi "articles" là **thực thể mạnh** vì nó có thể tồn tại độc lập với "authors" trong hầu hết các ứng dụng, với mỗi bài viết có một `article_id` duy nhất.
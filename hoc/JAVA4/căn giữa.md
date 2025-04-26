
## trick 
Đây là một câu hỏi rất hay! Thật ra, việc sử dụng **`left: 50%; transform: translateX(-50%)`** có lý do của nó khi chúng ta cần **căn giữa một phần tử có chiều rộng toàn màn hình (100vw) trong một bố cục cố định**.
- nhớ posititon - relative : thoát khỏi thẻ cha.

### Tại sao cần dùng `left: 50%; transform: translateX(-50%)` thay vì chỉ để `width: 100vw`?

Nếu chỉ đặt `width: 100vw` mà không có **`left: 50%; transform: translateX(-50%)`**, phần tử sẽ không thực sự được căn giữa nếu nó nằm trong một container có chiều rộng cố định. Thay vào đó, nó sẽ mở rộng từ **trái sang phải toàn bộ chiều ngang của viewport** nhưng không đảm bảo vị trí chính giữa.

### Ví dụ về vấn đề

Giả sử phần tử `<section>` đang nằm trong một container trung tâm có chiều rộng giới hạn (ví dụ `container` của Bootstrap). Khi đó, nếu chỉ đặt `width: 100vw`, phần tử sẽ mở rộng vượt quá container, nhưng điểm bắt đầu vẫn là từ **rìa trái của container** chứ không phải chính giữa màn hình. Điều này sẽ khiến phần tử **lệch sang bên phải** so với viewport, không đúng với ý muốn căn giữa toàn màn hình.

### Tại sao lại cần `left: 50%; transform: translateX(-50%)`?

- **`left: 50%`**: Di chuyển điểm bắt đầu của phần tử đến chính giữa màn hình.
- **`transform: translateX(-50%)`**: Kéo ngược phần tử lại một nửa chiều rộng của chính nó, làm cho nó được căn giữa tuyệt đối.
-  ==> **kéo đi kéo lại cho vừa .**

### Khi nào cần kỹ thuật này?

Kỹ thuật **`left: 50%; transform: translateX(-50%)`** hữu ích khi:

- Bạn muốn phần tử nằm chính giữa màn hình, bất kể container của nó có chiều rộng cố định hoặc linh hoạt.
- Bạn đang làm việc với các phần tử có **chiều rộng toàn màn hình** (100vw) nhưng nằm trong một cấu trúc bố cục có giới hạn chiều rộng (như container của Bootstrap).

### Tóm lại

- **Nếu phần tử nằm trong một bố cục có giới hạn chiều rộng** (như `container`), thì kỹ thuật này đảm bảo phần tử được căn giữa toàn bộ viewport, không bị lệch.
- **Nếu phần tử nằm trực tiếp trong `<body>` hoặc một container chiếm toàn bộ chiều rộng** của màn hình, bạn có thể chỉ cần `width: 100vw` mà không cần `left: 50%; transform: translateX(-50%)`.
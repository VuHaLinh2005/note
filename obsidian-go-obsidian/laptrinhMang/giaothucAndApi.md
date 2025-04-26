
#giaoThucAndApiKnow

# đơn giản là ?
	1. Giao thức (protocol) và API (Application Programming Interface) liên quan đến cách các hệ thống, phần mềm giao tiếp và làm việc với nhau, nhưng chúng có vai trò khác nhau.**Giao thức** là **bộ quy tắc** về cách các thiết bị hoặc phần mềm trao đổi thông tin. Giống như quy tắc về ngôn ngữ và hành vi cần tuân theo khi giao tiếp.

**API** là **cầu nối** giúp phần mềm này yêu cầu và nhận dịch vụ từ phần mềm khác thông qua các giao thức.

**Ví dụ trực quan:**

### **Giao Thức (Protocol)**

- **Tương Tự Địa Chỉ**: Giao thức URI giống như địa chỉ của dịch vụ hoặc ứng dụng. Nó cho hệ điều hành hoặc trình duyệt biết ứng dụng nào sẽ xử lý liên kết.
- **Ví Dụ**:
    - `http://` – Địa chỉ cho trình duyệt web biết để mở một trang web.
    - `mailto://` – Địa chỉ cho ứng dụng email biết để soạn một email mới.

### **API (Application Programming Interface)**

- **Tương Tự Quy Tắc hoặc Đặc Điểm**: API giống như các quy tắc hoặc đặc điểm cho phép các ứng dụng giao tiếp với nhau. Nó cung cấp các phương thức và quy tắc để gửi yêu cầu và nhận dữ liệu.
- **Ví Dụ**:
    - Một API web có thể cho phép ứng dụng gửi dữ liệu đến máy chủ và nhận dữ liệu về từ máy chủ.
    - API của Obsidian có thể cung cấp các phương thức để tạo ghi chú mới, mở một vault, hoặc tìm kiếm ghi chú.

### Sự Tương Quan

1. **Giao Thức (Địa Chỉ)**
    
    - **Chức Năng**: Chỉ định dịch vụ hoặc ứng dụng cụ thể.
    - **Ví Dụ**: `obsidian://` cho biết liên kết thuộc về ứng dụng Obsidian.
2. **API (Quy Tắc/Đặc Điểm)**
    
    - **Chức Năng**: Cung cấp các phương thức và quy tắc để giao tiếp và thực hiện các hành động trong ứng dụng.
    - **Ví Dụ**: API của Obsidian có thể cho phép các ứng dụng bên ngoài gửi lệnh để mở một ghi chú hoặc tạo một ghi chú mới.

### Ví Dụ Cụ Thể

- **Giao Thức URI**:
    
    - `obsidian://open?vault=obsidian-go-obsidian` – `obsidian://` là giao thức chỉ định rằng liên kết này cần được xử lý bởi Obsidian.
- **API (Nếu có)**:
    
    - API của Obsidian có thể bao gồm các phương thức như `openVault` hoặc `createNote` để thực hiện các hành động cụ thể trong ứng dụng.

### Tóm Tắt

- **Giao Thức**: Là địa chỉ cho biết ứng dụng hoặc dịch vụ nào sẽ xử lý liên kết.
- **API**: Là các quy tắc hoặc phương thức cho phép giao tiếp và thực hiện các hành động trong ứng dụng.

Như vậy, giao thức URI giúp xác định ứng dụng nào sẽ xử lý liên kết, trong khi API cung cấp các phương thức và quy tắc để thực hiện các thao tác cụ thể trong ứng dụng đó.

ví dụ paste uri này lên web , web có khả năng cho tương tác uri được : obsidian://open?vault=obsidian-go-obsidian

	



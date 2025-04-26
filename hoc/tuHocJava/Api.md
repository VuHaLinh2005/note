

## what ? 
Hiểu nôm na, API giống như một người trung gian giúp hai ứng dụng (hoặc phần mềm) giao tiếp với nhau. Bạn cứ hình dung là bạn có một app thời tiết, và app đó cần thông tin thời tiết từ server của một dịch vụ nào đó. Thay vì tự đi tìm kiếm dữ liệu, app của bạn có thể gọi API của dịch vụ thời tiết đó để yêu cầu thông tin.

**~={red}đơn giản=~** : 
- 1 đường link **~={red}url=~** tại backend 
- fonend gọi đến để **~={red}lấy=~** và **~={red}sử dụng=~** dữ liệu


Ví dụ cụ thể:

Giả sử bạn làm một ứng dụng đơn giản để hiển thị thời tiết. Bạn sẽ:

1. **Gọi API của dịch vụ thời tiết**: Gửi yêu cầu lên API của dịch vụ thời tiết (như OpenWeatherMap hay WeatherAPI), yêu cầu thông tin về thời tiết cho một thành phố cụ thể.
    
2. **API trả về dữ liệu (thường là JSON)**: API sẽ phản hồi bằng một đoạn dữ liệu JSON chứa thông tin về nhiệt độ, độ ẩm, dự báo, v.v. Ví dụ:
    

- note : **API** **(Application Programming Interface) là một tập các quy tắc và cơ chế mà theo đó, một ứng dụng hay một thành phần sẽ tương tác với một ứng dụng hay thành phần khác. API có thể trả về dữ liệu mà bạn cần cho ứng dụng của mình ở những kiểu dữ liệu phổ biến như [JSON](https://topdev.vn/blog/json-la-gi/) hay XML.**

Copy code

`{   "city": "Hanoi",   "temperature": "30°C",   "humidity": "70%",   "description": "clear sky" }`

3. **Hiển thị dữ liệu trong app**: Bạn lấy các thông tin này từ JSON và hiển thị nó trên giao diện app của bạn.

Với JSON ở trên, bạn sẽ hiển thị: “Hà Nội, Nhiệt độ: 30°C, Độ ẩm: 70%, Trời quang.”

API cho phép bạn không cần phải lưu trữ hay cập nhật dữ liệu thời tiết mà chỉ cần lấy dữ liệu từ nơi đã có sẵn, giúp app của bạn luôn có thông tin mới.




Tài liệu: [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

  

Mã lỗi ám chỉ request thành công:

200 - request succeeded (hay dùng cho method GET/PUT/DELETE)

201 - request created a resource (hay dùng cho method POST)

204 - no content to return (dùng khi bạn muốn thông báo không có data ở phản hồi)

  

202 - Accepted (the request has been accepted for processing, but the processing has not been completed): dùng khi bạn chạy job/background task và muốn gửi phản hồi cho client

  

Mã lỗi ám chỉ request thất bại (lỗi do client):

400 - Bad request (lỗi exception, validate...)

401 - Unauthorized (unauthenticated): bạn chưa đăng nhập, có nghĩa rằng bạn cần login thành công thì mới có quyền sử dụng endpoint (API)

403 - Forbidden (unauthorized): bạn đã đăng nhập thành công, tuy nhiên, bạn không có quyền hạn (authorization) để thực hiện tác vụ này

404 - Resource not found : lỗi huyền thoại cmnr :v

405 - Method not supported : check cho đúng method khi sử dụng với endpoint

  

415 - Media not supported: bạn cần truyền đúng định dạng format mà server/client mong muốn. Ví dụ, bạn không thể dùng JSON để gửi file lên 

server (cần dùng formData)

  

Mã lỗi ám chỉ request thất bại (lỗi do server):

500 - Internal Server error: lỗi xảy ra bên trong Server, cần đọc logs để biết lỗi gì (exception, bugs...)

503 - Service Unavailable : server ngỏm (không chạy) nên không có sẵn để sử dụng

504 - Gateway Timeout : server (có thể) không ngỏm, cơ mà không phản hồi trong thời gian quy định (quá lâu để phản hồi)


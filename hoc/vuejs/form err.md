


### Vấn đề:

Khi bạn sửa thẻ `<form>` thành một thẻ khác và việc login thành công thì bảng hiển thị trạng thái `isLogin` đúng, nhưng khi bạn sử dụng thẻ `<form>` mà không chặn hành vi mặc định (ví dụ, qua `@submit.prevent`), hàm `checkLogin` của bạn không được gọi lại sau khi form bị reset, do đó, giá trị `isLogin` không được cập nhật và bảng không phản ánh thay đổi đó.

### Phân tích:

Khi bạn sử dụng thẻ `<form>`, mặc định khi nhấn nút submit, form sẽ bị reset và trang có thể được tải lại (reload). Điều này khiến cho:

1. **Không gọi lại hàm `checkLogin`** sau khi form bị reset, do hành động submit sẽ chặn Vue không tiếp tục xử lý JavaScript của bạn.
2. **Không cập nhật trạng thái `isLogin` trong bảng**. Vì hàm `checkLogin` không được gọi lại và giá trị `isLogin` trong `users` không thay đổi, bảng không biết có sự thay đổi và không được cập nhật.

Khi bạn **thay đổi thẻ form sang một thẻ khác** (ví dụ, dùng một nút `<button>` ngoài form hoặc `div`), bạn không bị ràng buộc bởi hành vi submit mặc định của form. Do đó, `checkLogin` được gọi đúng lúc và bảng cập nhật như mong muốn.

### Giải pháp:

1. **Chặn hành vi mặc định của form**: Khi bạn dùng thẻ `<form>`, luôn phải chặn hành vi mặc định của nó để ngăn việc tải lại trang và đảm bảo rằng hàm `checkLogin` sẽ được gọi đúng cách.
2. **Xử lý sự kiện login đúng cách**: Bạn cần đảm bảo rằng form không bị reset sau khi submit, và khi đăng nhập thành công, dữ liệu của bảng được cập nhật.

### Cách sửa mã:

Dưới đây là cách để chắc chắn rằng hàm `checkLogin` sẽ được gọi đúng và bảng sẽ được cập nhật khi trạng thái `isLogin` thay đổi:

vue

Copy code

`<template>   <main class="container py-5 my-3">     <section>       <h3>Login</h3>       <div class="py-2">         <p>           Tạo tài khoản mới?           <span><a href="" class="text-decoration-none">Create an account</a></span>         </p>       </div>       <!-- Chặn hành vi mặc định của form bằng @submit.prevent -->       <form @submit.prevent="login">         <div class="mb-3">           <input class="form-control" type="text" placeholder="Phone number/UserName/Email" v-model="email" />         </div>         <div class="mb-3">           <input class="form-control" type="text" placeholder="Password" v-model="passWord" />         </div>         <div class="mb-1">           <input type="submit" value="Login" class="btn btn-outline-info" />         </div>         <div class="d-flex justify-content-between py-2">           <div><a href="" class="text-decoration-none text-info-emphasis">Forgot Password</a></div>           <div>             <a href="" class="text-decoration-none text-info-emphasis">Login with phone number</a>           </div>         </div>         <div class="d-flex align-items-center my-4">           <hr class="flex-grow-1" />           <span class="mx-2">or</span>           <hr class="flex-grow-1" />         </div>       </form>       <div class="row">         <div class="col-md-4 d-flex align-items-center ">           <div><img src="https://img.icons8.com/?size=48&id=13912&format=png" alt="" /></div>           Continue with Facebook         </div>         <div class="col-md-4 d-flex align-items-center ">           <div><img src="https://img.icons8.com/?size=48&id=17949&format=png" alt="" /></div>           Continue with Google         </div>         <div class="col-md-4 d-flex align-items-center ">           <div><img src="https://img.icons8.com/?size=50&id=30840&format=png" alt="" /></div>           Continue with Apple         </div>       </div>     </section>   </main> </template>  <script setup> import { checkLogin } from '@/api/UserApi' import { ref } from 'vue'  const email = ref('') const passWord = ref('') const login = () => {   // Gọi hàm checkLogin khi submit, sẽ cập nhật bảng sau khi đăng nhập   checkLogin(email.value, passWord.value) } </script>`

### Giải thích:

1. **`@submit.prevent="login"`**: Sự kiện này chặn hành vi mặc định của form khi submit, ngăn việc reload trang và cho phép Vue xử lý đăng nhập mà không làm mất dữ liệu trong các thẻ input.
2. **`checkLogin(email.value, passWord.value)`**: Sau khi submit form, bạn gọi hàm `checkLogin` để xác thực và cập nhật giá trị `isLogin` cho người dùng. Hàm này sẽ trực tiếp cập nhật dữ liệu trong `users` và đảm bảo bảng được cập nhật.

### Tại sao khi dùng thẻ `<form>`, nếu không chặn hành vi mặc định, bảng không được cập nhật:

Khi bạn sử dụng thẻ `<form>`, hành động submit sẽ khiến trang reload lại (hoặc reset form), do đó Vue không thể tiếp tục xử lý JavaScript (ví dụ: không gọi lại `checkLogin` sau khi submit). Tuy nhiên, khi bạn thay thế form bằng một thẻ khác (chẳng hạn nút ngoài form), hành động này không xảy ra, do đó `checkLogin` được gọi và bảng được cập nhật.

### Xem thêm:

- Vue 3 Forms Guide
- Vue 3 Event Modifiers
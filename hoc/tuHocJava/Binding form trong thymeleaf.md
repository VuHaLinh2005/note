
Trong Thymeleaf, khi bạn dùng thuộc tính **th:field** trên một thẻ form (ví dụ như thẻ select), bạn đang thực hiện việc binding trực tiếp thuộc tính của model với form control đó. Điều này có nghĩa là:

1. **Tự động tạo thuộc tính name:**  
    Khi gán `th:field="*{phongKham.id}"` lên thẻ select, Thymeleaf sẽ tự động tạo ra thuộc tính HTML ~={red}**`name="phongKham.id"`=~. Thuộc tính này rất quan trọng vì khi form được submit, Spring MVC sẽ tìm kiếm các ~={red}parameter=~ có tên giống như này để ~={red}binding=~ vào thuộc tính của ~={red}đối tượng=~ model tương ứng.
#### **Tóm tắt chi phí**

- Nếu có `n` phần tử trong mảng và bạn xóa `k` phần tử:
    - Số thao tác dịch chuyển tổng cộng là:

```java
total = (n - 1) + (n - 2) + ... + (n - k)

```

Đây là một chuỗi số học có độ phức tạp **O(n * k)**.
## tại sao 
Để giải thích rõ hơn, đây là công thức **ước tính tổng số lần dịch chuyển phần tử** khi sử dụng `splice` trong một vòng lặp nhiều lần trên mảng.

---

### **Chi tiết: Công thức này có nghĩa là gì?**

Khi bạn xóa phần tử trong mảng bằng `splice`, các phần tử phía sau phần tử bị xóa phải dịch chuyển lên để lấp khoảng trống.

Nếu bạn xóa **nhiều phần tử** (giả sử `k` phần tử) từ mảng, thì:

1. Với lần xóa đầu tiên, số phần tử phải dịch chuyển sẽ gần bằng `n - 1` (phần tử cuối cùng trong mảng không cần dịch chuyển).
2. Với lần xóa thứ hai, số phần tử phải dịch chuyển sẽ giảm xuống còn `n - 2`.
3. Cứ tiếp tục như vậy, số lần dịch chuyển sẽ giảm dần cho đến khi bạn xóa `k` phần tử.

- Lần 1: Xóa `1`, mảng còn `[2, 3, 4, 5]`. **4 phần tử dịch chuyển.**
- Lần 2: Xóa `2`, mảng còn `[3, 4, 5]`. **3 phần tử dịch chuyển.**
- Lần 3: Xóa `3`, mảng còn `[4, 5]`. **2 phần tử dịch chuyển.**
- Lần 4: Xóa `4`, mảng còn `[5]`. **1 phần tử dịch chuyển.**

tông sô lần dịch : 4 + 3 + 2 + 1 = 10

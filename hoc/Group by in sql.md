
Trong SQL, **GROUP BY** dùng để ~={red}**nhóm**=~ các ~={red}**hàng**=~ có cùng ~={red}**giá trị=~** trong một hoặc nhiều **~={red}cột**=~, rồi tính toán gì đó (như tổng, trung bình) trên từng nhóm.

  

### Cách hoạt động:

- Chia dữ liệu thành các nhóm dựa trên cột bạn chọn.
- Thường dùng với hàm như COUNT, SUM, AVG để tính toán trên mỗi nhóm.
  
### Ví dụ siêu ngắn:

  id | san_pham | gia
1  | Banh     | 10
2  | Keo      | 5
3  | Banh     | 15

SELECT san_pham, SUM(gia)
FROM don_hang
GROUP BY san_pham;

san_pham | SUM(gia)
Banh     | 25       (10 + 15)
Keo      | 5        (5)

**Hiểu luôn:** GROUP BY san_pham nhóm các hàng theo san_pham, rồi SUM(gia) tính tổng giá cho mỗi nhóm.
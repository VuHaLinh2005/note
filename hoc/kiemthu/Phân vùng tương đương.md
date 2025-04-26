
**Phân vùng tương đương (Equivalence Partitioning)** là một kỹ thuật thiết kế ca kiểm thử, trong đó ta **~={red}chia=~** tập hợp **~={red}đầu vào=~** của phần mềm thành các nhóm (**phân vùng**) sao cho các giá trị trong cùng một nhóm có hành vi xử lý tương tự nhau. Ý tưởng là nếu ta kiểm thử **một** giá trị ~={red}đại diện =~cho một phân vùng, ta có thể giả định rằng các giá trị khác trong cùng phân vùng cũng sẽ được **xử lý đúng**.

### Ví dụ đơn giản với bài toán tính tổng n số nguyên

Giả sử bạn có hàm tính tổng các số nguyên được truyền vào dưới dạng danh sách. Ta có thể phân chia các đầu vào thành các phân vùng sau:

1. **Phân vùng hợp lệ (Valid Input):**
    - **Trường hợp 1:** Danh sách chứa nhiều số nguyên dương.
    - **Trường hợp 2:** Danh sách chứa các số nguyên âm.
    - **Trường hợp 3:** Danh sách chứa hỗn hợp số dương, số âm và số 0.
    - **Trường hợp 4:** Danh sách chỉ chứa một số duy nhất.
2. **Phân vùng không hợp lệ (Invalid Input):**
    - **Trường hợp 5:** Danh sách rỗng hoặc giá trị null (nếu theo yêu cầu, đầu vào không được rỗng).

Mỗi phân vùng đại diện cho một nhóm các đầu vào có hành vi xử lý tương tự. Ta chỉ cần chọn một giá trị đại diện từ mỗi phân vùng để làm ca kiểm thử.

### 5 Test Case dựa trên phân vùng tương đương

Dưới đây là 5 test case cụ thể cho bài toán:

1. **Test Case 1: Danh sách chứa nhiều số nguyên dương**
    
    - **Đầu vào:** `[1, 2, 3, 4, 5]`
    - **Kỳ vọng:** Tổng là `15`.
    - **Lý do:** Kiểm thử phân vùng hợp lệ với các số nguyên dương.
2. **Test Case 2: Danh sách chứa các số nguyên âm**
    
    - **Đầu vào:** `[-1, -2, -3, -4, -5]`
    - **Kỳ vọng:** Tổng là `-15`.
    - **Lý do:** Kiểm thử phân vùng hợp lệ với các số nguyên âm.
3. **Test Case 3: Danh sách chứa hỗn hợp số dương, số âm và số 0**
    
    - **Đầu vào:** `[10, -5, 0, 3, -2]`
    - **Kỳ vọng:** Tổng là `6` (10 - 5 + 0 + 3 - 2).
    - **Lý do:** Kiểm thử phân vùng hợp lệ với sự pha trộn của các loại số.
4. **Test Case 4: Danh sách chỉ chứa một số duy nhất**
    
    - **Đầu vào:** `[7]`
    - **Kỳ vọng:** Tổng là `7`.
    - **Lý do:** Kiểm thử phân vùng hợp lệ cho trường hợp danh sách chỉ có một phần tử.
5. **Test Case 5: Danh sách rỗng (hoặc null nếu không được phép)**
    
    - **Đầu vào:** `[]` (hoặc `null`)
    - **Kỳ vọng:** Hệ thống có thể trả về lỗi hoặc thông báo cụ thể (tùy theo yêu cầu thiết kế). Ví dụ: ném ra ngoại lệ `IllegalArgumentException` với thông báo "Danh sách không được rỗng".
    - **Lý do:** Kiểm thử phân vùng không hợp lệ.

### Tổng kết

- **Bước 1:** Xác định các phân vùng đầu vào hợp lệ và không hợp lệ.
- **Bước 2:** Chọn một ca kiểm thử đại diện cho mỗi phân vùng.
- **Bước 3:** Xác định kết quả kỳ vọng cho mỗi ca kiểm thử.


 

### 1. Xác định các nhóm (Equivalence Partitions)

- **Nhóm số chia hết cho 6 (hợp lệ – trả về true):**
    - Ví dụ: 6, -6, 0, 12, …
- **Nhóm số không chia hết cho 6 (hợp lệ – trả về false):**
    - Ví dụ: 5, 7, -5, -7, …
- **Trường hợp input không hợp lệ:**
    - Ví dụ: `null` (nên ném exception)

### 2. Kiểm thử vùng biên (Boundary Value Analysis)

Đối với mỗi nhóm, bạn cần kiểm tra các giá trị “cạnh” (biên) của tập hợp:

- **Xung quanh số 6:**
    - Biên dưới: 5
    - Biên trên: 7
- **Xung quanh số -6:**
    - Biên dưới: -7
    - Biên trên: -5
- **Xung quanh số 0:**
    - Biên dưới: -1
    - Biên trên: 1

### 3. Nhận xét về bộ kiểm thử của bạn

Trong code hiện tại, bạn có:

- **Phân vùng:**
    - `testPhanVung1`: kiểm thử với 6
    - `testPhanVung2`: kiểm thử với -6
- **Vùng biên:**
    - `testVungBien1`: kiểm thử với 5
    - `testVungBien2`: kiểm thử với 7
    - `testVungBien3`: kiểm thử với -5
    - `testVungBien4`: kiểm thử với -7
- **Trường hợp input không hợp lệ:**
    - `testInvalid`: kiểm thử với `null`

**Chưa có:**

- Các test case cho giá trị 0 (với 0 thuộc nhóm chia hết cho 6) và vùng biên của 0 (các giá trị -1 và 1).
- Nếu mục tiêu là có **10 test case hợp lệ** (không tính trường hợp `null`), bạn chỉ mới có 6 test case, nên cần bổ sung thêm 4 trường hợp nữa.

### 4. Đề xuất 10 test case cho giá trị số (bao gồm phân vùng và vùng biên)

Bạn có thể sắp xếp lại các trường hợp như sau:

#### **Các trường hợp cho số chia hết cho 6 (true – Phân vùng):**

1. **Test 1 (Phân vùng):** `6`
2. **Test 2 (Phân vùng):** `-6`
3. **Test 3 (Phân vùng):** `0`
4. **Test 4 (Phân vùng):** `12`

#### **Các trường hợp cho số không chia hết cho 6 (false – Vùng biên):**

1. **Test 5 (Vùng biên):** `5` _(biên dưới của 6)_
2. **Test 6 (Vùng biên):** `7` _(biên trên của 6)_
3. **Test 7 (Vùng biên):** `-7` _(biên dưới của -6)_
4. **Test 8 (Vùng biên):** `-5` _(biên trên của -6)_
5. **Test 9 (Vùng biên):** `-1` _(biên dưới của 0)_
6. **Test 10 (Vùng biên):** `1` _(biên trên của 0)_

Ngoài ra, bạn vẫn giữ lại trường hợp kiểm thử với `null` để đảm bảo hàm xử lý input không hợp lệ.


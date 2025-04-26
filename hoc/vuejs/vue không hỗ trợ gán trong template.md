
Sử dụng logic đúng nhưng không chạy được là do những vấn đề sau đây:

### 1. **Phép gán trong template không được hỗ trợ**

Vue template không cho phép sử dụng trực tiếp **phép gán (`=`)** trong biểu thức. Điều này là do các biểu thức trong template chỉ hỗ trợ **biểu thức trả về giá trị**, không hỗ trợ **tác vụ** (như gán giá trị).

```html
<p>{{ task.name.includes(keySearch) ? task.isShow = true : task.isShow = false }}</p>

```

- `task.isShow = true` là một tác vụ thay đổi trạng thái, không phải là một biểu thức trả về giá trị hợp lệ.
- Vue cấm thực hiện thay đổi trạng thái dữ liệu trực tiếp trong template để đảm bảo tính nhất quán và an toàn của reactivity.

Sử dụng logic đúng nhưng không chạy được là do những vấn đề sau đây:

### 1. **Phép gán trong template không được hỗ trợ**

Vue template không cho phép sử dụng trực tiếp **phép gán (`=`)** trong biểu thức. Điều này là do các biểu thức trong template chỉ hỗ trợ **biểu thức trả về giá trị**, không hỗ trợ **tác vụ** (như gán giá trị).

Ví dụ sau không hợp lệ:

```html
<p>{{ task.name.includes(keySearch) ? task.isShow = true : task.isShow = false }}</p>
```



Lý do không hợp lệ:

- `task.isShow = true` là một tác vụ thay đổi trạng thái, không phải là một biểu thức trả về giá trị hợp lệ.
- Vue cấm thực hiện thay đổi trạng thái dữ liệu trực tiếp trong template để đảm bảo tính nhất quán và an toàn của reactivity.

---

### 2. **Reactivity không được kích hoạt đúng cách**

Khi bạn gán trực tiếp giá trị cho một thuộc tính trong template (nếu được phép), Vue không theo dõi thay đổi đó, vì thay đổi này nằm ngoài phạm vi mà Vue kiểm soát.

---

### 3. **Gán giá trị trong template làm ảnh hưởng tới hiệu suất**

Khi Vue render lại, logic trong template sẽ được thực thi lại. Nếu logic đó gán giá trị, thì mỗi lần render lại sẽ gán giá trị mới, gây ra các hành vi không mong muốn và làm giảm hiệu suất.

---

### Cách giải quyết vấn đề

Để giải quyết vấn đề, bạn cần di chuyển logic gán này ra ngoài template, như sử dụng:

1. **Phương thức (method)**.
2. **Thuộc tính tính toán (computed)**.

---

#### Sử dụng phương thức

javascript

Copy code

`const search = () => {   listTask.value.forEach((task) => {     task.isShow = task.name.includes(keySearch.value.trim());   }); };`

Template:

html

Copy code

`<input type="text" v-model="keySearch" @input="search" /> <div v-for="task in listTask" :key="task.id" v-show="task.isShow">   <p>{{ task.name }}</p> </div>`

---

#### Sử dụng thuộc tính tính toán (computed)

javascript

Copy code

`const filteredTasks = computed(() => {   return listTask.value.map(task => ({     ...task,     isShow: task.name.includes(keySearch.value.trim()),   })); });`

Template:

html

Copy code

`<input type="text" v-model="keySearch" /> <div v-for="task in filteredTasks" :key="task.id" v-show="task.isShow">   <p>{{ task.name }}</p> </div>`

---

### Tại sao cần làm như vậy?

1. **Template chỉ hiển thị UI**:
    
    - Template không phải nơi thực hiện logic gán giá trị hoặc thay đổi dữ liệu.
    - Nếu logic này được xử lý trong JavaScript (method hoặc computed), bạn sẽ giữ code gọn gàng, dễ bảo trì.
2. **Reactivity trong Vue**:
    
    - Khi bạn thay đổi giá trị trong method hoặc computed, Vue sẽ tự động phát hiện thay đổi và cập nhật giao diện.
3. **Tối ưu hóa hiệu suất**:
    
    - Gán giá trị trong template làm Vue phải xử lý lại logic gán mỗi lần render, gây lãng phí tài nguyên. Đưa logic ra method/computed giúp Vue quản lý hiệu quả hơn.

---

### Lời khuyên

Hãy luôn giữ template đơn giản. Mọi logic liên quan đến thay đổi trạng thái dữ liệu nên được xử lý trong `method`, `computed` hoặc `watch`. Điều này giúp mã dễ bảo trì và tuân thủ đúng nguyên tắc của Vue.

4o
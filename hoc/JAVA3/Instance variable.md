#InstanceVariable

Nếu bạn khai báo `studentList` là thuộc tính (instance variable) nhưng lại khởi tạo danh sách bằng từ khóa `new` bên trong hàm, kết quả sẽ phụ thuộc vào cách bạn sử dụng nó. 

Cụ thể, ví dụ như sau:

```java
public class StudentDao {
    private ArrayList<Student> studentList;

    public ArrayList<Student> getStudentList() {
        studentList = new ArrayList<>(); // Khởi tạo lại mỗi lần gọi phương thức
        // Thêm dữ liệu từ database vào danh sách
        return studentList;
    }
}
```

### Điều gì sẽ xảy ra?

- **Khai báo thuộc tính nhưng khởi tạo trong hàm**: Khi bạn khai báo `studentList` là thuộc tính nhưng chỉ khởi tạo danh sách trong phương thức `getStudentList()`, thì mỗi lần bạn gọi phương thức này, danh sách sẽ được làm mới (vì lệnh `new ArrayList<>()` sẽ được thực thi mỗi lần gọi hàm).
    
- **Khởi tạo lại thuộc tính trong phương thức**: Điều này có nghĩa là, mặc dù bạn khai báo `studentList` là một thuộc tính của lớp, nhưng thực tế bạn đang khởi tạo lại nó mỗi lần gọi phương thức. Điều này tương đương với việc không lưu giữ danh sách sau khi phương thức kết thúc, và danh sách cũ sẽ bị ghi đè mỗi lần phương thức được gọi.


## hiểu rõ :
Trong Java, biến **instance** (hay còn gọi là biến thuộc tính của đối tượng) được gắn liền với một đối tượng cụ thể của lớp. Khi bạn khai báo một biến instance và khởi tạo nó (sử dụng `new`), biến đó sẽ chỉ được khởi tạo **một lần duy nhất** trong suốt vòng đời của đối tượng.

### Lý do tại sao biến instance chỉ được khởi tạo 1 lần

1. **Vòng đời của đối tượng**:
    
    - Biến instance được khởi tạo khi đối tượng của lớp được tạo (sử dụng từ khóa `new`) và **tồn tại cho đến khi đối tượng đó bị hủy** (khi không còn tham chiếu và bị Garbage Collector xóa).
    - Khi đối tượng được tạo, các biến instance của đối tượng cũng được khởi tạo theo cùng thời điểm.
    - Do đó, trong suốt vòng đời của đối tượng, biến instance chỉ được khởi tạo một lần duy nhất tại thời điểm đối tượng được tạo ra.
2. **`new` trong constructor hoặc khối khởi tạo**:
    
    - Khi bạn sử dụng từ khóa `new` để khởi tạo biến instance bên ngoài phương thức (tức là khi khai báo thuộc tính của lớp), lệnh `new` đó chỉ được thực thi **khi đối tượng được tạo ra lần đầu tiên**.
    - Sau khi đối tượng đã được tạo ra, biến instance đó sẽ không được khởi tạo lại trừ khi bạn tự mình gọi lệnh `new` trong một phương thức, hoặc tạo ra một đối tượng mới của lớp.
3. **Không phải mỗi lần gọi phương thức là khởi tạo lại đối tượng**:
    
    - Biến instance chỉ thuộc về **đối tượng của lớp**, không phải phương thức. Khi phương thức được gọi nhiều lần, **nó vẫn làm việc với cùng một đối tượng và cùng một biến instance đã được khởi tạo từ lần đầu**.
    - Nếu bạn muốn khởi tạo lại biến mỗi lần phương thức được gọi, bạn cần khởi tạo biến đó bên trong phương thức, không phải ở mức thuộc tính (instance variable).

### Ví dụ minh họa:

Nếu bạn khai báo biến instance `studentList` như sau:


```java

Copy code

`public class StudentDao {     private ArrayList<Student> studentList = new ArrayList<>();  // Instance variable      public void addStudent(Student student) {         studentList.add(student);     }      public ArrayList<Student> getStudentList() {         return studentList;     } }`

```

- Khi bạn tạo một đối tượng của lớp `StudentDao` như sau:
    
    java
    
    Copy code
    
    `StudentDao dao = new StudentDao();`
    
    -> Lúc này, **biến instance `studentList` được khởi tạo một lần duy nhất** với lệnh `new ArrayList<>()`.
    
- Nếu bạn gọi phương thức `addStudent` nhiều lần:
    
    java
    
    
    
    `dao.addStudent(new Student(1, "Linh")); dao.addStudent(new Student(2, "Minh"));`
    
    -> Các sinh viên sẽ được thêm vào danh sách `studentList` cũ, vì danh sách này chỉ được khởi tạo một lần khi đối tượng `dao` được tạo ra.
    
- **Lưu ý**: Biến instance sẽ **không** được khởi tạo lại mỗi lần bạn gọi phương thức `addStudent`, vì lệnh `new ArrayList<>()` đã chạy khi đối tượng `StudentDao` được tạo. Nếu bạn muốn danh sách được khởi tạo lại mỗi lần gọi phương thức, bạn phải di chuyển lệnh `new ArrayList<>()` vào bên trong phương thức.
    

### Tóm lại:

- **Biến instance** được khởi tạo một lần khi đối tượng của lớp được tạo, và tồn tại trong suốt vòng đời của đối tượng đó.
- **Lệnh `new`** ở mức thuộc tính chỉ chạy một lần khi đối tượng được khởi tạo.
- Nếu bạn cần khởi tạo lại biến mỗi lần gọi phương thức, hãy di chuyển lệnh `new` vào bên trong phương thức thay vì để ở mức khai báo thuộc tính của lớp.


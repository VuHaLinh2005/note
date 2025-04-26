[[Inject | chi tiết inject]]
Bạn nói rất đúng. Nếu trình biên dịch chỉ biết `UserRepository` là một interface mà không biết implementation cụ thể, thì làm sao nó biết code nào cần thực thi khi `UserService` gọi một phương thức của `UserRepository`?

Câu trả lời nằm ở **runtime** và **polymorphism (đa hình)**.  Mặc dù trình biên dịch không biết **implementation** cụ thể, nhưng **JVM (Java Virtual Machine)** sẽ biết trong **runtime**.

**Ví dụ cụ thể:**

```java
// Interface
interface UserRepository {
    User findById(Long id);
}

// Implementation 1
class UserRepositoryImpl implements UserRepository {
    @Override
    public User findById(Long id) {
        // Code để lấy User từ database
        System.out.println("Lấy User từ database");
        return new User(id); 
    }
}

// Implementation 2
class InMemoryUserRepositoryImpl implements UserRepository {
    @Override
    public User findById(Long id) {
        // Code để lấy User từ bộ nhớ
        System.out.println("Lấy User từ bộ nhớ");
        return new User(id);
    }
}

// UserService
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public User getUser(Long id) {
        return userRepository.findById(id);
    }
}


public class Main {
    public static void main(String[] args) {
        // Giả lập Spring container (thực tế Spring làm phức tạp hơn)
        UserRepository repo;
        if (/* một số điều kiện */) {
            repo = new UserRepositoryImpl();
        } else {
            repo = new InMemoryUserRepositoryImpl();
        }

        UserService userService = new UserService();
        userService.userRepository = repo; // Inject dependency


        User user = userService.getUser(1L);
    }
}

```

**Giải thích:**

1. **Thời điểm biên dịch:** Trình biên dịch chỉ kiểm tra xem `userRepository.findById(id)` có hợp lệ về mặt cú pháp không (kiểu dữ liệu, số lượng tham số,...).  Nó *không biết* `findById()` sẽ thực thi code nào.

2. **Thời điểm chạy:**
    * Spring container (hoặc trong ví dụ đơn giản này là code trong `main()`) sẽ tạo một **instance** của một **implementation** cụ thể (ví dụ `UserRepositoryImpl` hoặc `InMemoryUserRepositoryImpl`).
    * **Instance** này được **[[Inject]]** vào `userRepository` của `UserService`.
3. Khi `userService.getUser(1L)` được gọi, JVM sẽ dựa vào **kiểu thực tế**(**dc inject**) của đối tượng được `userRepository` **tham chiếu** (là `UserRepositoryImpl` hay `InMemoryUserRepositoryImpl`) để xác định code nào của `findById()` cần được **thực thi**.  Đây chính là **polymorphism (đa hình)**.


**Tóm lại:**

Mặc dù trình biên dịch không biết implementation cụ thể, JVM sẽ biết trong runtime nhờ vào **[[polymorphism]]**.  JVM sẽ thực thi code của phương thức dựa trên **kiểu thực tế** của **đối tượng**, chứ không phải kiểu được khai báo trong code.  Nhờ đó, `UserService` có thể sử dụng `userRepository` mà không cần biết trước implementation cụ thể, giúp code linh hoạt và dễ dàng thay đổi.

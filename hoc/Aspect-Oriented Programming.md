AOP (Aspect-Oriented Programming) là một **mô hình lập trình** tập trung vào việc modular hóa các **[[Cross-cutting concerns]]** – những chức năng **ảnh hưởng** đến nhiều phần khác nhau của ứng dụng nhưng **không** trực tiếp thuộc về **logic** **nghiệp** **vụ** cốt lõi.  AOP bổ sung cho OOP bằng cách cung cấp một cách để **tách biệt** các **mối quan tâm** này, giúp code sạch hơn, dễ bảo trì và mở rộng hơn.

**Các trường hợp AOP phát huy tác dụng:**

1. **Logging:** Ghi lại nhật ký hoạt động của ứng dụng.  AOP cho phép bạn ghi log tại các điểm cụ thể (ví dụ: trước và sau khi gọi một phương thức) mà không cần phải thêm code log trực tiếp vào phương thức đó.

2. **Security:** Xác thực và phân quyền người dùng.  AOP có thể được sử dụng để kiểm tra quyền truy cập của người dùng trước khi cho phép họ thực hiện một hành động nào đó.  Ví dụ: kiểm tra xem người dùng đã đăng nhập hay chưa, có đủ quyền để xem trang này hay không, v.v.

3. **Caching:** Lưu trữ dữ liệu tạm thời để tăng hiệu suất.  AOP có thể được sử dụng để cache kết quả của một phương thức, tránh việc phải tính toán lại nhiều lần.

4. **Transaction Management:** Quản lý các giao dịch database. AOP cho phép bạn đảm bảo tính nhất nguyên dữ liệu bằng cách tự động bắt đầu, commit hoặc rollback transaction.

5. **Exception Handling:** Xử lý các ngoại lệ. AOP có thể được sử dụng để bắt và xử lý các ngoại lệ một cách tập trung, tránh việc phải viết lại code xử lý ngoại lệ trong mỗi phương thức.

6. **Performance Monitoring:** Giám sát hiệu suất của ứng dụng.  AOP có thể được sử dụng để đo thời gian thực thi của các phương thức, giúp bạn xác định các điểm nghẽn hiệu suất.

7. **Data Validation:** Kiểm tra dữ liệu đầu vào. AOP có thể được sử dụng để kiểm tra tính hợp lệ của dữ liệu trước khi xử lý.


## ví dụ : 
Được rồi, hãy cùng xem ví dụ cụ thể về bài toán tính tổng a + b với cả hai cách: không dùng AOP và dùng AOP.

**Cách 1: Không dùng AOP**

```java
public class Calculator {

    public int sum(int a, int b) {
        System.out.println("Tham số đầu vào: a = " + a + ", b = " + b); // Log tham số đầu vào

        int sum = a + b;

        System.out.println("Kết quả: " + sum); // Log kết quả
        return sum;
    }

    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        int result = calculator.sum(5, 3);
    }
}
```

**Cách 2: Sử dụng AOP**

Đầu tiên, ta cần thêm các dependency cần thiết cho Spring AOP và (tùy chọn) Spring Context để quản lý bean:

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.0.9</version> </dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
    <version>6.0.9</version>
</dependency>

<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.19</version>
</dependency>
```

Tiếp theo, tạo Aspect:

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.Calculator.sum(..))")
    public void beforeSum(JoinPoint joinPoint) {
        Object[] args = joinPoint.getArgs();
        System.out.println("Tham số đầu vào: a = " + args[0] + ", b = " + args[1]);
    }

    @AfterReturning(pointcut = "execution(* com.example.Calculator.sum(..))", returning = "result")
    public void afterReturningSum(JoinPoint joinPoint, int result) {
        System.out.println("Kết quả: " + result);
    }
}
```

Và class `Calculator` (không cần `System.out.println` nữa):

```java
@Component
public class Calculator {

    public int sum(int a, int b) {
        return a + b;
    }
}
```

Cuối cùng, một class main để chạy ví dụ:

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@Configuration
@EnableAspectJAutoProxy
@ComponentScan("com.example") // Thay bằng package của bạn
public class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
        Calculator calculator = context.getBean(Calculator.class);
        calculator.sum(5, 3);
        context.close();
    }
}
```


**So sánh:**

* **Cách 1 (không AOP):** Code logging nằm lẫn với logic nghiệp vụ.
* **Cách 2 (AOP):** Logic logging được tách biệt trong `LoggingAspect`. `Calculator` chỉ tập trung vào logic tính toán.  Việc logging được thực hiện tự động bởi aspect mà không cần sửa đổi code của `Calculator`.


## ví dụ về phân quyền : 
**Không sử dụng AOP:**

```java
public class UserService {

    public void viewProfile(User user, int profileId) {
        if (user == null || !user.isLoggedIn()) { // Kiểm tra đăng nhập
            throw new SecurityException("Bạn cần đăng nhập để xem trang cá nhân.");
        }

        // Logic để lấy và hiển thị thông tin trang cá nhân
        System.out.println("Hiển thị trang cá nhân có ID: " + profileId);
    }


    public void editProfile(User user, Profile profile) {
        if (user == null || !user.isLoggedIn()) { // Kiểm tra đăng nhập
            throw new SecurityException("Bạn cần đăng nhập để chỉnh sửa trang cá nhân.");
        }

        if (!user.hasRole("ADMIN")) { // Kiểm tra quyền
            throw new SecurityException("Bạn không có quyền chỉnh sửa trang cá nhân.");
        }

        // Logic để chỉnh sửa thông tin trang cá nhân
        System.out.println("Chỉnh sửa trang cá nhân: " + profile.getName());

    }
}
```

Như bạn thấy, code kiểm tra security (đăng nhập và phân quyền) bị lặp lại ở mỗi phương thức.

**Sử dụng AOP:**

```java
@Aspect
@Component
public class SecurityAspect {

    @Before("execution(* com.example.UserService.*(..))")
    public void checkSecurity(JoinPoint joinPoint) {
        Object[] args = joinPoint.getArgs();
        User user = (User) args[0];

        if (user == null || !user.isLoggedIn()) {
            throw new SecurityException("Bạn cần đăng nhập để thực hiện hành động này.");
        }


        String methodName = joinPoint.getSignature().getName();
        if (methodName.equals("editProfile") && !user.hasRole("ADMIN")) {
                throw new SecurityException("Bạn không có quyền chỉnh sửa trang cá nhân.");
        }
    }
}


@Component
public class UserService {

    public void viewProfile(User user, int profileId) {
       // Logic để lấy và hiển thị thông tin trang cá nhân
        System.out.println("Hiển thị trang cá nhân có ID: " + profileId);
    }


    public void editProfile(User user, Profile profile) {
       // Logic để chỉnh sửa thông tin trang cá nhân
        System.out.println("Chỉnh sửa trang cá nhân: " + profile.getName());

    }
}
```

**Giải thích:**

* `SecurityAspect` là aspect xử lý security.  `@Before` advice sẽ được thực thi trước mỗi phương thức trong `UserService`.
* Code kiểm tra đăng nhập được đặt trong aspect.
* Code kiểm tra phân quyền cho `editProfile` cũng được đặt trong aspect.

**Tác dụng của AOP:**

* Code security được tách biệt khỏi logic nghiệp vụ của `UserService`, giúp code sạch hơn và dễ bảo trì hơn.
* Tránh trùng lặp code kiểm tra security.
* Dễ dàng thêm hoặc thay đổi chính sách security mà không cần sửa đổi code của `UserService`.

Với ví dụ này, bạn có thể thấy rõ ràng AOP giúp đơn giản hóa code và cải thiện khả năng bảo trì của ứng dụng như thế nào.  Code security được tập trung vào một chỗ, giúp dễ dàng quản lý và thay đổi.  `UserService` chỉ tập trung vào logic nghiệp vụ, không bị xen lẫn với code security.





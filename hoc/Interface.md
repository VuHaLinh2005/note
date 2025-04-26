
Interface trong Java là **một bản thiết kế**, **một hợp đồng**, hoặc một kiểu dữ liệu **trừu tượng**. Nó định nghĩa **một tập hợp các phương thức** (chỉ có khai báo, **không** có phần **thân code**) mà các class khác phải implement (triển khai).

**Đặc điểm chính của interface:**

* **Chỉ chứa khai báo phương thức:**  Trước Java 8, interface chỉ chứa khai báo phương thức và hằng số (biến `static final`). Từ Java 8, interface có thể chứa `default` methods và `static` methods (có phần thân code).  Từ Java 9, interface có thể chứa `private` methods.
* **Không thể khởi tạo trực tiếp:**  Bạn **không** thể dùng **`new` để tạo instance của interface.**  Bạn phải tạo **instance** của một class đã ***implement* interface** đó.
* **Hỗ trợ đa thừa kế:** Một class có thể implement nhiều interface cùng lúc. Điều này khác với class, class trong Java chỉ kế thừa được từ một class cha duy nhất.
* **Tính trừu tượng:** Interface thể hiện tính **trừu tượng** trong lập trình hướng đối tượng. Nó tập trung vào ***cái gì* cần làm**, chứ không phải ***làm như thế nào***.
* **Loose Coupling:**  Interface giúp **giảm sự phụ thuộc giữa** các thành phần trong chương trình.([[Interface và Dependency Injection#^03023c| xem thêm ở đây]])


**Khai báo interface:**

```java
interface MyInterface {
    void method1(); // Khai báo phương thức
    int CONSTANT = 10; // Hằng số (tương đương static final)

    default void method2() { // Default method (từ Java 8)
        System.out.println("Default method");
    }

    static void method3() { // Static method (từ Java 8)
        System.out.println("Static method");
    }

    private void method4() {  // Private method (từ Java 9)
        System.out.println("Private method");
    }
}
```


**Implement interface:**

```java
class MyClass implements MyInterface {
    @Override
    public void method1() {
        // Cài đặt phương thức method1
    }

    // Không cần implement method2, method3, method4 vì chúng đã có default implementation hoặc là static/private
}
```


**Sử dụng interface:**

```java
MyInterface obj = new MyClass();
obj.method1();
obj.method2();
MyInterface.method3(); // Gọi static method
```


**Tóm lại:** Interface là một công cụ quan trọng trong lập trình hướng đối tượng, giúp thiết kế code linh hoạt, dễ bảo trì và mở rộng. Nó là nền tảng cho các khái niệm như đa hình, dependency injection, và abstraction.

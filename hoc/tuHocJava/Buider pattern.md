
## Cách buider hoạt động

OK, mình sẽ tóm gọn cách **Builder Pattern** hoạt động với **từ khóa** **chính** và ví dụ siêu đơn giản để bạn nắm rõ!

### Cách Builder hoạt động (tóm gọn)
- **Từ khóa**: ***~={red}Gom data*=~** → ***~={red}Tạo=~** đối tượng*.
- **Cơ chế**: 
  1. Dùng một class `Builder` để *gom dữ liệu* từng bước (qua các phương thức).
  2. Khi đủ data, gọi `build()` để *tạo đối tượng chính* từ data đó.
- **Điểm nổi bật**: Đảm bảo đối tượng *hoàn chỉnh*, *dễ đọc*, *linh hoạt*.

### Ví dụ đơn giản nhất
Tạo một đối tượng `Car` với 2 thuộc tính: `color` (bắt buộc) và `engine` (tùy chọn).

```java
public class Car {
    private String color;  // Bắt buộc
    private String engine; // Tùy chọn

    // Constructor riêng tư, chỉ Builder dùng
    private Car(Builder builder) {
        this.color = builder.color;
        this.engine = builder.engine;
    }

    // Class Builder
    public static class Builder {
        private String color;
        private String engine;

        public Builder(String color) { // Bắt buộc color
            this.color = color;
        }

        public Builder engine(String engine) { // Tùy chọn engine
            this.engine = engine;
            return this;
        }

        public Car build() { // Tạo Car từ data đã gom
            return new Car(this);
        }
    }
}
```

**Cách dùng**:
```java
Car car = new Car.Builder("red") // Gom data: color
    .engine("V8")               // Gom data: engine
    .build();                   // Tạo Car
```

Hoặc đơn giản hơn:
```java
Car basicCar = new Car.Builder("blue").build(); // Chỉ cần color
```


### Cách bình thường (dùng constructor hoặc setter) gặp vấn đề gì?
1. **Constructor dài dòng và khó đọc**:
   - Giả sử `Pizza` có 5 thuộc tính: size, crust, topping, cheese, sauce. Constructor sẽ là:
     ```java
     Pizza pizza = new Pizza("large", "thin", "pepperoni", "extra cheese", true);
     ```
     - Nếu có 10 thuộc tính thì sao? Constructor siêu dài, dễ nhầm thứ tự tham số.
     - Muốn thêm thuộc tính mới (như "spicy level"), phải sửa constructor và mọi chỗ dùng nó.

2. **Constructor quá tải (overloading)**:
   - Để linh hoạt, bạn phải tạo nhiều constructor:
     ```java
     Pizza(String size)
     Pizza(String size, String topping)
     Pizza(String size, String topping, String cheese)
     ```
     - Càng nhiều thuộc tính, số lượng constructor tăng vọt, code lặp lại nhiều.

3. **Setter gây trạng thái không nhất quán**:
   - Nếu dùng setter:
     ```java
     Pizza pizza = new Pizza();
     pizza.setSize("large");
     pizza.setTopping("pepperoni");
     ```
     - Vấn đề: Sau khi tạo `pizza`, nó có thể ở trạng thái "nửa vời" (chưa có size mà đã dùng được). Điều này nguy hiểm trong hệ thống lớn, nơi đối tượng cần hoàn chỉnh ngay từ đầu.

4. **Không bắt buộc được thuộc tính cần thiết**:
   - Ví dụ size là bắt buộc, nhưng với setter, bạn không ép được người dùng phải set nó.

### Builder Pattern giải quyết thế nào?
- **~={red}Dễ đọc=~ và mở rộng**: Bạn **~={red}set=~** từng thứ một, **~={red}không=~** cần nhớ **~={red}thứ tự=~** tham số. Thêm thuộc tính mới chỉ cần thêm phương thức vào Builder.
- **Kiểm soát được quá trình tạo**: Đối tượng chỉ được tạo khi gọi `build()`, đảm bảo hoàn chỉnh.
- **Bắt buộc thuộc tính cần thiết**: Ví dụ, `PizzaBuilder` yêu cầu `size` trong constructor của nó, không ai quên được.

### Ví dụ so sánh
**Cách bình thường (constructor)**:
```java
Pizza pizza = new Pizza("large", "thin", "pepperoni", null, true);
// Nếu quên tham số hoặc truyền null thì sao? Rối!
```

**Builder**:
```java
Pizza pizza = new Pizza.Builder("large") // Size bắt buộc
    .topping("pepperoni")
    .crust("thin")
    .sauce(true)
    .build();
```
- Dài hơn thật, nhưng rõ ràng, không sợ nhầm, dễ bảo trì.

### Khi nào Builder dài hơn nhưng đáng giá?
- Khi đối tượng có **nhiều thuộc tính** (5-10 cái trở lên).
- Khi cần **tùy chỉnh linh hoạt** (không phải lúc nào cũng set hết mọi thứ).
- Khi làm việc trong **dự án lớn**, cần code dễ đọc và ít lỗi.

### Khi nào không cần Builder?
- Nếu đối tượng chỉ có 1-2 thuộc tính, dùng constructor bình thường là đủ, Builder sẽ thừa thãi.
 
Các cách sử dụng @Autowired annotation trong Spring

December 16, 2020

Mục lục \[[ẩn](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#)\]

-   [1 Kích hoạt @Autowired annotation trong Spring](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Kich_hoat_Autowired_annotation_trong_Spring)
-   [2 Cách sử dụng @Autowired](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Cach_su_dung_Autowired)
    -   [2.1 @Autowired trực tiếp trên thuộc tính](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowirednbsptruc_tiep_tren_thuoc_tinh)
    -   [2.2 @Autowired trên setter method](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowired_tren_setter_method)
    -   [2.3 @Autowired constructor](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowired_constructor)
-   [3 @Autowired với các optional dependency](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowired_voi_cac_optional_dependency)
-   [4 Các trường lỗi khi sử dụng @Autowired](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Cac_truong_loi_khi_su_dung_Autowired)
    -   [4.1 @Autowired với @Qualifier](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowired_voi_Qualifier)
    -   [4.2 Autowired by name](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Autowired_by_name)
-   [5 Kết bài](https://shareprogramming.net/cac-cach-su-dung-autowired-annotation-trong-spring/#Ket_bai)

Bắt đầu từ Spring 2.5, framework đã giới thiệu một annotation mới _@Autowired_ cho phép Spring tự động tìm kiếm và tiêm các bean tương ứng mà chúng ta đã khai báo trong class.

Trong bài viết này chúng sẽ cùng nhau tìm hiểu một số cách sử dụng _@Autowired_ annotation trong Spring và cách để xử lý xung đột khi có nhiều hơn một bean có thể sử dụng trong một class cụ thể.

## Kích hoạt @Autowired annotation trong Spring

Spring cho phép tự động tiêm các dependency cách tự động, vì vậy chúng ta chỉ cần [khai báo bean](https://shareprogramming.net//tai-sao-spring-bean-duoc-goi-la-xuong-song-cua-ung-dung/) bên trong các file cấu hình với _@Bean_ annotation hay các class được chú thích với _@Component_ annotation, [Spring IoC container](https://shareprogramming.net//gioi-thieu-inversion-of-control-va-dependency-injection-trong-spring/) sẽ tự động tiêm các dependency tương ứng mà chúng ta đã khai báo để sử dụng. 

Ví dụ dưới đây mình tạo Company bean thông qua _@ComponentScan_ (được dùng để chỉ ra những nơi mà nó cần tìm những @Component class) và _Address_ bean được đặt trong file cấu hình (được chú thích với _@Configuration_ annotation)

```js
public Company(Address address) {

// getter, setter and other properties

@ComponentScan(basePackageClasses = Company.class)

public Address getAddress() {

return new Address("High Street", 1000);
```

Hơn ngoài mong đợi, với Spring Boot bạn chỉ cần sử dụng _@SpringBootApplication_ annotation. Nó là một annotation kết hợp _@Configuration_, _@EnableAutoConfiguration_, và _@ComponentScan._ Thông thường nó được dùng với Main class trong ứng dụng Spring Boot, chỉ định cho Spring sẽ tìm kiếm các bean cùng cấp hoặc thuộc các package con của Main class.

```js
public class AutowiredDemoApplication {

public static void main(String\[\] args) {

SpringApplication.run(AutowiredDemoApplication.class, args);

```
## Cách sử dụng @Autowired

Sau khi các bean đã được khởi tạo và đăng ký với Spring IoC, giờ đây bạn có thể sử dụng _@Autowired_ để tiêm các bean tương ứng cần sử dụng. Spring cung cấp cho chúng ta 3 cách để sử dụng _@Autowired_ annotation hoặc là chú thích trên _contructor_, _setter_ hay trực tiếp trên thuộc tính.

### _@Autowired_ trực tiếp trên thuộc tính

Đây là cách sử dụng nhanh và ngắn gọn nhất, chúng ta chỉ cần chú thích _@Autowired_ trực tiếp trên thuộc tính. Spring IoC sẽ tự động tìm kiếm và tiêm bean tương ứng thông qua Reflection API.

Trước tiên, giả sử mình có một _ExampleClassBean_ bean như thế này

```js
public String getName() {

Sau đó mình tiến hành tiêm một _ExampleClassBean_ bean vào _ExampleService_ với _@Autowired_ được chú thích trên thuộc tính.

public interface FieldExampleService {

public class FieldExampleServiceImpl implements FieldExampleService {

private FieldBean fieldBean;

public String getName() {

return fieldBean.getName();
```

Giờ đây, chúng ta có thể kiểm tra với mong muốn khi gọi đến getName() method sẽ nhận về giá trị _“Deft Blog”_ như đã khai báo trước đó.

```js
class AutowiredDemoApplicationTests {

private FieldExampleService fieldExampleService;

public void propertyAutowiredTest() {

assertEquals(fieldExampleService.getName(), "Deft Blog");
```

### @Autowired trên setter method

Thông thường, _setter method_ được dùng để khởi tạo hay cập nhật giá trị của một thuộc tính trong class. Đây cũng là một nới lý tưởng để Spring có thể tiêm dependency vào.

```js
public class SetterBean {

Giờ, mình sẽ tạo một _SetterExampleService_ tiêm _SetterBean_ theo kiểu _setter method_.

public interface SetterExampleService {

public class SetterExampleServiceImpl implements SetterExampleService {

private SetterBean setterBean;

private void setBean(SetterBean setterBean) {

this.setterBean = setterBean;

return setterBean.getValue();

public void setterAutowiredTest() {

assertEquals(setterExampleService.getValue(), 10);
```

### @Autowired constructor

Cuối cùng, chúng ta có thể sử dụng @Autowired trên contructor, Spring sẽ tự động tìm kiếm các bean tương ứng được khai báo như là tham số trong constructor.

Trong ví dụ này mình sẽ sử dụng lại _FieldBean_ và _SetterBean_ là 2 tham số trong constructor, Spring sẽ tự động tìm kiếm 2 bean này vào service để sử dụng.

```js
public class ContructorExampleServiceImpl implements ConstructorExampleService {

private final FieldBean fieldBean;

private final SetterBean setterBean;

public ContructorExampleServiceImpl(FieldBean fieldBean, SetterBean setterBean) {

this.fieldBean = fieldBean;

this.setterBean = setterBean;

return fieldBean.getName() + " - " + setterBean.getValue();

Các bạn có thể chạy unit-test sau để kiểm tra kết quả

public void constructorAutowiredTest() {

assertEquals(constructorExampleService.print(), "Deft Blog - 10");
```

## @Autowired với các optional dependency

Khi Spring không thể tìm thấy bean trong container để tiêm chúng vào nơi cần sử dụng, nó sẽ ném ra một [exception](https://shareprogramming.net//qua-trinh-lan-truyen-exception-trong-java/) khiến chương trình không thể khởi chạy.

Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException:

No qualifying bean of type \[com.autowire.sample.FooDAO\] found for dependency:

expected at least 1 bean which qualifies as autowire candidate for this dependency.

{@org.springframework.beans.factory.annotation.Autowired(required=true)}

Để khắc phục lỗi này, chúng ta có thể sử dụng thuộc tính required trong _@Autowired_ annotation chuyển nó thành FALSE, mặc định là TRUE sẽ gây ra lỗi khi một dependency được chú thích với _@Autowired_ annotation không được tìm thấy.

public class FieldExampleServiceImpl implements FieldExampleService {

@Autowired(required = false)

private FieldBean fieldBean;

Nhưng trong thực tế, cách này thường khá ít sử dụng. Thông thường, các bạn phải đảm bảo các bean được tạo đủ trong quá trình chạy ứng dụng.

## Các trường lỗi khi sử dụng @Autowired

Mặc định, Spring sẽ tìm kiếm các dependency được chú thích bởi _@Autowired_ annotation theo kiểu dữ liệu. Nếu có nhiều hơn một bean có cùng kiểu dữ liệu trong container nó sẽ ném ra một exception.

Để xử lý cho trường hợp xung đột này, chúng ta phải chỉ định rõ bean nào chúng ta đang cần dùng trong số những bean có cùng kiểu dữ liệu đang tồn tại trong container.

### @Autowired với @Qualifier

Đây là một thông dụng dùng để chỉ rõ bean chúng ta cần dùng trong số nhiều bean có cùng kiểu dữ liệu.

Giả sử mình có một Formatter cùng với 2 bean đều implement từ nó

```js
public interface Formatter {

public class BarFormatter implements Formatter {

public class FooFormatter implements Formatter {
```

Trong trường hợp trên, chúng ta có đến 2 bean có cùng kiểu dữ liệu _Formatter_, nên khi mình khởi tạo ConflictServiceExample service với một dependency Formatter thì gây ra lỗi

> No qualifying bean of type ‘com.deft.autowireddemo.conflict.Formatter’ available: expected single matching bean but found 2: bar,foo  
> at org.springframework.beans.factory.config.DependencyDescriptor.resolveNotUnique(DependencyDescriptor.java:220)

public class ConflictServiceExample {

private Formatter formatter;

return formatter.format()

Để tránh trường hợp xung đột này, chúng ta có thể sử dụng @Qualifier để chỉ rõ tên của bean muốn sử dụng.

public class ConflictServiceExample {

private Formatter formatter;

return formatter.format()

### Autowired by name

Spring sử dụng tên của bean làm giá trị mặc định trong _@Qualifier._ Nghĩa là khi chúng ta khai báo

private Formatter formatter;

Thì có thể ngầm hiểu như 

private Formatter formatter;

Vì trong trường hợp này, không có bean nào có tên tương tự nên Spring chỉ tìm theo kiểu dữ liệu và tìm ra được 2 bean _foo_ và _bar_ tương ứng.

Do vậy, các bạn có thể không dùng _@Qualifier_ annotation mà chỉ cần thay đổi tên tương ứng với tên của bean cần sử dụng.

Như đoạn code dưới đây, mình sử dụng foo bean mà không cần sử dụng _@Qualifier_ mà chỉ cần thay đổi tên thuộc tính tương ứng với _@Component_ name đã đặt trước đó (foo)

public class ConflictByNameServiceExample {

## Kết bài

Qua bài viết này, chúng ta sẽ biết được cách sử dụng _@Autowired_ để tiêm các dependency tự động. Có tới 3 cách áp dụng @Autowired tuy nhiên, thiên hạ đồn rằng nên sử dụng **constructor autowired** vì nó cho tốc độ nhanh hơn là dùng field autowired phải dùng reflection để khởi tạo. Không những vậy, khi sử dụng constructor mà các tham số quá nhiều, nghĩa là chúng ta có thể đang vi phạm nguyên tắc SOLID vì nhiều dependency đồng nghĩa với việc class của chúng ta đang chịu trách nhiệm xử lý quá nhiều logic.

Sau cùng các bạn có thể xem mã nguồn mình công khai trên gitlab để chạy và kiểm thử nếu cần thiết: [autowired-demo](https://github.com/devjoyvn/spring_tutorials/tree/master/autowired-demo). 

Nguồn tham khảo

https://www.baeldung.com/spring-autowire
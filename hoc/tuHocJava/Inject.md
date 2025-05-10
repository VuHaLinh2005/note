Chính xác! Inject (tiêm) bao gồm hai bước:

1. **Khởi tạo instance:** DI container sẽ tạo một instance của class cụ thể (implementation của interface).  Giống như bạn dùng **`new MyServiceImpl()`** vậy.

2. **Tiêm (inject) instance vào dependency:** DI container sẽ lấy instance vừa tạo và "tiêm" nó vào constructor (hoặc setter method) của class **cần dependency** đó (ví dụ: `BuildingApi`).  Nói cách khác, **DI container** sẽ truyền instance đó như một argument cho constructor của `BuildingApi`.

Vì vậy, "inject" là toàn bộ quá trình bao gồm cả khởi tạo instance và truyền instance đó vào dependency.  "**Tiêm**" chỉ là cách diễn đạt hình tượng cho việc **truyền instance vào dependency**.


Ví dụ, với đoạn code:

```java
public class BuildingApi {

    private final BuildingService buildingService;

    public BuildingApi(BuildingService buildingService) {
        this.buildingService = buildingService;
    }
}
```

Và một implementation:

```java
@Service
public class BuildingServiceImpl implements BuildingService {
    // ...
}
```
 




 



## name ?

Đúng rồi! Trong Vue Router, thuộc tính `name` được sử dụng để xác định đúng **route** mà bạn muốn điều hướng đến. Khi bạn sử dụng `router.push`, bạn có thể chỉ định tên của route thay vì sử dụng trực tiếp URL hoặc `path`.

### Cách hoạt động của `name` trong Vue Router:

- `name: 'detailSanPham'` là tên của route mà bạn muốn điều hướng đến. Tên này phải **khớp chính xác** với tên mà bạn đã khai báo trong cấu hình routes của Vue Router.
- Việc sử dụng `name` giúp bạn dễ dàng quản lý và điều hướng đến các routes mà không cần phải lo lắng về việc thay đổi URL hoặc path.

### Ví dụ về cách khai báo route với `name`:

```js
const routes = [
  {
    path: '/detailSanPham',        // Định nghĩa path của route
    name: 'detailSanPham',         // Tên route
    component: ProductDetailComponent // Component tương ứng với route này
  }
];

```

Khi bạn điều hướng bằng `router.push` với `name`, Vue Router sẽ tự động tìm route có tên `'detailSanPham'` và chuyển hướng đến path tương ứng mà bạn đã khai báo.

### Ví dụ sử dụng `name` trong `router.push`:

```js
router.push({
  name: 'detailSanPham',  // Điều hướng tới route có tên 'detailSanPham'
  query: { id: product.id } // Truyền tham số query
})

```

Điều này sẽ khiến Vue Router tự động tìm route có tên `'detailSanPham'` và tạo URL tương ứng với path của route đó (ví dụ `/detailSanPham?id=123`).

### Ưu điểm của việc sử dụng `name`:

1. **Tính linh hoạt**: Bạn không cần phải sửa lại tất cả các điểm điều hướng nếu thay đổi path của route. Chỉ cần thay đổi tên route trong một lần khai báo, mà không cần phải thay đổi URL trong toàn bộ ứng dụng.--> giống việc không truyền verb vào url in spring
2. **Dễ dàng bảo trì**: Việc sử dụng tên giúp mã dễ hiểu và dễ bảo trì, đặc biệt là khi ứng dụng có nhiều route.

Tóm lại, việc sử dụng `name` trong `router.push` là cách để bạn điều hướng đến đúng route trong Vue Router.


## router ??

Không, **router** không phải là một URL, nhưng **router** giúp bạn quản lý và điều hướng các **URL** trong ứng dụng của bạn.

Cụ thể hơn, trong Vue.js (và nhiều framework JavaScript khác), **Vue Router** là một công cụ cho phép bạn xác định các route (tức là các đường dẫn) trong ứng dụng của mình, và điều hướng người dùng giữa các view (giao diện) khác nhau dựa trên URL.

### Router là gì?

- **Router** trong Vue.js là một công cụ giúp bạn xử lý việc điều hướng trong ứng dụng. Nó xác định và quản lý các **route** (đường dẫn) và **component** (component tương ứng với mỗi route).
- **Router** giúp bạn xác định các URL mà người dùng có thể truy cập trong ứng dụng, đồng thời liên kết các URL này với các component khác nhau.

### Cách hoạt động của Vue Router:

- Khi người dùng truy cập một **URL**, Vue Router sẽ kiểm tra **route** tương ứng và hiển thị **component** phù hợp.
- Bạn có thể xác định nhiều **routes** trong cấu hình của Vue Router, mỗi route sẽ có một **path** (đường dẫn) và một **component**. Khi người dùng truy cập một đường dẫn, Vue Router sẽ chuyển đến **component** đó.

### Cách hoạt động của một URL trong Vue Router:

Ví dụ, giả sử bạn có một ứng dụng với các route như sau:
```js
const routes = [
  {
    path: '/home',          // Đường dẫn (URL) cho trang chủ
    name: 'home',
    component: HomePage     // Component hiển thị khi truy cập /home
  },
  {
    path: '/product/:id',   // Đường dẫn cho trang chi tiết sản phẩm
    name: 'productDetail',
    component: ProductDetailPage // Component hiển thị khi truy cập /product/:id
  }
]

```

### Tóm lại:

- **Router** không phải là URL, nhưng nó giúp **quản lý** các **URL** trong ứng dụng và quyết định **component** nào sẽ được hiển thị khi người dùng truy cập vào các URL đó.


## truyền tham số

Để làm rõ sự khác nhau giữa việc truyền tham số kiểu **`query`** và **`params`** trong Vue Router, ta sẽ so sánh hai phương pháp này qua cách thức sử dụng và cách thức dữ liệu được thể hiện trong URL.

### 1. Truyền tham số kiểu `query`

Khi bạn truyền tham số qua **query** trong Vue Router, các tham số này sẽ được đính kèm vào URL dưới dạng **query string**, sau dấu `?` trong URL.

#### Cách sử dụng:

- **Dùng `query`** khi bạn muốn truyền tham số qua URL mà không cần thay đổi cấu trúc của đường dẫn (`path`).
- **Tham số được truyền dưới dạng cặp `key=value`** trong URL và có thể có nhiều tham số, được phân cách nhau bằng dấu `&`.

#### Ví dụ sử dụng `query`:

```js
router.push({
  name: 'productDetail',
  query: { id: product.id, category: product.category }
});

```

```js
/productDetail?id=123&category=electronics

```

Ở đây:

- **`id=123`** và **`category=electronics`** là các tham số **query**.
- Bạn có thể truyền nhiều tham số và sẽ thấy chúng trong URL dưới dạng query string.

### 2. Truyền tham số kiểu `params`

Khi bạn truyền tham số qua **params**, tham số đó sẽ được đưa vào **path** của URL dưới dạng **segment**.

#### Cách sử dụng:

- **Dùng `params`** khi bạn muốn tham số trở thành một phần của đường dẫn (path) URL.
- Các tham số được **định nghĩa trực tiếp trong `path` của route** thông qua dấu `:` trong định nghĩa của `path` (ví dụ `/product/:id`).

#### Ví dụ sử dụng `params`:

```js
router.push({
  name: 'productDetail',
  params: { id: product.id }
});

```

url sẽ :
```js
/product/123

```

Ở đây:

- **`id=123`** là tham số **params** và nó trở thành một phần của đường dẫn URL.
- Tham số này sẽ không xuất hiện trong query string, mà nằm trong **URL path**.


### Khi nào sử dụng `query` và khi nào sử dụng `params`?

- **Sử dụng `query`**:(**chả ảnh hưởng url**)
    
    - Khi bạn muốn truyền tham số bổ sung, chẳng hạn như các bộ lọc, tìm kiếm hoặc các giá trị không phải là phần của URL chính.
    - Tham số trong `query` có thể thay đổi mà không ảnh hưởng đến cấu trúc của URL chính.
    - Ví dụ: tìm kiếm sản phẩm theo tên, lọc theo danh mục, sắp xếp kết quả...
    
    **Ví dụ:**
    ```js
    router.push({ name: 'products', query: { search: 'laptop', sort: 'price' } });
// URL: /products?search=laptop&sort=price

```
**Sử dụng `params`**:(**đường dẫn mới**)

- Khi tham số là một phần thiết yếu của URL và bạn muốn nó trở thành một phần không thể thiếu trong **cấu trúc đường dẫn**.
- Thường được dùng cho các tham số định danh, chẳng hạn như ID của sản phẩm, bài viết, hoặc trang.
- Ví dụ: Chi tiết sản phẩm theo ID, trang chi tiết bài viết, v.v.

### Tóm lại:

- **`query`**: Tham số sẽ được thêm vào URL sau dấu `?` và có thể có nhiều tham số. Đây là lựa chọn khi bạn muốn truyền các tham số bổ sung mà không thay đổi cấu trúc URL chính.
- **`params`**: Tham số sẽ là một phần của URL và được định nghĩa trong `path` của route. Đây là lựa chọn khi tham số là một phần thiết yếu của URL, chẳng hạn như ID hoặc các giá trị định danh khác.

| **Yếu tố**              | **Query**                                                                | **Params**                                                                 |
| ----------------------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| **Cấu trúc URL**        | `/path?key=value`                                                        | `/path/:key`                                                               |
| **Tham số trong URL**   | Sau dấu `?`, phân tách bởi `&`                                           | **Là một phần của URL path**(tức url phải có nó)                           |
| **Ví dụ URL**           | `/productDetail?id=123&category=elec`                                    | `/product/123`                                                             |
| **Sử dụng trong route** | Không cần phải định nghĩa trong `path`                                   | Cần định nghĩa tham số trong `path` (ví dụ: `/product/:id`)                |
| **Khi nào sử dụng?**    | Khi bạn muốn truyền tham số bổ sung mà không thay đổi cấu trúc đường dẫn | Khi tham số là một phần thiết yếu của URL và có thể thay đổi URL structure |
| **Truy xuất tham số**   | Truy xuất qua `this.$route.query`                                        | Truy xuất qua `this.$route.params`                                         |



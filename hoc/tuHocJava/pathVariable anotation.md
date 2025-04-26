
Khi bạn sử dụng **`@PathVariable`** để ánh xạ giá trị từ đường dẫn URL vào tham số của phương thức, Spring yêu cầu tên tham số trong URL phải khớp chính xác với tên tham số trong phương thức.


```js
@DeleteMapping(value="/api/building/{id1}/{name}")
public void deleteBuilding(@PathVariable int id, @PathVariable String name, @RequestParam String ward) {
    System.out.println("delete success id is : " + id);
    System.out.println("delete success name is : " + name);
    System.out.println("delete success ward is : " + ward);
}

```
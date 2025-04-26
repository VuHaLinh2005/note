 
`Collection<? extends GrantedAuthority>` có nghĩa là cần một `Collection` (như `List`, `Set`,...) chứa các phần tử là `GrantedAuthority` hoặc bất kỳ class nào kế thừa từ `GrantedAuthority`.

* **`Collection`**:  Đây là một interface trong Java Collections Framework, đại diện cho một nhóm các đối tượng.  `List` và `Set` là các implementation phổ biến của `Collection`.
* **`? extends GrantedAuthority`**: Đây là wildcard generics trong Java.  
    * **`?`**: **Wildcard**, đại diện cho một kiểu dữ liệu **chưa xác định**.
    * **`extends GrantedAuthority`**:  Wildcard này bị giới hạn bởi `GrantedAuthority`.  Nó có nghĩa là kiểu dữ liệu chưa xác định kia phải là `GrantedAuthority` **hoặc** một class **con** của `GrantedAuthority`.

 -- giới hạn chỉ đến : extends .

 
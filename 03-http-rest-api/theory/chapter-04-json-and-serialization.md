# Chapter 04: JSON & Serialization/Deserialization (Jackson)

## 1. JSON Format
```json
{
  "id": 1,
  "name": "Nguyễn Văn An",
  "email": "an@gmail.com",
  "age": 25,
  "active": true,
  "roles": ["USER", "ADMIN"],
  "address": { "city": "HCM", "district": "Q1" }
}
```
- **JSON Object**: `{}` chứa cặp `"key": value`.
- **JSON Array**: `[]` chứa danh sách giá trị.
- Value types: String, Number, Boolean, null, Object, Array.

## 2. Serialization & Deserialization
- **Serialization**: Java Object → JSON String (gửi response).
- **Deserialization**: JSON String → Java Object (nhận request body).
- Spring Boot dùng **Jackson** (tự động) để chuyển đổi.

```java
ObjectMapper mapper = new ObjectMapper();

// Serialize
User user = new User(1L, "An", "an@gmail.com");
String json = mapper.writeValueAsString(user);
// {"id":1,"name":"An","email":"an@gmail.com"}

// Deserialize
User parsed = mapper.readValue(json, User.class);
```

## 3. Jackson Annotations quan trọng
```java
public class UserDto {
    private Long id;

    @JsonProperty("full_name")           // Đổi tên field trong JSON
    private String name;

    @JsonIgnore                           // Ẩn field khỏi JSON
    private String password;

    @JsonFormat(pattern = "dd/MM/yyyy")   // Format ngày
    private LocalDate birthDate;

    @JsonInclude(JsonInclude.Include.NON_NULL)  // Ẩn field nếu null
    private String address;
}
```

| Annotation | Mục đích |
|-----------|---------|
| `@JsonProperty("name")` | Đổi tên field khi serialize/deserialize |
| `@JsonIgnore` | Bỏ qua field (không xuất ra JSON) |
| `@JsonFormat` | Format date/time |
| `@JsonInclude(NON_NULL)` | Không xuất field có giá trị null |
| `@JsonIgnoreProperties(ignoreUnknown=true)` | Bỏ qua field lạ khi deserialize |

## 4. Câu hỏi phỏng vấn & Trả lời chi tiết

### 4.1. Serialization và Deserialization là gì?
- **Serialization (Tuần tự hóa):**
  - Là quá trình chuyển đổi một **Đối tượng Java (Java Object)** trên bộ nhớ Heap thành một chuỗi dữ liệu định dạng văn bản (như **JSON String**) hoặc dòng byte (Byte Stream) để có thể truyền qua mạng Internet hoặc lưu xuống file/database.
  - Trong Spring Boot: Diễn ra tự động khi Controller return một Object $\rightarrow$ Jackson ObjectMapper biến đổi thành JSON gửi về cho Client.
- **Deserialization (Giải tuần tự hóa):**
  - Là quá trình ngược lại: Đọc một chuỗi dữ liệu (như **JSON String** gửi từ Client lên qua Request Body) và phân tích cú pháp (parse) để tái tạo lại thành một **Đối tượng Java (Java Object)** hợp lệ trên Heap.
  - Trong Spring Boot: Diễn ra tự động khi sử dụng annotation `@RequestBody UserDTO dto`.

### 4.2. Khi nào dùng `@JsonIgnore`? Cho ví dụ thực tế (Ẩn Password)
- **Mục đích:** Dùng để đánh dấu một trường dữ liệu (field) mà bạn **tuyệt đối không muốn xuất hiện** trong chuỗi JSON trả về cho Client, hoặc bỏ qua không đọc khi parse JSON.
- **Ví dụ thực tế:**
  ```java
  public class UserResponse {
      private Long id;
      private String username;
      private String email;

      @JsonIgnore
      private String passwordHash; // ❌ Không bao giờ để lộ mật khẩu đã mã hóa ra ngoài API!
  }
  ```
- **Ứng dụng khác:** Dùng để chặn vòng lặp tuần hoàn vô tận (Infinite Recursion) khi 2 Entity trong Hibernate có quan hệ 2 chiều (`@OneToMany` và `@ManyToOne` gọi qua lại lẫn nhau gây tràn bộ nhớ Stack).

### 4.3. `@JsonProperty` dùng để làm gì?
- **Mục đích:** Dùng để tùy biến ánh xạ (mapping) giữa **tên thuộc tính trong Java (theo quy tắc camelCase)** và **tên khóa trong chuỗi JSON (theo quy tắc snake_case hoặc chuẩn bên thứ 3)**.
- **Ví dụ:**
  ```java
  public class OrderDto {
      @JsonProperty("order_id")
      private Long orderId;

      @JsonProperty("customer_full_name")
      private String customerFullName;
  }
  ```
  Khi xuất ra JSON, key sẽ là `"order_id"` và `"customer_full_name"`.
- **Hỗ trợ quyền truy cập (Access control):**
  - `@JsonProperty(access = JsonProperty.Access.WRITE_ONLY)`: Chỉ cho phép nhận vào khi deserialize (tạo mới/cập nhật), nhưng khi serialize trả về response cho client thì tự động giấu đi (rất thích hợp cho trường `password`).

---
*Thực hành:* Thử dùng `ObjectMapper` của Jackson serialize một object có `@JsonIgnore` và `@JsonProperty` ra chuỗi JSON.

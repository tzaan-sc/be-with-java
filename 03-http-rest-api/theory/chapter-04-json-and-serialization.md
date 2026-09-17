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

## 4. Câu hỏi phỏng vấn
1. Serialization và Deserialization là gì?
2. Khi nào dùng `@JsonIgnore`? Cho ví dụ thực tế (ẩn password).
3. `@JsonProperty` dùng để làm gì?

---

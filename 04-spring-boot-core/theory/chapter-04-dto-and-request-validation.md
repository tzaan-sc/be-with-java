# Chapter 04: DTO Pattern & Bean Validation

## 1. DTO (Data Transfer Object)
- **Không** trả Entity/Database Model trực tiếp cho client (lộ cấu trúc DB, password, metadata).
- Tạo **DTO riêng** cho request (input) và response (output).

```java
// Request DTO (nhận dữ liệu từ client)
public class UserRequest {
    @NotBlank(message = "Tên không được để trống")
    @Size(min = 2, max = 50, message = "Tên từ 2-50 ký tự")
    private String name;

    @NotBlank @Email(message = "Email không hợp lệ")
    private String email;

    @NotBlank @Size(min = 6, message = "Mật khẩu ít nhất 6 ký tự")
    private String password;

    @Min(value = 1, message = "Tuổi phải ≥ 1")
    @Max(value = 150, message = "Tuổi phải ≤ 150")
    private int age;
}

// Response DTO (trả về cho client – KHÔNG có password)
public class UserResponse {
    private Long id;
    private String name;
    private String email;
    private int age;
    private LocalDateTime createdAt;
}
```

## 2. Ánh xạ Entity ↔ DTO
```java
// Thủ công (đơn giản, dễ hiểu)
public static UserResponse toResponse(UserEntity entity) {
    UserResponse dto = new UserResponse();
    dto.setId(entity.getId());
    dto.setName(entity.getName());
    dto.setEmail(entity.getEmail());
    dto.setAge(entity.getAge());
    dto.setCreatedAt(entity.getCreatedAt());
    return dto;
}

// Hoặc dùng thư viện: MapStruct, ModelMapper
```

## 3. Validation Annotations
| Annotation | Mô tả |
|-----------|-------|
| `@NotNull` | Không được null |
| `@NotEmpty` | Không null và không rỗng (`""`) |
| `@NotBlank` | Không null, không rỗng, không chỉ có khoảng trắng |
| `@Size(min, max)` | Giới hạn độ dài String/Collection |
| `@Min(value)` / `@Max(value)` | Giới hạn giá trị số |
| `@Email` | Phải đúng định dạng email |
| `@Pattern(regexp)` | Khớp regex |
| `@Positive` / `@PositiveOrZero` | Số dương / không âm |

## 4. Kích hoạt Validation
```java
@PostMapping
public ResponseEntity<UserResponse> createUser(@Valid @RequestBody UserRequest request) {
    // Nếu validation fail → Spring tự quăng MethodArgumentNotValidException
    return ResponseEntity.status(HttpStatus.CREATED).body(userService.createUser(request));
}
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Tại sao BẮT BUỘC phải dùng DTO thay vì trả trực tiếp Entity ra ngoài API?
Trả trực tiếp Entity (`@Entity User`) ra Controller là một cạm bẫy cực kỳ nguy hiểm trong Backend:
1. **Lỗ hổng bảo mật rò rỉ dữ liệu (Over-fetching & Security):** Entity chứa các cột nhạy cảm như `password_hash`, `salt`, `internal_notes`, `failed_login_attempts`. Nếu không có DTO, toàn bộ các trường này sẽ bị serialize thành JSON gửi về trình duyệt của người dùng!
2. **Lỗ hổng gán hàng loạt (Mass Assignment Vulnerability):** Khi nhận dữ liệu tạo mới/cập nhật, nếu hứng trực tiếp bằng Entity, kẻ xấu có thể gửi kèm JSON `{"role": "ADMIN", "balance": 999999}`. Nếu lười biễn lưu thẳng Entity, kẻ xấu sẽ tự nâng quyền của mình thành Admin. DTO hoạt động như một bộ lọc (Whitelist) chỉ cho phép những trường hợp lệ đi vào.
3. **Tránh lỗi tuần hoàn vô hạn (Circular Reference & LazyInitializationException):** Trong Hibernate, Entity `User` có thể chứa `List<Order>`, và `Order` lại chứa ngược lại `User`. Khi Jackson parse JSON sẽ văng lỗi `StackOverflowError` hoặc lỗi `LazyInitializationException` khi Session DB đã đóng.
4. **Tách biệt Database Schema và API Contract:** Bạn có thể tự do sửa đổi tên bảng, tách cột trong Database mà không sợ làm thay đổi cấu trúc JSON trả về cho Frontend (API Contract luôn ổn định).

### 5.2. `@NotNull` vs `@NotEmpty` vs `@NotBlank` khác nhau thế nào?
| Tiêu chí | `@NotNull` | `@NotEmpty` | `@NotBlank` (Khuyên dùng cho String) |
| :--- | :--- | :--- | :--- |
| **Áp dụng cho** | Mọi kiểu dữ liệu (Object, Number, Date, String). | `CharSequence`, `Collection`, `Map`, `Array`. | **Chỉ áp dụng cho chuỗi ký tự (`String`, `CharSequence`)**. |
| **`null`** | ❌ Báo lỗi | ❌ Báo lỗi | ❌ Báo lỗi |
| **`""` (Chuỗi rỗng độ dài 0)** | ✅ Hợp lệ (Cho qua) | ❌ Báo lỗi | ❌ Báo lỗi |
| **`"   "` (Chuỗi chỉ toàn dấu cách)**| ✅ Hợp lệ (Cho qua) | ✅ Hợp lệ (Cho qua vì length > 0) | ❌ **Báo lỗi** (Tự động `.trim()` trước khi kiểm tra) |
| **Thực tế:** Với các trường như `name`, `email`, `password`, **LUÔN DÙNG `@NotBlank`** để chặn người dùng nhập khoảng trắng vô nghĩa.

### 5.3. `@Valid` đặt ở đâu để kích hoạt Validation trong Spring Boot?
1. **Trên tham số Request Body của Controller:**
   ```java
   @PostMapping("/users")
   public ResponseEntity<?> create(@Valid @RequestBody UserCreateRequest request)
   ```
   Nếu dữ liệu vi phạm annotation (như `@NotBlank`, `@Min`), Spring sẽ chặn request lại và ném ra ngoại lệ `MethodArgumentNotValidException`.
2. **Trước các Object lồng nhau bên trong DTO (Nested Validation):**
   Nếu DTO chứa một đối tượng con hoặc danh sách con:
   ```java
   public class OrderRequest {
       @Valid // 👈 BẮT BUỘC phải có @Valid ở đây thì Spring mới duyệt sâu vào trong để kiểm tra các trường của OrderItemRequest!
       @NotEmpty
       private List<OrderItemRequest> items;
   }
   ```
3. **Trên Controller Class level (`@Validated`) khi validate PathVariable hoặc RequestParam:**
   ```java
   @RestController
   @Validated // 👈 Cần đặt trên Class
   public class UserController {
       @GetMapping("/{id}")
       public UserResponse getById(@PathVariable @Min(1) Long id) // Ném ConstraintViolationException nếu id < 1
   }
   ```

---
*Thực hành:* Tạo `UserRegisterRequest` có kiểm tra `@NotBlank` cho tên, `@Email` cho email, `@Size(min=8)` cho password, và bọc `@Valid` tại Controller.

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

## 5. Câu hỏi phỏng vấn
1. Tại sao cần DTO thay vì trả trực tiếp Entity?
2. `@NotNull` vs `@NotEmpty` vs `@NotBlank` khác nhau thế nào?
3. `@Valid` đặt ở đâu để kích hoạt validation?

---

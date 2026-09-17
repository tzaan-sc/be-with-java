# Chapter 02: JPA/Hibernate Basics – @Entity, @Id, @Column, @Table

## 1. ORM là gì?
- **Object-Relational Mapping**: Ánh xạ Java Class ↔ Database Table tự động.
- **JPA** (Jakarta Persistence API): Specification (chuẩn). **Hibernate**: Implementation phổ biến nhất.

## 2. Entity cơ bản
```java
@Entity
@Table(name = "users")
public class UserEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // Auto-increment
    private Long id;

    @Column(name = "full_name", nullable = false, length = 100)
    private String name;

    @Column(unique = true, nullable = false)
    private String email;

    @Enumerated(EnumType.STRING)  // Lưu enum dạng String (không phải ordinal)
    private Role role;            // enum Role { USER, ADMIN }

    @CreationTimestamp
    private LocalDateTime createdAt;

    @UpdateTimestamp
    private LocalDateTime updatedAt;
}
```

## 3. Annotation chính
| Annotation | Mô tả |
|-----------|-------|
| `@Entity` | Đánh dấu class là entity, map với table |
| `@Table(name)` | Đặt tên bảng (mặc định = tên class) |
| `@Id` | Primary Key |
| `@GeneratedValue` | Chiến lược sinh ID (IDENTITY, SEQUENCE, UUID) |
| `@Column` | Tuỳ chỉnh cột (name, nullable, unique, length) |
| `@Enumerated` | Lưu enum: `STRING` (khuyên dùng) hoặc `ORDINAL` |
| `@CreationTimestamp` | Tự gán thời gian khi INSERT |
| `@UpdateTimestamp` | Tự cập nhật thời gian khi UPDATE |
| `@Transient` | KHÔNG lưu vào DB |

## 4. Cấu hình kết nối (application.yml)
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb?useSSL=false&serverTimezone=UTC
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update   # create | create-drop | update | validate | none
    show-sql: true
    properties:
      hibernate.format_sql: true
```

## 5. ddl-auto modes
| Mode | Mô tả | Khi nào dùng |
|------|-------|-------------|
| `create` | Xoá + tạo lại bảng mỗi lần chạy | Test |
| `update` | Thêm cột/bảng mới, không xoá | Dev |
| `validate` | Chỉ kiểm tra schema khớp, không sửa | Staging/Prod |
| `none` | Không làm gì | Prod (dùng Flyway) |

## 6. Câu hỏi phỏng vấn
1. JPA và Hibernate khác nhau thế nào?
2. `ddl-auto: update` có an toàn cho production không?
3. `@Enumerated(STRING)` vs `@Enumerated(ORDINAL)` – tại sao nên dùng STRING?

---

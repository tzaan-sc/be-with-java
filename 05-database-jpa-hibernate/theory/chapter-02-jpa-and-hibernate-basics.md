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

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. JPA và Hibernate khác nhau thế nào?
- **JPA (Java Persistence API / Jakarta Persistence):**
  - Là một **Bộ tiêu chuẩn / Bản đặc tả giao diện (Specification)** do Oracle/Jakarta định nghĩa.
  - JPA chỉ bao gồm các **Interface** (`EntityManager`, `EntityTransaction`), các **Annotation** (`@Entity`, `@Id`, `@Table`) và các quy chuẩn lý thuyết. JPA hoàn toàn **không có mã nguồn thực thi bên dưới**. Bạn không thể chạy ứng dụng nếu chỉ có JPA.
- **Hibernate:**
  - Là một **Bộ khung triển khai cụ thể (Implementation / Provider)** của đặc tả JPA.
  - Hibernate chứa toàn bộ code thật sự để sinh câu lệnh SQL, quản lý kết nối, bộ đệm Session (First-level Cache, Second-level Cache), và thực thi giao tiếp với Database.
- $\rightarrow$ **Tóm lại:** JPA là chiếc "Vô lăng và Bàn đạp ga" chuẩn mực, còn Hibernate là "Động cơ xe" thực tế giúp cỗ máy vận hành bên dưới.

### 6.2. `ddl-auto: update` có an toàn cho Production không? Tại sao?
- **Khẳng định:** **TUYỆT ĐỐI KHÔNG BAO GIỜ DÙNG `ddl-auto: update` TRÊN PRODUCTION!**
- **Lý do:**
  1. **Không thể xóa cột hoặc đổi tên:** Nếu bạn đổi tên thuộc tính trong code từ `user_name` sang `full_name`, Hibernate sẽ tạo thêm 1 cột mới `full_name` và bỏ quên cột cũ `user_name`, làm dữ liệu cũ bị ngắt kết nối và phân mảnh.
  2. **Nguy cơ khóa bảng (Table Locking / Downtime):** Khi ứng dụng khởi động lại, lệnh `ALTER TABLE` tự động của Hibernate có thể khóa toàn bộ bảng dữ liệu hàng triệu dòng, gây nghẽn toàn bộ hệ thống đang phục vụ khách hàng.
  3. **Không kiểm soát được Version Database:** Không thể biết ai đã thay đổi cột gì, lúc mấy giờ, và không thể rollback (quay xe) khi có sự cố.
- **Giải pháp chuẩn công nghiệp trên Production:**
  - Cấu hình `spring.jpa.hibernate.ddl-auto = validate` hoặc `none`.
  - Quản lý lịch sử tiến hóa Database bằng các công cụ Migration chuyên nghiệp như **Flyway** hoặc **Liquibase**.

### 6.3. `@Enumerated(STRING)` vs `@Enumerated(ORDINAL)` – Tại sao BẮT BUỘC nên dùng `STRING`?
Giả sử bạn có Enum trạng thái đơn hàng:
```java
public enum OrderStatus {
    PENDING,   // Index 0
    SHIPPING,  // Index 1
    DELIVERED  // Index 2
}
```
- **Nếu dùng `@Enumerated(EnumType.ORDINAL)` (Mặc định của JPA):**
  - Hibernate sẽ lưu **số thứ tự index (0, 1, 2)** vào cột trong Database.
  - **THẢM HỌA XẢY RA KHI:** Sau này một lập trình viên thêm trạng thái mới `CANCELLED` chèn vào đầu hoặc giữa Enum:
    ```java
    public enum OrderStatus {
        PENDING, CANCELLED, SHIPPING, DELIVERED
    }
    ```
    Lúc này `CANCELLED` thành số 1, `SHIPPING` bị đẩy thành số 2! Toàn bộ các đơn hàng cũ trước đây đang lưu số 1 trong DB từ "Đang giao" bỗng nhiên biến thành "Đã hủy" $\rightarrow$ **Lệch toàn bộ dữ liệu kinh doanh!**
- **Khi dùng `@Enumerated(EnumType.STRING)`:**
  - Hibernate lưu thẳng chuỗi chữ: `"PENDING"`, `"SHIPPING"`, `"DELIVERED"` vào cột VARCHAR.
  - Dù bạn có đổi thứ tự, thêm bớt enum, dữ liệu trong Database vẫn nguyên vẹn 100% ngữ nghĩa và cực kỳ dễ đọc khi xem trực tiếp bằng SQL.

---
*Thực hành:* Tạo entity `Order` có trường Enum dùng `STRING`, cấu hình `ddl-auto: update` trên local và kiểm tra bảng sinh ra trong MySQL.

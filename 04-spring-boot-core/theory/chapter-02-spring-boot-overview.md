# Chapter 02: Spring Boot Overview – Auto-configuration, Starters, Config Properties

## 1. Spring Boot là gì?
- Framework giúp **khởi tạo nhanh** ứng dụng Spring mà không cần cấu hình XML phức tạp.
- Tích hợp sẵn **embedded server** (Tomcat), **auto-configuration**, **starter dependencies**.

## 2. Spring Boot Starters
| Starter | Mô tả |
|---------|-------|
| `spring-boot-starter-web` | REST API, Spring MVC, Tomcat |
| `spring-boot-starter-data-jpa` | JPA/Hibernate, Spring Data |
| `spring-boot-starter-security` | Spring Security |
| `spring-boot-starter-validation` | Bean Validation (Jakarta) |
| `spring-boot-starter-test` | JUnit 5, Mockito, MockMvc |

## 3. Auto-Configuration
- Spring Boot tự động cấu hình dựa trên **dependency có trong classpath**.
- Thêm `spring-boot-starter-data-jpa` + driver MySQL → tự cấu hình `DataSource`, `EntityManager`.
- Annotation `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.

## 4. File cấu hình

### application.properties
```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=123456
spring.jpa.hibernate.ddl-auto=update
```

### application.yml (khuyên dùng – dễ đọc hơn)
```yaml
server:
  port: 8081
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: 123456
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

## 5. Đọc cấu hình trong code

### @Value
```java
@Value("${server.port}")
private int port;

@Value("${app.jwt.secret-key}")
private String secretKey;
```

### @ConfigurationProperties (type-safe, khuyên dùng)
```java
@Configuration
@ConfigurationProperties(prefix = "app.jwt")
@Data  // Lombok
public class JwtProperties {
    private String secretKey;
    private long expiration;    // app.jwt.expiration
    private long refreshExpiration;
}
```

## 6. Profiles (Dev/Prod)
```yaml
# application-dev.yml
server:
  port: 8080
spring:
  jpa:
    show-sql: true

# application-prod.yml
server:
  port: 80
spring:
  jpa:
    show-sql: false
```
Chạy: `java -jar app.jar --spring.profiles.active=prod`

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Auto-configuration trong Spring Boot hoạt động như thế nào?
- **Bản chất:** Spring Boot tự động đoán xem ứng dụng của bạn cần những cấu hình nào dựa trên **các thư viện `.jar` có mặt trong classpath** và các Bean bạn đã tự định nghĩa.
- **Cơ chế hoạt động bên dưới:**
  1. File trung tâm: `@SpringBootApplication` bọc `@EnableAutoConfiguration`.
  2. Spring Boot đọc file cấu hình `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`.
  3. Sử dụng hàng loạt các annotation điều kiện **`@ConditionalOn...`**:
     - `@ConditionalOnClass(DataSource.class)`: Chỉ tự động cấu hình kết nối DB nếu tìm thấy driver trong classpath (ví dụ `mysql-connector-j`).
     - `@ConditionalOnMissingBean(DataSource.class)`: **Chỉ tự động tạo Bean mặc định nếu Developer CHƯA TỰ VIẾT bean đó**. Nếu bạn tự viết `@Bean DataSource`, Spring Boot sẽ nhường quyền ưu tiên cho bạn (Opinionated Defaults).
     - `@ConditionalOnProperty`: Bật/tắt cấu hình dựa vào cờ trong file `application.yml`.

### 7.2. So sánh `@Value` vs `@ConfigurationProperties`
| Tiêu chí | `@Value("${app.jwt.secret}")` | `@ConfigurationProperties(prefix = "app.jwt")` |
| :--- | :--- | :--- |
| **Cách tiếp cận** | Rời rạc, tiêm trực tiếp từng biến đơn lẻ. | **Gom cụm có cấu trúc thành một Class Java (Type-safe POJO)**. |
| **Kiểm tra kiểu (Type-Safety)** | Kém (dễ gõ sai chính tả chuỗi String key, lỗi chỉ ném ra lúc chạy). | **Rất cao**: Hỗ trợ validation (`@NotBlank`, `@Min`), tự động ép kiểu sang `Duration`, `DataSize`, `List`, `Map`. |
| **Relaxed Binding** | Rất hạn chế: Tên key phải khớp chính xác. | **Rất mạnh**: Tự động khớp `secret-key`, `secret_key`, `SECRET_KEY` vào trường `secretKey`. |
| **Khuyên dùng** | Chỉ dùng cho các biến đơn giản, lẻ tẻ (1-2 biến). | **Chuẩn Production**: Dùng cho mọi nhóm cấu hình phức tạp (JWT, AWS S3, Payment Gateway, Mail Server). |

### 7.3. Spring Boot Profile dùng để làm gì? Cách chuyển đổi trong thực tế?
- **Mục đích:** Tách biệt môi trường chạy của ứng dụng, cho phép cùng một bộ mã nguồn có thể chạy với các cấu hình cơ sở dữ liệu, cổng mạng và chế độ debug khác nhau trên từng môi trường:
  - `dev` (Development - Máy cá nhân lập trình viên): Cổng 8080, bật `show-sql: true`, dùng DB H2 hoặc MySQL local, level log `DEBUG`.
  - `test` / `staging` (Môi trường kiểm thử): Dùng DB giả lập trên Docker, kết nối Sandbox của bên thứ 3.
  - `prod` (Production - Thực tế phục vụ khách hàng): Tắt `show-sql`, dùng MySQL Cluster có bảo mật cao, pool kết nối HikariCP tối đa, level log `WARN/ERROR`.
- **Cách kích hoạt Profile trong thực tế:**
  1. Trong file cấu hình: `spring.profiles.active=prod`
  2. Bằng biến môi trường (Environment Variable trên Docker/K8s): `SPRING_PROFILES_ACTIVE=prod`
  3. Bằng tham số dòng lệnh khi chạy file Jar: `java -jar app.jar --spring.profiles.active=prod`

---
*Thực hành:* Tạo 2 file `application-dev.yml` và `application-prod.yml`, chạy thử với tham số `--spring.profiles.active=dev` để kiểm chứng.

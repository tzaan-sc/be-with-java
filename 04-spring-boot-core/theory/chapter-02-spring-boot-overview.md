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

## 7. Câu hỏi phỏng vấn
1. Auto-configuration hoạt động thế nào?
2. `@Value` vs `@ConfigurationProperties` khác nhau?
3. Spring Boot Profile dùng để làm gì?

---

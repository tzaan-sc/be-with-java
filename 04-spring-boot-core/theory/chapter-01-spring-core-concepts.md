# Chapter 01: Spring Core – IoC, Dependency Injection, Bean Lifecycle

## 1. IoC (Inversion of Control)
- Thay vì class **tự tạo** dependency (`new Service()`), Spring **quản lý và tiêm** (inject) dependency vào.
- **IoC Container** = `ApplicationContext`: quản lý vòng đời tất cả Bean.

## 2. Dependency Injection (DI) – 3 cách

### Constructor Injection ✅ (Khuyên dùng)
```java
@Service
public class UserService {
    private final UserRepository userRepository;  // final = immutable

    public UserService(UserRepository userRepository) {  // Spring tự inject
        this.userRepository = userRepository;
    }
}
// Với Lombok: @RequiredArgsConstructor thay constructor
```

### Field Injection ❌ (Không khuyên dùng)
```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;  // Khó viết unit test
}
```

### Setter Injection (Ít dùng)
```java
@Autowired
public void setUserRepository(UserRepository repo) { this.userRepository = repo; }
```

> **Tại sao Constructor Injection tốt nhất?** Hỗ trợ `final` (immutable), dễ viết Unit Test (truyền mock qua constructor), phát hiện circular dependency sớm.

## 3. Stereotype Annotations
| Annotation | Dùng cho | Ý nghĩa |
|-----------|---------|---------|
| `@Component` | Class bất kỳ | Đánh dấu là Bean |
| `@Service` | Business Logic | Tầng Service |
| `@Repository` | Data Access | Tầng Repository (tự dịch DB exception) |
| `@Controller` | MVC Controller | Trả view (HTML) |
| `@RestController` | REST API | = `@Controller` + `@ResponseBody` |
| `@Configuration` | Cấu hình | Khai báo `@Bean` methods |

## 4. @Bean vs @Component
```java
// @Component: Đánh dấu class của MÌNH
@Component
public class EmailService { }

// @Bean: Khai báo Bean từ THƯ VIỆN BÊN NGOÀI (không sửa được source code)
@Configuration
public class AppConfig {
    @Bean
    public ObjectMapper objectMapper() {
        return new ObjectMapper().registerModule(new JavaTimeModule());
    }
}
```

## 5. @Qualifier & @Primary
```java
// Khi có 2 Bean cùng kiểu → xung đột
@Service("vnpay")
public class VnPayService implements PaymentService { }

@Service("momo")
public class MomoService implements PaymentService { }

// Giải quyết bằng @Qualifier
@Service
public class OrderService {
    public OrderService(@Qualifier("vnpay") PaymentService payment) { }
}

// Hoặc @Primary: Bean mặc định
@Primary @Service
public class VnPayService implements PaymentService { }
```

## 6. Bean Scope
| Scope | Mô tả |
|-------|-------|
| `singleton` (mặc định) | 1 instance duy nhất trong toàn bộ Application Context |
| `prototype` | Tạo instance mới mỗi lần inject/getBean |
| `request` | 1 instance mỗi HTTP request (Web) |
| `session` | 1 instance mỗi HTTP session (Web) |

## 7. Bean Lifecycle
```
Constructor → @PostConstruct → Sử dụng → @PreDestroy → Huỷ
```

## 8. Câu hỏi phỏng vấn
1. IoC và DI là gì? Liên quan thế nào?
2. Tại sao khuyên dùng Constructor Injection?
3. `@Component` vs `@Bean` khác nhau thế nào?
4. Bean Scope mặc định là gì? Singleton có vấn đề gì trong multi-thread?

---

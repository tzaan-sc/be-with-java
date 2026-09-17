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

## 8. Câu hỏi phỏng vấn & Trả lời chi tiết

### 8.1. IoC và DI là gì? Chúng liên quan mật thiết với nhau như thế nào?
- **Inversion of Control (IoC - Đảo ngược điều khiển):**
  - Là một **nguyên lý thiết kế kiến trúc (Design Principle)**.
  - *Truyền thống:* Lập trình viên tự chủ động quản lý vòng đời và tự tay `new ClassB()` bên trong `ClassA`.
  - *IoC:* Quyền kiểm soát việc khởi tạo, cấu hình và quản lý vòng đời của các đối tượng được "chuyển giao" (inversion) cho một bên thứ ba quản lý — đó chính là **Spring IoC Container**.
- **Dependency Injection (DI - Tiêm phụ thuộc):**
  - Là **mẫu thiết kế (Design Pattern) cụ thể** dùng để **hiện thực hóa nguyên lý IoC**.
  - Thay vì class tự đi tìm hoặc tạo ra phụ thuộc, Spring Container sẽ chủ động "tiêm" (inject) phụ thuộc đó vào class thông qua Constructor, Setter hoặc Field.
- $\rightarrow$ **Mối quan hệ:** IoC là tư tưởng/mục tiêu, còn DI là công cụ/hành động cụ thể để đạt được mục tiêu đó.

### 8.2. Tại sao Spring khuyên dùng Constructor Injection thay vì Field Injection (`@Autowired`)?
Field Injection (`@Autowired private UserService userService;`) tuy viết ngắn hơn nhưng bị coi là **Code Smell (Anti-pattern)** vì 4 lý do:
1. **Bất biến (Immutability):** Constructor Injection cho phép khai báo thuộc tính là `private final`, đảm bảo dependency không bao giờ bị thay đổi hay mang giá trị `null` sau khi khởi tạo.
2. **Dễ viết Unit Test:** Với Constructor Injection, ta có thể dễ dàng khởi tạo class và truyền Mock Object vào bằng tay (`new OrderService(mockRepo)`) mà không cần phải dùng Reflection hoặc khởi động cả Spring Context nặng nề.
3. **Phát hiện Circular Dependency (Phụ thuộc vòng):** Nếu Bean A cần Bean B và Bean B lại cần Bean A, Constructor Injection sẽ khiến Spring báo lỗi ngay lập tức lúc khởi động app, ép developer phải sửa thiết kế code thay vì để lỗi âm thầm lúc runtime.
4. **Ngăn chặn vi phạm SRP:** Nếu 1 class có constructor nhận tới 8-10 tham số, bạn sẽ lập tức nhận ra class này đang ôm đồm quá nhiều việc (vi phạm Single Responsibility Principle) để refactor sớm.

### 8.3. `@Component` vs `@Bean` khác nhau thế nào?
| Tiêu chí | `@Component` (kèm `@Service`, `@Repository`, `@Controller`) | `@Bean` |
| :--- | :--- | :--- |
| **Vị trí áp dụng** | Đặt trên **Class level** (đầu file class). | Đặt trên **Method level** bên trong class cấu hình `@Configuration`. |
| **Cơ chế phát hiện** | Spring tự động phát hiện thông qua tính năng **Component Scanning** (`@ComponentScan`). | Lập trình viên chủ động viết phương thức trả về instance và đánh dấu `@Bean`. |
| **Quyền sở hữu mã nguồn** | Dùng cho **code do chính bạn viết trong dự án** (có quyền mở file thêm annotation). | **Bắt buộc dùng khi tích hợp thư viện bên thứ 3** (ví dụ: cấu hình `RestTemplate`, `ModelMapper`, `BCryptPasswordEncoder` - những class trong file `.jar` có sẵn mà bạn không thể sửa code để thêm `@Component`). |
| **Tùy biến khởi tạo** | Khởi tạo tự động mặc định. | Cực kỳ linh hoạt: Bạn có thể viết logic điều kiện (`if-else`), đọc biến môi trường để tùy biến cách khởi tạo object. |

### 8.4. Bean Scope mặc định là gì? Singleton Scope có vấn đề gì trong Multi-threading?
- **Bean Scope mặc định trong Spring:** Là **`Singleton`** (Toàn bộ Spring IoC Container chỉ tạo và quản lý duy nhất **1 instance** của Bean đó trong suốt vòng đời ứng dụng).
- **Vấn đề tiềm ẩn trong môi trường Đa luồng (Multi-threading):**
  - Mặc định mỗi HTTP request từ người dùng gửi tới Tomcat sẽ được phục vụ bởi một **Thread riêng biệt**.
  - Cả 100 thread này sẽ **cùng lúc gọi vào phương thức của DUY NHẤT 1 instance Singleton Bean** (Controller hoặc Service).
  - **NGUY HIỂM:** Nếu bạn khai báo **Biến trạng thái có thể thay đổi (Mutable State / Instance Variable)** bên trong Bean:
    ```java
    @Service
    public class OrderService {
        private Long currentUserId; // ❌ CHẾT NGƯỜI: Nhiều thread cùng ghi đè biến này!
    }
    ```
    Luồng của User A sẽ đọc nhầm `currentUserId` của User B $\rightarrow$ Lộ dữ liệu chéo (Race Condition / Thread-safety bug).
- **Quy tắc vàng:** Các Bean Spring (Service, Controller, Repository) **bắt buộc phải là STATELESS** (không chứa biến instance lưu trạng thái người dùng; mọi dữ liệu phải truyền qua tham số hàm cục bộ nằm trên Stack của từng Thread).

---
*Thực hành:* Tạo 1 Service dùng Constructor Injection với `@RequiredArgsConstructor` của Lombok, thử nghiệm in Hashcode của Bean để thấy tính chất Singleton.

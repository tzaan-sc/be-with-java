# Chapter 03: 5 Nguyên Lý SOLID trong Java Backend

## Tổng quan
SOLID là 5 nguyên lý thiết kế hướng đối tượng giúp code **dễ bảo trì**, **dễ mở rộng** và **dễ test**.

## 1. S – Single Responsibility Principle (SRP)
> Mỗi class chỉ có **một lý do duy nhất để thay đổi** (một nhiệm vụ duy nhất).

```java
// ❌ Vi phạm SRP: UserService vừa xử lý user, vừa gửi email, vừa ghi log
public class UserService {
    public void createUser(User user) { /* lưu DB */ }
    public void sendWelcomeEmail(User user) { /* gửi email */ }
    public void writeLog(String message) { /* ghi log */ }
}

// ✅ Tuân thủ SRP: Mỗi class 1 nhiệm vụ
public class UserService { public void createUser(User user) { /* lưu DB */ } }
public class EmailService { public void sendEmail(String to, String content) { } }
public class LogService { public void log(String message) { } }
```

## 2. O – Open/Closed Principle (OCP)
> **Mở** cho việc mở rộng, **Đóng** cho việc sửa đổi code cũ.

```java
// ❌ Vi phạm: Mỗi lần thêm hình dạng mới phải SỬA method calculateArea
public double calculateArea(Shape shape) {
    if (shape.type.equals("circle")) return Math.PI * shape.radius * shape.radius;
    if (shape.type.equals("rectangle")) return shape.width * shape.height;
    // Thêm triangle? Phải sửa method này...
}

// ✅ Tuân thủ: Thêm hình dạng mới = tạo class mới, KHÔNG sửa code cũ
public abstract class Shape {
    public abstract double calculateArea();
}
public class Circle extends Shape {
    @Override public double calculateArea() { return Math.PI * radius * radius; }
}
public class Triangle extends Shape {  // MỞ RỘNG mà không sửa code cũ
    @Override public double calculateArea() { return 0.5 * base * height; }
}
```

## 3. L – Liskov Substitution Principle (LSP)
> Class con phải **thay thế được** class cha mà không làm sai logic chương trình.

```java
// ❌ Vi phạm: Chim cánh cụt không bay được nhưng kế thừa Bird có fly()
public class Bird { public void fly() { System.out.println("Bay"); } }
public class Penguin extends Bird {
    @Override public void fly() { throw new UnsupportedOperationException("Không bay được!"); }
}

// ✅ Tuân thủ: Tách interface riêng
public interface Flyable { void fly(); }
public class Sparrow implements Flyable { public void fly() { /* bay */ } }
public class Penguin { /* không implements Flyable */ }
```

## 4. I – Interface Segregation Principle (ISP)
> **Không** ép class implement interface mà nó **không cần**.

```java
// ❌ Vi phạm: Interface quá lớn
public interface Worker {
    void code();
    void test();
    void manageTeam();  // Developer không cần quản lý team!
}

// ✅ Tuân thủ: Tách nhỏ
public interface Coder { void code(); }
public interface Tester { void test(); }
public interface TeamLeader { void manageTeam(); }

public class Developer implements Coder, Tester { /* chỉ code và test */ }
public class Manager implements TeamLeader { /* chỉ quản lý */ }
```

## 5. D – Dependency Inversion Principle (DIP)
> Module cấp cao **không phụ thuộc** module cấp thấp. Cả hai phụ thuộc **abstraction** (interface).
> Đây chính là **nền tảng của Spring Dependency Injection**.

```java
// ❌ Vi phạm: OrderService phụ thuộc TRỰC TIẾP vào MySQLOrderRepository
public class OrderService {
    private MySQLOrderRepository repo = new MySQLOrderRepository(); // Tight coupling!
}

// ✅ Tuân thủ: Phụ thuộc Interface, inject implementation từ bên ngoài
public interface OrderRepository { void save(Order order); }
public class MySQLOrderRepository implements OrderRepository { /* MySQL */ }
public class MongoOrderRepository implements OrderRepository { /* MongoDB */ }

public class OrderService {
    private final OrderRepository repo;  // Phụ thuộc Interface (abstraction)
    public OrderService(OrderRepository repo) { this.repo = repo; }  // Inject qua constructor
}

// Dễ dàng đổi implementation mà KHÔNG sửa OrderService
OrderService service = new OrderService(new MongoOrderRepository());
```

## 6. Bảng tóm tắt

| Nguyên lý | Ý nghĩa ngắn gọn | Từ khoá nhớ |
|-----------|-------------------|-------------|
| **S** | 1 class = 1 nhiệm vụ | "Tách nhỏ" |
| **O** | Mở rộng mà không sửa code cũ | "Thêm mới, không sửa" |
| **L** | Class con thay thế được cha | "Đổi con vẫn chạy đúng" |
| **I** | Interface nhỏ, chuyên biệt | "Không ép làm thừa" |
| **D** | Phụ thuộc Interface, không phụ thuộc class cụ thể | "Tiền đề Spring DI" |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Giải thích SOLID bằng ví dụ thực tế trong Java Backend
1. **S - Single Responsibility Principle (Đơn trách nhiệm):**
   - *Vi phạm:* Một class `OrderController` vừa nhận HTTP request, vừa tính toán thuế/kho, vừa gọi câu lệnh SQL `INSERT INTO orders...`, vừa tự bắn email cho khách.
   - *Chuẩn:* Tách thành `OrderController` (HTTP routing) $\rightarrow$ `OrderService` (nghiệp vụ tính toán) $\rightarrow$ `OrderRepository` (lưu DB) $\rightarrow$ `NotificationService` (gửi mail).
2. **O - Open/Closed Principle (Đóng để sửa, Mở để thêm):**
   - *Ví dụ:* Hệ thống thanh toán có `PaymentService`. Khi tích hợp thêm cổng thanh toán mới (như Apple Pay), ta chỉ cần tạo class mới `ApplePayStrategy implements PaymentStrategy` mà không phải vào sửa đổi chuỗi `if-else` trong code cũ.
3. **L - Liskov Substitution Principle (Thay thế Liskov):**
   - *Ví dụ:* Class cha `ReadOnlyRepository` có hàm `findById()`. Class con `UserRepository` kế thừa từ nó thì bất kỳ chỗ nào nhận `ReadOnlyRepository` đều có thể truyền `UserRepository` vào thay thế mà chương trình vẫn chạy chính xác, không văng ngoại lệ bất thường `UnsupportedOperationException`.
4. **I - Interface Segregation Principle (Phân tách Interface):**
   - *Ví dụ:* Thay vì một `SuperWorkerInterface` có cả `work()`, `eat()`, `sleep()`, ép cả `RobotWorker` phải triển khai `eat()`. Ta tách thành `Workable` và `Eatable`. `RobotWorker` chỉ cần `implements Workable`.
5. **D - Dependency Inversion Principle (Đảo ngược phụ thuộc):**
   - *Ví dụ:* `UserService` không được `new MySQLUserRepository()` trực tiếp trong thân class. Thay vào đó, `UserService` phụ thuộc vào interface `UserRepository`. Việc đưa implementation nào vào sẽ do Spring Boot lo thông qua Dependency Injection.

### 7.2. Nguyên lý nào là nền tảng của Dependency Injection trong Spring?
- **Nguyên lý chữ D: Dependency Inversion Principle (DIP).**
- **Cơ chế:**
  - *Module cấp cao (High-level - như Service)* không được phụ thuộc trực tiếp vào *Module cấp thấp (Low-level - như Database Repository, Third-party SDK)*. Cả hai phải cùng phụ thuộc vào **sự trừu tượng (Abstraction / Interface)**.
  - Spring Framework hiện thực hóa nguyên lý này thông qua cơ chế **Inversion of Control (IoC)** và **Dependency Injection (DI)**: Spring Container sẽ tự động tìm kiếm Bean phù hợp và "tiêm" (inject) vào Service qua Constructor lúc khởi động ứng dụng.

### 7.3. Cho ví dụ vi phạm SRP và cách Refactor trong thực tế
- **Đoạn code vi phạm:**
  ```java
  public class UserService {
      public void registerUser(User user) {
          // 1. Validate email, password
          if (!user.getEmail().contains("@")) throw new RuntimeException("Invalid email");
          
          // 2. Lưu vào Database
          String sql = "INSERT INTO users VALUES (...)";
          jdbcTemplate.update(sql);
          
          // 3. Gửi email kích hoạt
          JavaMailSender.sendMail(user.getEmail(), "Welcome!");
      }
  }
  ```
  Class này có tới 3 lý do để bị sửa đổi: khi quy tắc validate đổi, khi câu lệnh SQL đổi, hoặc khi mẫu email đổi.
- **Refactor chuẩn SRP:**
  ```java
  @Service
  @RequiredArgsConstructor
  public class UserService {
      private final UserValidator validator;
      private final UserRepository repository;
      private final EmailService emailService;

      public void registerUser(User user) {
          validator.validate(user);
          User savedUser = repository.save(user);
          emailService.sendWelcomeEmail(savedUser.getEmail());
      }
  }
  ```

### 7.4. OCP áp dụng trong Spring Boot thế nào? (Strategy Pattern + @Service)
Spring Boot hỗ trợ triển khai Open/Closed Principle cực kỳ thanh lịch thông qua **Strategy Pattern** và tính năng **Auto-wiring Map/List Beans**:
```java
// 1. Interface chung
public interface PaymentGateway {
    String getPaymentType(); // "MOMO", "VNPAY", "ZALOPAY"
    void process(double amount);
}

// 2. Các Service triển khai độc lập
@Service
public class MomoGateway implements PaymentGateway {
    public String getPaymentType() { return "MOMO"; }
    public void process(double amount) { /* Logic Momo */ }
}

@Service
public class VnPayGateway implements PaymentGateway {
    public String getPaymentType() { return "VNPAY"; }
    public void process(double amount) { /* Logic VNPay */ }
}

// 3. Quản lý tập trung không cần if-else
@Service
public class PaymentFactory {
    private final Map<String, PaymentGateway> gatewayMap;

    // Spring tự động quét tất cả các bean implements PaymentGateway và nhét vào Map!
    public PaymentFactory(List<PaymentGateway> gateways) {
        gatewayMap = gateways.stream()
            .collect(Collectors.toMap(PaymentGateway::getPaymentType, Function.identity()));
    }

    public void pay(String type, double amount) {
        PaymentGateway gateway = gatewayMap.get(type);
        if (gateway == null) throw new IllegalArgumentException("Cổng không hỗ trợ: " + type);
        gateway.process(amount);
    }
}
```
$\rightarrow$ **Khi cần thêm cổng thanh toán ZaloPay:** Ta chỉ cần tạo class mới `ZaloPayGateway implements PaymentGateway`. Class `PaymentFactory` hoàn toàn **đóng để sửa (không cần sửa một dòng code nào)** nhưng hệ thống vẫn **mở rộng thêm tính năng mới thành công**!

---
*Thực hành:* Phân tích 1 class vi phạm SRP, refactor lại. Viết code minh hoạ DIP bằng Interface + Constructor Injection.

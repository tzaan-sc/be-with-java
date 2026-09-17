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

## 7. Câu hỏi phỏng vấn
1. Giải thích SOLID bằng ví dụ thực tế trong Java Backend.
2. Nguyên lý nào là nền tảng của Dependency Injection trong Spring?
3. Cho ví dụ vi phạm SRP và cách refactor.
4. OCP áp dụng trong Spring Boot thế nào? (Strategy Pattern, Interface + @Service)

---
*Thực hành:* Phân tích 1 class vi phạm SRP, refactor lại. Viết code minh hoạ DIP bằng Interface + Constructor Injection.

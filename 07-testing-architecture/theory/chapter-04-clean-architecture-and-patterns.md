# Chapter 04: Kiến Trúc Clean Architecture & Design Patterns Trong Spring Boot

---

## 1. Từ Layered Architecture đến Clean Architecture

### A. Kiến trúc 3 tầng truyền thống (Layered Architecture)
Mô hình phổ biến nhất: **Controller $\rightarrow$ Service $\rightarrow$ Repository $\rightarrow$ Database**.
- **Điểm yếu**: Tầng nghiệp vụ (Service) thường bị phụ thuộc chặt chẽ vào Database Entity và các thư viện bên ngoài (JPA, Jackson). Khi thay đổi công nghệ DB hoặc nâng cấp framework, mã nguồn nghiệp vụ cốt lõi bị ảnh hưởng theo.

### B. Clean Architecture (Hexagonal / Ports & Adapters)
Nguyên tắc cốt lõi của Clean Architecture: **Quy tắc phụ thuộc (Dependency Rule)**.
> **Các tầng bên ngoài chỉ được phụ thuộc vào các tầng bên trong, tầng bên trong tuyệt đối KHÔNG ĐƯỢC biết gì về tầng bên ngoài!**

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ 1. FRAMEWORKS & DRIVERS (Tầng Ngoại Vi - Web, DB, Devices, UI, External Interfaces)     │
│    [Web MVC / REST]       [MySQL / Spring Data JPA]       [VNPay / Email Service]      │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │ 2. INTERFACE ADAPTERS (Tầng Chuyển Đổi - Controllers, Gateways, Presenters)      │  │
│  │    [DTOs & Controllers]                    [Repository Implementations / DAOs]   │  │
│  │  ┌────────────────────────────────────────────────────────────────────────────┐  │  │
│  │  │ 3. APPLICATION BUSINESS RULES (Tầng Ứng Dụng - Use Cases / Services)       │  │  │
│  │  │    [CreateUserUseCase]                  [OrderProcessingService]           │  │  │
│  │  │  ┌──────────────────────────────────────────────────────────────────────┐  │  │  │
│  │  │  │ 4. ENTERPRISE BUSINESS RULES (Tầng Cốt Lõi - Domain Entities)        │  │  │  │
│  │  │  │    [Domain Models: User, Order, Product]                             │  │  │  │
│  │  │  │    (Java thuần khiết POJO, KHÔNG phụ thuộc Spring, JPA hay DB)       │  │  │  │
│  │  │  └──────────────────────────────────▲───────────────────────────────────┘  │  │  │
│  │  │                                     │ Phụ thuộc hướng vào tâm            │  │  │
│  │  └─────────────────────────────────────┼────────────────────────────────────┘  │  │
│  │                                        │ (Dependency Rule)                     │  │
│  └────────────────────────────────────────┼───────────────────────────────────────┘  │
│                                           │                                          │
└───────────────────────────────────────────┴──────────────────────────────────────────┘
```

---

## 2. Tổ chức cấu trúc thư mục dự án chuẩn (Package by Feature)

Thay vì gom tất cả Controller vào một thư mục, gom tất cả Service vào một thư mục (`Package by Layer`), các dự án lớn ưu tiên tổ chức theo **Tính năng (Package by Feature)** để tăng tính đóng gói:

```text
src/main/java/com/example/app/
├── common/                     <-- Các tiện ích dùng chung (BaseResponse, Exception, Utils)
│   ├── exception/
│   └── response/
├── config/                     <-- Các file cấu hình Spring (@Configuration, Security, Cors)
└── modules/                    <-- Chia theo nghiệp vụ độc lập
    ├── auth/
    │   ├── controller/
    │   ├── dto/
    │   └── service/
    ├── user/
    │   ├── controller/
    │   ├── dto/
    │   ├── entity/
    │   ├── repository/
    │   └── service/
    └── order/
        ├── controller/
        ├── dto/
        ├── entity/
        ├── repository/
        └── service/
```

---

## 3. Các Design Pattern thực tế phổ biến trong Spring Boot

### Pattern 1: Strategy Pattern (Xử lý đa cổng thanh toán)
Tránh dùng chuỗi `if-else` hoặc `switch-case` dài dòng khi cần xử lý nhiều phương thức thanh toán (`VNPAY`, `MOMO`, `ZALOPAY`).

```java
// 1. Khai báo Strategy Interface
public interface PaymentStrategy {
    PaymentType getType();
    PaymentResult process(BigDecimal amount);
}

// 2. Các Concrete Strategies
@Component
public class VnPayStrategy implements PaymentStrategy {
    @Override
    public PaymentType getType() { return PaymentType.VNPAY; }
    @Override
    public PaymentResult process(BigDecimal amount) {
        // Gọi SDK VNPay...
        return new PaymentResult(true, "Thanh toán VNPay thành công");
    }
}

@Component
public class MomoStrategy implements PaymentStrategy {
    @Override
    public PaymentType getType() { return PaymentType.MOMO; }
    @Override
    public PaymentResult process(BigDecimal amount) {
        // Gọi SDK MoMo...
        return new PaymentResult(true, "Thanh toán MoMo thành công");
    }
}

// 3. Strategy Factory / Manager
@Service
public class PaymentContext {

    private final Map<PaymentType, PaymentStrategy> strategies = new EnumMap<>(PaymentType.class);

    // Spring tự động tiêm tất cả các bean implement PaymentStrategy vào danh sách!
    public PaymentContext(List<PaymentStrategy> strategyList) {
        for (PaymentStrategy strategy : strategyList) {
            strategies.put(strategy.getType(), strategy);
        }
    }

    public PaymentResult executePayment(PaymentType type, BigDecimal amount) {
        PaymentStrategy strategy = strategies.get(type);
        if (strategy == null) {
            throw new IllegalArgumentException("Cổng thanh toán không hỗ trợ: " + type);
        }
        return strategy.process(amount);
    }
}
```

---

### Pattern 2: Event-Driven Pattern với `ApplicationEventPublisher`
Tách rời luồng xử lý chính với các tác vụ phụ trợ (như gửi email xác nhận, cộng điểm thưởng):

```java
// 1. Tạo Sự Kiện (Event)
public record OrderPlacedEvent(Long orderId, String customerEmail, BigDecimal totalAmount) {}

// 2. Phát Sự Kiện từ OrderService
@Service
@RequiredArgsConstructor
public class OrderService {
    private final ApplicationEventPublisher eventPublisher;

    @Transactional
    public void createOrder(OrderRequest request) {
        // Lưu đơn hàng vào DB...
        OrderEntity order = orderRepository.save(newOrder);

        // Bắn sự kiện ra hệ thống (OrderService không cần biết ai lắng nghe)
        eventPublisher.publishEvent(new OrderPlacedEvent(order.getId(), order.getCustomerEmail(), order.getTotal()));
    }
}

// 3. Người Lắng Nghe Sự Kiện (EventListener)
@Component
@Slf4j
public class EmailNotificationListener {

    @EventListener
    @Async // Chạy bất đồng bộ trong background thread, không block luồng tạo đơn hàng!
    public void onOrderPlaced(OrderPlacedEvent event) {
        log.info("Đang gửi email xác nhận đơn hàng #{} tới {}", event.orderId(), event.customerEmail());
        // Gửi email...
    }
}
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Quy tắc phụ thuộc (The Dependency Rule) trong Clean Architecture là gì?
- **Nguyên lý bất biến:**
  > *"Chiều của các mũi tên phụ thuộc mã nguồn BẮT BUỘC PHẢI LUÔN HƯỚNG VÀO TRONG (Hướng về trung tâm Domain Entities & Use Cases)."*
- **Ý nghĩa thực tế:**
  - Tầng Domain (Nghiệp vụ cốt lõi) nằm ở tâm: Hoàn toàn trong sáng, **không chứa bất kỳ annotation nào của Spring, Hibernate hay cơ sở dữ liệu**.
  - Tầng ngoài cùng (Frameworks & Drivers: Web Controller, MySQL Database, Redis, REST Client) phải phụ thuộc vào Domain.
  - Tầng Domain **không bao giờ được biết đến sự tồn tại của Database hay Framework**. Nhờ đó, bạn có thể thay thế Database từ PostgreSQL sang MongoDB, đổi Spring Boot sang Quarkus mà toàn bộ Logic nghiệp vụ trung tâm vẫn nguyên vẹn 100%.

### 4.2. Khác biệt giữa Package-by-Layer và Package-by-Feature? Dự án lớn nên chọn gì?
- **Package-by-Layer (Chia theo tầng kỹ thuật):**
  - Cấu trúc: `com.app.controller`, `com.app.service`, `com.app.repository`.
  - Nhược điểm: Khi dự án có 50 tính năng, thư mục `service/` sẽ có 50 file chen chúc nhau. Muốn sửa tính năng "Đặt hàng", bạn phải nhảy qua 5 package khác nhau.
- **Package-by-Feature (Chia theo mô-đun nghiệp vụ):**
  - Cấu trúc: `com.app.order` (chứa `OrderController`, `OrderService`, `OrderRepository`), `com.app.user`, `com.app.payment`.
  - Ưu điểm: Đóng gói tính năng độc lập, dễ dàng chuyển đổi sang kiến trúc **Microservices** sau này khi dự án phình to.
  - **Khuyên dùng:** Các dự án lớn trong thực tế **luôn ưu tiên Package-by-Feature**.

### 4.3. Lợi ích của Event-Driven Pattern nội bộ (`ApplicationEventPublisher`) so với việc gọi trực tiếp Service?
- **Nếu gọi trực tiếp (`OrderService` tự gọi `emailService.sendEmail()`):**
  - `OrderService` bị dính chặt (Tightly coupled) với `EmailService`.
  - Nếu gửi email bị chậm 3 giây hoặc sập mạng, toàn bộ API tạo đơn hàng của khách hàng sẽ bị chậm 3 giây hoặc bị lỗi theo!
- **Khi dùng Event-Driven:**
  - `OrderService` chỉ việc lưu đơn hàng và bắn ra `OrderPlacedEvent` rồi kết thúc trong 50ms.
  - `EmailNotificationListener` lắng nghe sự kiện và chạy `@Async` ở background thread độc lập.
  - Sau này nếu bạn muốn làm thêm tính năng: "Cộng điểm tích lũy" hay "Bắn thông báo qua Telegram", bạn chỉ cần viết thêm `BonusPointsListener` mới mà **hoàn toàn không cần sửa 1 dòng code nào trong `OrderService`** (Tuân thủ chuẩn Open/Closed Principle).

---
*Thực hành:* Tạo 1 event `UserRegisteredEvent`, viết `@EventListener` có `@Async` để giả lập gửi email chào mừng bất đồng bộ.

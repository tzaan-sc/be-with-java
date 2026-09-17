# Chapter 02: Interface vs Abstract Class & Default/Static Methods

## 1. Interface là gì?
- Interface là **hợp đồng** (contract) định nghĩa các method mà class phải triển khai.
- Mặc định tất cả method trong interface là `public abstract` (trước Java 8).

```java
public interface PaymentService {
    void pay(double amount);            // abstract (bắt buộc triển khai)
    boolean refund(String transactionId);
}

public class VnPayService implements PaymentService {
    @Override
    public void pay(double amount) {
        System.out.println("Thanh toán qua VNPay: " + amount + "đ");
    }
    @Override
    public boolean refund(String txId) {
        System.out.println("Hoàn tiền VNPay: " + txId);
        return true;
    }
}

public class MomoService implements PaymentService {
    @Override
    public void pay(double amount) {
        System.out.println("Thanh toán qua Momo: " + amount + "đ");
    }
    @Override
    public boolean refund(String txId) { return false; }
}
```

### Đa kế thừa qua Interface
```java
public interface Loggable { void log(String message); }
public interface Auditable { void audit(); }

// 1 class có thể implements NHIỀU interface
public class OrderService implements PaymentService, Loggable, Auditable {
    // Phải triển khai TẤT CẢ method từ 3 interface
}
```

## 2. Default & Static Methods (Java 8+)

### 2.1 Default Method
```java
public interface PaymentService {
    void pay(double amount);

    // Default method: CÓ body, class con kế thừa mà không cần override
    default String getPaymentStatus() {
        return "PENDING";
    }
}
// VnPayService tự động có method getPaymentStatus() mà không cần viết lại
```

- Mục đích: Thêm method mới vào interface **mà không phá vỡ** các class đã implement.

### 2.2 Static Method
```java
public interface PaymentService {
    static PaymentService create(String provider) {
        return switch (provider) {
            case "vnpay" -> new VnPayService();
            case "momo"  -> new MomoService();
            default -> throw new IllegalArgumentException("Unknown: " + provider);
        };
    }
}

// Gọi qua tên interface
PaymentService payment = PaymentService.create("vnpay");
```

### 2.3 Diamond Problem
```java
interface A { default void hello() { System.out.println("A"); } }
interface B { default void hello() { System.out.println("B"); } }

// Class phải override để giải quyết xung đột
class C implements A, B {
    @Override
    public void hello() {
        A.super.hello();  // Chọn gọi A
    }
}
```

## 3. So sánh Interface vs Abstract Class

| Tiêu chí | Interface | Abstract Class |
|----------|-----------|---------------|
| Từ khoá | `implements` | `extends` |
| Đa kế thừa | ✅ Nhiều interface | ❌ Chỉ 1 class |
| Constructor | ❌ Không có | ✅ Có |
| Field | Chỉ `public static final` (hằng số) | Mọi loại field |
| Method có body | `default`, `static` (Java 8+) | Method thường + abstract |
| Khi nào dùng | Định nghĩa **hành vi chung** (contract) | Chia sẻ **code chung** giữa các class liên quan |

### Quy tắc chọn
- **Interface**: Khi các class **không liên quan** về mặt kế thừa nhưng cần cùng 1 hành vi (VD: `PaymentService` cho VNPay, Momo, Stripe).
- **Abstract Class**: Khi các class **có quan hệ IS-A** rõ ràng và chia sẻ code chung (VD: `Shape` → `Circle`, `Rectangle`).

## 4. Câu hỏi phỏng vấn
1. Interface và Abstract Class khác nhau thế nào? Khi nào dùng cái nào?
2. Default method trong Interface giải quyết vấn đề gì?
3. Diamond Problem là gì? Java giải quyết thế nào?
4. Có thể tạo biến (field) trong Interface không? Có ràng buộc gì?
5. Tại sao Java không cho phép đa kế thừa class nhưng cho phép đa kế thừa interface?

---
*Thực hành:* Tạo `PaymentService` interface → `VnPayService`, `MomoService` implements. Thêm default method. Thử Diamond Problem.

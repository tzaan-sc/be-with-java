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

## 4. Câu hỏi phỏng vấn & Trả lời chi tiết

### 4.1. Interface và Abstract Class khác nhau thế nào? Khi nào dùng cái nào?
- **Khác biệt cốt lõi:**
  - **Interface là "Bản hợp đồng về hành vi" (Contract - CAN-DO):** Nhấn mạnh đối tượng **có thể làm được gì**, không quan tâm đối tượng đó là ai (vd: `Flyable`, `Serializable`, `PaymentService`).
  - **Abstract Class là "Bản thiết kế gốc chung" (Identity - IS-A):** Nhấn mạnh đối tượng **bản chất là cái gì**, dùng để chia sẻ cấu trúc thuộc tính và hành vi chung cho các class con có quan hệ họ hàng mật thiết (vd: `Animal` $\rightarrow$ `Dog, Cat`, `BaseEntity` $\rightarrow$ `User, Product`).
- **Khi nào chọn cái nào:**
  - **Chọn Interface khi:** Muốn định nghĩa chuẩn giao tiếp (API contract), muốn hỗ trợ đa triển khai (loose coupling trong Spring Boot Service layer), hoặc khi các class triển khai hoàn toàn không có họ hàng với nhau (ví dụ cả `Bird` và `Airplane` đều `implements Flyable`).
  - **Chọn Abstract Class khi:** Cần chia sẻ mã nguồn dùng chung (code reuse), cần có thuộc tính non-static (trạng thái riêng của object), hoặc cần có Constructor để khởi tạo dữ liệu chung.

### 4.2. Default method trong Interface giải quyết vấn đề gì?
- **Vấn đề lịch sử (trước Java 8):** Interface chỉ chứa abstract method. Khi một thư viện mở rộng thêm 1 hàm mới vào Interface, **hàng ngàn class đang implements interface đó trên toàn thế giới sẽ lập tức bị lỗi biên dịch** vì chưa override hàm mới đó.
- **Giải pháp của Java 8:** Bổ sung từ khóa `default`:
  ```java
  public interface List<E> {
      default void sort(Comparator<? super E> c) {
          // Cung cấp sẵn mã nguồn mặc định
      }
  }
  ```
  Nhờ có `default method`, Java có thể thêm các tính năng hiện đại (như `.stream()`, `.forEach()`, `.sort()`) vào Collection Interface mà vẫn đảm bảo **tính tương thích ngược (Backward Compatibility)** hoàn hảo.

### 4.3. Diamond Problem là gì? Java giải quyết thế nào với Default Method?
- **Diamond Problem với Interface:** Nếu Class `C` triển khai 2 Interface `A` và `B`, mà cả `A` và `B` đều có cùng một hàm `default void print()`.
- **Cách Java bắt buộc xử lý:** Trình biên dịch Java sẽ phát hiện xung đột và **báo lỗi biên dịch ngay lập tức**. Java ép lập trình viên tại Class `C` **bắt buộc phải Override lại hàm `print()`** để chỉ định rõ ràng muốn dùng triển khai của interface nào:
  ```java
  public class C implements A, B {
      @Override
      public void print() {
          // Cách 1: Chỉ định gọi cụ thể của A
          A.super.print();
          // Hoặc Cách 2: Tự viết lại logic riêng hoàn toàn cho C
      }
  }
  ```

### 4.4. Có thể tạo biến (field) trong Interface không? Có ràng buộc gì?
- **Câu trả lời:** Có thể khai báo trường dữ liệu trong Interface, nhưng **chỉ duy nhất dưới dạng HẰNG SỐ**.
- **Ràng buộc mặc định:** Dù bạn không viết từ khóa nào, JVM luôn tự động ngầm định mọi field trong Interface đều là:
  $$\text{public static final}$$
  - `public`: Bất kỳ đâu cũng có thể truy cập được.
  - `static`: Thuộc về chính interface đó, không gắn liền với instance.
  - `final`: Phải gán giá trị ngay khi khai báo và không bao giờ được phép thay đổi.
  - *Lưu ý:* Không thể khai báo biến instance bình thường (như `private int count;`) trong Interface.

### 4.5. Tại sao Java cấm đa kế thừa class nhưng lại cho phép đa kế thừa interface?
- **Với Class:** Chứa thuộc tính (State) và thân hàm (Implementation). Đa kế thừa class sẽ dẫn tới:
  1. Xung đột trạng thái (hai cha đều có field `int x`, con sẽ có 2 ô nhớ `x` hay 1?).
  2. Xung đột Constructor (thứ tự gọi `super()` từ cha nào trước?).
  3. Lỗi Diamond Problem khó lường lúc runtime.
- **Với Interface:** Thuần túy là "đặc tả giao diện" (chỉ có tên hàm và tham số). Kể cả 2 interface có hàm trùng tên, class con cũng chỉ cần triển khai một thân hàm duy nhất để thỏa mãn cả 2 giao diện. Không có xung đột bộ nhớ, không có vấn đề Constructor, do đó hoàn toàn an toàn và trong sáng.

---
*Thực hành:* Tạo `PaymentService` interface → `VnPayService`, `MomoService` implements. Thêm default method. Thử Diamond Problem.

# Chapter 05: Transaction Management – @Transactional

## 1. ACID
| Thuộc tính | Ý nghĩa |
|-----------|---------|
| **A**tomicity | Tất cả hoặc không gì cả (rollback nếu lỗi) |
| **C**onsistency | Dữ liệu luôn hợp lệ trước và sau transaction |
| **I**solation | Transaction này không ảnh hưởng transaction khác |
| **D**urability | Dữ liệu đã commit sẽ không mất dù server crash |

## 2. @Transactional trong Spring
```java
@Service
public class OrderService {
    @Transactional  // Nếu bất kỳ bước nào lỗi → rollback TẤT CẢ
    public void placeOrder(OrderRequest request) {
        OrderEntity order = orderRepository.save(mapToEntity(request));  // Bước 1
        paymentService.charge(request.getAmount());                      // Bước 2 (nếu lỗi → rollback bước 1)
        inventoryService.reduceStock(request.getProductId());            // Bước 3
        emailService.sendConfirmation(order);                            // Bước 4
    }
}
```

## 3. Propagation
| Type | Mô tả |
|------|-------|
| `REQUIRED` (mặc định) | Dùng transaction hiện tại, tạo mới nếu chưa có |
| `REQUIRES_NEW` | Luôn tạo transaction MỚI, tạm dừng transaction cũ |
| `SUPPORTS` | Dùng transaction nếu có, không có thì chạy không transaction |
| `NOT_SUPPORTED` | Chạy không transaction |

## 4. Rollback Rules
```java
// Mặc định: Chỉ rollback với RuntimeException (Unchecked)
@Transactional  // IOException (Checked) sẽ KHÔNG rollback!

// Cấu hình rollback mọi Exception
@Transactional(rollbackFor = Exception.class)

// Không rollback cho exception cụ thể
@Transactional(noRollbackFor = EmailException.class)
```

## 5. Isolation Levels
| Level | Mô tả |
|-------|-------|
| `READ_UNCOMMITTED` | Đọc dữ liệu chưa commit (dirty read) |
| `READ_COMMITTED` | Chỉ đọc dữ liệu đã commit (mặc định PostgreSQL) |
| `REPEATABLE_READ` | Đảm bảo đọc lại cùng giá trị (mặc định MySQL) |
| `SERIALIZABLE` | Tuần tự hoàn toàn, chậm nhất |

## 6. Lưu ý quan trọng
- `@Transactional` chỉ hoạt động khi gọi từ **BÊN NGOÀI** class (qua proxy). Gọi method trong cùng class → **KHÔNG có transaction**!
- Đặt `@Transactional` trên **Service layer**, không đặt trên Controller.

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. ACID là gì? Ý nghĩa của từng chữ cái trong giao dịch cơ sở dữ liệu
- **A - Atomicity (Tính nguyên tử - "Tất cả hoặc Không có gì"):**
  - Toàn bộ các thao tác trong giao dịch phải thành công trọn vẹn 100%. Nếu có bất kỳ bước nào thất bại, toàn bộ các bước đã làm trước đó phải được hoàn tác (**Rollback**) về trạng thái ban đầu (ví dụ: chuyển tiền thành công ở bên gửi nhưng bên nhận lỗi $\rightarrow$ hoàn tiền lại cho bên gửi).
- **C - Consistency (Tính nhất quán):**
  - Dữ liệu trước và sau giao dịch đều phải tuân thủ đúng mọi ràng buộc toàn vẹn (Constraints, Foreign Keys, Triggers, số dư tài khoản không được âm).
- **I - Isolation (Tính cô lập):**
  - Nhiều giao dịch chạy đồng thời (Concurrent Transactions) không được can thiệp hay nhìn thấy dữ liệu dở dang chưa commit của nhau. Tránh các hiện tượng: *Dirty Read, Non-repeatable Read, Phantom Read*.
- **D - Durability (Tính bền vững):**
  - Một khi giao dịch đã báo Commit thành công, dữ liệu sẽ được ghi vĩnh viễn xuống ổ cứng (Write-Ahead Logging - WAL). Dù sau đó máy chủ có mất điện đột ngột hay sập server thì dữ liệu vẫn không bao giờ bị biến mất.

### 7.2. `@Transactional` mặc định Rollback khi nào? Cách cấu hình để Rollback cả Checked Exception?
- **Mặc định nguy hiểm trong Spring:**
  - Spring `@Transactional` **CHỈ TỰ ĐỘNG ROLLBACK khi gặp `RuntimeException` (Unchecked Exception) và `Error`**.
  - Nếu gặp **`Checked Exception`** (như `IOException`, `SQLException`, hoặc class custom kế thừa từ `Exception`), Spring **MẶC ĐỊNH SẼ KHÔNG ROLLBACK** (Giao dịch vẫn bị Commit dù có lỗi!).
- **Cách cấu hình chuẩn an toàn:**
  Bắt buộc phải thêm thuộc tính `rollbackFor = Exception.class`:
  ```java
  @Transactional(rollbackFor = Exception.class)
  public void transferMoney(...) { ... }
  ```
  Lúc này, bất kỳ ngoại lệ nào xảy ra (cả Checked lẫn Unchecked), Spring đều sẽ kích hoạt Rollback toàn bộ dữ liệu.

### 7.3. `REQUIRED` vs `REQUIRES_NEW` khác nhau thế nào?
| Tiêu chí | `Propagation.REQUIRED` (Mặc định) | `Propagation.REQUIRES_NEW` |
| :--- | :--- | :--- |
| **Cơ chế** | Nếu **đã có transaction cha**: Tham gia vào transaction đó. Nếu **chưa có**: Tạo mới. | **Luôn luôn tạo một Transaction mới hoàn toàn độc lập**. |
| **Ảnh hưởng lẫn nhau** | Nếu phương thức con bị lỗi $\rightarrow$ Toàn bộ Transaction cha cũng bị **Rollback theo**. | Transaction con chạy độc lập trong kết nối DB riêng. Nếu con lỗi/thành công, nó commit/rollback riêng mà **không làm chết Transaction cha** (và ngược lại). |
| **Ứng dụng thực tế** | Dùng cho **95% các nghiệp vụ thông thường** (tạo đơn, cập nhật kho, trừ tiền). | Dùng cho các tác vụ phụ bắt buộc phải ghi dữ liệu kể cả khi nghiệp vụ chính lỗi: **Ghi lịch sử Audit Log, Lưu vết thanh toán thất bại, Đếm số lần đăng nhập sai**. |

### 7.4. Tại sao `@Transactional` KHÔNG HOẠT ĐỘNG khi gọi nội bộ trong cùng Class (Self-Invocation)?
- **Nguyên nhân gốc rễ (Spring AOP Proxy Mechanism):**
  - `@Transactional` hoạt động dựa trên cơ chế **Dynamic Proxy**.
  - Khi một Class bên ngoài (như `Controller`) gọi `orderService.placeOrder()`, thực chất nó đang gọi xuyên qua một lớp vỏ bọc **Proxy Object**. Proxy này sẽ mở kết nối DB $\rightarrow$ Bắt đầu Transaction $\rightarrow$ Gọi hàm thật $\rightarrow$ Commit / Rollback.
  - Nhưng khi bạn viết:
    ```java
    public void methodA() {
        methodB(); // 👈 Gọi nội bộ cùng class (this.methodB())
    }

    @Transactional
    public void methodB() { ... }
    ```
    Lệnh `methodB()` được gọi trực tiếp trên con trỏ `this` (đối tượng thật bên trong), cuộc gọi này **hoàn toàn đi tắt mà không hề đi qua lớp vỏ bọc Spring Proxy**.
  - $\rightarrow$ Kết quả: Annotation `@Transactional` trên `methodB()` bị **vô hiệu hóa hoàn toàn**, không có transaction nào được tạo ra!
- **Cách khắc phục:**
  1. Tách `methodB()` sang một Service/Component riêng biệt rồi inject vào.
  2. Hoặc tự inject chính interface của Service vào bản thân (Self-autowiring).

---
*Thực hành:* Viết 1 hàm chuyển tiền có `@Transactional(rollbackFor = Exception.class)`, thử quăng `RuntimeException` để kiểm tra số dư không bị trừ lẹm.

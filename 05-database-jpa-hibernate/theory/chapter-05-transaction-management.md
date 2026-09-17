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

## 7. Câu hỏi phỏng vấn
1. ACID là gì? Mỗi chữ cái nghĩa gì?
2. `@Transactional` mặc định rollback khi nào? Cách rollback Checked Exception?
3. `REQUIRED` vs `REQUIRES_NEW` khác nhau thế nào?
4. Tại sao `@Transactional` không hoạt động khi self-invocation?

---

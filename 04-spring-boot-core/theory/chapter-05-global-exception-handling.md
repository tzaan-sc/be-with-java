# Chapter 05: Global Exception Handling – @RestControllerAdvice

## 1. Vấn đề
- Không bắt exception → client nhận **500 Internal Server Error** với stack trace lộ thông tin nội bộ.
- Bắt trong từng controller → **code trùng lặp**, khó bảo trì.

## 2. Giải pháp: @RestControllerAdvice
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    // Bắt ResourceNotFoundException → 404
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex, WebRequest request) {
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.NOT_FOUND.value())
            .message(ex.getMessage())
            .path(request.getDescription(false))
            .build();
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }

    // Bắt Validation Error → 400
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException ex) {
        List<String> errors = ex.getBindingResult().getFieldErrors().stream()
            .map(err -> err.getField() + ": " + err.getDefaultMessage())
            .toList();
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.BAD_REQUEST.value())
            .message("Validation failed")
            .errors(errors)
            .build();
        return ResponseEntity.badRequest().body(error);
    }

    // Bắt mọi Exception khác → 500
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception ex) {
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.INTERNAL_SERVER_ERROR.value())
            .message("Đã xảy ra lỗi hệ thống")
            .build();
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
    }
}
```

## 3. ErrorResponse class
```java
@Data @Builder @AllArgsConstructor @NoArgsConstructor
public class ErrorResponse {
    private LocalDateTime timestamp;
    private int status;
    private String message;
    private String path;
    private List<String> errors;
}
```

## 4. Custom Exception
```java
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String resource, Long id) {
        super(resource + " không tìm thấy với ID: " + id);
    }
}

public class DuplicateResourceException extends RuntimeException {
    public DuplicateResourceException(String message) { super(message); }
}
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. `@RestControllerAdvice` hoạt động như thế nào trong kiến trúc Spring MVC?
- **Bản chất:** `@RestControllerAdvice` là sự kết hợp của hai annotation:
  $$\text{@ControllerAdvice} + \text{@ResponseBody}$$
- **Nguyên lý hoạt động bên dưới (AOP - Aspect-Oriented Programming):**
  - `@ControllerAdvice` áp dụng kỹ thuật **Interception (Đánh chặn xung quanh)** trên toàn bộ các `@RestController` trong ứng dụng.
  - Khi bất kỳ phương thức nào trong bất kỳ Controller nào ném ra một Exception chưa được bắt (Uncaught Exception):
    1. Exception sẽ nổi lên và được Spring DispatcherServlet đón lấy.
    2. Spring quét tìm class có gắn `@RestControllerAdvice`.
    3. Tìm xem trong class đó có hàm nào gắn `@ExceptionHandler(Tên_Exception.class)` khớp với ngoại lệ vừa xảy ra không.
    4. Kích hoạt hàm đó để định dạng đối tượng lỗi (Error Response Object).
    5. Tự động serialize object đó thành JSON gửi về cho Client kèm mã HTTP Status tương ứng.

### 5.2. Tại sao BẮT BUỘC cần Global Exception Handler thay vì viết `try-catch` trong từng Controller?
1. **Loại bỏ trùng lặp mã nguồn (DRY - Don't Repeat Yourself):** Nếu không có Global Handler, bạn sẽ phải viết hàng trăm khối `try { ... } catch (Exception e)` giống hệt nhau ở khắp mọi Controller trong dự án.
2. **Chuẩn hóa cấu trúc lỗi trả về (Consistent Error Response):** Đảm bảo 100% các API trong hệ thống (dù lỗi 400, 404, hay 500) đều trả về một cấu trúc JSON đồng nhất duy nhất:
   ```json
   {
     "status": 404,
     "message": "User không tìm thấy với ID: 10",
     "timestamp": "2026-09-17T12:00:00"
   }
   ```
   Giúp đội ngũ Frontend (React/Mobile) chỉ cần viết 1 hàm xử lý lỗi chung duy nhất để hiển thị thông báo Toast/Popup cho người dùng.
3. **Bảo mật hệ thống (Prevent Information Leakage):** Ngăn chặn hoàn toàn việc server tự động văng ra màn hình trắng lỗi kỹ thuật (Whitelabel Error Page) hoặc phơi bày toàn bộ mã nguồn `stack trace` ra ngoài Internet cho hacker soi thấy.

### 5.3. Cách bắt lỗi Validation (`@Valid`) và trả về định dạng đẹp, chi tiết từng trường cho Client
Khi tham số `@Valid` bị vi phạm, Spring sẽ ném ra `MethodArgumentNotValidException`. Ta bắt ngoại lệ này trong Global Handler như sau:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, Object>> handleValidationErrors(MethodArgumentNotValidException ex) {
        // Gom toàn bộ các lỗi theo từng field vào Map
        Map<String, String> fieldErrors = new HashMap<>();
        for (FieldError error : ex.getBindingResult().getFieldErrors()) {
            fieldErrors.put(error.getField(), error.getDefaultMessage());
        }

        Map<String, Object> response = new HashMap<>();
        response.put("status", HttpStatus.BAD_REQUEST.value());
        response.put("message", "Dữ liệu đầu vào không hợp lệ");
        response.put("errors", fieldErrors); // {"email": "Sai định dạng", "age": "Phải >= 18"}
        response.put("timestamp", LocalDateTime.now());

        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(response);
    }
}
```

---
*Thực hành:* Tạo `GlobalExceptionHandler` bắt `ResourceNotFoundException` trả về 404, và bắt `MethodArgumentNotValidException` trả về map lỗi trường 400.

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

## 5. Câu hỏi phỏng vấn
1. `@RestControllerAdvice` hoạt động thế nào?
2. Tại sao cần Global Exception Handler thay vì try-catch trong mỗi controller?
3. Cách bắt lỗi validation và trả về format đẹp cho client?

---

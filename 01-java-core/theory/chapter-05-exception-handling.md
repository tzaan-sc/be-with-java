# Chapter 05: Xử lý Ngoại lệ (Exception Handling)

## 1. Exception là gì?
- **Exception** (Ngoại lệ) là sự kiện bất thường xảy ra trong quá trình chạy chương trình, làm gián đoạn luồng thực thi bình thường.
- Nếu không xử lý, chương trình sẽ **crash** và in ra stack trace.

```java
int[] arr = {1, 2, 3};
System.out.println(arr[5]);  // ❌ ArrayIndexOutOfBoundsException → Chương trình crash!
```

## 2. Hệ thống phân cấp Exception trong Java

```
┌────────────────────────────────────────────────────────────────────────┐
│                              Throwable                                 │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
      ┌─────────────────────────────┴─────────────────────────────┐
      ▼                                                           ▼
┌───────────────────────────┐               ┌───────────────────────────┐
│           Error           │               │         Exception         │
│  (JVM Crash / Hệ thống)   │               │     (Có thể xử lý)        │
└─────────────┬─────────────┘               └─────────────┬─────────────┘
              │                                           │
  ├── StackOverflowError            ┌─────────────────────┴─────────────────────┐
  └── OutOfMemoryError (OOM)        ▼                                           ▼
                              ┌───────────────────────────┐       ┌───────────────────────────┐
                              │     Checked Exception     │       │     RuntimeException      │
                              │ (Bắt buộc try-catch/throw)│       │    (Unchecked Exception)  │
                              └─────────────┬─────────────┘       └─────────────┬─────────────┘
                                            │                                   │
                                ├── IOException                     ├── NullPointerException
                                ├── SQLException                    ├── ArrayIndexOutOfBounds
                                └── ParseException                  ├── ArithmeticException
                                                                    ├── IllegalArgumentException
                                                                    └── NumberFormatException
```

### 2.1 Error (Lỗi hệ thống)
- **Không nên bắt / xử lý** vì quá nghiêm trọng (JVM gặp vấn đề).
- Ví dụ: `StackOverflowError`, `OutOfMemoryError`.

### 2.2 Checked Exception (Ngoại lệ kiểm tra)
- **Bắt buộc phải xử lý** tại compile‑time (dùng `try-catch` hoặc `throws`).
- Compiler sẽ báo lỗi nếu bạn không xử lý.
- Ví dụ: `IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`.

```java
// ❌ Compile Error nếu không xử lý IOException
FileReader file = new FileReader("data.txt");  // FileNotFoundException (checked)
```

### 2.3 Unchecked Exception (Ngoại lệ không kiểm tra)
- Kế thừa từ `RuntimeException`.
- **Không bắt buộc** phải xử lý tại compile‑time (nhưng nên bắt nếu có thể).
- Thường do **lỗi logic của lập trình viên**.
- Ví dụ: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`, `IllegalArgumentException`.

```java
String s = null;
s.length();          // ❌ NullPointerException (unchecked, runtime crash)

int result = 10 / 0; // ❌ ArithmeticException (unchecked)
```

### 2.4 Bảng so sánh

| Tiêu chí | Checked Exception | Unchecked Exception |
|----------|-------------------|---------------------|
| Kế thừa từ | `Exception` (trực tiếp) | `RuntimeException` |
| Bắt buộc xử lý? | ✅ Có (compile-time) | ❌ Không |
| Nguyên nhân | Yếu tố bên ngoài (file, network, DB) | Lỗi logic code |
| Ví dụ | `IOException`, `SQLException` | `NullPointerException`, `ArithmeticException` |

## 3. Cú pháp try – catch – finally

### 3.1 Cấu trúc cơ bản
```java
try {
    // Code có thể gây exception
    int result = 10 / 0;
    System.out.println(result);       // Dòng này KHÔNG chạy
} catch (ArithmeticException e) {
    // Xử lý khi bắt được exception
    System.out.println("Lỗi: " + e.getMessage());  // "Lỗi: / by zero"
} finally {
    // LUÔN LUÔN chạy, dù có exception hay không
    System.out.println("Khối finally luôn chạy");
}
System.out.println("Chương trình tiếp tục chạy bình thường");
```

### 3.2 Luồng thực thi

```
              ┌────────────────────────┐
              │     Bắt đầu try        │
              └───────────┬────────────┘
                          │
                          ▼
              ┌────────────────────────┐
              │   Exception xảy ra?    │
              └─────┬────────────┬─────┘
                CÓ  │            │  KHÔNG
                    ▼            ▼
┌────────────────────────┐  ┌────────────────────────┐
│ Nhảy vào khối catch    │  │ Chạy hết khối try      │
│ tương ứng để xử lý     │  │ một cách bình thường   │
└───────────────────┬────┘  └────┬───────────────────┘
                    │            │
                    └─────┬──────┘
                          ▼
              ┌────────────────────────┐
              │  finally (luôn chạy)   │
              │(Giải phóng tài nguyên) │
              └───────────┬────────────┘
                          │
                          ▼
              ┌────────────────────────┐
              │ Tiếp tục code sau khối │
              │      try - catch       │
              └────────────────────────┘
```

### 3.3 Bắt nhiều Exception
```java
try {
    String s = null;
    s.length();         // NullPointerException
} catch (NullPointerException e) {
    System.out.println("Lỗi null: " + e.getMessage());
} catch (ArithmeticException e) {
    System.out.println("Lỗi số học: " + e.getMessage());
} catch (Exception e) {
    // Catch chung (đặt cuối cùng, vì Exception là cha của tất cả)
    System.out.println("Lỗi khác: " + e.getMessage());
}

// Hoặc gộp nhiều exception trong 1 catch (Java 7+):
try {
    // ...
} catch (NullPointerException | ArithmeticException e) {
    System.out.println("Lỗi: " + e.getMessage());
}
```

> ⚠️ **Thứ tự catch:** Từ Exception **cụ thể** → **tổng quát** (con trước, cha sau).

## 4. throw & throws

### 4.1 `throw` – Quăng exception ra
```java
public void setAge(int age) {
    if (age < 0 || age > 150) {
        throw new IllegalArgumentException("Tuổi không hợp lệ: " + age);
    }
    this.age = age;
}
```

### 4.2 `throws` – Khai báo method có thể quăng exception
```java
// Khai báo: method này CÓ THỂ quăng IOException (checked)
// Người gọi method PHẢI xử lý (try-catch hoặc throws tiếp)
public String readFile(String path) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(path));
    return reader.readLine();
}
```

### 4.3 So sánh throw vs throws

| | `throw` | `throws` |
|---|---------|---------|
| Vị trí | Trong **thân** method | Tại **khai báo** method |
| Mục đích | **Quăng** 1 exception cụ thể | **Khai báo** method có thể quăng exception |
| Số lượng | 1 exception mỗi lần | Nhiều exception (phẩy phân cách) |
| Ví dụ | `throw new RuntimeException("msg");` | `void read() throws IOException, SQLException` |

## 5. Custom Exception (Ngoại lệ tự tạo)

### 5.1 Tại sao cần Custom Exception?
- Exception có sẵn quá chung chung, không mô tả đúng lỗi nghiệp vụ.
- Custom Exception giúp code **rõ ràng hơn** và dễ xử lý theo từng loại lỗi.

### 5.2 Tạo Unchecked Custom Exception (phổ biến nhất)
```java
// Kế thừa RuntimeException → KHÔNG bắt buộc try-catch
public class ResourceNotFoundException extends RuntimeException {

    public ResourceNotFoundException(String message) {
        super(message);
    }

    public ResourceNotFoundException(String resourceName, Long id) {
        super(resourceName + " không tìm thấy với ID: " + id);
    }
}

// Sử dụng:
public User getUserById(Long id) {
    return userRepository.findById(id)
        .orElseThrow(() -> new ResourceNotFoundException("User", id));
    // Quăng: "User không tìm thấy với ID: 5"
}
```

### 5.3 Tạo Checked Custom Exception (ít dùng hơn)
```java
// Kế thừa Exception → BẮT BUỘC try-catch
public class InsufficientBalanceException extends Exception {

    private final double currentBalance;
    private final double withdrawAmount;

    public InsufficientBalanceException(double currentBalance, double withdrawAmount) {
        super("Số dư không đủ. Hiện có: " + currentBalance + ", cần rút: " + withdrawAmount);
        this.currentBalance = currentBalance;
        this.withdrawAmount = withdrawAmount;
    }
    
    // Getter nếu cần
}
```

## 6. Try-with-Resources (Java 7+)

### 6.1 Vấn đề: Quên đóng tài nguyên
```java
// ❌ Phải đóng resource trong finally (code dài dòng, dễ quên)
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("data.txt"));
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try { reader.close(); } catch (IOException e) { e.printStackTrace(); }
    }
}
```

### 6.2 Giải pháp: try-with-resources
```java
// ✅ Tự động đóng resource khi kết thúc try (gọn, an toàn)
try (BufferedReader reader = new BufferedReader(new FileReader("data.txt"))) {
    String line = reader.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
// reader.close() được gọi TỰ ĐỘNG khi ra khỏi try, dù có exception hay không
```

### 6.3 Điều kiện sử dụng
- Resource phải implement interface `AutoCloseable` (hoặc `Closeable`).
- Có thể khai báo **nhiều resource** cách nhau bằng `;`:

```java
try (
    FileInputStream fis = new FileInputStream("input.txt");
    FileOutputStream fos = new FileOutputStream("output.txt")
) {
    // Đọc input, ghi output
} catch (IOException e) {
    e.printStackTrace();
}
// Cả fis và fos đều tự động đóng
```

## 7. Best Practices xử lý Exception

| ✅ Nên | ❌ Không nên |
|--------|-------------|
| Bắt exception **cụ thể** (`NullPointerException`) | Bắt `Exception` chung chung |
| Ghi log đầy đủ (`logger.error("msg", e)`) | Bắt rồi **nuốt** (catch trống rỗng) |
| Dùng **Custom Exception** cho lỗi nghiệp vụ | Dùng `RuntimeException("msg")` chung chung |
| Dùng `try-with-resources` cho I/O | Tự `close()` trong finally |
| Quăng sớm, bắt muộn (Throw early, Catch late) | Bắt exception ở mọi nơi |

```java
// ❌ Anti-pattern: Nuốt exception (swallowing)
try {
    riskyOperation();
} catch (Exception e) {
    // Không làm gì cả → bug ẩn, rất khó debug!
}

// ✅ Best practice: Log hoặc throw lại
try {
    riskyOperation();
} catch (SpecificException e) {
    logger.error("Lỗi khi xử lý: {}", e.getMessage(), e);
    throw new BusinessException("Xử lý thất bại", e);
}
```

## 8. Câu hỏi phỏng vấn & Trả lời chi tiết

### 8.1. Phân biệt Checked và Unchecked Exception? Cho ví dụ mỗi loại
| Tiêu chí | Checked Exception | Unchecked Exception (Runtime) |
| :--- | :--- | :--- |
| **Kế thừa từ** | Kế thừa trực tiếp từ `Exception` (trừ `RuntimeException`). | Kế thừa từ `RuntimeException`. |
| **Thời điểm kiểm tra** | **Compile-time** (Trình biên dịch bắt buộc phải xử lý bằng `try-catch` hoặc khai báo `throws`). | **Runtime** (Trình biên dịch không bắt buộc khai báo hay bắt lỗi). |
| **Bản chất nguyên nhân** | Lỗi ngoại cảnh nằm ngoài tầm kiểm soát của code (Mạng rớt, file không tồn tại, kết nối DB ngắt). | Lỗi do **bug logic của lập trình viên** (truy cập null, chia cho 0, vượt biên mảng). |
| **Ví dụ điển hình** | `IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`. | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`. |

### 8.2. Phân biệt `Error` và `Exception`?
- Cả hai đều kế thừa từ lớp cha `Throwable`:
  - **`Error`:** Đại diện cho các **sự cố nghiêm trọng ở mức hệ thống / máy ảo JVM** (ví dụ: `OutOfMemoryError`, `StackOverflowError`). Ứng dụng thông thường **không nên và không thể bắt (`catch`) hay phục hồi** khi gặp `Error`. Khi `Error` xảy ra, ứng dụng thường phải dừng lại.
  - **`Exception`:** Đại diện cho các **tình huống ngoại lệ trong luồng thực thi của ứng dụng** mà lập trình viên có thể lường trước, bắt lại bằng `try-catch` và xử lý khắc phục (graceful degradation) để chương trình tiếp tục chạy ổn định.

### 8.3. Khối `finally` có LUÔN LUÔN chạy không?
- **Quy tắc chung:** Khối `finally` **gần như luôn luôn chạy**, kể cả khi trong khối `try` hoặc `catch` có lệnh `return`, `continue`, hoặc văng ra exception khác.
- **Những trường hợp hiếm hoi `finally` KHÔNG chạy:**
  1. Gọi lệnh tắt JVM cưỡng bức: `System.exit(0);`
  2. Máy chủ bị sập nguồn điện đột ngột hoặc tiến trình JVM bị hệ điều hành kill (`kill -9`).
  3. Lỗi phần cứng hoặc JVM bị crash nặng (`Fatal Error`).
  4. Vòng lặp vô hạn bên trong khối `try` khiến luồng không bao giờ chạm tới được `finally`.

### 8.4. `throw` và `throws` khác nhau thế nào?
| Tiêu chí | Từ khóa `throw` | Từ khóa `throws` |
| :--- | :--- | :--- |
| **Vị trí sử dụng** | Nằm **bên trong thân hàm / phương thức**. | Nằm ở **chữ ký phương thức (Method Signature)**. |
| **Mục đích** | Chủ động **kích hoạt / ném ra** một đối tượng ngoại lệ cụ thể (`throw new BusinessException("Lỗi");`). | **Cảnh báo / Khai báo** rằng phương thức này CÓ THỂ ném ra các loại ngoại lệ nào để nơi gọi nó chuẩn bị xử lý. |
| **Cú pháp** | Theo sau là một **đối tượng ngoại lệ (Instance)**: `throw exceptionInstance;` | Theo sau là một hoặc nhiều **tên lớp ngoại lệ (Class Name)**: `throws IOException, SQLException` |

### 8.5. Tại sao nên tạo Custom Exception thay vì dùng `RuntimeException` trực tiếp?
1. **Phân loại nghiệp vụ rõ ràng:** Tạo `UserNotFoundException`, `InsufficientBalanceException` giúp code mang tính tự diễn giải (Self-documenting), người đọc hiểu ngay lỗi nghiệp vụ là gì.
2. **Bắt lỗi tập trung (Global Exception Handling):** Trong Spring Boot (`@RestControllerAdvice`), ta có thể viết các hàm `@ExceptionHandler` riêng cho từng Custom Exception để trả về đúng mã HTTP Status (ví dụ: `UserNotFoundException` trả về `404 Not Found`, `InvalidOrderException` trả về `400 Bad Request`).
3. **Đính kèm dữ liệu bổ sung:** Custom Exception có thể chứa thêm các trường dữ liệu tùy biến (ví dụ: `errorCode`, `timestamp`, `fieldName`) để phục vụ việc debug và trả lỗi chi tiết cho Frontend.

### 8.6. Try-with-resources hoạt động thế nào? Điều kiện để resource được tự đóng?
- **Cơ chế:** Khối `try (Resource res = new Resource())` đảm bảo hàm `res.close()` sẽ luôn luôn được tự động gọi khi luồng thực thi rời khỏi khối `try`, bất kể có exception xảy ra hay không.
- **Điều kiện bắt buộc:** Biến tài nguyên được khai báo trong ngoặc tròn của `try` **phải implement interface `java.lang.AutoCloseable`** (hoặc con của nó là `java.io.Closeable`).
- **Ưu điểm:** Loại bỏ hoàn toàn mã thừa thãi `finally { res.close(); }`, tránh rò rỉ tài nguyên (Resource Leak), và tự động xử lý các trường hợp ngoại lệ bị che lấp (Suppressed Exceptions).

### 8.7. Thứ tự `catch` có quan trọng không? Nếu để `catch (Exception e)` trước `catch (IOException e)` thì sao?
- **Thứ tự CỰC KỲ QUAN TRỌNG:** Phải luôn bắt các Exception **từ cụ thể đến chung chung (từ lớp con tới lớp cha)**.
- **Nếu để `catch (Exception e)` trước `catch (IOException e)`:**
  - Chương trình sẽ **bị lỗi biên dịch (Compilation Error: Unreachable code)**.
  - *Lý do:* Vì `IOException` là lớp con kế thừa từ `Exception`. Khi có ngoại lệ `IOException` xảy ra, khối `catch (Exception e)` nằm ở trên đã tóm gọn nó trước, khiến cho khối `catch (IOException e)` phía dưới sẽ **vĩnh viễn không bao giờ được chạm tới**.

### 8.8. Giải thích nguyên tắc "Throw early, Catch late"
- **Throw early (Ném lỗi càng sớm càng tốt):** Ngay khi phát hiện tham số không hợp lệ hoặc điều kiện tiên quyết bị vi phạm ở đầu hàm, ném ngoại lệ ngay lập tức (ví dụ: `if (id == null) throw new IllegalArgumentException();`). Tránh để dữ liệu sai đi sâu vào hệ thống rồi mới phát sinh lỗi khó đoán ở tầng Database.
- **Catch late (Bắt lỗi càng muộn càng tốt):** Không nên vội vàng đặt `try-catch` ở khắp mọi hàm nhỏ nếu hàm đó không biết cách khắc phục lỗi. Hãy để ngoại lệ nổi lên (bubble up) tới các tầng trên cùng (như Controller hoặc Global Exception Handler) - nơi có bức tranh toàn cảnh và thẩm quyền quyết định: ghi log ra sao, rollback transaction thế nào, và trả thông điệp gì cho người dùng.

---
*Thực hành:* Viết code bắt `ArithmeticException` và `ArrayIndexOutOfBoundsException`, tạo `ResourceNotFoundException` kế thừa `RuntimeException`, thử `try-with-resources` đọc file.

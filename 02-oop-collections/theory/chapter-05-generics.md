# Chapter 05: Generics & Bounded Type Parameters

## 1. Generics là gì?
- Generics cho phép viết code **an toàn kiểu dữ liệu** (type-safe) tại compile-time mà vẫn linh hoạt.
- Thay vì ép kiểu thủ công, compiler kiểm tra lỗi kiểu ngay khi viết code.

```java
// Không có Generics → phải ép kiểu, dễ lỗi runtime
List list = new ArrayList();
list.add("Hello");
list.add(123);               // Compile OK nhưng...
String s = (String) list.get(1);  // ❌ ClassCastException tại runtime!

// Có Generics → compiler bắt lỗi ngay
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123);             // ❌ Compile Error (an toàn!)
String s = list.get(0);       // Không cần ép kiểu
```

## 2. Generic Class
```java
public class ApiResponse<T> {
    private int statusCode;
    private String message;
    private T data;           // T là kiểu tuỳ ý, quyết định khi tạo object

    public ApiResponse(int statusCode, String message, T data) {
        this.statusCode = statusCode;
        this.message = message;
        this.data = data;
    }
    // Getter/Setter...
}

// Sử dụng:
ApiResponse<User> userRes = new ApiResponse<>(200, "OK", new User("An"));
ApiResponse<List<Product>> productRes = new ApiResponse<>(200, "OK", productList);
```

## 3. Generic Method
```java
public class Utils {
    // <T> khai báo trước return type
    public static <T> void printArray(T[] arr) {
        for (T item : arr) System.out.print(item + " ");
    }
}

String[] names = {"An", "Bình"};
Integer[] nums = {1, 2, 3};
Utils.printArray(names);  // An Bình
Utils.printArray(nums);   // 1 2 3
```

## 4. Bounded Type Parameters
```java
// T phải là Number hoặc subclass của Number
public static <T extends Number> double sum(List<T> list) {
    double total = 0;
    for (T item : list) total += item.doubleValue();
    return total;
}

sum(List.of(1, 2, 3));        // ✅ Integer extends Number
sum(List.of(1.5, 2.5));       // ✅ Double extends Number
// sum(List.of("a", "b"));    // ❌ String không extends Number

// Multiple bounds
public <T extends Comparable<T> & Serializable> T findMax(List<T> list) { ... }
```

## 5. Wildcards (`?`)

| Wildcard | Ý nghĩa | Đọc/Ghi |
|----------|---------|---------|
| `<?>` | Bất kỳ kiểu nào | Chỉ đọc (read-only) |
| `<? extends T>` | T hoặc subclass của T | Chỉ đọc (Producer) |
| `<? super T>` | T hoặc superclass của T | Ghi được (Consumer) |

### PECS: Producer Extends, Consumer Super
```java
// Producer (đọc dữ liệu ra): extends
public double sumOfList(List<? extends Number> list) {
    double sum = 0;
    for (Number n : list) sum += n.doubleValue();  // Đọc OK
    // list.add(1);  // ❌ Không ghi được
    return sum;
}

// Consumer (ghi dữ liệu vào): super
public void addNumbers(List<? super Integer> list) {
    list.add(1);     // Ghi OK
    list.add(2);
    // Integer n = list.get(0); // ❌ Không đọc chính xác kiểu được
}
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Generics giải quyết vấn đề gì? Type Erasure là gì?
- **2 Vấn đề lớn mà Generics giải quyết:**
  1. **An toàn kiểu dữ liệu tại Compile-time (Type Safety):** Trước Java 5, `ArrayList` lưu `Object`. Lập trình viên có thể vô tình nhét nhầm `Integer` vào danh sách `String`. Đến khi chạy chương trình mới văng lỗi `ClassCastException`. Generics phát hiện và chặn đứng lỗi này ngay khi đang gõ code.
  2. **Loại bỏ việc ép kiểu thủ công (Eliminate Type Casting):** Không cần phải viết `String s = (String) list.get(0);` ở khắp mọi nơi nữa.
- **Type Erasure (Xóa bỏ kiểu) là gì?**
  - Là cơ chế của Java Compiler nhằm đảm bảo **tính tương thích ngược (Backward Compatibility)** với các phiên bản Java cũ (Java 1.4 trở về trước).
  - Lúc Compile-time: Compiler kiểm tra tính hợp lệ của kiểu `<T>`.
  - Lúc sinh Bytecode: Compiler **xóa bỏ toàn bộ thông tin generic `<T>`** và thay thế bằng kiểu giới hạn trên của nó (thường là `Object` hoặc `Number`), đồng thời tự động chèn các lệnh ép kiểu bytecode thích hợp.
  - $\rightarrow$ Do đó, lúc **Runtime**, JVM hoàn toàn không biết `List<String>` hay `List<Integer>`, đối với JVM chúng đều chỉ là `List` thông thường.

### 6.2. `<T extends Number>` nghĩa là gì? (Bounded Type Parameter)
- **Ý nghĩa:** Giới hạn trên (Upper Bound). Nó quy định rằng kiểu dữ liệu thay thế cho `T` **bắt buộc phải là `Number` hoặc là một lớp con của `Number`** (chẳng hạn như `Integer`, `Double`, `Float`, `Long`, `Byte`, `Short`).
- **Lợi ích:**
  - Ngăn không cho truyền các kiểu không hợp lệ vào (ví dụ truyền `String` hay `User` vào sẽ bị báo lỗi compile ngay).
  - Cho phép bên trong thân hàm/class được phép gọi trực tiếp các phương thức của lớp `Number` (như `.doubleValue()`, `.intValue()`) mà không cần phải ép kiểu.

### 6.3. Phân biệt `<? extends T>` và `<? super T>`. Giải thích nguyên tắc PECS
- **`<? extends T>` (Upper Bounded Wildcard):** Chấp nhận kiểu `T` hoặc bất kỳ kiểu con nào của `T`.
- **`<? super T>` (Lower Bounded Wildcard):** Chấp nhận kiểu `T` hoặc bất kỳ kiểu cha nào của `T` (lên tới `Object`).
- **Nguyên tắc vàng PECS (Producer Extends, Consumer Super):**
  - **Producer Extends:** Nếu Collection đóng vai trò là **nguồn cung cấp dữ liệu** (bạn chỉ lấy dữ liệu ra để đọc: `get()`, duyệt for) $\rightarrow$ Dùng `<? extends T>`. *(Lưu ý: Không được phép gọi `.add()` vào list này vì compiler không biết chính xác kiểu con cụ thể là gì).*
  - **Consumer Super:** Nếu Collection đóng vai trò là **nơi tiếp nhận dữ liệu** (bạn ghi dữ liệu mới vào: `add()`) $\rightarrow$ Dùng `<? super T>`. *(Lúc này an toàn 100% để add đối tượng kiểu `T` hoặc con của `T` vào list).*

### 6.4. Tại sao không thể tạo `new T()` hoặc `new T[]` trong Generic?
- **Nguyên nhân chính:** Do cơ chế **Type Erasure**.
  - Để thực thi lệnh `new T()`, JVM lúc runtime cần phải biết kích thước bộ nhớ chính xác của `T` và cần constructor cụ thể nào để gọi. Nhưng do Type Erasure, lúc runtime `T` đã bị xóa thành `Object`, JVM không thể biết `T` thực sự là gì để cấp phát.
  - Tương tự, mảng trong Java là Reifiable (lưu giữ kiểu phần tử lúc runtime để kiểm tra an toàn mảng `ArrayStoreException`), trong khi Generics lại bị Erasure lúc runtime, hai cơ chế này xung đột trực tiếp nên Java cấm `new T[10]`.
- **Cách giải quyết thực tế:**
  - Truyền đối tượng `Class<T> clazz` vào constructor và dùng Reflection: `clazz.getDeclaredConstructor().newInstance()`.
  - Hoặc tạo mảng Object rồi ép kiểu: `(T[]) new Object[size];` (như cách mã nguồn của `ArrayList` trong JDK đang làm).

---
*Thực hành:* Tạo `ApiResponse<T>`, viết hàm `sumOfList(List<? extends Number>)`, áp dụng PECS.

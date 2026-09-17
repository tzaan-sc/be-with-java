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

## 6. Câu hỏi phỏng vấn
1. Generics giải quyết vấn đề gì? Type Erasure là gì?
2. `<T extends Number>` nghĩa là gì?
3. Phân biệt `<? extends T>` và `<? super T>`. Giải thích PECS.
4. Tại sao không thể tạo `new T()` hoặc `new T[]` trong generic method?

---
*Thực hành:* Tạo `ApiResponse<T>`, viết hàm `sumOfList(List<? extends Number>)`, áp dụng PECS.

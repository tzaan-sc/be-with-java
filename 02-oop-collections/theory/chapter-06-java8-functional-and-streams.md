# Chapter 06: Java 8 – Lambda, Functional Interface, Stream API & Optional

## 1. Lambda Expression
- Cú pháp viết gọn cho **anonymous class** chỉ có 1 method (Functional Interface).

```java
// Trước Java 8: Anonymous class
Comparator<String> comp = new Comparator<String>() {
    @Override
    public int compare(String a, String b) { return a.compareTo(b); }
};

// Java 8 Lambda
Comparator<String> comp = (a, b) -> a.compareTo(b);

// Method Reference (ngắn hơn nữa)
Comparator<String> comp = String::compareTo;
```

### Cú pháp Lambda
```java
(parameters) -> expression              // 1 dòng, tự return
(parameters) -> { statements; }         // Nhiều dòng, cần return tường minh
() -> System.out.println("Hello")       // Không tham số
x -> x * 2                              // 1 tham số, bỏ dấu ()
```

## 2. Functional Interface (4 cốt lõi)

| Interface | Input | Output | Method | Ví dụ |
|-----------|-------|--------|--------|-------|
| `Predicate<T>` | T | boolean | `test(T)` | Kiểm tra điều kiện |
| `Function<T,R>` | T | R | `apply(T)` | Biến đổi kiểu |
| `Consumer<T>` | T | void | `accept(T)` | Nhận và xử lý |
| `Supplier<T>` | — | T | `get()` | Cung cấp dữ liệu |

```java
Predicate<Integer> isAdult = age -> age >= 18;
isAdult.test(20);  // true

Function<String, Integer> strLen = String::length;
strLen.apply("Hello");  // 5

Consumer<String> printer = System.out::println;
printer.accept("Hi!");  // In "Hi!"

Supplier<Double> random = Math::random;
random.get();  // 0.xxxx
```

## 3. Stream API

### Pipeline: Source → Intermediate → Terminal
```java
List<String> names = List.of("An", "Bình", "Cường", "An", "Dũng");

List<String> result = names.stream()       // 1. Source
    .filter(n -> n.length() > 2)           // 2. Intermediate: lọc
    .map(String::toUpperCase)              // 2. Intermediate: biến đổi
    .distinct()                            // 2. Intermediate: loại trùng
    .sorted()                              // 2. Intermediate: sắp xếp
    .toList();                             // 3. Terminal: thu kết quả
// ["BÌNH", "CƯỜNG", "DŨNG"]
```

### Intermediate Operations (Lazy – chưa chạy ngay)
| Method | Mô tả |
|--------|-------|
| `filter(Predicate)` | Lọc phần tử thoả điều kiện |
| `map(Function)` | Biến đổi mỗi phần tử (1→1) |
| `flatMap(Function)` | Làm phẳng danh sách lồng (1→N) |
| `distinct()` | Loại phần tử trùng |
| `sorted()` / `sorted(Comparator)` | Sắp xếp |
| `limit(n)` / `skip(n)` | Giới hạn / bỏ qua n phần tử |
| `peek(Consumer)` | Debug: xem giá trị giữa pipeline |

### Terminal Operations (Kích hoạt stream chạy)
| Method | Mô tả |
|--------|-------|
| `toList()` / `collect(Collectors.toList())` | Thu về List |
| `forEach(Consumer)` | Duyệt và xử lý |
| `count()` | Đếm |
| `reduce(BinaryOperator)` | Gộp thành 1 giá trị |
| `findFirst()` / `findAny()` | Tìm phần tử (trả Optional) |
| `anyMatch` / `allMatch` / `noneMatch` | Kiểm tra điều kiện |

### Collectors nâng cao
```java
// groupingBy: Gom nhóm theo category
Map<String, List<Product>> grouped = products.stream()
    .collect(Collectors.groupingBy(Product::getCategory));

// joining: Nối chuỗi
String csv = names.stream().collect(Collectors.joining(", "));

// toMap: Chuyển về Map
Map<Long, String> idToName = users.stream()
    .collect(Collectors.toMap(User::getId, User::getName));
```

### map() vs flatMap()
```java
// map: 1 → 1
List<String> upper = List.of("an", "bình").stream()
    .map(String::toUpperCase).toList();  // ["AN", "BÌNH"]

// flatMap: 1 → N (làm phẳng)
List<List<Integer>> nested = List.of(List.of(1,2), List.of(3,4));
List<Integer> flat = nested.stream()
    .flatMap(Collection::stream).toList();  // [1, 2, 3, 4]
```

## 4. Optional\<T\> – Xử lý Null an toàn

```java
// Tạo Optional
Optional<String> opt1 = Optional.of("Hello");          // Không được null
Optional<String> opt2 = Optional.ofNullable(null);     // Cho phép null
Optional<String> opt3 = Optional.empty();              // Rỗng

// Lấy giá trị an toàn
opt2.orElse("Default");                                // "Default"
opt2.orElseGet(() -> "Computed Default");               // Lazy evaluation
opt2.orElseThrow(() -> new RuntimeException("Empty!")); // Quăng exception

// Chuỗi xử lý
Optional<User> userOpt = userRepository.findById(1L);
String email = userOpt
    .map(User::getEmail)
    .filter(e -> e.contains("@"))
    .orElse("unknown@email.com");

// ❌ Tránh dùng: opt.get() (NullPointerException nếu empty)
// ❌ Tránh dùng: opt.isPresent() rồi opt.get() (code cũ)
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Lambda Expression là gì? Khác Anonymous Class thế nào?
- **Khái niệm:** Lambda Expression là một hàm ẩn danh (Anonymous Function) không có tên, không có kiểu trả về khai báo cụ thể, cho phép truyền hành vi (Behavior) dưới dạng tham số một cách cực kỳ ngắn gọn: `(params) -> { body }`.
- **So sánh Lambda vs Anonymous Class:**
  | Tiêu chí | Lambda Expression (Java 8+) | Anonymous Class (Lớp ẩn danh cũ) |
  | :--- | :--- | :--- |
  | **Cú pháp** | Cực kỳ ngắn gọn: `x -> x * 2`. | Cồng kềnh: Phải `new Interface() { public ... }`. |
  | **Cơ chế biên dịch** | Dùng chỉ lệnh bytecode **`invokedynamic`** (không tạo file `.class` mới trên ổ đĩa, tiết kiệm Metaspace và khởi động nhanh). | Trình biên dịch sinh ra một file class riêng: `OuterClass$1.class`. |
  | **Phạm vi từ khóa `this`** | `this` trỏ tới **chính đối tượng của class bao bọc bên ngoài (Enclosing class)**. | `this` trỏ tới **bản thân thể hiện của Anonymous class đó**. |
  | **Khả năng áp dụng** | **Chỉ áp dụng** cho **Functional Interface** (interface có đúng 1 abstract method). | Áp dụng cho bất kỳ Interface hoặc Abstract class nào (kể cả có nhiều method). |

### 5.2. Kể tên 4 Functional Interface cốt lõi trong Java và mục đích
1. **`Predicate<T>` (Kiểm tra điều kiện):**
   - Method: `boolean test(T t)`
   - Nhận vào 1 đối tượng, trả về `true/false`. Thường dùng trong hàm `.filter()` của Stream (ví dụ: `u -> u.getAge() >= 18`).
2. **`Function<T, R>` (Biến đổi dữ liệu):**
   - Method: `R apply(T t)`
   - Nhận vào đối tượng kiểu `T`, biến đổi và trả về kiểu `R`. Thường dùng trong `.map()` (ví dụ: `User -> UserDTO`, `User::getName`).
3. **`Consumer<T>` (Tiêu thụ dữ liệu):**
   - Method: `void accept(T t)`
   - Nhận vào đối tượng kiểu `T` để xử lý (in ra màn hình, gửi log, lưu DB) và không trả về gì. Thường dùng trong `.forEach()` (ví dụ: `System.out::println`).
4. **`Supplier<T>` (Cung cấp dữ liệu):**
   - Method: `T get()`
   - Không nhận tham số đầu vào, tự sản sinh và trả về một đối tượng kiểu `T`. Thường dùng trong Lazy Evaluation hoặc tạo Factory (ví dụ: `() -> new NotFoundException()`).

### 5.3. Stream Intermediate vs Terminal operations? Lazy Evaluation nghĩa là gì?
- **Intermediate Operations (Thao tác trung gian):**
  - Trả về một `Stream` mới (ví dụ: `.filter()`, `.map()`, `.sorted()`, `.distinct()`, `.limit()`).
  - Có thể xâu chuỗi (chain) liên tiếp nhiều thao tác với nhau.
- **Terminal Operations (Thao tác kết thúc):**
  - Trả về một kết quả cụ thể hoặc kiểu void (ví dụ: `.collect()`, `.count()`, `.forEach()`, `.findFirst()`, `.reduce()`).
  - Khi Terminal operation được gọi, Stream sẽ thực thi và sau đó **bị đóng vĩnh viễn** (không thể tái sử dụng lại Stream đó).
- **Lazy Evaluation (Thực thi lười biếng / Trì hoãn):**
  - Các thao tác Intermediate **hoàn toàn KHÔNG chạy ngay** khi được khai báo. Chúng chỉ được kích hoạt khi và chỉ khi gặp một Terminal operation.
  - *Lợi ích:* Tối ưu hiệu năng vượt trội. Nếu bạn có danh sách 1 triệu phần tử, lọc rồi `.findFirst()`, Java sẽ dừng duyệt ngay tại phần tử đầu tiên thỏa mãn chứ không bao giờ lọc toàn bộ 1 triệu phần tử!

### 5.4. `map()` vs `flatMap()` khác nhau thế nào?
- **`map()` (Ánh xạ 1 - 1):**
  - Chuyển đổi mỗi phần tử trong Stream thành một phần tử mới.
  - Ví dụ: `Stream<String>` biến đổi thành `Stream<Integer>` (lấy độ dài chuỗi).
- **`flatMap()` (Ánh xạ 1 - Nhiều & Làm phẳng - Flatten):**
  - Chuyển đổi mỗi phần tử thành một Stream con, sau đó "làm phẳng" (merge) tất cả các Stream con đó thành **một Stream phẳng duy nhất**.
  - *Ví dụ kinh điển:* Một `Order` có danh sách `List<OrderItem>`.
    - Dùng `.map(Order::getItems)` $\rightarrow$ Trả về `Stream<List<OrderItem>>` (danh sách lồng nhau).
    - Dùng `.flatMap(order -> order.getItems().stream())` $\rightarrow$ Trả về `Stream<OrderItem>` phẳng, dễ dàng tính tổng hoặc lọc sản phẩm.

### 5.5. Tại sao nên dùng `Optional` thay vì return `null`?
1. **Loại bỏ lỗi kinh hoàng `NullPointerException` (NPE):** Ép buộc người gọi hàm phải chủ động kiểm tra và xử lý trường hợp không có dữ liệu ngay tại compile-time.
2. **Thể hiện rõ ý đồ của API:** Khi một hàm trả về `Optional<User> findById(Long id)`, người đọc hàm hiểu ngay: *"Dữ liệu này có thể có hoặc không tồn tại"*. Nếu trả về `User`, người ta dễ chủ quan gọi ngay `user.getName()` dẫn tới crash ứng dụng.
3. **Lập trình theo phong cách hàm (Functional Fluent API):** Dễ dàng xâu chuỗi logic với `.map()`, `.filter()`, `.orElseThrow()` mà không cần viết chuỗi `if (x != null)` lồng nhau rối rắm.

### 5.6. `orElse()` vs `orElseGet()` khác nhau thế nào? (Cạm bẫy Eager vs Lazy)
- **`orElse(defaultValue)` (Eager Evaluation - Đánh giá ngay lập tức):**
  - Biểu thức bên trong `orElse()` **LUÔN LUÔN ĐƯỢC TÍNH TOÁN / GỌI THỰC THI**, kể cả khi `Optional` **đang có giá trị**!
- **`orElseGet(() -> defaultValue)` (Lazy Evaluation - Đánh giá trì hoãn):**
  - Chỉ khi nào `Optional` **thực sự rỗng (`empty`)** thì hàm Supplier bên trong mới được gọi.
- *Cạm bẫy chết người trong Backend:*
  ```java
  // ❌ NGUY HIỂM: Hàm createDefaultUser() sẽ LUÔN ĐƯỢC CHẠY và gọi ghi DB tốn tài nguyên, dù userOpt đã tìm thấy!
  User user = userOpt.orElse(createDefaultUserInDatabase());

  // ✅ CHUẨN: Hàm chỉ chạy khi userOpt thực sự rỗng!
  User user = userOpt.orElseGet(() -> createDefaultUserInDatabase());
  ```

---
*Thực hành:* Lọc danh sách user > 18 tuổi bằng Stream, gom nhóm sản phẩm theo category, dùng Optional xử lý findById().

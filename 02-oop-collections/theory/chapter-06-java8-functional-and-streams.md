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

## 5. Câu hỏi phỏng vấn
1. Lambda Expression là gì? Khác Anonymous class thế nào?
2. Kể tên 4 Functional Interface chính và mục đích.
3. Stream Intermediate vs Terminal operations? Lazy evaluation nghĩa là gì?
4. `map()` vs `flatMap()` khác nhau thế nào?
5. Tại sao nên dùng `Optional` thay vì return `null`?
6. `orElse()` vs `orElseGet()` khác nhau thế nào? (Eager vs Lazy)

---
*Thực hành:* Lọc danh sách user > 18 tuổi bằng Stream, gom nhóm sản phẩm theo category, dùng Optional xử lý findById().

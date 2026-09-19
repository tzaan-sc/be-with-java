# Chapter 04: String, StringBuilder & String Pool

## 1. Bản chất String trong Java

### 1.1 String là Immutable (Bất biến)
- Sau khi tạo, **nội dung** của String **không thể thay đổi**.
- Mọi thao tác "thay đổi" String (concat, replace, toUpperCase…) đều **tạo ra String MỚI** trên Heap, String gốc không bị ảnh hưởng.

```java
String s = "Hello";
s.concat(" World");       // Tạo String mới "Hello World" nhưng KHÔNG gán lại cho s
System.out.println(s);    // "Hello" ← Không đổi!

s = s.concat(" World");   // Gán lại: s trỏ sang String mới "Hello World"
System.out.println(s);    // "Hello World"
// String cũ "Hello" vẫn tồn tại trên Heap (chờ GC thu hồi nếu không ai trỏ tới)
```

### 1.2 Tại sao String được thiết kế là Immutable?
| Lý do | Giải thích |
|-------|-----------|
| **Security** | Không thể sửa đổi giá trị URL, username, password sau khi tạo → tránh bị tấn công injection |
| **Thread Safety** | Nhiều Thread có thể dùng chung 1 String mà không cần synchronize |
| **String Pool** | Vì immutable nên JVM có thể chia sẻ 1 String giữa nhiều biến (caching) |
| **HashCode caching** | hashCode được tính 1 lần và cache lại → tăng performance khi dùng làm key trong HashMap |

## 2. String Pool (String Constant Pool)

### 2.1 Khái niệm
- String Pool là **vùng nhớ đặc biệt** trong Heap, JVM dùng để **tái sử dụng** các String literal trùng nhau.
- Khi viết `String s = "abc"`, JVM kiểm tra Pool:
  - Nếu `"abc"` **đã tồn tại** → trả về reference tới String cũ (không tạo mới).
  - Nếu **chưa có** → tạo mới trong Pool.

### 2.2 Minh hoạ

```
┌────────────────────────┐             ┌────────────────────────────────────────────────────────┐
│      STACK MEMORY      │             │                      HEAP MEMORY                       │
├────────────────────────┤             ├────────────────────────────────────────────────────────┤
│                        │             │                                                        │
│  a ────────────────────┼─────────────┼─┐   ┌───────────────────────────────┐                  │
│                        │             │ │   │          String Pool          │                  │
│  b ────────────────────┼─────────────┼─┴──►│  "java"  (tại địa chỉ 0xA1)   │                  │
│                        │             │     └───────────────────────────────┘                  │
│                        │             │                                                        │
│  c ────────────────────┼─────────────┼───► new String("java") (Object ngoài Pool tại 0xC3)    │
│                        │             │                                                        │
└────────────────────────┘             └────────────────────────────────────────────────────────┘
```

```java
String a = "java";              // Tạo "java" trong Pool
String b = "java";              // Tìm thấy "java" trong Pool → dùng lại
String c = new String("java");  // Tạo object MỚI trên Heap (NGOÀI Pool)

System.out.println(a == b);       // true  (cùng trỏ 1 object trong Pool)
System.out.println(a == c);       // false (a trỏ Pool, c trỏ Heap khác)
System.out.println(a.equals(c));  // true  (nội dung giống nhau)
```

### 2.3 Phương thức `intern()`
```java
String c = new String("java");
String d = c.intern();   // Đưa "java" vào Pool (hoặc lấy lại nếu đã có)
System.out.println(a == d);  // true (d giờ trỏ vào Pool giống a)
```

## 3. So sánh `==` vs `.equals()`

| Toán tử | So sánh gì | Dùng cho |
|---------|-----------|---------|
| `==` | **Địa chỉ bộ nhớ** (reference) | Primitive (so giá trị), Reference (so địa chỉ) |
| `.equals()` | **Nội dung** (đã override trong String) | So sánh nội dung String, Object |

> 🔴 **Quy tắc vàng:** Luôn dùng `.equals()` khi so sánh nội dung String. KHÔNG dùng `==` cho String.

```java
String x = "hello";
String y = new String("hello");

System.out.println(x == y);          // false ← So sánh địa chỉ
System.out.println(x.equals(y));     // true  ← So sánh nội dung
System.out.println(x.equalsIgnoreCase("HELLO"));  // true ← Bỏ qua hoa/thường
```

## 4. Các method String thường dùng

```java
String s = "  Hello World  ";

s.length();                    // 15 (tính cả khoảng trắng)
s.trim();                      // "Hello World" (xoá khoảng trắng 2 đầu)
s.strip();                     // "Hello World" (Java 11, xử lý Unicode tốt hơn trim)
s.toLowerCase();               // "  hello world  "
s.toUpperCase();               // "  HELLO WORLD  "
s.charAt(2);                   // 'H' (ký tự tại index 2)
s.indexOf("World");            // 8 (vị trí đầu tiên tìm thấy)
s.contains("Hello");           // true
s.startsWith("  He");          // true
s.endsWith("  ");              // true
s.substring(2, 7);             // "Hello" (từ index 2 đến 6)
s.replace("World", "Java");   // "  Hello Java  "
s.isEmpty();                   // false (có ký tự)
s.isBlank();                   // false (Java 11, kiểm tra cả khoảng trắng)
"".isEmpty();                  // true
"   ".isBlank();               // true (chỉ có khoảng trắng)

// Chuyển đổi
String.valueOf(123);           // "123" (int → String)
Integer.parseInt("123");       // 123  (String → int)
Double.parseDouble("3.14");    // 3.14 (String → double)

// Tách / Nối
String csv = "a,b,c,d";
String[] parts = csv.split(",");         // ["a", "b", "c", "d"]
String joined = String.join("-", parts); // "a-b-c-d"
```

## 5. StringBuilder & StringBuffer

### 5.1 Vấn đề khi nối String trong vòng lặp
```java
// ❌ CHẬM: Mỗi lần += tạo 1 String MỚI → O(n²) bộ nhớ
String result = "";
for (int i = 0; i < 10000; i++) {
    result += i;  // Tạo 10.000 object String tạm trên Heap!
}
```

### 5.2 Giải pháp: StringBuilder (Mutable)
```java
// ✅ NHANH: StringBuilder sửa trực tiếp buffer nội bộ
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append(i);  // Không tạo object mới
}
String result = sb.toString();
```

### 5.3 Các method StringBuilder phổ biến
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");         // "Hello World"
sb.insert(5, ",");           // "Hello, World"
sb.delete(5, 6);             // "Hello World"
sb.replace(6, 11, "Java");  // "Hello Java"
sb.reverse();                // "avaJ olleH"
sb.length();                 // 10
sb.toString();               // Chuyển về String
```

### 5.4 StringBuilder vs StringBuffer

| Tiêu chí | StringBuilder | StringBuffer |
|----------|--------------|-------------|
| Thread‑safe? | ❌ Không (nhanh hơn) | ✅ Có (synchronized) |
| Performance | ⚡ Nhanh | 🐢 Chậm hơn do lock |
| Khi nào dùng? | **Single-thread** (99% trường hợp) | **Multi-thread** (hiếm dùng) |

> 💡 Trong thực tế, **luôn dùng StringBuilder** trừ khi có yêu cầu thread-safe rõ ràng.

### 5.5 Đo thời gian thực thi
```java
// Đo String concatenation
long start = System.currentTimeMillis();
String s = "";
for (int i = 0; i < 100000; i++) { s += "a"; }
long end = System.currentTimeMillis();
System.out.println("String: " + (end - start) + "ms");   // ~5000ms+

// Đo StringBuilder
start = System.currentTimeMillis();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 100000; i++) { sb.append("a"); }
end = System.currentTimeMillis();
System.out.println("StringBuilder: " + (end - start) + "ms"); // ~3ms
```

## 6. Tóm tắt khi nào dùng gì

| Tình huống | Dùng |
|-----------|------|
| Chuỗi ít thay đổi, gán 1 lần | `String` |
| Nối chuỗi trong vòng lặp | `StringBuilder` |
| Nối chuỗi trong môi trường multi-thread | `StringBuffer` |
| So sánh nội dung chuỗi | `.equals()` hoặc `.equalsIgnoreCase()` |
| So sánh xem có cùng 1 object không | `==` (hiếm khi cần) |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Tại sao String trong Java là Immutable (Bất biến)? Lợi ích?
- **Khái niệm:** Một khi đối tượng `String` được tạo ra trên Heap, nội dung chuỗi của nó **không bao giờ có thể bị thay đổi**. Mọi thao tác cắt, nối (`concat`, `replace`, `substring`) thực chất đều sinh ra một đối tượng `String` hoàn toàn mới.
- **3 Lợi ích sống còn của String Immutability:**
  1. **Bảo mật (Security):** String được dùng làm tham số kết nối Database URL, Username, Password, cổng mạng, tên file. Nếu String có thể bị sửa đổi (mutable), một luồng mã độc có thể âm thầm đổi địa chỉ Database sau khi đã qua bước kiểm tra xác thực.
  2. **An toàn đa luồng (Thread-Safety):** Vì dữ liệu không bao giờ thay đổi, nhiều luồng (threads) có thể đồng thời đọc cùng một String mà không bao giờ cần đồng bộ hóa (synchronization), loại bỏ hoàn toàn nguy cơ tranh chấp Race Condition.
  3. **Tối ưu bộ nhớ với String Constant Pool:** Nhờ bất biến, hàng trăm biến mang cùng giá trị `"ACTIVE"` có thể cùng trỏ về 1 ô nhớ duy nhất trên Heap mà không sợ một biến sửa làm ảnh hưởng tới các biến khác.
  4. **Caching Hashcode:** Mã hash (`hashCode()`) của String chỉ cần tính toán 1 lần duy nhất lúc khởi tạo và lưu cache lại. Điều này giúp String trở thành Key lý tưởng nhất cho `HashMap` với tốc độ tìm kiếm $O(1)$ siêu nhanh.

### 7.2. String Pool là gì? Hoạt động thế nào?
- **String Constant Pool (SCP):** Là một vùng nhớ đặc biệt nằm bên trong bộ nhớ **Heap** của JVM.
- **Cơ chế hoạt động:**
  - Khi ta khai báo bằng chuỗi literal: `String s = "hello";`
  - JVM sẽ kiểm tra trong String Pool xem đã có chuỗi `"hello"` nào tồn tại chưa.
  - Nếu **đã có:** JVM trả về ngay địa chỉ tham chiếu của đối tượng có sẵn trong Pool (không tạo mới).
  - Nếu **chưa có:** JVM tạo mới một đối tượng `"hello"` đặt vào Pool và trả về địa chỉ.

### 7.3. `String a = "abc"` và `String b = new String("abc")` tạo bao nhiêu object?
- **Trường hợp 1:** Nếu chuỗi `"abc"` **chưa hề tồn tại** trong String Pool từ trước:
  - Lệnh `String a = "abc";` $\rightarrow$ Tạo **1 object** nằm trong **String Pool**.
  - Lệnh `String b = new String("abc");` $\rightarrow$ Tạo thêm **1 object** nằm ở **vùng nhớ Heap thông thường** (ngoài Pool).
  - $\rightarrow$ Tổng cộng tạo **2 objects**.
- **Trường hợp 2:** Nếu chuỗi `"abc"` **đã có sẵn** trong String Pool:
  - Lệnh `new String("abc")` chỉ tạo duy nhất **1 object** trên Heap thông thường.

### 7.4. Phân biệt `==` và `.equals()` khi dùng với String
- **Toán tử `==`:** So sánh **địa chỉ ô nhớ** (hai biến có cùng trỏ tới 1 object hay không).
- **Phương thức `.equals()`:** So sánh **nội dung ký tự bên trong chuỗi**.
- *Ví dụ kinh điển:*
  ```java
  String s1 = "Java";
  String s2 = "Java";
  String s3 = new String("Java");

  System.out.println(s1 == s2);      // true (cùng trỏ vào 1 object trong String Pool)
  System.out.println(s1 == s3);      // false (s1 ở trong Pool, s3 là object riêng trên Heap)
  System.out.println(s1.equals(s3)); // true (nội dung đều là "Java")
  ```
  > **Quy tắc bất di bất dịch:** Trong Backend Java, **LUÔN LUÔN dùng `.equals()`** để so sánh chuỗi!

### 7.5. Tại sao không nên dùng `+=` để nối String trong vòng lặp?
- Vì String là bất biến, mỗi lần gọi `str += "a"` trong vòng lặp $N$ lần, JVM phải tạo ra một đối tượng `StringBuilder` tạm, append, rồi gọi `.toString()` tạo ra một đối tượng `String` mới và vứt bỏ đối tượng cũ làm rác.
- **Hậu quả:**
  - Độ phức tạp thời gian: $O(N^2)$ thay vì $O(N)$.
  - Tạo ra hàng ngàn object rác trên Heap, ép Garbage Collector phải chạy liên tục (gây giật lag hệ thống).
  - Với vòng lặp 100.000 lần: Nối chuỗi bằng `+=` mất **vài phút**, trong khi dùng `StringBuilder` chỉ mất **chưa tới 10 mili-giây**.

### 7.6. StringBuilder và StringBuffer khác nhau thế nào? Khi nào dùng cái nào?
| Tiêu chí | `StringBuilder` (Java 5+) | `StringBuffer` (Java 1.0) |
| :--- | :--- | :--- |
| **Tính an toàn đa luồng** | **Không Thread-safe** (các phương thức không có `synchronized`). | **Thread-safe** (hầu hết phương thức đều bọc từ khóa `synchronized`). |
| **Tốc độ thực thi** | **Cực nhanh** (vì không mất chi phí khóa luồng - lock overhead). | Chậm hơn do chi phí đồng bộ luồng. |
| **Ứng dụng thực tế** | Dùng trong **99% trường hợp thực tế** (nối chuỗi trong một hàm, một luồng duy nhất). | Chỉ dùng khi nhiều Thread cùng lúc chỉnh sửa chung một bộ đệm chuỗi (rất hiếm khi gặp). |

### 7.7. Phương thức `intern()` dùng để làm gì?
- Khi gọi `s.intern()`, JVM sẽ kiểm tra xem nội dung của `s` đã có trong String Constant Pool chưa:
  - Nếu đã có: Trả về tham chiếu của đối tượng trong Pool.
  - Nếu chưa có: Đưa `s` vào String Pool và trả về tham chiếu đó.
- *Ví dụ:*
  ```java
  String s1 = new String("hello"); // Nằm trên Heap
  String s2 = s1.intern();          // Ép lấy đối tượng trong Pool
  String s3 = "hello";              // Nằm trong Pool
  System.out.println(s2 == s3);     // true
  ```
- *Ứng dụng:* Dùng khi đọc một lượng cực lớn dữ liệu từ file/database có nhiều chuỗi trùng lặp (ví dụ: tên thành phố, mã quốc gia) để đưa vào Pool giúp tiết kiệm dung lượng RAM.

---
*Thực hành:* Code kiểm chứng `==` vs `.equals()` với String literal và `new String()`, đo thời gian nối 100.000 chuỗi bằng String vs StringBuilder.

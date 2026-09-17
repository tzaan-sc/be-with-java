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

```mermaid
graph LR
    subgraph Stack
        a["a = ref → "]
        b["b = ref → "]
        c["c = ref → "]
    end
    subgraph Heap
        subgraph Pool["String Pool"]
            P1["\"java\""]
        end
        H1["new String(\"java\") tại 0xC3"]
    end
    a --> P1
    b --> P1
    c --> H1
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

## 7. Câu hỏi phỏng vấn thường gặp
1. Tại sao String trong Java là **immutable**? Lợi ích?
2. **String Pool** là gì? Hoạt động thế nào?
3. `String a = "abc"` và `String b = new String("abc")` tạo bao nhiêu object?
4. Phân biệt `==` và `.equals()` khi dùng với String?
5. Tại sao không nên dùng `+=` để nối String trong vòng lặp?
6. StringBuilder và StringBuffer khác nhau thế nào? Khi nào dùng cái nào?
7. Phương thức `intern()` dùng để làm gì?

---
*Thực hành:* Code kiểm chứng `==` vs `.equals()` với String literal và `new String()`, đo thời gian nối 100.000 chuỗi bằng String vs StringBuilder.

# Chapter 01: Biến, Kiểu dữ liệu & Ép kiểu (Variables, Data Types & Casting)

## 1. Biến (Variable) là gì?
- Biến là **ô nhớ** trong RAM dùng để lưu trữ giá trị. Mỗi biến gồm 3 phần:
  - **Kiểu dữ liệu** (Data Type): quyết định kích thước ô nhớ và loại giá trị.
  - **Tên biến** (Identifier): tuân theo quy tắc camelCase.
  - **Giá trị** (Value): giá trị được gán.

```java
int age = 25;           // kiểu int, tên "age", giá trị 25
String name = "Minh";   // kiểu String (tham chiếu), tên "name"
boolean isActive = true; // kiểu boolean
```

## 2. Hai nhóm kiểu dữ liệu

### 2.1 Kiểu nguyên thuỷ (Primitive Types) – 8 kiểu
Lưu **trực tiếp giá trị** trên **Stack**, kích thước cố định.

| Kiểu | Kích thước | Phạm vi | Giá trị mặc định | Ví dụ |
|------|-----------|---------|-------------------|-------|
| `byte` | 1 byte | −128 → 127 | 0 | `byte b = 100;` |
| `short` | 2 bytes | −32 768 → 32 767 | 0 | `short s = 30000;` |
| `int` | 4 bytes | −2³¹ → 2³¹ − 1 (~2.1 tỷ) | 0 | `int count = 1000;` |
| `long` | 8 bytes | −2⁶³ → 2⁶³ − 1 | 0L | `long id = 99999999L;` |
| `float` | 4 bytes | ≈ ±3.4 × 10³⁸ (7 chữ số thập phân) | 0.0f | `float pi = 3.14f;` |
| `double` | 8 bytes | ≈ ±1.7 × 10³⁰⁸ (15 chữ số thập phân) | 0.0d | `double price = 19.99;` |
| `char` | 2 bytes | Ký tự Unicode (0 → 65 535) | '\u0000' | `char grade = 'A';` |
| `boolean` | 1 bit* | `true` hoặc `false` | false | `boolean ok = true;` |

> *Lưu ý: JVM thực tế cấp ít nhất 1 byte cho boolean.

### 2.2 Kiểu tham chiếu (Reference Types)
Lưu **địa chỉ** (reference) trỏ tới **đối tượng trên Heap**.

- `String`, `Integer`, `Double`, `Boolean` (Wrapper Classes)
- Mảng (`int[]`, `String[]`), Class tự tạo (`User`, `Product`)
- Giá trị mặc định: `null`

```java
String greeting = "Hello";   // greeting chứa ĐỊA CHỈ trỏ tới "Hello" trên Heap
int[] numbers = {1, 2, 3};   // numbers chứa địa chỉ trỏ tới mảng trên Heap
User user = new User();      // user chứa địa chỉ trỏ tới object User trên Heap
```

### 2.3 So sánh nhanh

```mermaid
graph LR
    subgraph Stack
        age["age = 25 (int)"]
        ref["greeting = 0x7A3F (địa chỉ)"]
    end
    subgraph Heap
        obj["\"Hello\" (String object)"]
    end
    ref -->|trỏ tới| obj
```

| Tiêu chí | Primitive | Reference |
|----------|-----------|-----------|
| Lưu ở đâu? | Stack (giá trị trực tiếp) | Stack (địa chỉ) + Heap (đối tượng) |
| Giá trị mặc định? | 0, false, '\u0000' | `null` |
| So sánh bằng `==`? | So sánh **giá trị** | So sánh **địa chỉ bộ nhớ** (không phải nội dung!) |
| Kích thước? | Cố định (1‑8 bytes) | Tuỳ thuộc đối tượng |

## 3. Wrapper Classes & Autoboxing
- Mỗi kiểu primitive có 1 Wrapper Class tương ứng: `int` → `Integer`, `double` → `Double`, `boolean` → `Boolean`…
- **Autoboxing**: tự động chuyển primitive → Wrapper.
- **Unboxing**: tự động chuyển Wrapper → primitive.

```java
int a = 10;
Integer b = a;         // Autoboxing: int → Integer
int c = b;             // Unboxing: Integer → int

// Cẩn thận: Unboxing null gây NullPointerException!
Integer x = null;
int y = x;             // ❌ NullPointerException tại runtime!
```

## 4. Ép kiểu (Type Casting)

### 4.1 Ép kiểu ngầm định (Widening / Implicit Casting)
Chuyển từ kiểu **nhỏ → lớn**, Java tự động thực hiện, **không mất dữ liệu**.

```
byte → short → int → long → float → double
```

```java
int num = 100;
long bigNum = num;      // int → long (tự động)
double d = bigNum;      // long → double (tự động)
System.out.println(d);  // 100.0
```

### 4.2 Ép kiểu tường minh (Narrowing / Explicit Casting)
Chuyển từ kiểu **lớn → nhỏ**, **có thể mất dữ liệu** (tràn số / mất phần thập phân).

```java
double pi = 3.14159;
int intPi = (int) pi;      // Ép tường minh: mất phần thập phân → intPi = 3
System.out.println(intPi);  // 3

long bigValue = 130;
byte smallValue = (byte) bigValue;  // ⚠️ Tràn số! 130 > 127 → smallValue = -126
System.out.println(smallValue);     // -126 (overflow!)
```

### 4.3 Lỗi phổ biến khi chia số nguyên
```java
int a = 5, b = 2;
System.out.println(a / b);           // 2 (mất phần thập phân vì int / int = int)
System.out.println((double) a / b);  // 2.5 (ép 1 vế sang double trước khi chia)
```

## 5. Toán tử (Operators)

### 5.1 Toán tử số học
| Toán tử | Ý nghĩa | Ví dụ |
|---------|---------|-------|
| `+` | Cộng | `5 + 3` → 8 |
| `-` | Trừ | `5 - 3` → 2 |
| `*` | Nhân | `5 * 3` → 15 |
| `/` | Chia | `5 / 2` → 2 (int), `5.0 / 2` → 2.5 |
| `%` | Chia lấy dư (Modulo) | `5 % 2` → 1 |

### 5.2 Toán tử so sánh & logic
```java
// So sánh: ==, !=, >, <, >=, <=
// Logic:   && (AND), || (OR), ! (NOT)
if (age >= 18 && isActive) {
    System.out.println("Đủ điều kiện");
}
```

### 5.3 Toán tử tăng/giảm
```java
int i = 5;
System.out.println(i++);  // In 5 rồi tăng i lên 6 (post-increment)
System.out.println(++i);  // Tăng i lên 7 rồi in 7 (pre-increment)
```

### 5.4 Toán tử gán mở rộng
```java
int x = 10;
x += 5;   // x = x + 5 → 15
x -= 3;   // x = x - 3 → 12
x *= 2;   // x = x * 2 → 24
x /= 4;   // x = x / 4 → 6
x %= 4;   // x = x % 4 → 2
```

## 6. Hằng số (Constants) với `final`
```java
final double TAX_RATE = 0.1;   // Không thể thay đổi giá trị sau khi gán
// TAX_RATE = 0.2;             // ❌ Compilation Error
```

- Quy ước đặt tên hằng số: **UPPER_SNAKE_CASE**

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Primitive và Reference type khác nhau thế nào? Lưu ở đâu trong bộ nhớ?
- **Primitive (Nguyên thuỷ - 8 kiểu):**
  - Lưu **trực tiếp giá trị nhị phân** trong vùng nhớ **Stack** (hoặc nằm gọn trong object trên Heap nếu là biến instance của class).
  - Không có phương thức đi kèm, kích thước cố định (1 - 8 bytes), tốc độ truy xuất cực nhanh.
- **Reference (Tham chiếu):**
  - Biến chỉ lưu **địa chỉ con trỏ (Memory Address)** trên vùng nhớ **Stack**.
  - Đối tượng thực sự (Object Data) luôn được cấp phát động trên vùng nhớ **Heap**.
  - Có các phương thức (`equals()`, `hashCode()`, `toString()`), giá trị mặc định là `null`.

### 7.2. Toán tử `==` hoạt động khác nhau thế nào khi dùng với `int` và `Integer`?
- **Với `int` (Primitive):** `==` so sánh **giá trị số học**.
  ```java
  int a = 10, b = 10;
  System.out.println(a == b); // true (vì cùng mang giá trị 10)
  ```
- **Với `Integer` (Reference Object):** `==` so sánh **địa chỉ ô nhớ** (hai biến có trỏ cùng một object trên Heap hay không), chứ KHÔNG so sánh giá trị nội dung (để so sánh giá trị phải dùng `.equals()`).
  - *Cạm bẫy Integer Cache (-128 đến 127):*
    ```java
    Integer x = 100, y = 100;
    System.out.println(x == y); // true (do nằm trong Integer Cache từ -128 đến 127, JVM tái sử dụng object)

    Integer a = 200, b = 200;
    System.out.println(a == b); // false (vượt ngoài cache, tạo 2 object độc lập trên Heap!)
    System.out.println(a.equals(b)); // true (luôn dùng .equals() để so sánh đối tượng)
    ```

### 7.3. Giải thích Autoboxing / Unboxing và khi nào có thể gây NullPointerException?
- **Autoboxing:** Trình biên dịch tự động chuyển kiểu nguyên thuỷ sang Wrapper class (vd: `int` $\rightarrow$ `Integer.valueOf()`).
- **Unboxing:** Trình biên dịch tự động gọi `.intValue()` để lấy giá trị nguyên thuỷ từ Wrapper class.
- **Nguy cơ gây `NullPointerException` (NPE):**
  Xảy ra khi ta thực hiện phép toán hoặc gán một Wrapper object đang mang giá trị `null` về kiểu nguyên thuỷ:
  ```java
  Integer count = null;
  int total = count; // ❌ Ném ra NullPointerException tại runtime vì JVM âm thầm gọi count.intValue()
  ```

### 7.4. Kết quả của `5 / 2` khác `5.0 / 2` như thế nào? Tại sao?
- `5 / 2` $\rightarrow$ Kết quả là `2` (kiểu `int`). Vì cả `5` và `2` đều là số nguyên (`int`), phép chia nguyên trong Java sẽ cắt bỏ toàn bộ phần thập phân (không làm tròn).
- `5.0 / 2` $\rightarrow$ Kết quả là `2.5` (kiểu `double`). Khi một trong hai toán hạng là kiểu số thực (`double`), Java sẽ tự động ép toán hạng còn lại (`2`) thành `2.0` (Widening Casting) rồi thực hiện phép chia số thực.

### 7.5. Khi ép `(byte) 130`, kết quả là bao nhiêu? Giải thích cơ chế overflow
- **Kết quả:** `-126`
- **Giải thích cơ chế tràn số (Overflow):**
  - Kiểu `byte` trong Java có kích thước 8-bit có dấu (Signed 2's Complement), phạm vi từ `-128` đến `127`.
  - Số nguyên `130` dưới dạng nhị phân 32-bit: `00000000 00000000 00000000 10000010`.
  - Khi ép kiểu tường minh sang `(byte)`, Java cắt lấy đúng **8 bit cuối**: `10000010`.
  - Bit đầu tiên là `1` đại diện cho số âm.
  - Giá trị bù 2 của `10000010` là: $-(2^7) + 2^1 = -128 + 2 = -126$.

---
*Thực hành:* Tạo class `Main`, khai báo đầy đủ 8 kiểu primitive, thử ép kiểu ngầm định & tường minh, và chạy các ví dụ chia số nguyên.

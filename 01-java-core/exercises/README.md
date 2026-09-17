# 🛠 Bài Tập Thực Hành – Phase 1: Java Core

> Bài tập theo lộ trình **20‑30 phút/ngày** (Ngày 09 – Ngày 22).
> Mỗi bài gắn với nội dung lý thuyết tương ứng. Tự gõ code, **KHÔNG copy‑paste**.
> Ký hiệu: `[ ]` Chưa làm · `[x]` Đã hoàn thành

---

## Bài tập Ngày 09‑10: Biến, Kiểu dữ liệu & Ép kiểu
*(Tương ứng Chapter 01)*

### Bài 1.1 – Khai báo 8 kiểu Primitive *(~10 phút)*
[ ] Tạo class `DataTypesDemo`, khai báo đầy đủ 8 kiểu primitive và in ra giá trị:

```java
public class DataTypesDemo {
    public static void main(String[] args) {
        byte myByte = ____;
        short myShort = ____;
        int myInt = ____;
        long myLong = ____L;
        float myFloat = ____f;
        double myDouble = ____;
        char myChar = ____;
        boolean myBoolean = ____;

        // In ra tất cả
        System.out.println("byte: " + myByte);
        // ... tiếp tục cho các biến còn lại
    }
}
```

### Bài 1.2 – Thí nghiệm ép kiểu *(~10 phút)*
[ ] Viết code kiểm chứng và ghi kết quả:

```java
public class CastingDemo {
    public static void main(String[] args) {
        // Widening (tự động)
        int a = 100;
        long b = a;          // Kết quả b = ____
        double c = b;        // Kết quả c = ____

        // Narrowing (tường minh)
        double pi = 3.14159;
        int intPi = (int) pi;           // Kết quả intPi = ____

        long bigValue = 130;
        byte smallValue = (byte) bigValue;  // Kết quả smallValue = ____ (tại sao?)

        // Chia số nguyên
        int x = 5, y = 2;
        System.out.println(x / y);              // Kết quả = ____
        System.out.println((double) x / y);     // Kết quả = ____

        // Autoboxing & Unboxing
        int num = 42;
        Integer wrapped = num;       // Autoboxing
        int unwrapped = wrapped;     // Unboxing
        System.out.println(wrapped == unwrapped);  // Kết quả = ____
    }
}
```

### Bài 1.3 – Câu hỏi tự trả lời *(~5 phút)*
[ ] Ghi đáp án:

```
1. Primitive type lưu ở đâu trong bộ nhớ?
   → ___________________________________________

2. Reference type lưu ở đâu?
   → ___________________________________________

3. Khi viết `Integer x = null; int y = x;` thì điều gì xảy ra?
   → ___________________________________________
```

---

## Bài tập Ngày 11‑13: Cấu trúc điều khiển, Vòng lặp & Mảng
*(Tương ứng Chapter 02)*

### Bài 2.1 – Phân loại học lực *(~10 phút)*
[ ] Viết method `classifyGrade(int score)` trả về String:

```
score >= 90      → "Xuất sắc"
score >= 80      → "Giỏi"
score >= 70      → "Khá"
score >= 50      → "Trung bình"
score < 50       → "Yếu"
```

```java
public static String classifyGrade(int score) {
    // Viết code ở đây dùng if-else
}

// Test:
System.out.println(classifyGrade(95));  // "Xuất sắc"
System.out.println(classifyGrade(42));  // "Yếu"
```

### Bài 2.2 – In ngày trong tuần bằng switch *(~10 phút)*
[ ] Viết method `getDayName(int day)` dùng **Switch Expression** (cú pháp `→`):

```java
public static String getDayName(int day) {
    return switch (day) {
        // Viết code ở đây
        // 1 → "Chủ nhật", 2 → "Thứ Hai", ..., 7 → "Thứ Bảy"
        // default → "Không hợp lệ"
    };
}

// Test:
System.out.println(getDayName(2));  // "Thứ Hai"
System.out.println(getDayName(8));  // "Không hợp lệ"
```

### Bài 2.3 – Tính tổng số chẵn trong mảng *(~10 phút)*
[ ] Viết code tính tổng **các số chẵn** trong mảng dùng `for-each`:

```java
int[] numbers = {3, 8, 15, 22, 7, 40, 11, 6};

int sum = 0;
for (int num : numbers) {
    // Kiểm tra số chẵn và cộng vào sum
}
System.out.println("Tổng số chẵn: " + sum);  // Kết quả đúng: 76
```

### Bài 2.4 – Tìm Max và Min trong mảng *(~10 phút)*
[ ] Viết method `findMax(int[] arr)` và `findMin(int[] arr)`:

```java
public static int findMax(int[] arr) {
    // Viết code ở đây
}

public static int findMin(int[] arr) {
    // Viết code ở đây
}

// Test:
int[] data = {23, 7, 45, 12, 89, 3, 56};
System.out.println("Max: " + findMax(data));  // 89
System.out.println("Min: " + findMin(data));  // 3
```

### Bài 2.5 – Đảo ngược mảng *(~10 phút)*
[ ] Viết method `reverseArray(int[] arr)` đảo ngược mảng **tại chỗ** (không tạo mảng mới):

```java
public static void reverseArray(int[] arr) {
    // Gợi ý: dùng 2 con trỏ đầu (left) và cuối (right), swap phần tử
}

// Test:
int[] arr = {1, 2, 3, 4, 5};
reverseArray(arr);
// Kết quả: arr = {5, 4, 3, 2, 1}
```

### Bài 2.6 – Kiểm tra số nguyên tố *(~10 phút)*
[ ] Viết method `isPrime(int n)` trả về `true` nếu n là số nguyên tố:

```java
public static boolean isPrime(int n) {
    // Gợi ý: kiểm tra n <= 1 (false), duyệt từ 2 đến sqrt(n)
}

// Test:
System.out.println(isPrime(7));   // true
System.out.println(isPrime(12));  // false
System.out.println(isPrime(1));   // false
System.out.println(isPrime(2));   // true
```

---

## Bài tập Ngày 14‑16: Stack vs Heap, Pass‑by‑Value & Garbage Collection
*(Tương ứng Chapter 03)*

### Bài 3.1 – Vẽ sơ đồ bộ nhớ *(~10 phút)*
[ ] Cho đoạn code sau, vẽ **sơ đồ Stack & Heap** tại dòng đánh dấu `// ← VẼ TẠI ĐÂY`:

```java
public static void main(String[] args) {
    int x = 10;
    int y = 20;
    String name = "Java";
    int[] scores = {90, 85, 70};
    User user = new User("An", 25);
    // ← VẼ SƠ ĐỒ BỘ NHỚ TẠI ĐÂY
}
```

Ghi ra:
```
STACK:                          HEAP:
┌─────────────────┐            ┌─────────────────────┐
│ x = ____        │            │ __________________  │
│ y = ____        │            │ __________________  │
│ name = ____     │ ──→        │ __________________  │
│ scores = ____   │ ──→        │ __________________  │
│ user = ____     │ ──→        │ __________________  │
└─────────────────┘            └─────────────────────┘
```

### Bài 3.2 – Chứng minh Pass‑by‑Value *(~15 phút)*
[ ] Viết code **chạy thật** và ghi kết quả:

```java
public class PassByValueDemo {
    public static void main(String[] args) {
        // Test 1: Primitive
        int number = 100;
        changeNumber(number);
        System.out.println("Sau changeNumber: " + number);  // Kết quả = ____

        // Test 2: Object – thay đổi thuộc tính
        User user = new User("An");
        changeName(user);
        System.out.println("Sau changeName: " + user.getName());  // Kết quả = ____

        // Test 3: Object – gán lại reference
        replaceUser(user);
        System.out.println("Sau replaceUser: " + user.getName()); // Kết quả = ____
    }

    static void changeNumber(int n) { n = 999; }
    static void changeName(User u) { u.setName("Bình"); }
    static void replaceUser(User u) { u = new User("Cường"); }
}

// class User đơn giản:
class User {
    private String name;
    public User(String name) { this.name = name; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

[ ] Giải thích bằng lời:
```
Tại sao Test 1 không đổi?
→ ___________________________________________

Tại sao Test 2 đổi được?
→ ___________________________________________

Tại sao Test 3 không đổi?
→ ___________________________________________
```

### Bài 3.3 – Câu hỏi Garbage Collection *(~5 phút)*
[ ] Cho đoạn code, đánh dấu object nào trở thành "rác" (eligible for GC) tại mỗi dòng:

```java
User a = new User("An");     // Object 1 tạo
User b = new User("Bình");   // Object 2 tạo
User c = a;                  // c trỏ tới Object 1
a = b;                       // → Object nào thành rác? ____
b = null;                    // → Object nào thành rác? ____
c = null;                    // → Object nào thành rác? ____
```

---

## Bài tập Ngày 17‑19: String, String Pool & StringBuilder
*(Tương ứng Chapter 04)*

### Bài 4.1 – Kiểm chứng String Immutability *(~10 phút)*
[ ] Chạy code và ghi kết quả:

```java
String s = "Hello";
s.concat(" World");
System.out.println(s);                    // Kết quả = ____

s = s.concat(" World");
System.out.println(s);                    // Kết quả = ____

String a = s.toUpperCase();
System.out.println("s = " + s);          // Kết quả s = ____
System.out.println("a = " + a);          // Kết quả a = ____
```

### Bài 4.2 – Kiểm chứng String Pool & `==` vs `.equals()` *(~10 phút)*
[ ] Chạy code, **dự đoán TRƯỚC** rồi mới chạy kiểm tra:

```java
String a = "java";
String b = "java";
String c = new String("java");
String d = c.intern();

System.out.println(a == b);         // Dự đoán: ____ | Thực tế: ____
System.out.println(a == c);         // Dự đoán: ____ | Thực tế: ____
System.out.println(a.equals(c));    // Dự đoán: ____ | Thực tế: ____
System.out.println(a == d);         // Dự đoán: ____ | Thực tế: ____
System.out.println(c == d);         // Dự đoán: ____ | Thực tế: ____
```

### Bài 4.3 – Đo hiệu năng String vs StringBuilder *(~10 phút)*
[ ] Viết code đo thời gian nối 50.000 ký tự:

```java
// String concatenation
long start = System.currentTimeMillis();
String s = "";
for (int i = 0; i < 50000; i++) {
    s += "a";
}
long stringTime = System.currentTimeMillis() - start;

// StringBuilder
start = System.currentTimeMillis();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 50000; i++) {
    sb.append("a");
}
long sbTime = System.currentTimeMillis() - start;

System.out.println("String:        " + stringTime + "ms");    // Kết quả: ____ms
System.out.println("StringBuilder: " + sbTime + "ms");         // Kết quả: ____ms
System.out.println("Nhanh hơn:     " + (stringTime / Math.max(sbTime, 1)) + " lần");
```

### Bài 4.4 – Bài toán xử lý chuỗi *(~10 phút)*
[ ] Viết method `countVowels(String str)` đếm số nguyên âm (a, e, i, o, u) trong chuỗi (không phân biệt hoa/thường):

```java
public static int countVowels(String str) {
    // Gợi ý: chuyển thành chữ thường, duyệt từng ký tự bằng charAt()
}

// Test:
System.out.println(countVowels("Hello World"));     // 3
System.out.println(countVowels("JAVA Backend"));    // 4
System.out.println(countVowels("rhythm"));           // 0
```

### Bài 4.5 – Đảo ngược chuỗi *(~5 phút)*
[ ] Viết method `reverseString(String str)` bằng 2 cách:
- **Cách 1:** Dùng `StringBuilder.reverse()`
- **Cách 2:** Dùng vòng lặp duyệt ngược

```java
// Cách 1:
public static String reverseString1(String str) {
    // Viết code
}

// Cách 2:
public static String reverseString2(String str) {
    // Viết code
}

// Test:
System.out.println(reverseString1("Hello"));  // "olleH"
System.out.println(reverseString2("Java"));   // "avaJ"
```

---

## Bài tập Ngày 20‑21: Exception Handling & Custom Exception
*(Tương ứng Chapter 05)*

### Bài 5.1 – Bắt Exception căn bản *(~10 phút)*
[ ] Viết code bắt 2 loại Exception riêng biệt:

```java
public class ExceptionDemo {
    public static void main(String[] args) {
        // Bài a: Bắt ArithmeticException
        try {
            int result = 10 / 0;
        } catch (____) {
            System.out.println("Lỗi chia cho 0: " + e.getMessage());
        }

        // Bài b: Bắt ArrayIndexOutOfBoundsException
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]);
        } catch (____) {
            System.out.println("Lỗi truy cập index: " + e.getMessage());
        }

        // Bài c: Khối finally
        try {
            String s = null;
            s.length();
        } catch (NullPointerException e) {
            System.out.println("Lỗi null");
        } finally {
            System.out.println("Finally luôn chạy");
        }
    }
}
```

### Bài 5.2 – Tạo Custom Exception *(~10 phút)*
[ ] Tạo class `InvalidAgeException` kế thừa `RuntimeException`:

```java
public class InvalidAgeException extends RuntimeException {
    // Viết constructor nhận message
}
```

[ ] Viết method `validateAge(int age)` quăng `InvalidAgeException` nếu tuổi < 0 hoặc > 150:

```java
public static void validateAge(int age) {
    // Kiểm tra và throw InvalidAgeException nếu không hợp lệ
}

// Test:
try {
    validateAge(200);
} catch (InvalidAgeException e) {
    System.out.println(e.getMessage());  // "Tuổi không hợp lệ: 200"
}
```

### Bài 5.3 – Phân loại Exception *(~5 phút)*
[ ] Điền vào bảng: Checked hay Unchecked?

| Exception | Checked / Unchecked |
|-----------|-------------------|
| `NullPointerException` | *(điền)* |
| `IOException` | *(điền)* |
| `ArithmeticException` | *(điền)* |
| `SQLException` | *(điền)* |
| `ArrayIndexOutOfBoundsException` | *(điền)* |
| `FileNotFoundException` | *(điền)* |
| `IllegalArgumentException` | *(điền)* |
| `ClassNotFoundException` | *(điền)* |

### Bài 5.4 – Try-with-Resources *(~10 phút)*
[ ] Viết code đọc nội dung file bằng `try-with-resources`:

```java
import java.io.*;

public class FileReaderDemo {
    public static void main(String[] args) {
        // Tạo file test trước: tạo file "test.txt" với nội dung bất kỳ

        try (BufferedReader reader = new BufferedReader(new FileReader("test.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("File không tồn tại: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
        // reader tự động đóng ở đây
    }
}
```

---

## Bài tập Ngày 22: Ôn tập tổng hợp Phase 1

### Bài 6.1 – Quiz tổng hợp *(~15 phút)*
[ ] Trả lời 10 câu hỏi:

```
1. Có bao nhiêu kiểu Primitive trong Java? Kể tên.
   → ___________________________________________

2. Kết quả của `(byte) 130` là bao nhiêu? Tại sao?
   → ___________________________________________

3. `for-each` có thay đổi được phần tử mảng gốc không?
   → ___________________________________________

4. Stack lưu gì? Heap lưu gì?
   → ___________________________________________

5. Java là Pass-by-Value hay Pass-by-Reference?
   → ___________________________________________

6. String a = "hello"; String b = new String("hello");
   Tạo bao nhiêu object? Ở đâu?
   → ___________________________________________

7. Tại sao không nên dùng += nối String trong vòng lặp?
   → ___________________________________________

8. Checked Exception và Unchecked Exception khác nhau thế nào?
   → ___________________________________________

9. try-with-resources tự động đóng resource khi nào?
   Resource cần implement interface gì?
   → ___________________________________________

10. OutOfMemoryError và StackOverflowError khác nhau thế nào?
    → ___________________________________________
```

---

## 📋 Bảng đáp án tham khảo

<details>
<summary><b>👉 Click để xem đáp án (chỉ xem SAU KHI đã tự làm)</b></summary>

### Bài 1.3
1. Stack (giá trị trực tiếp)
2. Stack (reference/địa chỉ) + Heap (object thật)
3. `NullPointerException` do Unboxing null

### Bài 3.3 – GC
- `a = b;` → Chưa có rác (Object 1 vẫn có c trỏ tới)
- `b = null;` → Chưa có rác (Object 2 vẫn có a trỏ tới)
- `c = null;` → Object 1 thành rác (không ai trỏ tới)

### Bài 4.2 – String Pool
```
a == b       → true  (cùng Pool)
a == c       → false (Pool vs Heap)
a.equals(c)  → true  (nội dung giống)
a == d       → true  (intern() trả về Pool)
c == d       → false (Heap vs Pool)
```

### Bài 5.3 – Phân loại Exception
| Exception | Loại |
|-----------|------|
| NullPointerException | Unchecked |
| IOException | Checked |
| ArithmeticException | Unchecked |
| SQLException | Checked |
| ArrayIndexOutOfBoundsException | Unchecked |
| FileNotFoundException | Checked |
| IllegalArgumentException | Unchecked |
| ClassNotFoundException | Checked |

### Bài 6.1 – Quiz
1. 8 kiểu: byte, short, int, long, float, double, char, boolean
2. -126 (overflow: 130 − 256 = −126, vì byte chỉ chứa −128 → 127)
3. Không, for-each tạo bản copy giá trị (với primitive), không thay đổi mảng gốc
4. Stack: biến cục bộ, reference, call stack. Heap: object (new), mảng, String
5. Pass-by-Value (luôn copy giá trị, kể cả reference)
6. 2 objects: 1 trong String Pool ("hello"), 1 trên Heap (new String)
7. Mỗi lần += tạo String mới → O(n²) bộ nhớ, rất chậm
8. Checked bắt buộc xử lý (compile-time), Unchecked không bắt buộc (runtime)
9. Khi ra khỏi khối try. Resource cần implement AutoCloseable
10. StackOverflow: đệ quy quá sâu (Stack đầy). OutOfMemory: Heap đầy (tạo quá nhiều object)

</details>

---
*Hoàn thành xong = sẵn sàng bước vào Phase 2: OOP & Collections! 🚀*

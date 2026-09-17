# Chapter 02: Cấu trúc Điều khiển & Vòng lặp (Control Flow)

## 1. Cấu trúc rẽ nhánh

### 1.1 if – else if – else
```java
int score = 75;

if (score >= 90) {
    System.out.println("Xuất sắc");
} else if (score >= 70) {
    System.out.println("Khá");       // ← In ra dòng này
} else if (score >= 50) {
    System.out.println("Trung bình");
} else {
    System.out.println("Yếu");
}
```

- Sử dụng khi có **nhiều điều kiện** cần kiểm tra tuần tự.
- Điều kiện nào đúng **trước** sẽ thực thi, các nhánh sau **bị bỏ qua**.

### 1.2 Toán tử 3 ngôi (Ternary Operator)
```java
// Cú pháp: điều_kiện ? giá_trị_đúng : giá_trị_sai
String result = (score >= 50) ? "Đậu" : "Rớt";
System.out.println(result);  // "Đậu"
```

- Thay thế `if-else` đơn giản trong 1 dòng. Không nên lồng nhiều tầng (khó đọc).

### 1.3 switch – case (Truyền thống)
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Chủ nhật");
        break;
    case 2:
        System.out.println("Thứ Hai");
        break;
    case 3:
        System.out.println("Thứ Ba");   // ← In ra
        break;
    default:
        System.out.println("Ngày khác");
        break;
}
```

- **Phải có `break`** sau mỗi case, nếu không sẽ bị **fall-through** (chạy xuống case tiếp theo).
- `default` xử lý trường hợp không khớp case nào.
- Hỗ trợ: `byte`, `short`, `int`, `char`, `String`, `enum` (không hỗ trợ `long`, `float`, `double`).

### 1.4 Switch Expression (Java 14+) – Cú pháp mới
```java
String dayName = switch (day) {
    case 1 -> "Chủ nhật";
    case 2 -> "Thứ Hai";
    case 3 -> "Thứ Ba";
    case 4 -> "Thứ Tư";
    case 5 -> "Thứ Năm";
    case 6 -> "Thứ Sáu";
    case 7 -> "Thứ Bảy";
    default -> "Không hợp lệ";
};
System.out.println(dayName);  // "Thứ Ba"
```

- **Không cần `break`**, mỗi case dùng `->` (arrow syntax).
- Có thể **trả về giá trị** (expression), gán vào biến.
- Gom nhiều case: `case 2, 3, 4, 5, 6 -> "Ngày trong tuần";`

### 1.5 Khi nào dùng if-else, khi nào dùng switch?
| Tình huống | Nên dùng |
|-----------|---------|
| Kiểm tra **phạm vi** (ví dụ: score >= 90) | `if-else` |
| So sánh **giá trị cố định** (day == 1, day == 2...) | `switch-case` |
| Nhiều điều kiện **phức tạp** kết hợp && / \|\| | `if-else` |
| Enum hoặc String có **số lượng giới hạn** | `switch-case` |

---

## 2. Vòng lặp (Loops)

### 2.1 Vòng lặp `for`
Dùng khi **biết trước số lần lặp**.

```java
// In các số từ 1 đến 5
for (int i = 1; i <= 5; i++) {
    System.out.print(i + " ");  // 1 2 3 4 5
}
```

Cấu trúc: `for (khởi_tạo; điều_kiện; cập_nhật)`
1. **Khởi tạo** (`int i = 1`): chạy 1 lần duy nhất.
2. **Điều kiện** (`i <= 5`): kiểm tra trước mỗi vòng, nếu `false` → dừng.
3. **Cập nhật** (`i++`): chạy sau mỗi vòng.

### 2.2 Vòng lặp `while`
Dùng khi **chưa biết trước số lần lặp**, kiểm tra điều kiện **trước** khi chạy.

```java
int count = 1;
while (count <= 5) {
    System.out.print(count + " ");  // 1 2 3 4 5
    count++;
}
```

- ⚠️ Nếu quên `count++` → **vòng lặp vô hạn** (infinite loop).

### 2.3 Vòng lặp `do-while`
Chạy **ít nhất 1 lần**, kiểm tra điều kiện **sau** khi chạy.

```java
int num = 10;
do {
    System.out.println("Chạy ít nhất 1 lần, num = " + num);
    num++;
} while (num < 5);  // Điều kiện sai ngay → nhưng vẫn chạy 1 lần
```

- Phù hợp cho: nhập liệu từ người dùng (nhập → kiểm tra → nhập lại nếu sai).

### 2.4 Vòng lặp `for-each` (Enhanced for)
Dùng để duyệt **mảng** hoặc **Collection** mà không cần index.

```java
int[] scores = {90, 85, 72, 68, 95};
for (int score : scores) {
    System.out.print(score + " ");  // 90 85 72 68 95
}
```

- **Không thể** thay đổi phần tử mảng gốc bên trong for-each.
- **Không có** biến index (`i`), nếu cần index → dùng `for` truyền thống.

### 2.5 So sánh các loại vòng lặp

| Loại | Khi nào dùng | Biết trước số lần? | Kiểm tra ĐK |
|------|-------------|-------------------|-------------|
| `for` | Lặp với counter cụ thể | ✅ | Trước |
| `while` | Lặp tới khi điều kiện sai | ❌ | Trước |
| `do-while` | Chạy ít nhất 1 lần | ❌ | Sau |
| `for-each` | Duyệt mảng/collection | ✅ | — |

---

## 3. Lệnh điều khiển luồng lặp

### 3.1 `break` – Thoát vòng lặp ngay lập tức
```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) break;              // Dừng khi i = 5
    System.out.print(i + " ");      // 1 2 3 4
}
```

### 3.2 `continue` – Bỏ qua lần lặp hiện tại, chạy lần tiếp
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;           // Bỏ qua khi i = 3
    System.out.print(i + " ");      // 1 2 4 5
}
```

### 3.3 Labeled break/continue (ít dùng)
```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) break outer;    // Thoát cả 2 vòng lặp
        System.out.println(i + "," + j);  // Chỉ in: 0,0
    }
}
```

---

## 4. Mảng 1 chiều (Array) căn bản

### 4.1 Khai báo & Khởi tạo
```java
// Cách 1: Khai báo kích thước, giá trị mặc định (0 cho int)
int[] numbers = new int[5];       // [0, 0, 0, 0, 0]

// Cách 2: Khai báo kèm giá trị
int[] scores = {90, 85, 72, 68};  // Kích thước = 4

// Cách 3: Khai báo kiểu cũ (ít dùng)
int ages[] = new int[3];
```

### 4.2 Truy xuất & Gán giá trị
```java
scores[0] = 100;                  // Gán giá trị index 0
System.out.println(scores[0]);    // 100
System.out.println(scores.length);// 4 (thuộc tính length, KHÔNG phải method)
// scores[4] → ❌ ArrayIndexOutOfBoundsException (index chạy từ 0 → length-1)
```

### 4.3 Duyệt mảng
```java
// Dùng for truyền thống (có index)
for (int i = 0; i < scores.length; i++) {
    System.out.println("Index " + i + ": " + scores[i]);
}

// Dùng for-each (không có index)
for (int s : scores) {
    System.out.println(s);
}
```

### 4.4 Lưu ý quan trọng
- Kích thước mảng **cố định** sau khi khởi tạo, không thể thêm/xóa phần tử.
- Nếu cần co giãn → dùng `ArrayList` (sẽ học ở Phase 2).
- Mảng là **reference type**, truyền mảng vào hàm → hàm có thể **thay đổi** phần tử gốc.

## 5. Câu hỏi phỏng vấn thường gặp
1. Sự khác nhau giữa `if-else` và `switch-case`? Khi nào nên dùng cái nào?
2. Fall-through trong switch là gì? Có thể gây lỗi gì?
3. `for` và `while` khác nhau thế nào? `do-while` khác `while` chỗ nào?
4. Khi nào dùng `break`? Khi nào dùng `continue`?
5. Tại sao kích thước mảng trong Java cố định? Khi cần thêm phần tử thì dùng gì?
6. `for-each` có thể thay đổi giá trị phần tử mảng gốc không? Tại sao?

---
*Thực hành:* Viết hàm phân loại học lực (if-else), in ngày trong tuần (switch), tính tổng số chẵn trong mảng (for-each), tìm Max/Min trong mảng (for).

# 🛠 Bài Tập Thực Hành – Phase 2: OOP & Collections

> Lộ trình Ngày 23 – Ngày 42 (20‑30 phút/ngày). Tự gõ code, KHÔNG copy‑paste.

---

## Bài tập Ngày 23‑26: OOP 4 trụ cột *(Chapter 01)*

### Bài 1.1 – Encapsulation: BankAccount *(~15p)*
[ ] Tạo class `BankAccount` với: `private` fields (`accountNumber`, `balance`), Constructor, Getter, method `deposit()` và `withdraw()` có validate (không cho rút quá số dư, không cho nạp số âm).

### Bài 1.2 – Inheritance & Overriding *(~15p)*
[ ] Tạo `Employee`(name, salary) → `Manager`(teamSize) kế thừa. Override method `calculateBonus()`: Employee thưởng 10%, Manager thưởng 20% + 500k/người.

### Bài 1.3 – Abstract Class: Shape *(~10p)*
[ ] Tạo `abstract class Shape` có abstract method `calculateArea()`. Tạo `Circle`(radius) và `Rectangle`(width, height) kế thừa và triển khai.

---

## Bài tập Ngày 27‑28: Interface *(Chapter 02)*

### Bài 2.1 – Payment Interface *(~15p)*
[ ] Tạo `interface PaymentService` có `void pay(double amount)` và `default String getStatus()`. Tạo `VnPayService` và `MomoService` implements. Viết code gọi `pay()` qua biến kiểu `PaymentService` (Polymorphism).

---

## Bài tập Ngày 29‑30: SOLID *(Chapter 03)*

### Bài 3.1 – Refactor SRP *(~15p)*
[ ] Cho class dưới đây vi phạm SRP. Hãy tách thành 3 class riêng biệt:
```java
public class UserManager {
    public void saveUser(User u) { /* lưu DB */ }
    public void sendEmail(String to) { /* gửi email */ }
    public void generateReport() { /* tạo báo cáo */ }
}
```

### Bài 3.2 – DIP: Constructor Injection *(~10p)*
[ ] Tạo `interface NotificationService` → `EmailNotification`, `SmsNotification`. Tạo `OrderService` nhận `NotificationService` qua constructor (DIP). Test đổi implementation mà không sửa `OrderService`.

---

## Bài tập Ngày 31‑35: Collections *(Chapter 04)*

### Bài 4.1 – ArrayList CRUD *(~10p)*
[ ] Tạo `List<String>` chứa 5 tên sinh viên. Thực hiện: thêm, sửa (`set`), xoá theo index, tìm kiếm (`contains`), duyệt bằng `for-each`.

### Bài 4.2 – HashSet loại trùng *(~10p)*
[ ] Cho mảng `{"An","Bình","An","Cường","Bình","Dũng"}`. Dùng `HashSet` loại bỏ trùng, in ra. Thử `TreeSet` để xem kết quả sắp xếp.

### Bài 4.3 – HashMap đếm tần suất *(~15p)*
[ ] Cho mảng `{"apple","banana","apple","cherry","banana","apple"}`. Dùng `HashMap<String, Integer>` đếm số lần xuất hiện mỗi từ. Kết quả: `{apple=3, banana=2, cherry=1}`.

---

## Bài tập Ngày 36‑37: Generics *(Chapter 05)*

### Bài 5.1 – Generic ApiResponse *(~15p)*
[ ] Tạo class `ApiResponse<T>` gồm: `int statusCode`, `String message`, `T data`. Test với `ApiResponse<User>` và `ApiResponse<List<String>>`.

### Bài 5.2 – Bounded Type *(~10p)*
[ ] Viết method `<T extends Number> double average(List<T> list)` tính trung bình. Test với `List<Integer>` và `List<Double>`.

---

## Bài tập Ngày 38‑41: Lambda & Stream API *(Chapter 06)*

### Bài 6.1 – Lambda cơ bản *(~10p)*
[ ] Chuyển Comparator anonymous class sang Lambda, sau đó sang Method Reference: `names.sort(String::compareToIgnoreCase);`

### Bài 6.2 – Stream: Lọc & Biến đổi *(~15p)*
[ ] Cho `List<User>` (name, age). Dùng Stream: lọc user > 18 tuổi → lấy tên → viết hoa → sắp xếp → thu về List. In kết quả.

### Bài 6.3 – Collectors.groupingBy *(~10p)*
[ ] Cho `List<Product>` (name, category, price). Gom nhóm theo `category` bằng `Collectors.groupingBy()`. In mỗi nhóm.

### Bài 6.4 – Optional *(~10p)*
[ ] Viết method `findUserByEmail(String email)` trả về `Optional<User>`. Dùng `.map()`, `.filter()`, `.orElseThrow()` xử lý kết quả.

---

## Bài tập Ngày 42: Mini‑Project tổng hợp *(~30p)*

### Bài 7.1 – Quản lý sản phẩm Console
[ ] Xây dựng chương trình quản lý sản phẩm (`Product`: id, name, category, price):
- Lưu trong `List<Product>`.
- Dùng `Stream` lọc theo category, sắp xếp theo price, tìm sản phẩm đắt nhất.
- Dùng `Collectors.groupingBy()` thống kê số sản phẩm mỗi category.
- Trả kết quả qua `ApiResponse<T>`.
- Dùng `Optional` cho findById.

---

<details>
<summary><b>👉 Đáp án tham khảo (xem sau khi tự làm)</b></summary>

### Bài 4.3 – Đếm tần suất
```java
String[] fruits = {"apple","banana","apple","cherry","banana","apple"};
Map<String, Integer> count = new HashMap<>();
for (String f : fruits) count.merge(f, 1, Integer::sum);
// Hoặc: Arrays.stream(fruits).collect(Collectors.groupingBy(f->f, Collectors.summingInt(f->1)));
```

### Bài 6.2 – Stream lọc user
```java
List<String> result = users.stream()
    .filter(u -> u.getAge() > 18)
    .map(User::getName)
    .map(String::toUpperCase)
    .sorted()
    .toList();
```
</details>

---
*Hoàn thành = sẵn sàng Phase 3: HTTP & REST API! 🚀*

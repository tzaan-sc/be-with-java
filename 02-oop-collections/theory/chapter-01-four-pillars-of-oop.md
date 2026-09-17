# Chapter 01: 4 Trụ Cột OOP (Encapsulation, Inheritance, Polymorphism, Abstraction)

## 1. Lập trình hướng đối tượng (OOP) là gì?
- OOP tổ chức code xoay quanh **đối tượng** (Object) thay vì chỉ là hàm và biến rời rạc.
- Mỗi Object là 1 thực thể có **thuộc tính** (field/property) và **hành vi** (method).
- Java là ngôn ngữ OOP thuần tuý: mọi thứ đều nằm trong Class.

### Class vs Object
```java
// Class = bản thiết kế (blueprint)
public class User {
    private String name;
    private int age;
    
    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// Object = thực thể tạo từ Class
User user1 = new User("An", 25);   // Object 1
User user2 = new User("Bình", 30); // Object 2
```

## 2. Trụ cột 1: Đóng gói (Encapsulation)
> Ẩn dữ liệu bên trong, chỉ cho phép truy cập thông qua các method công khai.

```java
public class BankAccount {
    private double balance;  // ẨN: không cho truy cập trực tiếp từ bên ngoài

    public BankAccount(double initialBalance) {
        if (initialBalance < 0) throw new IllegalArgumentException("Số dư không hợp lệ");
        this.balance = initialBalance;
    }

    // Getter: cho phép ĐỌC
    public double getBalance() {
        return balance;
    }

    // Method công khai: KIỂM SOÁT cách thay đổi dữ liệu
    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("Số tiền phải > 0");
        this.balance += amount;
    }

    public void withdraw(double amount) {
        if (amount > balance) throw new IllegalArgumentException("Số dư không đủ");
        this.balance -= amount;
    }
}

// Sử dụng:
BankAccount acc = new BankAccount(1000);
// acc.balance = -9999;  // ❌ Compile Error (private)
acc.deposit(500);        // ✅ Qua method kiểm soát
```

### Access Modifiers (Phạm vi truy cập)
| Modifier | Cùng Class | Cùng Package | Subclass (khác package) | Mọi nơi |
|----------|-----------|-------------|------------------------|---------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` (không ghi) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> 💡 **Quy tắc:** Field luôn `private`, method public/protected tuỳ mục đích.

## 3. Trụ cột 2: Kế thừa (Inheritance)
> Class con **kế thừa** thuộc tính và phương thức từ Class cha, mở rộng hoặc ghi đè.

```java
// Class cha
public class Employee {
    protected String name;
    protected double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double calculateBonus() {
        return salary * 0.1;  // Thưởng 10%
    }
}

// Class con kế thừa
public class Manager extends Employee {
    private int teamSize;

    public Manager(String name, double salary, int teamSize) {
        super(name, salary);    // Gọi constructor cha
        this.teamSize = teamSize;
    }

    @Override
    public double calculateBonus() {
        return salary * 0.2 + teamSize * 500;  // Thưởng 20% + 500/người
    }
}
```

### Lưu ý quan trọng
- Java chỉ hỗ trợ **đơn kế thừa** (1 class chỉ extends 1 class cha).
- Từ khoá `super`: gọi constructor hoặc method của class cha.
- Từ khoá `this`: tham chiếu tới object hiện tại.
- Class `Object` là cha của mọi class trong Java.

## 4. Trụ cột 3: Đa hình (Polymorphism)

### 4.1 Compile-time Polymorphism: Overloading (Nạp chồng)
Cùng **tên method**, khác **tham số** (số lượng, kiểu, thứ tự).

```java
public class Calculator {
    public int add(int a, int b) { return a + b; }
    public double add(double a, double b) { return a + b; }
    public int add(int a, int b, int c) { return a + b + c; }
}
```

### 4.2 Runtime Polymorphism: Overriding (Ghi đè)
Class con **ghi đè** method cha, JVM quyết định chạy method nào tại **runtime**.

```java
Employee emp = new Manager("An", 5000, 10);
System.out.println(emp.calculateBonus());  
// Gọi method của Manager (runtime), KHÔNG phải Employee!
```

### 4.3 So sánh

| | Overloading | Overriding |
|---|-----------|-----------|
| Thời điểm | Compile-time | Runtime |
| Tên method | Giống | Giống |
| Tham số | **Khác** | **Giống** |
| Return type | Có thể khác | Giống hoặc covariant |
| Annotation | — | `@Override` |
| Phạm vi | Cùng class | Cha – Con |

## 5. Trụ cột 4: Trừu tượng (Abstraction)
> Ẩn chi tiết triển khai, chỉ lộ ra **"cái gì"** chứ không lộ **"làm thế nào"**.

### Dùng Abstract Class
```java
public abstract class Shape {
    protected String color;

    public Shape(String color) { this.color = color; }

    // Method trừu tượng: KHÔNG có body, bắt buộc class con triển khai
    public abstract double calculateArea();

    // Method thường: có body, class con kế thừa được
    public String getColor() { return color; }
}

public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;  // Triển khai cụ thể
    }
}
```

- **Không thể** tạo object trực tiếp từ abstract class (`new Shape()` → ❌).
- Có thể có cả abstract method và method thường.

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Giải thích 4 trụ cột OOP bằng ví dụ thực tế (Hệ thống Ngân hàng)
1. **Encapsulation (Đóng gói):**
   - *Ví dụ:* Lớp `BankAccount` có biến `private double balance;`. Người ngoài không thể tùy tiện gán `account.balance = 999999999;`. Muốn nạp tiền, bắt buộc phải thông qua hàm `public void deposit(double amount)` - nơi code sẽ kiểm tra điều kiện `amount > 0` và ghi lại lịch sử giao dịch.
2. **Inheritance (Kế thừa):**
   - *Ví dụ:* Lớp cha `Account` có chung các thuộc tính `accountNumber`, `ownerName`, `balance`. Các lớp con `SavingAccount` (tài khoản tiết kiệm có thêm `interestRate`) và `CreditAccount` (tài khoản tín dụng có thêm `creditLimit`) kế thừa lại code từ cha, tránh trùng lặp.
3. **Polymorphism (Đa hình):**
   - *Ví dụ:* Lớp cha `Payment` có hàm `pay(double amount)`. Khi gọi `payment.pay(100)`, nếu đối tượng thực tế là `CreditCardPayment` thì sẽ trừ thẻ tín dụng, nếu là `VnPayPayment` thì sinh mã QR, nếu là `MomoPayment` thì mở app Momo. Cùng một lời gọi hàm nhưng có nhiều cách biểu hiện khác nhau tùy theo đối tượng lúc runtime.
4. **Abstraction (Trừu tượng hóa):**
   - *Ví dụ:* Khi bạn rút tiền ở cây ATM, bạn chỉ cần đưa thẻ, bấm số tiền và nhận tiền mặt (`atm.withdraw(500000)`). Bạn hoàn toàn không cần biết bên trong cây ATM kết nối viễn thông ra sao, kiểm tra số dư ở chi nhánh nào, cơ chế đếm tờ tiền cơ học chạy như thế nào. Trừu tượng hóa giúp ẩn đi sự phức tạp bên trong và chỉ lộ ra giao diện sử dụng cần thiết.

### 6.2. Tại sao nên để field là `private`? Encapsulation giải quyết vấn đề gì?
- **Kiểm soát tính hợp lệ của dữ liệu (Data Validation):** Nếu field là `public`, bất kỳ ai cũng có thể gán `age = -5` hoặc `email = "khong-phai-email"`. Với `private` kết hợp getter/setter, ta có thể chặn dữ liệu rác ngay tại setter.
- **Tính toàn vẹn và bất biến (Immutability / Read-only):** Ta có thể tạo các trường chỉ đọc (chỉ cung cấp hàm Getter mà không có Setter).
- **Linh hoạt thay đổi logic nội bộ mà không làm hỏng code bên ngoài:** Ví dụ ban đầu lưu `fullName`, sau này tách thành `firstName` và `lastName`. Nếu code ngoài gọi `getFullName()`, ta chỉ cần sửa code bên trong hàm getter đó mà không làm crash hàng trăm file khác đang dùng.

### 6.3. Phân biệt Overloading (Nạp chồng) và Overriding (Ghi đè)
| Tiêu chí | Method Overloading | Method Overriding |
| :--- | :--- | :--- |
| **Vị trí** | Trong **cùng một class**. | Giữa **class con** và **class cha** (quan hệ kế thừa). |
| **Tên phương thức** | **Bắt buộc giống nhau**. | **Bắt buộc giống nhau**. |
| **Danh sách tham số** | **Bắt buộc phải khác nhau** (số lượng, kiểu dữ liệu, hoặc thứ tự). | **Bắt buộc phải giống hệt** class cha. |
| **Kiểu trả về** | Có thể giống hoặc khác. | Phải giống hoặc là kiểu con (Covariant return type). |
| **Thời điểm phân giải** | **Compile-time** (Static Polymorphism - dựa vào tham số lúc gọi). | **Runtime** (Dynamic Polymorphism - dựa vào kiểu đối tượng thực tế trên Heap). |
| **Annotation** | Không dùng. | Dùng `@Override` để nhờ compiler kiểm tra tính chính xác. |

### 6.4. Java có hỗ trợ đa kế thừa (Multiple Inheritance) không? Tại sao? Giải pháp thay thế?
- **Câu trả lời:** Java **KHÔNG** hỗ trợ đa kế thừa class (`class C extends A, B` $\rightarrow$ ❌ Lỗi biên dịch).
- **Tại sao Java cấm đa kế thừa class?**
  - Để tránh bài toán hiểm hóc **Kim Cương (The Diamond Problem)**: Giả sử cả Class `A` và Class `B` đều có hàm `display()`. Class `C` kế thừa cả `A` và `B`. Khi gọi `c.display()`, JVM sẽ không thể biết được nên chạy hàm `display()` của `A` hay của `B`, dẫn tới sự nhập nhằng mơ hồ.
- **Giải pháp thay thế:**
  1. **Triển khai nhiều Interface (Multiple Interfaces):** Một class có thể `implements` vô số interface: `class C implements InterfaceA, InterfaceB`.
  2. **Ưu tiên Thành phần hơn Kế thừa (Composition over Inheritance):** Thay vì kế thừa, ta nhét các object của `A` và `B` làm thuộc tính bên trong `C`:
     ```java
     class C {
         private A a = new A();
         private B b = new B();
     }
     ```

### 6.5. Abstract class có thể có Constructor không? Mục đích?
- **Câu trả lời:** **CÓ THỂ VÀ HOÀN TOÀN HỢP LỆ.** Mặc dù không thể gọi `new AbstractClass()` trực tiếp.
- **Mục đích:**
  1. Khởi tạo các thuộc tính chung mà lớp cha quản lý (ví dụ: `id`, `createdAt`, `color`).
  2. Khi một class con được khởi tạo (`new Dog()`), constructor của class con **bắt buộc phải gọi `super(...)`** để khởi tạo phần thuộc tính của class cha trước tiên theo đúng thứ tự phân cấp bộ nhớ.
  3. Áp dụng Design Pattern (ví dụ: Template Method Pattern), ép buộc các giá trị mặc định phải có ngay khi tạo đối tượng con.

---
*Thực hành:* Tạo class `Employee` → `Manager` với kế thừa, viết `BankAccount` minh hoạ Encapsulation, tạo `Shape` abstract → `Circle`, `Rectangle`.

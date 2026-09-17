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

## 6. Câu hỏi phỏng vấn thường gặp
1. Giải thích 4 trụ cột OOP bằng ví dụ thực tế.
2. Tại sao nên để field là `private`? Encapsulation giải quyết vấn đề gì?
3. Phân biệt Overloading và Overriding.
4. Java có hỗ trợ đa kế thừa không? Tại sao? Giải pháp thay thế?
5. Abstract class có thể có constructor không? Mục đích?

---
*Thực hành:* Tạo class `Employee` → `Manager` với kế thừa, viết `BankAccount` minh hoạ Encapsulation, tạo `Shape` abstract → `Circle`, `Rectangle`.

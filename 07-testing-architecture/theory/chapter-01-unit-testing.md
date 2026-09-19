# Chapter 01: Unit Testing với JUnit 5 & Assertions

---

## 1. Unit Testing là gì?

**Unit Test (Kiểm thử đơn vị)** là việc kiểm tra các thành phần nhỏ nhất có thể kiểm thử được của phần mềm (thường là một method hoặc một class) một cách độc lập và cô lập.

### Kim tự tháp kiểm thử (Testing Pyramid):
```
                          ┌───────────────────────────┐
                          │     End-to-End Tests      │  ▲ ÍT NHẤT, CHẬM NHẤT, CHI PHÍ CAO
                          │ (UI / Toàn bộ hệ thống)   │  │ Chạy: vài chục giây - vài phút
                     ┌────┴───────────────────────────┴────┐
                     │          Integration Tests          │  │ TRUNG BÌNH
                     │  (Kiểm thử tích hợp API / DB / Web) │  │ Chạy: vài giây
                ┌────┴─────────────────────────────────────┴────┐
                │                  Unit Tests                   │  │ NHIỀU NHẤT, NHANH NHẤT, CHI PHÍ THẤP
                │ (Kiểm thử cô lập từng Method / Service Logic) │  ▼ Chạy: vài mili-giây
                └───────────────────────────────────────────────┘
```

---

## 2. Mô hình AAA (Arrange - Act - Assert)

Mỗi test case chuẩn mực nên được cấu trúc rõ ràng theo 3 bước:
1. **Arrange (Chuẩn bị)**: Khởi tạo dữ liệu đầu vào, đối tượng và điều kiện tiên quyết.
2. **Act (Hành động)**: Gọi hàm/phương thức cần kiểm thử với dữ liệu đã chuẩn bị.
3. **Assert (Kiểm chứng)**: So sánh kết quả trả về thực tế với kết quả mong đợi.

---

## 3. Các Annotation cốt lõi trong JUnit 5 (Jupiter)

| Annotation | Ý nghĩa |
| :--- | :--- |
| `@Test` | Đánh dấu phương thức là một test case có thể thực thi. |
| `@DisplayName("Mô tả")` | Đặt tên hiển thị trực quan, dễ hiểu trên giao diện chạy test. |
| `@BeforeEach` | Chạy **trước mỗi** `@Test` method (dùng để reset dữ liệu/khởi tạo đối tượng). |
| `@AfterEach` | Chạy **sau mỗi** `@Test` method (dọn dẹp tài nguyên). |
| `@BeforeAll` | Chạy **duy nhất 1 lần trước tất cả** các test methods (phải là `static`). |
| `@AfterAll` | Chạy **duy nhất 1 lần sau tất cả** các test methods (phải là `static`). |
| `@Disabled` | Bỏ qua test case này khi chạy test tự động. |
| `@ParameterizedTest` | Chạy cùng 1 test case với nhiều bộ dữ liệu đầu vào khác nhau (kết hợp `@ValueSource`, `@CsvSource`). |

---

## 4. Các Assertions thông dụng trong JUnit 5

```java
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

class CalculatorTest {

    private final Calculator calculator = new Calculator();

    @Test
    @DisplayName("Cộng hai số nguyên dương chính xác")
    void testAddPositiveNumbers() {
        // Arrange
        int a = 10;
        int b = 20;

        // Act
        int result = calculator.add(a, b);

        // Assert
        assertEquals(30, result, "10 + 20 phải bằng 30");
        assertTrue(result > 0);
    }

    @Test
    @DisplayName("Chia cho 0 phải ném ra ArithmeticException")
    void testDivideByZeroThrowsException() {
        // Kiểm thử ngoại lệ
        ArithmeticException exception = assertThrows(ArithmeticException.class, () -> {
            calculator.divide(10, 0);
        });

        assertEquals("/ by zero", exception.getMessage());
    }

    @Test
    @DisplayName("Kiểm tra nhiều assertions cùng lúc với assertAll")
    void testMultipleProperties() {
        User user = new User("John", 25);

        // assertAll đảm bảo chạy hết mọi assertion dù có một assertion fail
        assertAll("Kiểm tra thông tin user",
            () -> assertEquals("John", user.getName()),
            () -> assertEquals(25, user.getAge()),
            () -> assertNotNull(user)
        );
    }
}
```

---

## 5. Parameterized Tests (Kiểm thử với nhiều bộ dữ liệu)

Giúp giảm trùng lặp code khi kiểm tra cùng một hàm logic với nhiều case khác nhau:

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;
import static org.junit.jupiter.api.Assertions.assertTrue;

class StringUtilsTest {

    @ParameterizedTest
    @ValueSource(strings = {"racecar", "radar", "level", "madam"})
    @DisplayName("Kiểm tra các chuỗi đối xứng (Palindrome)")
    void testIsPalindrome(String word) {
        assertTrue(StringUtils.isPalindrome(word));
    }
}
```

---

## 6. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 6.1. Nguyên tắc F.I.R.S.T trong Unit Testing là gì?
Một bộ Unit Test chất lượng cao bắt buộc phải thỏa mãn 5 tiêu chí **F.I.R.S.T**:
1. **F - Fast (Nhanh):** Test phải chạy trong vài phần nghìn giây. Nếu cả bộ test mất 30 phút, developer sẽ lười chạy test.
2. **I - Independent / Isolated (Độc lập):** Các hàm test không được phụ thuộc vào nhau. Thứ tự chạy test không được ảnh hưởng kết quả. Không chia sẻ trạng thái chung (State).
3. **R - Repeatable (Lặp lại được):** Chạy ở bất kỳ đâu (máy dev, máy tester, hay CI/CD không có mạng) đều phải cho ra cùng một kết quả duy nhất.
4. **S - Self-validating (Tự kiểm chứng):** Test phải tự động trả về `Pass` hoặc `Fail` thông qua các lệnh Assertion, không bắt con người phải tự nhìn log để đoán đúng sai.
5. **T - Timely / Thorough (Kịp thời & Toàn diện):** Viết test song song hoặc trước khi viết code nghiệp vụ (TDD), bao phủ cả các trường hợp biên (Edge cases, Null, Negative numbers).

### 6.2. Cấu trúc 3A (Arrange - Act - Assert) tổ chức một ca kiểm thử thế nào?
Mọi hàm Unit Test chuẩn mực đều được chia thành 3 phần rõ ràng:
```java
@Test
void withdraw_shouldDeductBalance_whenBalanceIsSufficient() {
    // 1. Arrange (Chuẩn bị): Thiết lập dữ liệu đầu vào và trạng thái ban đầu
    BankAccount account = new BankAccount(1000.0);
    double amountToWithdraw = 400.0;

    // 2. Act (Hành động): Kích hoạt phương thức cần kiểm thử
    account.withdraw(amountToWithdraw);

    // 3. Assert (Khẳng định): So sánh kết quả thực tế với kỳ vọng
    assertEquals(600.0, account.getBalance());
}
```

### 6.3. Test Coverage (Độ phủ kiểm thử) là gì? Có nên cố gắng đạt 100% Code Coverage không?
- **Code Coverage:** Là tỷ lệ phần trăm số dòng code (Line Coverage) hoặc nhánh rẽ `if-else` (Branch Coverage) được thực thi trong quá trình chạy bộ test.
- **Có nên chạy theo 100% Coverage?**
  - **KHÔNG NÊN.** 100% Coverage chỉ chứng minh rằng "mọi dòng code đã được đi qua", chứ **KHÔNG HỀ CHỨNG MINH code không có bug logic** (ví dụ bạn gọi hàm nhưng không viết câu `assertEquals()` nào thì coverage vẫn là 100% nhưng test hoàn toàn vô dụng!).
  - **Mục tiêu thực tế:** Mức độ phủ lý tưởng của các dự án Backend chất lượng thường là **75% - 85%**, tập trung 100% cho các **Core Business Logic nhạy cảm** (tính tiền, bảo mật, xử lý giao dịch) và bỏ qua các hàm Getter/Setter, DTO, Config boiler-plate.

---
*Thực hành:* Viết Unit Test bằng JUnit 5 cho hàm tính chiết khấu đơn hàng với `@ParameterizedTest` và `@CsvSource`.

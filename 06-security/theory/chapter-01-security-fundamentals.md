# Chapter 01: Nền Tảng Bảo Mật – Authentication vs Authorization & Hash Mật Khẩu với BCrypt

---

## 1. Authentication (Xác thực) vs Authorization (Phân quyền)

Trong phát triển hệ thống Backend, đây là 2 khái niệm nền tảng luôn đi kèm nhưng có mục đích hoàn toàn riêng biệt:

```mermaid
graph LR
    User["Client / User"] -->|1. Cung cấp thông tin đăng nhập (Credentials)| Auth["Authentication (Xác thực)"]
    Auth -->|"Bạn là ai? (Hợp lệ)"| Token["Cấp Danh Tính / Token"]
    Token -->|2. Gửi request kèm Token| Author["Authorization (Phân quyền)"]
    Author -->|"Bạn có quyền làm gì?"| Resource["Tài nguyên / API"]
```

| Tiêu chí | Authentication (Xác thực - 401 Unauthorized) | Authorization (Phân quyền - 403 Forbidden) |
| :--- | :--- | :--- |
| **Câu hỏi cốt lõi** | **"Bạn là ai?" (Who are you?)** | **"Bạn có quyền làm gì?" (What can you do?)** |
| **Thời điểm diễn ra**| Luôn diễn ra **đầu tiên**. | Diễn ra **sau** khi đã xác thực danh tính thành công. |
| **Thông tin kiểm tra**| Username, Password, OTP, Sinh trắc học, Chữ ký số. | Vai trò (Roles: `ADMIN`, `USER`), Quyền hạn (Permissions: `READ`, `WRITE`, `DELETE`). |
| **Lỗi trả về HTTP**| **`401 Unauthorized`** (Chưa đăng nhập hoặc token sai/hết hạn). | **`403 Forbidden`** (Đã đăng nhập nhưng không đủ thẩm quyền truy cập). |

---

## 2. Nguyên tắc bảo mật mật khẩu người dùng

> ⚠️ **Quy tắc bất biến:** TUYỆT ĐỐI KHÔNG BAO GIỜ lưu mật khẩu dưới dạng chuỗi thuần (Plaintext) vào Database!

### Tại sao không dùng các thuật toán băm thông thường (MD5, SHA-1, SHA-256)?
- **MD5 / SHA-256** là các thuật toán băm hướng tới **tốc độ nhanh** (thích hợp kiểm tra checksum file).
- Tuy nhiên, vì quá nhanh nên kẻ tấn công có thể dùng kỹ thuật vét cạn (Brute-force) hoặc tra cứu qua **Rainbow Table** (bảng bảng băm tính sẵn hàng tỉ mật khẩu phổ biến) để giải ngược ra mật khẩu gốc chỉ trong vài giây.

---

## 3. Giải pháp chuẩn: BCrypt Hashing Algorithm

**BCrypt** là thuật toán băm mật khẩu chuẩn trong ngành phát triển phần mềm nhờ 2 đặc tính ưu việt:

### A. Tự động sinh Salt (Muối ngẫu nhiên)
- Mỗi lần băm cùng một mật khẩu (ví dụ: `"password123"`), BCrypt tự động tạo ra một chuỗi ngẫu nhiên (Salt) và nhúng chung vào chuỗi kết quả.
- Kết quả là: Hai tài khoản có cùng mật khẩu `"password123"` sẽ có 2 chuỗi băm **hoàn toàn khác nhau** trong cơ sở dữ liệu.
- Kẻ tấn công không thể sử dụng Rainbow Table để dò quét hàng loạt.

### B. Cơ chế Work Factor (Độ phức tạp tính toán)
- Cho phép điều chỉnh số vòng lặp tính toán (Cost factor, mặc định là $10$ hoặc $12$, tương đương $2^{10} = 1024$ vòng lặp).
- Máy tính càng mạnh lên theo thời gian thì ta chỉ cần nâng Cost factor lên để kéo dài thời gian tính toán băm, vô hiệu hóa các dàn máy đào GPU giải mã Brute-force.

---

## 4. Cấu trúc của một chuỗi BCrypt Hash

Một chuỗi BCrypt lưu trong database thường có độ dài 60 ký tự, chia thành 3 phần:

```text
$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
\__/ \/ \____________________/\_____________________________/
 (1) (2)         (3)                        (4)
```

1. **`$2a$`**: Phiên bản thuật toán BCrypt.
2. **`10`**: Cost factor ($2^{10}$ vòng băm).
3. **`N9qo8uLOickgx2ZMRZoMye`**: 22 ký tự Salt ngẫu nhiên được sinh ra.
4. **`IjZAgcfl7p92ldGxad68LJZdL17lhWy`**: 31 ký tự băm của (Mật khẩu + Salt).

---

## 5. Cài đặt và sử dụng `PasswordEncoder` trong Spring Boot

Spring Security cung cấp interface `PasswordEncoder` với implementation chuẩn mực là `BCryptPasswordEncoder`.

### Cấu hình Bean trong Spring:
```java
package com.example.app.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
public class SecurityBeanConfig {

    @Bean
    public PasswordEncoder passwordEncoder() {
        // Độ mạnh mặc định: 10 vòng lặp
        return new BCryptPasswordEncoder();
    }
}
```

### Sử dụng khi Đăng ký (Encode) & Đăng nhập (Matches):
```java
@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;

    // 1. Khi người dùng ĐĂNG KÝ
    public void register(RegisterRequest request) {
        // Băm mật khẩu trước khi lưu DB
        String encodedPassword = passwordEncoder.encode(request.getPassword());

        UserEntity user = UserEntity.builder()
                .email(request.getEmail())
                .password(encodedPassword)
                .role(Role.USER)
                .build();

        userRepository.save(user);
    }

    // 2. Khi người dùng ĐĂNG NHẬP
    public boolean checkLogin(String rawPassword, String encodedPasswordFromDb) {
        // KHÔNG BAO GIỜ băm lại rawPassword rồi so sánh chuỗi (vì Salt ngẫu nhiên nên sẽ không bao giờ bằng nhau)
        // BẮT BUỘC dùng phương thức matches() của BCrypt
        return passwordEncoder.matches(rawPassword, encodedPasswordFromDb);
    }
}
```

---

## 6. Câu hỏi phỏng vấn thường gặp (Interview Q&A)

### Q1: Vì sao hàm `passwordEncoder.encode("123456")` chạy 2 lần cho ra 2 kết quả khác nhau, nhưng hàm `passwordEncoder.matches("123456", hash)` vẫn trả về `true`?
**Trả lời:**
- Do mỗi lần gọi `encode()`, BCrypt tự động sinh ra một chuỗi Salt ngẫu nhiên và gắn luôn vào trong chuỗi hash kết quả.
- Khi gọi `matches(rawPassword, hash)`, BCrypt sẽ bóc tách chuỗi Salt nằm trong chuỗi `hash` có sẵn, lấy Salt đó băm chung với `rawPassword` và đối chiếu phần còn lại. Nếu khớp, trả về `true`.

### Q2: Sự khác biệt giữa mã hóa (Encryption) và băm (Hashing) là gì?
**Trả lời:**
- **Mã hóa (Encryption)**: Là thuật toán **2 chiều** (Reversible). Dữ liệu sau khi mã hóa có thể được giải mã ngược lại thành bản rõ nếu có Secret Key (ví dụ: AES, RSA).
- **Băm (Hashing)**: Là thuật toán **1 chiều** (Irreversible). Không thể giải mã ngược chuỗi băm về ban đầu. Mật khẩu bắt buộc phải dùng Hashing, không dùng Encryption.

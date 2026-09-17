# Chapter 05: Cấu Hình CORS & CSRF Trong REST API

---

## 1. CORS (Cross-Origin Resource Sharing)

### A. Same-Origin Policy (Chính sách cùng nguồn gốc) là gì?
Mặc định, các trình duyệt web (Chrome, Firefox, Safari) áp dụng chính sách **Same-Origin Policy** vì lý do an toàn. Một trang web chỉ được phép gửi request JavaScript (AJAX/Fetch) đến một server khác nếu có **cùng Nguồn (Origin)**:
$$\text{Origin} = \text{Protocol (http/https)} + \text{Domain/Host} + \text{Port}$$

Ví dụ:
- Trang Frontend: `http://localhost:3000` (React/Vue/Angular)
- Server Backend: `http://localhost:8080` (Spring Boot)
- **Khác Port (3000 vs 8080) $\rightarrow$ Khác Origin $\rightarrow$ Trình duyệt tự động chặn kết quả và báo lỗi CORS!**

```text
Access to fetch at 'http://localhost:8080/api/v1/products' from origin 'http://localhost:3000' 
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

---

### B. Cơ chế Preflight Request (HTTP `OPTIONS`)
Khi gửi các request làm thay đổi dữ liệu hoặc có chứa Header tùy biến (như `Authorization: Bearer <token>`):
1. Trình duyệt sẽ tự động bắn một request thăm dò gọi là **Preflight Request** với HTTP method là **`OPTIONS`**.
2. Server Backend phải phản hồi cho phép Origin, Method và Headers đó.
3. Sau khi nhận được sự đồng ý từ Server, trình duyệt mới gửi HTTP Request chính thức (`GET`, `POST`, `PUT`, `DELETE`).

---

### C. Cấu hình CORS chuẩn mực trong Spring Security 6.x

Trong ứng dụng Spring Security, **CorsFilter phải được đặt trước chuỗi xác thực**, cấu hình thông qua `CorsConfigurationSource`:

```java
package com.example.app.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.CorsConfigurationSource;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;

import java.util.List;

@Configuration
public class CorsConfig {

    @Bean
    public CorsConfigurationSource corsConfigurationSource() {
        CorsConfiguration configuration = new CorsConfiguration();

        // 1. Cho phép các Origin của Frontend
        configuration.setAllowedOrigins(List.of("http://localhost:3000", "https://myfrontend.com"));

        // 2. Cho phép các HTTP Methods
        configuration.setAllowedMethods(List.of("GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"));

        // 3. Cho phép các Headers cần thiết
        configuration.setAllowedHeaders(List.of("Authorization", "Content-Type", "X-Requested-With", "Accept"));

        // 4. Cho phép gửi kèm Credentials (Cookies, Auth Headers)
        configuration.setAllowCredentials(true);

        // 5. Cho phép Client đọc các Headers phản hồi
        configuration.setExposedHeaders(List.of("Authorization", "Link", "X-Total-Count"));

        // 6. Thời gian cache kết quả Preflight request (1 giờ)
        configuration.setMaxAge(3600L);

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration);
        return source;
    }
}
```

Kích hoạt trong `SecurityFilterChain`:
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        // Bật CORS sử dụng Bean cấu hình ở trên
        .cors(cors -> cors.configurationSource(corsConfigurationSource()))
        .csrf(csrf -> csrf.disable())
        // ...
        ;
    return http.build();
}
```

---

## 2. CSRF (Cross-Site Request Forgery)

### A. Tấn công CSRF là gì?
**CSRF** là hình thức tấn công mà kẻ gian lừa trình duyệt của nạn nhân gửi một request trái phép đến một website mà nạn nhân đã đăng nhập từ trước:

1. Nạn nhân đăng nhập vào ngân hàng `bank.com`, ngân hàng lưu phiên đăng nhập trong **Cookie**.
2. Nạn nhân vô tình bấm vào link độc của hacker `evil.com`.
3. Trang `evil.com` chạy script âm thầm gửi `POST https://bank.com/transfer?to=hacker&amount=1000`.
4. Trình duyệt tự động đính kèm **Cookie** của `bank.com` theo request $\rightarrow$ Ngân hàng tưởng nạn nhân gửi và thực hiện chuyển tiền!

---

### B. Tại sao trong REST API dùng JWT lại TẮT CSRF (`csrf.disable()`)?

| Kiến trúc | Quản lý phiên | Nguy cơ CSRF | Cấu hình CSRF |
| :--- | :--- | :--- | :--- |
| **Monolith (JSP / Thymeleaf / MVC)** | Dùng **Session ID lưu trong Cookie** do trình duyệt tự động gửi kèm. | **Rất cao** (Bị mạo danh cookie dễ dàng). | **Bắt buộc BẬT** CSRF Token. |
| **REST API + JWT (Stateless)** | Lưu JWT trong **LocalStorage / Memory**, gửi qua header `Authorization: Bearer <token>`. | **Không có nguy cơ CSRF**, vì trình duyệt KHÔNG tự động gắn Header Authorization khi click link lạ! | **TẮT (`csrf.disable()`)** để tránh xung đột không cần thiết. |

> 📌 **Lưu ý ngoại lệ:** Nếu hệ thống của bạn lưu JWT trong **HttpOnly Cookie** thay vì LocalStorage, lúc này bạn **vẫn phải bật bảo vệ CSRF** (bằng cơ chế Double Submit Cookie hoặc SameSite attribute).

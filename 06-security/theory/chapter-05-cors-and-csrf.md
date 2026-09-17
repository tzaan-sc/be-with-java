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

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. CORS là cơ chế bảo mật của ai? Server hay Browser?
- **Khẳng định:** CORS là chính sách bảo mật do **TRÌNH DUYỆT (BROWSER)** thực thi (Client-side Security Mechanism), **KHÔNG PHẢI của Server**!
- **Chứng minh:**
  - Nếu bạn dùng Postman, cURL, hoặc code Backend gọi tới một API không cấu hình CORS, request **vẫn chạy thành công 100% và nhận đủ dữ liệu**.
  - Nhưng nếu chạy JavaScript trên trình duyệt (từ `http://localhost:3000` gọi tới `http://localhost:8080`), trình duyệt sẽ kiểm tra Header phản hồi: Nếu không thấy `Access-Control-Allow-Origin`, chính **trình duyệt sẽ chủ động chặn dữ liệu lại** và ném lỗi đỏ lòm trên màn hình Console để bảo vệ người dùng.

### 4.2. Preflight Request (OPTIONS) là gì? Khi nào trình duyệt gửi Preflight Request?
- **Preflight Request:** Là một HTTP request thăm dò với phương thức **`OPTIONS`** do trình duyệt tự động âm thầm gửi lên Server **TRƯỚC KHI** gửi request thật sự.
- **Mục đích:** Hỏi Server: *"Này máy chủ, tôi từ domain này, muốn gửi method PUT/DELETE kèm header Authorization này, máy chủ có cho phép không?"*. Nếu Server trả về mã `200 OK` kèm các header cho phép, trình duyệt mới gửi request chính thức.
- **Khi nào bị kích hoạt Preflight:**
  Khi request **KHÔNG PHẢI là "Simple Request"**:
  1. Dùng các HTTP Method: `PUT`, `DELETE`, `PATCH`.
  2. Dùng Content-Type: `application/json` (Simple request chỉ cho phép `text/plain`, `multipart/form-data`, `application/x-www-form-urlencoded`).
  3. Có đính kèm Custom Headers như `Authorization: Bearer <token>`.

### 4.3. Kịch bản tấn công CSRF (Cross-Site Request Forgery) diễn ra như thế nào?
- **Kịch bản:**
  1. Nạn nhân đăng nhập vào trang ngân hàng `mybank.com`. Ngân hàng cấp một Cookie xác thực lưu trong trình duyệt.
  2. Nạn nhân vô tình mở một tab mới và click vào một đường link độc hại trên trang web lừa đảo `evil.com`.
  3. Trang `evil.com` âm thầm chứa một đoạn mã:
     `<img src="https://mybank.com/api/transfer?toAccount=hacker&amount=10000000" />`
  4. Trình duyệt tự động đính kèm Cookie ngân hàng hợp lệ của nạn nhân vào request chuyển tiền đó.
  5. Ngân hàng nhận được request kèm đúng Cookie của nạn nhân nên tưởng là lệnh thật $\rightarrow$ Chuyển tiền thành công cho hacker!
- **Cách phòng chống:** Dùng **CSRF Token** (mỗi form có 1 token ngẫu nhiên mà trang lạ không thể đọc được), hoặc cấu hình thuộc tính Cookie **`SameSite=Strict`** để cấm trình duyệt gửi cookie khi click từ trang web khác.

---
*Thực hành:* Cấu hình `CorsConfigurationSource` cho phép Frontend `http://localhost:3000` gọi API với đầy đủ các method `GET, POST, PUT, DELETE`.

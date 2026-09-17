# 🛠 Bài Tập Thực Hành – Phase 6: Spring Security & Bảo Mật Hệ Thống

> Lộ trình Ngày 93 – Ngày 106 (20‑30 phút/ngày). Từng bước xây dựng hệ thống bảo mật Authentication/Authorization chuẩn cho REST API.

---

## Bài tập Ngày 93‑95: Căn Bản Spring Security & BCrypt *(Chapter 01 & 02)*

### Bài 1.1 – Kiểm nghiệm tính năng Hashing của BCrypt *(~15p)*
[ ] Thêm dependency `spring-boot-starter-security` vào `pom.xml`.
[ ] Tạo class test kiểm tra `BCryptPasswordEncoder`:
```java
PasswordEncoder encoder = new BCryptPasswordEncoder();
String rawPass = "admin123";
String hash1 = encoder.encode(rawPass);
String hash2 = encoder.encode(rawPass);

System.out.println("Hash 1: " + hash1);
System.out.println("Hash 2: " + hash2);
System.out.println("Matches 1: " + encoder.matches(rawPass, hash1)); // true
System.out.println("Matches 2: " + encoder.matches(rawPass, hash2)); // true
```
[ ] Quan sát: 2 chuỗi hash hoàn toàn khác nhau nhưng cả 2 đều trả về `true` khi gọi `.matches()`.

### Bài 1.2 – Cấu hình SecurityFilterChain cơ bản *(~20p)*
[ ] Tạo class `SecurityConfig`:
  - Cho phép `GET /api/v1/public/**` không cần đăng nhập.
  - Các API khác yêu cầu đăng nhập.
  - Tắt CSRF: `.csrf(csrf -> csrf.disable())`.
[ ] Dùng Postman gọi thử:
  - `GET /api/v1/public/hello`: Trả về `200 OK`.
  - `GET /api/v1/products`: Trả về `401 Unauthorized` hoặc form login mặc định.

---

## Bài tập Ngày 96‑97: Nạp User từ Database *(Chapter 02)*

### Bài 2.1 – Cài đặt `CustomUserDetails` & `CustomUserDetailsService` *(~30p)*
[ ] Tạo class `CustomUserDetails implements UserDetails`:
  - Bọc lấy `UserEntity`.
  - Trả về `SimpleGrantedAuthority("ROLE_" + user.getRole().name())`.
[ ] Tạo class `CustomUserDetailsService implements UserDetailsService`:
  - Inject `UserRepository`.
  - Triển khai hàm `loadUserByUsername(String email)` tìm user trong DB và trả về `CustomUserDetails`.
[ ] Khai báo Bean `AuthenticationProvider` và `AuthenticationManager` trong file cấu hình.

---

## Bài tập Ngày 98‑101: JWT Service & Filter Chain *(Chapter 03)*

### Bài 3.1 – Tạo `JwtService` *(~25p)*
[ ] Thêm 3 thư viện `jjwt` (api, impl, jackson).
[ ] Viết `JwtService` với các chức năng:
  - `generateToken(UserDetails user)`: Sinh JWT có thời hạn sống 24h.
  - `extractUsername(String token)`: Đọc claim `subject`.
  - `isTokenValid(String token, UserDetails user)`: Kiểm tra khớp email và chưa quá hạn.

### Bài 3.2 – Tạo `JwtAuthenticationFilter` *(~30p)*
[ ] Tạo class `JwtAuthenticationFilter extends OncePerRequestFilter`:
  - Trích xuất header `Authorization: Bearer <token>`.
  - Nếu có token và chưa xác thực trong `SecurityContextHolder`: kiểm tra hợp lệ, tải `UserDetails` và nạp `UsernamePasswordAuthenticationToken` vào `SecurityContext`.
[ ] Đăng ký filter vào `SecurityConfig`:
  - `.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))`
  - `.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class)`

---

## Bài tập Ngày 102‑103: API Đăng Ký & Đăng Nhập & Refresh Token *(Chapter 03)*

### Bài 4.1 – Xây dựng AuthController & AuthService *(~30p)*
[ ] Viết API `POST /api/v1/auth/register`:
  - Nhận `RegisterRequest(fullName, email, password)`.
  - Kiểm tra email trùng lặp, hash password với BCrypt và lưu DB.
  - Trả về `RegisterResponse` thông báo thành công.
[ ] Viết API `POST /api/v1/auth/login`:
  - Nhận `LoginRequest(email, password)`.
  - Gọi `authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(email, password))`.
  - Sinh JWT và trả về `AuthResponse(accessToken, refreshToken)`.

### Bài 4.2 – Kiểm thử với Postman *(~20p)*
[ ] Gọi API Đăng ký tài khoản mới.
[ ] Gọi API Đăng nhập và copy chuỗi `accessToken` nhận được.
[ ] Gọi API bảo mật `GET /api/v1/products`:
  - Đính kèm Header `Authorization: Bearer <accessToken>` $\rightarrow$ Nhận `200 OK`.
  - Thử sửa 1 ký tự trong chuỗi Token $\rightarrow$ Nhận `401 Unauthorized` hoặc `403 Forbidden`.

---

## Bài tập Ngày 104‑106: Phân Quyền RBAC, CORS & Hoàn Thiện Hệ Thống *(Chapter 04 & 05)*

### Bài 5.1 – Phân quyền bằng `@PreAuthorize` *(~25p)*
[ ] Bật `@EnableMethodSecurity` trong `SecurityConfig`.
[ ] Thêm bảo vệ vào `ProductController`:
  - `GET /api/v1/products`: Ai cũng xem được (`permitAll()` hoặc chỉ cần đăng nhập).
  - `POST /api/v1/products`: `@PreAuthorize("hasRole('ADMIN')")`.
  - `DELETE /api/v1/products/{id}`: `@PreAuthorize("hasRole('ADMIN')")`.
[ ] Tạo 2 tài khoản: 1 tài khoản role `USER`, 1 tài khoản role `ADMIN`.
[ ] Dùng Postman test: Dùng token của tài khoản `USER` gọi `DELETE /api/v1/products/1` $\rightarrow$ Xác nhận bị chặn lỗi `403 Forbidden`.

### Bài 5.2 – Cấu hình CORS chuẩn *(~15p)*
[ ] Tạo Bean `CorsConfigurationSource` cho phép `http://localhost:3000` với đầy đủ methods (`GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`).
[ ] Gắn `.cors(cors -> cors.configurationSource(corsConfigurationSource()))` vào chuỗi bảo mật.

### Bài 5.3 – Chuẩn hóa định dạng lỗi 401 & 403 JSON *(~20p)*
[ ] Tạo `CustomAuthenticationEntryPoint` xử lý lỗi 401 (Chưa đăng nhập / Token không hợp lệ).
[ ] Tạo `CustomAccessDeniedHandler` xử lý lỗi 403 (Không đủ quyền hạn).
[ ] Đảm bảo cả hai đều trả về JSON format chuẩn:
```json
{
  "timestamp": "2026-09-17T10:30:00",
  "status": 403,
  "error": "Forbidden",
  "message": "Bạn không có quyền truy cập chức năng này!",
  "path": "/api/v1/products/1"
}
```

---
*Hoàn thành = Sẵn sàng cho Phase 7: Testing, Clean Architecture & Production! 🚀*

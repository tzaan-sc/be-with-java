# Chapter 03: Xác Thực Không Trạng Thái với JWT (JSON Web Token)

---

## 1. JSON Web Token (JWT) là gì?

**JWT** (RFC 7519) là một chuẩn mở định nghĩa phương thức truyền tải thông tin an toàn, nhỏ gọn giữa các bên dưới dạng đối tượng JSON.

Trong kiến trúc Backend hiện đại:
- **Session/Cookie truyền thống**: Server lưu trạng thái đăng nhập vào RAM/Redis. Khi có hàng triệu user hoặc nhiều cụm server (Horizontal Scaling), việc đồng bộ session trở nên phức tạp và tốn tài nguyên.
- **JWT (Stateless)**: Server **không lưu trạng thái phiên**. Thông tin user (Id, Email, Role) được đóng gói trực tiếp vào chuỗi token, ký số bằng mật mã bí mật và giao cho Client lưu giữ. Mỗi request client chỉ cần gửi token kèm theo.

---

## 2. Cấu trúc của chuỗi JWT

Một chuỗi JWT gồm 3 phần được phân tách bằng dấu chấm (`.`):

$$\text{JWT} = \underbrace{\text{Header}}_{\text{Base64Url}} \,.\, \underbrace{\text{Payload}}_{\text{Base64Url}} \,.\, \underbrace{\text{Signature}}_{\text{Mã băm bí mật}}$$

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
\_________________________________/ \____________________________________________________________________/ \____________________________________________/
             Header                                                 Payload                                                     Signature
```

### A. Header
Chứa loại token (`JWT`) và thuật toán ký mã hóa sử dụng (thường là `HS256` hoặc `RS256`):
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### B. Payload (Claims)
Chứa dữ liệu cần truyền tải (Không bao giờ để thông tin nhạy cảm như password vào đây vì ai cũng có thể giải mã Base64 để xem):
- **Registered Claims**: `sub` (Subject - username/id), `iat` (Issued At), `exp` (Expiration Time).
- **Custom Claims**: `role`, `userId`, `permissions`.
```json
{
  "sub": "user@example.com",
  "role": "ROLE_USER",
  "iat": 1690000000,
  "exp": 1690003600
}
```

### C. Signature (Chữ ký điện tử)
Được tạo ra bằng cách lấy:
$$\text{Signature} = \text{HMACSHA256}(\text{Base64Url}(\text{Header}) + "." + \text{Base64Url}(\text{Payload}), \text{SECRET\_KEY})$$
- Nếu kẻ tấn công thay đổi Payload (ví dụ: tự ý sửa `"role": "USER"` thành `"ADMIN"`), chữ ký sẽ không còn khớp với `SECRET_KEY` của Server -> Request bị từ chối ngay lập tức!

---

## 3. Quy trình Access Token & Refresh Token Flow

```mermaid
sequenceDiagram
    autonumber
    actor Client
    participant Server as Backend Server
    participant DB as Database

    Client->>Server: POST /auth/login (email, password)
    Server->>DB: Kiểm tra tài khoản & mật khẩu
    Server->>Client: Trả về Access Token (sống 15 phút) + Refresh Token (sống 7 ngày)
    
    Note over Client,Server: Client gửi request bình thường
    Client->>Server: GET /api/v1/orders (Header: Authorization: Bearer <Access_Token>)
    Server->>Client: 200 OK (Trả về danh sách đơn hàng)
    
    Note over Client,Server: Sau 15 phút, Access Token hết hạn
    Client->>Server: GET /api/v1/orders (Access Token đã hết hạn)
    Server->>Client: 401 Unauthorized (Token Expired)
    
    Client->>Server: POST /auth/refresh-token (Refresh Token)
    Server->>DB: Kiểm tra Refresh Token trong DB
    Server->>Client: Cấp Access Token mới (15 phút)
```

---

## 4. Cài đặt JWT Service với thư viện `jjwt`

Thêm dependency trong `pom.xml`:
```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

### Class `JwtService`:
```java
package com.example.app.security;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.security.Keys;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Service;

import java.security.Key;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

@Service
public class JwtService {

    @Value("${application.security.jwt.secret-key:404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970}")
    private String secretKey;

    @Value("${application.security.jwt.expiration:86400000}") // 1 ngày (ms)
    private long jwtExpiration;

    public String generateToken(UserDetails userDetails) {
        return generateToken(new HashMap<>(), userDetails);
    }

    public String generateToken(Map<String, Object> extraClaims, UserDetails userDetails) {
        return Jwts.builder()
                .setClaims(extraClaims)
                .setSubject(userDetails.getUsername())
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() + jwtExpiration))
                .signWith(getSignInKey(), SignatureAlgorithm.HS256)
                .compact();
    }

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public boolean isTokenValid(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);
    }

    private boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    private Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(getSignInKey())
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    private Key getSignInKey() {
        byte[] keyBytes = io.jsonwebtoken.io.Decoders.BASE64.decode(secretKey);
        return Keys.hmacShaKeyFor(keyBytes);
    }
}
```

---

## 5. Xây dựng `JwtAuthenticationFilter`

Bộ lọc này sẽ can thiệp vào từng request để trích xuất Header `Authorization: Bearer <token>`:

```java
package com.example.app.security;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.RequiredArgsConstructor;
import org.springframework.lang.NonNull;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtService jwtService;
    private final UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(
            @NonNull HttpServletRequest request,
            @NonNull HttpServletResponse response,
            @NonNull FilterChain filterChain
    ) throws ServletException, IOException {

        final String authHeader = request.getHeader("Authorization");
        final String jwt;
        final String userEmail;

        // 1. Kiểm tra header Authorization có chứa Bearer Token không
        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            filterChain.doFilter(request, response);
            return;
        }

        // 2. Cắt chuỗi lấy Token
        jwt = authHeader.substring(7);
        userEmail = jwtService.extractUsername(jwt);

        // 3. Nếu token hợp lệ và chưa được nạp vào SecurityContext
        if (userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);

            if (jwtService.isTokenValid(jwt, userDetails)) {
                UsernamePasswordAuthenticationToken authToken = new UsernamePasswordAuthenticationToken(
                        userDetails,
                        null,
                        userDetails.getAuthorities()
                );
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

                // 4. Lưu danh tính user vào SecurityContext cho request hiện tại
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        // 5. Chuyển tiếp request cho filter tiếp theo trong chuỗi
        filterChain.doFilter(request, response);
    }
}
```

### Đăng ký Filter vào `SecurityConfig`:
```java
http.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Cấu trúc 3 phần của JWT hoạt động thế nào? Ai có thể đọc được Payload?
Một JWT gồm 3 phần ngăn cách bởi dấu chấm `.` : `header.payload.signature`
1. **Header:** Chứa thuật toán ký (vd: `HS256`, `RS256`) và kiểu token (`JWT`), được mã hóa bằng Base64Url.
2. **Payload:** Chứa thông tin dữ liệu (Claims) như `sub` (userId), `email`, `roles`, `iat` (issued at), `exp` (expiration), cũng được mã hóa bằng Base64Url.
   > ⚠️ **CỰC KỲ QUAN TRỌNG:** Base64Url **KHÔNG PHẢI LÀ MÃ HÓA BẢO MẬT**, nó chỉ là định dạng nén chuỗi! Bất kỳ ai cầm JWT cũng có thể lên trang `jwt.io` giải mã và đọc được 100% nội dung bên trong Payload. Do đó: **TUYỆT ĐỐI KHÔNG BAO GIỜ lưu thông tin nhạy cảm (như mật khẩu, số thẻ tín dụng, số CCCD) vào trong Payload của JWT!**
3. **Signature (Chữ ký điện tử):** Được tạo ra bằng công thức:
   $$\text{Signature} = \text{HMACSHA256}(\text{base64(Header)} + "." + \text{base64(Payload)}, \ \text{SecretKey})$$
   Chữ ký này đảm bảo tính toàn vẹn. Nếu hacker sửa đổi bất kỳ ký tự nào trong Payload (ví dụ sửa role từ `USER` thành `ADMIN`), khi Server dùng SecretKey để tính lại chữ ký sẽ thấy lệch ngay lập tức và từ chối token.

### 4.2. Access Token vs Refresh Token? Vì sao bắt buộc phải dùng cả hai?
- **Access Token:**
  - Thời hạn sống **rất ngắn (15 - 30 phút)**.
  - Gửi kèm trong mọi request gọi API.
  - Nếu bị hacker nghe lén (sniff) đánh cắp, thiệt hại chỉ tồn tại tối đa trong 15-30 phút là token tự hết hạn.
- **Refresh Token:**
  - Thời hạn sống **dài (7 ngày - 30 ngày)**.
  - Lưu an toàn trong Database hoặc HttpOnly Cookie, **chỉ gửi lên duy nhất endpoint `/auth/refresh-token`** khi Access Token đã hết hạn.
- **Tại sao cần cả hai:**
  - Nếu chỉ dùng 1 token sống lâu (30 ngày): Quá nguy hiểm khi bị lộ.
  - Nếu chỉ dùng 1 token sống ngắn (15 phút): Trải nghiệm người dùng cực tệ vì cứ 15 phút lại bị văng ra bắt đăng nhập lại từ đầu.
  - **Sự kết hợp:** Người dùng vừa an toàn tối đa (Access Token hết hạn nhanh) mà vừa có trải nghiệm mượt mà không bị ngắt quãng (Refresh Token âm thầm xin cấp Access Token mới ngầm dưới background).

### 4.3. Làm sao để thu hồi (Revoke / Blacklist / Logout) một JWT khi nó chưa hết hạn?
Vì JWT là Stateless (Server không lưu trạng thái), khi người dùng bấm "Đăng xuất" hoặc "Đổi mật khẩu", token cũ trên máy client vẫn còn hạn và vẫn có thể dùng được. 
- **3 Giải pháp chuẩn thực tế:**
  1. **Dùng Redis Token Blacklist:** Khi user Logout, lấy `jti` (JWT ID) hoặc chuỗi token đó lưu vào Redis với thời gian hết hạn đúng bằng thời gian còn lại của token (`TTL = exp - now`). Tại `JwtAuthenticationFilter`, kiểm tra nếu token có trong Redis Blacklist $\rightarrow$ Chặn ngay `401`. Sau khi token hết hạn, Redis tự động giải phóng RAM.
  2. **Token Rotation với Refresh Token:** Mỗi lần dùng Refresh Token để lấy cặp token mới, Refresh Token cũ sẽ bị vô hiệu hóa ngay lập tức. Nếu phát hiện Refresh Token cũ bị dùng lại $\rightarrow$ Cảnh báo tài khoản bị tấn công và hủy toàn bộ các phiên đăng nhập của user đó.
  3. **Lưu `token_version` trong Database:** Bảng `users` lưu cột `token_version = 1`. Đưa số `1` vào claims của JWT. Khi user đổi mật khẩu hoặc bấm đăng xuất khỏi mọi thiết bị $\rightarrow$ Tăng `token_version` trong DB lên `2`. Các token cũ mang version `1` sẽ tự động bị coi là không hợp lệ khi kiểm tra.

---
*Thực hành:* Viết API `POST /auth/refresh-token` nhận Refresh Token, kiểm tra trong DB và cấp lại Access Token mới.

# Chapter 01: HTTP Fundamentals – Request, Response, Headers, Cookies

## 1. Giao thức HTTP
- **HTTP** (HyperText Transfer Protocol) là giao thức truyền tải dữ liệu giữa Client và Server trên nền TCP.
- Đặc tính: **Stateless** (mỗi request độc lập, server không nhớ request trước).

## 2. Cấu trúc HTTP Request
```
POST /api/v1/users HTTP/1.1          ← Request Line (Method + URL + Version)
Host: api.example.com                 ← Headers
Content-Type: application/json
Authorization: Bearer eyJhbG...
Content-Length: 85

{                                     ← Body (payload)
  "name": "An",
  "email": "an@gmail.com"
}
```

| Thành phần | Mô tả |
|-----------|-------|
| **Request Line** | Method (GET/POST...) + URL + HTTP version |
| **Headers** | Metadata: Content-Type, Authorization, Accept, Cookie... |
| **Body** | Dữ liệu gửi kèm (POST, PUT, PATCH). GET thường không có body |

## 3. Cấu trúc HTTP Response
```
HTTP/1.1 200 OK                       ← Status Line
Content-Type: application/json
Set-Cookie: sessionId=abc123

{                                     ← Response Body
  "status": 200,
  "data": {"id": 1, "name": "An"}
}
```

## 4. Headers quan trọng
| Header | Mô tả |
|--------|-------|
| `Content-Type` | Định dạng body: `application/json`, `text/html`, `multipart/form-data` |
| `Accept` | Client muốn nhận định dạng nào |
| `Authorization` | Token xác thực: `Bearer <jwt>` |
| `Cookie` / `Set-Cookie` | Quản lý session/cookie |
| `Cache-Control` | Chính sách cache |
| `X-Request-Id` | Tracking ID cho logging |

## 5. Cookie & Session
- **Cookie**: Server gửi `Set-Cookie` → Browser tự động gửi kèm trong mọi request sau.
- **Session**: Server lưu trạng thái người dùng (Stateful, ít dùng cho REST API).
- **Token (JWT)**: Stateless, client gửi trong header `Authorization: Bearer <token>` (phổ biến cho REST API).

## 6. HTTP/1.1 vs HTTP/2 vs HTTP/3
| | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---------|--------|--------|
| Multiplexing | ❌ 1 request/connection | ✅ Nhiều request/connection | ✅ |
| Header compression | ❌ | ✅ HPACK | ✅ QPACK |
| Protocol | TCP | TCP | **QUIC (UDP)** |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. HTTP là Stateless nghĩa là gì? Làm sao để duy trì trạng thái đăng nhập?
- **HTTP là Stateless (Phi trạng thái):** Mỗi một HTTP request được gửi đi là hoàn toàn độc lập và cô lập. Máy chủ không hề lưu giữ ký ức hay biết được request hiện tại có liên quan gì đến request trước đó hay không.
- **Cách duy trì trạng thái đăng nhập:**
  1. **Session-based (Stateful):** Khi login thành công, Server tạo một Session Object trong RAM/Redis với `sessionId` ngẫu nhiên. Server trả `Set-Cookie: JSESSIONID=xyz` về Browser. Các lần gọi sau Browser tự gửi cookie này lên để Server đối chiếu.
  2. **Token-based (Stateless - Chuẩn của REST API hiện đại):** Khi login thành công, Server cấp một **JWT (JSON Web Token)** tự chứa đầy đủ thông tin (UserId, Roles, Expiration). Client lưu vào `localStorage` hoặc Secure Cookie và tự đính kèm header `Authorization: Bearer <token>` trong mỗi request. Server chỉ cần xác thực chữ ký (Signature) mà không cần query Session trong RAM.

### 7.2. Phân biệt Cookie, Session, và JWT Token
| Tiêu chí | Cookie | Session | JWT Token |
| :--- | :--- | :--- | :--- |
| **Nơi lưu trữ** | Trình duyệt Client (Browser Storage). | Máy chủ Server (RAM, Redis, DB). | Client lưu (LocalStorage/Memory/Cookie). |
| **Bản chất dữ liệu** | Đoạn text nhỏ ($\le 4\text{KB}$) tự động gửi kèm mỗi HTTP request. | Đối tượng dữ liệu lớn chứa trạng thái người dùng trên Server. | Chuỗi mã hóa (Base64Url) có chữ ký số mật mã (Signature). |
| **Mở rộng máy chủ (Scaling)** | Không ảnh hưởng Server. | **Khó scale ngang**: Cần Sticky Session hoặc phân tán Redis Cluster. | **Cực dễ scale ngang**: Bất kỳ máy chủ nào có Secret Key đều tự giải mã được. |
| **Bảo mật** | Dễ bị tấn công CSRF và XSS nếu không đặt cờ `HttpOnly` và `SameSite`. | An toàn hơn vì dữ liệu nằm ở Server, chỉ lộ SessionID. | Dễ lộ nếu lưu ở `localStorage` (XSS), không thu hồi token sớm được nếu không có Blacklist. |

### 7.3. `application/json` vs `application/x-www-form-urlencoded` khi nào dùng?
- **`application/x-www-form-urlencoded`:**
  - Dữ liệu được mã hóa thành chuỗi Key-Value nối nhau bằng dấu `&` và `=`: `name=Nguyen+Van+A&age=25`.
  - Thường dùng cho các form HTML truyền thống gửi trực tiếp từ trình duyệt, hoặc luồng OAuth2 Authorization Code / Token exchange (`/oauth/token`).
- **`application/json`:**
  - Dữ liệu ở định dạng JSON có cấu trúc phức tạp: mảng lồng nhau, object lồng object, kiểu dữ liệu boolean, number rõ ràng.
  - **Là chuẩn số 1 tuyệt đối cho các RESTful API hiện đại**, giao tiếp giữa Frontend (React/Vue/Flutter) với Backend (Spring Boot).

---
*Thực hành:* Dùng Postman hoặc cURL gửi cả 2 loại `Content-Type` để quan sát sự khác nhau trong Request Body.

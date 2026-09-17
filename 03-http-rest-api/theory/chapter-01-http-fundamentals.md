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

## 7. Câu hỏi phỏng vấn
1. HTTP là Stateless nghĩa là gì? Làm sao duy trì trạng thái đăng nhập?
2. Phân biệt Cookie, Session, JWT Token.
3. `Content-Type: application/json` vs `application/x-www-form-urlencoded` khi nào dùng?

---

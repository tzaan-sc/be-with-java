# Chapter 02: HTTP Methods & Status Codes

## 1. HTTP Methods

| Method | Mục đích | Idempotent? | Có Body? |
|--------|---------|-------------|----------|
| `GET` | Đọc / Lấy dữ liệu | ✅ | ❌ |
| `POST` | Tạo mới resource | ❌ | ✅ |
| `PUT` | Thay thế **toàn bộ** resource | ✅ | ✅ |
| `PATCH` | Cập nhật **một phần** resource | ❌ | ✅ |
| `DELETE` | Xoá resource | ✅ | ❌ thường |

### Idempotency (Tính bất biến)
> Gọi 1 lần hay gọi 10 lần, **kết quả hệ thống** vẫn như nhau.
- `GET /users/1` → luôn trả về User#1.
- `PUT /users/1 {name:"An"}` → User#1 luôn là "An".
- `DELETE /users/1` → User#1 luôn bị xoá (gọi lại trả 404).
- `POST /users` → **KHÔNG** idempotent: mỗi lần gọi tạo 1 user mới!

### PUT vs PATCH
```json
// PUT: Thay thế TOÀN BỘ (field không gửi sẽ bị null/default)
PUT /api/v1/users/1
{ "name": "An Updated", "email": "an@new.com", "age": 26 }

// PATCH: Chỉ cập nhật PHẦN gửi lên
PATCH /api/v1/users/1
{ "email": "an@new.com" }  // chỉ đổi email, name và age giữ nguyên
```

## 2. HTTP Status Codes

### 2xx – Success
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `200` | OK | GET, PUT, PATCH thành công |
| `201` | Created | POST tạo mới thành công |
| `204` | No Content | DELETE thành công (không trả body) |

### 4xx – Client Error
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `400` | Bad Request | Dữ liệu gửi lên sai format, validation fail |
| `401` | Unauthorized | **Chưa xác thực** (chưa đăng nhập, token hết hạn) |
| `403` | Forbidden | **Đã xác thực** nhưng không đủ quyền |
| `404` | Not Found | Resource không tồn tại |
| `405` | Method Not Allowed | Sai HTTP method |
| `409` | Conflict | Trùng dữ liệu (duplicate email) |
| `422` | Unprocessable Entity | Dữ liệu đúng format nhưng sai logic |
| `429` | Too Many Requests | Rate limiting |

> 🔴 **401 vs 403:** 401 = "Bạn là ai?" (chưa login). 403 = "Biết bạn rồi nhưng không có quyền".

### 5xx – Server Error
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `500` | Internal Server Error | Bug code, exception không bắt |
| `502` | Bad Gateway | Reverse proxy không kết nối được backend |
| `503` | Service Unavailable | Server quá tải hoặc đang bảo trì |

## 3. Câu hỏi phỏng vấn
1. PUT và PATCH khác nhau thế nào? Cho ví dụ.
2. Idempotency là gì? Những method nào idempotent?
3. Phân biệt 401 và 403.
4. Khi nào dùng 200, khi nào 201, khi nào 204?

---

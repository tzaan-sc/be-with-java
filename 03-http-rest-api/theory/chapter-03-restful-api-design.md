# Chapter 03: Quy chuẩn thiết kế RESTful API

## 1. REST là gì?
- **RE**presentational **S**tate **T**ransfer – kiến trúc thiết kế API dựa trên **resource** (tài nguyên).
- 6 ràng buộc: Client-Server, Stateless, Cacheable, Uniform Interface, Layered System, Code on Demand (optional).

## 2. Quy tắc đặt tên URL (Resource Naming)

### ✅ Đúng chuẩn
```
GET    /api/v1/users              → Lấy danh sách users
GET    /api/v1/users/1            → Lấy user có id=1
POST   /api/v1/users              → Tạo user mới
PUT    /api/v1/users/1            → Cập nhật toàn bộ user id=1
PATCH  /api/v1/users/1            → Cập nhật 1 phần user id=1
DELETE /api/v1/users/1            → Xoá user id=1
```

### ❌ Sai chuẩn
```
GET /api/v1/getUser?id=1          → Dùng động từ trong URL
GET /api/v1/User/1                → Viết hoa
POST /api/v1/create-user          → Động từ + kebab-case
GET /api/v1/user/1                → Số ít (nên số nhiều)
```

### Quy tắc vàng
| Quy tắc | Ví dụ |
|---------|-------|
| URL dùng **danh từ số nhiều** | `/users`, `/products`, `/orders` |
| Chữ **thường**, phân cách bằng `-` (kebab-case) | `/order-items` |
| Quan hệ cha-con qua URL lồng | `/users/{userId}/orders/{orderId}` |
| Hành động dùng **HTTP method**, KHÔNG đặt trong URL | `POST /users` thay vì `POST /createUser` |
| Versioning | `/api/v1/...`, `/api/v2/...` |

## 3. Query Parameters (Phân trang, Tìm kiếm, Lọc)
```
GET /api/v1/products?page=0&size=20&sort=price,desc&category=electronics&keyword=iphone
```

| Param | Mục đích |
|-------|---------|
| `page`, `size` | Phân trang |
| `sort` | Sắp xếp (`price,desc` hoặc `name,asc`) |
| `category`, `status` | Lọc theo trường |
| `keyword`, `q` | Tìm kiếm full-text |

### Path Variable vs Query Param
- **Path Variable** `/users/{id}`: Định danh resource cụ thể (bắt buộc).
- **Query Param** `/users?status=active`: Lọc, phân trang, tuỳ chọn.

## 4. Cấu trúc Response chuẩn

### Thành công
```json
{
  "status": 200,
  "message": "Lấy danh sách thành công",
  "data": [ { "id": 1, "name": "An" } ],
  "timestamp": "2026-09-17T10:00:00"
}
```

### Lỗi
```json
{
  "status": 400,
  "message": "Validation failed",
  "errors": [
    { "field": "email", "message": "Email không hợp lệ" },
    { "field": "name", "message": "Tên không được để trống" }
  ],
  "timestamp": "2026-09-17T10:00:00"
}
```

### Phân trang
```json
{
  "status": 200,
  "data": { "content": [...], "pageNo": 0, "pageSize": 20, "totalElements": 150, "totalPages": 8, "last": false },
  "timestamp": "2026-09-17T10:00:00"
}
```

## 5. Câu hỏi phỏng vấn
1. RESTful API là gì? Kể 3 ràng buộc quan trọng nhất.
2. Tại sao URL dùng danh từ số nhiều?
3. Khi nào dùng Path Variable, khi nào dùng Query Param?
4. Thiết kế API CRUD cho hệ thống quản lý đơn hàng (orders có order-items).

---

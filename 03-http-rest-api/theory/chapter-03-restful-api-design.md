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

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. RESTful API là gì? Kể 3 ràng buộc kiến trúc quan trọng nhất
- **RESTful API:** Là API tuân thủ theo phong cách kiến trúc **REST (Representational State Transfer)** do Roy Fielding đề xuất năm 2000, lấy **Tài nguyên (Resources)** làm trung tâm và tận dụng tối đa các chuẩn sẵn có của giao thức HTTP.
- **3 Ràng buộc kiến trúc quan trọng nhất:**
  1. **Stateless (Phi trạng thái):** Server không lưu phiên làm việc (Session) của client. Mỗi request phải tự chứa đủ thông tin để server hiểu và xác thực (Token).
  2. **Client-Server Architecture:** Tách biệt hoàn toàn giữa giao diện người dùng (Client) và logic xử lý/lưu trữ dữ liệu (Server), giúp hai bên phát triển và scale độc lập.
  3. **Cacheable (Khả năng lưu bộ đệm):** Response phải tự định nghĩa rõ ràng nó có được phép cache hay không (qua header `Cache-Control`, `ETag`) để client hoặc proxy trung gian tái sử dụng, giảm tải cho server.

### 5.2. Tại sao URL trong REST API nên dùng danh từ số nhiều (Plural Nouns)?
- **Nguyên tắc cốt lõi:** Endpoint URL dùng để **định danh tài nguyên**, còn hành động làm gì với tài nguyên đó được thể hiện bằng **HTTP Method**:
  - ❌ *Thiết kế xấu (RPC style):* `GET /getUser`, `POST /createUser`, `POST /deleteUser`
  - ✅ *Thiết kế chuẩn REST:* `GET /users`, `POST /users`, `DELETE /users/1`
- **Lý do dùng số nhiều (`/users`):**
  - Đồng nhất và trực quan: `/users` đại diện cho "tập hợp người dùng".
  - `GET /users`: Lấy danh sách cả tập hợp.
  - `POST /users`: Thêm 1 phần tử mới vào tập hợp đó.
  - `GET /users/123`: Lấy 1 phần tử cụ thể có ID 123 ra khỏi tập hợp.

### 5.3. Khi nào dùng Path Variable, khi nào dùng Query Parameter?
| Tiêu chí | Path Variable (`/users/{id}`) | Query Parameter (`/users?role=ADMIN&page=1`) |
| :--- | :--- | :--- |
| **Vị trí** | Nằm trực tiếp trong đường dẫn URL. | Nằm sau dấu chấm hỏi `?` dạng Key=Value. |
| **Mục đích** | Dùng để **định danh tài nguyên bắt buộc duy nhất** (Identity). Không thể thiếu nó để tìm đúng đối tượng. | Dùng để **lọc (filter), tìm kiếm (search), sắp xếp (sort), hoặc phân trang (pagination)**. |
| **Ví dụ** | `GET /orders/105` (Xem đơn hàng số 105), `DELETE /products/42`. | `GET /products?category=laptop&sort=price,desc&page=0&size=20`. |

### 5.4. Thiết kế API CRUD chuẩn REST cho hệ thống Quản lý Đơn hàng (Orders & Items)
```http
# 1. Quản lý Đơn hàng (Orders)
GET    /api/v1/orders                 -> Lấy danh sách đơn hàng (hỗ trợ phân trang ?page=0&size=10)
POST   /api/v1/orders                 -> Tạo đơn hàng mới
GET    /api/v1/orders/{orderId}       -> Xem chi tiết đơn hàng theo ID
PUT    /api/v1/orders/{orderId}       -> Cập nhật toàn bộ đơn hàng
PATCH  /api/v1/orders/{orderId}       -> Cập nhật trạng thái đơn (vd: đổi sang DELIVERED)
DELETE /api/v1/orders/{orderId}       -> Hủy / Xóa đơn hàng

# 2. Quản lý Sản phẩm con bên trong Đơn hàng (Nested Sub-resources)
GET    /api/v1/orders/{orderId}/items           -> Lấy danh sách các món hàng trong đơn
POST   /api/v1/orders/{orderId}/items           -> Thêm 1 món hàng mới vào đơn
DELETE /api/v1/orders/{orderId}/items/{itemId}  -> Xóa món hàng cụ thể khỏi đơn
```

---
*Thực hành:* Viết danh sách URL cho hệ thống quản lý Blog (posts, comments, tags) tuân thủ 100% chuẩn RESTful.

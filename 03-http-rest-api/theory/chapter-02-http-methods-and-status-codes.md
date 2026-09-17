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

## 3. Câu hỏi phỏng vấn & Trả lời chi tiết

### 3.1. PUT và PATCH khác nhau thế nào? Cho ví dụ
- **`PUT` (Thay thế toàn bộ tài nguyên - Complete Replacement):**
  - Client gửi lên **toàn bộ dữ liệu của đối tượng**. Những trường nào không gửi lên sẽ bị coi là mang giá trị `null` hoặc bị ghi đè thành mặc định.
  - *Ví dụ:* User có `{id: 1, name: "An", email: "an@gmail.com", role: "USER"}`.
    Nếu gửi `PUT /users/1` với body `{"name": "Bình"}` $\rightarrow$ User sau khi cập nhật sẽ bị mất email hoặc email thành `null`.
- **`PATCH` (Cập nhật một phần - Partial Modification):**
  - Client chỉ gửi **duy nhất những trường thông tin cần thay đổi**. Các trường dữ liệu khác giữ nguyên vẹn.
  - *Ví dụ:* Gửi `PATCH /users/1` với body `{"name": "Bình"}` $\rightarrow$ Chỉ có `name` đổi thành `"Bình"`, trường `email` và `role` vẫn giữ nguyên.

### 3.2. Idempotency (Tính bất biến / Tính lũy đẳng) là gì? Những method nào Idempotent?
- **Định nghĩa:** Một HTTP method được coi là **Idempotent** nếu việc bạn **thực hiện request đó 1 lần hay 100 lần liên tiếp** thì trạng thái của tài nguyên trên Server **vẫn mang lại cùng một kết quả cuối cùng hệt như nhau** (không gây tác dụng phụ - side effect phụ thêm).
- **Phân loại:**
  - **`GET`, `HEAD`, `OPTIONS`:** Vừa Idempotent vừa **Safe** (chỉ đọc dữ liệu, không làm biến đổi DB).
  - **`PUT`:** **Idempotent** (ghi đè toàn bộ tài nguyên, gửi 10 lần cùng nội dung thì bản ghi trên DB vẫn mang trạng thái đó).
  - **`DELETE`:** **Idempotent** (gọi xóa ID=5 lần đầu thì bản ghi bị xóa, các lần sau gọi lại thì bản ghi vẫn ở trạng thái đã xóa, không làm mất thêm dữ liệu khác).
  - **`POST`:** **KHÔNG Idempotent (Non-idempotent)** (mỗi lần bấm Submit gửi `POST /orders`, hệ thống sẽ tạo thêm 1 đơn hàng mới, gây duplicate đơn hàng).

### 3.3. Phân biệt 401 Unauthorized và 403 Forbidden
- **`401 Unauthorized` (Lỗi Xác thực - Authentication):**
  - Ý nghĩa: *"Bạn là ai? Tôi chưa biết bạn!"*
  - Nguyên nhân: Client chưa gửi token, gửi token sai định dạng, hoặc token đã hết hạn.
  - Cách khắc phục: Yêu cầu người dùng đăng nhập lại để lấy Token hợp lệ.
- **`403 Forbidden` (Lỗi Phân quyền - Authorization):**
  - Ý nghĩa: *"Tôi biết rõ bạn là ai rồi (bạn là User thường), nhưng bạn KHÔNG CÓ QUYỀN động vào tài nguyên này!"*
  - Nguyên nhân: Người dùng đã đăng nhập thành công, nhưng tài khoản không có quyền tương ứng (ví dụ: User thường cố tình gọi API xóa tài khoản của Admin).

### 3.4. Khi nào dùng 200, 201, 204?
- **`200 OK`:** Yêu cầu thành công và Server **có trả về dữ liệu** trong Response Body. Dùng cho hầu hết các request `GET`, `PUT`, `PATCH` thành công.
- **`201 Created`:** Yêu cầu thành công và **một tài nguyên mới vừa được khởi tạo** trong Database. Dùng cho `POST` tạo User, tạo Đơn hàng (kèm header `Location: /api/v1/orders/123`).
- **`204 No Content`:** Yêu cầu thành công nhưng Server **cố tình không trả về dữ liệu gì** trong Response Body. Rất phổ biến khi thực hiện `DELETE /users/1` thành công, hoặc cập nhật nhanh không cần trả về entity.

---
*Thực hành:* Mở Chrome DevTools kiểm tra status code của các thao tác Đăng nhập, Xem bài viết, Xóa bài viết.

# 🛠 Bài Tập – Phase 3: HTTP & REST API (Ngày 43–54)

---

### Bài 1 – Phân tích HTTP Request/Response *(~10p)*
[ ] Mở Chrome DevTools (F12) → Network → truy cập `https://jsonplaceholder.typicode.com/posts/1`. Ghi lại: Method, URL, Status Code, Content-Type, Response Body.

### Bài 2 – Phân biệt HTTP Methods *(~10p)*
[ ] Điền bảng: Method nào dùng cho tạo mới? Cập nhật toàn bộ? Cập nhật 1 phần? Xoá? Method nào idempotent?

### Bài 3 – Thiết kế RESTful API *(~15p)*
[ ] Thiết kế bộ API CRUD cho hệ thống Blog gồm `Post` và `Comment`:
```
GET    /api/v1/posts
POST   /api/v1/posts
GET    /api/v1/posts/{postId}
PUT    /api/v1/posts/{postId}
DELETE /api/v1/posts/{postId}
GET    /api/v1/posts/{postId}/comments
POST   /api/v1/posts/{postId}/comments
...
```
[ ] Thiết kế URL phân trang: `GET /api/v1/posts?page=___&size=___&sort=___`

### Bài 4 – Viết JSON Response chuẩn *(~10p)*
[ ] Viết mẫu JSON response cho: thành công (200 + data), lỗi validation (400 + errors), resource not found (404).

### Bài 5 – Thực hành Postman *(~15p)*
[ ] Cài Postman, tạo Collection "Learn-API", tạo Environment với `base_url = https://jsonplaceholder.typicode.com`.
[ ] Tạo 3 request: GET `/posts`, GET `/posts/1`, POST `/posts` với JSON body.
[ ] Viết test script kiểm tra status 200 và response có chứa field `id`.

### Bài 6 – Thực hành cURL *(~10p)*
[ ] Chạy các lệnh cURL trong terminal:
```bash
curl https://jsonplaceholder.typicode.com/users/1
curl -I https://google.com
curl -X POST https://jsonplaceholder.typicode.com/posts -H "Content-Type: application/json" -d "{\"title\":\"Test\",\"body\":\"Hello\"}"
```

### Bài 7 – Quiz 401 vs 403 *(~5p)*
[ ] Trường hợp nào trả 401? Trường hợp nào trả 403?
- User chưa đăng nhập gọi API → ____
- User đã đăng nhập nhưng role là USER, gọi API chỉ dành cho ADMIN → ____

---
*Hoàn thành = sẵn sàng Phase 4: Spring Boot Core! 🚀*

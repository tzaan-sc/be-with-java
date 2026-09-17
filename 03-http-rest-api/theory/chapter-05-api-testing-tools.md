# Chapter 05: API Testing Tools – Postman & cURL

## 1. Postman
### Tạo Collections & Environments
- **Collection**: Nhóm các request theo project/module (`User API`, `Product API`).
- **Environment**: Lưu biến chung (`{{base_url}}` = `http://localhost:8080`).

### Tạo Request
```
Method: POST
URL: {{base_url}}/api/v1/users
Headers: Content-Type: application/json
Body (raw JSON):
{
  "name": "An",
  "email": "an@gmail.com"
}
```

### Test Script (tab Tests)
```javascript
pm.test("Status 201 Created", () => {
    pm.response.to.have.status(201);
});
pm.test("Response has id", () => {
    const body = pm.response.json();
    pm.expect(body.data.id).to.be.a("number");
});
// Lưu token vào biến environment
const token = pm.response.json().data.token;
pm.environment.set("jwt_token", token);
```

### Sử dụng biến token
```
Headers: Authorization: Bearer {{jwt_token}}
```

## 2. cURL (Command Line)
```bash
# GET
curl https://jsonplaceholder.typicode.com/posts/1

# GET với headers
curl -H "Authorization: Bearer <token>" http://localhost:8080/api/v1/users

# POST với JSON body
curl -X POST http://localhost:8080/api/v1/users \
  -H "Content-Type: application/json" \
  -d '{"name":"An","email":"an@gmail.com"}'

# PUT
curl -X PUT http://localhost:8080/api/v1/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"An Updated","email":"an@new.com"}'

# DELETE
curl -X DELETE http://localhost:8080/api/v1/users/1

# Xem headers response
curl -I https://google.com

# Verbose (xem chi tiết kết nối)
curl -v http://localhost:8080/api/v1/health
```

## 3. Câu hỏi phỏng vấn & Trả lời chi tiết

### 3.1. Bạn dùng công cụ gì để test API? Mô tả quy trình test 1 endpoint thực tế
- **Công cụ thường dùng:** **Postman** (giao diện trực quan, quản lý Collection/Environment, viết script test tự động), **cURL** (test nhanh trên terminal hoặc server Linux), và **Swagger/OpenAPI UI** (tài liệu hóa và test trực tiếp trên trình duyệt).
- **Quy trình chuẩn để test một Endpoint mới (ví dụ: `POST /api/v1/orders`):**
  1. **Kiểm thử trường hợp thành công (Happy Path):**
     - Gửi đúng Header `Authorization: Bearer <valid_token>` và Body JSON hợp lệ.
     - Kỳ vọng: Status Code `201 Created`, body trả về `orderId`, dữ liệu trong Database được lưu chính xác, tồn kho sản phẩm bị trừ tương ứng.
  2. **Kiểm thử xác thực & phân quyền (Auth & Permissions):**
     - Gửi request không có token $\rightarrow$ Phải trả về `401 Unauthorized`.
     - Dùng token của User thường gọi API chỉ dành cho Admin $\rightarrow$ Phải trả về `403 Forbidden`.
  3. **Kiểm thử dữ liệu đầu vào (Validation & Negative Testing):**
     - Bỏ trống các trường bắt buộc, gửi sai định dạng email, số tiền âm, ID không tồn tại.
     - Kỳ vọng: Status Code `400 Bad Request` kèm mảng lỗi chi tiết (`errors: [{field: "...", message: "..."}]`).
  4. **Kiểm thử ngoại lệ & trùng lặp (Edge cases & Idempotency):**
     - Bấm đặt hàng 2 lần liên tiếp thật nhanh $\rightarrow$ Kiểm tra hệ thống có bị duplicate đơn hàng không (chống double-spend).
     - Đặt hàng vượt quá số lượng hàng tồn kho $\rightarrow$ Phải trả về `400` hoặc `409 Conflict`.

### 3.2. Làm sao tự động hoá test API trong Postman? (Postman Tests & Newman CLI)
- **Viết Test Scripts trong tab "Tests" của Postman:**
  Sử dụng cú pháp JavaScript của thư viện Chai Assertion được tích hợp sẵn:
  ```javascript
  // 1. Kiểm tra Status Code
  pm.test("Status code is 201 Created", function () {
      pm.response.to.have.status(201);
  });

  // 2. Kiểm tra thời gian phản hồi (Latency SLA)
  pm.test("Response time is less than 500ms", function () {
      pm.expect(pm.response.responseTime).to.be.below(500);
  });

  // 3. Kiểm tra cấu trúc dữ liệu JSON trả về
  pm.test("Response has orderId and status", function () {
      const res = pm.response.json();
      pm.expect(res.data).to.have.property("orderId");
      pm.expect(res.data.status).to.eql("PENDING");
  });

  // 4. Trích xuất biến dùng cho request kế tiếp (Chaining API)
  const orderId = pm.response.json().data.orderId;
  pm.environment.set("current_order_id", orderId);
  ```
- **Chạy tự động trong CI/CD bằng Newman CLI:**
  - Export Postman Collection và Environment ra file `.json`.
  - Chạy lệnh: `newman run my_collection.json -e my_env.json --reporters cli,junit`
  - Nhúng lệnh này vào GitHub Actions / GitLab CI để tự động test toàn bộ API mỗi khi developer push code mới lên repository.

---
*Thực hành:* Tạo Postman Collection gồm 3 request: Login -> Lấy Token -> Tạo Order dùng Token đó.

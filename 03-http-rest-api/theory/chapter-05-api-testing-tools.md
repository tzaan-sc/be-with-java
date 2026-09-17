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

## 3. Câu hỏi phỏng vấn
1. Bạn dùng công cụ gì để test API? Mô tả quy trình test 1 endpoint.
2. Làm sao tự động hoá test API trong Postman?

---

# 🛠 Bài Tập – Phase 4: Spring Boot Core (Ngày 55–72)

---

### Bài 1 – Khởi tạo dự án *(~15p)*
[ ] Truy cập `start.spring.io`, tạo dự án Spring Boot 3.x (Java 17+, Maven, Spring Web, Lombok, Validation). Import vào IDE, chạy `main()`.

### Bài 2 – IoC & DI *(~15p)*
[ ] Tạo `interface GreetingService` → `VietnameseGreeting` và `EnglishGreeting` implements. Inject vào Controller bằng Constructor Injection. Dùng `@Qualifier` chọn Bean.

### Bài 3 – REST Controller CRUD *(~30p)*
[ ] Tạo `UserController` với 5 endpoints CRUD (`GET all`, `GET by id`, `POST`, `PUT`, `DELETE`). Lưu tạm trong `List<User>` (In-Memory). Test bằng Postman.

### Bài 4 – DTO & Validation *(~20p)*
[ ] Tạo `UserRequestDto` với validation (`@NotBlank`, `@Email`, `@Size`, `@Min`). Thêm `@Valid` trong Controller. Gửi dữ liệu sai format qua Postman để xem lỗi.

### Bài 5 – Global Exception Handler *(~20p)*
[ ] Tạo `ResourceNotFoundException`, `GlobalExceptionHandler`, `ErrorResponse`. Bắt lỗi 404 (Not Found) và 400 (Validation). Test trên Postman.

### Bài 6 – Cấu hình `application.yml` *(~10p)*
[ ] Đổi port sang 8081 trong `application.yml`. Tạo `@ConfigurationProperties` class đọc cấu hình custom `app.name` và `app.version`.

### Bài 7 – Tổ chức package chuẩn *(~15p)*
[ ] Tổ chức lại code theo package: `controller/`, `service/`, `service/impl/`, `repository/`, `model/dto/`, `model/entity/`, `exception/`, `config/`.

---
*Hoàn thành = sẵn sàng Phase 5: Database & JPA! 🚀*

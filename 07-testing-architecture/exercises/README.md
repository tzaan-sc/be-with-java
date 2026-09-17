# 🛠 Bài Tập Thực Hành – Phase 7: Testing, Architecture & Production Readiness

> Lộ trình Ngày 107 – Ngày 120 (20‑30 phút/ngày). Hoàn thiện kỹ năng chuyên nghiệp: Kiểm thử tự động, chuẩn hóa kiến trúc, tài liệu Swagger và đóng gói Docker container.

---

## Bài tập Ngày 107‑109: Unit Testing & Mockito *(Chapter 01 & 02)*

### Bài 1.1 – Viết Unit Test đầu tiên với JUnit 5 *(~20p)*
[ ] Thêm dependency `spring-boot-starter-test` (đã bao gồm JUnit 5 và Mockito).
[ ] Viết test class cho một Utility class (ví dụ: `FormatUtils.formatCurrency(BigDecimal amount)` hoặc `ValidatorUtils.isValidEmail(String email)`).
[ ] Áp dụng đúng mô hình AAA (Arrange - Act - Assert) và các assertion: `assertEquals()`, `assertTrue()`, `assertFalse()`.

### Bài 1.2 – Viết Unit Test tầng Service với Mockito *(~30p)*
[ ] Tạo test class `ProductServiceImplTest` sử dụng `@ExtendWith(MockitoExtension.class)`.
[ ] Giả lập `@Mock private ProductRepository productRepository;`.
[ ] Tiêm vào `@InjectMocks private ProductServiceImpl productService;`.
[ ] Viết 2 test case:
  - Case 1: Tìm thấy sản phẩm theo ID $\rightarrow$ Trả về `ProductResponseDto`, verify `productRepository.findById()` gọi đúng 1 lần.
  - Case 2: Không tìm thấy sản phẩm $\rightarrow$ Kiểm tra ném ra `ResourceNotFoundException`, verify không gọi hàm mapper.

---

## Bài tập Ngày 110: Integration Test Controller với `@WebMvcTest` *(Chapter 03)*

### Bài 2.1 – MockMvc Slice Testing *(~30p)*
[ ] Tạo `ProductControllerTest` với `@WebMvcTest(ProductController.class)`.
[ ] Sử dụng `@MockBean private ProductService productService;`.
[ ] Viết test gửi request giả lập:
```java
mockMvc.perform(get("/api/v1/products/1"))
       .andExpect(status().isOk())
       .andExpect(jsonPath("$.id").value(1))
       .andExpect(jsonPath("$.name").value("iPhone 15 Pro"));
```
[ ] Viết test case gửi body thiếu trường bắt buộc $\rightarrow$ kiểm chứng trả về `400 Bad Request`.

---

## Bài tập Ngày 111: Clean Architecture & Refactoring *(Chapter 04)*

### Bài 3.1 – Chuẩn hóa cấu trúc thư mục (Package by Feature) *(~25p)*
[ ] Sắp xếp lại mã nguồn thành các module tính năng độc lập: `modules/auth/`, `modules/product/`, `modules/order/`.
[ ] Tách các DTO riêng cho Request (`CreateProductRequest`, `UpdateProductRequest`) và Response (`ProductResponse`).

### Bài 3.2 – Áp dụng Strategy Pattern *(~20p)*
[ ] Tạo interface `PaymentStrategy` và triển khai 2 class: `VnPayStrategy` và `CodStrategy`.
[ ] Inject danh sách `List<PaymentStrategy>` vào `PaymentService` để tự động chọn cổng thanh toán theo lựa chọn của người dùng.

---

## Bài tập Ngày 112‑113: Tích hợp Swagger / OpenAPI 3 *(Chapter 05)*

### Bài 4.1 – Cài đặt `springdoc` & Kiểm tra Swagger UI *(~15p)*
[ ] Thêm dependency `springdoc-openapi-starter-webmvc-ui` vào `pom.xml`.
[ ] Khởi chạy app và truy cập `http://localhost:8080/swagger-ui/index.html`.
[ ] Kiểm tra các Controller đã tự động xuất hiện trên giao diện.

### Bài 4.2 – Bổ sung mô tả & Cấu hình nút Authorize JWT *(~25p)*
[ ] Tạo `OpenApiConfig` để kích hoạt nút `Authorize 🔓` (Bearer JWT).
[ ] Thêm `@Operation(summary = "...")` và `@ApiResponse` vào các Controller.
[ ] Lấy JWT Token từ API Login dán vào nút Authorize trên Swagger UI và gửi request test trực tiếp trên trình duyệt.

---

## Bài tập Ngày 114‑117: Đóng Gói Với Docker & Docker Compose *(Chapter 06)*

### Bài 5.1 – Viết Dockerfile Multi-stage & Build Image *(~30p)*
[ ] Tạo file `Dockerfile` tại thư mục gốc của project (áp dụng Multi-stage build với JDK và JRE Alpine).
[ ] Mở Terminal chạy lệnh:
```bash
docker build -t my-spring-backend:latest .
```
[ ] Kiểm tra kích thước image bằng `docker images` (đảm bảo dưới 200MB).

### Bài 5.2 – Khởi chạy hệ sinh thái bằng Docker Compose *(~30p)*
[ ] Tạo file `docker-compose.yml` gồm 2 dịch vụ: `backend-api` và `postgres-db`.
[ ] Chạy lệnh:
```bash
docker compose up -d
```
[ ] Kiểm tra trạng thái bằng `docker compose ps` và xem log ứng dụng bằng `docker compose logs -f`.
[ ] Mở trình duyệt truy cập `http://localhost:8080/swagger-ui/index.html` $\rightarrow$ Xác nhận ứng dụng kết nối DB và hoạt động hoàn hảo trong Docker!

---

## Bài tập Ngày 118‑120: Capstone Project & Hoàn Thiện Portfolio

### Bài 6.1 – Tự động hóa CI với GitHub Actions *(~25p)*
[ ] Tạo file `.github/workflows/maven.yml`:
```yaml
name: Java CI with Maven
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build with Maven
        run: mvn clean test
```
[ ] Push code lên GitHub và kiểm tra tab Actions xem quy trình chạy test tự động pass màu xanh.

### Bài 6.2 – Capstone Project & README Portfolio *(~30p)*
[ ] Hoàn thiện 1 dự án tổng thể (REST API E-Commerce / Booking / Blog) áp dụng trọn vẹn:
  - Spring Boot 3 + Spring Data JPA
  - PostgreSQL / MySQL Database
  - Spring Security + JWT Authentication & RBAC
  - Global Exception Handling & Validation
  - Swagger UI Documentation
  - Docker & Docker Compose deployment
[ ] Viết `README.md` giới thiệu dự án chuyên nghiệp: Kiến trúc, Tech-stack, Hướng dẫn chạy 1-click với Docker Compose.

---
🎉 **CHÚC MỪNG BẠN ĐÃ HOÀN THÀNH TOÀN BỘ CHƯƠNG TRÌNH JAVA BACKEND!**

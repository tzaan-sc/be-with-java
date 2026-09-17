# Chapter 05: Tự Động Tạo Tài Liệu API Với Swagger / OpenAPI 3 (springdoc)

---

## 1. OpenAPI 3 và Swagger là gì?

- **OpenAPI**: Là một quy chuẩn định dạng (Specification) mô tả các API RESTful theo chuẩn JSON hoặc YAML.
- **Swagger**: Là bộ công cụ triển khai OpenAPI, cung cấp giao diện trực quan (**Swagger UI**) giúp các lập trình viên Frontend, Mobile và Tester có thể:
  - Xem danh sách toàn bộ Endpoints của hệ thống.
  - Xem mô tả các trường dữ liệu Request Body, Query Params và Response JSON.
  - Thực thi gửi request và nhận kết quả trực tiếp ngay trên trình duyệt mà không cần dùng Postman.

---

## 2. Tích hợp `springdoc-openapi` vào Spring Boot 3.x

Trong Spring Boot 3.x, không dùng `springfox` (đã lỗi thời), ta sử dụng thư viện **`springdoc-openapi-starter-webmvc-ui`**:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.3.0</version>
</dependency>
```

Sau khi thêm dependency và chạy ứng dụng, truy cập vào đường dẫn:
👉 **`http://localhost:8080/swagger-ui/index.html`**

---

## 3. Cấu hình JWT Bearer Authorize Button

Để xuất hiện nút **Authorize 🔓** trên giao diện Swagger UI (cho phép dán JWT token và test các API có bảo mật), ta tạo class cấu hình `OpenApiConfig`:

```java
package com.example.app.config;

import io.swagger.v3.oas.models.Components;
import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Contact;
import io.swagger.v3.oas.models.info.Info;
import io.swagger.v3.oas.models.info.License;
import io.swagger.v3.oas.models.security.SecurityRequirement;
import io.swagger.v3.oas.models.security.SecurityScheme;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class OpenApiConfig {

    private static final String SECURITY_SCHEME_NAME = "BearerAuth";

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                // 1. Thông tin tổng quan hệ thống
                .info(new Info()
                        .title("E-Commerce Backend API")
                        .description("Tài liệu đặc tả hệ thống RESTful API xây dựng với Spring Boot 3 & Spring Security")
                        .version("v1.0.0")
                        .contact(new Contact().name("Đội ngũ Backend").email("backend@example.com"))
                        .license(new License().name("Apache 2.0").url("http://springdoc.org")))
                // 2. Yêu cầu Security toàn cục
                .addSecurityItem(new SecurityRequirement().addList(SECURITY_SCHEME_NAME))
                // 3. Định nghĩa cơ chế xác thực Bearer JWT
                .components(new Components()
                        .addSecuritySchemes(SECURITY_SCHEME_NAME, new SecurityScheme()
                                .name(SECURITY_SCHEME_NAME)
                                .type(SecurityScheme.Type.HTTP)
                                .scheme("bearer")
                                .bearerFormat("JWT")
                                .description("Nhập chuỗi JWT Token vào ô bên dưới (không cần gõ chữ 'Bearer ')")));
    }
}
```

---

## 4. Các Annotation mô tả chi tiết Endpoint

| Annotation | Vị trí đặt | Mục đích |
| :--- | :--- | :--- |
| `@Tag(name, description)` | Trên Controller class | Nhóm các API theo phân hệ (Ví dụ: `User Management`, `Order Management`). |
| `@Operation(summary, description)` | Trên Controller method | Tóm tắt chức năng và mô tả chi tiết luồng nghiệp vụ của endpoint. |
| `@ApiResponse(responseCode, description)` | Trên Controller method | Mô tả các mã HTTP trả về (200, 201, 400, 404, 500). |
| `@Schema(description, example)` | Trên trường của DTO | Mô tả ý nghĩa của trường dữ liệu và cung cấp giá trị ví dụ mẫu trên Swagger. |

### Ví dụ áp dụng thực tế:
```java
@Tag(name = "Product Management", description = "Quản lý danh mục và sản phẩm trong kho")
@RestController
@RequestMapping("/api/v1/products")
public class ProductController {

    @Operation(summary = "Lấy chi tiết sản phẩm theo ID", description = "Trả về thông tin chi tiết của sản phẩm bao gồm danh mục liên kết")
    @ApiResponses({
        @ApiResponse(responseCode = "200", description = "Lấy dữ liệu thành công"),
        @ApiResponse(responseCode = "404", description = "Không tìm thấy sản phẩm với ID cung cấp"),
        @ApiResponse(responseCode = "500", description = "Lỗi hệ thống nội bộ")
    })
    @GetMapping("/{id}")
    public ResponseEntity<ProductResponseDto> getById(
        @Parameter(description = "ID của sản phẩm cần lấy", example = "10")
        @PathVariable Long id
    ) {
        return ResponseEntity.ok(productService.getById(id));
    }
}
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Swagger vs OpenAPI Specification (OAS) khác nhau thế nào?
- **OpenAPI Specification (OAS):** Là một **Chuẩn đặc tả quốc tế độc lập (Open Standard)** do liên minh các tập đoàn công nghệ (Linux Foundation, Google, Microsoft) quản lý. Nó định nghĩa cấu trúc tài liệu mô tả REST API dưới dạng file JSON hoặc YAML.
- **Swagger:** Là **Bộ công cụ phần mềm thương mại / mã nguồn mở** (do SmartBear phát triển) dùng để hiện thực hóa chuẩn OpenAPI:
  - `Swagger UI`: Giao diện web tương tác trực quan cho phép gọi thử API trên trình duyệt.
  - `Swagger Editor`: Trình soạn thảo file OAS.
  - `Swagger Codegen`: Công cụ tự sinh code Client/Server từ file spec OAS.
- $\rightarrow$ **Tóm lại:** OpenAPI là bản thiết kế tiêu chuẩn, còn Swagger là công cụ phần mềm.

### 4.2. Code-First vs Design-First (Contract-First) trong thiết kế API: Nên chọn cái nào?
| Tiêu chí | Code-First (SpringDoc OpenAPI) | Design-First (Contract-First) |
| :--- | :--- | :--- |
| **Quy trình** | Backend viết code Java trước $\rightarrow$ Thư viện tự sinh ra file OpenAPI JSON và Swagger UI. | Viết file thiết kế `openapi.yaml` trước $\rightarrow$ Thống nhất giữa các đội $\rightarrow$ Sinh code Java và TypeScript. |
| **Ưu điểm** | **Cực nhanh, dễ làm**, tài liệu luôn khớp 100% với code thật, không tốn công cập nhật file spec bằng tay. | Đội Frontend và Backend có thể làm việc song song ngay từ ngày đầu tiên; làm "bản hợp đồng" chuẩn trước khi gõ code. |
| **Nhược điểm** | Frontend phải chờ Backend viết xong code mới có tài liệu để tích hợp. | Tốn nhiều thời gian ban đầu để viết file YAML/JSON thủ công. |
| **Khuyên dùng** | Rất phù hợp cho các dự án Startup, Agile/Scrum vừa và nhỏ, làm việc nhanh. | Bắt buộc cho các hệ sinh thái lớn, ngân hàng, viễn thông có hàng chục đội Microservices độc lập. |

### 4.3. Làm sao bảo vệ trang Swagger UI trên môi trường Production?
Trang Swagger UI phơi bày toàn bộ danh sách endpoint, tham số và cấu trúc Database của bạn cho công chúng. Trên Production, bạn phải bảo vệ bằng 1 trong 3 cách:
1. **Tắt hoàn toàn Swagger trên Production bằng Profile:**
   ```yaml
   # application-prod.yml
   springdoc:
     api-docs:
       enabled: false
     swagger-ui:
       enabled: false
   ```
2. **Khóa bằng Spring Security:** Chỉ cho phép người dùng có vai trò `ROLE_ADMIN` hoặc tài khoản nội bộ (Internal IP) mới được mở trang `/swagger-ui/**`.
3. **Đổi đường dẫn mặc định:** Đổi `/swagger-ui.html` thành một URL bí mật nội bộ bằng cấu hình `springdoc.swagger-ui.path=/internal-secret-docs`.

---
*Thực hành:* Tích hợp dependency `springdoc-openapi-starter-webmvc-ui`, cấu hình nút Authorize nhập Bearer Token và mở `/swagger-ui/index.html` gọi thử API.

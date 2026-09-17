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

# Chapter 06: Containerization – Đóng Gói Spring Boot & Database Với Docker & Docker Compose

---

## 1. Tại sao cần Docker trong Backend Development?

### Vấn đề kinh điển: "It works on my machine!" (Code chạy trên máy tôi nhưng lỗi trên máy bạn/server)
Sự khác biệt về phiên bản Java, cấu hình hệ điều hành (Windows vs Linux), driver DB hoặc biến môi trường thường gây ra lỗi khi triển khai (Deployment).

### Giải pháp của Docker:
**Docker** đóng gói toàn bộ mã nguồn ứng dụng, môi trường chạy (JRE), các thư viện phụ thuộc và biến cấu hình vào một đơn vị độc lập gọi là **Docker Container**.
- Chạy giống hệt nhau trên máy Mac, Windows, Linux server hay Cloud (AWS, GCP).

```
┌────────────────────────────────────────────────────────┐
│     Source Code (Mã nguồn Java Spring Boot + pom.xml)  │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Cung cấp chỉ dẫn nạp & đóng gói
                            ▼
┌────────────────────────────────────────────────────────┐
│       Dockerfile (Tập lệnh build JAR & thiết lập JRE)  │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ docker build -t my-app .
                            ▼
┌────────────────────────────────────────────────────────┐
│     Docker Image (Bản thiết kế đóng gói độc lập)       │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ docker run -p 8080:8080 my-app
                            ▼
┌────────────────────────────────────────────────────────┐
│    Docker Container (Tiến trình đang chạy cô lập)      │
└────────────────────────────────────────────────────────┘
```

---

## 2. Viết `Dockerfile` tối ưu với Multi-Stage Build

Kỹ thuật **Multi-stage build** giúp tách biệt quá trình compile (cần JDK và Maven cồng kềnh) với quá trình runtime (chỉ cần JRE siêu nhẹ), giúp giảm dung lượng image từ ~700MB xuống chỉ còn **~150MB**:

Tạo file `Dockerfile` ngay tại thư mục gốc của project:
```dockerfile
# ==========================================
# GIAI ĐOẠN 1: BUILD JAR VỚI MAVEN & JDK
# ==========================================
FROM eclipse-temurin:17-jdk-alpine AS builder
WORKDIR /build

# Copy file định nghĩa dependency trước để tận dụng Docker Cache
COPY pom.xml .
COPY .mvn .mvn
COPY mvnw .
RUN ./mvnw dependency:go-offline

# Copy toàn bộ mã nguồn và build đóng gói file JAR
COPY src src
RUN ./mvnw clean package -DskipTests

# ==========================================
# GIAI ĐOẠN 2: RUNTIME VỚI JRE SIÊU NHẸ
# ==========================================
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Tạo user bảo mật không quyền root để chạy app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# Copy file JAR đã build từ giai đoạn 1 sang
COPY --from=builder /build/target/*.jar app.jar

# Khai báo port của ứng dụng
EXPOSE 8080

# Thiết lập tham số bộ nhớ JVM và khởi chạy ứng dụng
ENTRYPOINT ["java", "-XX:+UseG1GC", "-XX:MaxRAMPercentage=75.0", "-jar", "app.jar"]
```

---

## 3. Các lệnh Docker CLI thiết yếu hàng ngày

| Lệnh | Ý nghĩa |
| :--- | :--- |
| `docker build -t my-backend-app:1.0 .` | Build Docker image từ Dockerfile trong thư mục hiện tại. |
| `docker images` | Liệt kê tất cả các Docker Image đang có trên máy. |
| `docker run -d -p 8080:8080 --name backend-service my-backend-app:1.0` | Khởi chạy container ở chế độ ngầm (`-d`) và map port máy thật 8080 vào container. |
| `docker ps` | Xem danh sách các container đang chạy. |
| `docker logs -f backend-service` | Xem trực tiếp log console của ứng dụng bên trong container. |
| `docker stop backend-service` | Dừng container. |
| `docker rm backend-service` | Xóa container sau khi đã dừng. |

---

## 4. Điều phối toàn bộ hệ thống với `docker-compose.yml`

Thay vì phải chạy thủ công từng lệnh khởi động PostgreSQL, rồi sau đó mới khởi động Spring Boot, **Docker Compose** cho phép khởi chạy toàn bộ kiến trúc chỉ bằng **1 lệnh duy nhất**:

Tạo file `docker-compose.yml` tại thư mục gốc:
```yaml
version: '3.8'

services:
  # Service 1: Cơ sở dữ liệu PostgreSQL
  postgres-db:
    image: postgres:15-alpine
    container_name: shop-postgres
    restart: unless-stopped
    environment:
      POSTGRES_DB: shop_db
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secretpassword
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - shop-network

  # Service 2: Backend Spring Boot
  backend-api:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: shop-backend
    restart: unless-stopped
    ports:
      - "8080:8080"
    depends_on:
      - postgres-db
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres-db:5432/shop_db
      SPRING_DATASOURCE_USERNAME: admin
      SPRING_DATASOURCE_PASSWORD: secretpassword
      SPRING_JPA_HIBERNATE_DDL_AUTO: update
    networks:
      - shop-network

volumes:
  postgres_data:
    driver: local

networks:
  shop-network:
    driver: bridge
```

### Các lệnh vận hành Docker Compose:
- **Khởi động toàn bộ**: `docker compose up -d`
- **Xem log toàn hệ thống**: `docker compose logs -f`
- **Dừng và dọn dẹp**: `docker compose down`
- **Rebuild và chạy lại khi có code mới**: `docker compose up --build -d`

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Docker Container vs Virtual Machine (VM) khác nhau thế nào?
| Tiêu chí | Docker Container | Virtual Machine (Máy ảo VMware / VirtualBox) |
| :--- | :--- | :--- |
| **Kiến trúc phần cứng** | **Chia sẻ chung nhân hệ điều hành (Shared Host OS Kernel)**. | Mỗi máy ảo phải cài riêng một hệ điều hành khách (**Guest OS**) đầy đủ. |
| **Dung lượng lưu trữ** | Cực nhẹ (vài chục MB tới vài trăm MB). | Rất nặng (vài GB tới vài chục GB). |
| **Thời gian khởi động** | **Gần như tức thì (vài giây)** vì chỉ là một tiến trình (Process) của OS. | Chậm (vài chục giây tới vài phút) để boot toàn bộ Guest OS. |
| **Mức độ tiêu tốn tài nguyên** | Tối ưu tuyệt đối: Sử dụng trực tiếp RAM/CPU của máy chủ khi cần. | Lãng phí tài nguyên: Phải cấp phát cứng trước dung lượng RAM và Core CPU. |

### 4.2. Tại sao BẮT BUỘC nên dùng Multi-stage Build khi đóng gói ứng dụng Spring Boot?
- **Vấn đề của Single-stage thông thường:** Nếu dùng 1 image duy nhất chứa JDK và Maven để vừa build vừa chạy, image cuối cùng sẽ nặng tới **hơn 800MB - 1GB**, chứa đầy mã nguồn gốc, file cache maven rác và các công cụ biên dịch không cần thiết (nguy cơ bảo mật).
- **Lợi ích vượt trội của Multi-stage Build:**
  - **Giai đoạn 1 (Builder):** Dùng image `maven:3.9-eclipse-temurin-17` để tải dependencies và biên dịch file `app.jar`.
  - **Giai đoạn 2 (Runner):** Chỉ dùng image siêu nhẹ `eclipse-temurin:17-jre-alpine` (chỉ có JRE, không có trình biên dịch) và chỉ copy đúng duy nhất 1 file `app.jar` sang.
  - $\rightarrow$ **Kết quả:** Kích thước Docker Image giảm từ 800MB xuống chỉ còn **khoảng 150MB - 200MB**, kéo/đẩy qua mạng siêu nhanh và bảo mật tuyệt đối trên Production!

### 4.3. Sự khác nhau giữa `CMD` và `ENTRYPOINT` trong Dockerfile?
- **`ENTRYPOINT`:** Định nghĩa câu lệnh **cố định và bất biến** sẽ luôn luôn được chạy khi Container khởi động (ví dụ: `ENTRYPOINT ["java", "-jar", "app.jar"]`).
- **`CMD`:** Cung cấp các **tham số mặc định** cho `ENTRYPOINT`. Các tham số này có thể dễ dàng bị **ghi đè (override)** khi người dùng truyền tham số từ dòng lệnh `docker run`.
- **Thực tiễn tốt nhất cho Spring Boot:**
  ```dockerfile
  ENTRYPOINT ["java", "-jar", "app.jar"]
  CMD ["--spring.profiles.active=prod"]
  ```
  Nếu chạy `docker run my-app` $\rightarrow$ Profile sẽ là `prod`. Nếu chạy `docker run my-app --spring.profiles.active=dev` $\rightarrow$ Lệnh mới sẽ ghi đè tham số của `CMD` để chạy profile `dev` linh hoạt.

---
*Thực hành:* Viết file `Dockerfile` Multi-stage build cho dự án Spring Boot, build image bằng `docker build -t my-app .` và chạy thử bằng `docker run -p 8080:8080 my-app`.

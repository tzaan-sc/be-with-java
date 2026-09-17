# Chapter 04: Web Server, App Server & Database

## 1. Định nghĩa
- **Web Server**: Phục vụ các tài nguyên **tĩnh** (HTML, CSS, JS, hình ảnh) và thường có khả năng chuyển tiếp yêu cầu tới **Application Server**. Các server phổ biến:
  - **Nginx** – reverse proxy, load‑balancer, static file server.
  - **Apache HTTPD** – mô-đun linh hoạt, hỗ trợ mod_php, mod_proxy.
- **Application Server** (App Server): Chạy **mã nghiệp vụ** (Java, .NET, Node.js, Python). Ví dụ:
  - **Tomcat** – Servlet container cho Java web.
  - **Jetty**, **Undertow**, **WildFly**.
  - **Spring Boot** (embedded Tomcat/Jetty) – tự động chạy như một App Server.
- **Database**: Hệ quản trị dữ liệu, lưu trữ **bền vững** và cung cấp **transaction** ACID.
  - **SQL** (MySQL, PostgreSQL, Oracle) – quan hệ, schema cố định.
  - **NoSQL** (MongoDB, Redis, Cassandra) – phi quan hệ, linh hoạt, tốc độ cao.

## 2. Kiến trúc thường gặp
```mermaid
graph LR
    C[Client / Browser] -->|HTTPS| LB[Load‑Balancer (Nginx)]
    LB -->|Reverse Proxy| WS[Web Server (Nginx/Apache)]
    WS -->|Static files / Proxy| AS[App Server (Tomcat/Spring Boot)]
    AS -->|JDBC / JPA| DB[(Database)]
    DB -->|Result Set| AS
    AS -->|JSON / HTML| WS
    WS -->|Response| C
```
- **Load Balancer** (Nginx, HAProxy) phân phối request tới nhiều Web Server.
- **Web Server** có thể **serve static** và **proxy** tới App Server (đại diện cho các micro‑service).
- **App Server** thực hiện **business logic**, **transaction**, **security**, và **return** dữ liệu cho Web Server.

## 3. Khi nào dùng Web Server riêng?
| Trường hợp | Lý do |
|------------|-------|
| Tài nguyên tĩnh lớn (hình ảnh, video) | Giảm tải cho App Server, cache hiệu quả. |
| Need **SSL termination** & **gzip compression** ở edge | Nginx/Apache thực hiện nhanh, App Server không cần.
| **Load‑balancing** nhiều micro‑service | Nginx/HAProxy quản lý routing, health‑check. |
| **Static site** hoặc **SPA** (React/Vue) | Web Server chỉ serve `index.html` + assets. |

## 4. Các tính năng quan trọng
- **Reverse Proxy** – chuyển tiếp request, ẩn IP nội bộ của App Server.
- **SSL/TLS termination** – TLS handshake ở Web Server, giảm overhead cho App Server.
- **Caching** – `proxy_cache` (Nginx) hoặc `mod_cache` (Apache) lưu kết quả tạm thời.
- **Compression** – `gzip` giảm kích thước payload.
- **Rate limiting** – bảo vệ khỏi DDoS.

## 5. Cấu hình mẫu (Nginx)
```nginx
# /etc/nginx/conf.d/backend.conf
server {
    listen 80;
    server_name api.example.com;

    # SSL (optional – use certbot / Let's Encrypt)
    # listen 443 ssl; ssl_certificate /etc/letsencrypt/live/api.example.com/fullchain.pem;

    location / {
        proxy_pass http://localhost:8080;   # Spring Boot (App Server)
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Serve static assets directly (if any)
    location /static/ {
        alias /var/www/static/;
        expires 30d;
        add_header Cache-Control "public, max-age=2592000";
    }
}
```
- **proxy_pass** chuyển mọi request `/` tới Spring Boot đang chạy trên cổng 8080.
- Header `X‑Forwarded‑*` giúp App Server biết thông tin gốc của client.

## 6. Kết nối Database – Các chế độ
| Kiểu DB | Đặc điểm |
|---------|----------|
| **Relational** (MySQL, PostgreSQL) | Transaction ACID, JOIN, schema cố định, mạnh cho dữ liệu quan hệ.
| **NoSQL – Document** (MongoDB) | Lưu trữ JSON‑like, schema linh hoạt, truy vấn nhanh cho dữ liệu phi‑quan hệ.
| **NoSQL – Key‑Value** (Redis) | Cache, session store, tốc độ micro‑seconds.

**Kết nối** thường dùng **JDBC** (Java Database Connectivity) hoặc **ORM** (Hibernate, Spring Data JPA) kết hợp cùng **Connection Pool (HikariCP)** để tái sử dụng kết nối tới Database, tránh chi phí tạo/ngắt kết nối liên tục.

---

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Khi nào bạn sẽ tách Web Server và App Server thành 2 service độc lập?
Nên tách khi hệ thống phát triển lên quy mô thực tế (Production):
1. **Phục vụ tài nguyên tĩnh & Single Page Application (SPA):** Giao diện React/Vue/Angular build ra HTML/JS/CSS chỉ cần Web Server (Nginx) phân phối với tốc độ cực nhanh mà không cần động tới JVM của Spring Boot.
2. **Cân bằng tải (Load Balancing):** Một Web Server Nginx đứng ngoài phân phối request tới cụm 3 - 5 Spring Boot App Server chạy ngầm bên trong mạng nội bộ.
3. **Bảo mật (Reverse Proxy & Firewall):** Giấu toàn bộ IP thật và port nội bộ của App Server, chỉ mở cổng 80/443 của Nginx ra Internet.
4. **Giảm tải xử lý SSL và Nén (SSL Termination & Gzip):** Nginx xử lý việc mã hóa SSL/TLS bằng C tối ưu cực nhanh, giúp CPU của App Server rảnh tay để tập trung 100% xử lý nghiệp vụ Java.

### 7.2. So sánh Nginx và Apache – Ưu, nhược điểm trong môi trường Microservice
| Tiêu chí | Nginx | Apache HTTPD |
| :--- | :--- | :--- |
| **Kiến trúc luồng** | **Event-driven, Asynchronous, Non-blocking:** 1 worker process có thể xử lý hàng chục ngàn kết nối đồng thời với lượng RAM cực thấp. | **Process / Thread-driven:** Mỗi kết nối mới thường tốn 1 thread/process riêng, tốn nhiều RAM khi chịu tải cao (C10K problem). |
| **Hiệu năng file tĩnh & Proxy** | Cực nhanh, tiêu tốn rất ít RAM và CPU. Là lựa chọn số 1 làm API Gateway / Reverse Proxy cho Microservices. | Chậm hơn và tốn nhiều RAM hơn khi tải nặng. |
| **Mô-đun & Cấu hình** | Cấu hình tập trung trong file config (`nginx.conf`), nạp lại config không cần restart server. | Hỗ trợ cấu hình phi tập trung `.htaccess` linh hoạt cho từng thư mục (phù hợp hosting PHP truyền thống). |
| **Vai trò Microservice** | Chuẩn công nghiệp: Nginx Ingress Controller trong Kubernetes, Reverse Proxy, API Gateway. | Ít khi dùng làm Edge Gateway cho microservices hiện đại. |

### 7.3. Giải thích SSL Termination ở Nginx và tại sao lại làm ở "Edge" (biên giới)?
- **SSL Termination là gì:** Là quá trình giải mã HTTPS (bắt tay mã hóa SSL/TLS) ngay tại tầng Web Server (Nginx) đứng ở rìa ngoài cùng (Edge).
- **Luồng dữ liệu:** Client gửi HTTPS đến Nginx $\rightarrow$ Nginx giải mã traffic thành HTTP thông thường $\rightarrow$ Nginx chuyển tiếp request dạng HTTP nội bộ tới App Server (Spring Boot) qua mạng riêng (Private VPC).
- **Tại sao lại làm ở Edge:**
  1. **Tối ưu tài nguyên:** Mã hóa/giải mã tiêu tốn nhiều năng lượng CPU. Nginx được viết bằng C chuyên dụng để làm việc này nhanh hơn nhiều so với Java Virtual Machine.
  2. **Quản lý chứng chỉ tập trung:** Bạn chỉ cần cài và gia hạn chứng chỉ SSL (Let's Encrypt / Cloudflare SSL) ở duy nhất 1 chỗ (trên Nginx), thay vì phải cài chứng chỉ vào từng service Spring Boot.

### 7.4. Khi một API trả về 500 Internal Server Error nhưng server logs không có lỗi, bạn sẽ kiểm tra gì?
Nếu log của Spring Boot hoàn toàn trống mà client nhận `500`:
1. **Kiểm tra Log của Web Server / Reverse Proxy (Nginx Access Log & Error Log):** Xem lỗi `500` do chính Nginx sinh ra hay do Nginx nhận được từ một tầng trung gian khác.
2. **Kiểm tra Load Balancer / API Gateway:** Có thể Load Balancer (AWS ALB, Cloudflare) gặp lỗi cấu hình timeout hoặc định tuyến sai.
3. **Lỗi ở Tầng Filter / Security trước khi vào ứng dụng:** Exception văng ra ở một Filter sớm (như Servlet Filter, Spring Security) nhưng bị nuốt log hoặc cấu hình Logging level chưa bật (`INFO` thay vì `DEBUG`).
4. **Kiểm tra file cấu hình Log:** Kiểm tra xem file log có bị đầy ổ cứng (`Disk Full`), quyền ghi log (`Permission Denied`), hoặc log đang ghi vào một file/console khác mà bạn chưa mở.

### 7.5. Đưa ra cách caching nội dung tĩnh và dynamic response ở Nginx
- **Nội dung tĩnh (Static Assets - CSS, JS, Image):** Bật cache trình duyệt bằng header `Cache-Control` và `expires`:
  ```nginx
  location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
      expires 30d;
      add_header Cache-Control "public, no-transform";
  }
  ```
- **Dynamic Response (API):** Dùng `proxy_cache`:
  ```nginx
  proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_api_cache:10m inactive=60m;
  
  location /api/v1/products {
      proxy_cache my_api_cache;
      proxy_cache_valid 200 10m;  # Lưu cache kết quả 200 trong 10 phút
      proxy_cache_use_stale error timeout updating;
      proxy_pass http://localhost:8080;
  }
  ```

### 7.6. Khi triển khai Spring Boot (Tomcat), cấu hình maxThreads và Connection Pool thế nào để tối ưu?
- **Tomcat `maxThreads` (số luồng xử lý đồng thời):** Mặc định trong Spring Boot là `200`.
  - Cấu hình qua: `server.tomcat.threads.max=200`
  - *Nguyên tắc:* Không nên đặt quá cao (vd 1000) vì sẽ gây Context Switching làm CPU bị nghẽn và tốn bộ nhớ RAM (mỗi thread tốn ~1MB stack).
- **Database Connection Pool (HikariCP - Mặc định của Spring Boot):**
  - Cấu hình qua: `spring.datasource.hikari.maximum-pool-size=20-30`
  - *Quy tắc vàng của PostgreSQL/HikariCP:*
    $$\text{pool\_size} = 2 \times \text{Core CPU} + \text{Số lượng ổ cứng}$$
    Ví dụ máy chủ DB có 4 Core CPU $\rightarrow$ connection pool tối ưu chỉ khoảng $10 - 15$ kết nối. Đặt connection pool quá lớn sẽ khiến Database tranh chấp khóa và nghẽn I/O đĩa cứng.
- **Tương quan:** `maxThreads` của Tomcat luôn lớn hơn `pool_size` của HikariCP vì không phải request nào cũng cần query Database (có request chỉ kiểm tra logic hoặc đọc cache Redis).

---
*Thực hành Ngày 07 & 08:* Cài đặt Nginx làm Reverse Proxy trỏ về ứng dụng hoặc dùng Docker để chạy thử Nginx kết hợp Tomcat.

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

**Kết nối** thường dùng **JDBC** (Java) hoặc **ORM** (Hibernate, JPA) để ánh xạ **Entity ↔ Table**.

## 7. Câu hỏi phỏng vấn thường gặp
- Khi nào bạn sẽ **tách Web Server và App Server** thành 2 service độc lập?
- So sánh **Nginx** và **Apache** – ưu, nhược điểm trong môi trường micro‑service.
- Giải thích **SSL termination** ở Nginx và tại sao lại làm ở **edge**.
- Khi một API trả về **500 Internal Server Error** nhưng server logs không có lỗi, bạn sẽ kiểm tra gì?
- Đưa ra cách **caching** nội dung tĩnh (static assets) và **dynamic response** (API) ở Nginx.
- Khi triển khai **Spring Boot** dưới Tomcat, bạn sẽ cấu hình **maxThreads** và **connection pool** như thế nào để tối ưu performance?

---
*Thực hành:* Cài Nginx, cấu hình reverse proxy tới Spring Boot, kiểm tra `curl -I http://localhost/api/health` và xác nhận header `X-Forwarded-For` xuất hiện.

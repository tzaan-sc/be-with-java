# Chapter 02: Kiến trúc Client‑Server & Vòng đời Request‑Response

## 1. Khái niệm
- **Client‑Server** là mô hình 2 lớp cơ bản: **Client** (frontend, trình duyệt, app) gửi **request** tới **Server** (backend) và nhận **response**.
- Server chịu trách nhiệm **xử lý nghiệp vụ**, **truy cập dữ liệu**, **bảo mật** và **trả kết quả**.

## 2. Thành phần chính
```mermaid
sequenceDiagram
    participant C as Client (Browser/App)
    participant LB as Load‑Balancer (Optional)
    participant S as Backend Server
    C->>LB: HTTP Request (GET/POST …)
    LB->>S: Forward request
    S->>S: Auth → Business Logic → DB
    S->>LB: HTTP Response
    LB->>C: Response (JSON/HTML)
```
- **Load Balancer** (Nginx, HAProxy) – phân phối tải tới nhiều server.
- **Web Server** – nhận request, trả file tĩnh, chuyển tiếp tới **App Server**.
- **App Server** – thực thi logic, gọi **Service Layer** → **Repository/DAO** → **Database**.

## 3. Cấu tạo của một HTTP Request & Response (Ngày 03)

### 3.1. Cấu tạo của một HTTP Request
Mỗi yêu cầu từ Client gửi lên Server gồm 3 thành phần chính:
1. **Request Line (Dòng đầu tiên):**
   - **HTTP Method:** Hành động mong muốn (`GET`: lấy dữ liệu, `POST`: tạo mới, `PUT`/`PATCH`: cập nhật, `DELETE`: xóa).
   - **Request URL / URI:** Đường dẫn tới tài nguyên (ví dụ: `/api/v1/products?page=1`).
   - **HTTP Version:** Phiên bản giao thức (ví dụ: `HTTP/1.1`, `HTTP/2`).
2. **Request Headers:**
   - Siêu dữ liệu (metadata) dưới dạng Key-Value:
     - `Host: api.example.com` (Tên miền máy chủ).
     - `Authorization: Bearer <token>` (Thông tin xác thực danh tính).
     - `Content-Type: application/json` (Định dạng của dữ liệu gửi kèm).
     - `User-Agent: Mozilla/5.0...` (Thông tin thiết bị/trình duyệt của Client).
3. **Request Body (Thân thông điệp):**
   - Chứa dữ liệu thực tế (Payload), thường ở định dạng JSON khi gửi `POST` hoặc `PUT`.
   - Lưu ý: Request `GET` và `DELETE` thông thường sẽ **không** có body.

### 3.2. Cấu tạo của một HTTP Response
Khi xử lý xong, Server trả về gồm:
1. **Status Line:** Gồm HTTP Version + **HTTP Status Code** + Status Text:
   - `2xx (Success):` `200 OK`, `201 Created` (Tạo mới thành công).
   - `3xx (Redirection):` `301 Moved Permanently`, `304 Not Modified` (Dùng bản cache).
   - `4xx (Client Error):` `400 Bad Request` (Dữ liệu gửi lên sai định dạng), `401 Unauthorized` (Chưa đăng nhập), `403 Forbidden` (Không đủ quyền), `404 Not Found` (Không tìm thấy tài nguyên).
   - `5xx (Server Error):` `500 Internal Server Error` (Lỗi crash code Backend), `502 Bad Gateway`, `503 Service Unavailable` (Server quá tải).
2. **Response Headers:** `Content-Type: application/json`, `Set-Cookie`, `Date`...
3. **Response Body:** Dữ liệu JSON hoặc mã HTML/file gửi về cho Client.

---

## 4. Giao thức TCP/IP & Bắt tay 3 bước (3-way Handshake) (Ngày 04)

Trước khi Client có thể gửi được bất kỳ HTTP Request nào, tầng Giao vận (Transport Layer) phải thiết lập một kết nối tin cậy giữa Client và Server thông qua **TCP 3-way Handshake**:

```mermaid
sequenceDiagram
    autonumber
    actor Client as Client (Trình duyệt / App)
    participant Server as Backend Server (Port 80/443)

    Note over Client, Server: Bắt đầu bắt tay 3 bước (TCP 3-way Handshake)
    Client->>Server: 1. Gói tin SYN (Synchronize): "Tôi muốn kết nối, số seq của tôi là X"
    Server->>Client: 2. Gói tin SYN-ACK: "Tôi đồng ý kết nối (ACK X+1), số seq của tôi là Y"
    Client->>Server: 3. Gói tin ACK (Acknowledge): "Tôi đã nhận được phản hồi (ACK Y+1). Kết nối đã sẵn sàng!"
    
    Note over Client, Server: KẾT NỐI TCP THÀNH CÔNG -> Bắt đầu truyền HTTP Data
    Client->>Server: 4. Gửi HTTP Request (GET /api/v1/products)
    Server->>Client: 5. Gửi HTTP Response (200 OK + JSON)
    
    Note over Client, Server: Đóng kết nối (TCP 4-way Handshake)
    Client->>Server: FIN -> Server trả ACK -> Server gửi FIN -> Client trả ACK (Đóng cổng)
```

### Tại sao HTTP/HTTPS bắt buộc phải chạy trên nền TCP thay vì UDP?
- **Độ tin cậy tuyệt đối:** TCP đảm bảo các gói tin không bị mất (nếu mất gói sẽ tự động gửi lại - Retransmission) và đảm bảo thứ tự các gói tin (đúng thứ tự văn bản, code JSON). Nếu dùng UDP, dữ liệu có thể bị mất gói dẫn tới hỏng cấu trúc JSON hoặc thiếu sót thông tin quan trọng.
- **Kiểm soát luồng & Tránh tắc nghẽn (Flow & Congestion Control):** TCP tự động điều tiết tốc độ truyền dữ liệu phù hợp với băng thông mạng của cả hai bên.

---

## 5. Ví dụ thực tế – GET danh sách sản phẩm
```http
GET /api/v1/products?page=1&size=20 HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1Ni...
Accept: application/json
```
- **Server** xác thực token, gọi `ProductService.getProducts(page, size)`, truy vấn DB, trả về JSON:
```json
{
  "status": 200,
  "data": [
    {"id": 1, "name": "Bàn phím cơ", "price": 1200000}
  ],
  "page": 1,
  "size": 20,
  "totalElements": 1
}
```

---

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Client‑Server khác gì so với Peer‑to‑Peer (P2P)?
- **Mô hình Client - Server (Tập trung - Centralized):** Có sự phân vai rõ ràng: Client chỉ yêu cầu, Server là trung tâm phục vụ và nắm giữ toàn bộ dữ liệu. Ưu điểm là dễ quản lý, dễ bảo mật và cập nhật logic; nhược điểm là nếu Server sập thì toàn bộ hệ thống tê liệt (Single Point of Failure).
- **Mô hình Peer-to-Peer (Ngang hàng - Decentralized):** Mọi nút (Node) trong mạng đều vừa là Client vừa là Server (như BitTorrent, Blockchain). Không có máy chủ trung tâm; ưu điểm là khả năng chịu lỗi cực cao và khó bị đánh sập, nhược điểm là khó kiểm soát bảo mật và đồng bộ trạng thái dữ liệu.

### 6.2. Giải thích TCP 3‑way handshake và tại sao HTTP/HTTPS dựa trên TCP?
- **Cơ chế:** Gồm 3 bước:
  1. `SYN`: Client gửi yêu cầu đồng bộ số thứ tự chuỗi dữ liệu (Sequence Number).
  2. `SYN-ACK`: Server xác nhận đã nhận và gửi lại Sequence Number của chính mình.
  3. `ACK`: Client xác nhận lại lần cuối, kênh truyền 2 chiều chính thức được mở.
- **Lý do HTTP dựa trên TCP:** Dữ liệu web (mã HTML, JSON API, file ảnh) đòi hỏi tính chính xác 100%. TCP cung cấp cơ chế kiểm tra lỗi checksum, tự động gửi lại gói tin bị mất và sắp xếp lại đúng thứ tự trước khi đưa lên ứng dụng.

### 6.3. Khi nào nên dùng HTTP/2 thay vì HTTP/1.1?
- Trong hầu hết các ứng dụng Web/App hiện đại, **HTTP/2 luôn là sự lựa chọn vượt trội** vì:
  - **Multiplexing (Đa ghép kênh):** HTTP/1.1 phải mở nhiều kết nối TCP song song hoặc chờ request trước xong mới gửi request sau (Head-of-Line blocking ở tầng ứng dụng). HTTP/2 cho phép gửi/nhận hàng trăm request và response cùng lúc trên **duy nhất 1 kết nối TCP**.
  - **Header Compression (HPACK):** Nén kích thước header (vốn lặp đi lặp lại như cookie, user-agent), tiết kiệm băng thông.
  - **Server Push:** Cho phép Server chủ động gửi trước các tài nguyên kèm theo (CSS/JS) trước khi Client kịp yêu cầu.

### 6.4. Làm sao để Keep‑Alive giảm số lần thiết lập kết nối?
- Mặc định trong HTTP/1.0, mỗi lần tải một tài nguyên (1 file ảnh, 1 API call) là một lần phải thực hiện lại bắt tay TCP 3 bước rồi đóng kết nối ngay, gây lãng phí CPU và độ trễ mạng cực lớn.
- Header `Connection: keep-alive` (mặc định được bật trong HTTP/1.1) cho phép **tái sử dụng kết nối TCP hiện có** để gửi tiếp các request sau mà không phải đóng đi mở lại, giúp giảm độ trễ (latency) đáng kể.

### 6.5. Đưa ra giải pháp Load Balancing cho một dịch vụ có 10.000 req/s
Để chịu tải 10.000 requests/giây (RPS), kiến trúc chuẩn gồm:
1. **DNS Load Balancing / Anycast DNS (Tầng ngoài cùng):** Phân chia lưu lượng theo vị trí địa lý của người dùng tới các Data Center gần nhất.
2. **Cụm Load Balancer phần mềm chuyên dụng:** Dùng **Nginx** hoặc **HAProxy** (hoặc AWS ALB) chạy mô hình Master - Backup (Keepalived) để tránh điểm chết đơn độc (SPOF).
3. **Thuật toán điều phối:** Dùng `Round Robin` hoặc `Least Connections` (chuyển request tới server đang rảnh nhất).
4. **Cụm Application Server (Horizontal Scaling):** Chia đều 10.000 req/s cho 10 - 20 máy chủ backend (mỗi máy gánh 500 - 1.000 req/s).
5. **Caching Layer:** Đặt Redis Cache ở giữa App Server và Database để chặn 80-90% các request đọc (Read requests), ngăn Database bị nghẽn I/O.

---
*Thực hành Ngày 03 & 04:* 
1. Mở Chrome DevTools (F12) -> Tab **Network** -> Bấm F5 một trang web bất kỳ để xem các request: Method, Status Code, Headers.
2. Mở Terminal gõ `curl -I https://google.com` để xem Header trả về có `HTTP/2` hay `Connection: keep-alive` không.

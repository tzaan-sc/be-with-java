# 🛠 Bài Tập Thực Hành – Phase 0: Backend Căn Bản

> Bài tập được thiết kế theo lộ trình **20‑30 phút/ngày**.  
> Mỗi bài tương ứng với nội dung lý thuyết đã học trong ngày, giúp bạn **chốt kiến thức** ngay sau khi đọc xong.  
> Ký hiệu: `[ ]` Chưa làm · `[x]` Đã hoàn thành

---

## Bài tập Ngày 01‑02: Backend là gì & Các thành phần cốt lõi
*(Tương ứng Chapter 01)*

### Bài 1.1 – Phân biệt Frontend vs Backend *(~5 phút)*
[x] Điền vào bảng bên dưới:

| Tiêu chí | Frontend | Backend |
|----------|----------|---------|
| Chạy ở đâu? | *client (trình duyệt, ứng dụng mobile)* | *server (máy chủ)* |
| Ngôn ngữ phổ biến? | *Html,css,javascript* | *java, go, python, nodejs,...* |
| Ai tương tác trực tiếp? | *user* | *developer, admin, hệ thống khác qua API* |
| Ví dụ công việc chính? | *hiển thị giao diện, trải nghiệm ng dùng* | *logic nghiệp vụ, tương tác DB, nhận request, trả response* |

### Bài 1.2 – Vẽ sơ đồ kiến trúc hệ thống *(~10 phút)*
[x] Vẽ sơ đồ (trên giấy hoặc tool bất kỳ) mô tả luồng đi khi người dùng **đăng nhập** vào một ứng dụng web:

**Yêu cầu sơ đồ phải thể hiện được:**
1. Client (Browser) gửi Request tới đâu?
2. Backend Server xử lý qua những lớp nào? (Security → Service → Database)
3. Database trả kết quả về theo chiều nào?
4. Response cuối cùng trả về cho Client chứa gì?
#### Đáp án:
```
┌──────────────────┐
│  Client / Browser│
└────────┬─────────┘
         │
         │ 1. POST /login
         │    username + password
         ▼
┌──────────────────┐
│ Backend Server   │
│                  │
│ ┌──────────────┐ │
│ │   Security   │ │
│ │ Xác thực     │ │
│ │ username +   │ │
│ │ password     │ │
│ └──────┬───────┘ │
│        │         │
│        ▼         │
│ ┌──────────────┐ │
│ │   Service    │ │
│ │ Xử lý        │ │
│ │ đăng nhập    │ │
│ └──────┬───────┘ │
└─────────┼────────┘
          │
          │ 2. Truy vấn thông tin
          ▼
┌──────────────────┐
│    Database      │
│                  │
│ users            │
│ username         │
│ password_hash    │
│ roles            │
└────────┬─────────┘
         │
         │ 3. Trả kết quả
         │    user information
         ▼
┌──────────────────┐
│     Service      │
└────────┬─────────┘
         │
         │ 4. Kết quả xác thực
         │    + tạo Token/Session
         ▼
┌──────────────────┐
│    Security      │
└────────┬─────────┘
         │
         │ 5. Authentication Result
         ▼
┌──────────────────┐
│ Backend Server   │
└────────┬─────────┘
         │
         │ 6. HTTP Response
         │    200 OK + Token/Session
         ▼
┌──────────────────┐
│  Client / Browser│
│                  │
│ Đăng nhập thành  │
│ công              │
└──────────────────┘
```

```
Browser
   ↓
Security Filter
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

### Bài 1.3 – Phân tích luồng mua hàng *(~10 phút)*
[x] Mô tả **bằng lời của bạn** (viết ra giấy hoặc ghi vào đây) toàn bộ các bước Backend xử lý khi người dùng nhấn nút **"Thêm vào giỏ hàng"** trên Shopee:

```
Bước 1: User click nút "Thêm vào giỏ hàng"
Bước 2: Frontend gửi Request "Add to cart"
Bước 3: Middleware kiểm tra 
Bước 3: Controller nhận Request và gọi Service
Bước 4: Service truy vấn Database kiểm tra sản phẩm có tồn tại và còn hàng hay không
Bước 5: Service kiểm tra sản phẩm có thuộc giỏ hàng của user chưa, nếu có thì cập nhật số lượng, nếu chưa thì thêm mới
Bước 6: Service trả kết quả về cho Controller
Bước 7: Controller trả kết quả về cho Frontend
Bước 8: Frontend hiển thị kết quả cho User
```

**Gợi ý:** Nghĩ về kiểm tra đăng nhập, kiểm tra sản phẩm tồn tại, kiểm tra tồn kho, lưu vào giỏ hàng trong DB, trả kết quả.

### Bài 1.4 – Câu hỏi trắc nghiệm nhanh *(~5 phút)*
[x] Trả lời các câu hỏi sau (ghi đáp án A/B/C/D):

**Câu 1:** Middleware trong Backend đóng vai trò gì?
- A. Hiển thị giao diện người dùng
- **B. Xử lý trung gian giữa Request và Business Logic (logging, auth, validation)**
- C. Lưu trữ dữ liệu vào ổ cứng
- D. Thiết kế CSS cho trang web

**Câu 2:** API là viết tắt của gì và dùng để làm gì?
- **A. Application Programming Interface – giao tiếp giữa các phần mềm**
- B. Advanced Protocol Integration – mã hoá dữ liệu
- C. Automated Process Installer – cài đặt phần mềm tự động
- D. Application Page Interface – hiển thị trang web

**Câu 3:** Trong kiến trúc Backend, tầng nào chịu trách nhiệm chính cho logic nghiệp vụ (tính giá, kiểm kho, áp voucher)?
- A. Controller Layer
- **B. Service Layer**
- C. Repository Layer
- D. Database Layer

```
Đáp án: Câu 1: B | Câu 2: A | Câu 3: B
```

---

## Bài tập Ngày 03‑04: Client‑Server & Request‑Response
*(Tương ứng Chapter 02)*

### Bài 2.1 – Quan sát Request/Response thực tế bằng Chrome DevTools *(~10 phút)*
[ ] Thực hiện các bước sau:
1. Mở trình duyệt Chrome, truy cập `https://jsonplaceholder.typicode.com/posts/1`
2. Nhấn `F12` → chuyển sang tab **Network** → nhấn `F5` để reload
3. Click vào dòng request `1` xuất hiện trong danh sách
4. Ghi lại các thông tin sau:

```
Request URL:      ___________________________
Request Method:   ___________________________
Status Code:      ___________________________
Content-Type:     ___________________________
Response Body (3 dòng đầu):
___________________________
___________________________
___________________________
```

### Bài 2.2 – Phân biệt thành phần của HTTP Request *(~5 phút)*
[ ] Cho đoạn HTTP Request sau, hãy chỉ ra đâu là **Method**, **URL**, **Header**, **Body**:

```http
POST /api/v1/users HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...

{
  "name": "Nguyễn Văn A",
  "email": "a@gmail.com",
  "password": "123456"
}
```

```
Method:  ___________________________
URL:     ___________________________
Headers: ___________________________
         ___________________________
Body:    ___________________________
```

### Bài 2.3 – Mô tả TCP 3‑Way Handshake *(~5 phút)*
[ ] Điền vào chỗ trống để hoàn thành quy trình bắt tay 3 bước:

```
Bước 1: Client gửi gói tin _______ tới Server  (Ý nghĩa: "Tôi muốn kết nối")
Bước 2: Server trả về gói tin _______ cho Client  (Ý nghĩa: "OK, tôi đồng ý, bạn sẵn sàng chưa?")
Bước 3: Client gửi lại gói tin _______ cho Server  (Ý nghĩa: "Sẵn sàng, bắt đầu truyền dữ liệu!")
```

### Bài 2.4 – So sánh TCP vs UDP *(~5 phút)*
[ ] Điền vào bảng so sánh:

| Tiêu chí | TCP | UDP |
|----------|-----|-----|
| Có kết nối trước khi truyền? | *(điền)* | *(điền)* |
| Đảm bảo thứ tự gói tin? | *(điền)* | *(điền)* |
| Tốc độ? | *(điền)* | *(điền)* |
| Ứng dụng phù hợp? | *(điền)* | *(điền)* |

[ ] **Câu hỏi mở:** Tại sao xem video trực tiếp (livestream) dùng UDP mà không dùng TCP?

```
Trả lời: ___________________________________________
```

---

## Bài tập Ngày 05‑06: Mạng máy tính, IP, Port & DNS
*(Tương ứng Chapter 03)*

### Bài 3.1 – Thực hành lệnh Terminal *(~10 phút)*
[ ] Mở **Command Prompt** (Windows) hoặc **Terminal** (Mac/Linux) và chạy lần lượt:

**Lệnh 1: Ping**
```bash
ping google.com
```
Ghi lại kết quả:
```
IP của google.com:    ___________________________
Thời gian trung bình: ___________________________ ms
```

**Lệnh 2: NSLookup**
```bash
nslookup facebook.com
```
Ghi lại kết quả:
```
DNS Server đã dùng:  ___________________________
IP trả về:           ___________________________
```

**Lệnh 3: Tracert (Windows) / Traceroute (Mac/Linux)**
```bash
tracert google.com
```
Ghi lại kết quả:
```
Số lượng hops (bước nhảy): ___________________________
Hop nào có latency cao nhất?: ___________________________
```

### Bài 3.2 – Bài tập Port *(~5 phút)*
[ ] Nối cột: Mỗi Port mặc định tương ứng với dịch vụ nào?

| Port | Dịch vụ |
|------|---------|
| 80   | *(điền)* |
| 443  | *(điền)* |
| 3306 | *(điền)* |
| 5432 | *(điền)* |
| 8080 | *(điền)* |
| 27017| *(điền)* |

### Bài 3.3 – Mô tả luồng DNS bằng lời *(~5 phút)*
[ ] Khi bạn gõ `https://api.shopee.vn/products` trên trình duyệt, hãy mô tả từng bước DNS phân giải tên miền:

```
Bước 1: Trình duyệt kiểm tra _______ (cache nội bộ)
Bước 2: Nếu không có, hỏi _______ (DNS Resolver của ISP / Google 8.8.8.8)
Bước 3: Resolver hỏi _______ (Root Server → .vn TLD → shopee.vn Authoritative)
Bước 4: Trả về địa chỉ IP: _______
Bước 5: Trình duyệt dùng IP đó để thiết lập kết nối _______ tới server
```

### Bài 3.4 – Thực hành cURL *(~10 phút)*
[ ] Mở Terminal và chạy lệnh sau:

```bash
curl -I https://google.com
```

Ghi lại các thông tin quan trọng từ kết quả:
```
HTTP Status:      ___________________________
Content-Type:     ___________________________
Location (nếu có): ___________________________
Server:           ___________________________
```

[ ] Thử gọi một API công khai và xem nội dung response body:
```bash
curl https://jsonplaceholder.typicode.com/users/1
```

Ghi lại:
```
Tên user trả về:  ___________________________
Email:            ___________________________
Website:          ___________________________
```

---

## Bài tập Ngày 07: Web Server, App Server & Database
*(Tương ứng Chapter 04)*

### Bài 4.1 – Phân biệt Web Server vs App Server *(~5 phút)*
[ ] Điền vào bảng so sánh:

| Tiêu chí | Web Server (Nginx/Apache) | App Server (Tomcat/Spring Boot) |
|----------|--------------------------|-------------------------------|
| Nhiệm vụ chính? | *(điền)* | *(điền)* |
| Xử lý file tĩnh (HTML/CSS/JS)? | *(điền)* | *(điền)* |
| Xử lý Business Logic? | *(điền)* | *(điền)* |
| Ví dụ phần mềm? | *(điền)* | *(điền)* |

### Bài 4.2 – So sánh SQL vs NoSQL *(~5 phút)*
[ ] Điền vào bảng so sánh:

| Tiêu chí | SQL (MySQL, PostgreSQL) | NoSQL (MongoDB, Redis) |
|----------|------------------------|----------------------|
| Cấu trúc dữ liệu? | *(Bảng, hàng, cột – schema cố định)* | *(điền)* |
| Quan hệ giữa các bảng? | *(điền)* | *(điền)* |
| Ngôn ngữ truy vấn? | *(điền)* | *(điền)* |
| Phù hợp cho? | *(điền)* | *(điền)* |

### Bài 4.3 – Phân tích kiến trúc triển khai thực tế *(~10 phút)*
[ ] Cho hệ thống **web bán hàng online** gồm:
- **Frontend**: React chạy trên browser
- **Backend**: Spring Boot API
- **Database**: PostgreSQL

Hãy vẽ sơ đồ hoặc mô tả bằng lời kiến trúc triển khai với các câu hỏi:

```
1. Nginx đặt ở đâu và đóng vai trò gì?
   Trả lời: ___________________________________________

2. Spring Boot (Tomcat) chạy ở cổng nào? Nginx forward request tới đâu?
   Trả lời: ___________________________________________

3. PostgreSQL chạy ở cổng mặc định nào?
   Trả lời: ___________________________________________

4. Nếu muốn chạy 3 bản sao Spring Boot để chịu tải, bạn sẽ dùng gì?
   Trả lời: ___________________________________________
```

### Bài 4.4 – Câu hỏi tình huống *(~5 phút)*
[ ] Trả lời các tình huống sau:

**Tình huống 1:** Bạn có 1 trang web bán hàng, 90% request là xem hình ảnh sản phẩm (file tĩnh). Bạn sẽ cấu hình hệ thống thế nào để giảm tải cho App Server?

```
Trả lời: ___________________________________________
```

**Tình huống 2:** Sếp yêu cầu lưu trữ đơn hàng (có quan hệ: User → Order → OrderItem → Product). Bạn chọn SQL hay NoSQL? Tại sao?

```
Trả lời: ___________________________________________
```

**Tình huống 3:** Hệ thống cần lưu session đăng nhập với tốc độ truy xuất cực nhanh (microseconds). Bạn chọn database nào?

```
Trả lời: ___________________________________________
```

---

## Bài tập Ngày 08: Ôn tập tổng kết Phase 0

### Bài 5.1 – Quiz tổng hợp *(~10 phút)*
[ ] Trả lời **10 câu hỏi** tổng hợp toàn bộ Phase 0:

```
1. Backend chịu trách nhiệm cho 3 nhiệm vụ chính nào?
   → ___________________________________________

2. HTTP Request gồm những thành phần nào?
   → ___________________________________________

3. TCP Handshake 3 bước là gì? (ghi tên 3 gói tin)
   → ___________________________________________

4. DNS dùng để làm gì? Giải thích bằng 1 câu ngắn.
   → ___________________________________________

5. Port 443 dùng cho giao thức gì?
   → ___________________________________________

6. Phân biệt Nginx và Tomcat bằng 1 câu.
   → ___________________________________________

7. Reverse Proxy nghĩa là gì?
   → ___________________________________________

8. ACID trong Database là viết tắt của 4 từ nào?
   → ___________________________________________

9. Khi nào nên dùng NoSQL thay vì SQL?
   → ___________________________________________

10. Stateless (không trạng thái) trong HTTP nghĩa là gì?
    → ___________________________________________
```

### Bài 5.2 – Chuẩn bị môi trường cho Phase 1 *(~10 phút)*
[ ] Checklist cài đặt trước khi bắt đầu học Java Core:

```
[ ] Cài JDK 17 hoặc JDK 21 (kiểm tra: java -version)
[ ] Cài IDE: IntelliJ IDEA Community hoặc VS Code + Extension Pack for Java
[ ] Tạo project Java đầu tiên, chạy thử System.out.println("Hello Backend!");
[ ] Cài Git (kiểm tra: git --version)
```

---

## 📋 Bảng đáp án tham khảo

<details>
<summary><b>👉 Click để xem đáp án (chỉ xem SAU KHI đã tự làm)</b></summary>

### Bài 1.4 – Trắc nghiệm
- Câu 1: **B** – Middleware xử lý trung gian (logging, auth, validation)
- Câu 2: **A** – Application Programming Interface
- Câu 3: **B** – Service Layer

### Bài 2.3 – TCP Handshake
- Bước 1: **SYN**
- Bước 2: **SYN‑ACK**
- Bước 3: **ACK**

### Bài 3.2 – Port
| Port  | Dịch vụ |
|-------|---------|
| 80    | HTTP |
| 443   | HTTPS |
| 3306  | MySQL |
| 5432  | PostgreSQL |
| 8080  | Tomcat / Spring Boot (dev) |
| 27017 | MongoDB |

### Bài 4.4 – Tình huống
- **Tình huống 1:** Dùng Nginx serve file tĩnh trực tiếp (location /images/), chỉ proxy request API tới App Server.
- **Tình huống 2:** SQL (PostgreSQL/MySQL) – vì dữ liệu có quan hệ rõ ràng, cần JOIN, transaction ACID.
- **Tình huống 3:** Redis – key‑value store, tốc độ microseconds, phù hợp cho session/cache.

### Bài 5.1 – Quiz
1. Business Logic, Data Persistence, Security & Authorization
2. Method, URL, Headers, Body
3. SYN → SYN‑ACK → ACK
4. DNS dịch tên miền thành địa chỉ IP để máy tính có thể kết nối tới server
5. HTTPS (HTTP over TLS/SSL)
6. Nginx là Web Server / Reverse Proxy, Tomcat là Application Server chạy Java
7. Reverse Proxy là server trung gian nhận request từ client rồi chuyển tiếp tới backend server phía sau
8. Atomicity, Consistency, Isolation, Durability
9. Khi dữ liệu phi quan hệ, schema thay đổi liên tục, cần scale ngang dễ dàng (VD: log, IoT data, chat messages)
10. Server không lưu trạng thái giữa các request, mỗi request phải tự chứa đầy đủ thông tin (token, params)

</details>

---
*Hoàn thành xong tất cả bài tập trên = bạn đã sẵn sàng bước vào Phase 1: Java Core! 🚀*

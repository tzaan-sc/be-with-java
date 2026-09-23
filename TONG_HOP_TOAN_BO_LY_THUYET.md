# SỔ TAY BÁCH KHOA TOÀN THƯ LÝ THUYẾT JAVA BACKEND
---

## 📑 MỤC LỤC ĐIỀU HƯỚNG CHI TIẾT 42 CHƯƠNG

### [PHASE 0: BACKEND CĂN BẢN (BASIC BACKEND)](#phase-0)

- [Chapter 01: Backend là gì? & Vai trò trong hệ thống](#phase-0-chapter-01)
- [Chapter 02: Kiến trúc Client‑Server & Vòng đời Request‑Response](#phase-0-chapter-02)
- [Chapter 03: Networking, IP, Port & DNS](#phase-0-chapter-03)
- [Chapter 04: Web Server, App Server & Database](#phase-0-chapter-04)

### [PHASE 1: JAVA CORE NỀN TẢNG (CORE LANGUAGE & JVM)](#phase-1)

- [Chapter 01: Biến, Kiểu dữ liệu & Ép kiểu (Variables, Data Types & Casting)](#phase-1-chapter-01)
- [Chapter 02: Cấu trúc Điều khiển & Vòng lặp (Control Flow)](#phase-1-chapter-02)
- [Chapter 03: Quản lý Bộ nhớ Java – Stack vs Heap & Garbage Collection](#phase-1-chapter-03)
- [Chapter 04: String, StringBuilder & String Pool](#phase-1-chapter-04)
- [Chapter 05: Xử lý Ngoại lệ (Exception Handling)](#phase-1-chapter-05)

### [PHASE 2: HƯỚNG ĐỐI TƯỢNG (OOP) & COLLECTIONS FRAMEWORK](#phase-2)

- [Chapter 01: 4 Trụ Cột OOP (Encapsulation, Inheritance, Polymorphism, Abstraction)](#phase-2-chapter-01)
- [Chapter 02: Interface vs Abstract Class & Default/Static Methods](#phase-2-chapter-02)
- [Chapter 03: 5 Nguyên Lý SOLID trong Java Backend](#phase-2-chapter-03)
- [Chapter 04: Java Collections Framework – List, Set, Map, Queue](#phase-2-chapter-04)
- [Chapter 05: Generics & Bounded Type Parameters](#phase-2-chapter-05)
- [Chapter 06: Java 8 – Lambda, Functional Interface, Stream API & Optional](#phase-2-chapter-06)

### [PHASE 3: GIAO THỨC HTTP & THIẾT KẾ RESTFUL API](#phase-3)

- [Chapter 01: HTTP Fundamentals – Request, Response, Headers, Cookies](#phase-3-chapter-01)
- [Chapter 02: HTTP Methods & Status Codes](#phase-3-chapter-02)
- [Chapter 03: Quy chuẩn thiết kế RESTful API](#phase-3-chapter-03)
- [Chapter 04: JSON & Serialization/Deserialization (Jackson)](#phase-3-chapter-04)
- [Chapter 05: API Testing Tools – Postman & cURL](#phase-3-chapter-05)

### [PHASE 4: SPRING BOOT CORE & KIẾN TRÚC 3 TẦNG](#phase-4)

- [Chapter 01: Spring Core – IoC, Dependency Injection, Bean Lifecycle](#phase-4-chapter-01)
- [Chapter 02: Spring Boot Overview – Auto-configuration, Starters, Config Properties](#phase-4-chapter-02)
- [Chapter 03: Kiến trúc 3 tầng Spring MVC – Controller, Service, Repository](#phase-4-chapter-03)
- [Chapter 04: DTO Pattern & Bean Validation](#phase-4-chapter-04)
- [Chapter 05: Global Exception Handling – @RestControllerAdvice](#phase-4-chapter-05)

### [PHASE 5: DATABASE, JPA & HIBERNATE ORM](#phase-5)

- [Chapter 01: RDBMS & SQL – Primary Key, Foreign Key, Indexing](#phase-5-chapter-01)
- [Chapter 02: JPA/Hibernate Basics – @Entity, @Id, @Column, @Table](#phase-5-chapter-02)
- [Chapter 03: Entity Relationships – @OneToMany, @ManyToOne, Lazy vs Eager](#phase-5-chapter-03)
- [Chapter 04: Spring Data JPA – Derived Query, JPQL, N+1 Problem](#phase-5-chapter-04)
- [Chapter 05: Transaction Management – @Transactional](#phase-5-chapter-05)
- [Chapter 06: Pagination & Sorting – Pageable, Page, Slice](#phase-5-chapter-06)

### [PHASE 6: BẢO MẬT HỆ THỐNG (SPRING SECURITY & JWT)](#phase-6)

- [Chapter 01: Nền Tảng Bảo Mật – Authentication vs Authorization & Hash Mật Khẩu với BCrypt](#phase-6-chapter-01)
- [Chapter 02: Kiến Trúc Spring Security – SecurityFilterChain, AuthenticationManager & UserDetailsService](#phase-6-chapter-02)
- [Chapter 03: Xác Thực Không Trạng Thái với JWT (JSON Web Token)](#phase-6-chapter-03)
- [Chapter 04: Phân Quyền Theo Vai Trò (RBAC) & Method Security (@PreAuthorize)](#phase-6-chapter-04)
- [Chapter 05: Cấu Hình CORS & CSRF Trong REST API](#phase-6-chapter-05)

### [PHASE 7: KIỂM THỬ, KIẾN TRÚC SẠCH & VẬN HÀNH DOCKER](#phase-7)

- [Chapter 01: Unit Testing với JUnit 5 & Assertions](#phase-7-chapter-01)
- [Chapter 02: Mocking Dependencies Trong Unit Test Với Mockito](#phase-7-chapter-02)
- [Chapter 03: Integration Testing Với @SpringBootTest, MockMvc & Testcontainers](#phase-7-chapter-03)
- [Chapter 04: Kiến Trúc Clean Architecture & Design Patterns Trong Spring Boot](#phase-7-chapter-04)
- [Chapter 05: Tự Động Tạo Tài Liệu API Với Swagger / OpenAPI 3 (springdoc)](#phase-7-chapter-05)
- [Chapter 06: Containerization – Đóng Gói Spring Boot & Database Với Docker & Docker Compose](#phase-7-chapter-06)

- [PHỤ LỤC: BẢNG TRA CỨU NHANH TRẢ LỜI PHỎNG VẤN SENIOR (CHEAT SHEET)](#phu-luc-cheat-sheet)

---

<div style="page-break-before: always;"></div>

<a id="phase-0"></a>

# PHASE 0: BACKEND CĂN BẢN (BASIC BACKEND)

---

<div style="page-break-before: always;"></div>

<a id="phase-0-chapter-01"></a>

# Chapter 01: Backend là gì? & Vai trò trong hệ thống

## 1. Khái niệm cơ bản
- **Backend** (hay Server‑Side) là phần xử lý *logic nghiệp vụ*, *quản lý dữ liệu* và *cung cấp API* cho Frontend (Client).
- Nhiệm vụ chính:
  1. Nhận yêu cầu (Request) từ Client.
  2. Xác thực/Phân quyền (Security).
  3. Thực thi nghiệp vụ (Business Logic).
  4. Tương tác với Database (CRUD).
  5. Trả kết quả (Response) về Client.

## 2. Các thành phần cốt lõi của một Backend

Để một hệ thống Backend vận hành hoàn chỉnh, nó được cấu thành từ 4 thành phần trụ cột sau:

```┌──────────────────────────────┐
│ Client: Web / Mobile         │
└──────────────┬───────────────┘
               │
               │ 1. HTTP Request
               ▼
┌──────────────────────────────┐
│ Web / App Server             │
│ Tomcat, Nginx                │
└──────────────┬───────────────┘
               │
               │ 2. Đi qua các tầng lọc
               ▼
┌──────────────────────────────────────────────┐
│ Middleware – "Người gác cổng"                │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │ Auth Filter                            │  │
│  │ → Kiểm tra Token                       │  │
│  └────────────────────────────────────────┘  │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │ Rate Limiter                           │  │
│  │ → Chống Spam / giới hạn Request        │  │
│  └────────────────────────────────────────┘  │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │ CORS & Logger                          │  │
│  │ → Kiểm tra CORS + Ghi log              │  │
│  └────────────────────────────────────────┘  │
└──────────────────────┬───────────────────────┘
                       │
                       │ 3. Hợp lệ → Chuyển tiếp
                       ▼
┌──────────────────────────────────────┐
│ Application Core                     │
│ Controller + Service                  │
│                                      │
│ → Xử lý nghiệp vụ                    │
└──────────────────┬───────────────────┘
                   │
                   │ 4. Đọc / Ghi dữ liệu
                   ▼
        ┌─────────────────────────┐
        │ Database                │
        │ MySQL / Redis / ...     │
        └────────────┬────────────┘
                     │
                     │ 5. Trả kết quả
                     ▼
┌──────────────────────────────────────┐
│ Application Core                     │
│ Controller + Service                  │
└──────────────────┬───────────────────┘
                   │
                   │ 6. Đóng gói JSON
                   ▼
┌──────────────────────────────┐
│ Web / App Server             │
│ Tomcat, Nginx                │
└──────────────┬───────────────┘
               │
               │ 7. HTTP Response
               ▼
┌──────────────────────────────┐
│ Client: Web / Mobile         │
└──────────────────────────────┘
```

```
Client
  │
  │ HTTP Request
  ▼
Web/App Server
  │
  ▼
Middleware
  ├── Auth Filter      → Xác thực
  ├── Rate Limiter     → Giới hạn request
  └── CORS & Logger    → CORS + Ghi log
  │
  │ Request hợp lệ
  ▼
Controller
  │
  ▼
Service
  │
  │ Đọc/Ghi
  ▼
Database
  │
  │ Kết quả
  ▼
Service
  │
  ▼
Controller
  │
  │ JSON Response
  ▼
Web/App Server
  │
  │ HTTP Response
  ▼
Client
```
- **Client → Server → Middleware → Controller → Service → Database → Service → Controller → Server → Client**
---

### 2.1. Server (Web Server & Application Server)
- **Bản chất:** Là một máy tính (phần cứng) chạy các phần mềm chuyên dụng (phần mềm máy chủ) luôn luôn hoạt động 24/7 để lắng nghe các kết nối từ Internet qua các cổng mạng (Port như `80` cho HTTP, `443` cho HTTPS, `8080` cho development).
- **Phân loại trong thực tế:**
  - **Web Server (ví dụ: Nginx, Apache):** Đứng ở lớp ngoài cùng, chuyên phục vụ các file tĩnh (HTML, CSS, ảnh), điều hướng lưu lượng (Reverse Proxy), cân bằng tải (Load Balancer) và mã hóa SSL/TLS.
  - **Application Server (ví dụ: Embedded Tomcat trong Spring Boot, Node.js runtime):** Chạy mã nguồn ứng dụng, quản lý vòng đời ứng dụng, cấp phát luồng (Thread) để thực thi logic Backend.

---

### 2.2. API (Application Programming Interface)
- **Bản chất:** Là "bản hợp đồng" giao tiếp chuẩn hóa giữa Frontend và Backend. Nếu Frontend là khách hàng và Backend là nhà bếp, thì API chính là **Menu món ăn**.
- **Đặc điểm:**
  - Định nghĩa rõ: Đường dẫn (Endpoint/URL), Phương thức gửi (HTTP Method: `GET`, `POST`, `PUT`, `DELETE`), Dữ liệu gửi đi (Request Payload) và Dữ liệu trả về (Response).
  - Chuẩn định dạng trao đổi phổ biến nhất hiện nay: **JSON (JavaScript Object Notation)** vì nhẹ, dễ đọc và đa ngôn ngữ đều hỗ trợ.

---

### 2.3. Middleware ("Người gác cổng" - The Gatekeeper)
- **Bản chất:** Là các đoạn mã hoặc tầng trung gian nằm **giữa** lúc Server vừa nhận được HTTP Request và **trước khi** Request đó được chuyển tới phần xử lý nghiệp vụ chính (Controller/Service).
- **Tại sao Middleware được gọi là "Người gác cổng"?**
  Bởi vì bất kỳ yêu cầu nào từ bên ngoài muốn vào được "ngôi nhà" (Logic nghiệp vụ & Database) đều phải đi qua sự kiểm tra nghiêm ngặt của các Middleware:
  1. **Authentication & Authorization (Soát vé):** Kiểm tra xem người dùng đã đăng nhập chưa (Token hợp lệ không?) và có quyền thực hiện hành động này không (ví dụ: User thường không được gọi API của Admin).
  2. **Rate Limiting & Throttling (Chống giẫm đạp / Chống DDoS):** Giới hạn số lượng request từ 1 địa chỉ IP (ví dụ: tối đa 60 request/phút). Nếu gửi quá nhiều sẽ bị chặn ngay (`429 Too Many Requests`).
  3. **CORS (Cross-Origin Resource Sharing - Kiểm tra hộ chiếu):** Kiểm soát xem trang web từ tên miền khác có được phép truy cập tài nguyên của API này hay không.
  4. **Logging & Monitoring (Camera an ninh):** Ghi chép lại lịch sử truy cập: IP nào, gọi URL nào, lúc mấy giờ, tốn bao nhiêu mili-giây để sau này điều tra sự cố.
  5. **Global Exception Handling (Đội cấp cứu):** Bắt toàn bộ các lỗi bất ngờ (Exception) xảy ra trong hệ thống, chuyển đổi thành định dạng lỗi JSON lịch sự gửi về cho Client, ngăn không cho hệ thống văng lỗi lộ thông tin nhạy cảm.

---

### 2.4. Database (Hệ cơ sở dữ liệu)
- **Bản chất:** Nơi lưu trữ dữ liệu lâu dài và bền vững (Persistent Storage). Khi server tắt hoặc khởi động lại, dữ liệu trong Database vẫn nguyên vẹn.
- **Phân loại chính:**
  - **Cơ sở dữ liệu quan hệ (RDBMS / SQL - ví dụ: MySQL, PostgreSQL):** Dữ liệu được tổ chức chặt chẽ thành các bảng (Table), có khóa chính, khóa ngoại, đảm bảo tính toàn vẹn tuyệt đối theo chuẩn **ACID** (rất quan trọng cho giao dịch tiền tệ, đặt hàng).
  - **Cơ sở dữ liệu phi quan hệ (NoSQL - ví dụ: MongoDB):** Dữ liệu dạng tài liệu (Document/JSON), linh hoạt thay đổi cấu trúc, phù hợp với dữ liệu lớn, tốc độ ghi cao (bình luận, tin nhắn, bài viết mạng xã hội).
  - **Bộ nhớ đệm (In-Memory Cache - ví dụ: Redis):** Lưu trữ tạm thời dữ liệu thường xuyên truy cập trên RAM để phản hồi cực nhanh (chỉ mất 1 - 2 ms), giúp giảm tải tới 80% cho Database chính.

## 3. Ví dụ thực tế – Luồng mua hàng
1. Người dùng nhấn **"Đặt hàng"** trên Frontend.
2. Frontend gửi **POST /orders** tới Backend.
3. Backend thực hiện:
   - Kiểm tra token (đã đăng nhập?).
   - Kiểm tra tồn kho trong DB.
   - Tính tổng tiền, áp dụng voucher, phí ship.
   - Gọi cổng thanh toán (VNPAY/Momo/Stripe).
   - Lưu đơn hàng, trả về **orderId** và trạng thái.

## 4. Điểm mạnh của Backend
- **Bảo mật**: Dữ liệu nhạy cảm luôn ở server, không để lộ trên client.
- **Quy mô**: Có thể mở rộng bằng cách tăng server, cache, load‑balancer.
- **Kiểm soát**: Business logic tập trung, dễ duy trì, dễ kiểm thử.

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Backend và Frontend khác nhau như thế nào?

| Tiêu chí | Frontend (Client-side) | Backend (Server-side) |
| :--- | :--- | :--- |
| **Môi trường thực thi** | Chạy trên thiết bị người dùng (Trình duyệt web, ứng dụng di động). | Chạy trên máy chủ (Server, Cloud, Docker container). |
| **Nhiệm vụ chính** | Hiển thị giao diện (UI), tương tác người dùng (UX), thu thập thao tác và hiển thị dữ liệu nhận được từ API. | Xử lý logic nghiệp vụ (Business Logic), xác thực bảo mật, quản lý giao dịch và lưu trữ dữ liệu (Database). |
| **Bảo mật** | **Không an toàn**: Code tải về máy người dùng nên có thể bị can thiệp, soi mã nguồn hoặc sửa đổi. | **Bảo mật cao**: Code và dữ liệu nằm kín trên server; kiểm soát quyền truy cập, bảo vệ dữ liệu nhạy cảm (mật khẩu, thanh toán). |
| **Công nghệ tiêu biểu** | HTML, CSS, JavaScript/TypeScript, React, Vue, Angular, Flutter... | Java (Spring Boot), Node.js, Python, Go, C# (.NET), MySQL, PostgreSQL, Redis, Kafka... |

> **Tóm tắt:** Frontend là *"bộ mặt"* (những gì người dùng nhìn thấy và tương tác), còn Backend là *"bộ não"* và *"động cơ"* (nơi tính toán, xử lý bảo mật và lưu trữ dữ liệu âm thầm đằng sau).

---

### 5.2. Tại sao chúng ta phải có lớp Service (Business Logic) giữa Controller và Repository?

Mô hình chuẩn 3 lớp trong ứng dụng Backend (3-Tier Architecture):
$$\text{Client} \longrightarrow \text{Controller} \longrightarrow \text{Service} \longrightarrow \text{Repository} \longrightarrow \text{Database}$$

Việc tách riêng lớp **Service** tuân theo nguyên lý **Separation of Concerns (SoC)** và **Single Responsibility Principle (SRP)**:
1. **Phân định rõ trách nhiệm:**
   - **Controller:** Chỉ lo giao tiếp HTTP (nhận URL, validate định dạng request body/DTO, trả về mã HTTP status 200, 400, 404, 500).
   - **Service:** Chứa toàn bộ **quy tắc nghiệp vụ** (kiểm tra tồn kho, áp dụng voucher, tính thuế, kiểm tra quyền nâng cao, gọi cổng thanh toán bên thứ ba).
   - **Repository:** Chỉ tương tác dữ liệu với Database (CRUD, SQL/JPA queries).
2. **Khả năng tái sử dụng (Reusability):**
   - Cùng một hàm nghiệp vụ trong Service có thể được gọi từ nhiều nơi: REST Controller, GraphQL, Kafka Consumer hoặc Job chạy nền định kỳ (Cron Scheduler).
3. **Quản lý Transaction (`@Transactional`):**
   - Một nghiệp vụ thường tương tác với **nhiều Repository cùng lúc** (ví dụ khi đặt hàng: trừ tiền, trừ tồn kho, tạo đơn hàng). Service là nơi gom cụm các thao tác này vào một Transaction để đảm bảo tính toàn vẹn (rollback nếu có bước thất bại).
4. **Dễ viết Unit Test:**
   - Kiểm thử logic nghiệp vụ độc lập mà chỉ cần Mock Repository, không cần khởi chạy môi trường HTTP/Web Server.

---

### 5.3. JWT được sử dụng ở đâu trong luồng trên?

```
┌──────────────────────┐
│  Frontend / Mobile   │
│       (Client)       │
└──────────┬───────────┘
           │
           │ Giai đoạn 1: Đăng nhập lấy Token
           │
           │ POST /auth/login
           │ (username, password)
           ▼
┌──────────────────────┐
│ Security Filter      │
│    (Auth Layer)      │
└──────────────────────┘
           │
           │
           ▼
┌──────────────────────┐
│     Controller       │
└──────────┬───────────┘
           │
           │ Xác thực tài khoản
           ▼
┌──────────────────────┐
│    Service Layer     │
└──────────┬───────────┘
           │
           │ Kiểm tra mật khẩu (hash)
           ▼
┌──────────────────────┐
│      Database        │
└──────────┬───────────┘
           │
           │ Kết quả xác thực
           ▼
┌──────────────────────┐
│    Service Layer     │
│                      │
│ Ký & tạo JWT         │
│ payload:             │
│ - userId             │
│ - roles              │
│ - exp                 │
└──────────┬───────────┘
           │
           │ Trả JWT
           ▼
┌──────────────────────┐
│     Controller       │
└──────────┬───────────┘
           │
           │ Token (JWT)
           ▼
┌──────────────────────┐
│  Frontend / Mobile   │
│       (Client)       │
└──────────────────────┘


══════════════════════════════════════════════════════════════
       GIAI ĐOẠN 2: GỌI API NGHIỆP VỤ (POST /orders)
══════════════════════════════════════════════════════════════

┌──────────────────────┐
│  Frontend / Mobile   │
│       (Client)       │
└──────────┬───────────┘
           │
           │ POST /orders
           │ Authorization:
           │ Bearer <JWT>
           ▼
┌──────────────────────┐
│ Security Filter      │
│    (Auth Layer)      │
└──────────┬───────────┘
           │
           │ Giải mã JWT
           │ Kiểm tra:
           │ ✓ Chữ ký
           │ ✓ Hạn dùng (exp)
           ▼
        ┌─────────────────────┐
        │ Token hợp lệ ?      │
        └─────────┬───────────┘
             ┌────┴────┐
             │         │
           KHÔNG       CÓ
             │         │
             ▼         ▼
   ┌────────────────┐  ┌──────────────────────────┐
   │ 401 Unauthorized│  │ Đưa UserInfo / Roles    │
   │ Chặn ngay       │  │ vào SecurityContext     │
   │ tại Filter      │  └────────────┬─────────────┘
   └───────┬────────┘               │
           │                        │ Cho phép đi tiếp
           ▼                        ▼
      ┌───────────┐       ┌──────────────────────┐
      │  Client   │       │     Controller       │
      │ nhận 401  │       └──────────┬───────────┘
      └───────────┘                  │
                                     │ Xử lý tạo đơn hàng
                                     ▼
                           ┌──────────────────────┐
                           │    Service Layer     │
                           └──────────┬───────────┘
                                      │
                                      │ Lưu đơn hàng
                                      ▼
                           ┌──────────────────────┐
                           │      Database        │
                           └──────────┬───────────┘
                                      │
                                      │ Thành công
                                      ▼
                           ┌──────────────────────┐
                           │     Controller       │
                           └──────────┬───────────┘
                                      │
                                      │ 200 OK
                                      ▼
                           ┌──────────────────────┐
                           │  Frontend / Mobile   │
                           │       (Client)       │
                           └──────────────────────┘
```

- **Vị trí trong kiến trúc:** JWT nằm ở **Security Filter / Interceptor** (tầng bảo mật ngay cổng vào của Backend, trước khi request chạm tới `Controller`).
- Nếu Token không hợp lệ hoặc hết hạn, request bị chặn ngay lập tức (`401 Unauthorized`), giúp bảo vệ Controller, Service và Database khỏi việc phải tốn tài nguyên xử lý request rác.

---

### 5.4. Khi nào nên dùng Synchronous vs Asynchronous request?

#### **A. Synchronous (Đồng bộ - Blocking):**
- **Cơ chế:** Client gửi request và **chờ đợi** Server xử lý xong mới nhận kết quả để tiếp tục bước sau.
- **Khi nào nên dùng:**
  - Cần dữ liệu ngay tức thì để hiển thị cho người dùng: Đăng nhập, lấy thông tin cá nhân, kiểm tra số dư ví, xem chi tiết sản phẩm.
  - Tác vụ xử lý nhanh (dưới vài trăm mili-giây).
  - Nghiệp vụ có các bước phụ thuộc chặt chẽ vào kết quả của bước liền trước.

#### **B. Asynchronous (Bất đồng bộ - Non-blocking / Background Processing):**
- **Cơ chế:** Client gửi yêu cầu, Server tiếp nhận ngay (trả về mã `202 Accepted` hoặc Task/Job ID) rồi đẩy việc vào hàng đợi (Queue như RabbitMQ, Kafka, hoặc Thread Pool ngầm) để xử lý sau.
- **Khi nào nên dùng:**
  - **Tác vụ tốn nhiều thời gian:** Xuất/nhập file Excel lớn hàng trăm ngàn dòng, render/encode video, tạo báo cáo PDF nặng, gửi email thông báo hoặc SMS OTP.
  - **Giảm tải hệ thống khi có lưu lượng tăng vọt (Peak Traffic):** Xếp hàng xử lý giao dịch flash-sale, đặt vé xem phim để tránh làm sập Database.
  - **Tác vụ gọi dịch vụ bên thứ ba:** Bắn webhook, ghi log phân tích tracking hành vi người dùng.

---

<div style="page-break-before: always;"></div>

<a id="phase-0-chapter-02"></a>

# Chapter 02: Kiến trúc Client‑Server & Vòng đời Request‑Response

## 1. Khái niệm
- **Client‑Server** là mô hình 2 lớp cơ bản: **Client** (frontend, trình duyệt, app) gửi **request** tới **Server** (backend) và nhận **response**.
- Server chịu trách nhiệm **xử lý nghiệp vụ**, **truy cập dữ liệu**, **bảo mật** và **trả kết quả**.

## 2. Thành phần chính

```
┌────────────────────────────────────────────────────────┐
│ Client: Web / Mobile (Browser / App)                   │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ 1. Gửi HTTP Request (GET, POST...)
                            ▼
┌────────────────────────────────────────────────────────┐
│ Load Balancer (Nginx / HAProxy - Tùy chọn)             │
│ → Cân bằng tải & phân phối request                     │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ 2. Forward Request tới Server rảnh
                            ▼
┌────────────────────────────────────────────────────────┐
│ Backend Server (Web Server / App Server)               │
│                                                        │
│   ┌────────────────────────────────────────────────┐   │
│   │ 1. Xác thực & Phân quyền (Auth Filter)         │   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 2. Xử lý nghiệp vụ (Business Logic - Service)  │   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 3. Đọc / Ghi dữ liệu (Repository → Database)   │   │
│   └────────────────────────────────────────────────┘   │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ 3. Trả về HTTP Response
                            ▼
┌────────────────────────────────────────────────────────┐
│ Load Balancer                                          │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ 4. Chuyển tiếp Response (JSON / HTML)
                            ▼
┌────────────────────────────────────────────────────────┐
│ Client: Web / Mobile                                   │
└────────────────────────────────────────────────────────┘
```

```
Client                      Load Balancer                   Backend Server
  │                               │                               │
  │─── 1. HTTP Request (GET/POST)─►                               │
  │                               │─── 2. Forward Request ────────►
  │                               │                               │ ──┐
  │                               │                               │   │ Auth → Logic → DB
  │                               │                               │ ◄─┘
  │                               │◄── 3. HTTP Response ──────────│
  │◄── 4. Response (JSON/HTML) ───│                               │
  │                               │                               │
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

```
┌──────────────────────────────┐                ┌──────────────────────────────┐
│  Client (Trình duyệt / App)  │                │ Backend Server (Port 80/443) │
└──────────────┬───────────────┘                └──────────────┬───────────────┘
               │                                               │
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │   GIAI ĐOẠN 1: BẮT TAY 3 BƯỚC (TCP 3-WAY HANDSHAKE)
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │                                               │
               │ 1. Gói SYN (seq = X)                          │
               │ ────────────────────────────────────────────► │ "Tôi muốn kết nối,
               │                                               │  seq của tôi là X"
               │                                               │
               │ 2. Gói SYN-ACK (seq = Y, ack = X+1)           │
               │ ◄──────────────────────────────────────────── │ "Tôi đồng ý (ACK X+1),
               │                                               │  seq của tôi là Y"
               │                                               │
               │ 3. Gói ACK (ack = Y+1)                        │
               │ ────────────────────────────────────────────► │ "Đã nhận (ACK Y+1).
               │                                               │  Kết nối sẵn sàng!"
               │                                               │
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │   GIAI ĐOẠN 2: TRUYỀN DỮ LIỆU HTTP (DATA TRANSFER)
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │                                               │
               │ 4. Gửi HTTP Request (GET /api/v1/products)    │
               │ ────────────────────────────────────────────► │ Xử lý nghiệp vụ...
               │                                               │
               │ 5. Gửi HTTP Response (200 OK + JSON)          │
               │ ◄──────────────────────────────────────────── │ Trả kết quả JSON
               │                                               │
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │   GIAI ĐOẠN 3: ĐÓNG KẾT NỐI (TCP 4-WAY HANDSHAKE)
═══════════════╪═══════════════════════════════════════════════╪═══════════════
               │                                               │
               │ 1. Gói FIN (Client muốn đóng kết nối)         │
               │ ────────────────────────────────────────────► │
               │ 2. Gói ACK (Server xác nhận yêu cầu đóng)     │
               │ ◄──────────────────────────────────────────── │
               │ 3. Gói FIN (Server cũng đóng kết nối)         │
               │ ◄──────────────────────────────────────────── │
               │ 4. Gói ACK (Client xác nhận -> Đóng hoàn toàn)│
               │ ────────────────────────────────────────────► │
               │                                               │
               ▼                                               ▼
         [Đóng kết nối]                                  [Đóng kết nối]
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

<div style="page-break-before: always;"></div>

<a id="phase-0-chapter-03"></a>

# Chapter 03: Networking, IP, Port & DNS

## 1. Địa chỉ IP & Port
- **IP (Internet Protocol) address** là địa chỉ duy nhất cho mỗi thiết bị trên mạng.
  - IPv4: 32‑bit, dạng `192.168.0.1` (≈ 4,3 tỷ địa chỉ).
  - IPv6: 128‑bit, dạng `2001:0db8:85a3:0000:0000:8a2e:0370:7334` (không còn lo hết địa chỉ).
- **Port** là số hiệu 0‑65535 dùng để phân biệt các dịch vụ trên cùng một IP.
  - Port 80 → HTTP, 443 → HTTPS, 3306 → MySQL, 5432 → PostgreSQL, 8080 → Tomcat/Spring Boot.
- Khi client muốn gọi API, nó sẽ **kết nối tới `IP:Port`** của server.

## 2. TCP vs UDP
| Thuộc tính | TCP | UDP |
|------------|-----|-----|
| Kết nối | Three‑way handshake (đảm bảo giao tiếp ổn định) | Không kết nối, gửi gói độc lập |
| Độ tin cậy | Đảm bảo thứ tự, retransmission nếu mất gói | Không bảo guarantee, tốc độ cao |
| Ứng dụng | Web (HTTP/HTTPS), email, file transfer | Streaming video, VoIP, DNS query |

## 3. DNS (Domain Name System) – "Cuốn danh bạ Internet"
- **Bản chất:** Con người dễ nhớ tên chữ (`google.com`, `shopee.vn`), nhưng máy tính chỉ hiểu địa chỉ số IP (`142.250.190.46`). DNS đóng vai trò như **cuốn danh bạ điện thoại**, tra cứu từ "Tên người" sang "Số điện thoại".
- **Quy trình phân giải DNS (DNS Resolution Flow):**

```
┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│  Trình duyệt  │     │  OS / Cache   │     │ DNS Resolver  │     │  Root Server  │     │  TLD Server   │     │  Auth Server  │
│   (Browser)   │     │ (Local Cache) │     │ (ISP/8.8.8.8) │     │      (.)      │     │    (.com)     │     │ (example.com) │
└───────┬───────┘     └───────┬───────┘     └───────┬───────┘     └───────┬───────┘     └───────┬───────┘     └───────┬───────┘
        │                     │                     │                     │                     │                     │
        │ 1. https://api.example.com                │                     │                     │                     │
        │ ──────────────────► │                     │                     │                     │                     │
        │                     │                     │                     │                     │                     │
        │ [Trường hợp 1: Có sẵn trong Cache]        │                     │                     │                     │
        │ ◄- Trả IP ngay (0ms)│                     │                     │                     │                     │
        │                     │                     │                     │                     │                     │
        │ [Trường hợp 2: Chưa có trong Cache]       │                     │                     │                     │
        │                     │ 2. Nhờ phân giải hộ │                     │                     │                     │
        │                     │ ──────────────────► │                     │                     │                     │
        │                     │                     │                     │                     │                     │
        │                     │                     │ 3. Hỏi: Quản lý .com?                     │                     │
        │                     │                     │ ──────────────────► │                     │                     │
        │                     │                     │ ◄- IP của TLD .com ─│                     │                     │
        │                     │                     │                     │                     │                     │
        │                     │                     │ 4. Hỏi: Ai giữ example.com?               │                     │
        │                     │                     │ ────────────────────────────────────────► │                     │
        │                     │                     │ ◄- IP của Auth Server (example.com) ──────│                     │
        │                     │                     │                     │                     │                     │
        │                     │                     │ 5. Hỏi: IP của api.example.com là gì?                           │
        │                     │                     │ ──────────────────────────────────────────────────────────────► │
        │                     │                     │ ◄- IP: 203.0.113.12 (A Record, TTL=300s) ───────────────────────│
        │                     │                     │                     │                     │                     │
        │                     │ 6. Trả IP + Lưu cache                     │                     │                     │
        │                     │ ◄────────────────── │                     │                     │                     │
        │ 7. Trả IP: 203.0.113.12                   │                     │                     │                     │
        │ ◄────────────────── │                     │                     │                     │                     │
        ▼                     ▼                     ▼                     ▼                     ▼                     ▼
```

- **Các Record DNS phổ biến:**
  - `A (Address)`: Ánh xạ tên miền -> Địa chỉ **IPv4** (ví dụ: `api.example.com -> 203.0.113.12`).
  - `AAAA`: Ánh xạ tên miền -> Địa chỉ **IPv6**.
  - `CNAME (Canonical Name)`: Tên miền bí danh trỏ tới một tên miền khác (ví dụ: `www.example.com -> example.com`).
  - `MX (Mail Exchange)`: Chỉ định máy chủ nhận email của tên miền.
  - `TXT`: Lưu trữ văn bản tự do, dùng để xác thực quyền sở hữu tên miền, cấu hình bảo mật email chống giả mạo (SPF, DKIM).
- **TTL (Time-To-Live):** Thời gian (tính bằng giây) mà các máy chủ trung gian được phép lưu cache bản ghi DNS. Ví dụ `TTL = 300` (5 phút). Sau thời gian này, cache hết hạn và máy chủ sẽ phải hỏi lại Authoritative server.

---

## 4. Công cụ kiểm tra mạng qua CLI
```bash
# 1. ping: Kiểm tra xem máy chủ đích có online không và đo độ trễ (latency RTT)
ping google.com

# 2. nslookup: Tra cứu địa chỉ IP và máy chủ DNS đang giải quyết tên miền
nslookup google.com

# 3. traceroute (Windows dùng: tracert): Theo dõi đường đi qua bao nhiêu trạm router (hops) để đến đích
tracert 8.8.8.8

# 4. curl -I: Kiểm tra kết nối HTTP/HTTPS, Header phản hồi và Status Code
curl -I https://google.com
```

---

## 5. Ví dụ thực tế – Gọi API Backend
```http
GET /api/v1/products HTTP/1.1
Host: api.example.com   # DNS giải thành IP (203.0.113.12)
Port: 443               # HTTPS, kết nối TCP an toàn SSL/TLS
```
- **Ý nghĩa Port trong đời thực:**
  - Hãy tưởng tượng địa chỉ IP giống như **Địa chỉ của một tòa nhà chung cư**.
  - Số Port chính là **Số phòng căn hộ** bên trong tòa nhà đó:
    - Phòng `80` / `443`: Tiếp khách Web (HTTP/HTTPS).
    - Phòng `3306`: Quản lý kho hàng Database (MySQL).
    - Phòng `8080`: Xưởng chế tạo Java (Tomcat / Spring Boot).
  - Nhờ có Port, một máy chủ duy nhất có thể chạy song song hàng chục dịch vụ khác nhau mà không hề bị xung đột hay nhầm lẫn gói tin.

---

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. IPv4 và IPv6 khác nhau như thế nào? Lợi ích của IPv6?
- **Khác biệt:**
  - **IPv4:** Độ dài 32-bit (dạng 4 nhóm số thập phân, vd: `192.168.1.1`), cung cấp tối đa khoảng $2^{32} \approx 4,3$ tỷ địa chỉ. Hiện nay địa chỉ IPv4 toàn cầu đã cạn kiệt, buộc phải dùng kỹ thuật NAT (Network Address Translation) để chia sẻ chung IP công cộng.
  - **IPv6:** Độ dài 128-bit (dạng 8 nhóm số thập lục phân, vd: `2001:0db8:85a3::7334`), cung cấp tới $2^{128} \approx 3,4 \times 10^{38}$ địa chỉ (đủ để gán cho mỗi hạt cát trên trái đất một địa chỉ IP).
- **Lợi ích IPv6:** Không lo cạn kiệt địa chỉ, loại bỏ hoàn toàn sự phức tạp của NAT, tích hợp sẵn giao thức mã hóa bảo mật IPSec ở tầng mạng và định tuyến gói tin nhanh hơn.

### 6.2. Khi một API chậm, làm sao kiểm tra vấn đề do DNS, Network Latency hay Server Processing?
Sử dụng công cụ `curl` với các tham số đo thời gian chuyên sâu (`curl -w`):
```bash
curl -o /dev/null -s -w 'DNS: %{time_namelookup}s | Connect TCP: %{time_connect}s | TLS: %{time_appconnect}s | First Byte (Server): %{time_starttransfer}s | Total: %{time_total}s\n' https://api.example.com/health
```
- Nếu `time_namelookup` lớn (> 200ms) $\rightarrow$ **Nghẽn do DNS Resolution** (cần đổi DNS Server hoặc tăng TTL).
- Nếu `time_connect` hoặc `time_appconnect` lớn $\rightarrow$ **Nghẽn do Mạng (Network Latency/Khoảng cách địa lý)**.
- Nếu `time_starttransfer` (thời gian từ lúc gửi xong request đến khi nhận byte đầu tiên - TTFB) lớn $\rightarrow$ **Server Processing chậm** (Backend code query DB chậm, thiếu Index hoặc nghẽn CPU/RAM).

### 6.3. Giải thích TCP 3-way handshake chi tiết (SYN, SYN-ACK, ACK)
- **Bước 1 (SYN):** Client sinh ngẫu nhiên số thứ tự $ISN_C = X$ và gửi gói tin cờ `SYN = 1` tới Server để yêu cầu mở kết nối. Trạng thái Client chuyển thành `SYN_SENT`.
- **Bước 2 (SYN-ACK):** Server nhận được, đồng ý kết nối. Server sinh số thứ tự $ISN_S = Y$, gửi lại gói tin có cờ `SYN = 1` và `ACK = X + 1` (xác nhận đã nhận được $X$). Trạng thái Server thành `SYN_RCVD`.
- **Bước 3 (ACK):** Client nhận được SYN-ACK, gửi lại gói tin xác nhận `ACK = Y + 1`. Trạng thái cả hai chuyển sang `ESTABLISHED`. Lúc này kết nối tin cậy 2 chiều hoàn tất và dữ liệu HTTP bắt đầu truyền tải.

### 6.4. Tại sao DNS Caching quan trọng? TTL ảnh hưởng thế nào đến thay đổi IP?
- **Tầm quan trọng:** Tra cứu DNS qua nhiều cấp server tốn từ 50ms - vài trăm mili-giây. Caching tại Trình duyệt, OS và ISP giúp trả về IP ngay lập tức (0ms), giảm tải cho toàn bộ hệ thống DNS trên Internet.
- **Ảnh hưởng của TTL khi đổi IP:**
  - Nếu đặt **TTL quá lớn** (ví dụ 1 ngày = 86400s): Khi bạn chuyển server sang IP mới, người dùng vẫn tiếp tục trỏ về IP cũ trong suốt 24 giờ do cache chưa hết hạn (dẫn tới gián đoạn dịch vụ).
  - **Kinh nghiệm thực tế (DevOps):** Trước khi chuyển đổi IP máy chủ 2 ngày, hạ TTL xuống thấp (ví dụ: `300` giây - 5 phút). Khi chuyển IP xong và hệ thống chạy ổn định, nâng TTL lên lại (ví dụ: `3600` giây) để tận dụng cache.

### 6.5. Khi muốn load-balance các service, bạn có thể dùng DNS Round-Robin? Nhược điểm?
- **DNS Round-Robin là gì:** Cấu hình 1 domain trỏ tới nhiều A-Record (nhiều IP máy chủ). DNS Server sẽ xoay vòng danh sách IP trả về cho mỗi client khác nhau để san sẻ tải.
- **Nhược điểm chí mạng:**
  1. **Không biết tình trạng máy chủ (No Health Check):** Nếu 1 trong các server bị sập (die), DNS vẫn vô tư phát IP đó cho người dùng, khiến người dùng gặp lỗi trắng trang hoặc không thể kết nối.
  2. **Vấn đề do Cache (TTL):** Trình duyệt hoặc nhà mạng ISP lưu cache IP đó hàng chục phút, khiến lưu lượng không thể phân bổ đều và không thể ngắt người dùng khỏi server gặp sự cố ngay lập tức.
- **Khuyến nghị:** DNS Round-Robin chỉ nên dùng cho tầng phân phối vùng địa lý (GeoDNS). Để cân bằng tải thực tế cho Backend, nên dùng Load Balancer chuyên dụng (Nginx, HAProxy, AWS ALB) có cơ chế Health Check tự động loại bỏ server lỗi.

---

<div style="page-break-before: always;"></div>

<a id="phase-0-chapter-04"></a>

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
```
┌────────────────────────────────────────────────────────┐
│ Client / Browser (Web / Mobile App)                    │
└───────────────────────────┬────────────────────────────┘
                            │ ▲
               1. Gửi HTTPS │ │ 6. Trả Response
                            ▼ │
┌────────────────────────────────────────────────────────┐
│ Load Balancer (Nginx / HAProxy)                        │
└───────────────────────────┬────────────────────────────┘
                            │ ▲
           2. Reverse Proxy │ │ 5. Trả JSON / HTML
                            ▼ │
┌────────────────────────────────────────────────────────┐
│ Web Server (Nginx / Apache)                            │
│ → Phục vụ static file, SSL termination                 │
└───────────────────────────┬────────────────────────────┘
                            │ ▲
           3. Proxy Request │ │ 4. Trả kết quả xử lý
                            ▼ │
┌────────────────────────────────────────────────────────┐
│ Application Server (Tomcat / Spring Boot)              │
│ → Xử lý Business Logic, Transaction, Security          │
└───────────────────────────┬────────────────────────────┘
                            │ ▲
          JDBC / JPA Query  │ │ Result Set
                            ▼ │
┌────────────────────────────────────────────────────────┐
│ Database (MySQL / PostgreSQL / Redis)                  │
└────────────────────────────────────────────────────────┘
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

<div style="page-break-before: always;"></div>

<a id="phase-1"></a>

# PHASE 1: JAVA CORE NỀN TẢNG (CORE LANGUAGE & JVM)

---

<div style="page-break-before: always;"></div>

<a id="phase-1-chapter-01"></a>

# Chapter 01: Biến, Kiểu dữ liệu & Ép kiểu (Variables, Data Types & Casting)

## 1. Biến (Variable) là gì?
- Biến là **ô nhớ** trong RAM dùng để lưu trữ giá trị. Mỗi biến gồm 3 phần:
  - **Kiểu dữ liệu** (Data Type): quyết định kích thước ô nhớ và loại giá trị.
  - **Tên biến** (Identifier): tuân theo quy tắc camelCase.
  - **Giá trị** (Value): giá trị được gán.

```java
int age = 25;           // kiểu int, tên "age", giá trị 25
String name = "Minh";   // kiểu String (tham chiếu), tên "name"
boolean isActive = true; // kiểu boolean
```

## 2. Hai nhóm kiểu dữ liệu

### 2.1 Kiểu nguyên thuỷ (Primitive Types) – 8 kiểu
Lưu **trực tiếp giá trị** trên **Stack**, kích thước cố định.

| Kiểu | Kích thước | Phạm vi | Giá trị mặc định | Ví dụ |
|------|-----------|---------|-------------------|-------|
| `byte` | 1 byte | −128 → 127 | 0 | `byte b = 100;` |
| `short` | 2 bytes | −32 768 → 32 767 | 0 | `short s = 30000;` |
| `int` | 4 bytes | −2³¹ → 2³¹ − 1 (~2.1 tỷ) | 0 | `int count = 1000;` |
| `long` | 8 bytes | −2⁶³ → 2⁶³ − 1 | 0L | `long id = 99999999L;` |
| `float` | 4 bytes | ≈ ±3.4 × 10³⁸ (7 chữ số thập phân) | 0.0f | `float pi = 3.14f;` |
| `double` | 8 bytes | ≈ ±1.7 × 10³⁰⁸ (15 chữ số thập phân) | 0.0d | `double price = 19.99;` |
| `char` | 2 bytes | Ký tự Unicode (0 → 65 535) | '\u0000' | `char grade = 'A';` |
| `boolean` | 1 bit* | `true` hoặc `false` | false | `boolean ok = true;` |

> *Lưu ý: JVM thực tế cấp ít nhất 1 byte cho boolean.

### 2.2 Kiểu tham chiếu (Reference Types)
Lưu **địa chỉ** (reference) trỏ tới **đối tượng trên Heap**.

- `String`, `Integer`, `Double`, `Boolean` (Wrapper Classes)
- Mảng (`int[]`, `String[]`), Class tự tạo (`User`, `Product`)
- Giá trị mặc định: `null`

```java
String greeting = "Hello";   // greeting chứa ĐỊA CHỈ trỏ tới "Hello" trên Heap
int[] numbers = {1, 2, 3};   // numbers chứa địa chỉ trỏ tới mảng trên Heap
User user = new User();      // user chứa địa chỉ trỏ tới object User trên Heap
```

### 2.3 So sánh nhanh

```
┌──────────────────────────────────────┐          ┌──────────────────────────────────────┐
│             STACK MEMORY             │          │             HEAP MEMORY              │
├──────────────────────────────────────┤          ├──────────────────────────────────────┤
│                                      │          │                                      │
│  age = 25  (Primitive type)          │          │                                      │
│                                      │          │                                      │
│  greeting = 0x7A3F (Reference type) ─┼──────────┼──► "Hello" (String Object tại 0x7A3F)│
│                                      │          │                                      │
└──────────────────────────────────────┘          └──────────────────────────────────────┘
```

| Tiêu chí | Primitive | Reference |
|----------|-----------|-----------|
| Lưu ở đâu? | Stack (giá trị trực tiếp) | Stack (địa chỉ) + Heap (đối tượng) |
| Giá trị mặc định? | 0, false, '\u0000' | `null` |
| So sánh bằng `==`? | So sánh **giá trị** | So sánh **địa chỉ bộ nhớ** (không phải nội dung!) |
| Kích thước? | Cố định (1‑8 bytes) | Tuỳ thuộc đối tượng |

## 3. Wrapper Classes & Autoboxing
- Mỗi kiểu primitive có 1 Wrapper Class tương ứng: `int` → `Integer`, `double` → `Double`, `boolean` → `Boolean`…
- **Autoboxing**: tự động chuyển primitive → Wrapper.
- **Unboxing**: tự động chuyển Wrapper → primitive.

```java
int a = 10;
Integer b = a;         // Autoboxing: int → Integer
int c = b;             // Unboxing: Integer → int

// Cẩn thận: Unboxing null gây NullPointerException!
Integer x = null;
int y = x;             // ❌ NullPointerException tại runtime!
```

## 4. Ép kiểu (Type Casting)

### 4.1 Ép kiểu ngầm định (Widening / Implicit Casting)
Chuyển từ kiểu **nhỏ → lớn**, Java tự động thực hiện, **không mất dữ liệu**.

```
byte → short → int → long → float → double
```

```java
int num = 100;
long bigNum = num;      // int → long (tự động)
double d = bigNum;      // long → double (tự động)
System.out.println(d);  // 100.0
```

### 4.2 Ép kiểu tường minh (Narrowing / Explicit Casting)
Chuyển từ kiểu **lớn → nhỏ**, **có thể mất dữ liệu** (tràn số / mất phần thập phân).

```java
double pi = 3.14159;
int intPi = (int) pi;      // Ép tường minh: mất phần thập phân → intPi = 3
System.out.println(intPi);  // 3

long bigValue = 130;
byte smallValue = (byte) bigValue;  // ⚠️ Tràn số! 130 > 127 → smallValue = -126
System.out.println(smallValue);     // -126 (overflow!)
```

### 4.3 Lỗi phổ biến khi chia số nguyên
```java
int a = 5, b = 2;
System.out.println(a / b);           // 2 (mất phần thập phân vì int / int = int)
System.out.println((double) a / b);  // 2.5 (ép 1 vế sang double trước khi chia)
```

## 5. Toán tử (Operators)

### 5.1 Toán tử số học
| Toán tử | Ý nghĩa | Ví dụ |
|---------|---------|-------|
| `+` | Cộng | `5 + 3` → 8 |
| `-` | Trừ | `5 - 3` → 2 |
| `*` | Nhân | `5 * 3` → 15 |
| `/` | Chia | `5 / 2` → 2 (int), `5.0 / 2` → 2.5 |
| `%` | Chia lấy dư (Modulo) | `5 % 2` → 1 |

### 5.2 Toán tử so sánh & logic
```java
// So sánh: ==, !=, >, <, >=, <=
// Logic:   && (AND), || (OR), ! (NOT)
if (age >= 18 && isActive) {
    System.out.println("Đủ điều kiện");
}
```

### 5.3 Toán tử tăng/giảm
```java
int i = 5;
System.out.println(i++);  // In 5 rồi tăng i lên 6 (post-increment)
System.out.println(++i);  // Tăng i lên 7 rồi in 7 (pre-increment)
```

### 5.4 Toán tử gán mở rộng
```java
int x = 10;
x += 5;   // x = x + 5 → 15
x -= 3;   // x = x - 3 → 12
x *= 2;   // x = x * 2 → 24
x /= 4;   // x = x / 4 → 6
x %= 4;   // x = x % 4 → 2
```

## 6. Hằng số (Constants) với `final`
```java
final double TAX_RATE = 0.1;   // Không thể thay đổi giá trị sau khi gán
// TAX_RATE = 0.2;             // ❌ Compilation Error
```

- Quy ước đặt tên hằng số: **UPPER_SNAKE_CASE**

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Primitive và Reference type khác nhau thế nào? Lưu ở đâu trong bộ nhớ?
- **Primitive (Nguyên thuỷ - 8 kiểu):**
  - Lưu **trực tiếp giá trị nhị phân** trong vùng nhớ **Stack** (hoặc nằm gọn trong object trên Heap nếu là biến instance của class).
  - Không có phương thức đi kèm, kích thước cố định (1 - 8 bytes), tốc độ truy xuất cực nhanh.
- **Reference (Tham chiếu):**
  - Biến chỉ lưu **địa chỉ con trỏ (Memory Address)** trên vùng nhớ **Stack**.
  - Đối tượng thực sự (Object Data) luôn được cấp phát động trên vùng nhớ **Heap**.
  - Có các phương thức (`equals()`, `hashCode()`, `toString()`), giá trị mặc định là `null`.

### 7.2. Toán tử `==` hoạt động khác nhau thế nào khi dùng với `int` và `Integer`?
- **Với `int` (Primitive):** `==` so sánh **giá trị số học**.
  ```java
  int a = 10, b = 10;
  System.out.println(a == b); // true (vì cùng mang giá trị 10)
  ```
- **Với `Integer` (Reference Object):** `==` so sánh **địa chỉ ô nhớ** (hai biến có trỏ cùng một object trên Heap hay không), chứ KHÔNG so sánh giá trị nội dung (để so sánh giá trị phải dùng `.equals()`).
  - *Cạm bẫy Integer Cache (-128 đến 127):*
    ```java
    Integer x = 100, y = 100;
    System.out.println(x == y); // true (do nằm trong Integer Cache từ -128 đến 127, JVM tái sử dụng object)

    Integer a = 200, b = 200;
    System.out.println(a == b); // false (vượt ngoài cache, tạo 2 object độc lập trên Heap!)
    System.out.println(a.equals(b)); // true (luôn dùng .equals() để so sánh đối tượng)
    ```

### 7.3. Giải thích Autoboxing / Unboxing và khi nào có thể gây NullPointerException?
- **Autoboxing:** Trình biên dịch tự động chuyển kiểu nguyên thuỷ sang Wrapper class (vd: `int` $\rightarrow$ `Integer.valueOf()`).
- **Unboxing:** Trình biên dịch tự động gọi `.intValue()` để lấy giá trị nguyên thuỷ từ Wrapper class.
- **Nguy cơ gây `NullPointerException` (NPE):**
  Xảy ra khi ta thực hiện phép toán hoặc gán một Wrapper object đang mang giá trị `null` về kiểu nguyên thuỷ:
  ```java
  Integer count = null;
  int total = count; // ❌ Ném ra NullPointerException tại runtime vì JVM âm thầm gọi count.intValue()
  ```

### 7.4. Kết quả của `5 / 2` khác `5.0 / 2` như thế nào? Tại sao?
- `5 / 2` $\rightarrow$ Kết quả là `2` (kiểu `int`). Vì cả `5` và `2` đều là số nguyên (`int`), phép chia nguyên trong Java sẽ cắt bỏ toàn bộ phần thập phân (không làm tròn).
- `5.0 / 2` $\rightarrow$ Kết quả là `2.5` (kiểu `double`). Khi một trong hai toán hạng là kiểu số thực (`double`), Java sẽ tự động ép toán hạng còn lại (`2`) thành `2.0` (Widening Casting) rồi thực hiện phép chia số thực.

### 7.5. Khi ép `(byte) 130`, kết quả là bao nhiêu? Giải thích cơ chế overflow
- **Kết quả:** `-126`
- **Giải thích cơ chế tràn số (Overflow):**
  - Kiểu `byte` trong Java có kích thước 8-bit có dấu (Signed 2's Complement), phạm vi từ `-128` đến `127`.
  - Số nguyên `130` dưới dạng nhị phân 32-bit: `00000000 00000000 00000000 10000010`.
  - Khi ép kiểu tường minh sang `(byte)`, Java cắt lấy đúng **8 bit cuối**: `10000010`.
  - Bit đầu tiên là `1` đại diện cho số âm.
  - Giá trị bù 2 của `10000010` là: $-(2^7) + 2^1 = -128 + 2 = -126$.

---

<div style="page-break-before: always;"></div>

<a id="phase-1-chapter-02"></a>

# Chapter 02: Cấu trúc Điều khiển & Vòng lặp (Control Flow)

## 1. Cấu trúc rẽ nhánh

### 1.1 if – else if – else
```java
int score = 75;

if (score >= 90) {
    System.out.println("Xuất sắc");
} else if (score >= 70) {
    System.out.println("Khá");       // ← In ra dòng này
} else if (score >= 50) {
    System.out.println("Trung bình");
} else {
    System.out.println("Yếu");
}
```

- Sử dụng khi có **nhiều điều kiện** cần kiểm tra tuần tự.
- Điều kiện nào đúng **trước** sẽ thực thi, các nhánh sau **bị bỏ qua**.

### 1.2 Toán tử 3 ngôi (Ternary Operator)
```java
// Cú pháp: điều_kiện ? giá_trị_đúng : giá_trị_sai
String result = (score >= 50) ? "Đậu" : "Rớt";
System.out.println(result);  // "Đậu"
```

- Thay thế `if-else` đơn giản trong 1 dòng. Không nên lồng nhiều tầng (khó đọc).

### 1.3 switch – case (Truyền thống)
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Chủ nhật");
        break;
    case 2:
        System.out.println("Thứ Hai");
        break;
    case 3:
        System.out.println("Thứ Ba");   // ← In ra
        break;
    default:
        System.out.println("Ngày khác");
        break;
}
```

- **Phải có `break`** sau mỗi case, nếu không sẽ bị **fall-through** (chạy xuống case tiếp theo).
- `default` xử lý trường hợp không khớp case nào.
- Hỗ trợ: `byte`, `short`, `int`, `char`, `String`, `enum` (không hỗ trợ `long`, `float`, `double`).

### 1.4 Switch Expression (Java 14+) – Cú pháp mới
```java
String dayName = switch (day) {
    case 1 -> "Chủ nhật";
    case 2 -> "Thứ Hai";
    case 3 -> "Thứ Ba";
    case 4 -> "Thứ Tư";
    case 5 -> "Thứ Năm";
    case 6 -> "Thứ Sáu";
    case 7 -> "Thứ Bảy";
    default -> "Không hợp lệ";
};
System.out.println(dayName);  // "Thứ Ba"
```

- **Không cần `break`**, mỗi case dùng `->` (arrow syntax).
- Có thể **trả về giá trị** (expression), gán vào biến.
- Gom nhiều case: `case 2, 3, 4, 5, 6 -> "Ngày trong tuần";`

### 1.5 Khi nào dùng if-else, khi nào dùng switch?
| Tình huống | Nên dùng |
|-----------|---------|
| Kiểm tra **phạm vi** (ví dụ: score >= 90) | `if-else` |
| So sánh **giá trị cố định** (day == 1, day == 2...) | `switch-case` |
| Nhiều điều kiện **phức tạp** kết hợp && / \|\| | `if-else` |
| Enum hoặc String có **số lượng giới hạn** | `switch-case` |

---

## 2. Vòng lặp (Loops)

### 2.1 Vòng lặp `for`
Dùng khi **biết trước số lần lặp**.

```java
// In các số từ 1 đến 5
for (int i = 1; i <= 5; i++) {
    System.out.print(i + " ");  // 1 2 3 4 5
}
```

Cấu trúc: `for (khởi_tạo; điều_kiện; cập_nhật)`
1. **Khởi tạo** (`int i = 1`): chạy 1 lần duy nhất.
2. **Điều kiện** (`i <= 5`): kiểm tra trước mỗi vòng, nếu `false` → dừng.
3. **Cập nhật** (`i++`): chạy sau mỗi vòng.

### 2.2 Vòng lặp `while`
Dùng khi **chưa biết trước số lần lặp**, kiểm tra điều kiện **trước** khi chạy.

```java
int count = 1;
while (count <= 5) {
    System.out.print(count + " ");  // 1 2 3 4 5
    count++;
}
```

- ⚠️ Nếu quên `count++` → **vòng lặp vô hạn** (infinite loop).

### 2.3 Vòng lặp `do-while`
Chạy **ít nhất 1 lần**, kiểm tra điều kiện **sau** khi chạy.

```java
int num = 10;
do {
    System.out.println("Chạy ít nhất 1 lần, num = " + num);
    num++;
} while (num < 5);  // Điều kiện sai ngay → nhưng vẫn chạy 1 lần
```

- Phù hợp cho: nhập liệu từ người dùng (nhập → kiểm tra → nhập lại nếu sai).

### 2.4 Vòng lặp `for-each` (Enhanced for)
Dùng để duyệt **mảng** hoặc **Collection** mà không cần index.

```java
int[] scores = {90, 85, 72, 68, 95};
for (int score : scores) {
    System.out.print(score + " ");  // 90 85 72 68 95
}
```

- **Không thể** thay đổi phần tử mảng gốc bên trong for-each.
- **Không có** biến index (`i`), nếu cần index → dùng `for` truyền thống.

### 2.5 So sánh các loại vòng lặp

| Loại | Khi nào dùng | Biết trước số lần? | Kiểm tra ĐK |
|------|-------------|-------------------|-------------|
| `for` | Lặp với counter cụ thể | ✅ | Trước |
| `while` | Lặp tới khi điều kiện sai | ❌ | Trước |
| `do-while` | Chạy ít nhất 1 lần | ❌ | Sau |
| `for-each` | Duyệt mảng/collection | ✅ | — |

---

## 3. Lệnh điều khiển luồng lặp

### 3.1 `break` – Thoát vòng lặp ngay lập tức
```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) break;              // Dừng khi i = 5
    System.out.print(i + " ");      // 1 2 3 4
}
```

### 3.2 `continue` – Bỏ qua lần lặp hiện tại, chạy lần tiếp
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;           // Bỏ qua khi i = 3
    System.out.print(i + " ");      // 1 2 4 5
}
```

### 3.3 Labeled break/continue (ít dùng)
```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) break outer;    // Thoát cả 2 vòng lặp
        System.out.println(i + "," + j);  // Chỉ in: 0,0
    }
}
```

---

## 4. Mảng 1 chiều (Array) căn bản

### 4.1 Khai báo & Khởi tạo
```java
// Cách 1: Khai báo kích thước, giá trị mặc định (0 cho int)
int[] numbers = new int[5];       // [0, 0, 0, 0, 0]

// Cách 2: Khai báo kèm giá trị
int[] scores = {90, 85, 72, 68};  // Kích thước = 4

// Cách 3: Khai báo kiểu cũ (ít dùng)
int ages[] = new int[3];
```

### 4.2 Truy xuất & Gán giá trị
```java
scores[0] = 100;                  // Gán giá trị index 0
System.out.println(scores[0]);    // 100
System.out.println(scores.length);// 4 (thuộc tính length, KHÔNG phải method)
// scores[4] → ❌ ArrayIndexOutOfBoundsException (index chạy từ 0 → length-1)
```

### 4.3 Duyệt mảng
```java
// Dùng for truyền thống (có index)
for (int i = 0; i < scores.length; i++) {
    System.out.println("Index " + i + ": " + scores[i]);
}

// Dùng for-each (không có index)
for (int s : scores) {
    System.out.println(s);
}
```

### 4.4 Lưu ý quan trọng
- Kích thước mảng **cố định** sau khi khởi tạo, không thể thêm/xóa phần tử.
- Nếu cần co giãn → dùng `ArrayList` (sẽ học ở Phase 2).
- Mảng là **reference type**, truyền mảng vào hàm → hàm có thể **thay đổi** phần tử gốc.

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Sự khác nhau giữa `if-else` và `switch-case`? Khi nào nên dùng cái nào?
- **`if-else`:** Đánh giá biểu thức điều kiện boolean linh hoạt (so sánh lớn hơn `>`, nhỏ hơn `<`, khoảng giá trị `18 <= age && age <= 60`, kết hợp nhiều biến khác nhau). Thực thi tuần tự từ trên xuống dưới.
- **`switch-case`:** Chỉ so sánh **bằng tuyệt đối (`==`)** của 1 biến đơn lẻ với tập các hằng số (hỗ trợ `byte`, `short`, `int`, `char`, `String`, `enum`).
- **Khi nào dùng:**
  - Dùng `switch-case` khi có từ 3 - 4 giá trị rời rạc cố định trở lên (vd: mã trạng thái đơn hàng `PENDING, SHIPPING, DELIVERED`, các ngày trong tuần, các lệnh menu). Trình biên dịch có thể tối ưu `switch` thành bảng nhảy (Jump Table / `tableswitch` bytecode) giúp tốc độ $O(1)$, nhanh hơn chuỗi `if-else if` dài $O(n)$.
  - Dùng `if-else` khi kiểm tra khoảng số (Range check), điều kiện logic phức tạp hoặc toán tử không phải so sánh bằng.

### 5.2. Fall-through trong switch là gì? Có thể gây lỗi gì?
- **Fall-through:** Nếu trong một khối `case` mà quên viết lệnh `break;`, chương trình sẽ không dừng lại mà tiếp tục "trôi tuột" xuống thực thi mã của các `case` tiếp theo phía dưới cho tới khi gặp `break` hoặc hết khối `switch`.
- **Hậu quả:** Gây ra các bug logic cực kỳ nghiêm trọng (ví dụ: User vừa được cấp quyền GUEST lại bị trôi lệnh gán quyền ADMIN).
- **Giải pháp hiện đại (Java 14+):** Sử dụng cú pháp **Switch Expression mũi tên (`->`)**:
  ```java
  // Không bao giờ bị fall-through, không cần từ khóa break
  switch (day) {
      case 1 -> System.out.println("Thứ Hai");
      case 2 -> System.out.println("Thứ Ba");
      default -> System.out.println("Ngày khác");
  }
  ```

### 5.3. `for` và `while` khác nhau thế nào? `do-while` khác `while` chỗ nào?
- **`for` vs `while`:**
  - `for`: Dùng khi **biết trước số lần lặp** (vd: lặp từ 1 đến $N$, duyệt qua mảng $N$ phần tử).
  - `while`: Dùng khi **chưa biết trước số lần lặp**, chỉ biết điều kiện dừng (vd: đọc file cho tới khi hết dòng, chờ tín hiệu phản hồi mạng).
- **`do-while` vs `while`:**
  - `while`: Kiểm tra điều kiện *trước*. Nếu điều kiện sai ngay từ đầu, vòng lặp chạy **0 lần**.
  - `do-while`: Thực thi thân vòng lặp *trước*, kiểm tra điều kiện *sau*. Đảm bảo thân vòng lặp luôn được chạy **ít nhất 1 lần** (thường dùng cho menu nhập liệu Console bắt người dùng nhập lại nếu sai).

### 5.4. Khi nào dùng `break`? Khi nào dùng `continue`?
- **`break`:** Lập tức **kết thúc và thoát khỏi** toàn bộ vòng lặp hiện tại. Thường dùng khi đã tìm thấy kết quả mong muốn (tìm kiếm phần tử trong mảng).
- **`continue`:** Lập tức **bỏ qua phần còn lại** của lần lặp hiện tại và nhảy sang lần lặp tiếp theo. Thường dùng để lọc bỏ các phần tử không hợp lệ (bỏ qua số lẻ, bỏ qua user bị khóa).

### 5.5. Tại sao kích thước mảng trong Java cố định? Khi cần thêm phần tử thì dùng gì?
- **Lý do:** Mảng trong Java được cấp phát một **khối nhớ liên tục (Contiguous Memory Block)** trên Heap ngay tại thời điểm khởi tạo (`new int[10]`). Việc cấp phát liên tục giúp máy tính tính toán vị trí ô nhớ tức thì qua công thức:
  $$\text{Address}(A[i]) = \text{Base\_Address} + i \times \text{Size\_Of\_Type}$$
  Do đó truy xuất mảng đạt tốc độ tuyệt đối $O(1)$. Không thể mở rộng mảng vì vùng nhớ liền kề phía sau có thể đã bị đối tượng khác chiếm dụng.
- **Khi cần thêm/xóa phần tử linh hoạt:** Sử dụng các Collection động như **`ArrayList`** (bản chất `ArrayList` tự động tạo mảng mới lớn gấp 1.5 lần và copy dữ liệu cũ sang khi mảng đầy).

### 5.6. `for-each` có thể thay đổi giá trị phần tử mảng gốc không? Tại sao?
- **Với mảng kiểu nguyên thuỷ (Primitive như `int[]`):** **KHÔNG THỂ.**
  - *Tại sao:* Biến lặp trong `for (int x : arr)` chỉ là một biến cục bộ tạm thời chứa **bản sao (copy)** giá trị của từng phần tử. Gán `x = 10` chỉ đổi giá trị của biến tạm `x`, mảng gốc hoàn toàn không bị ảnh hưởng.
- **Với mảng kiểu đối tượng (Object Reference như `User[]`):**
  - Không thể trỏ phần tử sang đối tượng mới (`u = new User()`), nhưng **CÓ THỂ** thay đổi trạng thái bên trong đối tượng (`u.setName("Mới")`) vì cả biến tạm và mảng đều trỏ vào cùng một ô nhớ trên Heap.

---

<div style="page-break-before: always;"></div>

<a id="phase-1-chapter-03"></a>

# Chapter 03: Quản lý Bộ nhớ Java – Stack vs Heap & Garbage Collection

## 1. Tổng quan kiến trúc bộ nhớ JVM

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                                       JVM MEMORY                                       │
│                                                                                        │
│  ┌────────────────────────────────────────┐  ┌──────────────────────────────────────┐  │
│  │      STACK (Mỗi Thread 1 Stack)        │  │   HEAP (Dùng chung tất cả Thread)    │  │
│  ├────────────────────────────────────────┤  ├──────────────────────────────────────┤  │
│  │ Frame: calculate()                     │  │ • User object {name='Minh', age=25}  │  │
│  │   └─ int result = 10                   │  │   (tại địa chỉ 0xA1) ◄────────────┐  │  │
│  │                                        │  │                                   │  │  │
│  │ Frame: main()                          │  │ • String 'Hello' (tại 0xB2)       │  │  │
│  │   ├─ int x = 5                         │  │ • int[] {1, 2, 3} (tại 0xC3)      │  │  │
│  │   └─ User ref = 0xA1 ──────────────────┼──┼───────────────────────────────────┘  │  │
│  └────────────────────────────────────────┘  └──────────────────────────────────────┘  │
│                                                                                        │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                             METASPACE (Java 8+)                                  │  │
│  ├──────────────────────────────────────────────────────────────────────────────────┤  │
│  │ Class metadata, Method bytecode, Static variables, Constant Pool                 │  │
│  └──────────────────────────────────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

## 2. Stack Memory

### 2.1 Đặc điểm
- Mỗi **Thread** có 1 Stack riêng.
- Lưu trữ theo cơ chế **LIFO** (Last In, First Out).
- Mỗi khi gọi 1 method → tạo 1 **Stack Frame** mới, khi method kết thúc → frame bị xoá.
- Lưu gì?
  - **Biến cục bộ** kiểu primitive (`int`, `double`, `boolean`…)
  - **Tham chiếu** (reference / địa chỉ) trỏ tới đối tượng trên Heap.
  - **Thông tin method** (return address, parameters).
- **Nhanh** (truy xuất tuần tự), **kích thước giới hạn** (~512KB – 1MB mặc định).
- Lỗi: `StackOverflowError` khi đệ quy quá sâu (quá nhiều frame).

### 2.2 Ví dụ minh hoạ
```java
public class Demo {
    public static void main(String[] args) {
        int x = 10;                  // x lưu trên Stack
        User user = new User("An");  // user (reference) trên Stack, object trên Heap
        int result = add(x, 20);     // Tạo Stack Frame mới cho add()
        System.out.println(result);
    }

    static int add(int a, int b) {  // a, b lưu trên Stack Frame của add()
        int sum = a + b;            // sum lưu trên Stack Frame của add()
        return sum;                 // Frame add() bị xoá khi return
    }
}
```

**Trạng thái Stack khi đang chạy `add()`:**
```
┌─────────────────────────┐
│ Frame: add()            │  ← Đỉnh stack (đang chạy)
│   a = 10, b = 20       │
│   sum = 30              │
├─────────────────────────┤
│ Frame: main()           │
│   x = 10                │
│   user = 0xA1 (ref)     │
│   result = ? (chưa gán) │
└─────────────────────────┘
```

## 3. Heap Memory

### 3.1 Đặc điểm
- Dùng **chung** cho tất cả Thread.
- Lưu gì?
  - **Tất cả đối tượng** tạo bởi từ khoá `new` (Object, Array, String…).
  - **Biến instance** (thuộc tính) của đối tượng.
- **Kích thước lớn**, có thể cấu hình bằng `-Xms` (initial) và `-Xmx` (max).
- Lỗi: `OutOfMemoryError: Java heap space` khi Heap đầy.

### 3.2 Cấu trúc Heap (Generational)
```
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│                                       HEAP MEMORY                                        │
│                                                                                          │
│  ┌─────────────────────────────────────────────────────────┐  ┌───────────────────────┐  │
│  │               YOUNG GENERATION                          │  │    OLD GENERATION     │  │
│  │                                                         │  │       (Tenured)       │  │
│  │  ┌──────────────────┐    ┌────────────┐  ┌───────────┐  │  │                       │  │
│  │  │    Eden Space    │    │ Survivor 0 │  │Survivor 1 │  │  │ ┌───────────────────┐ │  │
│  │  │ (Object mới tạo) │    │    (S0)    │  │   (S1)    │  │  │ │  Object sống lâu  │ │  │
│  │  └────────┬─────────┘    └─────┬──────┘  └───────────┘  │  │ │ (vượt ngưỡng tuổi)│ │  │
│  │           │ Minor GC           │                        │  │ └─────────▲─────────┘ │  │
│  │           │ sống sót           │ Sống sót nhiều lần     │  │           │           │  │
│  │           └───────────────────►│ (Age > Threshold) ─────┼──┼───────────┘           │  │
│  └─────────────────────────────────────────────────────────┘  └───────────────────────┘  │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

| Vùng | Chứa gì | GC |
|------|---------|-----|
| **Eden** | Object mới tạo (`new`) | Minor GC (nhanh, thường xuyên) |
| **Survivor** (S0, S1) | Object sống sót qua Minor GC | Minor GC |
| **Old Gen** (Tenured) | Object tồn tại lâu (qua nhiều lần GC) | Major / Full GC (chậm, hiếm) |

## 4. Pass-by-Value trong Java

### 4.1 Quy tắc vàng
> **Java luôn luôn là Pass-by-Value**, KHÔNG BAO GIỜ có Pass-by-Reference.

- Với **primitive**: copy **giá trị** → hàm không thể thay đổi biến gốc.
- Với **reference type**: copy **địa chỉ (reference)** → hàm có thể thay đổi **thuộc tính** của object gốc, nhưng **không thể** thay đổi biến reference gốc trỏ sang object khác.

### 4.2 Ví dụ với Primitive
```java
public static void main(String[] args) {
    int x = 10;
    changeValue(x);
    System.out.println(x);  // 10 ← Không đổi!
}

static void changeValue(int num) {
    num = 999;  // Chỉ thay đổi bản copy, không ảnh hưởng x
}
```

### 4.3 Ví dụ với Reference Type
```java
public static void main(String[] args) {
    User user = new User("An");
    changeName(user);
    System.out.println(user.getName());  // "Bình" ← Thay đổi được thuộc tính!

    replaceUser(user);
    System.out.println(user.getName());  // "Bình" ← Không đổi! (vẫn trỏ object cũ)
}

// Thay đổi thuộc tính → CÓ ảnh hưởng object gốc
static void changeName(User u) {
    u.setName("Bình");   // u và user cùng trỏ tới 1 object → đổi được
}

// Gán lại reference → KHÔNG ảnh hưởng biến gốc
static void replaceUser(User u) {
    u = new User("Cường");  // u trỏ sang object MỚI, user vẫn trỏ object cũ
}
```

### 4.4 Giải thích bằng sơ đồ
```
Trước changeName():
  main: user ──→ [User: name="An"]    ← Heap
  changeName: u ──→ (cùng object)

Sau changeName():
  main: user ──→ [User: name="Bình"]  ← Object bị đổi thuộc tính
  
Trong replaceUser():
  main: user ──→ [User: name="Bình"]  ← Vẫn trỏ object cũ
  replaceUser: u ──→ [User: name="Cường"] ← Object MỚI (bị huỷ khi hàm kết thúc)
```

## 5. Garbage Collection (GC)

### 5.1 Khi nào Object thành "rác"?
Khi **không còn bất kỳ biến nào** tham chiếu tới nó.

```java
User a = new User("An");   // Object 1 được tạo, a trỏ tới
User b = a;                 // b cũng trỏ tới Object 1
a = new User("Bình");       // a trỏ sang Object 2, Object 1 vẫn có b trỏ tới
b = null;                   // Object 1 KHÔNG CÒN ai trỏ tới → trở thành RÁC
// GC sẽ tự động dọn Object 1 khi cần
```

### 5.2 Các loại GC trong JVM
| GC | Đặc điểm |
|----|----------|
| **Serial GC** | Đơn thread, phù hợp app nhỏ |
| **Parallel GC** | Đa thread, mặc định Java 8 |
| **G1 GC** | Mặc định Java 9+, cân bằng throughput & latency |
| **ZGC / Shenandoah** | Ultra-low latency (< 10ms pause), Java 15+ |

### 5.3 Các lỗi bộ nhớ phổ biến
| Lỗi | Nguyên nhân | Cách phòng tránh |
|-----|------------|-----------------|
| `StackOverflowError` | Đệ quy vô hạn / quá sâu | Kiểm tra base case, dùng iteration |
| `OutOfMemoryError: Java heap space` | Tạo quá nhiều object, memory leak | Tăng `-Xmx`, kiểm tra leak |
| `OutOfMemoryError: Metaspace` | Load quá nhiều class (plugin) | Tăng `-XX:MaxMetaspaceSize` |

### 5.4 Memory Leak trong Java
Dù có GC, Java vẫn có thể bị **memory leak** khi:
- Lưu object vào **static collection** mà không bao giờ xoá.
- Listener/callback đăng ký mà không huỷ (unregister).
- Thread pool giữ reference quá lâu.

```java
// ❌ Memory leak: List tĩnh cứ add mãi, GC không thu hồi được
static List<byte[]> cache = new ArrayList<>();

void processData() {
    byte[] data = new byte[1024 * 1024]; // 1MB
    cache.add(data);  // data sẽ KHÔNG BAO GIỜ bị GC vì cache là static
}
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Phân biệt Stack và Heap trong Java? Mỗi vùng lưu gì?
| Tiêu chí | Vùng nhớ Stack | Vùng nhớ Heap |
| :--- | :--- | :--- |
| **Nội dung lưu trữ** | Biến cục bộ nguyên thuỷ (primitive), địa chỉ tham chiếu (reference address) và khung ngăn xếp hàm (Stack Frames). | Toàn bộ **Đối tượng (Object)** thực tế (`new Object()`), các phần tử mảng, chuỗi String. |
| **Phạm vi truy cập** | Thuộc về từng Thread riêng biệt (Thread-safe, không chia sẻ giữa các thread). | Dùng chung cho toàn bộ ứng dụng (Shared Memory, các thread đều có thể truy cập). |
| **Thời gian tồn tại** | Rất ngắn: Tự động giải phóng ngay khi hàm kết thúc thực thi. | Lâu dài: Được quản lý và thu gom bởi tiến trình dọn rác ngầm **Garbage Collector (GC)**. |
| **Tốc độ truy xuất** | Cực kỳ nhanh (cơ chế LIFO - Last In First Out). | Chậm hơn Stack do cấp phát động và quản lý phân mảnh. |
| **Lỗi tràn bộ nhớ** | `java.lang.StackOverflowError` (khi đệ quy vô hạn). | `java.lang.OutOfMemoryError: Java heap space` (khi tạo quá nhiều object mà GC không dọn kịp). |

### 6.2. Java là Pass-by-Value hay Pass-by-Reference? Giải thích với ví dụ
- **Khẳng định 100%:** Java **CHỈ DUY NHẤT LÀ PASS-BY-VALUE** (Truyền theo giá trị). Không có bất kỳ ngoại lệ nào!
- **Giải thích:**
  - Khi truyền biến kiểu Primitive: Java copy **giá trị số** sang hàm mới.
  - Khi truyền biến kiểu Object Reference: Java copy **giá trị của địa chỉ ô nhớ (Memory Address)** sang hàm mới (chứ không phải truyền bản thân biến tham chiếu ban đầu).
  - *Ví dụ chứng minh:*
    ```java
    public static void swap(Person p1, Person p2) {
        Person temp = p1;
        p1 = p2;
        p2 = temp;
        // p1 và p2 ở đây chỉ là bản sao địa chỉ cục bộ, hoán đổi không làm ảnh hưởng gì tới biến gốc ở ngoài!
    }
    ```
    Sau khi gọi hàm `swap(a, b)`, `a` và `b` ở ngoài vẫn giữ nguyên vị trí cũ.

### 6.3. Tại sao truyền object vào hàm có thể thay đổi thuộc tính nhưng không thể thay đổi reference gốc?
- Vì hàm nhận vào một **bản sao của địa chỉ tham chiếu**.
- Cả biến gốc ở ngoài và biến tham số trong hàm đều đang cầm 2 bản sao chìa khóa mở vào **cùng một ngôi nhà (cùng một object trên Heap)**:
  - Khi gọi `p.setName("An")`: Ta dùng chìa khóa để vào trong nhà sơn lại tường $\rightarrow$ Thuộc tính object trên Heap bị thay đổi thật.
  - Khi gọi `p = new Person("Bình")`: Biến tham số cục bộ vứt chìa khóa cũ đi để cầm chìa khóa căn nhà mới $\rightarrow$ Tham chiếu gốc bên ngoài vẫn đang trỏ tới căn nhà ban đầu, hoàn toàn không bị ảnh hưởng.

### 6.4. Garbage Collection (GC) hoạt động thế nào? Khi nào 1 object bị thu hồi?
- **Thuật toán tiếp cận GC Roots (Reachability Analysis):** JVM bắt đầu rà soát từ các rễ GC (`GC Roots` gồm: biến cục bộ trên Stack, luồng đang chạy `Active Threads`, biến `static`).
- **Điều kiện thu hồi:** Một object trên Heap sẽ trở thành "Rác" (Eligible for GC) khi nó **không còn bất kỳ đường dẫn tham chiếu nào (Unreachable)** kết nối từ GC Roots tới nó.
- **Quy trình dọn:** GC thực hiện theo nguyên lý **Mark and Sweep** (Đánh dấu các object còn sống $\rightarrow$ Quét dọn các object rác $\rightarrow$ Dồn dịch bộ nhớ Compact để chống phân mảnh).

### 6.5. Minor GC và Major GC khác nhau thế nào? Cái nào ảnh hưởng performance hơn?
- **Bộ nhớ Heap chia thành các thế hệ (Generational Heap):**
  - **Young Generation (Eden + Survivor S0, S1):** Nơi các object mới sinh ra. Đa số object trong Java chết trẻ (chỉ sống trong một hàm rồi hết giá trị).
  - **Old Generation (Tenured):** Chứa các object sống sót qua nhiều chu kỳ dọn rác (Long-lived objects như Spring Beans, Connection Pools, Caches).
- **So sánh:**
  - **Minor GC:** Dọn rác ở vùng **Young Generation**. Diễn ra rất thường xuyên, tốc độ cực nhanh (vài mili-giây), ít ảnh hưởng hệ thống.
  - **Major GC (hay Full GC):** Dọn rác ở toàn bộ vùng nhớ (đặc biệt là **Old Generation**). Khi chạy Full GC, toàn bộ ứng dụng có thể bị dừng tạm thời (**Stop-The-World - STW**). Nếu Full GC diễn ra liên tục, hệ thống sẽ bị giật lag, tăng độ trễ (latency spike) nghiêm trọng.

### 6.6. `StackOverflowError` và `OutOfMemoryError` khác nhau thế nào?
- **`StackOverflowError`:** Xảy ra ở vùng nhớ **Stack**. Thường do hàm đệ quy không có điểm dừng hoặc gọi lồng nhau quá sâu làm đầy dung lượng ngăn xếp của Thread (mặc định ~1MB).
- **`OutOfMemoryError (OOM)`:** Xảy ra ở vùng nhớ **Heap**. Xảy ra khi ứng dụng liên tục tạo thêm đối tượng mới trên Heap mà dung lượng Heap đã chạm trần (`-Xmx`), đồng thời Garbage Collector đã cố gắng chạy hết sức nhưng không thể giải phóng đủ chỗ trống.

### 6.7. Giải thích Memory Leak trong Java có thể xảy ra dù đã có GC
- Trong Java, Memory Leak không phải là "thất lạc con trỏ" như C/C++, mà là tình trạng: **Một đối tượng KHÔNG CÒN ĐƯỢC ỨNG DỤNG SỬ DỤNG NỮA nhưng VẪN BỊ THAM CHIẾU (Referenced) bởi một object sống khác**, khiến GC không thể dọn dẹp nó.
- **Các nguyên nhân gây Memory Leak điển hình trong Backend:**
  1. **Dùng biến `static` giữ collection:** `public static List<User> cache = new ArrayList<>()` cứ nhét thêm vào mà không bao giờ xóa. Vì `static` sống trọn vòng đời của JVM, list này sẽ giữ chặt các object mãi mãi.
  2. **Không đóng tài nguyên (Unclosed Resources):** Quên đóng kết nối Database (`Connection`), `InputStream`, `Socket`.
  3. **Lắng nghe sự kiện (Event Listeners / Observers):** Đăng ký Listener nhưng quên unregister khi đối tượng bị hủy.
  4. **Dùng `ThreadLocal` không gọi `.remove()`:** Trong môi trường Thread Pool (như Tomcat), thread được tái sử dụng. Dữ liệu trong `ThreadLocal` nếu không dọn sẽ tích tụ dần làm tràn bộ nhớ.

---

<div style="page-break-before: always;"></div>

<a id="phase-1-chapter-04"></a>

# Chapter 04: String, StringBuilder & String Pool

## 1. Bản chất String trong Java

### 1.1 String là Immutable (Bất biến)
- Sau khi tạo, **nội dung** của String **không thể thay đổi**.
- Mọi thao tác "thay đổi" String (concat, replace, toUpperCase…) đều **tạo ra String MỚI** trên Heap, String gốc không bị ảnh hưởng.

```java
String s = "Hello";
s.concat(" World");       // Tạo String mới "Hello World" nhưng KHÔNG gán lại cho s
System.out.println(s);    // "Hello" ← Không đổi!

s = s.concat(" World");   // Gán lại: s trỏ sang String mới "Hello World"
System.out.println(s);    // "Hello World"
// String cũ "Hello" vẫn tồn tại trên Heap (chờ GC thu hồi nếu không ai trỏ tới)
```

### 1.2 Tại sao String được thiết kế là Immutable?
| Lý do | Giải thích |
|-------|-----------|
| **Security** | Không thể sửa đổi giá trị URL, username, password sau khi tạo → tránh bị tấn công injection |
| **Thread Safety** | Nhiều Thread có thể dùng chung 1 String mà không cần synchronize |
| **String Pool** | Vì immutable nên JVM có thể chia sẻ 1 String giữa nhiều biến (caching) |
| **HashCode caching** | hashCode được tính 1 lần và cache lại → tăng performance khi dùng làm key trong HashMap |

## 2. String Pool (String Constant Pool)

### 2.1 Khái niệm
- String Pool là **vùng nhớ đặc biệt** trong Heap, JVM dùng để **tái sử dụng** các String literal trùng nhau.
- Khi viết `String s = "abc"`, JVM kiểm tra Pool:
  - Nếu `"abc"` **đã tồn tại** → trả về reference tới String cũ (không tạo mới).
  - Nếu **chưa có** → tạo mới trong Pool.

### 2.2 Minh hoạ

```
┌────────────────────────┐             ┌────────────────────────────────────────────────────────┐
│      STACK MEMORY      │             │                      HEAP MEMORY                       │
├────────────────────────┤             ├────────────────────────────────────────────────────────┤
│                        │             │                                                        │
│  a ────────────────────┼─────────────┼─┐   ┌───────────────────────────────┐                  │
│                        │             │ │   │          String Pool          │                  │
│  b ────────────────────┼─────────────┼─┴──►│  "java"  (tại địa chỉ 0xA1)   │                  │
│                        │             │     └───────────────────────────────┘                  │
│                        │             │                                                        │
│  c ────────────────────┼─────────────┼───► new String("java") (Object ngoài Pool tại 0xC3)    │
│                        │             │                                                        │
└────────────────────────┘             └────────────────────────────────────────────────────────┘
```

```java
String a = "java";              // Tạo "java" trong Pool
String b = "java";              // Tìm thấy "java" trong Pool → dùng lại
String c = new String("java");  // Tạo object MỚI trên Heap (NGOÀI Pool)

System.out.println(a == b);       // true  (cùng trỏ 1 object trong Pool)
System.out.println(a == c);       // false (a trỏ Pool, c trỏ Heap khác)
System.out.println(a.equals(c));  // true  (nội dung giống nhau)
```

### 2.3 Phương thức `intern()`
```java
String c = new String("java");
String d = c.intern();   // Đưa "java" vào Pool (hoặc lấy lại nếu đã có)
System.out.println(a == d);  // true (d giờ trỏ vào Pool giống a)
```

## 3. So sánh `==` vs `.equals()`

| Toán tử | So sánh gì | Dùng cho |
|---------|-----------|---------|
| `==` | **Địa chỉ bộ nhớ** (reference) | Primitive (so giá trị), Reference (so địa chỉ) |
| `.equals()` | **Nội dung** (đã override trong String) | So sánh nội dung String, Object |

> 🔴 **Quy tắc vàng:** Luôn dùng `.equals()` khi so sánh nội dung String. KHÔNG dùng `==` cho String.

```java
String x = "hello";
String y = new String("hello");

System.out.println(x == y);          // false ← So sánh địa chỉ
System.out.println(x.equals(y));     // true  ← So sánh nội dung
System.out.println(x.equalsIgnoreCase("HELLO"));  // true ← Bỏ qua hoa/thường
```

## 4. Các method String thường dùng

```java
String s = "  Hello World  ";

s.length();                    // 15 (tính cả khoảng trắng)
s.trim();                      // "Hello World" (xoá khoảng trắng 2 đầu)
s.strip();                     // "Hello World" (Java 11, xử lý Unicode tốt hơn trim)
s.toLowerCase();               // "  hello world  "
s.toUpperCase();               // "  HELLO WORLD  "
s.charAt(2);                   // 'H' (ký tự tại index 2)
s.indexOf("World");            // 8 (vị trí đầu tiên tìm thấy)
s.contains("Hello");           // true
s.startsWith("  He");          // true
s.endsWith("  ");              // true
s.substring(2, 7);             // "Hello" (từ index 2 đến 6)
s.replace("World", "Java");   // "  Hello Java  "
s.isEmpty();                   // false (có ký tự)
s.isBlank();                   // false (Java 11, kiểm tra cả khoảng trắng)
"".isEmpty();                  // true
"   ".isBlank();               // true (chỉ có khoảng trắng)

// Chuyển đổi
String.valueOf(123);           // "123" (int → String)
Integer.parseInt("123");       // 123  (String → int)
Double.parseDouble("3.14");    // 3.14 (String → double)

// Tách / Nối
String csv = "a,b,c,d";
String[] parts = csv.split(",");         // ["a", "b", "c", "d"]
String joined = String.join("-", parts); // "a-b-c-d"
```

## 5. StringBuilder & StringBuffer

### 5.1 Vấn đề khi nối String trong vòng lặp
```java
// ❌ CHẬM: Mỗi lần += tạo 1 String MỚI → O(n²) bộ nhớ
String result = "";
for (int i = 0; i < 10000; i++) {
    result += i;  // Tạo 10.000 object String tạm trên Heap!
}
```

### 5.2 Giải pháp: StringBuilder (Mutable)
```java
// ✅ NHANH: StringBuilder sửa trực tiếp buffer nội bộ
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append(i);  // Không tạo object mới
}
String result = sb.toString();
```

### 5.3 Các method StringBuilder phổ biến
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");         // "Hello World"
sb.insert(5, ",");           // "Hello, World"
sb.delete(5, 6);             // "Hello World"
sb.replace(6, 11, "Java");  // "Hello Java"
sb.reverse();                // "avaJ olleH"
sb.length();                 // 10
sb.toString();               // Chuyển về String
```

### 5.4 StringBuilder vs StringBuffer

| Tiêu chí | StringBuilder | StringBuffer |
|----------|--------------|-------------|
| Thread‑safe? | ❌ Không (nhanh hơn) | ✅ Có (synchronized) |
| Performance | ⚡ Nhanh | 🐢 Chậm hơn do lock |
| Khi nào dùng? | **Single-thread** (99% trường hợp) | **Multi-thread** (hiếm dùng) |

> 💡 Trong thực tế, **luôn dùng StringBuilder** trừ khi có yêu cầu thread-safe rõ ràng.

### 5.5 Đo thời gian thực thi
```java
// Đo String concatenation
long start = System.currentTimeMillis();
String s = "";
for (int i = 0; i < 100000; i++) { s += "a"; }
long end = System.currentTimeMillis();
System.out.println("String: " + (end - start) + "ms");   // ~5000ms+

// Đo StringBuilder
start = System.currentTimeMillis();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 100000; i++) { sb.append("a"); }
end = System.currentTimeMillis();
System.out.println("StringBuilder: " + (end - start) + "ms"); // ~3ms
```

## 6. Tóm tắt khi nào dùng gì

| Tình huống | Dùng |
|-----------|------|
| Chuỗi ít thay đổi, gán 1 lần | `String` |
| Nối chuỗi trong vòng lặp | `StringBuilder` |
| Nối chuỗi trong môi trường multi-thread | `StringBuffer` |
| So sánh nội dung chuỗi | `.equals()` hoặc `.equalsIgnoreCase()` |
| So sánh xem có cùng 1 object không | `==` (hiếm khi cần) |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Tại sao String trong Java là Immutable (Bất biến)? Lợi ích?
- **Khái niệm:** Một khi đối tượng `String` được tạo ra trên Heap, nội dung chuỗi của nó **không bao giờ có thể bị thay đổi**. Mọi thao tác cắt, nối (`concat`, `replace`, `substring`) thực chất đều sinh ra một đối tượng `String` hoàn toàn mới.
- **3 Lợi ích sống còn của String Immutability:**
  1. **Bảo mật (Security):** String được dùng làm tham số kết nối Database URL, Username, Password, cổng mạng, tên file. Nếu String có thể bị sửa đổi (mutable), một luồng mã độc có thể âm thầm đổi địa chỉ Database sau khi đã qua bước kiểm tra xác thực.
  2. **An toàn đa luồng (Thread-Safety):** Vì dữ liệu không bao giờ thay đổi, nhiều luồng (threads) có thể đồng thời đọc cùng một String mà không bao giờ cần đồng bộ hóa (synchronization), loại bỏ hoàn toàn nguy cơ tranh chấp Race Condition.
  3. **Tối ưu bộ nhớ với String Constant Pool:** Nhờ bất biến, hàng trăm biến mang cùng giá trị `"ACTIVE"` có thể cùng trỏ về 1 ô nhớ duy nhất trên Heap mà không sợ một biến sửa làm ảnh hưởng tới các biến khác.
  4. **Caching Hashcode:** Mã hash (`hashCode()`) của String chỉ cần tính toán 1 lần duy nhất lúc khởi tạo và lưu cache lại. Điều này giúp String trở thành Key lý tưởng nhất cho `HashMap` với tốc độ tìm kiếm $O(1)$ siêu nhanh.

### 7.2. String Pool là gì? Hoạt động thế nào?
- **String Constant Pool (SCP):** Là một vùng nhớ đặc biệt nằm bên trong bộ nhớ **Heap** của JVM.
- **Cơ chế hoạt động:**
  - Khi ta khai báo bằng chuỗi literal: `String s = "hello";`
  - JVM sẽ kiểm tra trong String Pool xem đã có chuỗi `"hello"` nào tồn tại chưa.
  - Nếu **đã có:** JVM trả về ngay địa chỉ tham chiếu của đối tượng có sẵn trong Pool (không tạo mới).
  - Nếu **chưa có:** JVM tạo mới một đối tượng `"hello"` đặt vào Pool và trả về địa chỉ.

### 7.3. `String a = "abc"` và `String b = new String("abc")` tạo bao nhiêu object?
- **Trường hợp 1:** Nếu chuỗi `"abc"` **chưa hề tồn tại** trong String Pool từ trước:
  - Lệnh `String a = "abc";` $\rightarrow$ Tạo **1 object** nằm trong **String Pool**.
  - Lệnh `String b = new String("abc");` $\rightarrow$ Tạo thêm **1 object** nằm ở **vùng nhớ Heap thông thường** (ngoài Pool).
  - $\rightarrow$ Tổng cộng tạo **2 objects**.
- **Trường hợp 2:** Nếu chuỗi `"abc"` **đã có sẵn** trong String Pool:
  - Lệnh `new String("abc")` chỉ tạo duy nhất **1 object** trên Heap thông thường.

### 7.4. Phân biệt `==` và `.equals()` khi dùng với String
- **Toán tử `==`:** So sánh **địa chỉ ô nhớ** (hai biến có cùng trỏ tới 1 object hay không).
- **Phương thức `.equals()`:** So sánh **nội dung ký tự bên trong chuỗi**.
- *Ví dụ kinh điển:*
  ```java
  String s1 = "Java";
  String s2 = "Java";
  String s3 = new String("Java");

  System.out.println(s1 == s2);      // true (cùng trỏ vào 1 object trong String Pool)
  System.out.println(s1 == s3);      // false (s1 ở trong Pool, s3 là object riêng trên Heap)
  System.out.println(s1.equals(s3)); // true (nội dung đều là "Java")
  ```
  > **Quy tắc bất di bất dịch:** Trong Backend Java, **LUÔN LUÔN dùng `.equals()`** để so sánh chuỗi!

### 7.5. Tại sao không nên dùng `+=` để nối String trong vòng lặp?
- Vì String là bất biến, mỗi lần gọi `str += "a"` trong vòng lặp $N$ lần, JVM phải tạo ra một đối tượng `StringBuilder` tạm, append, rồi gọi `.toString()` tạo ra một đối tượng `String` mới và vứt bỏ đối tượng cũ làm rác.
- **Hậu quả:**
  - Độ phức tạp thời gian: $O(N^2)$ thay vì $O(N)$.
  - Tạo ra hàng ngàn object rác trên Heap, ép Garbage Collector phải chạy liên tục (gây giật lag hệ thống).
  - Với vòng lặp 100.000 lần: Nối chuỗi bằng `+=` mất **vài phút**, trong khi dùng `StringBuilder` chỉ mất **chưa tới 10 mili-giây**.

### 7.6. StringBuilder và StringBuffer khác nhau thế nào? Khi nào dùng cái nào?
| Tiêu chí | `StringBuilder` (Java 5+) | `StringBuffer` (Java 1.0) |
| :--- | :--- | :--- |
| **Tính an toàn đa luồng** | **Không Thread-safe** (các phương thức không có `synchronized`). | **Thread-safe** (hầu hết phương thức đều bọc từ khóa `synchronized`). |
| **Tốc độ thực thi** | **Cực nhanh** (vì không mất chi phí khóa luồng - lock overhead). | Chậm hơn do chi phí đồng bộ luồng. |
| **Ứng dụng thực tế** | Dùng trong **99% trường hợp thực tế** (nối chuỗi trong một hàm, một luồng duy nhất). | Chỉ dùng khi nhiều Thread cùng lúc chỉnh sửa chung một bộ đệm chuỗi (rất hiếm khi gặp). |

### 7.7. Phương thức `intern()` dùng để làm gì?
- Khi gọi `s.intern()`, JVM sẽ kiểm tra xem nội dung của `s` đã có trong String Constant Pool chưa:
  - Nếu đã có: Trả về tham chiếu của đối tượng trong Pool.
  - Nếu chưa có: Đưa `s` vào String Pool và trả về tham chiếu đó.
- *Ví dụ:*
  ```java
  String s1 = new String("hello"); // Nằm trên Heap
  String s2 = s1.intern();          // Ép lấy đối tượng trong Pool
  String s3 = "hello";              // Nằm trong Pool
  System.out.println(s2 == s3);     // true
  ```
- *Ứng dụng:* Dùng khi đọc một lượng cực lớn dữ liệu từ file/database có nhiều chuỗi trùng lặp (ví dụ: tên thành phố, mã quốc gia) để đưa vào Pool giúp tiết kiệm dung lượng RAM.

---

<div style="page-break-before: always;"></div>

<a id="phase-1-chapter-05"></a>

# Chapter 05: Xử lý Ngoại lệ (Exception Handling)

## 1. Exception là gì?
- **Exception** (Ngoại lệ) là sự kiện bất thường xảy ra trong quá trình chạy chương trình, làm gián đoạn luồng thực thi bình thường.
- Nếu không xử lý, chương trình sẽ **crash** và in ra stack trace.

```java
int[] arr = {1, 2, 3};
System.out.println(arr[5]);  // ❌ ArrayIndexOutOfBoundsException → Chương trình crash!
```

## 2. Hệ thống phân cấp Exception trong Java

```
┌────────────────────────────────────────────────────────────────────────┐
│                              Throwable                                 │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
      ┌─────────────────────────────┴─────────────────────────────┐
      ▼                                                           ▼
┌───────────────────────────┐               ┌───────────────────────────┐
│           Error           │               │         Exception         │
│  (JVM Crash / Hệ thống)   │               │     (Có thể xử lý)        │
└─────────────┬─────────────┘               └─────────────┬─────────────┘
              │                                           │
  ├── StackOverflowError            ┌─────────────────────┴─────────────────────┐
  └── OutOfMemoryError (OOM)        ▼                                           ▼
                              ┌───────────────────────────┐       ┌───────────────────────────┐
                              │     Checked Exception     │       │     RuntimeException      │
                              │ (Bắt buộc try-catch/throw)│       │    (Unchecked Exception)  │
                              └─────────────┬─────────────┘       └─────────────┬─────────────┘
                                            │                                   │
                                ├── IOException                     ├── NullPointerException
                                ├── SQLException                    ├── ArrayIndexOutOfBounds
                                └── ParseException                  ├── ArithmeticException
                                                                    ├── IllegalArgumentException
                                                                    └── NumberFormatException
```

### 2.1 Error (Lỗi hệ thống)
- **Không nên bắt / xử lý** vì quá nghiêm trọng (JVM gặp vấn đề).
- Ví dụ: `StackOverflowError`, `OutOfMemoryError`.

### 2.2 Checked Exception (Ngoại lệ kiểm tra)
- **Bắt buộc phải xử lý** tại compile‑time (dùng `try-catch` hoặc `throws`).
- Compiler sẽ báo lỗi nếu bạn không xử lý.
- Ví dụ: `IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`.

```java
// ❌ Compile Error nếu không xử lý IOException
FileReader file = new FileReader("data.txt");  // FileNotFoundException (checked)
```

### 2.3 Unchecked Exception (Ngoại lệ không kiểm tra)
- Kế thừa từ `RuntimeException`.
- **Không bắt buộc** phải xử lý tại compile‑time (nhưng nên bắt nếu có thể).
- Thường do **lỗi logic của lập trình viên**.
- Ví dụ: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`, `IllegalArgumentException`.

```java
String s = null;
s.length();          // ❌ NullPointerException (unchecked, runtime crash)

int result = 10 / 0; // ❌ ArithmeticException (unchecked)
```

### 2.4 Bảng so sánh

| Tiêu chí | Checked Exception | Unchecked Exception |
|----------|-------------------|---------------------|
| Kế thừa từ | `Exception` (trực tiếp) | `RuntimeException` |
| Bắt buộc xử lý? | ✅ Có (compile-time) | ❌ Không |
| Nguyên nhân | Yếu tố bên ngoài (file, network, DB) | Lỗi logic code |
| Ví dụ | `IOException`, `SQLException` | `NullPointerException`, `ArithmeticException` |

## 3. Cú pháp try – catch – finally

### 3.1 Cấu trúc cơ bản
```java
try {
    // Code có thể gây exception
    int result = 10 / 0;
    System.out.println(result);       // Dòng này KHÔNG chạy
} catch (ArithmeticException e) {
    // Xử lý khi bắt được exception
    System.out.println("Lỗi: " + e.getMessage());  // "Lỗi: / by zero"
} finally {
    // LUÔN LUÔN chạy, dù có exception hay không
    System.out.println("Khối finally luôn chạy");
}
System.out.println("Chương trình tiếp tục chạy bình thường");
```

### 3.2 Luồng thực thi

```
              ┌────────────────────────┐
              │     Bắt đầu try        │
              └───────────┬────────────┘
                          │
                          ▼
              ┌────────────────────────┐
              │   Exception xảy ra?    │
              └─────┬────────────┬─────┘
                CÓ  │            │  KHÔNG
                    ▼            ▼
┌────────────────────────┐  ┌────────────────────────┐
│ Nhảy vào khối catch    │  │ Chạy hết khối try      │
│ tương ứng để xử lý     │  │ một cách bình thường   │
└───────────────────┬────┘  └────┬───────────────────┘
                    │            │
                    └─────┬──────┘
                          ▼
              ┌────────────────────────┐
              │  finally (luôn chạy)   │
              │(Giải phóng tài nguyên) │
              └───────────┬────────────┘
                          │
                          ▼
              ┌────────────────────────┐
              │ Tiếp tục code sau khối │
              │      try - catch       │
              └────────────────────────┘
```

### 3.3 Bắt nhiều Exception
```java
try {
    String s = null;
    s.length();         // NullPointerException
} catch (NullPointerException e) {
    System.out.println("Lỗi null: " + e.getMessage());
} catch (ArithmeticException e) {
    System.out.println("Lỗi số học: " + e.getMessage());
} catch (Exception e) {
    // Catch chung (đặt cuối cùng, vì Exception là cha của tất cả)
    System.out.println("Lỗi khác: " + e.getMessage());
}

// Hoặc gộp nhiều exception trong 1 catch (Java 7+):
try {
    // ...
} catch (NullPointerException | ArithmeticException e) {
    System.out.println("Lỗi: " + e.getMessage());
}
```

> ⚠️ **Thứ tự catch:** Từ Exception **cụ thể** → **tổng quát** (con trước, cha sau).

## 4. throw & throws

### 4.1 `throw` – Quăng exception ra
```java
public void setAge(int age) {
    if (age < 0 || age > 150) {
        throw new IllegalArgumentException("Tuổi không hợp lệ: " + age);
    }
    this.age = age;
}
```

### 4.2 `throws` – Khai báo method có thể quăng exception
```java
// Khai báo: method này CÓ THỂ quăng IOException (checked)
// Người gọi method PHẢI xử lý (try-catch hoặc throws tiếp)
public String readFile(String path) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(path));
    return reader.readLine();
}
```

### 4.3 So sánh throw vs throws

| | `throw` | `throws` |
|---|---------|---------|
| Vị trí | Trong **thân** method | Tại **khai báo** method |
| Mục đích | **Quăng** 1 exception cụ thể | **Khai báo** method có thể quăng exception |
| Số lượng | 1 exception mỗi lần | Nhiều exception (phẩy phân cách) |
| Ví dụ | `throw new RuntimeException("msg");` | `void read() throws IOException, SQLException` |

## 5. Custom Exception (Ngoại lệ tự tạo)

### 5.1 Tại sao cần Custom Exception?
- Exception có sẵn quá chung chung, không mô tả đúng lỗi nghiệp vụ.
- Custom Exception giúp code **rõ ràng hơn** và dễ xử lý theo từng loại lỗi.

### 5.2 Tạo Unchecked Custom Exception (phổ biến nhất)
```java
// Kế thừa RuntimeException → KHÔNG bắt buộc try-catch
public class ResourceNotFoundException extends RuntimeException {

    public ResourceNotFoundException(String message) {
        super(message);
    }

    public ResourceNotFoundException(String resourceName, Long id) {
        super(resourceName + " không tìm thấy với ID: " + id);
    }
}

// Sử dụng:
public User getUserById(Long id) {
    return userRepository.findById(id)
        .orElseThrow(() -> new ResourceNotFoundException("User", id));
    // Quăng: "User không tìm thấy với ID: 5"
}
```

### 5.3 Tạo Checked Custom Exception (ít dùng hơn)
```java
// Kế thừa Exception → BẮT BUỘC try-catch
public class InsufficientBalanceException extends Exception {

    private final double currentBalance;
    private final double withdrawAmount;

    public InsufficientBalanceException(double currentBalance, double withdrawAmount) {
        super("Số dư không đủ. Hiện có: " + currentBalance + ", cần rút: " + withdrawAmount);
        this.currentBalance = currentBalance;
        this.withdrawAmount = withdrawAmount;
    }
    
    // Getter nếu cần
}
```

## 6. Try-with-Resources (Java 7+)

### 6.1 Vấn đề: Quên đóng tài nguyên
```java
// ❌ Phải đóng resource trong finally (code dài dòng, dễ quên)
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("data.txt"));
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try { reader.close(); } catch (IOException e) { e.printStackTrace(); }
    }
}
```

### 6.2 Giải pháp: try-with-resources
```java
// ✅ Tự động đóng resource khi kết thúc try (gọn, an toàn)
try (BufferedReader reader = new BufferedReader(new FileReader("data.txt"))) {
    String line = reader.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
// reader.close() được gọi TỰ ĐỘNG khi ra khỏi try, dù có exception hay không
```

### 6.3 Điều kiện sử dụng
- Resource phải implement interface `AutoCloseable` (hoặc `Closeable`).
- Có thể khai báo **nhiều resource** cách nhau bằng `;`:

```java
try (
    FileInputStream fis = new FileInputStream("input.txt");
    FileOutputStream fos = new FileOutputStream("output.txt")
) {
    // Đọc input, ghi output
} catch (IOException e) {
    e.printStackTrace();
}
// Cả fis và fos đều tự động đóng
```

## 7. Best Practices xử lý Exception

| ✅ Nên | ❌ Không nên |
|--------|-------------|
| Bắt exception **cụ thể** (`NullPointerException`) | Bắt `Exception` chung chung |
| Ghi log đầy đủ (`logger.error("msg", e)`) | Bắt rồi **nuốt** (catch trống rỗng) |
| Dùng **Custom Exception** cho lỗi nghiệp vụ | Dùng `RuntimeException("msg")` chung chung |
| Dùng `try-with-resources` cho I/O | Tự `close()` trong finally |
| Quăng sớm, bắt muộn (Throw early, Catch late) | Bắt exception ở mọi nơi |

```java
// ❌ Anti-pattern: Nuốt exception (swallowing)
try {
    riskyOperation();
} catch (Exception e) {
    // Không làm gì cả → bug ẩn, rất khó debug!
}

// ✅ Best practice: Log hoặc throw lại
try {
    riskyOperation();
} catch (SpecificException e) {
    logger.error("Lỗi khi xử lý: {}", e.getMessage(), e);
    throw new BusinessException("Xử lý thất bại", e);
}
```

## 8. Câu hỏi phỏng vấn & Trả lời chi tiết

### 8.1. Phân biệt Checked và Unchecked Exception? Cho ví dụ mỗi loại
| Tiêu chí | Checked Exception | Unchecked Exception (Runtime) |
| :--- | :--- | :--- |
| **Kế thừa từ** | Kế thừa trực tiếp từ `Exception` (trừ `RuntimeException`). | Kế thừa từ `RuntimeException`. |
| **Thời điểm kiểm tra** | **Compile-time** (Trình biên dịch bắt buộc phải xử lý bằng `try-catch` hoặc khai báo `throws`). | **Runtime** (Trình biên dịch không bắt buộc khai báo hay bắt lỗi). |
| **Bản chất nguyên nhân** | Lỗi ngoại cảnh nằm ngoài tầm kiểm soát của code (Mạng rớt, file không tồn tại, kết nối DB ngắt). | Lỗi do **bug logic của lập trình viên** (truy cập null, chia cho 0, vượt biên mảng). |
| **Ví dụ điển hình** | `IOException`, `SQLException`, `FileNotFoundException`, `ClassNotFoundException`. | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`. |

### 8.2. Phân biệt `Error` và `Exception`?
- Cả hai đều kế thừa từ lớp cha `Throwable`:
  - **`Error`:** Đại diện cho các **sự cố nghiêm trọng ở mức hệ thống / máy ảo JVM** (ví dụ: `OutOfMemoryError`, `StackOverflowError`). Ứng dụng thông thường **không nên và không thể bắt (`catch`) hay phục hồi** khi gặp `Error`. Khi `Error` xảy ra, ứng dụng thường phải dừng lại.
  - **`Exception`:** Đại diện cho các **tình huống ngoại lệ trong luồng thực thi của ứng dụng** mà lập trình viên có thể lường trước, bắt lại bằng `try-catch` và xử lý khắc phục (graceful degradation) để chương trình tiếp tục chạy ổn định.

### 8.3. Khối `finally` có LUÔN LUÔN chạy không?
- **Quy tắc chung:** Khối `finally` **gần như luôn luôn chạy**, kể cả khi trong khối `try` hoặc `catch` có lệnh `return`, `continue`, hoặc văng ra exception khác.
- **Những trường hợp hiếm hoi `finally` KHÔNG chạy:**
  1. Gọi lệnh tắt JVM cưỡng bức: `System.exit(0);`
  2. Máy chủ bị sập nguồn điện đột ngột hoặc tiến trình JVM bị hệ điều hành kill (`kill -9`).
  3. Lỗi phần cứng hoặc JVM bị crash nặng (`Fatal Error`).
  4. Vòng lặp vô hạn bên trong khối `try` khiến luồng không bao giờ chạm tới được `finally`.

### 8.4. `throw` và `throws` khác nhau thế nào?
| Tiêu chí | Từ khóa `throw` | Từ khóa `throws` |
| :--- | :--- | :--- |
| **Vị trí sử dụng** | Nằm **bên trong thân hàm / phương thức**. | Nằm ở **chữ ký phương thức (Method Signature)**. |
| **Mục đích** | Chủ động **kích hoạt / ném ra** một đối tượng ngoại lệ cụ thể (`throw new BusinessException("Lỗi");`). | **Cảnh báo / Khai báo** rằng phương thức này CÓ THỂ ném ra các loại ngoại lệ nào để nơi gọi nó chuẩn bị xử lý. |
| **Cú pháp** | Theo sau là một **đối tượng ngoại lệ (Instance)**: `throw exceptionInstance;` | Theo sau là một hoặc nhiều **tên lớp ngoại lệ (Class Name)**: `throws IOException, SQLException` |

### 8.5. Tại sao nên tạo Custom Exception thay vì dùng `RuntimeException` trực tiếp?
1. **Phân loại nghiệp vụ rõ ràng:** Tạo `UserNotFoundException`, `InsufficientBalanceException` giúp code mang tính tự diễn giải (Self-documenting), người đọc hiểu ngay lỗi nghiệp vụ là gì.
2. **Bắt lỗi tập trung (Global Exception Handling):** Trong Spring Boot (`@RestControllerAdvice`), ta có thể viết các hàm `@ExceptionHandler` riêng cho từng Custom Exception để trả về đúng mã HTTP Status (ví dụ: `UserNotFoundException` trả về `404 Not Found`, `InvalidOrderException` trả về `400 Bad Request`).
3. **Đính kèm dữ liệu bổ sung:** Custom Exception có thể chứa thêm các trường dữ liệu tùy biến (ví dụ: `errorCode`, `timestamp`, `fieldName`) để phục vụ việc debug và trả lỗi chi tiết cho Frontend.

### 8.6. Try-with-resources hoạt động thế nào? Điều kiện để resource được tự đóng?
- **Cơ chế:** Khối `try (Resource res = new Resource())` đảm bảo hàm `res.close()` sẽ luôn luôn được tự động gọi khi luồng thực thi rời khỏi khối `try`, bất kể có exception xảy ra hay không.
- **Điều kiện bắt buộc:** Biến tài nguyên được khai báo trong ngoặc tròn của `try` **phải implement interface `java.lang.AutoCloseable`** (hoặc con của nó là `java.io.Closeable`).
- **Ưu điểm:** Loại bỏ hoàn toàn mã thừa thãi `finally { res.close(); }`, tránh rò rỉ tài nguyên (Resource Leak), và tự động xử lý các trường hợp ngoại lệ bị che lấp (Suppressed Exceptions).

### 8.7. Thứ tự `catch` có quan trọng không? Nếu để `catch (Exception e)` trước `catch (IOException e)` thì sao?
- **Thứ tự CỰC KỲ QUAN TRỌNG:** Phải luôn bắt các Exception **từ cụ thể đến chung chung (từ lớp con tới lớp cha)**.
- **Nếu để `catch (Exception e)` trước `catch (IOException e)`:**
  - Chương trình sẽ **bị lỗi biên dịch (Compilation Error: Unreachable code)**.
  - *Lý do:* Vì `IOException` là lớp con kế thừa từ `Exception`. Khi có ngoại lệ `IOException` xảy ra, khối `catch (Exception e)` nằm ở trên đã tóm gọn nó trước, khiến cho khối `catch (IOException e)` phía dưới sẽ **vĩnh viễn không bao giờ được chạm tới**.

### 8.8. Giải thích nguyên tắc "Throw early, Catch late"
- **Throw early (Ném lỗi càng sớm càng tốt):** Ngay khi phát hiện tham số không hợp lệ hoặc điều kiện tiên quyết bị vi phạm ở đầu hàm, ném ngoại lệ ngay lập tức (ví dụ: `if (id == null) throw new IllegalArgumentException();`). Tránh để dữ liệu sai đi sâu vào hệ thống rồi mới phát sinh lỗi khó đoán ở tầng Database.
- **Catch late (Bắt lỗi càng muộn càng tốt):** Không nên vội vàng đặt `try-catch` ở khắp mọi hàm nhỏ nếu hàm đó không biết cách khắc phục lỗi. Hãy để ngoại lệ nổi lên (bubble up) tới các tầng trên cùng (như Controller hoặc Global Exception Handler) - nơi có bức tranh toàn cảnh và thẩm quyền quyết định: ghi log ra sao, rollback transaction thế nào, và trả thông điệp gì cho người dùng.

---

<div style="page-break-before: always;"></div>

<a id="phase-2"></a>

# PHASE 2: HƯỚNG ĐỐI TƯỢNG (OOP) & COLLECTIONS FRAMEWORK

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-01"></a>

# Chapter 01: 4 Trụ Cột OOP (Encapsulation, Inheritance, Polymorphism, Abstraction)

## 1. Lập trình hướng đối tượng (OOP) là gì?
- OOP tổ chức code xoay quanh **đối tượng** (Object) thay vì chỉ là hàm và biến rời rạc.
- Mỗi Object là 1 thực thể có **thuộc tính** (field/property) và **hành vi** (method).
- Java là ngôn ngữ OOP thuần tuý: mọi thứ đều nằm trong Class.

### Class vs Object
```java
// Class = bản thiết kế (blueprint)
public class User {
    private String name;
    private int age;
    
    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// Object = thực thể tạo từ Class
User user1 = new User("An", 25);   // Object 1
User user2 = new User("Bình", 30); // Object 2
```

## 2. Trụ cột 1: Đóng gói (Encapsulation)
> Ẩn dữ liệu bên trong, chỉ cho phép truy cập thông qua các method công khai.

```java
public class BankAccount {
    private double balance;  // ẨN: không cho truy cập trực tiếp từ bên ngoài

    public BankAccount(double initialBalance) {
        if (initialBalance < 0) throw new IllegalArgumentException("Số dư không hợp lệ");
        this.balance = initialBalance;
    }

    // Getter: cho phép ĐỌC
    public double getBalance() {
        return balance;
    }

    // Method công khai: KIỂM SOÁT cách thay đổi dữ liệu
    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("Số tiền phải > 0");
        this.balance += amount;
    }

    public void withdraw(double amount) {
        if (amount > balance) throw new IllegalArgumentException("Số dư không đủ");
        this.balance -= amount;
    }
}

// Sử dụng:
BankAccount acc = new BankAccount(1000);
// acc.balance = -9999;  // ❌ Compile Error (private)
acc.deposit(500);        // ✅ Qua method kiểm soát
```

### Access Modifiers (Phạm vi truy cập)
| Modifier | Cùng Class | Cùng Package | Subclass (khác package) | Mọi nơi |
|----------|-----------|-------------|------------------------|---------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` (không ghi) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

> 💡 **Quy tắc:** Field luôn `private`, method public/protected tuỳ mục đích.

## 3. Trụ cột 2: Kế thừa (Inheritance)
> Class con **kế thừa** thuộc tính và phương thức từ Class cha, mở rộng hoặc ghi đè.

```java
// Class cha
public class Employee {
    protected String name;
    protected double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double calculateBonus() {
        return salary * 0.1;  // Thưởng 10%
    }
}

// Class con kế thừa
public class Manager extends Employee {
    private int teamSize;

    public Manager(String name, double salary, int teamSize) {
        super(name, salary);    // Gọi constructor cha
        this.teamSize = teamSize;
    }

    @Override
    public double calculateBonus() {
        return salary * 0.2 + teamSize * 500;  // Thưởng 20% + 500/người
    }
}
```

### Lưu ý quan trọng
- Java chỉ hỗ trợ **đơn kế thừa** (1 class chỉ extends 1 class cha).
- Từ khoá `super`: gọi constructor hoặc method của class cha.
- Từ khoá `this`: tham chiếu tới object hiện tại.
- Class `Object` là cha của mọi class trong Java.

## 4. Trụ cột 3: Đa hình (Polymorphism)

### 4.1 Compile-time Polymorphism: Overloading (Nạp chồng)
Cùng **tên method**, khác **tham số** (số lượng, kiểu, thứ tự).

```java
public class Calculator {
    public int add(int a, int b) { return a + b; }
    public double add(double a, double b) { return a + b; }
    public int add(int a, int b, int c) { return a + b + c; }
}
```

### 4.2 Runtime Polymorphism: Overriding (Ghi đè)
Class con **ghi đè** method cha, JVM quyết định chạy method nào tại **runtime**.

```java
Employee emp = new Manager("An", 5000, 10);
System.out.println(emp.calculateBonus());  
// Gọi method của Manager (runtime), KHÔNG phải Employee!
```

### 4.3 So sánh

| | Overloading | Overriding |
|---|-----------|-----------|
| Thời điểm | Compile-time | Runtime |
| Tên method | Giống | Giống |
| Tham số | **Khác** | **Giống** |
| Return type | Có thể khác | Giống hoặc covariant |
| Annotation | — | `@Override` |
| Phạm vi | Cùng class | Cha – Con |

## 5. Trụ cột 4: Trừu tượng (Abstraction)
> Ẩn chi tiết triển khai, chỉ lộ ra **"cái gì"** chứ không lộ **"làm thế nào"**.

### Dùng Abstract Class
```java
public abstract class Shape {
    protected String color;

    public Shape(String color) { this.color = color; }

    // Method trừu tượng: KHÔNG có body, bắt buộc class con triển khai
    public abstract double calculateArea();

    // Method thường: có body, class con kế thừa được
    public String getColor() { return color; }
}

public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;  // Triển khai cụ thể
    }
}
```

- **Không thể** tạo object trực tiếp từ abstract class (`new Shape()` → ❌).
- Có thể có cả abstract method và method thường.

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Giải thích 4 trụ cột OOP bằng ví dụ thực tế (Hệ thống Ngân hàng)
1. **Encapsulation (Đóng gói):**
   - *Ví dụ:* Lớp `BankAccount` có biến `private double balance;`. Người ngoài không thể tùy tiện gán `account.balance = 999999999;`. Muốn nạp tiền, bắt buộc phải thông qua hàm `public void deposit(double amount)` - nơi code sẽ kiểm tra điều kiện `amount > 0` và ghi lại lịch sử giao dịch.
2. **Inheritance (Kế thừa):**
   - *Ví dụ:* Lớp cha `Account` có chung các thuộc tính `accountNumber`, `ownerName`, `balance`. Các lớp con `SavingAccount` (tài khoản tiết kiệm có thêm `interestRate`) và `CreditAccount` (tài khoản tín dụng có thêm `creditLimit`) kế thừa lại code từ cha, tránh trùng lặp.
3. **Polymorphism (Đa hình):**
   - *Ví dụ:* Lớp cha `Payment` có hàm `pay(double amount)`. Khi gọi `payment.pay(100)`, nếu đối tượng thực tế là `CreditCardPayment` thì sẽ trừ thẻ tín dụng, nếu là `VnPayPayment` thì sinh mã QR, nếu là `MomoPayment` thì mở app Momo. Cùng một lời gọi hàm nhưng có nhiều cách biểu hiện khác nhau tùy theo đối tượng lúc runtime.
4. **Abstraction (Trừu tượng hóa):**
   - *Ví dụ:* Khi bạn rút tiền ở cây ATM, bạn chỉ cần đưa thẻ, bấm số tiền và nhận tiền mặt (`atm.withdraw(500000)`). Bạn hoàn toàn không cần biết bên trong cây ATM kết nối viễn thông ra sao, kiểm tra số dư ở chi nhánh nào, cơ chế đếm tờ tiền cơ học chạy như thế nào. Trừu tượng hóa giúp ẩn đi sự phức tạp bên trong và chỉ lộ ra giao diện sử dụng cần thiết.

### 6.2. Tại sao nên để field là `private`? Encapsulation giải quyết vấn đề gì?
- **Kiểm soát tính hợp lệ của dữ liệu (Data Validation):** Nếu field là `public`, bất kỳ ai cũng có thể gán `age = -5` hoặc `email = "khong-phai-email"`. Với `private` kết hợp getter/setter, ta có thể chặn dữ liệu rác ngay tại setter.
- **Tính toàn vẹn và bất biến (Immutability / Read-only):** Ta có thể tạo các trường chỉ đọc (chỉ cung cấp hàm Getter mà không có Setter).
- **Linh hoạt thay đổi logic nội bộ mà không làm hỏng code bên ngoài:** Ví dụ ban đầu lưu `fullName`, sau này tách thành `firstName` và `lastName`. Nếu code ngoài gọi `getFullName()`, ta chỉ cần sửa code bên trong hàm getter đó mà không làm crash hàng trăm file khác đang dùng.

### 6.3. Phân biệt Overloading (Nạp chồng) và Overriding (Ghi đè)
| Tiêu chí | Method Overloading | Method Overriding |
| :--- | :--- | :--- |
| **Vị trí** | Trong **cùng một class**. | Giữa **class con** và **class cha** (quan hệ kế thừa). |
| **Tên phương thức** | **Bắt buộc giống nhau**. | **Bắt buộc giống nhau**. |
| **Danh sách tham số** | **Bắt buộc phải khác nhau** (số lượng, kiểu dữ liệu, hoặc thứ tự). | **Bắt buộc phải giống hệt** class cha. |
| **Kiểu trả về** | Có thể giống hoặc khác. | Phải giống hoặc là kiểu con (Covariant return type). |
| **Thời điểm phân giải** | **Compile-time** (Static Polymorphism - dựa vào tham số lúc gọi). | **Runtime** (Dynamic Polymorphism - dựa vào kiểu đối tượng thực tế trên Heap). |
| **Annotation** | Không dùng. | Dùng `@Override` để nhờ compiler kiểm tra tính chính xác. |

### 6.4. Java có hỗ trợ đa kế thừa (Multiple Inheritance) không? Tại sao? Giải pháp thay thế?
- **Câu trả lời:** Java **KHÔNG** hỗ trợ đa kế thừa class (`class C extends A, B` $\rightarrow$ ❌ Lỗi biên dịch).
- **Tại sao Java cấm đa kế thừa class?**
  - Để tránh bài toán hiểm hóc **Kim Cương (The Diamond Problem)**: Giả sử cả Class `A` và Class `B` đều có hàm `display()`. Class `C` kế thừa cả `A` và `B`. Khi gọi `c.display()`, JVM sẽ không thể biết được nên chạy hàm `display()` của `A` hay của `B`, dẫn tới sự nhập nhằng mơ hồ.
- **Giải pháp thay thế:**
  1. **Triển khai nhiều Interface (Multiple Interfaces):** Một class có thể `implements` vô số interface: `class C implements InterfaceA, InterfaceB`.
  2. **Ưu tiên Thành phần hơn Kế thừa (Composition over Inheritance):** Thay vì kế thừa, ta nhét các object của `A` và `B` làm thuộc tính bên trong `C`:
     ```java
     class C {
         private A a = new A();
         private B b = new B();
     }
     ```

### 6.5. Abstract class có thể có Constructor không? Mục đích?
- **Câu trả lời:** **CÓ THỂ VÀ HOÀN TOÀN HỢP LỆ.** Mặc dù không thể gọi `new AbstractClass()` trực tiếp.
- **Mục đích:**
  1. Khởi tạo các thuộc tính chung mà lớp cha quản lý (ví dụ: `id`, `createdAt`, `color`).
  2. Khi một class con được khởi tạo (`new Dog()`), constructor của class con **bắt buộc phải gọi `super(...)`** để khởi tạo phần thuộc tính của class cha trước tiên theo đúng thứ tự phân cấp bộ nhớ.
  3. Áp dụng Design Pattern (ví dụ: Template Method Pattern), ép buộc các giá trị mặc định phải có ngay khi tạo đối tượng con.

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-02"></a>

# Chapter 02: Interface vs Abstract Class & Default/Static Methods

## 1. Interface là gì?
- Interface là **hợp đồng** (contract) định nghĩa các method mà class phải triển khai.
- Mặc định tất cả method trong interface là `public abstract` (trước Java 8).

```java
public interface PaymentService {
    void pay(double amount);            // abstract (bắt buộc triển khai)
    boolean refund(String transactionId);
}

public class VnPayService implements PaymentService {
    @Override
    public void pay(double amount) {
        System.out.println("Thanh toán qua VNPay: " + amount + "đ");
    }
    @Override
    public boolean refund(String txId) {
        System.out.println("Hoàn tiền VNPay: " + txId);
        return true;
    }
}

public class MomoService implements PaymentService {
    @Override
    public void pay(double amount) {
        System.out.println("Thanh toán qua Momo: " + amount + "đ");
    }
    @Override
    public boolean refund(String txId) { return false; }
}
```

### Đa kế thừa qua Interface
```java
public interface Loggable { void log(String message); }
public interface Auditable { void audit(); }

// 1 class có thể implements NHIỀU interface
public class OrderService implements PaymentService, Loggable, Auditable {
    // Phải triển khai TẤT CẢ method từ 3 interface
}
```

## 2. Default & Static Methods (Java 8+)

### 2.1 Default Method
```java
public interface PaymentService {
    void pay(double amount);

    // Default method: CÓ body, class con kế thừa mà không cần override
    default String getPaymentStatus() {
        return "PENDING";
    }
}
// VnPayService tự động có method getPaymentStatus() mà không cần viết lại
```

- Mục đích: Thêm method mới vào interface **mà không phá vỡ** các class đã implement.

### 2.2 Static Method
```java
public interface PaymentService {
    static PaymentService create(String provider) {
        return switch (provider) {
            case "vnpay" -> new VnPayService();
            case "momo"  -> new MomoService();
            default -> throw new IllegalArgumentException("Unknown: " + provider);
        };
    }
}

// Gọi qua tên interface
PaymentService payment = PaymentService.create("vnpay");
```

### 2.3 Diamond Problem
```java
interface A { default void hello() { System.out.println("A"); } }
interface B { default void hello() { System.out.println("B"); } }

// Class phải override để giải quyết xung đột
class C implements A, B {
    @Override
    public void hello() {
        A.super.hello();  // Chọn gọi A
    }
}
```

## 3. So sánh Interface vs Abstract Class

| Tiêu chí | Interface | Abstract Class |
|----------|-----------|---------------|
| Từ khoá | `implements` | `extends` |
| Đa kế thừa | ✅ Nhiều interface | ❌ Chỉ 1 class |
| Constructor | ❌ Không có | ✅ Có |
| Field | Chỉ `public static final` (hằng số) | Mọi loại field |
| Method có body | `default`, `static` (Java 8+) | Method thường + abstract |
| Khi nào dùng | Định nghĩa **hành vi chung** (contract) | Chia sẻ **code chung** giữa các class liên quan |

### Quy tắc chọn
- **Interface**: Khi các class **không liên quan** về mặt kế thừa nhưng cần cùng 1 hành vi (VD: `PaymentService` cho VNPay, Momo, Stripe).
- **Abstract Class**: Khi các class **có quan hệ IS-A** rõ ràng và chia sẻ code chung (VD: `Shape` → `Circle`, `Rectangle`).

## 4. Câu hỏi phỏng vấn & Trả lời chi tiết

### 4.1. Interface và Abstract Class khác nhau thế nào? Khi nào dùng cái nào?
- **Khác biệt cốt lõi:**
  - **Interface là "Bản hợp đồng về hành vi" (Contract - CAN-DO):** Nhấn mạnh đối tượng **có thể làm được gì**, không quan tâm đối tượng đó là ai (vd: `Flyable`, `Serializable`, `PaymentService`).
  - **Abstract Class là "Bản thiết kế gốc chung" (Identity - IS-A):** Nhấn mạnh đối tượng **bản chất là cái gì**, dùng để chia sẻ cấu trúc thuộc tính và hành vi chung cho các class con có quan hệ họ hàng mật thiết (vd: `Animal` $\rightarrow$ `Dog, Cat`, `BaseEntity` $\rightarrow$ `User, Product`).
- **Khi nào chọn cái nào:**
  - **Chọn Interface khi:** Muốn định nghĩa chuẩn giao tiếp (API contract), muốn hỗ trợ đa triển khai (loose coupling trong Spring Boot Service layer), hoặc khi các class triển khai hoàn toàn không có họ hàng với nhau (ví dụ cả `Bird` và `Airplane` đều `implements Flyable`).
  - **Chọn Abstract Class khi:** Cần chia sẻ mã nguồn dùng chung (code reuse), cần có thuộc tính non-static (trạng thái riêng của object), hoặc cần có Constructor để khởi tạo dữ liệu chung.

### 4.2. Default method trong Interface giải quyết vấn đề gì?
- **Vấn đề lịch sử (trước Java 8):** Interface chỉ chứa abstract method. Khi một thư viện mở rộng thêm 1 hàm mới vào Interface, **hàng ngàn class đang implements interface đó trên toàn thế giới sẽ lập tức bị lỗi biên dịch** vì chưa override hàm mới đó.
- **Giải pháp của Java 8:** Bổ sung từ khóa `default`:
  ```java
  public interface List<E> {
      default void sort(Comparator<? super E> c) {
          // Cung cấp sẵn mã nguồn mặc định
      }
  }
  ```
  Nhờ có `default method`, Java có thể thêm các tính năng hiện đại (như `.stream()`, `.forEach()`, `.sort()`) vào Collection Interface mà vẫn đảm bảo **tính tương thích ngược (Backward Compatibility)** hoàn hảo.

### 4.3. Diamond Problem là gì? Java giải quyết thế nào với Default Method?
- **Diamond Problem với Interface:** Nếu Class `C` triển khai 2 Interface `A` và `B`, mà cả `A` và `B` đều có cùng một hàm `default void print()`.
- **Cách Java bắt buộc xử lý:** Trình biên dịch Java sẽ phát hiện xung đột và **báo lỗi biên dịch ngay lập tức**. Java ép lập trình viên tại Class `C` **bắt buộc phải Override lại hàm `print()`** để chỉ định rõ ràng muốn dùng triển khai của interface nào:
  ```java
  public class C implements A, B {
      @Override
      public void print() {
          // Cách 1: Chỉ định gọi cụ thể của A
          A.super.print();
          // Hoặc Cách 2: Tự viết lại logic riêng hoàn toàn cho C
      }
  }
  ```

### 4.4. Có thể tạo biến (field) trong Interface không? Có ràng buộc gì?
- **Câu trả lời:** Có thể khai báo trường dữ liệu trong Interface, nhưng **chỉ duy nhất dưới dạng HẰNG SỐ**.
- **Ràng buộc mặc định:** Dù bạn không viết từ khóa nào, JVM luôn tự động ngầm định mọi field trong Interface đều là:
  $$\text{public static final}$$
  - `public`: Bất kỳ đâu cũng có thể truy cập được.
  - `static`: Thuộc về chính interface đó, không gắn liền với instance.
  - `final`: Phải gán giá trị ngay khi khai báo và không bao giờ được phép thay đổi.
  - *Lưu ý:* Không thể khai báo biến instance bình thường (như `private int count;`) trong Interface.

### 4.5. Tại sao Java cấm đa kế thừa class nhưng lại cho phép đa kế thừa interface?
- **Với Class:** Chứa thuộc tính (State) và thân hàm (Implementation). Đa kế thừa class sẽ dẫn tới:
  1. Xung đột trạng thái (hai cha đều có field `int x`, con sẽ có 2 ô nhớ `x` hay 1?).
  2. Xung đột Constructor (thứ tự gọi `super()` từ cha nào trước?).
  3. Lỗi Diamond Problem khó lường lúc runtime.
- **Với Interface:** Thuần túy là "đặc tả giao diện" (chỉ có tên hàm và tham số). Kể cả 2 interface có hàm trùng tên, class con cũng chỉ cần triển khai một thân hàm duy nhất để thỏa mãn cả 2 giao diện. Không có xung đột bộ nhớ, không có vấn đề Constructor, do đó hoàn toàn an toàn và trong sáng.

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-03"></a>

# Chapter 03: 5 Nguyên Lý SOLID trong Java Backend

## Tổng quan
SOLID là 5 nguyên lý thiết kế hướng đối tượng giúp code **dễ bảo trì**, **dễ mở rộng** và **dễ test**.

## 1. S – Single Responsibility Principle (SRP)
> Mỗi class chỉ có **một lý do duy nhất để thay đổi** (một nhiệm vụ duy nhất).

```java
// ❌ Vi phạm SRP: UserService vừa xử lý user, vừa gửi email, vừa ghi log
public class UserService {
    public void createUser(User user) { /* lưu DB */ }
    public void sendWelcomeEmail(User user) { /* gửi email */ }
    public void writeLog(String message) { /* ghi log */ }
}

// ✅ Tuân thủ SRP: Mỗi class 1 nhiệm vụ
public class UserService { public void createUser(User user) { /* lưu DB */ } }
public class EmailService { public void sendEmail(String to, String content) { } }
public class LogService { public void log(String message) { } }
```

## 2. O – Open/Closed Principle (OCP)
> **Mở** cho việc mở rộng, **Đóng** cho việc sửa đổi code cũ.

```java
// ❌ Vi phạm: Mỗi lần thêm hình dạng mới phải SỬA method calculateArea
public double calculateArea(Shape shape) {
    if (shape.type.equals("circle")) return Math.PI * shape.radius * shape.radius;
    if (shape.type.equals("rectangle")) return shape.width * shape.height;
    // Thêm triangle? Phải sửa method này...
}

// ✅ Tuân thủ: Thêm hình dạng mới = tạo class mới, KHÔNG sửa code cũ
public abstract class Shape {
    public abstract double calculateArea();
}
public class Circle extends Shape {
    @Override public double calculateArea() { return Math.PI * radius * radius; }
}
public class Triangle extends Shape {  // MỞ RỘNG mà không sửa code cũ
    @Override public double calculateArea() { return 0.5 * base * height; }
}
```

## 3. L – Liskov Substitution Principle (LSP)
> Class con phải **thay thế được** class cha mà không làm sai logic chương trình.

```java
// ❌ Vi phạm: Chim cánh cụt không bay được nhưng kế thừa Bird có fly()
public class Bird { public void fly() { System.out.println("Bay"); } }
public class Penguin extends Bird {
    @Override public void fly() { throw new UnsupportedOperationException("Không bay được!"); }
}

// ✅ Tuân thủ: Tách interface riêng
public interface Flyable { void fly(); }
public class Sparrow implements Flyable { public void fly() { /* bay */ } }
public class Penguin { /* không implements Flyable */ }
```

## 4. I – Interface Segregation Principle (ISP)
> **Không** ép class implement interface mà nó **không cần**.

```java
// ❌ Vi phạm: Interface quá lớn
public interface Worker {
    void code();
    void test();
    void manageTeam();  // Developer không cần quản lý team!
}

// ✅ Tuân thủ: Tách nhỏ
public interface Coder { void code(); }
public interface Tester { void test(); }
public interface TeamLeader { void manageTeam(); }

public class Developer implements Coder, Tester { /* chỉ code và test */ }
public class Manager implements TeamLeader { /* chỉ quản lý */ }
```

## 5. D – Dependency Inversion Principle (DIP)
> Module cấp cao **không phụ thuộc** module cấp thấp. Cả hai phụ thuộc **abstraction** (interface).
> Đây chính là **nền tảng của Spring Dependency Injection**.

```java
// ❌ Vi phạm: OrderService phụ thuộc TRỰC TIẾP vào MySQLOrderRepository
public class OrderService {
    private MySQLOrderRepository repo = new MySQLOrderRepository(); // Tight coupling!
}

// ✅ Tuân thủ: Phụ thuộc Interface, inject implementation từ bên ngoài
public interface OrderRepository { void save(Order order); }
public class MySQLOrderRepository implements OrderRepository { /* MySQL */ }
public class MongoOrderRepository implements OrderRepository { /* MongoDB */ }

public class OrderService {
    private final OrderRepository repo;  // Phụ thuộc Interface (abstraction)
    public OrderService(OrderRepository repo) { this.repo = repo; }  // Inject qua constructor
}

// Dễ dàng đổi implementation mà KHÔNG sửa OrderService
OrderService service = new OrderService(new MongoOrderRepository());
```

## 6. Bảng tóm tắt

| Nguyên lý | Ý nghĩa ngắn gọn | Từ khoá nhớ |
|-----------|-------------------|-------------|
| **S** | 1 class = 1 nhiệm vụ | "Tách nhỏ" |
| **O** | Mở rộng mà không sửa code cũ | "Thêm mới, không sửa" |
| **L** | Class con thay thế được cha | "Đổi con vẫn chạy đúng" |
| **I** | Interface nhỏ, chuyên biệt | "Không ép làm thừa" |
| **D** | Phụ thuộc Interface, không phụ thuộc class cụ thể | "Tiền đề Spring DI" |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Giải thích SOLID bằng ví dụ thực tế trong Java Backend
1. **S - Single Responsibility Principle (Đơn trách nhiệm):**
   - *Vi phạm:* Một class `OrderController` vừa nhận HTTP request, vừa tính toán thuế/kho, vừa gọi câu lệnh SQL `INSERT INTO orders...`, vừa tự bắn email cho khách.
   - *Chuẩn:* Tách thành `OrderController` (HTTP routing) $\rightarrow$ `OrderService` (nghiệp vụ tính toán) $\rightarrow$ `OrderRepository` (lưu DB) $\rightarrow$ `NotificationService` (gửi mail).
2. **O - Open/Closed Principle (Đóng để sửa, Mở để thêm):**
   - *Ví dụ:* Hệ thống thanh toán có `PaymentService`. Khi tích hợp thêm cổng thanh toán mới (như Apple Pay), ta chỉ cần tạo class mới `ApplePayStrategy implements PaymentStrategy` mà không phải vào sửa đổi chuỗi `if-else` trong code cũ.
3. **L - Liskov Substitution Principle (Thay thế Liskov):**
   - *Ví dụ:* Class cha `ReadOnlyRepository` có hàm `findById()`. Class con `UserRepository` kế thừa từ nó thì bất kỳ chỗ nào nhận `ReadOnlyRepository` đều có thể truyền `UserRepository` vào thay thế mà chương trình vẫn chạy chính xác, không văng ngoại lệ bất thường `UnsupportedOperationException`.
4. **I - Interface Segregation Principle (Phân tách Interface):**
   - *Ví dụ:* Thay vì một `SuperWorkerInterface` có cả `work()`, `eat()`, `sleep()`, ép cả `RobotWorker` phải triển khai `eat()`. Ta tách thành `Workable` và `Eatable`. `RobotWorker` chỉ cần `implements Workable`.
5. **D - Dependency Inversion Principle (Đảo ngược phụ thuộc):**
   - *Ví dụ:* `UserService` không được `new MySQLUserRepository()` trực tiếp trong thân class. Thay vào đó, `UserService` phụ thuộc vào interface `UserRepository`. Việc đưa implementation nào vào sẽ do Spring Boot lo thông qua Dependency Injection.

### 7.2. Nguyên lý nào là nền tảng của Dependency Injection trong Spring?
- **Nguyên lý chữ D: Dependency Inversion Principle (DIP).**
- **Cơ chế:**
  - *Module cấp cao (High-level - như Service)* không được phụ thuộc trực tiếp vào *Module cấp thấp (Low-level - như Database Repository, Third-party SDK)*. Cả hai phải cùng phụ thuộc vào **sự trừu tượng (Abstraction / Interface)**.
  - Spring Framework hiện thực hóa nguyên lý này thông qua cơ chế **Inversion of Control (IoC)** và **Dependency Injection (DI)**: Spring Container sẽ tự động tìm kiếm Bean phù hợp và "tiêm" (inject) vào Service qua Constructor lúc khởi động ứng dụng.

### 7.3. Cho ví dụ vi phạm SRP và cách Refactor trong thực tế
- **Đoạn code vi phạm:**
  ```java
  public class UserService {
      public void registerUser(User user) {
          // 1. Validate email, password
          if (!user.getEmail().contains("@")) throw new RuntimeException("Invalid email");
          
          // 2. Lưu vào Database
          String sql = "INSERT INTO users VALUES (...)";
          jdbcTemplate.update(sql);
          
          // 3. Gửi email kích hoạt
          JavaMailSender.sendMail(user.getEmail(), "Welcome!");
      }
  }
  ```
  Class này có tới 3 lý do để bị sửa đổi: khi quy tắc validate đổi, khi câu lệnh SQL đổi, hoặc khi mẫu email đổi.
- **Refactor chuẩn SRP:**
  ```java
  @Service
  @RequiredArgsConstructor
  public class UserService {
      private final UserValidator validator;
      private final UserRepository repository;
      private final EmailService emailService;

      public void registerUser(User user) {
          validator.validate(user);
          User savedUser = repository.save(user);
          emailService.sendWelcomeEmail(savedUser.getEmail());
      }
  }
  ```

### 7.4. OCP áp dụng trong Spring Boot thế nào? (Strategy Pattern + @Service)
Spring Boot hỗ trợ triển khai Open/Closed Principle cực kỳ thanh lịch thông qua **Strategy Pattern** và tính năng **Auto-wiring Map/List Beans**:
```java
// 1. Interface chung
public interface PaymentGateway {
    String getPaymentType(); // "MOMO", "VNPAY", "ZALOPAY"
    void process(double amount);
}

// 2. Các Service triển khai độc lập
@Service
public class MomoGateway implements PaymentGateway {
    public String getPaymentType() { return "MOMO"; }
    public void process(double amount) { /* Logic Momo */ }
}

@Service
public class VnPayGateway implements PaymentGateway {
    public String getPaymentType() { return "VNPAY"; }
    public void process(double amount) { /* Logic VNPay */ }
}

// 3. Quản lý tập trung không cần if-else
@Service
public class PaymentFactory {
    private final Map<String, PaymentGateway> gatewayMap;

    // Spring tự động quét tất cả các bean implements PaymentGateway và nhét vào Map!
    public PaymentFactory(List<PaymentGateway> gateways) {
        gatewayMap = gateways.stream()
            .collect(Collectors.toMap(PaymentGateway::getPaymentType, Function.identity()));
    }

    public void pay(String type, double amount) {
        PaymentGateway gateway = gatewayMap.get(type);
        if (gateway == null) throw new IllegalArgumentException("Cổng không hỗ trợ: " + type);
        gateway.process(amount);
    }
}
```
$\rightarrow$ **Khi cần thêm cổng thanh toán ZaloPay:** Ta chỉ cần tạo class mới `ZaloPayGateway implements PaymentGateway`. Class `PaymentFactory` hoàn toàn **đóng để sửa (không cần sửa một dòng code nào)** nhưng hệ thống vẫn **mở rộng thêm tính năng mới thành công**!

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-04"></a>

# Chapter 04: Java Collections Framework – List, Set, Map, Queue

## 1. Tổng quan Collections Framework
```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              JAVA COLLECTIONS FRAMEWORK                                │
├────────────────────────────────────────────────────────────┬───────────────────────────┤
│                    COLLECTION HIERARCHY                    │       MAP HIERARCHY       │
│                                                            │ (Không kế thừa Collection)│
│                        ┌──────────┐                        │                           │
│                        │ Iterable │                        │                           │
│                        └────┬─────┘                        │                           │
│                             ▼                              │                           │
│                       ┌────────────┐                       │                           │
│                       │ Collection │                       │                           │
│                       └─────┬──────┘                       │                           │
│         ┌───────────────────┼───────────────────┐          │                           │
│         ▼                   ▼                   ▼          │             ▼             │
│   ┌───────────┐       ┌───────────┐       ┌───────────┐    │       ┌───────────┐       │
│   │   List    │       │    Set    │       │   Queue   │    │       │    Map    │       │
│   │(Có thứ tự,│       │(Không trùng│      │  (FIFO /  │    │       │(Key-Value)│       │
│   │ cho trùng)│       │ lặp phần tử│      │ Ưu tiên)  │    │       │           │       │
│   └─────┬─────┘       └─────┬─────┘       └─────┬─────┘    │       └─────┬─────┘       │
│         │                   │                   │          │             │             │
│   ├── ArrayList       ├── HashSet         ├── Priority     │       ├── HashMap         │
│   │                   │                   │   Queue        │       ├── LinkedHashMap   │
│   └── LinkedList      ├── LinkedHashSet   │                │       ├── TreeMap         │
│                       │                   └── ArrayDeque   │       └── Concurrent      │
│                       └── TreeSet                          │           HashMap         │
└────────────────────────────────────────────────────────────┴───────────────────────────┘
```

## 2. List Interface – Danh sách có thứ tự, cho phép trùng

### ArrayList (Dùng nhiều nhất)
- Cơ chế: **mảng động** (dynamic array), tự mở rộng khi đầy.
- `get(i)` → **O(1)** (truy xuất nhanh). `add/remove` ở giữa → **O(n)** (phải dịch phần tử).

```java
List<String> names = new ArrayList<>();
names.add("An");
names.add("Bình");
names.add("An");         // Cho phép trùng
names.get(0);            // "An" – O(1)
names.remove(1);         // Xoá "Bình" – O(n)
names.contains("An");    // true
names.size();            // 2
```

### LinkedList
- Cơ chế: **danh sách liên kết đôi** (doubly linked list).
- `add/remove` ở đầu/cuối → **O(1)**. `get(i)` → **O(n)** (phải duyệt).

| Thao tác | ArrayList | LinkedList |
|----------|-----------|------------|
| `get(i)` | **O(1)** ✅ | O(n) |
| `add(cuối)` | O(1)* | **O(1)** ✅ |
| `add/remove(giữa)` | O(n) | **O(1)** nếu có node ✅ |
| Bộ nhớ | Ít hơn | Nhiều hơn (lưu thêm pointer) |

> 💡 **Quy tắc:** 90% dùng `ArrayList`. Chỉ dùng `LinkedList` khi thêm/xóa ở đầu rất nhiều.

## 3. Set Interface – Không trùng lặp

### HashSet
- **Không thứ tự**, không trùng. Kiểm tra trùng qua `hashCode()` + `equals()`.
- `add`, `remove`, `contains` → **O(1)**.

### LinkedHashSet
- Giữ **thứ tự chèn**. Performance tương tự HashSet.

### TreeSet
- **Tự động sắp xếp** (natural ordering hoặc Comparator). Cài đặt bằng Red-Black Tree.
- `add`, `remove`, `contains` → **O(log n)**.

```java
Set<String> hashSet = new HashSet<>(List.of("Bình", "An", "Cường", "An"));
// [Cường, An, Bình] – không thứ tự, bỏ trùng "An"

Set<String> linkedSet = new LinkedHashSet<>(List.of("Bình", "An", "Cường"));
// [Bình, An, Cường] – giữ thứ tự chèn

Set<String> treeSet = new TreeSet<>(List.of("Bình", "An", "Cường"));
// [An, Bình, Cường] – sắp xếp alphabet
```

### hashCode() & equals()
```java
// Set kiểm tra trùng bằng: hashCode() → equals()
// Nếu override equals() thì PHẢI override hashCode()
public class Product {
    private Long id;
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Product p)) return false;
        return Objects.equals(id, p.id);
    }
    @Override
    public int hashCode() { return Objects.hash(id); }
}
```

## 4. Map Interface – Cặp Key-Value

### HashMap (Dùng nhiều nhất)
- Key **không trùng**, Value có thể trùng. Key cho phép 1 `null`.
- Cơ chế: Mảng Bucket → Hash Function → xử lý va chạm (LinkedList → Red-Black Tree khi > 8 node).
- `get`, `put`, `containsKey` → **O(1)** trung bình.

```java
Map<String, Integer> scores = new HashMap<>();
scores.put("An", 90);
scores.put("Bình", 85);
scores.put("An", 95);           // Key trùng → GHI ĐÈ value → An=95
scores.get("An");               // 95
scores.getOrDefault("Cường", 0);// 0 (key không tồn tại)
scores.containsKey("Bình");     // true
scores.size();                  // 2

// Duyệt Map
for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

### So sánh các Map
| | HashMap | LinkedHashMap | TreeMap | ConcurrentHashMap |
|---|---------|-------------|---------|-------------------|
| Thứ tự | Không | Thứ tự chèn | Sắp xếp theo key | Không |
| Null key | 1 null | 1 null | ❌ Không | ❌ Không |
| Thread-safe | ❌ | ❌ | ❌ | ✅ |
| Performance | O(1) | O(1) | O(log n) | O(1) |

## 5. Queue & Deque

```java
// PriorityQueue: phần tử nhỏ nhất luôn ở đầu (Min-Heap)
Queue<Integer> pq = new PriorityQueue<>();
pq.offer(30); pq.offer(10); pq.offer(20);
pq.poll();  // 10 (nhỏ nhất)

// ArrayDeque: Stack + Queue linh hoạt
Deque<String> deque = new ArrayDeque<>();
deque.push("A");   // Stack: addFirst
deque.push("B");
deque.pop();        // "B" (LIFO)
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. ArrayList vs LinkedList: Khi nào dùng cái nào?
| Tiêu chí | `ArrayList` | `LinkedList` |
| :--- | :--- | :--- |
| **Cấu trúc dữ liệu** | Mảng động (Dynamic Resizable Array). | Danh sách liên kết đôi (Doubly Linked List). |
| **Truy xuất ngẫu nhiên (`get(i)`)** | **$O(1)$ - Cực nhanh** nhờ tính toán offset chỉ mục. | **$O(n)$ - Chậm** vì phải duyệt tuần tự từ đầu hoặc đuôi danh sách đến vị trí `i`. |
| **Thêm/Xóa ở cuối danh sách** | **$O(1)$ amortized**. | **$O(1)$**. |
| **Thêm/Xóa ở đầu hoặc giữa danh sách** | **$O(n)$ - Chậm** vì phải dịch chuyển (shift) toàn bộ các phần tử phía sau. | **$O(1)$** (khi đã có con trỏ Node tại vị trí đó, chỉ cần đổi liên kết `prev` và `next`). |
| **Chi phí bộ nhớ** | Nhẹ (chỉ tốn dung lượng mảng). | Tốn nhiều RAM hơn vì mỗi Node phải lưu thêm 2 con trỏ `prev` và `next`. |
| **Thực tế:** Trong hầu hết các bài toán Backend (đọc danh sách từ DB, phân trang, duyệt dữ liệu), **`ArrayList` là sự lựa chọn mặc định** vì CPU cache locality cực kỳ tốt. Chỉ dùng `LinkedList` khi ứng dụng liên tục thêm/xóa ở đầu danh sách (như cấu trúc Queue/FIFO).

### 6.2. HashMap hoạt động bên dưới như thế nào? (Bucket, hashCode, Collision)
Mô hình cấu trúc nội bộ của `HashMap` trong Java 8+:
```
Table Array (Buckets):
Index 0: [ null ]
Index 1: [ Node: Key1=V1 ] -> [ Node: Key2=V2 ] (Linked List khi bucket <= 8 phần tử)
...
Index 7: [ TreeNode: Red-Black Tree (Khi collision > 8 phần tử -> O(log n)) ]
```
1. **Lưu dữ liệu (`put(K, V)`):**
   - JVM gọi `key.hashCode()`, sau đó áp dụng hàm hash phân tán (`hash(key)`) để tính ra vị trí **Bucket Index**:
     $$\text{index} = (n - 1) \ \& \ \text{hash}$$
   - Nếu Bucket đó đang trống: Tạo `Node(hash, key, value, null)` đặt vào bucket $\rightarrow$ Tốc độ $O(1)$.
   - Nếu Bucket đã có phần tử (**Xung đột băm - Hash Collision**):
     - Duyệt qua các Node trong bucket đó, dùng `equals()` so sánh `key`:
       + Nếu `equals() == true`: Ghi đè (update) value mới.
       + Nếu `equals() == false`: Chèn Node mới vào cuối danh sách liên kết.
2. **Cải tiến từ Java 8 (Treeification):**
   - Khi số phần tử trong 1 bucket vượt quá **`TREEIFY_THRESHOLD = 8`** (và dung lượng mảng $\ge 64$), danh sách liên kết sẽ được tự động chuyển đổi thành **Cây đỏ-đen (Red-Black Tree)**.
   - Giúp cải thiện độ phức tạp trong trường hợp va chạm tồi tệ nhất từ $O(n)$ xuống còn **$O(\log n)$**, ngăn chặn hoàn toàn tấn công HashDoS.

### 6.3. Tại sao Override `equals()` thì BẮT BUỘC phải Override `hashCode()`?
- **Quy tắc bất biến trong hợp đồng Java (Contract between equals and hashCode):**
  > *"Nếu hai đối tượng bằng nhau theo `equals()` (`a.equals(b) == true`), thì `hashCode()` của chúng BẮT BUỘC PHẢI TRẢ VỀ GIÁ TRỊ GIỐNG HỆT NHAU (`a.hashCode() == b.hashCode()`)."*
- **Hậu quả nếu vi phạm khi dùng `HashMap` / `HashSet`:**
  - Giả sử bạn tạo class `Student(id, name)`, bạn override `equals()` so sánh theo `id`, nhưng **quên override `hashCode()`**.
  - `Student s1 = new Student(1, "An");` và `Student s2 = new Student(1, "An");`
  - `s1.equals(s2)` trả về `true`.
  - Nhưng vì không override `hashCode()`, JVM dùng `hashCode()` mặc định của `Object` (dựa trên địa chỉ bộ nhớ), khiến `s1.hashCode() != s2.hashCode()`.
  - Kết quả: Khi gọi `map.put(s1, "Gioi")` rồi gọi `map.get(s2)` $\rightarrow$ **Trả về `null`!** Vì `s2` có hash khác nên `HashMap` tìm nhầm bucket khác, dẫn tới thất lạc dữ liệu.

### 6.4. So sánh HashSet vs TreeSet vs LinkedHashSet
| Tiêu chí | `HashSet` | `LinkedHashSet` | `TreeSet` |
| :--- | :--- | :--- | :--- |
| **Cấu trúc nền tảng** | Bọc bên ngoài một `HashMap`. | `HashMap` + Danh sách liên kết kép. | Cây đỏ-đen (Red-Black Tree - `TreeMap`). |
| **Thứ tự phần tử** | **Hỗn loạn**, không có bất kỳ thứ tự nào. | **Bảo toàn đúng thứ tự chèn (Insertion Order)**. | **Tự động sắp xếp tăng dần** (Natural order hoặc qua `Comparator`). |
| **Cho phép phần tử `null`** | Cho phép 1 phần tử `null`. | Cho phép 1 phần tử `null`. | **Không cho phép `null`** (ném `NullPointerException` vì cần gọi `compareTo()`). |
| **Độ phức tạp** | **$O(1)$** (thêm, xóa, tìm kiếm). | **$O(1)$** (chậm hơn HashSet một chút do cập nhật link list). | **$O(\log n)$**. |

### 6.5. `ConcurrentHashMap` khác `HashMap` thế nào trong môi trường đa luồng?
- **`HashMap`:** Hoàn toàn **không Thread-safe**. Nếu nhiều thread cùng `put()` đồng thời, có thể gây mất mát dữ liệu, ghi đè sai lệch, hoặc thậm chí gây vòng lặp vô hạn (Infinite Loop làm CPU 100% trong Java cũ).
- **`Collections.synchronizedMap(map)` hoặc `Hashtable` (Cách cũ):** Khóa toàn bộ Map (`synchronized` trên toàn bộ bảng). Bất kỳ ai đọc hay ghi đều phải xếp hàng, khiến hiệu năng cực kỳ nghèo nàn khi tải cao.
- **`ConcurrentHashMap` (Chuẩn hiện đại):**
  - **Khóa theo từng phân đoạn (Lock Striping / CAS + synchronized trên từng Node đầu bucket):** Khi một thread ghi vào Bucket số 1, các thread khác vẫn có thể đọc và ghi vào Bucket số 2, 3 hoàn toàn song song mà không bị chặn.
  - Các thao tác đọc (`get()`) diễn ra hoàn toàn không cần lock (**Lock-free**) nhờ dùng biến `volatile`, đem lại tốc độ siêu cao trong môi trường Backend đa luồng.

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-05"></a>

# Chapter 05: Generics & Bounded Type Parameters

## 1. Generics là gì?
- Generics cho phép viết code **an toàn kiểu dữ liệu** (type-safe) tại compile-time mà vẫn linh hoạt.
- Thay vì ép kiểu thủ công, compiler kiểm tra lỗi kiểu ngay khi viết code.

```java
// Không có Generics → phải ép kiểu, dễ lỗi runtime
List list = new ArrayList();
list.add("Hello");
list.add(123);               // Compile OK nhưng...
String s = (String) list.get(1);  // ❌ ClassCastException tại runtime!

// Có Generics → compiler bắt lỗi ngay
List<String> list = new ArrayList<>();
list.add("Hello");
// list.add(123);             // ❌ Compile Error (an toàn!)
String s = list.get(0);       // Không cần ép kiểu
```

## 2. Generic Class
```java
public class ApiResponse<T> {
    private int statusCode;
    private String message;
    private T data;           // T là kiểu tuỳ ý, quyết định khi tạo object

    public ApiResponse(int statusCode, String message, T data) {
        this.statusCode = statusCode;
        this.message = message;
        this.data = data;
    }
    // Getter/Setter...
}

// Sử dụng:
ApiResponse<User> userRes = new ApiResponse<>(200, "OK", new User("An"));
ApiResponse<List<Product>> productRes = new ApiResponse<>(200, "OK", productList);
```

## 3. Generic Method
```java
public class Utils {
    // <T> khai báo trước return type
    public static <T> void printArray(T[] arr) {
        for (T item : arr) System.out.print(item + " ");
    }
}

String[] names = {"An", "Bình"};
Integer[] nums = {1, 2, 3};
Utils.printArray(names);  // An Bình
Utils.printArray(nums);   // 1 2 3
```

## 4. Bounded Type Parameters
```java
// T phải là Number hoặc subclass của Number
public static <T extends Number> double sum(List<T> list) {
    double total = 0;
    for (T item : list) total += item.doubleValue();
    return total;
}

sum(List.of(1, 2, 3));        // ✅ Integer extends Number
sum(List.of(1.5, 2.5));       // ✅ Double extends Number
// sum(List.of("a", "b"));    // ❌ String không extends Number

// Multiple bounds
public <T extends Comparable<T> & Serializable> T findMax(List<T> list) { ... }
```

## 5. Wildcards (`?`)

| Wildcard | Ý nghĩa | Đọc/Ghi |
|----------|---------|---------|
| `<?>` | Bất kỳ kiểu nào | Chỉ đọc (read-only) |
| `<? extends T>` | T hoặc subclass của T | Chỉ đọc (Producer) |
| `<? super T>` | T hoặc superclass của T | Ghi được (Consumer) |

### PECS: Producer Extends, Consumer Super
```java
// Producer (đọc dữ liệu ra): extends
public double sumOfList(List<? extends Number> list) {
    double sum = 0;
    for (Number n : list) sum += n.doubleValue();  // Đọc OK
    // list.add(1);  // ❌ Không ghi được
    return sum;
}

// Consumer (ghi dữ liệu vào): super
public void addNumbers(List<? super Integer> list) {
    list.add(1);     // Ghi OK
    list.add(2);
    // Integer n = list.get(0); // ❌ Không đọc chính xác kiểu được
}
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Generics giải quyết vấn đề gì? Type Erasure là gì?
- **2 Vấn đề lớn mà Generics giải quyết:**
  1. **An toàn kiểu dữ liệu tại Compile-time (Type Safety):** Trước Java 5, `ArrayList` lưu `Object`. Lập trình viên có thể vô tình nhét nhầm `Integer` vào danh sách `String`. Đến khi chạy chương trình mới văng lỗi `ClassCastException`. Generics phát hiện và chặn đứng lỗi này ngay khi đang gõ code.
  2. **Loại bỏ việc ép kiểu thủ công (Eliminate Type Casting):** Không cần phải viết `String s = (String) list.get(0);` ở khắp mọi nơi nữa.
- **Type Erasure (Xóa bỏ kiểu) là gì?**
  - Là cơ chế của Java Compiler nhằm đảm bảo **tính tương thích ngược (Backward Compatibility)** với các phiên bản Java cũ (Java 1.4 trở về trước).
  - Lúc Compile-time: Compiler kiểm tra tính hợp lệ của kiểu `<T>`.
  - Lúc sinh Bytecode: Compiler **xóa bỏ toàn bộ thông tin generic `<T>`** và thay thế bằng kiểu giới hạn trên của nó (thường là `Object` hoặc `Number`), đồng thời tự động chèn các lệnh ép kiểu bytecode thích hợp.
  - $\rightarrow$ Do đó, lúc **Runtime**, JVM hoàn toàn không biết `List<String>` hay `List<Integer>`, đối với JVM chúng đều chỉ là `List` thông thường.

### 6.2. `<T extends Number>` nghĩa là gì? (Bounded Type Parameter)
- **Ý nghĩa:** Giới hạn trên (Upper Bound). Nó quy định rằng kiểu dữ liệu thay thế cho `T` **bắt buộc phải là `Number` hoặc là một lớp con của `Number`** (chẳng hạn như `Integer`, `Double`, `Float`, `Long`, `Byte`, `Short`).
- **Lợi ích:**
  - Ngăn không cho truyền các kiểu không hợp lệ vào (ví dụ truyền `String` hay `User` vào sẽ bị báo lỗi compile ngay).
  - Cho phép bên trong thân hàm/class được phép gọi trực tiếp các phương thức của lớp `Number` (như `.doubleValue()`, `.intValue()`) mà không cần phải ép kiểu.

### 6.3. Phân biệt `<? extends T>` và `<? super T>`. Giải thích nguyên tắc PECS
- **`<? extends T>` (Upper Bounded Wildcard):** Chấp nhận kiểu `T` hoặc bất kỳ kiểu con nào của `T`.
- **`<? super T>` (Lower Bounded Wildcard):** Chấp nhận kiểu `T` hoặc bất kỳ kiểu cha nào của `T` (lên tới `Object`).
- **Nguyên tắc vàng PECS (Producer Extends, Consumer Super):**
  - **Producer Extends:** Nếu Collection đóng vai trò là **nguồn cung cấp dữ liệu** (bạn chỉ lấy dữ liệu ra để đọc: `get()`, duyệt for) $\rightarrow$ Dùng `<? extends T>`. *(Lưu ý: Không được phép gọi `.add()` vào list này vì compiler không biết chính xác kiểu con cụ thể là gì).*
  - **Consumer Super:** Nếu Collection đóng vai trò là **nơi tiếp nhận dữ liệu** (bạn ghi dữ liệu mới vào: `add()`) $\rightarrow$ Dùng `<? super T>`. *(Lúc này an toàn 100% để add đối tượng kiểu `T` hoặc con của `T` vào list).*

### 6.4. Tại sao không thể tạo `new T()` hoặc `new T[]` trong Generic?
- **Nguyên nhân chính:** Do cơ chế **Type Erasure**.
  - Để thực thi lệnh `new T()`, JVM lúc runtime cần phải biết kích thước bộ nhớ chính xác của `T` và cần constructor cụ thể nào để gọi. Nhưng do Type Erasure, lúc runtime `T` đã bị xóa thành `Object`, JVM không thể biết `T` thực sự là gì để cấp phát.
  - Tương tự, mảng trong Java là Reifiable (lưu giữ kiểu phần tử lúc runtime để kiểm tra an toàn mảng `ArrayStoreException`), trong khi Generics lại bị Erasure lúc runtime, hai cơ chế này xung đột trực tiếp nên Java cấm `new T[10]`.
- **Cách giải quyết thực tế:**
  - Truyền đối tượng `Class<T> clazz` vào constructor và dùng Reflection: `clazz.getDeclaredConstructor().newInstance()`.
  - Hoặc tạo mảng Object rồi ép kiểu: `(T[]) new Object[size];` (như cách mã nguồn của `ArrayList` trong JDK đang làm).

---

<div style="page-break-before: always;"></div>

<a id="phase-2-chapter-06"></a>

# Chapter 06: Java 8 – Lambda, Functional Interface, Stream API & Optional

## 1. Lambda Expression
- Cú pháp viết gọn cho **anonymous class** chỉ có 1 method (Functional Interface).

```java
// Trước Java 8: Anonymous class
Comparator<String> comp = new Comparator<String>() {
    @Override
    public int compare(String a, String b) { return a.compareTo(b); }
};

// Java 8 Lambda
Comparator<String> comp = (a, b) -> a.compareTo(b);

// Method Reference (ngắn hơn nữa)
Comparator<String> comp = String::compareTo;
```

### Cú pháp Lambda
```java
(parameters) -> expression              // 1 dòng, tự return
(parameters) -> { statements; }         // Nhiều dòng, cần return tường minh
() -> System.out.println("Hello")       // Không tham số
x -> x * 2                              // 1 tham số, bỏ dấu ()
```

## 2. Functional Interface (4 cốt lõi)

| Interface | Input | Output | Method | Ví dụ |
|-----------|-------|--------|--------|-------|
| `Predicate<T>` | T | boolean | `test(T)` | Kiểm tra điều kiện |
| `Function<T,R>` | T | R | `apply(T)` | Biến đổi kiểu |
| `Consumer<T>` | T | void | `accept(T)` | Nhận và xử lý |
| `Supplier<T>` | — | T | `get()` | Cung cấp dữ liệu |

```java
Predicate<Integer> isAdult = age -> age >= 18;
isAdult.test(20);  // true

Function<String, Integer> strLen = String::length;
strLen.apply("Hello");  // 5

Consumer<String> printer = System.out::println;
printer.accept("Hi!");  // In "Hi!"

Supplier<Double> random = Math::random;
random.get();  // 0.xxxx
```

## 3. Stream API

### Pipeline: Source → Intermediate → Terminal
```java
List<String> names = List.of("An", "Bình", "Cường", "An", "Dũng");

List<String> result = names.stream()       // 1. Source
    .filter(n -> n.length() > 2)           // 2. Intermediate: lọc
    .map(String::toUpperCase)              // 2. Intermediate: biến đổi
    .distinct()                            // 2. Intermediate: loại trùng
    .sorted()                              // 2. Intermediate: sắp xếp
    .toList();                             // 3. Terminal: thu kết quả
// ["BÌNH", "CƯỜNG", "DŨNG"]
```

### Intermediate Operations (Lazy – chưa chạy ngay)
| Method | Mô tả |
|--------|-------|
| `filter(Predicate)` | Lọc phần tử thoả điều kiện |
| `map(Function)` | Biến đổi mỗi phần tử (1→1) |
| `flatMap(Function)` | Làm phẳng danh sách lồng (1→N) |
| `distinct()` | Loại phần tử trùng |
| `sorted()` / `sorted(Comparator)` | Sắp xếp |
| `limit(n)` / `skip(n)` | Giới hạn / bỏ qua n phần tử |
| `peek(Consumer)` | Debug: xem giá trị giữa pipeline |

### Terminal Operations (Kích hoạt stream chạy)
| Method | Mô tả |
|--------|-------|
| `toList()` / `collect(Collectors.toList())` | Thu về List |
| `forEach(Consumer)` | Duyệt và xử lý |
| `count()` | Đếm |
| `reduce(BinaryOperator)` | Gộp thành 1 giá trị |
| `findFirst()` / `findAny()` | Tìm phần tử (trả Optional) |
| `anyMatch` / `allMatch` / `noneMatch` | Kiểm tra điều kiện |

### Collectors nâng cao
```java
// groupingBy: Gom nhóm theo category
Map<String, List<Product>> grouped = products.stream()
    .collect(Collectors.groupingBy(Product::getCategory));

// joining: Nối chuỗi
String csv = names.stream().collect(Collectors.joining(", "));

// toMap: Chuyển về Map
Map<Long, String> idToName = users.stream()
    .collect(Collectors.toMap(User::getId, User::getName));
```

### map() vs flatMap()
```java
// map: 1 → 1
List<String> upper = List.of("an", "bình").stream()
    .map(String::toUpperCase).toList();  // ["AN", "BÌNH"]

// flatMap: 1 → N (làm phẳng)
List<List<Integer>> nested = List.of(List.of(1,2), List.of(3,4));
List<Integer> flat = nested.stream()
    .flatMap(Collection::stream).toList();  // [1, 2, 3, 4]
```

## 4. Optional\<T\> – Xử lý Null an toàn

```java
// Tạo Optional
Optional<String> opt1 = Optional.of("Hello");          // Không được null
Optional<String> opt2 = Optional.ofNullable(null);     // Cho phép null
Optional<String> opt3 = Optional.empty();              // Rỗng

// Lấy giá trị an toàn
opt2.orElse("Default");                                // "Default"
opt2.orElseGet(() -> "Computed Default");               // Lazy evaluation
opt2.orElseThrow(() -> new RuntimeException("Empty!")); // Quăng exception

// Chuỗi xử lý
Optional<User> userOpt = userRepository.findById(1L);
String email = userOpt
    .map(User::getEmail)
    .filter(e -> e.contains("@"))
    .orElse("unknown@email.com");

// ❌ Tránh dùng: opt.get() (NullPointerException nếu empty)
// ❌ Tránh dùng: opt.isPresent() rồi opt.get() (code cũ)
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Lambda Expression là gì? Khác Anonymous Class thế nào?
- **Khái niệm:** Lambda Expression là một hàm ẩn danh (Anonymous Function) không có tên, không có kiểu trả về khai báo cụ thể, cho phép truyền hành vi (Behavior) dưới dạng tham số một cách cực kỳ ngắn gọn: `(params) -> { body }`.
- **So sánh Lambda vs Anonymous Class:**
  | Tiêu chí | Lambda Expression (Java 8+) | Anonymous Class (Lớp ẩn danh cũ) |
  | :--- | :--- | :--- |
  | **Cú pháp** | Cực kỳ ngắn gọn: `x -> x * 2`. | Cồng kềnh: Phải `new Interface() { public ... }`. |
  | **Cơ chế biên dịch** | Dùng chỉ lệnh bytecode **`invokedynamic`** (không tạo file `.class` mới trên ổ đĩa, tiết kiệm Metaspace và khởi động nhanh). | Trình biên dịch sinh ra một file class riêng: `OuterClass$1.class`. |
  | **Phạm vi từ khóa `this`** | `this` trỏ tới **chính đối tượng của class bao bọc bên ngoài (Enclosing class)**. | `this` trỏ tới **bản thân thể hiện của Anonymous class đó**. |
  | **Khả năng áp dụng** | **Chỉ áp dụng** cho **Functional Interface** (interface có đúng 1 abstract method). | Áp dụng cho bất kỳ Interface hoặc Abstract class nào (kể cả có nhiều method). |

### 5.2. Kể tên 4 Functional Interface cốt lõi trong Java và mục đích
1. **`Predicate<T>` (Kiểm tra điều kiện):**
   - Method: `boolean test(T t)`
   - Nhận vào 1 đối tượng, trả về `true/false`. Thường dùng trong hàm `.filter()` của Stream (ví dụ: `u -> u.getAge() >= 18`).
2. **`Function<T, R>` (Biến đổi dữ liệu):**
   - Method: `R apply(T t)`
   - Nhận vào đối tượng kiểu `T`, biến đổi và trả về kiểu `R`. Thường dùng trong `.map()` (ví dụ: `User -> UserDTO`, `User::getName`).
3. **`Consumer<T>` (Tiêu thụ dữ liệu):**
   - Method: `void accept(T t)`
   - Nhận vào đối tượng kiểu `T` để xử lý (in ra màn hình, gửi log, lưu DB) và không trả về gì. Thường dùng trong `.forEach()` (ví dụ: `System.out::println`).
4. **`Supplier<T>` (Cung cấp dữ liệu):**
   - Method: `T get()`
   - Không nhận tham số đầu vào, tự sản sinh và trả về một đối tượng kiểu `T`. Thường dùng trong Lazy Evaluation hoặc tạo Factory (ví dụ: `() -> new NotFoundException()`).

### 5.3. Stream Intermediate vs Terminal operations? Lazy Evaluation nghĩa là gì?
- **Intermediate Operations (Thao tác trung gian):**
  - Trả về một `Stream` mới (ví dụ: `.filter()`, `.map()`, `.sorted()`, `.distinct()`, `.limit()`).
  - Có thể xâu chuỗi (chain) liên tiếp nhiều thao tác với nhau.
- **Terminal Operations (Thao tác kết thúc):**
  - Trả về một kết quả cụ thể hoặc kiểu void (ví dụ: `.collect()`, `.count()`, `.forEach()`, `.findFirst()`, `.reduce()`).
  - Khi Terminal operation được gọi, Stream sẽ thực thi và sau đó **bị đóng vĩnh viễn** (không thể tái sử dụng lại Stream đó).
- **Lazy Evaluation (Thực thi lười biếng / Trì hoãn):**
  - Các thao tác Intermediate **hoàn toàn KHÔNG chạy ngay** khi được khai báo. Chúng chỉ được kích hoạt khi và chỉ khi gặp một Terminal operation.
  - *Lợi ích:* Tối ưu hiệu năng vượt trội. Nếu bạn có danh sách 1 triệu phần tử, lọc rồi `.findFirst()`, Java sẽ dừng duyệt ngay tại phần tử đầu tiên thỏa mãn chứ không bao giờ lọc toàn bộ 1 triệu phần tử!

### 5.4. `map()` vs `flatMap()` khác nhau thế nào?
- **`map()` (Ánh xạ 1 - 1):**
  - Chuyển đổi mỗi phần tử trong Stream thành một phần tử mới.
  - Ví dụ: `Stream<String>` biến đổi thành `Stream<Integer>` (lấy độ dài chuỗi).
- **`flatMap()` (Ánh xạ 1 - Nhiều & Làm phẳng - Flatten):**
  - Chuyển đổi mỗi phần tử thành một Stream con, sau đó "làm phẳng" (merge) tất cả các Stream con đó thành **một Stream phẳng duy nhất**.
  - *Ví dụ kinh điển:* Một `Order` có danh sách `List<OrderItem>`.
    - Dùng `.map(Order::getItems)` $\rightarrow$ Trả về `Stream<List<OrderItem>>` (danh sách lồng nhau).
    - Dùng `.flatMap(order -> order.getItems().stream())` $\rightarrow$ Trả về `Stream<OrderItem>` phẳng, dễ dàng tính tổng hoặc lọc sản phẩm.

### 5.5. Tại sao nên dùng `Optional` thay vì return `null`?
1. **Loại bỏ lỗi kinh hoàng `NullPointerException` (NPE):** Ép buộc người gọi hàm phải chủ động kiểm tra và xử lý trường hợp không có dữ liệu ngay tại compile-time.
2. **Thể hiện rõ ý đồ của API:** Khi một hàm trả về `Optional<User> findById(Long id)`, người đọc hàm hiểu ngay: *"Dữ liệu này có thể có hoặc không tồn tại"*. Nếu trả về `User`, người ta dễ chủ quan gọi ngay `user.getName()` dẫn tới crash ứng dụng.
3. **Lập trình theo phong cách hàm (Functional Fluent API):** Dễ dàng xâu chuỗi logic với `.map()`, `.filter()`, `.orElseThrow()` mà không cần viết chuỗi `if (x != null)` lồng nhau rối rắm.

### 5.6. `orElse()` vs `orElseGet()` khác nhau thế nào? (Cạm bẫy Eager vs Lazy)
- **`orElse(defaultValue)` (Eager Evaluation - Đánh giá ngay lập tức):**
  - Biểu thức bên trong `orElse()` **LUÔN LUÔN ĐƯỢC TÍNH TOÁN / GỌI THỰC THI**, kể cả khi `Optional` **đang có giá trị**!
- **`orElseGet(() -> defaultValue)` (Lazy Evaluation - Đánh giá trì hoãn):**
  - Chỉ khi nào `Optional` **thực sự rỗng (`empty`)** thì hàm Supplier bên trong mới được gọi.
- *Cạm bẫy chết người trong Backend:*
  ```java
  // ❌ NGUY HIỂM: Hàm createDefaultUser() sẽ LUÔN ĐƯỢC CHẠY và gọi ghi DB tốn tài nguyên, dù userOpt đã tìm thấy!
  User user = userOpt.orElse(createDefaultUserInDatabase());

  // ✅ CHUẨN: Hàm chỉ chạy khi userOpt thực sự rỗng!
  User user = userOpt.orElseGet(() -> createDefaultUserInDatabase());
  ```

---

<div style="page-break-before: always;"></div>

<a id="phase-3"></a>

# PHASE 3: GIAO THỨC HTTP & THIẾT KẾ RESTFUL API

---

<div style="page-break-before: always;"></div>

<a id="phase-3-chapter-01"></a>

# Chapter 01: HTTP Fundamentals – Request, Response, Headers, Cookies

## 1. Giao thức HTTP
- **HTTP** (HyperText Transfer Protocol) là giao thức truyền tải dữ liệu giữa Client và Server trên nền TCP.
- Đặc tính: **Stateless** (mỗi request độc lập, server không nhớ request trước).

## 2. Cấu trúc HTTP Request
```
POST /api/v1/users HTTP/1.1          ← Request Line (Method + URL + Version)
Host: api.example.com                 ← Headers
Content-Type: application/json
Authorization: Bearer eyJhbG...
Content-Length: 85

{                                     ← Body (payload)
  "name": "An",
  "email": "an@gmail.com"
}
```

| Thành phần | Mô tả |
|-----------|-------|
| **Request Line** | Method (GET/POST...) + URL + HTTP version |
| **Headers** | Metadata: Content-Type, Authorization, Accept, Cookie... |
| **Body** | Dữ liệu gửi kèm (POST, PUT, PATCH). GET thường không có body |

## 3. Cấu trúc HTTP Response
```
HTTP/1.1 200 OK                       ← Status Line
Content-Type: application/json
Set-Cookie: sessionId=abc123

{                                     ← Response Body
  "status": 200,
  "data": {"id": 1, "name": "An"}
}
```

## 4. Headers quan trọng
| Header | Mô tả |
|--------|-------|
| `Content-Type` | Định dạng body: `application/json`, `text/html`, `multipart/form-data` |
| `Accept` | Client muốn nhận định dạng nào |
| `Authorization` | Token xác thực: `Bearer <jwt>` |
| `Cookie` / `Set-Cookie` | Quản lý session/cookie |
| `Cache-Control` | Chính sách cache |
| `X-Request-Id` | Tracking ID cho logging |

## 5. Cookie & Session
- **Cookie**: Server gửi `Set-Cookie` → Browser tự động gửi kèm trong mọi request sau.
- **Session**: Server lưu trạng thái người dùng (Stateful, ít dùng cho REST API).
- **Token (JWT)**: Stateless, client gửi trong header `Authorization: Bearer <token>` (phổ biến cho REST API).

## 6. HTTP/1.1 vs HTTP/2 vs HTTP/3
| | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---------|--------|--------|
| Multiplexing | ❌ 1 request/connection | ✅ Nhiều request/connection | ✅ |
| Header compression | ❌ | ✅ HPACK | ✅ QPACK |
| Protocol | TCP | TCP | **QUIC (UDP)** |

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. HTTP là Stateless nghĩa là gì? Làm sao để duy trì trạng thái đăng nhập?
- **HTTP là Stateless (Phi trạng thái):** Mỗi một HTTP request được gửi đi là hoàn toàn độc lập và cô lập. Máy chủ không hề lưu giữ ký ức hay biết được request hiện tại có liên quan gì đến request trước đó hay không.
- **Cách duy trì trạng thái đăng nhập:**
  1. **Session-based (Stateful):** Khi login thành công, Server tạo một Session Object trong RAM/Redis với `sessionId` ngẫu nhiên. Server trả `Set-Cookie: JSESSIONID=xyz` về Browser. Các lần gọi sau Browser tự gửi cookie này lên để Server đối chiếu.
  2. **Token-based (Stateless - Chuẩn của REST API hiện đại):** Khi login thành công, Server cấp một **JWT (JSON Web Token)** tự chứa đầy đủ thông tin (UserId, Roles, Expiration). Client lưu vào `localStorage` hoặc Secure Cookie và tự đính kèm header `Authorization: Bearer <token>` trong mỗi request. Server chỉ cần xác thực chữ ký (Signature) mà không cần query Session trong RAM.

### 7.2. Phân biệt Cookie, Session, và JWT Token
| Tiêu chí | Cookie | Session | JWT Token |
| :--- | :--- | :--- | :--- |
| **Nơi lưu trữ** | Trình duyệt Client (Browser Storage). | Máy chủ Server (RAM, Redis, DB). | Client lưu (LocalStorage/Memory/Cookie). |
| **Bản chất dữ liệu** | Đoạn text nhỏ ($\le 4\text{KB}$) tự động gửi kèm mỗi HTTP request. | Đối tượng dữ liệu lớn chứa trạng thái người dùng trên Server. | Chuỗi mã hóa (Base64Url) có chữ ký số mật mã (Signature). |
| **Mở rộng máy chủ (Scaling)** | Không ảnh hưởng Server. | **Khó scale ngang**: Cần Sticky Session hoặc phân tán Redis Cluster. | **Cực dễ scale ngang**: Bất kỳ máy chủ nào có Secret Key đều tự giải mã được. |
| **Bảo mật** | Dễ bị tấn công CSRF và XSS nếu không đặt cờ `HttpOnly` và `SameSite`. | An toàn hơn vì dữ liệu nằm ở Server, chỉ lộ SessionID. | Dễ lộ nếu lưu ở `localStorage` (XSS), không thu hồi token sớm được nếu không có Blacklist. |

### 7.3. `application/json` vs `application/x-www-form-urlencoded` khi nào dùng?
- **`application/x-www-form-urlencoded`:**
  - Dữ liệu được mã hóa thành chuỗi Key-Value nối nhau bằng dấu `&` và `=`: `name=Nguyen+Van+A&age=25`.
  - Thường dùng cho các form HTML truyền thống gửi trực tiếp từ trình duyệt, hoặc luồng OAuth2 Authorization Code / Token exchange (`/oauth/token`).
- **`application/json`:**
  - Dữ liệu ở định dạng JSON có cấu trúc phức tạp: mảng lồng nhau, object lồng object, kiểu dữ liệu boolean, number rõ ràng.
  - **Là chuẩn số 1 tuyệt đối cho các RESTful API hiện đại**, giao tiếp giữa Frontend (React/Vue/Flutter) với Backend (Spring Boot).

---

<div style="page-break-before: always;"></div>

<a id="phase-3-chapter-02"></a>

# Chapter 02: HTTP Methods & Status Codes

## 1. HTTP Methods

| Method | Mục đích | Idempotent? | Có Body? |
|--------|---------|-------------|----------|
| `GET` | Đọc / Lấy dữ liệu | ✅ | ❌ |
| `POST` | Tạo mới resource | ❌ | ✅ |
| `PUT` | Thay thế **toàn bộ** resource | ✅ | ✅ |
| `PATCH` | Cập nhật **một phần** resource | ❌ | ✅ |
| `DELETE` | Xoá resource | ✅ | ❌ thường |

### Idempotency (Tính bất biến)
> Gọi 1 lần hay gọi 10 lần, **kết quả hệ thống** vẫn như nhau.
- `GET /users/1` → luôn trả về User#1.
- `PUT /users/1 {name:"An"}` → User#1 luôn là "An".
- `DELETE /users/1` → User#1 luôn bị xoá (gọi lại trả 404).
- `POST /users` → **KHÔNG** idempotent: mỗi lần gọi tạo 1 user mới!

### PUT vs PATCH
```json
// PUT: Thay thế TOÀN BỘ (field không gửi sẽ bị null/default)
PUT /api/v1/users/1
{ "name": "An Updated", "email": "an@new.com", "age": 26 }

// PATCH: Chỉ cập nhật PHẦN gửi lên
PATCH /api/v1/users/1
{ "email": "an@new.com" }  // chỉ đổi email, name và age giữ nguyên
```

## 2. HTTP Status Codes

### 2xx – Success
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `200` | OK | GET, PUT, PATCH thành công |
| `201` | Created | POST tạo mới thành công |
| `204` | No Content | DELETE thành công (không trả body) |

### 4xx – Client Error
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `400` | Bad Request | Dữ liệu gửi lên sai format, validation fail |
| `401` | Unauthorized | **Chưa xác thực** (chưa đăng nhập, token hết hạn) |
| `403` | Forbidden | **Đã xác thực** nhưng không đủ quyền |
| `404` | Not Found | Resource không tồn tại |
| `405` | Method Not Allowed | Sai HTTP method |
| `409` | Conflict | Trùng dữ liệu (duplicate email) |
| `422` | Unprocessable Entity | Dữ liệu đúng format nhưng sai logic |
| `429` | Too Many Requests | Rate limiting |

> 🔴 **401 vs 403:** 401 = "Bạn là ai?" (chưa login). 403 = "Biết bạn rồi nhưng không có quyền".

### 5xx – Server Error
| Code | Tên | Khi nào dùng |
|------|-----|-------------|
| `500` | Internal Server Error | Bug code, exception không bắt |
| `502` | Bad Gateway | Reverse proxy không kết nối được backend |
| `503` | Service Unavailable | Server quá tải hoặc đang bảo trì |

## 3. Câu hỏi phỏng vấn & Trả lời chi tiết

### 3.1. PUT và PATCH khác nhau thế nào? Cho ví dụ
- **`PUT` (Thay thế toàn bộ tài nguyên - Complete Replacement):**
  - Client gửi lên **toàn bộ dữ liệu của đối tượng**. Những trường nào không gửi lên sẽ bị coi là mang giá trị `null` hoặc bị ghi đè thành mặc định.
  - *Ví dụ:* User có `{id: 1, name: "An", email: "an@gmail.com", role: "USER"}`.
    Nếu gửi `PUT /users/1` với body `{"name": "Bình"}` $\rightarrow$ User sau khi cập nhật sẽ bị mất email hoặc email thành `null`.
- **`PATCH` (Cập nhật một phần - Partial Modification):**
  - Client chỉ gửi **duy nhất những trường thông tin cần thay đổi**. Các trường dữ liệu khác giữ nguyên vẹn.
  - *Ví dụ:* Gửi `PATCH /users/1` với body `{"name": "Bình"}` $\rightarrow$ Chỉ có `name` đổi thành `"Bình"`, trường `email` và `role` vẫn giữ nguyên.

### 3.2. Idempotency (Tính bất biến / Tính lũy đẳng) là gì? Những method nào Idempotent?
- **Định nghĩa:** Một HTTP method được coi là **Idempotent** nếu việc bạn **thực hiện request đó 1 lần hay 100 lần liên tiếp** thì trạng thái của tài nguyên trên Server **vẫn mang lại cùng một kết quả cuối cùng hệt như nhau** (không gây tác dụng phụ - side effect phụ thêm).
- **Phân loại:**
  - **`GET`, `HEAD`, `OPTIONS`:** Vừa Idempotent vừa **Safe** (chỉ đọc dữ liệu, không làm biến đổi DB).
  - **`PUT`:** **Idempotent** (ghi đè toàn bộ tài nguyên, gửi 10 lần cùng nội dung thì bản ghi trên DB vẫn mang trạng thái đó).
  - **`DELETE`:** **Idempotent** (gọi xóa ID=5 lần đầu thì bản ghi bị xóa, các lần sau gọi lại thì bản ghi vẫn ở trạng thái đã xóa, không làm mất thêm dữ liệu khác).
  - **`POST`:** **KHÔNG Idempotent (Non-idempotent)** (mỗi lần bấm Submit gửi `POST /orders`, hệ thống sẽ tạo thêm 1 đơn hàng mới, gây duplicate đơn hàng).

### 3.3. Phân biệt 401 Unauthorized và 403 Forbidden
- **`401 Unauthorized` (Lỗi Xác thực - Authentication):**
  - Ý nghĩa: *"Bạn là ai? Tôi chưa biết bạn!"*
  - Nguyên nhân: Client chưa gửi token, gửi token sai định dạng, hoặc token đã hết hạn.
  - Cách khắc phục: Yêu cầu người dùng đăng nhập lại để lấy Token hợp lệ.
- **`403 Forbidden` (Lỗi Phân quyền - Authorization):**
  - Ý nghĩa: *"Tôi biết rõ bạn là ai rồi (bạn là User thường), nhưng bạn KHÔNG CÓ QUYỀN động vào tài nguyên này!"*
  - Nguyên nhân: Người dùng đã đăng nhập thành công, nhưng tài khoản không có quyền tương ứng (ví dụ: User thường cố tình gọi API xóa tài khoản của Admin).

### 3.4. Khi nào dùng 200, 201, 204?
- **`200 OK`:** Yêu cầu thành công và Server **có trả về dữ liệu** trong Response Body. Dùng cho hầu hết các request `GET`, `PUT`, `PATCH` thành công.
- **`201 Created`:** Yêu cầu thành công và **một tài nguyên mới vừa được khởi tạo** trong Database. Dùng cho `POST` tạo User, tạo Đơn hàng (kèm header `Location: /api/v1/orders/123`).
- **`204 No Content`:** Yêu cầu thành công nhưng Server **cố tình không trả về dữ liệu gì** trong Response Body. Rất phổ biến khi thực hiện `DELETE /users/1` thành công, hoặc cập nhật nhanh không cần trả về entity.

---

<div style="page-break-before: always;"></div>

<a id="phase-3-chapter-03"></a>

# Chapter 03: Quy chuẩn thiết kế RESTful API

## 1. REST là gì?
- **RE**presentational **S**tate **T**ransfer – kiến trúc thiết kế API dựa trên **resource** (tài nguyên).
- 6 ràng buộc: Client-Server, Stateless, Cacheable, Uniform Interface, Layered System, Code on Demand (optional).

## 2. Quy tắc đặt tên URL (Resource Naming)

### ✅ Đúng chuẩn
```
GET    /api/v1/users              → Lấy danh sách users
GET    /api/v1/users/1            → Lấy user có id=1
POST   /api/v1/users              → Tạo user mới
PUT    /api/v1/users/1            → Cập nhật toàn bộ user id=1
PATCH  /api/v1/users/1            → Cập nhật 1 phần user id=1
DELETE /api/v1/users/1            → Xoá user id=1
```

### ❌ Sai chuẩn
```
GET /api/v1/getUser?id=1          → Dùng động từ trong URL
GET /api/v1/User/1                → Viết hoa
POST /api/v1/create-user          → Động từ + kebab-case
GET /api/v1/user/1                → Số ít (nên số nhiều)
```

### Quy tắc vàng
| Quy tắc | Ví dụ |
|---------|-------|
| URL dùng **danh từ số nhiều** | `/users`, `/products`, `/orders` |
| Chữ **thường**, phân cách bằng `-` (kebab-case) | `/order-items` |
| Quan hệ cha-con qua URL lồng | `/users/{userId}/orders/{orderId}` |
| Hành động dùng **HTTP method**, KHÔNG đặt trong URL | `POST /users` thay vì `POST /createUser` |
| Versioning | `/api/v1/...`, `/api/v2/...` |

## 3. Query Parameters (Phân trang, Tìm kiếm, Lọc)
```
GET /api/v1/products?page=0&size=20&sort=price,desc&category=electronics&keyword=iphone
```

| Param | Mục đích |
|-------|---------|
| `page`, `size` | Phân trang |
| `sort` | Sắp xếp (`price,desc` hoặc `name,asc`) |
| `category`, `status` | Lọc theo trường |
| `keyword`, `q` | Tìm kiếm full-text |

### Path Variable vs Query Param
- **Path Variable** `/users/{id}`: Định danh resource cụ thể (bắt buộc).
- **Query Param** `/users?status=active`: Lọc, phân trang, tuỳ chọn.

## 4. Cấu trúc Response chuẩn

### Thành công
```json
{
  "status": 200,
  "message": "Lấy danh sách thành công",
  "data": [ { "id": 1, "name": "An" } ],
  "timestamp": "2026-09-17T10:00:00"
}
```

### Lỗi
```json
{
  "status": 400,
  "message": "Validation failed",
  "errors": [
    { "field": "email", "message": "Email không hợp lệ" },
    { "field": "name", "message": "Tên không được để trống" }
  ],
  "timestamp": "2026-09-17T10:00:00"
}
```

### Phân trang
```json
{
  "status": 200,
  "data": { "content": [...], "pageNo": 0, "pageSize": 20, "totalElements": 150, "totalPages": 8, "last": false },
  "timestamp": "2026-09-17T10:00:00"
}
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. RESTful API là gì? Kể 3 ràng buộc kiến trúc quan trọng nhất
- **RESTful API:** Là API tuân thủ theo phong cách kiến trúc **REST (Representational State Transfer)** do Roy Fielding đề xuất năm 2000, lấy **Tài nguyên (Resources)** làm trung tâm và tận dụng tối đa các chuẩn sẵn có của giao thức HTTP.
- **3 Ràng buộc kiến trúc quan trọng nhất:**
  1. **Stateless (Phi trạng thái):** Server không lưu phiên làm việc (Session) của client. Mỗi request phải tự chứa đủ thông tin để server hiểu và xác thực (Token).
  2. **Client-Server Architecture:** Tách biệt hoàn toàn giữa giao diện người dùng (Client) và logic xử lý/lưu trữ dữ liệu (Server), giúp hai bên phát triển và scale độc lập.
  3. **Cacheable (Khả năng lưu bộ đệm):** Response phải tự định nghĩa rõ ràng nó có được phép cache hay không (qua header `Cache-Control`, `ETag`) để client hoặc proxy trung gian tái sử dụng, giảm tải cho server.

### 5.2. Tại sao URL trong REST API nên dùng danh từ số nhiều (Plural Nouns)?
- **Nguyên tắc cốt lõi:** Endpoint URL dùng để **định danh tài nguyên**, còn hành động làm gì với tài nguyên đó được thể hiện bằng **HTTP Method**:
  - ❌ *Thiết kế xấu (RPC style):* `GET /getUser`, `POST /createUser`, `POST /deleteUser`
  - ✅ *Thiết kế chuẩn REST:* `GET /users`, `POST /users`, `DELETE /users/1`
- **Lý do dùng số nhiều (`/users`):**
  - Đồng nhất và trực quan: `/users` đại diện cho "tập hợp người dùng".
  - `GET /users`: Lấy danh sách cả tập hợp.
  - `POST /users`: Thêm 1 phần tử mới vào tập hợp đó.
  - `GET /users/123`: Lấy 1 phần tử cụ thể có ID 123 ra khỏi tập hợp.

### 5.3. Khi nào dùng Path Variable, khi nào dùng Query Parameter?
| Tiêu chí | Path Variable (`/users/{id}`) | Query Parameter (`/users?role=ADMIN&page=1`) |
| :--- | :--- | :--- |
| **Vị trí** | Nằm trực tiếp trong đường dẫn URL. | Nằm sau dấu chấm hỏi `?` dạng Key=Value. |
| **Mục đích** | Dùng để **định danh tài nguyên bắt buộc duy nhất** (Identity). Không thể thiếu nó để tìm đúng đối tượng. | Dùng để **lọc (filter), tìm kiếm (search), sắp xếp (sort), hoặc phân trang (pagination)**. |
| **Ví dụ** | `GET /orders/105` (Xem đơn hàng số 105), `DELETE /products/42`. | `GET /products?category=laptop&sort=price,desc&page=0&size=20`. |

### 5.4. Thiết kế API CRUD chuẩn REST cho hệ thống Quản lý Đơn hàng (Orders & Items)
```http
# 1. Quản lý Đơn hàng (Orders)
GET    /api/v1/orders                 -> Lấy danh sách đơn hàng (hỗ trợ phân trang ?page=0&size=10)
POST   /api/v1/orders                 -> Tạo đơn hàng mới
GET    /api/v1/orders/{orderId}       -> Xem chi tiết đơn hàng theo ID
PUT    /api/v1/orders/{orderId}       -> Cập nhật toàn bộ đơn hàng
PATCH  /api/v1/orders/{orderId}       -> Cập nhật trạng thái đơn (vd: đổi sang DELIVERED)
DELETE /api/v1/orders/{orderId}       -> Hủy / Xóa đơn hàng

# 2. Quản lý Sản phẩm con bên trong Đơn hàng (Nested Sub-resources)
GET    /api/v1/orders/{orderId}/items           -> Lấy danh sách các món hàng trong đơn
POST   /api/v1/orders/{orderId}/items           -> Thêm 1 món hàng mới vào đơn
DELETE /api/v1/orders/{orderId}/items/{itemId}  -> Xóa món hàng cụ thể khỏi đơn
```

---

<div style="page-break-before: always;"></div>

<a id="phase-3-chapter-04"></a>

# Chapter 04: JSON & Serialization/Deserialization (Jackson)

## 1. JSON Format
```json
{
  "id": 1,
  "name": "Nguyễn Văn An",
  "email": "an@gmail.com",
  "age": 25,
  "active": true,
  "roles": ["USER", "ADMIN"],
  "address": { "city": "HCM", "district": "Q1" }
}
```
- **JSON Object**: `{}` chứa cặp `"key": value`.
- **JSON Array**: `[]` chứa danh sách giá trị.
- Value types: String, Number, Boolean, null, Object, Array.

## 2. Serialization & Deserialization
- **Serialization**: Java Object → JSON String (gửi response).
- **Deserialization**: JSON String → Java Object (nhận request body).
- Spring Boot dùng **Jackson** (tự động) để chuyển đổi.

```java
ObjectMapper mapper = new ObjectMapper();

// Serialize
User user = new User(1L, "An", "an@gmail.com");
String json = mapper.writeValueAsString(user);
// {"id":1,"name":"An","email":"an@gmail.com"}

// Deserialize
User parsed = mapper.readValue(json, User.class);
```

## 3. Jackson Annotations quan trọng
```java
public class UserDto {
    private Long id;

    @JsonProperty("full_name")           // Đổi tên field trong JSON
    private String name;

    @JsonIgnore                           // Ẩn field khỏi JSON
    private String password;

    @JsonFormat(pattern = "dd/MM/yyyy")   // Format ngày
    private LocalDate birthDate;

    @JsonInclude(JsonInclude.Include.NON_NULL)  // Ẩn field nếu null
    private String address;
}
```

| Annotation | Mục đích |
|-----------|---------|
| `@JsonProperty("name")` | Đổi tên field khi serialize/deserialize |
| `@JsonIgnore` | Bỏ qua field (không xuất ra JSON) |
| `@JsonFormat` | Format date/time |
| `@JsonInclude(NON_NULL)` | Không xuất field có giá trị null |
| `@JsonIgnoreProperties(ignoreUnknown=true)` | Bỏ qua field lạ khi deserialize |

## 4. Câu hỏi phỏng vấn & Trả lời chi tiết

### 4.1. Serialization và Deserialization là gì?
- **Serialization (Tuần tự hóa):**
  - Là quá trình chuyển đổi một **Đối tượng Java (Java Object)** trên bộ nhớ Heap thành một chuỗi dữ liệu định dạng văn bản (như **JSON String**) hoặc dòng byte (Byte Stream) để có thể truyền qua mạng Internet hoặc lưu xuống file/database.
  - Trong Spring Boot: Diễn ra tự động khi Controller return một Object $\rightarrow$ Jackson ObjectMapper biến đổi thành JSON gửi về cho Client.
- **Deserialization (Giải tuần tự hóa):**
  - Là quá trình ngược lại: Đọc một chuỗi dữ liệu (như **JSON String** gửi từ Client lên qua Request Body) và phân tích cú pháp (parse) để tái tạo lại thành một **Đối tượng Java (Java Object)** hợp lệ trên Heap.
  - Trong Spring Boot: Diễn ra tự động khi sử dụng annotation `@RequestBody UserDTO dto`.

### 4.2. Khi nào dùng `@JsonIgnore`? Cho ví dụ thực tế (Ẩn Password)
- **Mục đích:** Dùng để đánh dấu một trường dữ liệu (field) mà bạn **tuyệt đối không muốn xuất hiện** trong chuỗi JSON trả về cho Client, hoặc bỏ qua không đọc khi parse JSON.
- **Ví dụ thực tế:**
  ```java
  public class UserResponse {
      private Long id;
      private String username;
      private String email;

      @JsonIgnore
      private String passwordHash; // ❌ Không bao giờ để lộ mật khẩu đã mã hóa ra ngoài API!
  }
  ```
- **Ứng dụng khác:** Dùng để chặn vòng lặp tuần hoàn vô tận (Infinite Recursion) khi 2 Entity trong Hibernate có quan hệ 2 chiều (`@OneToMany` và `@ManyToOne` gọi qua lại lẫn nhau gây tràn bộ nhớ Stack).

### 4.3. `@JsonProperty` dùng để làm gì?
- **Mục đích:** Dùng để tùy biến ánh xạ (mapping) giữa **tên thuộc tính trong Java (theo quy tắc camelCase)** và **tên khóa trong chuỗi JSON (theo quy tắc snake_case hoặc chuẩn bên thứ 3)**.
- **Ví dụ:**
  ```java
  public class OrderDto {
      @JsonProperty("order_id")
      private Long orderId;

      @JsonProperty("customer_full_name")
      private String customerFullName;
  }
  ```
  Khi xuất ra JSON, key sẽ là `"order_id"` và `"customer_full_name"`.
- **Hỗ trợ quyền truy cập (Access control):**
  - `@JsonProperty(access = JsonProperty.Access.WRITE_ONLY)`: Chỉ cho phép nhận vào khi deserialize (tạo mới/cập nhật), nhưng khi serialize trả về response cho client thì tự động giấu đi (rất thích hợp cho trường `password`).

---

<div style="page-break-before: always;"></div>

<a id="phase-3-chapter-05"></a>

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

## 3. Câu hỏi phỏng vấn & Trả lời chi tiết

### 3.1. Bạn dùng công cụ gì để test API? Mô tả quy trình test 1 endpoint thực tế
- **Công cụ thường dùng:** **Postman** (giao diện trực quan, quản lý Collection/Environment, viết script test tự động), **cURL** (test nhanh trên terminal hoặc server Linux), và **Swagger/OpenAPI UI** (tài liệu hóa và test trực tiếp trên trình duyệt).
- **Quy trình chuẩn để test một Endpoint mới (ví dụ: `POST /api/v1/orders`):**
  1. **Kiểm thử trường hợp thành công (Happy Path):**
     - Gửi đúng Header `Authorization: Bearer <valid_token>` và Body JSON hợp lệ.
     - Kỳ vọng: Status Code `201 Created`, body trả về `orderId`, dữ liệu trong Database được lưu chính xác, tồn kho sản phẩm bị trừ tương ứng.
  2. **Kiểm thử xác thực & phân quyền (Auth & Permissions):**
     - Gửi request không có token $\rightarrow$ Phải trả về `401 Unauthorized`.
     - Dùng token của User thường gọi API chỉ dành cho Admin $\rightarrow$ Phải trả về `403 Forbidden`.
  3. **Kiểm thử dữ liệu đầu vào (Validation & Negative Testing):**
     - Bỏ trống các trường bắt buộc, gửi sai định dạng email, số tiền âm, ID không tồn tại.
     - Kỳ vọng: Status Code `400 Bad Request` kèm mảng lỗi chi tiết (`errors: [{field: "...", message: "..."}]`).
  4. **Kiểm thử ngoại lệ & trùng lặp (Edge cases & Idempotency):**
     - Bấm đặt hàng 2 lần liên tiếp thật nhanh $\rightarrow$ Kiểm tra hệ thống có bị duplicate đơn hàng không (chống double-spend).
     - Đặt hàng vượt quá số lượng hàng tồn kho $\rightarrow$ Phải trả về `400` hoặc `409 Conflict`.

### 3.2. Làm sao tự động hoá test API trong Postman? (Postman Tests & Newman CLI)
- **Viết Test Scripts trong tab "Tests" của Postman:**
  Sử dụng cú pháp JavaScript của thư viện Chai Assertion được tích hợp sẵn:
  ```javascript
  // 1. Kiểm tra Status Code
  pm.test("Status code is 201 Created", function () {
      pm.response.to.have.status(201);
  });

  // 2. Kiểm tra thời gian phản hồi (Latency SLA)
  pm.test("Response time is less than 500ms", function () {
      pm.expect(pm.response.responseTime).to.be.below(500);
  });

  // 3. Kiểm tra cấu trúc dữ liệu JSON trả về
  pm.test("Response has orderId and status", function () {
      const res = pm.response.json();
      pm.expect(res.data).to.have.property("orderId");
      pm.expect(res.data.status).to.eql("PENDING");
  });

  // 4. Trích xuất biến dùng cho request kế tiếp (Chaining API)
  const orderId = pm.response.json().data.orderId;
  pm.environment.set("current_order_id", orderId);
  ```
- **Chạy tự động trong CI/CD bằng Newman CLI:**
  - Export Postman Collection và Environment ra file `.json`.
  - Chạy lệnh: `newman run my_collection.json -e my_env.json --reporters cli,junit`
  - Nhúng lệnh này vào GitHub Actions / GitLab CI để tự động test toàn bộ API mỗi khi developer push code mới lên repository.

---

<div style="page-break-before: always;"></div>

<a id="phase-4"></a>

# PHASE 4: SPRING BOOT CORE & KIẾN TRÚC 3 TẦNG

---

<div style="page-break-before: always;"></div>

<a id="phase-4-chapter-01"></a>

# Chapter 01: Spring Core – IoC, Dependency Injection, Bean Lifecycle

## 1. IoC (Inversion of Control)
- Thay vì class **tự tạo** dependency (`new Service()`), Spring **quản lý và tiêm** (inject) dependency vào.
- **IoC Container** = `ApplicationContext`: quản lý vòng đời tất cả Bean.

## 2. Dependency Injection (DI) – 3 cách

### Constructor Injection ✅ (Khuyên dùng)
```java
@Service
public class UserService {
    private final UserRepository userRepository;  // final = immutable

    public UserService(UserRepository userRepository) {  // Spring tự inject
        this.userRepository = userRepository;
    }
}
// Với Lombok: @RequiredArgsConstructor thay constructor
```

### Field Injection ❌ (Không khuyên dùng)
```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;  // Khó viết unit test
}
```

### Setter Injection (Ít dùng)
```java
@Autowired
public void setUserRepository(UserRepository repo) { this.userRepository = repo; }
```

> **Tại sao Constructor Injection tốt nhất?** Hỗ trợ `final` (immutable), dễ viết Unit Test (truyền mock qua constructor), phát hiện circular dependency sớm.

## 3. Stereotype Annotations
| Annotation | Dùng cho | Ý nghĩa |
|-----------|---------|---------|
| `@Component` | Class bất kỳ | Đánh dấu là Bean |
| `@Service` | Business Logic | Tầng Service |
| `@Repository` | Data Access | Tầng Repository (tự dịch DB exception) |
| `@Controller` | MVC Controller | Trả view (HTML) |
| `@RestController` | REST API | = `@Controller` + `@ResponseBody` |
| `@Configuration` | Cấu hình | Khai báo `@Bean` methods |

## 4. @Bean vs @Component
```java
// @Component: Đánh dấu class của MÌNH
@Component
public class EmailService { }

// @Bean: Khai báo Bean từ THƯ VIỆN BÊN NGOÀI (không sửa được source code)
@Configuration
public class AppConfig {
    @Bean
    public ObjectMapper objectMapper() {
        return new ObjectMapper().registerModule(new JavaTimeModule());
    }
}
```

## 5. @Qualifier & @Primary
```java
// Khi có 2 Bean cùng kiểu → xung đột
@Service("vnpay")
public class VnPayService implements PaymentService { }

@Service("momo")
public class MomoService implements PaymentService { }

// Giải quyết bằng @Qualifier
@Service
public class OrderService {
    public OrderService(@Qualifier("vnpay") PaymentService payment) { }
}

// Hoặc @Primary: Bean mặc định
@Primary @Service
public class VnPayService implements PaymentService { }
```

## 6. Bean Scope
| Scope | Mô tả |
|-------|-------|
| `singleton` (mặc định) | 1 instance duy nhất trong toàn bộ Application Context |
| `prototype` | Tạo instance mới mỗi lần inject/getBean |
| `request` | 1 instance mỗi HTTP request (Web) |
| `session` | 1 instance mỗi HTTP session (Web) |

## 7. Bean Lifecycle
```
Constructor → @PostConstruct → Sử dụng → @PreDestroy → Huỷ
```

## 8. Câu hỏi phỏng vấn & Trả lời chi tiết

### 8.1. IoC và DI là gì? Chúng liên quan mật thiết với nhau như thế nào?
- **Inversion of Control (IoC - Đảo ngược điều khiển):**
  - Là một **nguyên lý thiết kế kiến trúc (Design Principle)**.
  - *Truyền thống:* Lập trình viên tự chủ động quản lý vòng đời và tự tay `new ClassB()` bên trong `ClassA`.
  - *IoC:* Quyền kiểm soát việc khởi tạo, cấu hình và quản lý vòng đời của các đối tượng được "chuyển giao" (inversion) cho một bên thứ ba quản lý — đó chính là **Spring IoC Container**.
- **Dependency Injection (DI - Tiêm phụ thuộc):**
  - Là **mẫu thiết kế (Design Pattern) cụ thể** dùng để **hiện thực hóa nguyên lý IoC**.
  - Thay vì class tự đi tìm hoặc tạo ra phụ thuộc, Spring Container sẽ chủ động "tiêm" (inject) phụ thuộc đó vào class thông qua Constructor, Setter hoặc Field.
- $\rightarrow$ **Mối quan hệ:** IoC là tư tưởng/mục tiêu, còn DI là công cụ/hành động cụ thể để đạt được mục tiêu đó.

### 8.2. Tại sao Spring khuyên dùng Constructor Injection thay vì Field Injection (`@Autowired`)?
Field Injection (`@Autowired private UserService userService;`) tuy viết ngắn hơn nhưng bị coi là **Code Smell (Anti-pattern)** vì 4 lý do:
1. **Bất biến (Immutability):** Constructor Injection cho phép khai báo thuộc tính là `private final`, đảm bảo dependency không bao giờ bị thay đổi hay mang giá trị `null` sau khi khởi tạo.
2. **Dễ viết Unit Test:** Với Constructor Injection, ta có thể dễ dàng khởi tạo class và truyền Mock Object vào bằng tay (`new OrderService(mockRepo)`) mà không cần phải dùng Reflection hoặc khởi động cả Spring Context nặng nề.
3. **Phát hiện Circular Dependency (Phụ thuộc vòng):** Nếu Bean A cần Bean B và Bean B lại cần Bean A, Constructor Injection sẽ khiến Spring báo lỗi ngay lập tức lúc khởi động app, ép developer phải sửa thiết kế code thay vì để lỗi âm thầm lúc runtime.
4. **Ngăn chặn vi phạm SRP:** Nếu 1 class có constructor nhận tới 8-10 tham số, bạn sẽ lập tức nhận ra class này đang ôm đồm quá nhiều việc (vi phạm Single Responsibility Principle) để refactor sớm.

### 8.3. `@Component` vs `@Bean` khác nhau thế nào?
| Tiêu chí | `@Component` (kèm `@Service`, `@Repository`, `@Controller`) | `@Bean` |
| :--- | :--- | :--- |
| **Vị trí áp dụng** | Đặt trên **Class level** (đầu file class). | Đặt trên **Method level** bên trong class cấu hình `@Configuration`. |
| **Cơ chế phát hiện** | Spring tự động phát hiện thông qua tính năng **Component Scanning** (`@ComponentScan`). | Lập trình viên chủ động viết phương thức trả về instance và đánh dấu `@Bean`. |
| **Quyền sở hữu mã nguồn** | Dùng cho **code do chính bạn viết trong dự án** (có quyền mở file thêm annotation). | **Bắt buộc dùng khi tích hợp thư viện bên thứ 3** (ví dụ: cấu hình `RestTemplate`, `ModelMapper`, `BCryptPasswordEncoder` - những class trong file `.jar` có sẵn mà bạn không thể sửa code để thêm `@Component`). |
| **Tùy biến khởi tạo** | Khởi tạo tự động mặc định. | Cực kỳ linh hoạt: Bạn có thể viết logic điều kiện (`if-else`), đọc biến môi trường để tùy biến cách khởi tạo object. |

### 8.4. Bean Scope mặc định là gì? Singleton Scope có vấn đề gì trong Multi-threading?
- **Bean Scope mặc định trong Spring:** Là **`Singleton`** (Toàn bộ Spring IoC Container chỉ tạo và quản lý duy nhất **1 instance** của Bean đó trong suốt vòng đời ứng dụng).
- **Vấn đề tiềm ẩn trong môi trường Đa luồng (Multi-threading):**
  - Mặc định mỗi HTTP request từ người dùng gửi tới Tomcat sẽ được phục vụ bởi một **Thread riêng biệt**.
  - Cả 100 thread này sẽ **cùng lúc gọi vào phương thức của DUY NHẤT 1 instance Singleton Bean** (Controller hoặc Service).
  - **NGUY HIỂM:** Nếu bạn khai báo **Biến trạng thái có thể thay đổi (Mutable State / Instance Variable)** bên trong Bean:
    ```java
    @Service
    public class OrderService {
        private Long currentUserId; // ❌ CHẾT NGƯỜI: Nhiều thread cùng ghi đè biến này!
    }
    ```
    Luồng của User A sẽ đọc nhầm `currentUserId` của User B $\rightarrow$ Lộ dữ liệu chéo (Race Condition / Thread-safety bug).
- **Quy tắc vàng:** Các Bean Spring (Service, Controller, Repository) **bắt buộc phải là STATELESS** (không chứa biến instance lưu trạng thái người dùng; mọi dữ liệu phải truyền qua tham số hàm cục bộ nằm trên Stack của từng Thread).

---

<div style="page-break-before: always;"></div>

<a id="phase-4-chapter-02"></a>

# Chapter 02: Spring Boot Overview – Auto-configuration, Starters, Config Properties

## 1. Spring Boot là gì?
- Framework giúp **khởi tạo nhanh** ứng dụng Spring mà không cần cấu hình XML phức tạp.
- Tích hợp sẵn **embedded server** (Tomcat), **auto-configuration**, **starter dependencies**.

## 2. Spring Boot Starters
| Starter | Mô tả |
|---------|-------|
| `spring-boot-starter-web` | REST API, Spring MVC, Tomcat |
| `spring-boot-starter-data-jpa` | JPA/Hibernate, Spring Data |
| `spring-boot-starter-security` | Spring Security |
| `spring-boot-starter-validation` | Bean Validation (Jakarta) |
| `spring-boot-starter-test` | JUnit 5, Mockito, MockMvc |

## 3. Auto-Configuration
- Spring Boot tự động cấu hình dựa trên **dependency có trong classpath**.
- Thêm `spring-boot-starter-data-jpa` + driver MySQL → tự cấu hình `DataSource`, `EntityManager`.
- Annotation `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.

## 4. File cấu hình

### application.properties
```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=123456
spring.jpa.hibernate.ddl-auto=update
```

### application.yml (khuyên dùng – dễ đọc hơn)
```yaml
server:
  port: 8081
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: 123456
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

## 5. Đọc cấu hình trong code

### @Value
```java
@Value("${server.port}")
private int port;

@Value("${app.jwt.secret-key}")
private String secretKey;
```

### @ConfigurationProperties (type-safe, khuyên dùng)
```java
@Configuration
@ConfigurationProperties(prefix = "app.jwt")
@Data  // Lombok
public class JwtProperties {
    private String secretKey;
    private long expiration;    // app.jwt.expiration
    private long refreshExpiration;
}
```

## 6. Profiles (Dev/Prod)
```yaml
# application-dev.yml
server:
  port: 8080
spring:
  jpa:
    show-sql: true

# application-prod.yml
server:
  port: 80
spring:
  jpa:
    show-sql: false
```
Chạy: `java -jar app.jar --spring.profiles.active=prod`

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. Auto-configuration trong Spring Boot hoạt động như thế nào?
- **Bản chất:** Spring Boot tự động đoán xem ứng dụng của bạn cần những cấu hình nào dựa trên **các thư viện `.jar` có mặt trong classpath** và các Bean bạn đã tự định nghĩa.
- **Cơ chế hoạt động bên dưới:**
  1. File trung tâm: `@SpringBootApplication` bọc `@EnableAutoConfiguration`.
  2. Spring Boot đọc file cấu hình `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`.
  3. Sử dụng hàng loạt các annotation điều kiện **`@ConditionalOn...`**:
     - `@ConditionalOnClass(DataSource.class)`: Chỉ tự động cấu hình kết nối DB nếu tìm thấy driver trong classpath (ví dụ `mysql-connector-j`).
     - `@ConditionalOnMissingBean(DataSource.class)`: **Chỉ tự động tạo Bean mặc định nếu Developer CHƯA TỰ VIẾT bean đó**. Nếu bạn tự viết `@Bean DataSource`, Spring Boot sẽ nhường quyền ưu tiên cho bạn (Opinionated Defaults).
     - `@ConditionalOnProperty`: Bật/tắt cấu hình dựa vào cờ trong file `application.yml`.

### 7.2. So sánh `@Value` vs `@ConfigurationProperties`
| Tiêu chí | `@Value("${app.jwt.secret}")` | `@ConfigurationProperties(prefix = "app.jwt")` |
| :--- | :--- | :--- |
| **Cách tiếp cận** | Rời rạc, tiêm trực tiếp từng biến đơn lẻ. | **Gom cụm có cấu trúc thành một Class Java (Type-safe POJO)**. |
| **Kiểm tra kiểu (Type-Safety)** | Kém (dễ gõ sai chính tả chuỗi String key, lỗi chỉ ném ra lúc chạy). | **Rất cao**: Hỗ trợ validation (`@NotBlank`, `@Min`), tự động ép kiểu sang `Duration`, `DataSize`, `List`, `Map`. |
| **Relaxed Binding** | Rất hạn chế: Tên key phải khớp chính xác. | **Rất mạnh**: Tự động khớp `secret-key`, `secret_key`, `SECRET_KEY` vào trường `secretKey`. |
| **Khuyên dùng** | Chỉ dùng cho các biến đơn giản, lẻ tẻ (1-2 biến). | **Chuẩn Production**: Dùng cho mọi nhóm cấu hình phức tạp (JWT, AWS S3, Payment Gateway, Mail Server). |

### 7.3. Spring Boot Profile dùng để làm gì? Cách chuyển đổi trong thực tế?
- **Mục đích:** Tách biệt môi trường chạy của ứng dụng, cho phép cùng một bộ mã nguồn có thể chạy với các cấu hình cơ sở dữ liệu, cổng mạng và chế độ debug khác nhau trên từng môi trường:
  - `dev` (Development - Máy cá nhân lập trình viên): Cổng 8080, bật `show-sql: true`, dùng DB H2 hoặc MySQL local, level log `DEBUG`.
  - `test` / `staging` (Môi trường kiểm thử): Dùng DB giả lập trên Docker, kết nối Sandbox của bên thứ 3.
  - `prod` (Production - Thực tế phục vụ khách hàng): Tắt `show-sql`, dùng MySQL Cluster có bảo mật cao, pool kết nối HikariCP tối đa, level log `WARN/ERROR`.
- **Cách kích hoạt Profile trong thực tế:**
  1. Trong file cấu hình: `spring.profiles.active=prod`
  2. Bằng biến môi trường (Environment Variable trên Docker/K8s): `SPRING_PROFILES_ACTIVE=prod`
  3. Bằng tham số dòng lệnh khi chạy file Jar: `java -jar app.jar --spring.profiles.active=prod`

---

<div style="page-break-before: always;"></div>

<a id="phase-4-chapter-03"></a>

# Chapter 03: Kiến trúc 3 tầng Spring MVC – Controller, Service, Repository

## 1. Kiến trúc 3 tầng
```
┌──────────────────┐
│ Client / Browser │
└────────┬─────────┘
         │ ▲
  HTTP   │ │ HTTP
 Request │ │ Response
         ▼ │
┌──────────────────┐
│ @RestController  │ ──► Nhận HTTP Request, validate dữ liệu (DTO), điều hướng
└────────┬─────────┘
         │ ▲
    Gọi  │ │ Trả DTO/
  Service│ │ Domain model
         ▼ │
┌──────────────────┐
│     @Service     │ ──► Xử lý Business Logic, tính toán, phân quyền, Transaction
└────────┬─────────┘
         │ ▲
    Gọi  │ │ Trả
    Repo │ │ Entity
         ▼ │
┌──────────────────┐
│   @Repository    │ ──► Tương tác CSDL (Spring Data JPA / Hibernate / JDBC)
└────────┬─────────┘
         │ ▲
   Query │ │ Result
  SQL/JPA│ │ Set
         ▼ │
┌──────────────────┐
│     Database     │ ──► Lưu trữ dữ liệu bền vững (MySQL, PostgreSQL...)
└──────────────────┘
```

| Tầng | Annotation | Nhiệm vụ |
|------|-----------|---------|
| **Controller** | `@RestController` | Nhận request, validate input, trả response |
| **Service** | `@Service` | Business logic, transaction |
| **Repository** | `@Repository` | Truy cập database |

## 2. @RestController
```java
@RestController
@RequestMapping("/api/v1/users")
public class UserController {
    private final UserService userService;
    public UserController(UserService userService) { this.userService = userService; }

    @GetMapping
    public ResponseEntity<List<UserResponse>> getAllUsers() {
        return ResponseEntity.ok(userService.getAllUsers());
    }

    @GetMapping("/{id}")
    public ResponseEntity<UserResponse> getUserById(@PathVariable Long id) {
        return ResponseEntity.ok(userService.getUserById(id));
    }

    @PostMapping
    public ResponseEntity<UserResponse> createUser(@Valid @RequestBody UserRequest request) {
        return ResponseEntity.status(HttpStatus.CREATED).body(userService.createUser(request));
    }

    @PutMapping("/{id}")
    public ResponseEntity<UserResponse> updateUser(@PathVariable Long id, @Valid @RequestBody UserRequest request) {
        return ResponseEntity.ok(userService.updateUser(id, request));
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
        return ResponseEntity.noContent().build();
    }
}
```

## 3. Nhận dữ liệu đầu vào
| Annotation | Nguồn | Ví dụ |
|-----------|-------|-------|
| `@PathVariable` | URL path `/users/{id}` | `@PathVariable Long id` |
| `@RequestParam` | Query string `?name=An` | `@RequestParam(required = false) String name` |
| `@RequestBody` | JSON body (POST/PUT) | `@RequestBody UserRequest request` |
| `@RequestHeader` | HTTP header | `@RequestHeader("Authorization") String token` |

## 4. ResponseEntity\<T\>
```java
// Tuỳ biến status code, headers, body
return ResponseEntity.ok(data);                           // 200
return ResponseEntity.status(HttpStatus.CREATED).body(d); // 201
return ResponseEntity.noContent().build();                // 204
return ResponseEntity.notFound().build();                 // 404
return ResponseEntity.badRequest().body(errors);          // 400
```

## 5. Tổ chức Package chuẩn
```
com.example.app/
├── controller/         UserController.java
├── service/            UserService.java (interface)
│   └── impl/           UserServiceImpl.java
├── repository/         UserRepository.java
├── model/entity/       UserEntity.java
├── model/dto/          UserRequest.java, UserResponse.java
├── exception/          ResourceNotFoundException.java, GlobalExceptionHandler.java
└── config/             AppConfig.java
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. Tại sao cần tách 3 tầng Controller - Service - Repository?
Việc phân tầng tuân thủ nguyên lý thiết kế **Separation of Concerns (Phân tách mối quan tâm)** và **Single Responsibility Principle (SRP)**:
1. **Controller (Tầng Giao tiếp HTTP):** Chỉ quan tâm tới việc đón nhận request, bóc tách headers/path/query, validate định dạng sơ bộ, và định dạng lại HTTP Status Code gửi về. Controller **hoàn toàn không được chứa logic tính toán nghiệp vụ hay câu lệnh SQL**.
2. **Service (Tầng Nghiệp vụ cốt lõi - Core Business):** Chứa toàn bộ các quy tắc, công thức tính toán, kiểm tra quyền nâng cao, gọi các API bên thứ 3 và quản lý **Giao dịch cơ sở dữ liệu (`@Transactional`)**.
3. **Repository (Tầng Truy cập Dữ liệu - Data Access):** Chỉ quan tâm tới việc giao tiếp với Database (CRUD, câu lệnh SQL/JPA, tối ưu câu query).
- **Lợi ích to lớn:**
  - **Dễ bảo trì & Mở rộng:** Nếu sau này bạn muốn đổi Database từ MySQL sang MongoDB, bạn chỉ cần viết lại Repository mà Service và Controller vẫn giữ nguyên vẹn 100%. Nếu muốn thêm cổng giao tiếp gRPC hay CLI, bạn chỉ cần tạo thêm Controller mới và tái sử dụng lại Service cũ.
  - **Dễ viết Unit Test:** Dễ dàng kiểm thử Service bằng cách Mock Repository mà không cần bật Web Server.

### 6.2. `@PathVariable` vs `@RequestParam` khi nào dùng cái nào?
- **`@PathVariable` (Tham số đường dẫn):**
  - Trích xuất dữ liệu từ mẫu URL: `/api/v1/users/{id}` $\rightarrow$ `@PathVariable Long id`.
  - **Khi nào dùng:** Khi tham số đó là **thông tin định danh duy nhất và bắt buộc** để xác định tài nguyên cụ thể (User ID, Order ID).
- **`@RequestParam` (Tham số truy vấn Query String):**
  - Trích xuất dữ liệu sau dấu `?`: `/api/v1/users?page=1&size=10&role=ADMIN` $\rightarrow$ `@RequestParam(defaultValue = "0") int page`.
  - **Khi nào dùng:** Khi tham số mang tính **tùy chọn (Optional)**, dùng cho việc **lọc (Filtering), tìm kiếm (Searching), sắp xếp (Sorting), hoặc phân trang (Paging)**. Có thể thiết lập giá trị mặc định bằng `defaultValue = "..."`.

### 6.3. `ResponseEntity<T>` có lợi ích gì so với việc trả trực tiếp Object?
Khi viết `@GetMapping("/users/{id}")`:
- **Nếu trả trực tiếp Object:** `public UserResponse getUser(...)`
  - Bạn **bị trói buộc vào mã HTTP 200 OK**.
  - Không thể chủ động tùy biến HTTP Status Code (ví dụ: trả về `201 Created` khi tạo mới, `204 No Content` khi xóa, `404 Not Found` khi không tìm thấy).
  - Không thể tự thêm các HTTP Headers đặc thù (như `Location`, `Cache-Control`, `Set-Cookie`).
- **Khi dùng `ResponseEntity<T>`:**
  - Là một đối tượng bọc toàn diện đại diện cho toàn bộ HTTP Response của Spring:
    ```java
    return ResponseEntity.status(HttpStatus.CREATED)
            .header("Custom-Header", "Value")
            .body(savedUserDto);
    ```
  - Cung cấp cú pháp Fluent API cực kỳ linh hoạt (`ResponseEntity.ok()`, `ResponseEntity.noContent()`, `ResponseEntity.notFound()`).
  - Giúp API tuân thủ 100% chuẩn thiết kế RESTful chuyên nghiệp.

---

<div style="page-break-before: always;"></div>

<a id="phase-4-chapter-04"></a>

# Chapter 04: DTO Pattern & Bean Validation

## 1. DTO (Data Transfer Object)
- **Không** trả Entity/Database Model trực tiếp cho client (lộ cấu trúc DB, password, metadata).
- Tạo **DTO riêng** cho request (input) và response (output).

```java
// Request DTO (nhận dữ liệu từ client)
public class UserRequest {
    @NotBlank(message = "Tên không được để trống")
    @Size(min = 2, max = 50, message = "Tên từ 2-50 ký tự")
    private String name;

    @NotBlank @Email(message = "Email không hợp lệ")
    private String email;

    @NotBlank @Size(min = 6, message = "Mật khẩu ít nhất 6 ký tự")
    private String password;

    @Min(value = 1, message = "Tuổi phải ≥ 1")
    @Max(value = 150, message = "Tuổi phải ≤ 150")
    private int age;
}

// Response DTO (trả về cho client – KHÔNG có password)
public class UserResponse {
    private Long id;
    private String name;
    private String email;
    private int age;
    private LocalDateTime createdAt;
}
```

## 2. Ánh xạ Entity ↔ DTO
```java
// Thủ công (đơn giản, dễ hiểu)
public static UserResponse toResponse(UserEntity entity) {
    UserResponse dto = new UserResponse();
    dto.setId(entity.getId());
    dto.setName(entity.getName());
    dto.setEmail(entity.getEmail());
    dto.setAge(entity.getAge());
    dto.setCreatedAt(entity.getCreatedAt());
    return dto;
}

// Hoặc dùng thư viện: MapStruct, ModelMapper
```

## 3. Validation Annotations
| Annotation | Mô tả |
|-----------|-------|
| `@NotNull` | Không được null |
| `@NotEmpty` | Không null và không rỗng (`""`) |
| `@NotBlank` | Không null, không rỗng, không chỉ có khoảng trắng |
| `@Size(min, max)` | Giới hạn độ dài String/Collection |
| `@Min(value)` / `@Max(value)` | Giới hạn giá trị số |
| `@Email` | Phải đúng định dạng email |
| `@Pattern(regexp)` | Khớp regex |
| `@Positive` / `@PositiveOrZero` | Số dương / không âm |

## 4. Kích hoạt Validation
```java
@PostMapping
public ResponseEntity<UserResponse> createUser(@Valid @RequestBody UserRequest request) {
    // Nếu validation fail → Spring tự quăng MethodArgumentNotValidException
    return ResponseEntity.status(HttpStatus.CREATED).body(userService.createUser(request));
}
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Tại sao BẮT BUỘC phải dùng DTO thay vì trả trực tiếp Entity ra ngoài API?
Trả trực tiếp Entity (`@Entity User`) ra Controller là một cạm bẫy cực kỳ nguy hiểm trong Backend:
1. **Lỗ hổng bảo mật rò rỉ dữ liệu (Over-fetching & Security):** Entity chứa các cột nhạy cảm như `password_hash`, `salt`, `internal_notes`, `failed_login_attempts`. Nếu không có DTO, toàn bộ các trường này sẽ bị serialize thành JSON gửi về trình duyệt của người dùng!
2. **Lỗ hổng gán hàng loạt (Mass Assignment Vulnerability):** Khi nhận dữ liệu tạo mới/cập nhật, nếu hứng trực tiếp bằng Entity, kẻ xấu có thể gửi kèm JSON `{"role": "ADMIN", "balance": 999999}`. Nếu lười biễn lưu thẳng Entity, kẻ xấu sẽ tự nâng quyền của mình thành Admin. DTO hoạt động như một bộ lọc (Whitelist) chỉ cho phép những trường hợp lệ đi vào.
3. **Tránh lỗi tuần hoàn vô hạn (Circular Reference & LazyInitializationException):** Trong Hibernate, Entity `User` có thể chứa `List<Order>`, và `Order` lại chứa ngược lại `User`. Khi Jackson parse JSON sẽ văng lỗi `StackOverflowError` hoặc lỗi `LazyInitializationException` khi Session DB đã đóng.
4. **Tách biệt Database Schema và API Contract:** Bạn có thể tự do sửa đổi tên bảng, tách cột trong Database mà không sợ làm thay đổi cấu trúc JSON trả về cho Frontend (API Contract luôn ổn định).

### 5.2. `@NotNull` vs `@NotEmpty` vs `@NotBlank` khác nhau thế nào?
| Tiêu chí | `@NotNull` | `@NotEmpty` | `@NotBlank` (Khuyên dùng cho String) |
| :--- | :--- | :--- | :--- |
| **Áp dụng cho** | Mọi kiểu dữ liệu (Object, Number, Date, String). | `CharSequence`, `Collection`, `Map`, `Array`. | **Chỉ áp dụng cho chuỗi ký tự (`String`, `CharSequence`)**. |
| **`null`** | ❌ Báo lỗi | ❌ Báo lỗi | ❌ Báo lỗi |
| **`""` (Chuỗi rỗng độ dài 0)** | ✅ Hợp lệ (Cho qua) | ❌ Báo lỗi | ❌ Báo lỗi |
| **`"   "` (Chuỗi chỉ toàn dấu cách)**| ✅ Hợp lệ (Cho qua) | ✅ Hợp lệ (Cho qua vì length > 0) | ❌ **Báo lỗi** (Tự động `.trim()` trước khi kiểm tra) |
| **Thực tế:** Với các trường như `name`, `email`, `password`, **LUÔN DÙNG `@NotBlank`** để chặn người dùng nhập khoảng trắng vô nghĩa.

### 5.3. `@Valid` đặt ở đâu để kích hoạt Validation trong Spring Boot?
1. **Trên tham số Request Body của Controller:**
   ```java
   @PostMapping("/users")
   public ResponseEntity<?> create(@Valid @RequestBody UserCreateRequest request)
   ```
   Nếu dữ liệu vi phạm annotation (như `@NotBlank`, `@Min`), Spring sẽ chặn request lại và ném ra ngoại lệ `MethodArgumentNotValidException`.
2. **Trước các Object lồng nhau bên trong DTO (Nested Validation):**
   Nếu DTO chứa một đối tượng con hoặc danh sách con:
   ```java
   public class OrderRequest {
       @Valid // 👈 BẮT BUỘC phải có @Valid ở đây thì Spring mới duyệt sâu vào trong để kiểm tra các trường của OrderItemRequest!
       @NotEmpty
       private List<OrderItemRequest> items;
   }
   ```
3. **Trên Controller Class level (`@Validated`) khi validate PathVariable hoặc RequestParam:**
   ```java
   @RestController
   @Validated // 👈 Cần đặt trên Class
   public class UserController {
       @GetMapping("/{id}")
       public UserResponse getById(@PathVariable @Min(1) Long id) // Ném ConstraintViolationException nếu id < 1
   }
   ```

---

<div style="page-break-before: always;"></div>

<a id="phase-4-chapter-05"></a>

# Chapter 05: Global Exception Handling – @RestControllerAdvice

## 1. Vấn đề
- Không bắt exception → client nhận **500 Internal Server Error** với stack trace lộ thông tin nội bộ.
- Bắt trong từng controller → **code trùng lặp**, khó bảo trì.

## 2. Giải pháp: @RestControllerAdvice
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    // Bắt ResourceNotFoundException → 404
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex, WebRequest request) {
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.NOT_FOUND.value())
            .message(ex.getMessage())
            .path(request.getDescription(false))
            .build();
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }

    // Bắt Validation Error → 400
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException ex) {
        List<String> errors = ex.getBindingResult().getFieldErrors().stream()
            .map(err -> err.getField() + ": " + err.getDefaultMessage())
            .toList();
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.BAD_REQUEST.value())
            .message("Validation failed")
            .errors(errors)
            .build();
        return ResponseEntity.badRequest().body(error);
    }

    // Bắt mọi Exception khác → 500
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception ex) {
        ErrorResponse error = ErrorResponse.builder()
            .timestamp(LocalDateTime.now())
            .status(HttpStatus.INTERNAL_SERVER_ERROR.value())
            .message("Đã xảy ra lỗi hệ thống")
            .build();
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
    }
}
```

## 3. ErrorResponse class
```java
@Data @Builder @AllArgsConstructor @NoArgsConstructor
public class ErrorResponse {
    private LocalDateTime timestamp;
    private int status;
    private String message;
    private String path;
    private List<String> errors;
}
```

## 4. Custom Exception
```java
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String resource, Long id) {
        super(resource + " không tìm thấy với ID: " + id);
    }
}

public class DuplicateResourceException extends RuntimeException {
    public DuplicateResourceException(String message) { super(message); }
}
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. `@RestControllerAdvice` hoạt động như thế nào trong kiến trúc Spring MVC?
- **Bản chất:** `@RestControllerAdvice` là sự kết hợp của hai annotation:
  $$\text{@ControllerAdvice} + \text{@ResponseBody}$$
- **Nguyên lý hoạt động bên dưới (AOP - Aspect-Oriented Programming):**
  - `@ControllerAdvice` áp dụng kỹ thuật **Interception (Đánh chặn xung quanh)** trên toàn bộ các `@RestController` trong ứng dụng.
  - Khi bất kỳ phương thức nào trong bất kỳ Controller nào ném ra một Exception chưa được bắt (Uncaught Exception):
    1. Exception sẽ nổi lên và được Spring DispatcherServlet đón lấy.
    2. Spring quét tìm class có gắn `@RestControllerAdvice`.
    3. Tìm xem trong class đó có hàm nào gắn `@ExceptionHandler(Tên_Exception.class)` khớp với ngoại lệ vừa xảy ra không.
    4. Kích hoạt hàm đó để định dạng đối tượng lỗi (Error Response Object).
    5. Tự động serialize object đó thành JSON gửi về cho Client kèm mã HTTP Status tương ứng.

### 5.2. Tại sao BẮT BUỘC cần Global Exception Handler thay vì viết `try-catch` trong từng Controller?
1. **Loại bỏ trùng lặp mã nguồn (DRY - Don't Repeat Yourself):** Nếu không có Global Handler, bạn sẽ phải viết hàng trăm khối `try { ... } catch (Exception e)` giống hệt nhau ở khắp mọi Controller trong dự án.
2. **Chuẩn hóa cấu trúc lỗi trả về (Consistent Error Response):** Đảm bảo 100% các API trong hệ thống (dù lỗi 400, 404, hay 500) đều trả về một cấu trúc JSON đồng nhất duy nhất:
   ```json
   {
     "status": 404,
     "message": "User không tìm thấy với ID: 10",
     "timestamp": "2026-09-17T12:00:00"
   }
   ```
   Giúp đội ngũ Frontend (React/Mobile) chỉ cần viết 1 hàm xử lý lỗi chung duy nhất để hiển thị thông báo Toast/Popup cho người dùng.
3. **Bảo mật hệ thống (Prevent Information Leakage):** Ngăn chặn hoàn toàn việc server tự động văng ra màn hình trắng lỗi kỹ thuật (Whitelabel Error Page) hoặc phơi bày toàn bộ mã nguồn `stack trace` ra ngoài Internet cho hacker soi thấy.

### 5.3. Cách bắt lỗi Validation (`@Valid`) và trả về định dạng đẹp, chi tiết từng trường cho Client
Khi tham số `@Valid` bị vi phạm, Spring sẽ ném ra `MethodArgumentNotValidException`. Ta bắt ngoại lệ này trong Global Handler như sau:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, Object>> handleValidationErrors(MethodArgumentNotValidException ex) {
        // Gom toàn bộ các lỗi theo từng field vào Map
        Map<String, String> fieldErrors = new HashMap<>();
        for (FieldError error : ex.getBindingResult().getFieldErrors()) {
            fieldErrors.put(error.getField(), error.getDefaultMessage());
        }

        Map<String, Object> response = new HashMap<>();
        response.put("status", HttpStatus.BAD_REQUEST.value());
        response.put("message", "Dữ liệu đầu vào không hợp lệ");
        response.put("errors", fieldErrors); // {"email": "Sai định dạng", "age": "Phải >= 18"}
        response.put("timestamp", LocalDateTime.now());

        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(response);
    }
}
```

---

<div style="page-break-before: always;"></div>

<a id="phase-5"></a>

# PHASE 5: DATABASE, JPA & HIBERNATE ORM

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-01"></a>

# Chapter 01: RDBMS & SQL – Primary Key, Foreign Key, Indexing

## 1. Cơ sở dữ liệu quan hệ (RDBMS)
- Dữ liệu tổ chức thành **bảng** (table), mỗi bảng có **hàng** (row) và **cột** (column).
- Chuẩn hoá (Normalization): 1NF (không lặp), 2NF (phụ thuộc toàn phần PK), 3NF (không phụ thuộc bắc cầu).

## 2. Primary Key & Foreign Key
- **PK**: Định danh duy nhất 1 hàng. Thường dùng `id BIGINT AUTO_INCREMENT`.
- **FK**: Tham chiếu PK của bảng khác, tạo quan hệ giữa 2 bảng.

```sql
CREATE TABLE categories (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);
CREATE TABLE products (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(200) NOT NULL,
    price DECIMAL(10,2),
    category_id BIGINT,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

## 3. Index (Chỉ mục)
- **B-Tree Index**: Tăng tốc `SELECT WHERE`, `ORDER BY`. Đánh đổi: chậm `INSERT/UPDATE`.
- **Clustered Index**: PK mặc định, dữ liệu sắp xếp vật lý theo index.
- **Non-clustered Index**: Index phụ, trỏ tới vị trí dữ liệu.

```sql
CREATE INDEX idx_product_name ON products(name);
CREATE UNIQUE INDEX idx_user_email ON users(email);
```

> 💡 **Quy tắc:** Index các cột thường xuyên `WHERE`, `JOIN`, `ORDER BY`. Không index cột ít giá trị distinct (boolean).

## 4. Câu hỏi phỏng vấn & Trả lời chi tiết

### 4.1. Clustered Index vs Non-clustered Index khác nhau thế nào?
| Tiêu chí | Clustered Index (Chỉ mục cụm) | Non-clustered Index (Chỉ mục thứ cấp) |
| :--- | :--- | :--- |
| **Bản chất vật lý** | **Sắp xếp thứ tự vật lý thực tế của các dòng dữ liệu** trên đĩa cứng theo giá trị của Index. | Tạo một cấu trúc B-Tree riêng biệt lưu bản sao cột index + con trỏ (Row Pointer / PK) trỏ tới dòng dữ liệu thật. |
| **Số lượng trên 1 bảng** | **Chỉ DUY NHẤT 1 Clustered Index** trên mỗi bảng (mặc định chính là `PRIMARY KEY`). | Có thể tạo **nhiều** Non-clustered Index trên cùng 1 bảng (thường từ 3 - 5 index). |
| **Dung lượng lưu trữ** | Không tốn thêm dung lượng vì chính là bảng dữ liệu. | Tốn thêm dung lượng ổ cứng để lưu cây B-Tree phụ. |
| **Tốc độ truy vấn** | Siêu nhanh khi tìm kiếm theo khoảng (`BETWEEN`, `>`, `<`). | Nhanh với tìm kiếm chính xác, nhưng nếu query các cột không nằm trong index thì phải tốn thêm bước "Bookmark Lookup" để đọc dữ liệu từ Clustered Index. |

### 4.2. Khi nào KHÔNG NÊN tạo Index? (Cạm bẫy của việc lạm dụng Index)
Tạo Index không phải là "viên đạn bạc" (Silver Bullet), bạn không nên tạo index trong các trường hợp sau:
1. **Bảng có tần suất GHI (`INSERT`, `UPDATE`, `DELETE`) cực kỳ cao:** Mỗi khi có 1 dòng mới thêm vào, Database vừa phải ghi dữ liệu thật, vừa phải cân bằng lại toàn bộ các cây B-Tree Index, làm thao tác ghi bị chậm đi rõ rệt.
2. **Bảng có dung lượng quá nhỏ (dưới vài trăm dòng):** Database thực hiện quét toàn bộ bảng (**Full Table Scan**) còn nhanh hơn việc phải đọc cây Index rồi nhảy sang đọc dữ liệu thật.
3. **Cột có độ biến thiên thấp (Low Cardinality):** Ví dụ cột `gender` (Nam/Nữ), `status` (Active/Inactive), `is_deleted` (true/false). Index trên các cột này hầu như không giúp giảm số lượng dòng phải quét mà chỉ gây lãng phí RAM.
4. **Cột chứa dữ liệu văn bản quá dài (TEXT, BLOB):** Tốn cực nhiều bộ nhớ để lưu cây B-Tree. Nếu cần tìm kiếm văn bản dài, hãy dùng **Full-Text Search** hoặc **Elasticsearch**.

### 4.3. Chuẩn hoá dữ liệu 1NF, 2NF, 3NF là gì?
- **1NF (First Normal Form - Dạng chuẩn 1):**
  - Mỗi ô trong bảng phải chứa **giá trị nguyên tử (Atomic - không thể chia nhỏ hơn nữa)**.
  - Không được chứa danh sách lặp (ví dụ: cột `phone_numbers` không được lưu `"090123, 090456"`, phải tách thành các dòng riêng).
- **2NF (Second Normal Form - Dạng chuẩn 2):**
  - Đã đạt 1NF.
  - **Mọi cột không khóa phải phụ thuộc hoàn toàn vào toàn bộ Khóa chính (Full Functional Dependency)**, không được phụ thuộc vào một phần của khóa chính (đối với bảng có khóa chính hỗn hợp nhiều cột).
- **3NF (Third Normal Form - Dạng chuẩn 3):**
  - Đã đạt 2NF.
  - **Không có sự phụ thuộc bắc cầu (Transitive Dependency)** giữa các cột không khóa. Nếu cột A xác định cột B, và cột B xác định cột C $\rightarrow$ Phải tách C ra một bảng riêng (ví dụ: `order` lưu `customer_id`, không được lưu trực tiếp `customer_city` vào bảng `order` mà phải lưu ở bảng `customers`).

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-02"></a>

# Chapter 02: JPA/Hibernate Basics – @Entity, @Id, @Column, @Table

## 1. ORM là gì?
- **Object-Relational Mapping**: Ánh xạ Java Class ↔ Database Table tự động.
- **JPA** (Jakarta Persistence API): Specification (chuẩn). **Hibernate**: Implementation phổ biến nhất.

## 2. Entity cơ bản
```java
@Entity
@Table(name = "users")
public class UserEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // Auto-increment
    private Long id;

    @Column(name = "full_name", nullable = false, length = 100)
    private String name;

    @Column(unique = true, nullable = false)
    private String email;

    @Enumerated(EnumType.STRING)  // Lưu enum dạng String (không phải ordinal)
    private Role role;            // enum Role { USER, ADMIN }

    @CreationTimestamp
    private LocalDateTime createdAt;

    @UpdateTimestamp
    private LocalDateTime updatedAt;
}
```

## 3. Annotation chính
| Annotation | Mô tả |
|-----------|-------|
| `@Entity` | Đánh dấu class là entity, map với table |
| `@Table(name)` | Đặt tên bảng (mặc định = tên class) |
| `@Id` | Primary Key |
| `@GeneratedValue` | Chiến lược sinh ID (IDENTITY, SEQUENCE, UUID) |
| `@Column` | Tuỳ chỉnh cột (name, nullable, unique, length) |
| `@Enumerated` | Lưu enum: `STRING` (khuyên dùng) hoặc `ORDINAL` |
| `@CreationTimestamp` | Tự gán thời gian khi INSERT |
| `@UpdateTimestamp` | Tự cập nhật thời gian khi UPDATE |
| `@Transient` | KHÔNG lưu vào DB |

## 4. Cấu hình kết nối (application.yml)
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb?useSSL=false&serverTimezone=UTC
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update   # create | create-drop | update | validate | none
    show-sql: true
    properties:
      hibernate.format_sql: true
```

## 5. ddl-auto modes
| Mode | Mô tả | Khi nào dùng |
|------|-------|-------------|
| `create` | Xoá + tạo lại bảng mỗi lần chạy | Test |
| `update` | Thêm cột/bảng mới, không xoá | Dev |
| `validate` | Chỉ kiểm tra schema khớp, không sửa | Staging/Prod |
| `none` | Không làm gì | Prod (dùng Flyway) |

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. JPA và Hibernate khác nhau thế nào?
- **JPA (Java Persistence API / Jakarta Persistence):**
  - Là một **Bộ tiêu chuẩn / Bản đặc tả giao diện (Specification)** do Oracle/Jakarta định nghĩa.
  - JPA chỉ bao gồm các **Interface** (`EntityManager`, `EntityTransaction`), các **Annotation** (`@Entity`, `@Id`, `@Table`) và các quy chuẩn lý thuyết. JPA hoàn toàn **không có mã nguồn thực thi bên dưới**. Bạn không thể chạy ứng dụng nếu chỉ có JPA.
- **Hibernate:**
  - Là một **Bộ khung triển khai cụ thể (Implementation / Provider)** của đặc tả JPA.
  - Hibernate chứa toàn bộ code thật sự để sinh câu lệnh SQL, quản lý kết nối, bộ đệm Session (First-level Cache, Second-level Cache), và thực thi giao tiếp với Database.
- $\rightarrow$ **Tóm lại:** JPA là chiếc "Vô lăng và Bàn đạp ga" chuẩn mực, còn Hibernate là "Động cơ xe" thực tế giúp cỗ máy vận hành bên dưới.

### 6.2. `ddl-auto: update` có an toàn cho Production không? Tại sao?
- **Khẳng định:** **TUYỆT ĐỐI KHÔNG BAO GIỜ DÙNG `ddl-auto: update` TRÊN PRODUCTION!**
- **Lý do:**
  1. **Không thể xóa cột hoặc đổi tên:** Nếu bạn đổi tên thuộc tính trong code từ `user_name` sang `full_name`, Hibernate sẽ tạo thêm 1 cột mới `full_name` và bỏ quên cột cũ `user_name`, làm dữ liệu cũ bị ngắt kết nối và phân mảnh.
  2. **Nguy cơ khóa bảng (Table Locking / Downtime):** Khi ứng dụng khởi động lại, lệnh `ALTER TABLE` tự động của Hibernate có thể khóa toàn bộ bảng dữ liệu hàng triệu dòng, gây nghẽn toàn bộ hệ thống đang phục vụ khách hàng.
  3. **Không kiểm soát được Version Database:** Không thể biết ai đã thay đổi cột gì, lúc mấy giờ, và không thể rollback (quay xe) khi có sự cố.
- **Giải pháp chuẩn công nghiệp trên Production:**
  - Cấu hình `spring.jpa.hibernate.ddl-auto = validate` hoặc `none`.
  - Quản lý lịch sử tiến hóa Database bằng các công cụ Migration chuyên nghiệp như **Flyway** hoặc **Liquibase**.

### 6.3. `@Enumerated(STRING)` vs `@Enumerated(ORDINAL)` – Tại sao BẮT BUỘC nên dùng `STRING`?
Giả sử bạn có Enum trạng thái đơn hàng:
```java
public enum OrderStatus {
    PENDING,   // Index 0
    SHIPPING,  // Index 1
    DELIVERED  // Index 2
}
```
- **Nếu dùng `@Enumerated(EnumType.ORDINAL)` (Mặc định của JPA):**
  - Hibernate sẽ lưu **số thứ tự index (0, 1, 2)** vào cột trong Database.
  - **THẢM HỌA XẢY RA KHI:** Sau này một lập trình viên thêm trạng thái mới `CANCELLED` chèn vào đầu hoặc giữa Enum:
    ```java
    public enum OrderStatus {
        PENDING, CANCELLED, SHIPPING, DELIVERED
    }
    ```
    Lúc này `CANCELLED` thành số 1, `SHIPPING` bị đẩy thành số 2! Toàn bộ các đơn hàng cũ trước đây đang lưu số 1 trong DB từ "Đang giao" bỗng nhiên biến thành "Đã hủy" $\rightarrow$ **Lệch toàn bộ dữ liệu kinh doanh!**
- **Khi dùng `@Enumerated(EnumType.STRING)`:**
  - Hibernate lưu thẳng chuỗi chữ: `"PENDING"`, `"SHIPPING"`, `"DELIVERED"` vào cột VARCHAR.
  - Dù bạn có đổi thứ tự, thêm bớt enum, dữ liệu trong Database vẫn nguyên vẹn 100% ngữ nghĩa và cực kỳ dễ đọc khi xem trực tiếp bằng SQL.

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-03"></a>

# Chapter 03: Entity Relationships – @OneToMany, @ManyToOne, Lazy vs Eager

## 1. Các loại quan hệ
| Quan hệ | Ví dụ | FK ở bảng nào |
|---------|-------|-------------|
| `@OneToOne` | User ↔ Profile | Bảng con (profile) |
| `@ManyToOne` | Product → Category | Bảng Product (`category_id`) |
| `@OneToMany` | Category → List\<Product\> | Bảng Product |
| `@ManyToMany` | Student ↔ Course | Bảng trung gian (`student_course`) |

## 2. Quan hệ 1-N (Category – Product)
```java
@Entity @Table(name = "categories")
public class CategoryEntity {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany(mappedBy = "category", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<ProductEntity> products = new ArrayList<>();
}

@Entity @Table(name = "products")
public class ProductEntity {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private double price;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "category_id")  // FK column
    private CategoryEntity category;
}
```

### Khái niệm quan trọng
- **`mappedBy`**: Chỉ định bên KHÔNG sở hữu FK (Category). Giá trị = tên field bên sở hữu (`"category"` trong ProductEntity).
- **`@JoinColumn`**: Bên SỞ HỮU FK (Product chứa `category_id`).
- **Owning side**: Bên có `@JoinColumn` → Product.

## 3. CascadeType & OrphanRemoval
| Option | Mô tả |
|--------|-------|
| `CascadeType.PERSIST` | Khi save cha → tự save con |
| `CascadeType.REMOVE` | Khi xoá cha → tự xoá con |
| `CascadeType.ALL` | Tất cả cascade |
| `orphanRemoval = true` | Xoá con khi bị remove khỏi List cha |

## 4. FetchType: Lazy vs Eager
| | LAZY | EAGER |
|---|------|-------|
| Load dữ liệu | Chỉ khi **gọi getter** | **Ngay lập tức** cùng entity cha |
| Performance | ✅ Tốt hơn | ❌ Load thừa dữ liệu |
| Mặc định | `@OneToMany`, `@ManyToMany` | `@ManyToOne`, `@OneToOne` |

> 🔴 **Quy tắc vàng:** LUÔN đặt `FetchType.LAZY` cho tất cả relationships.
> `@ManyToOne(fetch = FetchType.LAZY)`

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. `mappedBy` dùng để làm gì? Điều gì xảy ra nếu quên đặt `mappedBy`?
- **Ý nghĩa:** Dùng trong mối quan hệ hai chiều (Bidirectional Relationship) để khai báo cho Hibernate biết rằng: **Phía này KHÔNG PHẢI là bên sở hữu khóa ngoại (Inverse / Non-owning side)**. Giá trị của `mappedBy = "category"` chính là tên biến thuộc tính của class bên đối diện đang giữ `@JoinColumn`.
- **Hậu quả nếu quên `mappedBy`:**
  - Nếu ở `@OneToMany` mà bạn không đặt `mappedBy`, Hibernate sẽ ngầm hiểu đây là 2 mối quan hệ 1 chiều độc lập.
  - Hibernate sẽ **tự động sinh ra một Bảng trung gian thừa thãi (Join Table)** có tên `categories_products(category_id, product_id)` để liên kết hai bảng, làm hỏng hoàn toàn cấu trúc thiết kế cơ sở dữ liệu và làm chậm tốc độ truy vấn!

### 5.2. Lazy vs Eager Loading? Tại sao BẮT BUỘC nên đặt mặc định là `LAZY`?
- **Khác biệt:**
  - **`EAGER` (Tải háo hức):** Khi load Entity cha, Hibernate tự động thực hiện câu lệnh `LEFT OUTER JOIN` để tải luôn toàn bộ các Entity con liên quan lên bộ nhớ, bất kể bạn có cần dùng tới chúng hay không.
  - **`LAZY` (Tải trì hoãn):** Khi load Entity cha, Hibernate chỉ gán một đối tượng giả lập (**Proxy Object**). Chỉ khi nào bạn thực sự gọi phương thức getter (`category.getProducts()`), Hibernate mới âm thầm bắn thêm 1 câu lệnh SQL xuống Database để kéo dữ liệu con về.
- **Tại sao bắt buộc mặc định là `LAZY`?**
  1. **Tránh nghẽn RAM và tràn bộ nhớ:** Nếu một `Category` có 100.000 `Product`, tải EAGER sẽ kéo toàn bộ 100.000 sản phẩm lên RAM của JVM ngay khi bạn chỉ muốn xem tên danh mục.
  2. **Tránh bài toán hiểm họa N+1 Queries:** EAGER là thủ phạm số 1 khiến ứng dụng bắn hàng trăm câu query rác xuống DB khi bạn duyệt danh sách entity.
  3. *Lưu ý sống còn:* Mặc định của `@ManyToOne` và `@OneToOne` trong chuẩn JPA là `EAGER`. Do đó, **bạn phải LUÔN LUÔN ghi đè rõ ràng:**
     `@ManyToOne(fetch = FetchType.LAZY)`!

### 5.3. `CascadeType.ALL` có nguy hiểm không? Khi nào TUYỆT ĐỐI KHÔNG NÊN dùng?
- **Bản chất của `CascadeType.ALL`:** Gồm cả `PERSIST`, `MERGE`, `REMOVE`, `REFRESH`, `DETACH`. Mọi thao tác trên entity cha sẽ lan truyền (cascade) xuống toàn bộ entity con.
- **Mức độ nguy hiểm của `CascadeType.REMOVE`:**
  - Nếu bạn đặt `CascadeType.ALL` ở mối quan hệ `Product -> Category`, khi một nhân viên xóa một món hàng `Product` hết date, Hibernate sẽ **TỰ ĐỘNG XÓA LUÔN CẢ DANH MỤC `Category` VÀ TOÀN BỘ CÁC SẢN PHẨM KHÁC NẰM TRONG DANH MỤC ĐÓ!**
- **Quy tắc sử dụng chuẩn:**
  - **CHỈ NÊN DÙNG `CascadeType.ALL` (kèm `orphanRemoval = true`):** Cho mối quan hệ cha - con phụ thuộc tuyệt đối (Composition / Parent-Child), nơi mà thực thể con **không thể tồn tại độc lập** nếu thiếu cha. Ví dụ: `Order` $\rightarrow$ `OrderItem`, `Post` $\rightarrow$ `Comment`.
  - **TUYỆT ĐỐI KHÔNG DÙNG:** Cho các mối quan hệ độc lập như `Product -> Category`, `User -> Role`.

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-04"></a>

# Chapter 04: Spring Data JPA – Derived Query, JPQL, N+1 Problem

## 1. JpaRepository
```java
public interface UserRepository extends JpaRepository<UserEntity, Long> {
    // Kế thừa sẵn: save(), findById(), findAll(), deleteById(), existsById(), count()
}
```

## 2. Derived Query Methods (Tự sinh SQL từ tên method)
```java
Optional<UserEntity> findByEmail(String email);
List<UserEntity> findByNameContainingIgnoreCase(String keyword);
List<UserEntity> findByAgeGreaterThanEqual(int age);
List<UserEntity> findByActiveTrue();
boolean existsByEmail(String email);
long countByRole(Role role);
List<UserEntity> findByNameOrderByCreatedAtDesc(String name);
```

## 3. @Query – JPQL & Native SQL
```java
// JPQL (truy vấn trên Entity, không phải table)
@Query("SELECT u FROM UserEntity u WHERE u.email = :email AND u.active = true")
Optional<UserEntity> findActiveByEmail(@Param("email") String email);

// Native SQL (truy vấn SQL thuần)
@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
Optional<UserEntity> findByEmailNative(String email);

// Update
@Modifying
@Query("UPDATE UserEntity u SET u.active = false WHERE u.id = :id")
void deactivateUser(@Param("id") Long id);
```

## 4. N+1 Problem
```java
// ❌ N+1: Lấy 10 categories → mỗi category query thêm products → 1 + 10 = 11 queries!
List<CategoryEntity> categories = categoryRepo.findAll();
for (CategoryEntity c : categories) {
    c.getProducts().size();  // Mỗi lần gọi = 1 query SELECT products WHERE category_id = ?
}
```

### Giải pháp
```java
// ✅ JOIN FETCH: 1 query duy nhất
@Query("SELECT c FROM CategoryEntity c LEFT JOIN FETCH c.products")
List<CategoryEntity> findAllWithProducts();

// ✅ @EntityGraph
@EntityGraph(attributePaths = {"products"})
List<CategoryEntity> findAll();
```

## 5. Câu hỏi phỏng vấn & Trả lời chi tiết

### 5.1. Derived Query Method trong Spring Data JPA hoạt động như thế nào?
- **Bản chất:** Bạn chỉ cần viết tên phương thức trong Interface (ví dụ: `findByEmailAndStatus(String email, Status status)`), Spring Data JPA sẽ **tự động sinh mã nguồn câu lệnh SQL tương ứng lúc runtime mà bạn không cần phải viết một dòng SQL hay class implementation nào!**
- **Cơ chế phân tích cú pháp (Method Name Parsing):**
  - Spring phân rã tên hàm theo tiền tố quy ước: `find...By`, `read...By`, `count...By`, `exists...By`, `delete...By`.
  - Phân tích các thuộc tính của Entity kết hợp cùng các từ khóa điều kiện logic: `And`, `Or`, `Between`, `LessThan`, `GreaterThan`, `Like`, `Containing`, `OrderBy...Desc`.
  - Tự động tạo Dynamic Proxy của Interface lúc ứng dụng khởi động và mapping với EntityManager.

### 5.2. JPQL khác Native SQL thế nào? Khi nào nên dùng cái nào?
| Tiêu chí | JPQL (Java Persistence Query Language) | Native SQL |
| :--- | :--- | :--- |
| **Đối tượng thao tác** | **Thao tác trên Entity Class và thuộc tính Java** (`SELECT u FROM UserEntity u WHERE u.email = :email`). | **Thao tác trực tiếp trên Bảng và Cột vật lý của DB** (`SELECT * FROM users WHERE email = ?`). |
| **Tính độc lập CSDL (Database Independence)** | **Rất cao**: Cùng 1 câu JPQL, Hibernate tự dịch sang đúng dialect của MySQL, PostgreSQL, hoặc Oracle. | Kém: Phụ thuộc vào cú pháp đặc thù của hệ quản trị CSDL đang dùng. |
| **Kiểm tra an toàn** | Compiler/Hibernate kiểm tra cú pháp lúc startup, bắt lỗi gõ sai tên trường sớm. | Dễ lỗi gõ sai tên cột, chỉ phát hiện khi câu query thực thi. |
| **Khuyên dùng** | **Dùng cho 90% các câu query trong dự án.** | Chỉ dùng khi cần tận dụng các hàm chuyên biệt của DB (ví dụ: hàm địa lý GIS, JSON operators trong Postgres, hoặc các câu query báo cáo phân tích siêu phức tạp cần tối ưu hiệu năng tối đa). |

### 5.3. N+1 Problem là gì? Phân tích 2 cách giải quyết triệt để nhất
- **N+1 Problem là gì?**
  - Xảy ra khi bạn muốn lấy danh sách $N$ đối tượng cha và thông tin đối tượng con liên quan của chúng.
  - Hibernate bắn **1 câu query đầu tiên** để lấy danh sách $N$ cha (`SELECT * FROM categories`).
  - Sau đó, khi duyệt qua từng cha trong vòng lặp `for`, Hibernate lại phải bắn thêm **$N$ câu query con riêng biệt** (`SELECT * FROM products WHERE category_id = ?`) để lấy các con của từng cha.
  - $\rightarrow$ Tổng số câu query bắn xuống DB: **$1 + N$ queries**. Nếu $N = 1000$, hệ thống sẽ bắn 1001 câu truy vấn, làm nghẽn mạng và sập Database ngay lập tức!
- **2 Cách giải quyết triệt để:**
  1. **Cách 1: Sử dụng `JOIN FETCH` trong JPQL (Khuyên dùng):**
     ```java
     @Query("SELECT c FROM CategoryEntity c LEFT JOIN FETCH c.products")
     List<CategoryEntity> findAllWithProducts();
     ```
     Hibernate sẽ gộp lại thành **DUY NHẤT 1 câu lệnh SQL `LEFT OUTER JOIN`** để kéo toàn bộ cha và con về cùng lúc.
  2. **Cách 2: Sử dụng `@EntityGraph`:**
     ```java
     @EntityGraph(attributePaths = {"products"})
     List<CategoryEntity> findAll();
     ```
     Khai báo cho Spring Data JPA biết trường `products` cần được nạp Eager tức thì trong câu query này mà không cần viết lại câu JPQL.

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-05"></a>

# Chapter 05: Transaction Management – @Transactional

## 1. ACID
| Thuộc tính | Ý nghĩa |
|-----------|---------|
| **A**tomicity | Tất cả hoặc không gì cả (rollback nếu lỗi) |
| **C**onsistency | Dữ liệu luôn hợp lệ trước và sau transaction |
| **I**solation | Transaction này không ảnh hưởng transaction khác |
| **D**urability | Dữ liệu đã commit sẽ không mất dù server crash |

## 2. @Transactional trong Spring
```java
@Service
public class OrderService {
    @Transactional  // Nếu bất kỳ bước nào lỗi → rollback TẤT CẢ
    public void placeOrder(OrderRequest request) {
        OrderEntity order = orderRepository.save(mapToEntity(request));  // Bước 1
        paymentService.charge(request.getAmount());                      // Bước 2 (nếu lỗi → rollback bước 1)
        inventoryService.reduceStock(request.getProductId());            // Bước 3
        emailService.sendConfirmation(order);                            // Bước 4
    }
}
```

## 3. Propagation
| Type | Mô tả |
|------|-------|
| `REQUIRED` (mặc định) | Dùng transaction hiện tại, tạo mới nếu chưa có |
| `REQUIRES_NEW` | Luôn tạo transaction MỚI, tạm dừng transaction cũ |
| `SUPPORTS` | Dùng transaction nếu có, không có thì chạy không transaction |
| `NOT_SUPPORTED` | Chạy không transaction |

## 4. Rollback Rules
```java
// Mặc định: Chỉ rollback với RuntimeException (Unchecked)
@Transactional  // IOException (Checked) sẽ KHÔNG rollback!

// Cấu hình rollback mọi Exception
@Transactional(rollbackFor = Exception.class)

// Không rollback cho exception cụ thể
@Transactional(noRollbackFor = EmailException.class)
```

## 5. Isolation Levels
| Level | Mô tả |
|-------|-------|
| `READ_UNCOMMITTED` | Đọc dữ liệu chưa commit (dirty read) |
| `READ_COMMITTED` | Chỉ đọc dữ liệu đã commit (mặc định PostgreSQL) |
| `REPEATABLE_READ` | Đảm bảo đọc lại cùng giá trị (mặc định MySQL) |
| `SERIALIZABLE` | Tuần tự hoàn toàn, chậm nhất |

## 6. Lưu ý quan trọng
- `@Transactional` chỉ hoạt động khi gọi từ **BÊN NGOÀI** class (qua proxy). Gọi method trong cùng class → **KHÔNG có transaction**!
- Đặt `@Transactional` trên **Service layer**, không đặt trên Controller.

## 7. Câu hỏi phỏng vấn & Trả lời chi tiết

### 7.1. ACID là gì? Ý nghĩa của từng chữ cái trong giao dịch cơ sở dữ liệu
- **A - Atomicity (Tính nguyên tử - "Tất cả hoặc Không có gì"):**
  - Toàn bộ các thao tác trong giao dịch phải thành công trọn vẹn 100%. Nếu có bất kỳ bước nào thất bại, toàn bộ các bước đã làm trước đó phải được hoàn tác (**Rollback**) về trạng thái ban đầu (ví dụ: chuyển tiền thành công ở bên gửi nhưng bên nhận lỗi $\rightarrow$ hoàn tiền lại cho bên gửi).
- **C - Consistency (Tính nhất quán):**
  - Dữ liệu trước và sau giao dịch đều phải tuân thủ đúng mọi ràng buộc toàn vẹn (Constraints, Foreign Keys, Triggers, số dư tài khoản không được âm).
- **I - Isolation (Tính cô lập):**
  - Nhiều giao dịch chạy đồng thời (Concurrent Transactions) không được can thiệp hay nhìn thấy dữ liệu dở dang chưa commit của nhau. Tránh các hiện tượng: *Dirty Read, Non-repeatable Read, Phantom Read*.
- **D - Durability (Tính bền vững):**
  - Một khi giao dịch đã báo Commit thành công, dữ liệu sẽ được ghi vĩnh viễn xuống ổ cứng (Write-Ahead Logging - WAL). Dù sau đó máy chủ có mất điện đột ngột hay sập server thì dữ liệu vẫn không bao giờ bị biến mất.

### 7.2. `@Transactional` mặc định Rollback khi nào? Cách cấu hình để Rollback cả Checked Exception?
- **Mặc định nguy hiểm trong Spring:**
  - Spring `@Transactional` **CHỈ TỰ ĐỘNG ROLLBACK khi gặp `RuntimeException` (Unchecked Exception) và `Error`**.
  - Nếu gặp **`Checked Exception`** (như `IOException`, `SQLException`, hoặc class custom kế thừa từ `Exception`), Spring **MẶC ĐỊNH SẼ KHÔNG ROLLBACK** (Giao dịch vẫn bị Commit dù có lỗi!).
- **Cách cấu hình chuẩn an toàn:**
  Bắt buộc phải thêm thuộc tính `rollbackFor = Exception.class`:
  ```java
  @Transactional(rollbackFor = Exception.class)
  public void transferMoney(...) { ... }
  ```
  Lúc này, bất kỳ ngoại lệ nào xảy ra (cả Checked lẫn Unchecked), Spring đều sẽ kích hoạt Rollback toàn bộ dữ liệu.

### 7.3. `REQUIRED` vs `REQUIRES_NEW` khác nhau thế nào?
| Tiêu chí | `Propagation.REQUIRED` (Mặc định) | `Propagation.REQUIRES_NEW` |
| :--- | :--- | :--- |
| **Cơ chế** | Nếu **đã có transaction cha**: Tham gia vào transaction đó. Nếu **chưa có**: Tạo mới. | **Luôn luôn tạo một Transaction mới hoàn toàn độc lập**. |
| **Ảnh hưởng lẫn nhau** | Nếu phương thức con bị lỗi $\rightarrow$ Toàn bộ Transaction cha cũng bị **Rollback theo**. | Transaction con chạy độc lập trong kết nối DB riêng. Nếu con lỗi/thành công, nó commit/rollback riêng mà **không làm chết Transaction cha** (và ngược lại). |
| **Ứng dụng thực tế** | Dùng cho **95% các nghiệp vụ thông thường** (tạo đơn, cập nhật kho, trừ tiền). | Dùng cho các tác vụ phụ bắt buộc phải ghi dữ liệu kể cả khi nghiệp vụ chính lỗi: **Ghi lịch sử Audit Log, Lưu vết thanh toán thất bại, Đếm số lần đăng nhập sai**. |

### 7.4. Tại sao `@Transactional` KHÔNG HOẠT ĐỘNG khi gọi nội bộ trong cùng Class (Self-Invocation)?
- **Nguyên nhân gốc rễ (Spring AOP Proxy Mechanism):**
  - `@Transactional` hoạt động dựa trên cơ chế **Dynamic Proxy**.
  - Khi một Class bên ngoài (như `Controller`) gọi `orderService.placeOrder()`, thực chất nó đang gọi xuyên qua một lớp vỏ bọc **Proxy Object**. Proxy này sẽ mở kết nối DB $\rightarrow$ Bắt đầu Transaction $\rightarrow$ Gọi hàm thật $\rightarrow$ Commit / Rollback.
  - Nhưng khi bạn viết:
    ```java
    public void methodA() {
        methodB(); // 👈 Gọi nội bộ cùng class (this.methodB())
    }

    @Transactional
    public void methodB() { ... }
    ```
    Lệnh `methodB()` được gọi trực tiếp trên con trỏ `this` (đối tượng thật bên trong), cuộc gọi này **hoàn toàn đi tắt mà không hề đi qua lớp vỏ bọc Spring Proxy**.
  - $\rightarrow$ Kết quả: Annotation `@Transactional` trên `methodB()` bị **vô hiệu hóa hoàn toàn**, không có transaction nào được tạo ra!
- **Cách khắc phục:**
  1. Tách `methodB()` sang một Service/Component riêng biệt rồi inject vào.
  2. Hoặc tự inject chính interface của Service vào bản thân (Self-autowiring).

---

<div style="page-break-before: always;"></div>

<a id="phase-5-chapter-06"></a>

# Chapter 06: Pagination & Sorting – Pageable, Page, Slice

## 1. Tạo Pageable
```java
// PageRequest.of(page, size, sort)  – page bắt đầu từ 0
Pageable pageable = PageRequest.of(0, 20, Sort.by("createdAt").descending());

// Nhiều trường sort
Pageable pageable = PageRequest.of(0, 20,
    Sort.by("price").ascending().and(Sort.by("name").descending()));
```

## 2. Repository
```java
public interface ProductRepository extends JpaRepository<ProductEntity, Long> {
    Page<ProductEntity> findByCategory(String category, Pageable pageable);
    Slice<ProductEntity> findByActiveTrue(Pageable pageable);
}
```

## 3. Page\<T\> vs Slice\<T\>
| | Page\<T\> | Slice\<T\> |
|---|----------|-----------|
| Count query | ✅ Có (`SELECT COUNT(*)`) | ❌ Không |
| `getTotalElements()` | ✅ | ❌ |
| `getTotalPages()` | ✅ | ❌ |
| `hasNext()` | ✅ | ✅ |
| Phù hợp | Phân trang truyền thống (1, 2, 3...) | Infinite scroll / Load more |

## 4. Controller nhận Pageable tự động
```java
@GetMapping
public ResponseEntity<Page<ProductResponse>> getProducts(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "20") int size,
    @RequestParam(defaultValue = "createdAt,desc") String[] sort
) {
    Pageable pageable = PageRequest.of(page, size, Sort.by(Sort.Direction.DESC, "createdAt"));
    Page<ProductEntity> productPage = productRepository.findAll(pageable);
    Page<ProductResponse> responsePage = productPage.map(this::toResponse);
    return ResponseEntity.ok(responsePage);
}
```

## 5. Response DTO cho phân trang
```json
{
  "content": [...],
  "pageNo": 0,
  "pageSize": 20,
  "totalElements": 150,
  "totalPages": 8,
  "last": false
}
```

## 6. Câu hỏi phỏng vấn & Trả lời chi tiết

### 6.1. `Page<T>` vs `Slice<T>` khác nhau thế nào? Khi nào nên dùng `Slice<T>`?
| Tiêu chí | `Page<T>` | `Slice<T>` |
| :--- | :--- | :--- |
| **Số câu query bắn xuống DB** | **Bắn 2 câu query**: 1 câu `SELECT ... LIMIT ... OFFSET` để lấy dữ liệu trang hiện tại, và **1 câu `SELECT COUNT(*)`** để tính tổng số bản ghi. | **Chỉ bắn duy nhất 1 câu query**: `SELECT ... LIMIT (size + 1) OFFSET ...`. Không bao giờ gọi `COUNT(*)`. |
| **Thông tin cung cấp** | Biết được tổng số trang (`totalPages`), tổng số bản ghi (`totalElements`), trang hiện tại. | **Không biết tổng số trang**. Chỉ biết duy nhất một thông tin: **Có còn trang kế tiếp hay không (`hasNext()`)**. |
| **Hiệu năng (Performance)** | **Chậm khi bảng có hàng triệu dòng**: Lệnh `COUNT(*)` trên bảng lớn sẽ quét rất lâu, gây nghẽn CPU Database. | **Cực nhanh và nhẹ**: Vì hoàn toàn không tốn chi phí chạy hàm `COUNT(*)`. |
| **Khi nào dùng:**
  - **Dùng `Page<T>` khi:** Giao diện có thanh điều hướng số trang cụ thể (Trang 1, 2, 3... 10 như trên website TMĐT tìm kiếm sản phẩm).
  - **Dùng `Slice<T>` khi:** Giao diện là **Cuộn vô tận (Infinite Scroll)** như Facebook Feed, TikTok, hoặc nút **"Xem thêm" (Load More)**. Người dùng chỉ cần biết còn bài viết để cuộn tiếp hay không chứ không quan tâm tổng số lượng bài viết là bao nhiêu.

### 6.2. Phân trang ảnh hưởng performance thế nào khi Offset lớn (Deep Pagination)? Cách khắc phục?
- **Vấn đề Deep Pagination:**
  - Khi client gọi trang quá sâu: `GET /products?page=10000&size=20` $\rightarrow$ SQL sinh ra:
    `SELECT * FROM products ORDER BY id LIMIT 20 OFFSET 200000;`
  - **Cơ chế nghẽn của Database:** Database **không thể nhảy cóc thẳng tới dòng 200.001**. Nó bắt buộc phải đọc và duyệt qua toàn bộ **200.000 dòng đầu tiên**, nạp vào bộ nhớ, rồi sau đó mới vứt bỏ 200.000 dòng đó đi để lấy đúng 20 dòng cuối cùng! Càng về các trang sau, query chạy càng chậm (mất vài giây tới vài chục giây).
- **Giải pháp tối ưu chuẩn công nghiệp: Phân trang theo con trỏ (Keyset / Cursor-based Pagination):**
  - Thay vì dùng `OFFSET`, Client gửi kèm `id` của phần tử cuối cùng ở trang trước:
    `GET /products?lastId=200000&size=20`
  - SQL chuyển thành câu lệnh tìm kiếm index trực tiếp:
    ```sql
    SELECT * FROM products WHERE id > 200000 ORDER BY id ASC LIMIT 20;
    ```
  - **Hiệu năng:** Database dùng B-Tree Index nhảy thẳng tới `id = 200000` với tốc độ **$O(1)$ tức thì (dưới 5 mili-giây)**, bất kể bạn đang phân trang ở trang thứ 1 hay trang thứ 1 triệu!

---

<div style="page-break-before: always;"></div>

<a id="phase-6"></a>

# PHASE 6: BẢO MẬT HỆ THỐNG (SPRING SECURITY & JWT)

---

<div style="page-break-before: always;"></div>

<a id="phase-6-chapter-01"></a>

# Chapter 01: Nền Tảng Bảo Mật – Authentication vs Authorization & Hash Mật Khẩu với BCrypt

---

## 1. Authentication (Xác thực) vs Authorization (Phân quyền)

Trong phát triển hệ thống Backend, đây là 2 khái niệm nền tảng luôn đi kèm nhưng có mục đích hoàn toàn riêng biệt:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           Client / Người dùng                           │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     │ 1. Cung cấp thông tin đăng nhập (Credentials)
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                      AUTHENTICATION (XÁC THỰC)                          │
│                      Câu hỏi: "BẠN LÀ AI?"                              │
│  → So khớp mật khẩu đã hash, kiểm tra tài khoản có tồn tại/bị khóa?     │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     │ Xác thực thành công → Cấp Danh tính (Token / Session)
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                   Cấp Danh Tính / Access Token (JWT)                    │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     │ 2. Gửi request nghiệp vụ kèm Token (Authorization: Bearer)
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                      AUTHORIZATION (PHÂN QUYỀN)                         │
│                      Câu hỏi: "BẠN ĐƯỢC PHÉP LÀM GÌ?"                   │
│  → Đọc Roles/Permissions trong Token, kiểm tra quyền truy cập Endpoint  │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     │ Hợp lệ (Đủ quyền hạn)
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│               Tài nguyên bảo vệ / API Endpoint (@PreAuthorize)          │
└─────────────────────────────────────────────────────────────────────────┘
```

| Tiêu chí | Authentication (Xác thực - 401 Unauthorized) | Authorization (Phân quyền - 403 Forbidden) |
| :--- | :--- | :--- |
| **Câu hỏi cốt lõi** | **"Bạn là ai?" (Who are you?)** | **"Bạn có quyền làm gì?" (What can you do?)** |
| **Thời điểm diễn ra**| Luôn diễn ra **đầu tiên**. | Diễn ra **sau** khi đã xác thực danh tính thành công. |
| **Thông tin kiểm tra**| Username, Password, OTP, Sinh trắc học, Chữ ký số. | Vai trò (Roles: `ADMIN`, `USER`), Quyền hạn (Permissions: `READ`, `WRITE`, `DELETE`). |
| **Lỗi trả về HTTP**| **`401 Unauthorized`** (Chưa đăng nhập hoặc token sai/hết hạn). | **`403 Forbidden`** (Đã đăng nhập nhưng không đủ thẩm quyền truy cập). |

---

## 2. Nguyên tắc bảo mật mật khẩu người dùng

> ⚠️ **Quy tắc bất biến:** TUYỆT ĐỐI KHÔNG BAO GIỜ lưu mật khẩu dưới dạng chuỗi thuần (Plaintext) vào Database!

### Tại sao không dùng các thuật toán băm thông thường (MD5, SHA-1, SHA-256)?
- **MD5 / SHA-256** là các thuật toán băm hướng tới **tốc độ nhanh** (thích hợp kiểm tra checksum file).
- Tuy nhiên, vì quá nhanh nên kẻ tấn công có thể dùng kỹ thuật vét cạn (Brute-force) hoặc tra cứu qua **Rainbow Table** (bảng bảng băm tính sẵn hàng tỉ mật khẩu phổ biến) để giải ngược ra mật khẩu gốc chỉ trong vài giây.

---

## 3. Giải pháp chuẩn: BCrypt Hashing Algorithm

**BCrypt** là thuật toán băm mật khẩu chuẩn trong ngành phát triển phần mềm nhờ 2 đặc tính ưu việt:

### A. Tự động sinh Salt (Muối ngẫu nhiên)
- Mỗi lần băm cùng một mật khẩu (ví dụ: `"password123"`), BCrypt tự động tạo ra một chuỗi ngẫu nhiên (Salt) và nhúng chung vào chuỗi kết quả.
- Kết quả là: Hai tài khoản có cùng mật khẩu `"password123"` sẽ có 2 chuỗi băm **hoàn toàn khác nhau** trong cơ sở dữ liệu.
- Kẻ tấn công không thể sử dụng Rainbow Table để dò quét hàng loạt.

### B. Cơ chế Work Factor (Độ phức tạp tính toán)
- Cho phép điều chỉnh số vòng lặp tính toán (Cost factor, mặc định là $10$ hoặc $12$, tương đương $2^{10} = 1024$ vòng lặp).
- Máy tính càng mạnh lên theo thời gian thì ta chỉ cần nâng Cost factor lên để kéo dài thời gian tính toán băm, vô hiệu hóa các dàn máy đào GPU giải mã Brute-force.

---

## 4. Cấu trúc của một chuỗi BCrypt Hash

Một chuỗi BCrypt lưu trong database thường có độ dài 60 ký tự, chia thành 3 phần:

```text
$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
\__/ \/ \____________________/\_____________________________/
 (1) (2)         (3)                        (4)
```

1. **`$2a$`**: Phiên bản thuật toán BCrypt.
2. **`10`**: Cost factor ($2^{10}$ vòng băm).
3. **`N9qo8uLOickgx2ZMRZoMye`**: 22 ký tự Salt ngẫu nhiên được sinh ra.
4. **`IjZAgcfl7p92ldGxad68LJZdL17lhWy`**: 31 ký tự băm của (Mật khẩu + Salt).

---

## 5. Cài đặt và sử dụng `PasswordEncoder` trong Spring Boot

Spring Security cung cấp interface `PasswordEncoder` với implementation chuẩn mực là `BCryptPasswordEncoder`.

### Cấu hình Bean trong Spring:
```java
package com.example.app.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
public class SecurityBeanConfig {

    @Bean
    public PasswordEncoder passwordEncoder() {
        // Độ mạnh mặc định: 10 vòng lặp
        return new BCryptPasswordEncoder();
    }
}
```

### Sử dụng khi Đăng ký (Encode) & Đăng nhập (Matches):
```java
@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;

    // 1. Khi người dùng ĐĂNG KÝ
    public void register(RegisterRequest request) {
        // Băm mật khẩu trước khi lưu DB
        String encodedPassword = passwordEncoder.encode(request.getPassword());

        UserEntity user = UserEntity.builder()
                .email(request.getEmail())
                .password(encodedPassword)
                .role(Role.USER)
                .build();

        userRepository.save(user);
    }

    // 2. Khi người dùng ĐĂNG NHẬP
    public boolean checkLogin(String rawPassword, String encodedPasswordFromDb) {
        // KHÔNG BAO GIỜ băm lại rawPassword rồi so sánh chuỗi (vì Salt ngẫu nhiên nên sẽ không bao giờ bằng nhau)
        // BẮT BUỘC dùng phương thức matches() của BCrypt
        return passwordEncoder.matches(rawPassword, encodedPasswordFromDb);
    }
}
```

---

## 6. Câu hỏi phỏng vấn thường gặp (Interview Q&A)

### Q1: Vì sao hàm `passwordEncoder.encode("123456")` chạy 2 lần cho ra 2 kết quả khác nhau, nhưng hàm `passwordEncoder.matches("123456", hash)` vẫn trả về `true`?
**Trả lời:**
- Do mỗi lần gọi `encode()`, BCrypt tự động sinh ra một chuỗi Salt ngẫu nhiên và gắn luôn vào trong chuỗi hash kết quả.
- Khi gọi `matches(rawPassword, hash)`, BCrypt sẽ bóc tách chuỗi Salt nằm trong chuỗi `hash` có sẵn, lấy Salt đó băm chung với `rawPassword` và đối chiếu phần còn lại. Nếu khớp, trả về `true`.

### Q2: Sự khác biệt giữa mã hóa (Encryption) và băm (Hashing) là gì?
**Trả lời:**
- **Mã hóa (Encryption)**: Là thuật toán **2 chiều** (Reversible). Dữ liệu sau khi mã hóa có thể được giải mã ngược lại thành bản rõ nếu có Secret Key (ví dụ: AES, RSA).
- **Băm (Hashing)**: Là thuật toán **1 chiều** (Irreversible). Không thể giải mã ngược chuỗi băm về ban đầu. Mật khẩu bắt buộc phải dùng Hashing, không dùng Encryption.

---

<div style="page-break-before: always;"></div>

<a id="phase-6-chapter-02"></a>

# Chapter 02: Kiến Trúc Spring Security – SecurityFilterChain, AuthenticationManager & UserDetailsService

---

## 1. Bản chất của Spring Security trong Web Application

Trong ứng dụng Spring Boot Web, mọi HTTP Request gửi tới server **không đi thẳng vào Controller ngay**.
Thay vào đó, nó phải đi qua một chuỗi các bộ lọc an ninh gọi là **Servlet Filter Chain**, trong đó Spring Security cắm vào một mắt xích tối quan trọng: **`DelegatingFilterProxy`** và **`FilterChainProxy`**.

```
┌────────────────────────────────────────────────────────┐
│                  Client HTTP Request                   │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│   DelegatingFilterProxy (Cầu nối giữa Servlet & Spring)│
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│        FilterChainProxy (Quản lý SecurityFilterChain)  │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│        SecurityFilterChain (Chuỗi các Security Filter) │
│                                                        │
│   ┌────────────────────────────────────────────────┐   │
│   │ 1. CorsFilter (Kiểm tra nguồn truy cập CORS)   │   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 2. CsrfFilter (Bảo vệ chống tấn công CSRF)     │   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 3. JwtAuthenticationFilter (Custom Token Parse)│   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 4. UsernamePasswordAuthenticationFilter        │   │
│   └───────────────────────┬────────────────────────┘   │
│                           ▼                            │
│   ┌────────────────────────────────────────────────┐   │
│   │ 5. AuthorizationFilter (Kiểm tra quyền Role)   │   │
│   └────────────────────────────────────────────────┘   │
└───────────────────────────┬────────────────────────────┘
                            │ (Vượt qua mọi Filter an toàn)
                            ▼
┌────────────────────────────────────────────────────────┐
│       DispatcherServlet ──► @RestController            │
└────────────────────────────────────────────────────────┘
```

---

## 2. Kiến trúc Xác thực (Authentication Architecture)

Khi một user gửi yêu cầu đăng nhập (username + password), hệ thống Spring Security điều phối các thành phần theo mô hình sau:

```
┌────────────────────────────────────────────────────────────────────────┐
│                 Request Đăng nhập (username, password)                 │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│      UsernamePasswordAuthenticationFilter / Custom AuthController      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Tạo UsernamePasswordAuthenticationToken (unauthenticated)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│       AuthenticationManager (Interface trung tâm điều phối xác thực)   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Giao việc cho Provider thích hợp
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                      DaoAuthenticationProvider                         │
│                                                                        │
│   ┌────────────────────────────────────────────────────────────────┐   │
│   │ 1. UserDetailsService: Tìm User theo username từ Database     │   │
│   │    └─► Database (Truy vấn User, Password hash, Roles)          │   │
│   └───────────────────────────────┬────────────────────────────────┘   │
│                                   ▼                                    │
│   ┌────────────────────────────────────────────────────────────────┐   │
│   │ 2. PasswordEncoder: BCrypt so khớp mật khẩu gửi lên vs DB hash │   │
│   └────────────────────────────────────────────────────────────────┘   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Trùng khớp thông tin (Credentials Valid)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│          Authentication Object (Trạng thái: Authenticated = true)      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Lưu trữ thông tin người dùng vào luồng hiện tại
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│           SecurityContextHolder ──► SecurityContext                    │
└────────────────────────────────────────────────────────────────────────┘
```

### Các thành phần cốt lõi:

1. **`SecurityContextHolder` & `SecurityContext`**:
   - Nơi lưu trữ thông tin của người dùng đang thực hiện request hiện tại (`Authentication` object).
   - Được gắn vào `ThreadLocal` của mỗi request thread.
   - Để lấy thông tin user hiện tại ở bất kỳ đâu trong code:
     ```java
     Authentication auth = SecurityContextHolder.getContext().getAuthentication();
     String currentUsername = auth.getName();
     ```

2. **`AuthenticationManager`**:
   - Nhận vào một đối tượng `Authentication` chưa xác thực (chứa username, raw password) và trả về đối tượng `Authentication` đã xác thực (kèm roles, permissions).

3. **`DaoAuthenticationProvider`**:
   - Triển khai chuẩn của `AuthenticationProvider`, chịu trách nhiệm:
     - Gọi `UserDetailsService` để tìm user theo username từ DB.
     - Dùng `PasswordEncoder` để so khớp mật khẩu raw với mật khẩu đã băm.

4. **`UserDetailsService` & `UserDetails`**:
   - **`UserDetails`**: Interface đại diện cho hồ sơ user của Spring Security (gồm username, password, authorities, trạng thái khóa tài khoản).
   - **`UserDetailsService`**: Interface chỉ có **duy nhất 1 phương thức**:
     ```java
     UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
     ```

---

## 3. Triển khai code thực tế (Spring Boot 3.x)

### Bước 1: Tạo Entity hoặc Adaptor triển khai `UserDetails`
```java
package com.example.app.security;

import com.example.app.entity.UserEntity;
import lombok.RequiredArgsConstructor;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.Collection;
import java.util.List;

@RequiredArgsConstructor
public class CustomUserDetails implements UserDetails {

    private final UserEntity user;

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        // Spring Security quy ước Role bắt đầu bằng tiền tố "ROLE_"
        return List.of(new SimpleGrantedAuthority("ROLE_" + user.getRole().name()));
    }

    @Override
    public String getPassword() {
        return user.getPassword();
    }

    @Override
    public String getUsername() {
        return user.getEmail(); // Dùng email làm tên đăng nhập
    }

    @Override
    public boolean isAccountNonExpired() { return true; }

    @Override
    public boolean isAccountNonLocked() { return true; }

    @Override
    public boolean isCredentialsNonExpired() { return true; }

    @Override
    public boolean isEnabled() { return user.isActive(); }
}
```

### Bước 2: Triển khai `UserDetailsService`
```java
package com.example.app.security;

import com.example.app.repository.UserRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

@Service
@RequiredArgsConstructor
public class CustomUserDetailsService implements UserDetailsService {

    private final UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String email) throws UsernameNotFoundException {
        return userRepository.findByEmail(email)
                .map(CustomUserDetails::new)
                .orElseThrow(() -> new UsernameNotFoundException("Không tìm thấy người dùng với email: " + email));
    }
}
```

### Bước 3: Cấu hình `SecurityFilterChain` trong Spring Boot 3.x
Từ Spring Security 6.x (Spring Boot 3.x), không còn dùng `WebSecurityConfigurerAdapter` mà sử dụng `SecurityFilterChain` Bean với Lambda DSL:

```java
package com.example.app.config;

import com.example.app.security.CustomUserDetailsService;
import lombok.RequiredArgsConstructor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.AuthenticationProvider;
import org.springframework.security.authentication.dao.DaoAuthenticationProvider;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
import org.springframework.security.config.annotation.method.configuration.EnableMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
@EnableMethodSecurity // Cho phép dùng @PreAuthorize ở tầng Controller/Service
@RequiredArgsConstructor
public class SecurityConfig {

    private final CustomUserDetailsService userDetailsService;
    private final PasswordEncoder passwordEncoder;

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            // 1. Tắt CSRF vì REST API dùng JWT không trạng thái
            .csrf(csrf -> csrf.disable())

            // 2. Phân quyền Endpoint
            .authorizeHttpRequests(auth -> auth
                // Cho phép tự do truy cập các endpoint công khai
                .requestMatchers("/api/v1/auth/**", "/swagger-ui/**", "/v3/api-docs/**").permitAll()
                // Chỉ role ADMIN mới vào được /api/v1/admin/**
                .requestMatchers("/api/v1/admin/**").hasRole("ADMIN")
                // Tất cả các request còn lại bắt buộc phải đăng nhập
                .anyRequest().authenticated()
            )

            // 3. Cấu hình Session Stateless (Không lưu session trên server memory)
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )

            // 4. Khai báo Authentication Provider
            .authenticationProvider(authenticationProvider());

        return http.build();
    }

    @Bean
    public AuthenticationProvider authenticationProvider() {
        DaoAuthenticationProvider authProvider = new DaoAuthenticationProvider();
        authProvider.setUserDetailsService(userDetailsService);
        authProvider.setPasswordEncoder(passwordEncoder);
        return authProvider;
    }

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }
}
```

---

## 4. Tóm tắt các điểm then chốt

1. Mọi request đều đi qua `SecurityFilterChain`.
2. Trong ứng dụng REST API Stateless, ta cấu hình `SessionCreationPolicy.STATELESS` và vô hiệu hóa CSRF.
3. `UserDetailsService` là cầu nối giữa Database của ứng dụng với cơ chế xác thực của Spring Security.
4. Thông tin định danh của request hiện tại luôn nằm trong `SecurityContextHolder`.

---

## 5. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 5.1. `SecurityContextHolder`, `SecurityContext` và `Authentication` liên kết với nhau như thế nào?
- **Mô hình búp bê Nga lồng nhau:**
  $$\text{SecurityContextHolder} \longrightarrow \text{SecurityContext} \longrightarrow \text{Authentication}$$
  1. **`SecurityContextHolder`:** Là lớp ngoài cùng, sử dụng chiến lược lưu trữ mặc định **`ThreadLocal`**. Đảm bảo mỗi luồng (Thread) phục vụ 1 HTTP request sẽ có một không gian lưu trữ bảo mật độc lập, không sợ bị lẫn lộn giữa các người dùng.
  2. **`SecurityContext`:** Là interface chứa thông tin bảo mật của request hiện tại, lấy qua `SecurityContextHolder.getContext()`.
  3. **`Authentication`:** Là đối tượng đại diện cho người dùng đã đăng nhập, chứa:
     - `getPrincipal()`: Thông tin user (thường là instance của `UserDetails`).
     - `getCredentials()`: Mật khẩu hoặc token (thường được xóa đi sau khi xác thực thành công để bảo mật).
     - `getAuthorities()`: Danh sách các quyền/vai trò (`GrantedAuthority` - ví dụ `ROLE_ADMIN`).
     - `isAuthenticated()`: `true` nếu đã xác thực thành công.

### 5.2. Tại sao Spring Security 6.x / Spring Boot 3.x loại bỏ `WebSecurityConfigurerAdapter`?
- **Lý do:** Trước Spring Boot 3.x, lập trình viên phải kế thừa lớp `WebSecurityConfigurerAdapter` và override hàm `configure(HttpSecurity http)`. Điều này vi phạm nguyên tắc *"Ưu tiên thành phần hơn kế thừa"* (Composition over Inheritance) và biến class cấu hình thành một "God class" cồng kềnh.
- **Cải tiến trong Spring Security 6.x:**
  - Chuyển sang mô hình **Component-based configuration**: Khai báo trực tiếp một `@Bean SecurityFilterChain`.
  - Sử dụng cú pháp **Lambda DSL (`http.csrf(csrf -> csrf.disable()).authorizeHttpRequests(...)`)** giúp code rõ ràng, có cấu trúc phân cấp chặt chẽ, loại bỏ hoàn toàn việc gọi `.and()` nối chuỗi rối rắm của thời kỳ cũ.

### 5.3. `AuthenticationManager` và `AuthenticationProvider` phối hợp xử lý như thế nào?
- Khi người dùng đăng nhập (`POST /login`):
  1. Controller gọi `authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(email, password))`.
  2. `AuthenticationManager` (mặc định là `ProviderManager`) duyệt qua danh sách các `AuthenticationProvider` được đăng ký.
  3. `DaoAuthenticationProvider` nhận nhiệm vụ:
     - Gọi `userDetailsService.loadUserByUsername(email)` để kéo thông tin user và mật khẩu băm từ Database lên.
     - Gọi `passwordEncoder.matches(rawPassword, encodedPasswordFromDb)` để so khớp mật khẩu.
  4. Nếu khớp: Trả về một đối tượng `Authentication` hoàn chỉnh (đã có cờ `authenticated = true` và danh sách Roles).
  5. Nếu sai: Ném ra ngoại lệ `BadCredentialsException`.

---

<div style="page-break-before: always;"></div>

<a id="phase-6-chapter-03"></a>

# Chapter 03: Xác Thực Không Trạng Thái với JWT (JSON Web Token)

---

## 1. JSON Web Token (JWT) là gì?

**JWT** (RFC 7519) là một chuẩn mở định nghĩa phương thức truyền tải thông tin an toàn, nhỏ gọn giữa các bên dưới dạng đối tượng JSON.

Trong kiến trúc Backend hiện đại:
- **Session/Cookie truyền thống**: Server lưu trạng thái đăng nhập vào RAM/Redis. Khi có hàng triệu user hoặc nhiều cụm server (Horizontal Scaling), việc đồng bộ session trở nên phức tạp và tốn tài nguyên.
- **JWT (Stateless)**: Server **không lưu trạng thái phiên**. Thông tin user (Id, Email, Role) được đóng gói trực tiếp vào chuỗi token, ký số bằng mật mã bí mật và giao cho Client lưu giữ. Mỗi request client chỉ cần gửi token kèm theo.

---

## 2. Cấu trúc của chuỗi JWT

Một chuỗi JWT gồm 3 phần được phân tách bằng dấu chấm (`.`):

$$\text{JWT} = \underbrace{\text{Header}}_{\text{Base64Url}} \,.\, \underbrace{\text{Payload}}_{\text{Base64Url}} \,.\, \underbrace{\text{Signature}}_{\text{Mã băm bí mật}}$$

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
\_________________________________/ \____________________________________________________________________/ \____________________________________________/
             Header                                                 Payload                                                     Signature
```

### A. Header
Chứa loại token (`JWT`) và thuật toán ký mã hóa sử dụng (thường là `HS256` hoặc `RS256`):
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### B. Payload (Claims)
Chứa dữ liệu cần truyền tải (Không bao giờ để thông tin nhạy cảm như password vào đây vì ai cũng có thể giải mã Base64 để xem):
- **Registered Claims**: `sub` (Subject - username/id), `iat` (Issued At), `exp` (Expiration Time).
- **Custom Claims**: `role`, `userId`, `permissions`.
```json
{
  "sub": "user@example.com",
  "role": "ROLE_USER",
  "iat": 1690000000,
  "exp": 1690003600
}
```

### C. Signature (Chữ ký điện tử)
Được tạo ra bằng cách lấy:
$$\text{Signature} = \text{HMACSHA256}(\text{Base64Url}(\text{Header}) + "." + \text{Base64Url}(\text{Payload}), \text{SECRET\_KEY})$$
- Nếu kẻ tấn công thay đổi Payload (ví dụ: tự ý sửa `"role": "USER"` thành `"ADMIN"`), chữ ký sẽ không còn khớp với `SECRET_KEY` của Server -> Request bị từ chối ngay lập tức!

---

## 3. Quy trình Access Token & Refresh Token Flow

```
┌──────────────┐                ┌──────────────────────────────┐                ┌──────────────┐
│    Client    │                │        Backend Server        │                │   Database   │
└──────┬───────┘                └──────────────┬───────────────┘                └──────┬───────┘
       │                                       │                                       │
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │ GIAI ĐOẠN 1: ĐĂNG NHẬP & CẤP TOKEN CẶP (ACCESS TOKEN + REFRESH TOKEN)
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │                                       │                                       │
       │ 1. POST /auth/login (email, password) │                                       │
       │ ────────────────────────────────────► │                                       │
       │                                       │ 2. Kiểm tra tài khoản & mật khẩu      │
       │                                       │ ────────────────────────────────────► │
       │                                       │ ◄──────────────────────────────────── │
       │ 3. Trả về Access Token (15 phút)      │                                       │
       │    + Refresh Token (7 ngày)           │                                       │
       │ ◄──────────────────────────────────── │                                       │
       │                                       │                                       │
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │ GIAI ĐOẠN 2: SỬ DỤNG ACCESS TOKEN ĐỂ GỌI API
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │                                       │                                       │
       │ 4. GET /api/v1/orders                 │                                       │
       │    Header: Authorization: Bearer <JWT>│                                       │
       │ ────────────────────────────────────► │ Kiểm tra chữ ký & hạn dùng (exp)     │
       │ 5. 200 OK (Trả về danh sách đơn hàng) │                                       │
       │ ◄──────────────────────────────────── │                                       │
       │                                       │                                       │
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │ GIAI ĐOẠN 3: ACCESS TOKEN HẾT HẠN & DÙNG REFRESH TOKEN ĐỔI TOKEN MỚI
═══════╪═══════════════════════════════════════╪═══════════════════════════════════════╪═══════
       │                                       │                                       │
       │ 6. GET /api/v1/orders (Token hết hạn) │                                       │
       │ ────────────────────────────────────► │ Hạn token < thời gian hiện tại        │
       │ 7. 401 Unauthorized (Token Expired)   │                                       │
       │ ◄──────────────────────────────────── │                                       │
       │                                       │                                       │
       │ 8. POST /auth/refresh-token           │                                       │
       │    Body: { refreshToken: "..." }      │                                       │
       │ ────────────────────────────────────► │ 9. Kiểm tra Refresh Token hợp lệ?    │
       │                                       │ ────────────────────────────────────► │
       │                                       │ ◄──────────────────────────────────── │
       │ 10. Cấp Access Token mới (15 phút)    │                                       │
       │ ◄──────────────────────────────────── │                                       │
       ▼                                       ▼                                       ▼
```

---

## 4. Cài đặt JWT Service với thư viện `jjwt`

Thêm dependency trong `pom.xml`:
```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

### Class `JwtService`:
```java
package com.example.app.security;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.security.Keys;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Service;

import java.security.Key;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

@Service
public class JwtService {

    @Value("${application.security.jwt.secret-key:404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970}")
    private String secretKey;

    @Value("${application.security.jwt.expiration:86400000}") // 1 ngày (ms)
    private long jwtExpiration;

    public String generateToken(UserDetails userDetails) {
        return generateToken(new HashMap<>(), userDetails);
    }

    public String generateToken(Map<String, Object> extraClaims, UserDetails userDetails) {
        return Jwts.builder()
                .setClaims(extraClaims)
                .setSubject(userDetails.getUsername())
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() + jwtExpiration))
                .signWith(getSignInKey(), SignatureAlgorithm.HS256)
                .compact();
    }

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public boolean isTokenValid(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername())) && !isTokenExpired(token);
    }

    private boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    private Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(getSignInKey())
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    private Key getSignInKey() {
        byte[] keyBytes = io.jsonwebtoken.io.Decoders.BASE64.decode(secretKey);
        return Keys.hmacShaKeyFor(keyBytes);
    }
}
```

---

## 5. Xây dựng `JwtAuthenticationFilter`

Bộ lọc này sẽ can thiệp vào từng request để trích xuất Header `Authorization: Bearer <token>`:

```java
package com.example.app.security;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.RequiredArgsConstructor;
import org.springframework.lang.NonNull;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
@RequiredArgsConstructor
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    private final JwtService jwtService;
    private final UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(
            @NonNull HttpServletRequest request,
            @NonNull HttpServletResponse response,
            @NonNull FilterChain filterChain
    ) throws ServletException, IOException {

        final String authHeader = request.getHeader("Authorization");
        final String jwt;
        final String userEmail;

        // 1. Kiểm tra header Authorization có chứa Bearer Token không
        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            filterChain.doFilter(request, response);
            return;
        }

        // 2. Cắt chuỗi lấy Token
        jwt = authHeader.substring(7);
        userEmail = jwtService.extractUsername(jwt);

        // 3. Nếu token hợp lệ và chưa được nạp vào SecurityContext
        if (userEmail != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(userEmail);

            if (jwtService.isTokenValid(jwt, userDetails)) {
                UsernamePasswordAuthenticationToken authToken = new UsernamePasswordAuthenticationToken(
                        userDetails,
                        null,
                        userDetails.getAuthorities()
                );
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

                // 4. Lưu danh tính user vào SecurityContext cho request hiện tại
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        // 5. Chuyển tiếp request cho filter tiếp theo trong chuỗi
        filterChain.doFilter(request, response);
    }
}
```

### Đăng ký Filter vào `SecurityConfig`:
```java
http.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Cấu trúc 3 phần của JWT hoạt động thế nào? Ai có thể đọc được Payload?
Một JWT gồm 3 phần ngăn cách bởi dấu chấm `.` : `header.payload.signature`
1. **Header:** Chứa thuật toán ký (vd: `HS256`, `RS256`) và kiểu token (`JWT`), được mã hóa bằng Base64Url.
2. **Payload:** Chứa thông tin dữ liệu (Claims) như `sub` (userId), `email`, `roles`, `iat` (issued at), `exp` (expiration), cũng được mã hóa bằng Base64Url.
   > ⚠️ **CỰC KỲ QUAN TRỌNG:** Base64Url **KHÔNG PHẢI LÀ MÃ HÓA BẢO MẬT**, nó chỉ là định dạng nén chuỗi! Bất kỳ ai cầm JWT cũng có thể lên trang `jwt.io` giải mã và đọc được 100% nội dung bên trong Payload. Do đó: **TUYỆT ĐỐI KHÔNG BAO GIỜ lưu thông tin nhạy cảm (như mật khẩu, số thẻ tín dụng, số CCCD) vào trong Payload của JWT!**
3. **Signature (Chữ ký điện tử):** Được tạo ra bằng công thức:
   $$\text{Signature} = \text{HMACSHA256}(\text{base64(Header)} + "." + \text{base64(Payload)}, \ \text{SecretKey})$$
   Chữ ký này đảm bảo tính toàn vẹn. Nếu hacker sửa đổi bất kỳ ký tự nào trong Payload (ví dụ sửa role từ `USER` thành `ADMIN`), khi Server dùng SecretKey để tính lại chữ ký sẽ thấy lệch ngay lập tức và từ chối token.

### 4.2. Access Token vs Refresh Token? Vì sao bắt buộc phải dùng cả hai?
- **Access Token:**
  - Thời hạn sống **rất ngắn (15 - 30 phút)**.
  - Gửi kèm trong mọi request gọi API.
  - Nếu bị hacker nghe lén (sniff) đánh cắp, thiệt hại chỉ tồn tại tối đa trong 15-30 phút là token tự hết hạn.
- **Refresh Token:**
  - Thời hạn sống **dài (7 ngày - 30 ngày)**.
  - Lưu an toàn trong Database hoặc HttpOnly Cookie, **chỉ gửi lên duy nhất endpoint `/auth/refresh-token`** khi Access Token đã hết hạn.
- **Tại sao cần cả hai:**
  - Nếu chỉ dùng 1 token sống lâu (30 ngày): Quá nguy hiểm khi bị lộ.
  - Nếu chỉ dùng 1 token sống ngắn (15 phút): Trải nghiệm người dùng cực tệ vì cứ 15 phút lại bị văng ra bắt đăng nhập lại từ đầu.
  - **Sự kết hợp:** Người dùng vừa an toàn tối đa (Access Token hết hạn nhanh) mà vừa có trải nghiệm mượt mà không bị ngắt quãng (Refresh Token âm thầm xin cấp Access Token mới ngầm dưới background).

### 4.3. Làm sao để thu hồi (Revoke / Blacklist / Logout) một JWT khi nó chưa hết hạn?
Vì JWT là Stateless (Server không lưu trạng thái), khi người dùng bấm "Đăng xuất" hoặc "Đổi mật khẩu", token cũ trên máy client vẫn còn hạn và vẫn có thể dùng được. 
- **3 Giải pháp chuẩn thực tế:**
  1. **Dùng Redis Token Blacklist:** Khi user Logout, lấy `jti` (JWT ID) hoặc chuỗi token đó lưu vào Redis với thời gian hết hạn đúng bằng thời gian còn lại của token (`TTL = exp - now`). Tại `JwtAuthenticationFilter`, kiểm tra nếu token có trong Redis Blacklist $\rightarrow$ Chặn ngay `401`. Sau khi token hết hạn, Redis tự động giải phóng RAM.
  2. **Token Rotation với Refresh Token:** Mỗi lần dùng Refresh Token để lấy cặp token mới, Refresh Token cũ sẽ bị vô hiệu hóa ngay lập tức. Nếu phát hiện Refresh Token cũ bị dùng lại $\rightarrow$ Cảnh báo tài khoản bị tấn công và hủy toàn bộ các phiên đăng nhập của user đó.
  3. **Lưu `token_version` trong Database:** Bảng `users` lưu cột `token_version = 1`. Đưa số `1` vào claims của JWT. Khi user đổi mật khẩu hoặc bấm đăng xuất khỏi mọi thiết bị $\rightarrow$ Tăng `token_version` trong DB lên `2`. Các token cũ mang version `1` sẽ tự động bị coi là không hợp lệ khi kiểm tra.

---

<div style="page-break-before: always;"></div>

<a id="phase-6-chapter-04"></a>

# Chapter 04: Phân Quyền Theo Vai Trò (RBAC) & Method Security (@PreAuthorize)

---

## 1. Khái niệm RBAC (Role-Based Access Control)

**RBAC** là mô hình quản lý quyền truy cập hệ thống dựa trên vai trò (Role) của người dùng. Thay vì cấp quyền trực tiếp cho từng cá nhân, quyền hạn (Permission/Privilege) được gán vào Vai trò, và Người dùng được gán một hoặc nhiều vai trò.

```
┌───────────────────────────────────────┐
│           Người dùng (User)           │
│   (Ví dụ: account 'nguyenvana')       │
└───────────────────┬───────────────────┘
                    │
                    │ Được gán (Assigned to)
                    ▼
┌───────────────────────────────────────┐
│        Vai trò (Roles: ROLE_*)        │
│   • ROLE_ADMIN                        │
│   • ROLE_STAFF                        │
│   • ROLE_USER                         │
└───────────────────┬───────────────────┘
                    │
                    │ Bao gồm một tập hợp (Contains)
                    ▼
┌───────────────────────────────────────┐
│  Quyền hạn chi tiết (Authorities)     │
│   • product:read                      │
│   • product:create                    │
│   • product:delete                    │
└───────────────────┬───────────────────┘
                    │
                    │ Dùng để bảo vệ (Secures)
                    ▼
┌───────────────────────────────────────┐
│    Endpoint / Nghiệp vụ (@PreAuth)    │
│   • GET /api/v1/products              │
│   • POST /api/v1/products             │
│   • DELETE /api/v1/products/{id}      │
└───────────────────────────────────────┘
```

---

## 2. Phân biệt Role và Authority trong Spring Security

Spring Security quản lý mọi đặc quyền thông qua interface **`GrantedAuthority`**:

| Thuộc tính | Role (Vai trò) | Authority / Privilege (Quyền chi tiết) |
| :--- | :--- | :--- |
| **Bản chất** | Một tập hợp nhóm nhiều quyền hạn cấp cao. | Quyền thao tác cụ thể trên một đối tượng/tài nguyên. |
| **Quy ước tên gọi**| Bắt buộc có tiền tố **`ROLE_`** khi lưu trong `GrantedAuthority` (ví dụ: `ROLE_ADMIN`, `ROLE_CUSTOMER`). | Tùy biến tự do (ví dụ: `product:read`, `order:delete`, `user:create`). |
| **Cách dùng với HttpSecurity** | `.hasRole("ADMIN")` *(tự động nối prefix `ROLE_`)* | `.hasAuthority("ROLE_ADMIN")` hoặc `.hasAuthority("product:read")` |
| **Cách dùng với `@PreAuthorize`** | `@PreAuthorize("hasRole('ADMIN')")` | `@PreAuthorize("hasAuthority('product:delete')")` |

---

## 3. Phân quyền cấp độ URL (URL-level Security)

Được cấu hình tập trung trong `SecurityFilterChain`:

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .csrf(csrf -> csrf.disable())
        .authorizeHttpRequests(auth -> auth
            // 1. Công khai không cần đăng nhập
            .requestMatchers("/api/v1/auth/**", "/api/v1/public/**").permitAll()

            // 2. Chỉ có Role ADMIN mới được truy cập các đường dẫn quản trị
            .requestMatchers("/api/v1/admin/**").hasRole("ADMIN")

            // 3. Cho phép cả ADMIN hoặc MANAGER
            .requestMatchers(HttpMethod.DELETE, "/api/v1/products/**").hasAnyRole("ADMIN", "MANAGER")

            // 4. Kiểm tra theo Authority cụ thể
            .requestMatchers(HttpMethod.POST, "/api/v1/orders/**").hasAuthority("order:create")

            // 5. Các request còn lại chỉ cần đăng nhập là được
            .anyRequest().authenticated()
        );
    return http.build();
}
```

---

## 4. Phân quyền cấp độ Phương thức (Method-level Security)

Phân quyền ở tầng URL rất hữu ích, nhưng trong các ứng dụng thực tế phức tạp, **Method-level Security** mạnh mẽ và linh hoạt hơn rất nhiều vì cho phép bảo vệ trực tiếp các hàm trong Controller hoặc Service.

### Bước 1: Kích hoạt trong cấu hình
```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity // Kích hoạt @PreAuthorize, @PostAuthorize, @Secured
public class SecurityConfig {
    // ...
}
```

### Bước 2: Sử dụng `@PreAuthorize` với biểu thức SpEL (Spring Expression Language)

```java
@RestController
@RequestMapping("/api/v1/users")
@RequiredArgsConstructor
public class UserController {

    private final UserService userService;

    // 1. Chỉ ADMIN được xem danh sách toàn bộ người dùng
    @GetMapping
    @PreAuthorize("hasRole('ADMIN')")
    public ResponseEntity<List<UserResponseDto>> getAllUsers() {
        return ResponseEntity.ok(userService.findAll());
    }

    // 2. Phải có role ADMIN HOẶC MANAGER
    @PutMapping("/{id}/status")
    @PreAuthorize("hasAnyRole('ADMIN', 'MANAGER')")
    public ResponseEntity<Void> updateUserStatus(@PathVariable Long id, @RequestParam boolean active) {
        userService.updateStatus(id, active);
        return ResponseEntity.noContent().build();
    }

    // 3. Quyền sở hữu dữ liệu (Data Ownership):
    // Người dùng chỉ được sửa thông tin của chính mình, HOẶC nếu là ADMIN thì được sửa bất kỳ ai!
    @PutMapping("/{id}")
    @PreAuthorize("hasRole('ADMIN') or #email == authentication.name")
    public ResponseEntity<UserResponseDto> updateProfile(
            @PathVariable Long id,
            @RequestParam String email,
            @RequestBody UpdateProfileDto dto
    ) {
        return ResponseEntity.ok(userService.update(id, dto));
    }
}
```

---

## 5. Xử lý phản hồi lỗi 403 Forbidden chuẩn mực

Khi một người dùng đã đăng nhập (đã có Token hợp lệ) nhưng không đủ quyền truy cập tài nguyên, Spring Security sẽ ném ra `AccessDeniedException`.

Ta cần tạo một custom `AccessDeniedHandler` để trả về JSON format đồng nhất:

```java
@Component
public class CustomAccessDeniedHandler implements AccessDeniedHandler {

    @Override
    public void handle(
            HttpServletRequest request,
            HttpServletResponse response,
            AccessDeniedException accessDeniedException
    ) throws IOException {
        response.setContentType(MediaType.APPLICATION_JSON_VALUE);
        response.setStatus(HttpServletResponse.SC_FORBIDDEN); // 403

        Map<String, Object> body = new HashMap<>();
        body.put("status", 403);
        body.put("error", "Forbidden");
        body.put("message", "Bạn không có quyền thực hiện hành động này!");
        body.put("path", request.getRequestURI());

        new ObjectMapper().writeValue(response.getOutputStream(), body);
    }
}
```

Đăng ký vào `SecurityFilterChain`:
```java
http.exceptionHandling(ex -> ex
    .accessDeniedHandler(customAccessDeniedHandler)
);
```

---

## 6. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 6.1. Phân biệt `Role` và `Privilege` (Permission) trong thực tế
- **Role (Vai trò / Chức danh):**
  - Là nhóm định danh cấp cao, mang tính bao quát (ví dụ: `ROLE_ADMIN`, `ROLE_MANAGER`, `ROLE_CUSTOMER`).
  - Trong Spring Security: Luôn được gắn tiền tố `ROLE_` ngầm định khi dùng hàm `hasRole("ADMIN")`.
- **Privilege / Permission (Quyền hạn chi tiết - Granular Permission):**
  - Là quyền thực hiện một hành động cụ thể trên một tài nguyên (ví dụ: `user:read`, `user:create`, `order:delete`, `report:export`).
  - Được kiểm tra qua: `hasAuthority("user:delete")`.
- **Mô hình chuẩn thực tế doanh nghiệp:**
  Một `User` có thể có nhiều `Role`, và mỗi `Role` sẽ chứa một danh sách tập hợp các `Privilege`. Khi phân quyền ở mức method, nên kiểm tra theo **`hasAuthority()`** để hệ thống linh hoạt thay đổi quyền cho từng vai trò mà không cần sửa lại code Java.

### 6.2. Phân biệt `AuthenticationEntryPoint` và `AccessDeniedHandler`
| Tiêu chí | `AuthenticationEntryPoint` | `AccessDeniedHandler` |
| :--- | :--- | :--- |
| **Mã lỗi HTTP** | **`401 Unauthorized`** | **`403 Forbidden`** |
| **Khi nào kích hoạt** | Khi người dùng **CHƯA ĐĂNG NHẬP** (thiếu token, token sai hoặc hết hạn) mà cố tình truy cập vào tài nguyên bảo vệ. | Khi người dùng **ĐÃ ĐĂNG NHẬP THÀNH CÔNG** (token chuẩn), nhưng **KHÔNG CÓ QUYỀN** tương ứng để truy cập tài nguyên đó. |
| **Cách xử lý** | Trả về JSON thông báo chưa đăng nhập, nhắc client redirect về trang Login. | Trả về JSON thông báo bị từ chối truy cập do thiếu quyền hạn. |

### 6.3. `@PreAuthorize` vs `@Secured` vs `@RolesAllowed` nên dùng cái nào?
- **`@Secured` (Spring cũ):** Chỉ nhận chuỗi String vai trò đơn giản (ví dụ `@Secured("ROLE_ADMIN")`), không hỗ trợ biểu thức logic, cú pháp hạn chế.
- **`@RolesAllowed` (Chuẩn Java EE/Jakarta JSR-250):** Tương tự `@Secured`, độc lập framework nhưng không có biểu thức logic.
- **`@PreAuthorize` (Chuẩn hiện đại - KHUYÊN DÙNG TUYỆT ĐỐI):**
  - Hỗ trợ đầy đủ ngôn ngữ biểu thức **SpEL (Spring Expression Language)**.
  - Cho phép kết hợp logic phức tạp: `@PreAuthorize("hasRole('ADMIN') or hasAuthority('order:write')")`.
  - Cho phép kiểm tra quyền sở hữu dữ liệu dựa trên tham số hàm:
    `@PreAuthorize("#userId == authentication.principal.id")` (chỉ cho phép user tự sửa thông tin của chính mình).

---

<div style="page-break-before: always;"></div>

<a id="phase-6-chapter-05"></a>

# Chapter 05: Cấu Hình CORS & CSRF Trong REST API

---

## 1. CORS (Cross-Origin Resource Sharing)

### A. Same-Origin Policy (Chính sách cùng nguồn gốc) là gì?
Mặc định, các trình duyệt web (Chrome, Firefox, Safari) áp dụng chính sách **Same-Origin Policy** vì lý do an toàn. Một trang web chỉ được phép gửi request JavaScript (AJAX/Fetch) đến một server khác nếu có **cùng Nguồn (Origin)**:
$$\text{Origin} = \text{Protocol (http/https)} + \text{Domain/Host} + \text{Port}$$

Ví dụ:
- Trang Frontend: `http://localhost:3000` (React/Vue/Angular)
- Server Backend: `http://localhost:8080` (Spring Boot)
- **Khác Port (3000 vs 8080) $\rightarrow$ Khác Origin $\rightarrow$ Trình duyệt tự động chặn kết quả và báo lỗi CORS!**

```text
Access to fetch at 'http://localhost:8080/api/v1/products' from origin 'http://localhost:3000' 
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

---

### B. Cơ chế Preflight Request (HTTP `OPTIONS`)
Khi gửi các request làm thay đổi dữ liệu hoặc có chứa Header tùy biến (như `Authorization: Bearer <token>`):
1. Trình duyệt sẽ tự động bắn một request thăm dò gọi là **Preflight Request** với HTTP method là **`OPTIONS`**.
2. Server Backend phải phản hồi cho phép Origin, Method và Headers đó.
3. Sau khi nhận được sự đồng ý từ Server, trình duyệt mới gửi HTTP Request chính thức (`GET`, `POST`, `PUT`, `DELETE`).

---

### C. Cấu hình CORS chuẩn mực trong Spring Security 6.x

Trong ứng dụng Spring Security, **CorsFilter phải được đặt trước chuỗi xác thực**, cấu hình thông qua `CorsConfigurationSource`:

```java
package com.example.app.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.CorsConfigurationSource;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;

import java.util.List;

@Configuration
public class CorsConfig {

    @Bean
    public CorsConfigurationSource corsConfigurationSource() {
        CorsConfiguration configuration = new CorsConfiguration();

        // 1. Cho phép các Origin của Frontend
        configuration.setAllowedOrigins(List.of("http://localhost:3000", "https://myfrontend.com"));

        // 2. Cho phép các HTTP Methods
        configuration.setAllowedMethods(List.of("GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"));

        // 3. Cho phép các Headers cần thiết
        configuration.setAllowedHeaders(List.of("Authorization", "Content-Type", "X-Requested-With", "Accept"));

        // 4. Cho phép gửi kèm Credentials (Cookies, Auth Headers)
        configuration.setAllowCredentials(true);

        // 5. Cho phép Client đọc các Headers phản hồi
        configuration.setExposedHeaders(List.of("Authorization", "Link", "X-Total-Count"));

        // 6. Thời gian cache kết quả Preflight request (1 giờ)
        configuration.setMaxAge(3600L);

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration);
        return source;
    }
}
```

Kích hoạt trong `SecurityFilterChain`:
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        // Bật CORS sử dụng Bean cấu hình ở trên
        .cors(cors -> cors.configurationSource(corsConfigurationSource()))
        .csrf(csrf -> csrf.disable())
        // ...
        ;
    return http.build();
}
```

---

## 2. CSRF (Cross-Site Request Forgery)

### A. Tấn công CSRF là gì?
**CSRF** là hình thức tấn công mà kẻ gian lừa trình duyệt của nạn nhân gửi một request trái phép đến một website mà nạn nhân đã đăng nhập từ trước:

1. Nạn nhân đăng nhập vào ngân hàng `bank.com`, ngân hàng lưu phiên đăng nhập trong **Cookie**.
2. Nạn nhân vô tình bấm vào link độc của hacker `evil.com`.
3. Trang `evil.com` chạy script âm thầm gửi `POST https://bank.com/transfer?to=hacker&amount=1000`.
4. Trình duyệt tự động đính kèm **Cookie** của `bank.com` theo request $\rightarrow$ Ngân hàng tưởng nạn nhân gửi và thực hiện chuyển tiền!

---

### B. Tại sao trong REST API dùng JWT lại TẮT CSRF (`csrf.disable()`)?

| Kiến trúc | Quản lý phiên | Nguy cơ CSRF | Cấu hình CSRF |
| :--- | :--- | :--- | :--- |
| **Monolith (JSP / Thymeleaf / MVC)** | Dùng **Session ID lưu trong Cookie** do trình duyệt tự động gửi kèm. | **Rất cao** (Bị mạo danh cookie dễ dàng). | **Bắt buộc BẬT** CSRF Token. |
| **REST API + JWT (Stateless)** | Lưu JWT trong **LocalStorage / Memory**, gửi qua header `Authorization: Bearer <token>`. | **Không có nguy cơ CSRF**, vì trình duyệt KHÔNG tự động gắn Header Authorization khi click link lạ! | **TẮT (`csrf.disable()`)** để tránh xung đột không cần thiết. |

> 📌 **Lưu ý ngoại lệ:** Nếu hệ thống của bạn lưu JWT trong **HttpOnly Cookie** thay vì LocalStorage, lúc này bạn **vẫn phải bật bảo vệ CSRF** (bằng cơ chế Double Submit Cookie hoặc SameSite attribute).

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. CORS là cơ chế bảo mật của ai? Server hay Browser?
- **Khẳng định:** CORS là chính sách bảo mật do **TRÌNH DUYỆT (BROWSER)** thực thi (Client-side Security Mechanism), **KHÔNG PHẢI của Server**!
- **Chứng minh:**
  - Nếu bạn dùng Postman, cURL, hoặc code Backend gọi tới một API không cấu hình CORS, request **vẫn chạy thành công 100% và nhận đủ dữ liệu**.
  - Nhưng nếu chạy JavaScript trên trình duyệt (từ `http://localhost:3000` gọi tới `http://localhost:8080`), trình duyệt sẽ kiểm tra Header phản hồi: Nếu không thấy `Access-Control-Allow-Origin`, chính **trình duyệt sẽ chủ động chặn dữ liệu lại** và ném lỗi đỏ lòm trên màn hình Console để bảo vệ người dùng.

### 4.2. Preflight Request (OPTIONS) là gì? Khi nào trình duyệt gửi Preflight Request?
- **Preflight Request:** Là một HTTP request thăm dò với phương thức **`OPTIONS`** do trình duyệt tự động âm thầm gửi lên Server **TRƯỚC KHI** gửi request thật sự.
- **Mục đích:** Hỏi Server: *"Này máy chủ, tôi từ domain này, muốn gửi method PUT/DELETE kèm header Authorization này, máy chủ có cho phép không?"*. Nếu Server trả về mã `200 OK` kèm các header cho phép, trình duyệt mới gửi request chính thức.
- **Khi nào bị kích hoạt Preflight:**
  Khi request **KHÔNG PHẢI là "Simple Request"**:
  1. Dùng các HTTP Method: `PUT`, `DELETE`, `PATCH`.
  2. Dùng Content-Type: `application/json` (Simple request chỉ cho phép `text/plain`, `multipart/form-data`, `application/x-www-form-urlencoded`).
  3. Có đính kèm Custom Headers như `Authorization: Bearer <token>`.

### 4.3. Kịch bản tấn công CSRF (Cross-Site Request Forgery) diễn ra như thế nào?
- **Kịch bản:**
  1. Nạn nhân đăng nhập vào trang ngân hàng `mybank.com`. Ngân hàng cấp một Cookie xác thực lưu trong trình duyệt.
  2. Nạn nhân vô tình mở một tab mới và click vào một đường link độc hại trên trang web lừa đảo `evil.com`.
  3. Trang `evil.com` âm thầm chứa một đoạn mã:
     `<img src="https://mybank.com/api/transfer?toAccount=hacker&amount=10000000" />`
  4. Trình duyệt tự động đính kèm Cookie ngân hàng hợp lệ của nạn nhân vào request chuyển tiền đó.
  5. Ngân hàng nhận được request kèm đúng Cookie của nạn nhân nên tưởng là lệnh thật $\rightarrow$ Chuyển tiền thành công cho hacker!
- **Cách phòng chống:** Dùng **CSRF Token** (mỗi form có 1 token ngẫu nhiên mà trang lạ không thể đọc được), hoặc cấu hình thuộc tính Cookie **`SameSite=Strict`** để cấm trình duyệt gửi cookie khi click từ trang web khác.

---

<div style="page-break-before: always;"></div>

<a id="phase-7"></a>

# PHASE 7: KIỂM THỬ, KIẾN TRÚC SẠCH & VẬN HÀNH DOCKER

---

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-01"></a>

# Chapter 01: Unit Testing với JUnit 5 & Assertions

---

## 1. Unit Testing là gì?

**Unit Test (Kiểm thử đơn vị)** là việc kiểm tra các thành phần nhỏ nhất có thể kiểm thử được của phần mềm (thường là một method hoặc một class) một cách độc lập và cô lập.

### Kim tự tháp kiểm thử (Testing Pyramid):
```
                          ┌───────────────────────────┐
                          │     End-to-End Tests      │  ▲ ÍT NHẤT, CHẬM NHẤT, CHI PHÍ CAO
                          │ (UI / Toàn bộ hệ thống)   │  │ Chạy: vài chục giây - vài phút
                     ┌────┴───────────────────────────┴────┐
                     │          Integration Tests          │  │ TRUNG BÌNH
                     │  (Kiểm thử tích hợp API / DB / Web) │  │ Chạy: vài giây
                ┌────┴─────────────────────────────────────┴────┐
                │                  Unit Tests                   │  │ NHIỀU NHẤT, NHANH NHẤT, CHI PHÍ THẤP
                │ (Kiểm thử cô lập từng Method / Service Logic) │  ▼ Chạy: vài mili-giây
                └───────────────────────────────────────────────┘
```

---

## 2. Mô hình AAA (Arrange - Act - Assert)

Mỗi test case chuẩn mực nên được cấu trúc rõ ràng theo 3 bước:
1. **Arrange (Chuẩn bị)**: Khởi tạo dữ liệu đầu vào, đối tượng và điều kiện tiên quyết.
2. **Act (Hành động)**: Gọi hàm/phương thức cần kiểm thử với dữ liệu đã chuẩn bị.
3. **Assert (Kiểm chứng)**: So sánh kết quả trả về thực tế với kết quả mong đợi.

---

## 3. Các Annotation cốt lõi trong JUnit 5 (Jupiter)

| Annotation | Ý nghĩa |
| :--- | :--- |
| `@Test` | Đánh dấu phương thức là một test case có thể thực thi. |
| `@DisplayName("Mô tả")` | Đặt tên hiển thị trực quan, dễ hiểu trên giao diện chạy test. |
| `@BeforeEach` | Chạy **trước mỗi** `@Test` method (dùng để reset dữ liệu/khởi tạo đối tượng). |
| `@AfterEach` | Chạy **sau mỗi** `@Test` method (dọn dẹp tài nguyên). |
| `@BeforeAll` | Chạy **duy nhất 1 lần trước tất cả** các test methods (phải là `static`). |
| `@AfterAll` | Chạy **duy nhất 1 lần sau tất cả** các test methods (phải là `static`). |
| `@Disabled` | Bỏ qua test case này khi chạy test tự động. |
| `@ParameterizedTest` | Chạy cùng 1 test case với nhiều bộ dữ liệu đầu vào khác nhau (kết hợp `@ValueSource`, `@CsvSource`). |

---

## 4. Các Assertions thông dụng trong JUnit 5

```java
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

class CalculatorTest {

    private final Calculator calculator = new Calculator();

    @Test
    @DisplayName("Cộng hai số nguyên dương chính xác")
    void testAddPositiveNumbers() {
        // Arrange
        int a = 10;
        int b = 20;

        // Act
        int result = calculator.add(a, b);

        // Assert
        assertEquals(30, result, "10 + 20 phải bằng 30");
        assertTrue(result > 0);
    }

    @Test
    @DisplayName("Chia cho 0 phải ném ra ArithmeticException")
    void testDivideByZeroThrowsException() {
        // Kiểm thử ngoại lệ
        ArithmeticException exception = assertThrows(ArithmeticException.class, () -> {
            calculator.divide(10, 0);
        });

        assertEquals("/ by zero", exception.getMessage());
    }

    @Test
    @DisplayName("Kiểm tra nhiều assertions cùng lúc với assertAll")
    void testMultipleProperties() {
        User user = new User("John", 25);

        // assertAll đảm bảo chạy hết mọi assertion dù có một assertion fail
        assertAll("Kiểm tra thông tin user",
            () -> assertEquals("John", user.getName()),
            () -> assertEquals(25, user.getAge()),
            () -> assertNotNull(user)
        );
    }
}
```

---

## 5. Parameterized Tests (Kiểm thử với nhiều bộ dữ liệu)

Giúp giảm trùng lặp code khi kiểm tra cùng một hàm logic với nhiều case khác nhau:

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;
import static org.junit.jupiter.api.Assertions.assertTrue;

class StringUtilsTest {

    @ParameterizedTest
    @ValueSource(strings = {"racecar", "radar", "level", "madam"})
    @DisplayName("Kiểm tra các chuỗi đối xứng (Palindrome)")
    void testIsPalindrome(String word) {
        assertTrue(StringUtils.isPalindrome(word));
    }
}
```

---

## 6. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 6.1. Nguyên tắc F.I.R.S.T trong Unit Testing là gì?
Một bộ Unit Test chất lượng cao bắt buộc phải thỏa mãn 5 tiêu chí **F.I.R.S.T**:
1. **F - Fast (Nhanh):** Test phải chạy trong vài phần nghìn giây. Nếu cả bộ test mất 30 phút, developer sẽ lười chạy test.
2. **I - Independent / Isolated (Độc lập):** Các hàm test không được phụ thuộc vào nhau. Thứ tự chạy test không được ảnh hưởng kết quả. Không chia sẻ trạng thái chung (State).
3. **R - Repeatable (Lặp lại được):** Chạy ở bất kỳ đâu (máy dev, máy tester, hay CI/CD không có mạng) đều phải cho ra cùng một kết quả duy nhất.
4. **S - Self-validating (Tự kiểm chứng):** Test phải tự động trả về `Pass` hoặc `Fail` thông qua các lệnh Assertion, không bắt con người phải tự nhìn log để đoán đúng sai.
5. **T - Timely / Thorough (Kịp thời & Toàn diện):** Viết test song song hoặc trước khi viết code nghiệp vụ (TDD), bao phủ cả các trường hợp biên (Edge cases, Null, Negative numbers).

### 6.2. Cấu trúc 3A (Arrange - Act - Assert) tổ chức một ca kiểm thử thế nào?
Mọi hàm Unit Test chuẩn mực đều được chia thành 3 phần rõ ràng:
```java
@Test
void withdraw_shouldDeductBalance_whenBalanceIsSufficient() {
    // 1. Arrange (Chuẩn bị): Thiết lập dữ liệu đầu vào và trạng thái ban đầu
    BankAccount account = new BankAccount(1000.0);
    double amountToWithdraw = 400.0;

    // 2. Act (Hành động): Kích hoạt phương thức cần kiểm thử
    account.withdraw(amountToWithdraw);

    // 3. Assert (Khẳng định): So sánh kết quả thực tế với kỳ vọng
    assertEquals(600.0, account.getBalance());
}
```

### 6.3. Test Coverage (Độ phủ kiểm thử) là gì? Có nên cố gắng đạt 100% Code Coverage không?
- **Code Coverage:** Là tỷ lệ phần trăm số dòng code (Line Coverage) hoặc nhánh rẽ `if-else` (Branch Coverage) được thực thi trong quá trình chạy bộ test.
- **Có nên chạy theo 100% Coverage?**
  - **KHÔNG NÊN.** 100% Coverage chỉ chứng minh rằng "mọi dòng code đã được đi qua", chứ **KHÔNG HỀ CHỨNG MINH code không có bug logic** (ví dụ bạn gọi hàm nhưng không viết câu `assertEquals()` nào thì coverage vẫn là 100% nhưng test hoàn toàn vô dụng!).
  - **Mục tiêu thực tế:** Mức độ phủ lý tưởng của các dự án Backend chất lượng thường là **75% - 85%**, tập trung 100% cho các **Core Business Logic nhạy cảm** (tính tiền, bảo mật, xử lý giao dịch) và bỏ qua các hàm Getter/Setter, DTO, Config boiler-plate.

---

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-02"></a>

# Chapter 02: Mocking Dependencies Trong Unit Test Với Mockito

---

## 1. Khái niệm Mocking & Tại sao cần Mockito?

Khi viết Unit Test cho tầng **`Service`**, chúng ta chỉ muốn kiểm tra **đúng logic nghiệp vụ của Service đó**.
- Ta **không muốn** kết nối vào Database thật (vì chậm, phụ thuộc dữ liệu có sẵn, làm bẩn DB).
- Ta **không muốn** gọi sang API bên thứ 3 thật (như cổng thanh toán VNPay, gửi SMS, gửi Email).

👉 **Mock** là đối tượng giả lập, bắt chước hành vi của đối tượng thật trong một kịch bản được định nghĩa trước. Thư viện chuẩn mực số 1 trong Java là **Mockito**.

---

## 2. Các Annotation cốt lõi của Mockito

```
┌────────────────────────────────────────────────────────────────────────┐
│                        TEST CLASS (@ExtendWith)                        │
│                                                                        │
│  ┌──────────────────────────────────────────────────────────────────┐  │
│  │    @InjectMocks: Đối tượng thật cần kiểm thử                      │  │
│  │    private UserServiceImpl userService;                          │  │
│  └──────────────────▲──────────────────▲──────────────────▲─────────┘  │
│                     │                  │                  │            │
│                     │ Tự động tiêm     │ Tự động tiêm     │ Tự động    │
│                     │ vào Constructor  │ vào Constructor  │ tiêm vào   │
│                     │                  │                  │            │
│  ┌──────────────────┴──┐    ┌──────────┴─────────┐    ┌───┴─────────┐  │
│  │        @Mock        │    │       @Mock        │    │    @Mock    │  │
│  │   UserRepository    │    │     UserMapper     │    │   Password  │  │
│  │  (Giả lập CSDL)     │    │  (Giả lập Mapper)  │    │   Encoder   │  │
│  └─────────────────────┘    └────────────────────┘    └─────────────┘  │
└────────────────────────────────────────────────────────────────────────┘
```

| Annotation | Mục đích |
| :--- | :--- |
| `@ExtendWith(MockitoExtension.class)` | Khai báo ở đầu test class để kích hoạt các annotation của Mockito. |
| `@Mock` | Tạo đối tượng giả lập rỗng (mọi method gọi vào mặc định trả về `null`, `0`, `false`). |
| `@InjectMocks` | Tạo instance thật của class cần kiểm thử, và tự động tiêm các `@Mock` vào constructor của nó. |
| `@Spy` | Bọc lấy một đối tượng thật; giữ nguyên hành vi gốc ngoại trừ các hàm được can thiệp. |

---

## 3. Cú pháp Stubbing & Verification

### A. Định nghĩa hành vi (Stubbing) với `when().thenReturn()`
```java
// Khi repo được gọi với ID = 1L, hãy trả về Optional chứa user mẫu
Mockito.when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

// Khi gọi với bất kỳ chuỗi email nào, trả về false
Mockito.when(userRepository.existsByEmail(anyString())).thenReturn(false);

// Giả lập ném ra lỗi khi gọi hàm
Mockito.when(userRepository.save(any())).thenThrow(new RuntimeException("Database error"));
```

### B. Kiểm chứng tương tác (Verification) với `verify()`
```java
// Kiểm tra method findById(1L) có được gọi đúng 1 lần không
Mockito.verify(userRepository, Mockito.times(1)).findById(1L);

// Kiểm tra method save() TUYỆT ĐỐI KHÔNG được gọi
Mockito.verify(userRepository, Mockito.never()).save(any());
```

---

## 4. Viết Unit Test hoàn chỉnh cho tầng Service

```java
package com.example.app.service;

import com.example.app.dto.UserRequestDto;
import com.example.app.dto.UserResponseDto;
import com.example.app.entity.UserEntity;
import com.example.app.exception.ResourceNotFoundException;
import com.example.app.repository.UserRepository;
import com.example.app.service.impl.UserServiceImpl;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.security.crypto.password.PasswordEncoder;

import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class UserServiceImplTest {

    @Mock
    private UserRepository userRepository;

    @Mock
    private PasswordEncoder passwordEncoder;

    @InjectMocks
    private UserServiceImpl userService;

    private UserEntity sampleUser;

    @BeforeEach
    void setUp() {
        sampleUser = UserEntity.builder()
                .id(1L)
                .email("test@example.com")
                .password("encoded_pass")
                .fullName("Nguyễn Văn A")
                .build();
    }

    @Test
    @DisplayName("Lấy User theo ID thành công khi ID tồn tại")
    void getUserById_Success() {
        // Arrange
        when(userRepository.findById(1L)).thenReturn(Optional.of(sampleUser));

        // Act
        UserResponseDto result = userService.getUserById(1L);

        // Assert
        assertNotNull(result);
        assertEquals("test@example.com", result.getEmail());
        assertEquals("Nguyễn Văn A", result.getFullName());
        verify(userRepository, times(1)).findById(1L);
    }

    @Test
    @DisplayName("Lấy User theo ID ném ResourceNotFoundException khi ID không tồn tại")
    void getUserById_NotFound_ThrowsException() {
        // Arrange
        when(userRepository.findById(99L)).thenReturn(Optional.empty());

        // Act & Assert
        assertThrows(ResourceNotFoundException.class, () -> {
            userService.getUserById(99L);
        });

        verify(userRepository, times(1)).findById(99L);
    }

    @Test
    @DisplayName("Tạo mới User thành công khi email chưa tồn tại")
    void createUser_Success() {
        // Arrange
        UserRequestDto request = new UserRequestDto("new@gmail.com", "rawPass", "Trần B");
        when(userRepository.existsByEmail("new@gmail.com")).thenReturn(false);
        when(passwordEncoder.encode("rawPass")).thenReturn("hashedPass");
        when(userRepository.save(any(UserEntity.class))).thenReturn(sampleUser);

        // Act
        UserResponseDto response = userService.createUser(request);

        // Assert
        assertNotNull(response);
        verify(userRepository, times(1)).existsByEmail("new@gmail.com");
        verify(passwordEncoder, times(1)).encode("rawPass");
        verify(userRepository, times(1)).save(any(UserEntity.class));
    }
}
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. `@Mock` vs `@Spy` khác nhau thế nào trong Mockito?
| Tiêu chí | `@Mock` (Giả lập hoàn toàn - Dummy) | `@Spy` (Theo dõi / Giả lập một phần - Partial Mock) |
| :--- | :--- | :--- |
| **Bản chất** | Tạo một đối tượng rỗng hoàn toàn bằng bytecode (CGLIB/ByteBuddy). | Bọc bên ngoài một **đối tượng thật sự (Real Object)**. |
| **Hành vi mặc định** | Mọi phương thức khi gọi đều trả về giá trị mặc định (`null`, `0`, `false`) trừ khi bạn chủ động stubbing bằng `when(...)`. | Mọi phương thức sẽ **chạy mã nguồn thật bên trong**, trừ khi bạn chủ động ghi đè hành vi của phương thức đó. |
| **Khi nào dùng** | Dùng cho **95% các trường hợp** (Mock Repository, Mock MailSender, Mock PaymentGateway). | Dùng khi kiểm thử một class tiện ích hoặc một Service cũ mà bạn chỉ muốn can thiệp vào đúng 1 hàm phụ bên trong nó. |

### 4.2. `@Mock` vs `@MockBean` khác nhau thế nào?
- **`@Mock` (Thuần túy Mockito):**
  - Khởi tạo độc lập cực nhanh (vài mili-giây) thông qua `@ExtendWith(MockitoExtension.class)`.
  - Hoàn toàn **không khởi động Spring IoC Container**. Dùng cho các bài **Unit Test** thuần túy ở tầng Service.
- **`@MockBean` (Tích hợp của Spring Boot Test):**
  - Khởi động một phần hoặc toàn bộ **Spring ApplicationContext**.
  - Nó tìm Bean thật trong Spring Context và **thay thế (hoán đổi) Bean đó bằng một Mockito mock**.
  - Dùng trong kiểm thử tích hợp tầng Controller (`@WebMvcTest`) để giả lập Service mà không cần Service thật.

### 4.3. Tại sao nên dùng `ArgumentCaptor`?
- **Vấn đề:** Đôi khi phương thức của bạn gọi `userRepository.save(entity)`, nhưng `entity` này được tạo ra bên trong thân hàm, bạn không có tham chiếu ở ngoài để `assertEquals()`.
- **Giải pháp `ArgumentCaptor`:**
  Cho phép "bắt trộm" chính xác đối tượng đã được truyền vào hàm mock để kiểm tra từng trường dữ liệu:
  ```java
  ArgumentCaptor<UserEntity> userCaptor = ArgumentCaptor.forClass(UserEntity.class);
  verify(userRepository).save(userCaptor.capture());

  UserEntity capturedUser = userCaptor.getValue();
  assertEquals("hashedPass", capturedUser.getPassword());
  assertEquals(Role.USER, capturedUser.getRole());
  ```

---

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-03"></a>

# Chapter 03: Integration Testing Với @SpringBootTest, MockMvc & Testcontainers

---

## 1. Phân biệt Unit Test vs Integration Test

| Tiêu chí | Unit Test (Tầng Service) | Integration Test (Kiểm thử tích hợp) |
| :--- | :--- | :--- |
| **Phạm vi** | 1 hàm duy nhất trong 1 class. | Tương tác giữa nhiều tầng (Controller $\leftrightarrow$ Filter $\leftrightarrow$ Service $\leftrightarrow$ DB). |
| **Spring Context**| **Không load** Spring Context (Chạy siêu nhanh, tính bằng mili-giây). | **Có load** một phần hoặc toàn bộ Spring Context. |
| **Mục đích** | Kiểm tra logic tính toán, rẽ nhánh if/else. | Kiểm tra serialization JSON, routing URL, HTTP status code, validation và transaction. |

---

## 2. Slice Testing cho Tầng Controller với `@WebMvcTest`

Nếu chỉ cần kiểm tra xem Controller có nhận đúng URL, đọc đúng `@PathVariable`, validate đúng `@Valid` và trả về đúng HTTP Status code hay không:
👉 **Không cần load toàn bộ ứng dụng bằng `@SpringBootTest`**. Hãy dùng **`@WebMvcTest`** để chỉ khởi động duy nhất tầng Web (nhanh hơn gấp nhiều lần).

```
┌───────────────────────────┐           ┌───────────────────────────┐           ┌───────────────────────────┐
│          MockMvc          │  1. Gửi   │      UserController       │  2. Gọi   │        @MockBean          │
│   (Giả lập HTTP Client)   │ ────────► │       (@WebMvcTest)       │ ────────► │        UserService        │
│                           │  Request  │                           │  hàm mock │                           │
│ Gửi GET, POST, Header...  │ ◄──────── │ Chỉ khởi động duy nhất    │ ◄──────── │ Trả dữ liệu giả lập sẵn   │
└───────────────────────────┘  4. Trả   │ Web Layer (Nhanh & cô lập)│  3. Trả   └───────────────────────────┘
                               Response └───────────────────────────┘  dữ liệu
```

### Triển khai code kiểm thử Controller với MockMvc:
```java
package com.example.app.controller;

import com.example.app.dto.UserRequestDto;
import com.example.app.dto.UserResponseDto;
import com.example.app.service.UserService;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.mockito.ArgumentMatchers.any;
import static org.mockito.ArgumentMatchers.eq;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserController.class)
@AutoConfigureMockMvc(addFilters = false) // Tạm tắt Spring Security Filters để tập trung test logic Controller
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @MockBean
    private UserService userService;

    @Test
    @DisplayName("GET /api/v1/users/1 trả về 200 OK và đúng dữ liệu JSON")
    void getUserById_ReturnsOk() throws Exception {
        // Arrange
        UserResponseDto mockResponse = new UserResponseDto(1L, "an@gmail.com", "Nguyễn Văn An");
        Mockito.when(userService.getUserById(1L)).thenReturn(mockResponse);

        // Act & Assert
        mockMvc.perform(get("/api/v1/users/1")
                        .accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().contentType(MediaType.APPLICATION_JSON))
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.email").value("an@gmail.com"))
                .andExpect(jsonPath("$.fullName").value("Nguyễn Văn An"));
    }

    @Test
    @DisplayName("POST /api/v1/users với email rỗng phải trả về 400 Bad Request")
    void createUser_InvalidEmail_ReturnsBadRequest() throws Exception {
        // Gửi payload vi phạm @NotBlank hoặc @Email
        UserRequestDto invalidRequest = new UserRequestDto("", "123456", "Nguyễn Văn An");

        mockMvc.perform(post("/api/v1/users")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(invalidRequest)))
                .andExpect(status().isBadRequest());
    }
}
```

---

## 3. Full Integration Test với `@SpringBootTest` & Testcontainers

### A. Vấn đề khi dùng H2 In-Memory Database để test
Nhiều dự án dùng H2 DB để chạy test cho tiện. Tuy nhiên:
- H2 có cú pháp và kiểu dữ liệu khác MySQL/PostgreSQL (ví dụ: JSON column, Full-text search, Stored Procedure).
- Test pass trên H2 nhưng khi deploy lên Production với Postgres/MySQL thì crash!

### B. Giải pháp hiện đại: Testcontainers
**Testcontainers** là thư viện Java cho phép tự động khởi chạy một Docker container chứa Database thật (MySQL, PostgreSQL, Redis, Kafka) ngay khi bắt đầu chạy test, và tự động xóa container khi test hoàn thành.

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@Testcontainers
class FullApplicationIntegrationTest {

    // Tự động kéo Docker image Postgres về và khởi chạy container
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15-alpine");

    @DynamicPropertySource
    static void configureProperties(DynamicPropertyRegistry registry) {
        // Gán tự động URL động của container vào cấu hình Spring
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Test
    @DisplayName("Toàn bộ ứng dụng khởi động và kết nối DB Postgres thật thành công")
    void contextLoads() {
        assertTrue(postgres.isRunning());
    }
}
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. `@WebMvcTest` vs `@SpringBootTest` khác nhau thế nào?
| Tiêu chí | `@WebMvcTest(UserController.class)` (Slice Test) | `@SpringBootTest` (Full Integration Test) |
| :--- | :--- | :--- |
| **Phạm vi khởi động** | **Chỉ khởi động tầng Web** (Controller, ControllerAdvice, Filter, Jackson). Không load Service và Repository. | **Khởi động toàn bộ ApplicationContext** (Toàn bộ Controller, Service, Repository, Database Connection). |
| **Tốc độ thực thi** | Cực nhanh (1 - 2 giây). | Chậm hơn (10 - 30 giây) do phải nạp toàn bộ bean và kết nối DB. |
| **Cách xử lý Service** | Phải dùng `@MockBean` để giả lập tầng Service. | Có thể dùng các Service và Repository thật để kiểm thử toàn luồng từ đầu đến cuối. |
| **Mục đích** | Kiểm tra validation `@Valid`, HTTP status code, format JSON, định tuyến URL của Controller. | Kiểm thử tích hợp toàn diện luồng nghiệp vụ thực tế (End-to-End). |

### 4.2. Tại sao H2 Database ngày nay ít được dùng cho Integration Test? Testcontainers giải quyết gì?
- **Nhược điểm của H2 Database:** H2 là CSDL trong bộ nhớ (In-Memory). Cú pháp SQL, các hàm xử lý chuỗi/ngày tháng, kiểu dữ liệu JSON, cơ chế khóa dòng (Row-level Locking) và phân biệt hoa/thường của H2 **hoàn toàn khác biệt so với MySQL hay PostgreSQL thật**. Rất nhiều trường hợp: *Code chạy Unit Test với H2 thì xanh rờn (Pass), nhưng khi deploy lên Production chạy MySQL thật thì văng lỗi cú pháp SQL và crash!*
- **Lợi ích vượt trội của Testcontainers:**
  - Chạy **Database MySQL/Postgres THẬT 100%** bên trong Docker container cô lập.
  - Tự động sinh cổng ngẫu nhiên (tránh xung đột port).
  - Tự động dọn dẹp và tiêu hủy container sau khi test chạy xong.
  - Đảm bảo môi trường Test và môi trường Production đồng nhất 100%.

### 4.3. Làm sao đảm bảo dữ liệu test không bị "bẩn" (Dirty Data) làm ảnh hưởng tới các ca test khác?
- Sử dụng annotation **`@Transactional` trên class hoặc hàm test**:
  ```java
  @SpringBootTest
  @Transactional // 👈 Phép màu của Spring Test
  class OrderServiceIntegrationTest { ... }
  ```
  - Khi đặt `@Transactional` trong bài test, Spring sẽ tự động **ROLLBACK toàn bộ dữ liệu về trạng thái ban đầu ngay sau khi hàm test kết thúc**, bất kể bài test đó Pass hay Fail!
  - Nhờ đó, Database luôn sạch sẽ và các bài test hoàn toàn độc lập, không làm sai lệch số lượng bản ghi của nhau.

---

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-04"></a>

# Chapter 04: Kiến Trúc Clean Architecture & Design Patterns Trong Spring Boot

---

## 1. Từ Layered Architecture đến Clean Architecture

### A. Kiến trúc 3 tầng truyền thống (Layered Architecture)
Mô hình phổ biến nhất: **Controller $\rightarrow$ Service $\rightarrow$ Repository $\rightarrow$ Database**.
- **Điểm yếu**: Tầng nghiệp vụ (Service) thường bị phụ thuộc chặt chẽ vào Database Entity và các thư viện bên ngoài (JPA, Jackson). Khi thay đổi công nghệ DB hoặc nâng cấp framework, mã nguồn nghiệp vụ cốt lõi bị ảnh hưởng theo.

### B. Clean Architecture (Hexagonal / Ports & Adapters)
Nguyên tắc cốt lõi của Clean Architecture: **Quy tắc phụ thuộc (Dependency Rule)**.
> **Các tầng bên ngoài chỉ được phụ thuộc vào các tầng bên trong, tầng bên trong tuyệt đối KHÔNG ĐƯỢC biết gì về tầng bên ngoài!**

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ 1. FRAMEWORKS & DRIVERS (Tầng Ngoại Vi - Web, DB, Devices, UI, External Interfaces)     │
│    [Web MVC / REST]       [MySQL / Spring Data JPA]       [VNPay / Email Service]      │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │ 2. INTERFACE ADAPTERS (Tầng Chuyển Đổi - Controllers, Gateways, Presenters)      │  │
│  │    [DTOs & Controllers]                    [Repository Implementations / DAOs]   │  │
│  │  ┌────────────────────────────────────────────────────────────────────────────┐  │  │
│  │  │ 3. APPLICATION BUSINESS RULES (Tầng Ứng Dụng - Use Cases / Services)       │  │  │
│  │  │    [CreateUserUseCase]                  [OrderProcessingService]           │  │  │
│  │  │  ┌──────────────────────────────────────────────────────────────────────┐  │  │  │
│  │  │  │ 4. ENTERPRISE BUSINESS RULES (Tầng Cốt Lõi - Domain Entities)        │  │  │  │
│  │  │  │    [Domain Models: User, Order, Product]                             │  │  │  │
│  │  │  │    (Java thuần khiết POJO, KHÔNG phụ thuộc Spring, JPA hay DB)       │  │  │  │
│  │  │  └──────────────────────────────────▲───────────────────────────────────┘  │  │  │
│  │  │                                     │ Phụ thuộc hướng vào tâm            │  │  │
│  │  └─────────────────────────────────────┼────────────────────────────────────┘  │  │
│  │                                        │ (Dependency Rule)                     │  │
│  └────────────────────────────────────────┼───────────────────────────────────────┘  │
│                                           │                                          │
└───────────────────────────────────────────┴──────────────────────────────────────────┘
```

---

## 2. Tổ chức cấu trúc thư mục dự án chuẩn (Package by Feature)

Thay vì gom tất cả Controller vào một thư mục, gom tất cả Service vào một thư mục (`Package by Layer`), các dự án lớn ưu tiên tổ chức theo **Tính năng (Package by Feature)** để tăng tính đóng gói:

```text
src/main/java/com/example/app/
├── common/                     <-- Các tiện ích dùng chung (BaseResponse, Exception, Utils)
│   ├── exception/
│   └── response/
├── config/                     <-- Các file cấu hình Spring (@Configuration, Security, Cors)
└── modules/                    <-- Chia theo nghiệp vụ độc lập
    ├── auth/
    │   ├── controller/
    │   ├── dto/
    │   └── service/
    ├── user/
    │   ├── controller/
    │   ├── dto/
    │   ├── entity/
    │   ├── repository/
    │   └── service/
    └── order/
        ├── controller/
        ├── dto/
        ├── entity/
        ├── repository/
        └── service/
```

---

## 3. Các Design Pattern thực tế phổ biến trong Spring Boot

### Pattern 1: Strategy Pattern (Xử lý đa cổng thanh toán)
Tránh dùng chuỗi `if-else` hoặc `switch-case` dài dòng khi cần xử lý nhiều phương thức thanh toán (`VNPAY`, `MOMO`, `ZALOPAY`).

```java
// 1. Khai báo Strategy Interface
public interface PaymentStrategy {
    PaymentType getType();
    PaymentResult process(BigDecimal amount);
}

// 2. Các Concrete Strategies
@Component
public class VnPayStrategy implements PaymentStrategy {
    @Override
    public PaymentType getType() { return PaymentType.VNPAY; }
    @Override
    public PaymentResult process(BigDecimal amount) {
        // Gọi SDK VNPay...
        return new PaymentResult(true, "Thanh toán VNPay thành công");
    }
}

@Component
public class MomoStrategy implements PaymentStrategy {
    @Override
    public PaymentType getType() { return PaymentType.MOMO; }
    @Override
    public PaymentResult process(BigDecimal amount) {
        // Gọi SDK MoMo...
        return new PaymentResult(true, "Thanh toán MoMo thành công");
    }
}

// 3. Strategy Factory / Manager
@Service
public class PaymentContext {

    private final Map<PaymentType, PaymentStrategy> strategies = new EnumMap<>(PaymentType.class);

    // Spring tự động tiêm tất cả các bean implement PaymentStrategy vào danh sách!
    public PaymentContext(List<PaymentStrategy> strategyList) {
        for (PaymentStrategy strategy : strategyList) {
            strategies.put(strategy.getType(), strategy);
        }
    }

    public PaymentResult executePayment(PaymentType type, BigDecimal amount) {
        PaymentStrategy strategy = strategies.get(type);
        if (strategy == null) {
            throw new IllegalArgumentException("Cổng thanh toán không hỗ trợ: " + type);
        }
        return strategy.process(amount);
    }
}
```

---

### Pattern 2: Event-Driven Pattern với `ApplicationEventPublisher`
Tách rời luồng xử lý chính với các tác vụ phụ trợ (như gửi email xác nhận, cộng điểm thưởng):

```java
// 1. Tạo Sự Kiện (Event)
public record OrderPlacedEvent(Long orderId, String customerEmail, BigDecimal totalAmount) {}

// 2. Phát Sự Kiện từ OrderService
@Service
@RequiredArgsConstructor
public class OrderService {
    private final ApplicationEventPublisher eventPublisher;

    @Transactional
    public void createOrder(OrderRequest request) {
        // Lưu đơn hàng vào DB...
        OrderEntity order = orderRepository.save(newOrder);

        // Bắn sự kiện ra hệ thống (OrderService không cần biết ai lắng nghe)
        eventPublisher.publishEvent(new OrderPlacedEvent(order.getId(), order.getCustomerEmail(), order.getTotal()));
    }
}

// 3. Người Lắng Nghe Sự Kiện (EventListener)
@Component
@Slf4j
public class EmailNotificationListener {

    @EventListener
    @Async // Chạy bất đồng bộ trong background thread, không block luồng tạo đơn hàng!
    public void onOrderPlaced(OrderPlacedEvent event) {
        log.info("Đang gửi email xác nhận đơn hàng #{} tới {}", event.orderId(), event.customerEmail());
        // Gửi email...
    }
}
```

---

## 4. Câu hỏi phỏng vấn thường gặp & Trả lời chi tiết

### 4.1. Quy tắc phụ thuộc (The Dependency Rule) trong Clean Architecture là gì?
- **Nguyên lý bất biến:**
  > *"Chiều của các mũi tên phụ thuộc mã nguồn BẮT BUỘC PHẢI LUÔN HƯỚNG VÀO TRONG (Hướng về trung tâm Domain Entities & Use Cases)."*
- **Ý nghĩa thực tế:**
  - Tầng Domain (Nghiệp vụ cốt lõi) nằm ở tâm: Hoàn toàn trong sáng, **không chứa bất kỳ annotation nào của Spring, Hibernate hay cơ sở dữ liệu**.
  - Tầng ngoài cùng (Frameworks & Drivers: Web Controller, MySQL Database, Redis, REST Client) phải phụ thuộc vào Domain.
  - Tầng Domain **không bao giờ được biết đến sự tồn tại của Database hay Framework**. Nhờ đó, bạn có thể thay thế Database từ PostgreSQL sang MongoDB, đổi Spring Boot sang Quarkus mà toàn bộ Logic nghiệp vụ trung tâm vẫn nguyên vẹn 100%.

### 4.2. Khác biệt giữa Package-by-Layer và Package-by-Feature? Dự án lớn nên chọn gì?
- **Package-by-Layer (Chia theo tầng kỹ thuật):**
  - Cấu trúc: `com.app.controller`, `com.app.service`, `com.app.repository`.
  - Nhược điểm: Khi dự án có 50 tính năng, thư mục `service/` sẽ có 50 file chen chúc nhau. Muốn sửa tính năng "Đặt hàng", bạn phải nhảy qua 5 package khác nhau.
- **Package-by-Feature (Chia theo mô-đun nghiệp vụ):**
  - Cấu trúc: `com.app.order` (chứa `OrderController`, `OrderService`, `OrderRepository`), `com.app.user`, `com.app.payment`.
  - Ưu điểm: Đóng gói tính năng độc lập, dễ dàng chuyển đổi sang kiến trúc **Microservices** sau này khi dự án phình to.
  - **Khuyên dùng:** Các dự án lớn trong thực tế **luôn ưu tiên Package-by-Feature**.

### 4.3. Lợi ích của Event-Driven Pattern nội bộ (`ApplicationEventPublisher`) so với việc gọi trực tiếp Service?
- **Nếu gọi trực tiếp (`OrderService` tự gọi `emailService.sendEmail()`):**
  - `OrderService` bị dính chặt (Tightly coupled) với `EmailService`.
  - Nếu gửi email bị chậm 3 giây hoặc sập mạng, toàn bộ API tạo đơn hàng của khách hàng sẽ bị chậm 3 giây hoặc bị lỗi theo!
- **Khi dùng Event-Driven:**
  - `OrderService` chỉ việc lưu đơn hàng và bắn ra `OrderPlacedEvent` rồi kết thúc trong 50ms.
  - `EmailNotificationListener` lắng nghe sự kiện và chạy `@Async` ở background thread độc lập.
  - Sau này nếu bạn muốn làm thêm tính năng: "Cộng điểm tích lũy" hay "Bắn thông báo qua Telegram", bạn chỉ cần viết thêm `BonusPointsListener` mới mà **hoàn toàn không cần sửa 1 dòng code nào trong `OrderService`** (Tuân thủ chuẩn Open/Closed Principle).

---

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-05"></a>

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

<div style="page-break-before: always;"></div>

<a id="phase-7-chapter-06"></a>

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

<div style="page-break-before: always;"></div>

<a id="phu-luc-cheat-sheet"></a>

# PHỤ LỤC: BẢNG TRA CỨU NHANH TRẢ LỜI PHỎNG VẤN SENIOR (CHEAT SHEET)

| Câu hỏi phỏng vấn cốt lõi | Điểm mấu chốt trả lời trong 30 giây |
| :--- | :--- |
| **Java là Pass-by-value hay Pass-by-reference?** | 100% là **Pass-by-value**. Khi truyền đối tượng (Object), giá trị được sao chép chính là bản sao của địa chỉ tham chiếu trỏ vào vùng nhớ Heap. |
| **Vì sao String trong Java lại bất biến (Immutable)?** | Đảm bảo an toàn vùng nhớ (String Pool tái sử dụng), an toàn đa luồng (Thread-safety), an toàn dữ liệu nhạy cảm (Username/Password/Socket) và giữ hash code bất biến khi dùng làm Key trong HashMap. |
| **Sự khác nhau giữa `==` và `.equals()`?** | `==` so sánh địa chỉ ô nhớ (2 con trỏ có trỏ cùng ô nhớ không). `.equals()` so sánh nội dung logic giữa các đối tượng. |
| **Giải thích cơ chế giải quyết xung đột trong HashMap?** | Sử dụng mảng Buckets kết hợp Separate Chaining (Linked List). Khi 1 bucket có từ 8 phần tử trở lên và mảng có ít nhất 64 buckets, danh sách liên kết sẽ tự động chuyển thành Cây Đỏ-Đen (Red-Black Tree) để tối ưu thời gian tìm kiếm từ O(n) về O(log n). |
| **Nguyên lý PECS trong Java Generics là gì?** | Producer Extends, Consumer Super. Cần đọc dữ liệu từ Collection (Producer) dùng `? extends T`; cần thêm/ghi dữ liệu vào Collection (Consumer) dùng `? super T`. |
| **Phân biệt `PUT` và `PATCH` trong RESTful API?** | `PUT` dùng để ghi đè/thay thế toàn bộ tài nguyên (Idempotent). `PATCH` dùng để cập nhật từng phần (Partial Update) một hoặc một số thuộc tính. |
| **DispatcherServlet đóng vai trò gì trong Spring MVC?** | Là Front Controller trung tâm, tiếp nhận mọi HTTP Request, tra cứu HandlerMapping để định tuyến đến Controller xử lý tương ứng, điều phối dữ liệu và trả Response về Client. |
| **Cách khắc phục bài toán N+1 Queries trong Hibernate/JPA?** | Sử dụng `JOIN FETCH` trong JPQL, sử dụng `@EntityGraph`, hoặc dùng DTO Projection để gộp thành 1 truy vấn SQL duy nhất. |
| **Khi nào `@Transactional` không tự động Rollback?** | Khi ngoại lệ xảy ra là **Checked Exception** (mà không chỉ định `rollbackFor = Exception.class`), hoặc khi gọi hàm nội bộ (Self-invocation) trong cùng một Bean do bỏ qua Spring AOP Proxy. |
| **Cấu trúc JSON Web Token (JWT) gồm mấy phần?** | 3 phần phân tách bởi dấu chấm: Header (thuật toán mã hoá), Payload (dữ liệu claims), Signature (chữ ký số dùng Secret Key để chống sửa đổi dữ liệu). |
| **Multi-stage build trong Docker đem lại lợi ích gì cho Spring Boot?** | Tách riêng môi trường build (cần Maven và JDK nặng) khỏi môi trường chạy (chỉ cần JRE siêu nhẹ), giúp giảm dung lượng image từ ~800MB xuống ~150MB và tăng tối đa tính bảo mật. |

---

*Chúc bạn học tập hiệu quả, in ấn thuận tiện và thành công trên con đường trở thành Java Backend Developer!* 

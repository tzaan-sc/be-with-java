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
*Thực hành:* Dùng `EXPLAIN ANALYZE SELECT * FROM users WHERE email = '...'` trong MySQL để xem câu query có đang dùng Index hay bị Full Table Scan.

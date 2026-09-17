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

## 4. Câu hỏi phỏng vấn
1. Clustered vs Non-clustered Index?
2. Khi nào KHÔNG nên tạo Index?
3. Chuẩn hoá 1NF, 2NF, 3NF là gì?

---

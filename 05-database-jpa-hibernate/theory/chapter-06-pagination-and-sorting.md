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
*Thực hành:* Viết API phân trang dùng `Pageable`, dùng Postman test thử truyền tham số `?page=0&size=5&sort=name,asc`.

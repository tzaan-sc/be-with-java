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
*Thực hành:* Bật `spring.jpa.show-sql: true` trong console để đếm số lượng câu query, viết `JOIN FETCH` để thấy số câu query giảm từ $1+N$ về còn duy nhất 1.

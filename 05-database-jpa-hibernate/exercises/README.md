# 🛠 Bài Tập Thực Hành – Phase 5: Database & JPA / Hibernate

> Lộ trình Ngày 73 – Ngày 92 (20‑30 phút/ngày). Thực hành trực tiếp trên IDE và Database (MySQL / PostgreSQL).

---

## Bài tập Ngày 73‑75: Entity & Mapping căn bản *(Chapter 01 & 02)*

### Bài 1.1 – Cấu hình Datasource & Kiểm tra kết nối *(~20p)*
[ ] Thêm dependency `spring-boot-starter-data-jpa` và driver MySQL/PostgreSQL vào `pom.xml`.
[ ] Cấu hình kết nối cơ sở dữ liệu trong `src/main/resources/application.yml`:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/shop_db?createDatabaseIfNotExist=true&useSSL=false
    username: root
    password: rootpassword
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
```
[ ] Chạy ứng dụng và quan sát log khởi động xem Hibernate đã kết nối thành công chưa.

### Bài 1.2 – Ánh xạ Entity `UserEntity` *(~25p)*
[ ] Tạo class `UserEntity` trong package `entity`:
  - Khóa chính: `@Id`, `@GeneratedValue(strategy = GenerationType.IDENTITY)` cho `Long id`.
  - Cột `email`: `@Column(nullable = false, unique = true, length = 100)`.
  - Cột `fullName`: `@Column(name = "full_name", nullable = false, length = 100)`.
  - Cột `password`: `@Column(nullable = false)`.
  - Cột `role`: Enum `Role { USER, ADMIN }` với `@Enumerated(EnumType.STRING)`.
  - Cột `status`: `@Column(name = "is_active")` boolean mặc định `true`.
  - Tự động ghi nhận thời gian: `@CreationTimestamp LocalDateTime createdAt;` và `@UpdateTimestamp LocalDateTime updatedAt;`.
[ ] Chạy ứng dụng, mở MySQL Workbench / DBeaver kiểm tra xem table `users` và các index unique đã được tự động sinh ra đúng chuẩn chưa.

---

## Bài tập Ngày 76‑78: Spring Data JPA Repository & Query *(Chapter 04)*

### Bài 2.1 – JpaRepository CRUD cơ bản *(~15p)*
[ ] Tạo interface `UserRepository extends JpaRepository<UserEntity, Long>`.
[ ] Viết `CommandLineRunner` hoặc Test để thử các method dựng sẵn:
  - `userRepository.save(user)`: Lưu mới 2 user mẫu.
  - `userRepository.findById(1L)`: Đọc và in thông tin ra console.
  - `userRepository.findAll()`: Lấy toàn bộ danh sách.
  - `userRepository.existsById(1L)`: Kiểm tra tồn tại.

### Bài 2.2 – Derived Query Methods *(~20p)*
[ ] Bổ sung các query method vào `UserRepository`:
  - `Optional<UserEntity> findByEmail(String email);`
  - `List<UserEntity> findByFullNameContainingIgnoreCase(String keyword);`
  - `boolean existsByEmail(String email);`
  - `List<UserEntity> findByRoleAndStatus(Role role, boolean status);`
[ ] Chạy gọi hàm và quan sát terminal để xem Hibernate tự động sinh ra câu lệnh SQL `WHERE email = ?`, `WHERE LOWER(full_name) LIKE ?`.

### Bài 2.3 – JPQL & Native Query *(~20p)*
[ ] Viết câu truy vấn JPQL tìm user hoạt động:
```java
@Query("SELECT u FROM UserEntity u WHERE u.email = :email AND u.status = true")
Optional<UserEntity> findActiveUserByEmail(@Param("email") String email);
```
[ ] Viết câu Native Query đếm số lượng user theo từng role:
```java
@Query(value = "SELECT role, COUNT(*) FROM users GROUP BY role", nativeQuery = true)
List<Object[]> countUsersByRole();
```
[ ] Tự giải thích: JPQL dùng tên Class/Thuộc tính Java (`UserEntity`, `status`), còn Native Query dùng tên bảng/cột vật lý trong DB (`users`, `is_active`).

---

## Bài tập Ngày 79‑82: Thiết lập Quan hệ Bảng *(Chapter 03)*

### Bài 3.1 – Thiết kế quan hệ `@OneToMany` & `@ManyToOne` *(~30p)*
[ ] Tạo 2 Entity có quan hệ 1-N: `CategoryEntity` (1) và `ProductEntity` (N):
  - `CategoryEntity`: `id`, `name`, `code`.
  - `ProductEntity`: `id`, `name`, `price`, `description`.
[ ] Thiết lập mapping:
  - Trong `ProductEntity` (Owning Side - nơi giữ Khóa Ngoại):
    ```java
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "category_id", nullable = false)
    private CategoryEntity category;
    ```
  - Trong `CategoryEntity` (Inverse Side):
    ```java
    @OneToMany(mappedBy = "category", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<ProductEntity> products = new ArrayList<>();
    ```
[ ] Viết helper method hai chiều trong `CategoryEntity`:
  ```java
  public void addProduct(ProductEntity product) {
      products.add(product);
      product.setCategory(this);
  }
  ```

### Bài 3.2 – Thực hành Cascade & OrphanRemoval *(~20p)*
[ ] Tạo 1 Category và thêm 2 Product vào list bằng `addProduct()`.
[ ] Gọi duy nhất lệnh `categoryRepository.save(category);`.
[ ] Kiểm tra DB: Xác nhận cả Category và 2 Product đều được tự động lưu nhờ `CascadeType.ALL`.
[ ] Thử xóa 1 Product khỏi danh sách `category.getProducts().remove(0);` và save lại: Xác nhận product đó bị xóa khỏi DB nhờ `orphanRemoval = true`.

### Bài 3.3 – Kiểm chứng Lazy Loading *(~15p)*
[ ] Gọi `productRepository.findById(productId)`.
[ ] Quan sát log console SQL: Thấy Hibernate chỉ `SELECT` từ bảng `products`, chưa JOIN hay SELECT từ bảng `categories`.
[ ] Gọi tiếp `product.getCategory().getName()`: Quan sát lúc này Hibernate mới phát sinh thêm câu lệnh SELECT lấy Category.

---

## Bài tập Ngày 83‑84: Xử lý bài toán N+1 Query *(Chapter 04)*

### Bài 4.1 – Tái hiện lỗi N+1 Query kinh điển *(~20p)*
[ ] Chèn dữ liệu mẫu gồm 5 Category, mỗi Category có 3 Product.
[ ] Viết hàm lấy toàn bộ Category và in tên sản phẩm của từng Category:
```java
List<CategoryEntity> categories = categoryRepository.findAll(); // 1 query
for (CategoryEntity c : categories) {
    System.out.println(c.getProducts().size()); // Mỗi vòng lặp bắn thêm 1 query -> N query!
}
```
[ ] Đếm tổng số câu query xuất hiện trên log console (1 + 5 = 6 queries).

### Bài 4.2 – Khắc phục triệt để bằng `JOIN FETCH` *(~15p)*
[ ] Bổ sung method tối ưu trong `CategoryRepository`:
```java
@Query("SELECT DISTINCT c FROM CategoryEntity c LEFT JOIN FETCH c.products")
List<CategoryEntity> findAllWithProducts();
```
[ ] Chạy lại logic in sản phẩm và quan sát log: Xác nhận chỉ còn **duy nhất 1 câu SQL** dùng `LEFT OUTER JOIN`.

---

## Bài tập Ngày 85‑86: Quản lý giao dịch với `@Transactional` *(Chapter 05)*

### Bài 5.1 – Kiểm chứng tính nguyên tử (Atomicity & Rollback) *(~25p)*
[ ] Xây dựng kịch bản chuyển tiền giữa 2 tài khoản ngân hàng (`AccountEntity`):
```java
@Service
@RequiredArgsConstructor
public class BankService {
    private final AccountRepository accountRepository;

    @Transactional(rollbackFor = Exception.class)
    public void transfer(Long fromId, Long toId, BigDecimal amount) {
        Account from = accountRepository.findById(fromId).orElseThrow();
        Account to = accountRepository.findById(toId).orElseThrow();

        from.setBalance(from.getBalance().subtract(amount));
        accountRepository.save(from);

        // Giả lập sự cố xảy ra giữa chừng
        if (amount.compareTo(BigDecimal.valueOf(1000000)) > 0) {
            throw new RuntimeException("Giao dịch vượt hạn mức cho phép!");
        }

        to.setBalance(to.getBalance().add(amount));
        accountRepository.save(to);
    }
}
```
[ ] Chạy test case chuyển 2,000,000đ: Xác nhận ngoại lệ xảy ra và tiền của tài khoản `fromId` **không hề bị trừ** (đã Rollback thành công).

---

## Bài tập Ngày 87‑88: Phân trang (Pagination) & Sắp xếp (Sorting) *(Chapter 06)*

### Bài 6.1 – Phân trang Product API *(~25p)*
[ ] Bổ sung API tìm kiếm và phân trang sản phẩm trong `ProductController`:
```java
@GetMapping
public ResponseEntity<Page<ProductResponseDto>> getProducts(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(defaultValue = "createdAt") String sortBy,
    @RequestParam(defaultValue = "desc") String direction
) {
    Sort sort = direction.equalsIgnoreCase("asc") ? Sort.by(sortBy).ascending() : Sort.by(sortBy).descending();
    Pageable pageable = PageRequest.of(page, size, sort);
    Page<ProductResponseDto> result = productService.getAllProducts(pageable);
    return ResponseEntity.ok(result);
}
```
[ ] Dùng Postman test các query param: `?page=0&size=5&sortBy=price&direction=desc`.
[ ] Kiểm tra các thông số trả về: `totalElements`, `totalPages`, `content`.

---

## Bài tập Ngày 89‑92: Tối ưu Index & Dự án CRUD Database hoàn chỉnh

### Bài 7.1 – Đánh Index tối ưu hóa truy vấn *(~15p)*
[ ] Khai báo Index cho các cột thường xuyên dùng trong `WHERE` và `ORDER BY`:
```java
@Table(name = "products", indexes = {
    @Index(name = "idx_product_category", columnList = "category_id"),
    @Index(name = "idx_product_price", columnList = "price")
})
```
[ ] Chạy lệnh `SHOW INDEX FROM products;` trong DB client để kiểm tra index đã được tạo.

### Bài 7.2 – Hoàn thiện CRUD gắn kết Database *(~30p)*
[ ] Chuyển đổi toàn bộ logic quản lý Product/Category từ In-Memory sang sử dụng Spring Data JPA Repository.
[ ] Đảm bảo có đầy đủ Validation đầu vào và Global Exception Handling đã làm ở Phase 4.
[ ] Kiểm tra toàn bộ 5 API CRUD trên Postman: Tạo Category -> Thêm Product vào Category -> Lấy danh sách phân trang -> Cập nhật giá -> Xóa.

---
*Hoàn thành = Sẵn sàng cho Phase 6: Spring Security & JWT Authentication! 🛡️*

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

## 6. Câu hỏi phỏng vấn
1. Page vs Slice khác nhau thế nào? Khi nào dùng Slice?
2. Phân trang ảnh hưởng performance thế nào khi offset lớn (deep pagination)?

---

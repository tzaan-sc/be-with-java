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

## 5. Câu hỏi phỏng vấn
1. Derived Query Method hoạt động thế nào?
2. JPQL khác Native SQL thế nào?
3. N+1 Problem là gì? Cách giải quyết?

---

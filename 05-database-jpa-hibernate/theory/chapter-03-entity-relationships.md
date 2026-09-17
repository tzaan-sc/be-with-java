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

## 5. Câu hỏi phỏng vấn
1. `mappedBy` dùng để làm gì?
2. Lazy vs Eager loading? Tại sao nên mặc định LAZY?
3. CascadeType.ALL có nguy hiểm không? Khi nào không nên dùng?

---

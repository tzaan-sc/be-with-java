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
*Thực hành:* Tạo mối quan hệ 2 chiều giữa `Category` (One) và `Product` (Many), nhớ dùng `mappedBy` và đặt `fetch = FetchType.LAZY`.

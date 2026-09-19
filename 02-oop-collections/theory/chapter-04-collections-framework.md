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
*Thực hành:* Dùng ArrayList, HashSet, HashMap thao tác CRUD. Test trùng lặp trong Set. Duyệt Map bằng entrySet().

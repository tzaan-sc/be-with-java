# Chapter 03: Networking, IP, Port & DNS

## 1. Địa chỉ IP & Port
- **IP (Internet Protocol) address** là địa chỉ duy nhất cho mỗi thiết bị trên mạng.
  - IPv4: 32‑bit, dạng `192.168.0.1` (≈ 4,3 tỷ địa chỉ).
  - IPv6: 128‑bit, dạng `2001:0db8:85a3:0000:0000:8a2e:0370:7334` (không còn lo hết địa chỉ).
- **Port** là số hiệu 0‑65535 dùng để phân biệt các dịch vụ trên cùng một IP.
  - Port 80 → HTTP, 443 → HTTPS, 3306 → MySQL, 5432 → PostgreSQL, 8080 → Tomcat/Spring Boot.
- Khi client muốn gọi API, nó sẽ **kết nối tới `IP:Port`** của server.

## 2. TCP vs UDP
| Thuộc tính | TCP | UDP |
|------------|-----|-----|
| Kết nối | Three‑way handshake (đảm bảo giao tiếp ổn định) | Không kết nối, gửi gói độc lập |
| Độ tin cậy | Đảm bảo thứ tự, retransmission nếu mất gói | Không bảo guarantee, tốc độ cao |
| Ứng dụng | Web (HTTP/HTTPS), email, file transfer | Streaming video, VoIP, DNS query |

## 3. DNS (Domain Name System)
- DNS dịch **tên miền** (`example.com`) thành **địa chỉ IP**.
- Quy trình (simplified):
  1. Browser hỏi **resolver** cục bộ (OS). 
  2. Nếu không có cache, resolver gửi query tới **root server** → **TLD server** → **Authoritative server**.
  3. Trả về **A record** (IPv4) hoặc **AAAA record** (IPv6).
- Các record phổ biến:
  - `A` – IPv4 address
  - `AAAA` – IPv6 address
  - `CNAME` – alias
  - `MX` – mail exchange
  - `TXT` – custom text (SPF, DKIM)
- **TTL (Time‑to‑Live)** quyết định thời gian cache, ảnh hưởng tới **propagation** khi thay đổi DNS.

## 4. Công cụ kiểm tra (CLI)
```bash
# Ping – kiểm tra khả năng reachability
ping google.com        # gửi ICMP Echo Request

# nslookup – tra cứu DNS
nslookup example.com

# dig – chi tiết hơn (Linux/macOS)
dig +short example.com

# traceroute – theo dõi hops tới đích
tracert 8.8.8.8      # Windows
traceroute 8.8.8.8   # Linux/macOS
```
- `ping` cho biết **latency** (ms).
- `nslookup`/`dig` hiển thị **record**, **TTL**, **server** trả lời.
- `traceroute` cho biết **đường truyền** qua các router.

## 5. Ví dụ thực tế – Gọi API Backend
```http
GET /api/v1/products HTTP/1.1
Host: api.example.com   # DNS sẽ chuyển thành IP (e.g., 203.0.113.12)
Port: 443               # HTTPS, SSL/TLS trên TCP
```
- Trình duyệt đầu tiên giải DNS, nhận IP, thiết lập **TCP handshake** tới `203.0.113.12:443`, sau đó tiến hành **TLS handshake** và gửi **HTTP request**.

## 6. Câu hỏi phỏng vấn thường gặp
- IPv4 và IPv6 khác nhau như thế nào? lợi ích của IPv6?
- Khi một API chậm, làm sao kiểm tra vấn đề là do **DNS resolution**, **network latency**, hay **server processing**?
- Giải thích **TCP 3‑way handshake** chi tiết (SYN, SYN‑ACK, ACK).
- Tại sao DNS caching quan trọng? TTL ảnh hưởng thế nào đến thay đổi IP?
- Khi muốn **load‑balance** các service, bạn có thể dùng **DNS round‑robin**? Nhược điểm?

---
*Thực hành:* Dùng `nslookup api.example.com` để xem IP và TTL; dùng `ping` đo latency; dùng `tracert` kiểm tra hops.

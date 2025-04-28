---
title: "Viết blog đầu tiên về Hệ thống phân tán"
date: "2025-04-28"
updated: "2023-04-28"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/image.png"
coverWidth: 16
coverHeight: 9
excerpt: Bài viết này giới thiệu tổng quan về hệ thống phân tán.
---
# Hệ Thống Phân Tán

## Tóm tắt

Bài viết này giới thiệu tổng quan về **hệ thống phân tán**: khái niệm, ứng dụng, các thuật ngữ quan trọng, ví dụ thực tế, kiến trúc phổ biến và tham khảo từ các nguồn đáng tin cậy.

---

## 1. Hệ thống phân tán là gì?

**Hệ thống phân tán** là tập hợp nhiều máy tính độc lập, kết nối với nhau thông qua mạng và phối hợp để hoạt động như một hệ thống duy nhất đối với người dùng cuối.

---

## 2. Các ứng dụng của hệ thống phân tán

- **Điện toán đám mây**: AWS, Azure, Google Cloud.
- **Chia sẻ file**: BitTorrent, Dropbox.
- **Trò chơi trực tuyến**: Fortnite, World of Warcraft.
- **Hệ thống thanh toán điện tử**: Blockchain (Bitcoin, Ethereum).
- **Mạng xã hội**: Facebook, Twitter.
- **IoT (Internet of Things)**: Nhà thông minh, lưới điện thông minh.

---

## 3. Các khái niệm chính

### Scalability
Khả năng mở rộng hệ thống để xử lý lượng tải tăng lên, bằng cách thêm tài nguyên (node mới) hoặc nâng cấp phần cứng.

### Fault Tolerance
Khả năng tiếp tục hoạt động ngay cả khi một số thành phần gặp lỗi.

### Availability
Khả năng hệ thống luôn sẵn sàng phục vụ ngay cả trong trường hợp có sự cố.

### Transparency
Ẩn đi sự phức tạp của hệ thống phân tán, khiến nó trông như một hệ thống duy nhất.

### Concurrency
Nhiều tiến trình hoặc người dùng có thể truy cập và xử lý dữ liệu cùng lúc.

### Parallelism
Chia nhỏ công việc và xử lý song song để tăng tốc độ thực thi.

### Openness
Hệ thống hỗ trợ mở rộng, tích hợp dễ dàng thông qua các chuẩn mở.

### Vertical Scaling
Mở rộng bằng cách nâng cấp phần cứng của máy hiện có (CPU, RAM...).

### Horizontal Scaling
Mở rộng bằng cách thêm nhiều máy mới vào hệ thống.

### Load Balancer
Cân bằng tải truy cập giữa nhiều máy chủ để tránh tình trạng quá tải.

### Replication
Sao chép dữ liệu hoặc dịch vụ ra nhiều máy chủ khác nhau để đảm bảo an toàn và hiệu năng.

---

## 4. Ví dụ thực tế

Giả sử xây dựng một **trang thương mại điện tử**:

- **Load Balancer** phân phối yêu cầu đến nhiều Web Server.
- Các Web Server truy cập vào các bản sao **Database Replicas** (Replication).
- Nếu một Server gặp sự cố, hệ thống vẫn tiếp tục phục vụ (Fault Tolerance, Availability).
- Người dùng không nhận ra server nào xử lý yêu cầu (Transparency).
- Hệ thống thực thi các giao dịch đồng thời (Concurrency, Parallelism).
- Khi nhu cầu tăng cao, ta có thể nâng cấp phần cứng (Vertical Scaling) hoặc thêm Server mới (Horizontal Scaling).
- Toàn bộ hệ thống thiết kế theo các giao thức mở để dễ dàng mở rộng và tích hợp thêm dịch vụ (Openness).

---

## 5. Kiến trúc hệ thống phân tán

Một số mô hình kiến trúc tiêu biểu:

- **Client-Server**: Máy khách gửi yêu cầu, máy chủ xử lý.
- **Peer-to-Peer (P2P)**: Các node hoạt động đồng thời như client và server.
- **Microservices Architecture**: Hệ thống chia thành nhiều dịch vụ nhỏ độc lập (ví dụ: Netflix).
- **Layered Architecture**: Phân lớp (presentation, business logic, data layer).
- **Event-Driven Architecture**: Hệ thống dựa trên cơ chế sự kiện và message bus.
- **Data-Centric Architecture**: Tập trung vào quản lý dữ liệu (ví dụ: Apache Ignite).
- **Shared-Nothing Architecture**: Mỗi node độc lập về CPU, RAM, Disk (thường dùng trong NoSQL, Big Data).





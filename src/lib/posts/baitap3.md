---
title: "Trao đổi thông tin"
date: "2025-11-28"
updated: "2025-11-5"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/comunicate.png"
coverWidth: 16
coverHeight: 9
excerpt:  Trao đổi thông tin trong ứng dụng phân tán.
---






# Bài 1: Giới thiệu về RabbitMQ

## 1. RabbitMQ là gì?
RabbitMQ là một hệ thống message broker mã nguồn mở, hỗ trợ giao tiếp giữa các dịch vụ bằng cách gửi và nhận thông điệp thông qua hàng đợi (queue).

## 2. Cơ chế hoạt động:
* **Producer:** Gửi thông điệp.
* **Exchange:** Phân phối thông điệp theo các loại (direct, fanout, topic).
* **Queue:** Hàng đợi lưu trữ tạm thời các thông điệp.
* **Consumer:** Nhận và xử lý thông điệp từ queue.

## 3. Chức năng chính:
* Giao tiếp phi đồng bộ giữa các dịch vụ.
* Tăng hiệu suất và mở rộng hệ thống dễ dàng.
* Đảm bảo tính bền vững của dữ liệu (durability, ack, retry).

---

# Bài 2: Link Git

Link Git: [Đây là link](https://github.com/nhanlanguoi/Rabbitmq)

---

# Bài 3: Remote Procedure Call (RPC) với jsonrpc4j

## 1. Giới thiệu về RPC
Remote Procedure Call (RPC) là cơ chế cho phép một chương trình gọi một thủ tục (hàm) trên một máy khác như thể nó đang gọi một hàm nội bộ. RPC giúp giao tiếp giữa các hệ thống phân tán trở nên đơn giản và trừu tượng hóa việc gửi nhận dữ liệu.

## 2. Định dạng JSON trong RPC
Trong các hệ thống hiện đại, RPC thường được kết hợp với định dạng JSON để truyền dữ liệu vì:
* Dễ đọc, dễ debug.
* Phổ biến, được hỗ trợ bởi hầu hết các ngôn ngữ.
* Tối ưu cho giao tiếp qua HTTP/REST.

## 3. Thư viện được chọn: jsonrpc4j
jsonrpc4j là một thư viện mã nguồn mở trong Java, hỗ trợ triển khai JSON-RPC 2.0 một cách đơn giản. Nó cho phép tạo client và server RPC sử dụng JSON làm định dạng dữ liệu.

**Tính năng nổi bật:**
* Tuân thủ JSON-RPC 2.0.
* Hỗ trợ dễ dàng tích hợp với Spring Boot.
* Có thể dùng với HTTP hoặc trực tiếp qua Java Socket.

## 4. Demo hệ thống JSON-RPC sử dụng jsonrpc4j

### 4.1. Cài đặt thư viện
Thêm dependency vào `pom.xml`:
```xml
<dependency>
    <groupId>com.github.briandilley</groupId>
    <artifactId>jsonrpc4j</artifactId>
    <version>1.5.0</version>
</dependency>
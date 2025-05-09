---
title: "Deliverable"
date: "2025-05-9"
updated: "2025-05-9"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/image_copy.png"
coverWidth: 16
coverHeight: 9
excerpt:  Deliverable.
---




# 1. Mục đích của thư viện được giao, thư viện có thể giải quyết vấn đề gì, điểm yếu, điểm mạnh, so sánh với các thư viện framework khác. Ứng dụng

## Hệ thống quản lý đơn hàng đa cửa hàng

### Mục đích

- Quản lý dữ liệu phân tán trên nhiều node
- Hỗ trợ truy vấn kiểu SQL (YQL)
- Đảm bảo tính nhất quán cao (ACID) kể cả trong môi trường đa node
- Hỗ trợ transaction phân tán và khả năng mở rộng mạnh mẽ

### Trong hệ thống phân tán, có các thách thức:

- Một đơn hàng có thể được xử lý bởi nhiều chi nhánh/kho hàng
- Tồn kho thay đổi theo từng khu vực
- Tránh tình trạng đặt hàng khi hết hàng do race condition
- Cần lưu lịch sử đơn hàng, hoàn tiền, đồng bộ real-time với hệ thống bán hàng

### YDB giải quyết được:

- Tính nhất quán cao (ACID) → không xảy ra mất dữ liệu khi thao tác đơn hàng
- Transaction phân tán → xử lý đơn hàng từ nhiều kho vẫn chính xác
- Mở rộng dễ dàng khi số lượng đơn hàng và chi nhánh tăng
- Truy vấn linh hoạt với YQL → thống kê nhanh lịch sử, hàng tồn, doanh thu

### Điểm mạnh:

- Giúp thao tác chính xác giữa các kho, đơn hàng
- Xử lý khối lượng đơn hàng lớn
- Không mất đơn hàng khi hệ thống gặp sự cố

### Điểm yếu:

- Cộng đồng nhỏ
- Không phổ biến cho sinh viên

# 2. Nộp kế hoạch dự kiến về bài giữa kỳ. Sử dụng vào bài toán gì.

## Tên dự án: Hệ thống quản lý đơn hàng đa cửa hàng

### Mục tiêu:

Xây dựng một hệ thống cho phép khách hàng:

- Đặt hàng từ nhiều chi nhánh khác nhau
- Hỗ trợ theo dõi trạng thái đơn hàng
- Quản lý tồn kho theo từng chi nhánh
- Cung cấp lịch sử giao dịch, thanh toán và hoàn trả minh bạch

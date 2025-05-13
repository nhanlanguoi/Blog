---
title: "Định danh"
date: "2025-04-28"
updated: "2025-05-5"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/imagedinhdanh.png"
coverWidth: 16
coverHeight: 9
excerpt:  Định danh.
---






# Bài tập 1: Diễn giải quy trình duyệt một trang web www.motvidu.com.

# 🕸️ Quy trình duyệt web tổng quát

## 1. Người dùng nhập URL
Bạn gõ "www.motvidu.com" vào trình duyệt.

## 2. Trình duyệt phân tích URL
Trình duyệt tách URL thành các thành phần:
- Giao thức: `http` hoặc `https`
- Tên miền: `www.motvidu.com`
- Đường dẫn (nếu có)

## 3. Tra cứu DNS (DNS Lookup)

### Mục đích
Trình duyệt cần tìm địa chỉ IP tương ứng với tên miền vì máy tính giao tiếp qua địa chỉ IP, không phải tên miền.

### Các bước tra cứu DNS:
- **Kiểm tra cache trình duyệt** – nếu đã từng truy cập, IP có thể được lưu lại.
- **Kiểm tra cache hệ điều hành (OS)**
- **Kiểm tra cache router**
- **Gửi truy vấn đến DNS Resolver** – thường do ISP cung cấp hoặc các DNS công cộng như:
  - Google DNS (`8.8.8.8`)
  - Cloudflare DNS (`1.1.1.1`)

## 4. Resolving DNS (Phân giải DNS)

### Quá trình truy vấn đệ quy:
1. **DNS Resolver** gửi truy vấn nếu cache không có kết quả.
2. **Root Server**: trả về địa chỉ của TLD Server cho `.com`.
3. **TLD Server**: trả về địa chỉ của **Authoritative Name Server** cho `motvidu.com`.
4. **Authoritative Name Server**: trả về địa chỉ IP cho `www.motvidu.com`.

## 5. DNS Caching (Bộ nhớ đệm DNS)

### Mục đích
Tăng tốc độ và giảm tải hệ thống DNS.

### Các cấp độ cache:
- **Trình duyệt:** Lưu tạm thời.
- **Hệ điều hành:** Lưu lâu hơn một chút.
- **DNS Resolver:** Lưu theo giá trị `TTL`.

### Time-To-Live (TTL)
Giá trị thời gian (số giây) mà kết quả DNS có thể được lưu trước khi phải truy vấn lại.

## 6. Thiết lập kết nối TCP/IP
Trình duyệt dùng địa chỉ IP đã có để thiết lập kết nối TCP (Three-way Handshake) với máy chủ web.

## 7. Gửi yêu cầu HTTP/HTTPS
Trình duyệt gửi HTTP/HTTPS request (thường là `GET`) kèm theo:
- Phiên bản HTTP
- User-Agent
- Cookie (nếu có), v.v.

## 8. Máy chủ web xử lý yêu cầu
Máy chủ phản hồi lại trình duyệt:
- **Mã trạng thái:** `200 OK`, `404 Not Found`, v.v.
- **Headers**
- **Nội dung trang:** HTML, CSS, JS, hình ảnh, v.v.

## 9. Trình duyệt hiển thị trang web
- Trình duyệt dựng DOM từ HTML.
- Tải các tài nguyên CSS, JS, hình ảnh…
- Áp dụng CSS để định dạng giao diện.
- Thực thi JavaScript cho tương tác.
- Hiển thị nội dung cho người dùng.

## 10. Đóng kết nối
Sau khi tài nguyên tải xong, kết nối TCP có thể được đóng hoặc giữ để tái sử dụng (HTTP Keep-Alive).

---

## 🔍 Tóm tắt nhanh

- **DNS Lookup:** Tìm địa chỉ IP từ tên miền, ưu tiên từ cache.
- **DNS Resolving:** Resolver truy vấn đệ quy đến Root, TLD và Authoritative server để lấy IP.
- **DNS Caching:** Lưu trữ kết quả DNS ở nhiều cấp để tăng tốc độ truy cập. Thời gian lưu phụ thuộc vào TTL.

---

## 🔗 Nguồn tham khảo

- **Cloudflare:** [What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
- **Google Cloud:** [Tổng quan về DNS](https://cloud.google.com/dns/docs/overview?hl=vi)
- **Mozilla MDN Web Docs:** [How the Web works](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/How_the_Web_works)
- **Wikipedia:** [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)


**3. Code thực nghiệm (Python)**

# [tại đây](https://github.com/namnguyenit/Smart_Park)
---
title: "Deliverable 3"
date: "2025-5-28" # Lưu ý: Định dạng ngày có thể không hợp lệ (tháng 18?), bạn có thể cần sửa lại.
updated: "2025-5-28" # Tương tự, kiểm tra lại định dạng ngày.
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/kientruchpt.png"
coverWidth: 16
coverHeight: 9
excerpt:  Deliverable 3
---




## 9. Tóm Tắt Tiến Độ Dự Án và Demo

Phần này cung cấp một cái nhìn tổng quan về những gì đã đạt được trong dự án "Quản Lý Tiệm Tạp Hóa" cho đến thời điểm hiện tại, những thách thức gặp phải và cách giải quyết, cùng với minh họa hoạt động của hệ thống.

### 9.1. Tóm tắt tiến độ dự án

**Những gì đã hoàn thành:**

* **Kiến trúc Microservices:** Đã thiết kế và triển khai nền tảng kiến trúc microservices với hai service chính: `branch-service` và `warehouse-service`.
* **Giao diện người dùng cơ bản:** Ba giao diện người dùng (Admin UI, Branch Manager UI, Branch POS UI) đã được xây dựng bằng HTML, CSS, và JavaScript thuần, cho phép thực hiện các chức năng cốt lõi.
* **Chức năng Quản lý Chi nhánh:** `branch-service` cùng với `Branch Manager UI` cho phép thực hiện các thao tác CRUD (Tạo, Đọc, Cập nhật, Xóa) đối với thông tin chi nhánh. Dữ liệu chi nhánh được lưu trữ trong PostgreSQL.
* **Chức năng Quản lý Sản phẩm và Tồn kho:** `warehouse-service` kết hợp với `Admin UI` cho phép quản lý sản phẩm, bao gồm thông tin cơ bản và tồn kho tại các chi nhánh. `Branch POS UI` có thể truy vấn sản phẩm và thực hiện giảm tồn kho khi bán hàng. Dữ liệu sản phẩm và tồn kho được lưu trữ và tìm kiếm bằng Elasticsearch.
* **Triển khai bằng Docker:** Toàn bộ hệ thống (frontend, backend, databases) được đóng gói và có thể triển khai bằng Docker Compose, tạo điều kiện cho việc thiết lập môi trường nhất quán.
* **Giao tiếp phân tán:**
    * Frontend UIs giao tiếp với các Backend Services qua HTTP/REST API bằng Fetch API.
    * `branch-service` giao tiếp với PostgreSQL qua JDBC.
    * `warehouse-service` giao tiếp với cụm Elasticsearch qua client của Elasticsearch.
* **Replication dữ liệu với Elasticsearch:** Cụm Elasticsearch gồm 3 node được thiết lập, cho phép tự động sharding và replication dữ liệu sản phẩm, tăng cường khả năng chịu lỗi và sẵn sàng của dữ liệu kho hàng.
* **Logging cơ bản:** Các backend service ghi log ra console, có thể truy cập qua `docker logs`.

**Những phần đang phát triển/cần cải thiện:**

* **Xác thực và Phân quyền:** Chưa triển khai. Đây là ưu tiên hàng đầu cho giai đoạn tiếp theo.
* **Fault Tolerance cho PostgreSQL và Application Services:** Hiện tại PostgreSQL và các backend service đang chạy dưới dạng single instance.
* **Monitoring và Logging tập trung:** Giải pháp hiện tại còn đơn giản. Cần tích hợp các công cụ chuyên dụng như Prometheus, Grafana, Elasticsearch Exporter, và giải pháp logging tập trung (ví dụ: ELK).
* **Stress Test:** Chưa thực hiện.

**Những vấn đề hoặc thử thách đã gặp phải và cách giải quyết:**

* **Vấn đề:** Cấu hình ban đầu cho cụm Elasticsearch 3 node trong Docker Compose để các node có thể "nhìn thấy" nhau và tạo thành cluster.
    * **Giải pháp:** Đảm bảo cấu hình đúng `cluster.initial_master_nodes` và `discovery.seed_hosts` trong `docker-compose.yml` cho từng node Elasticsearch, đồng thời sử dụng cùng một `cluster.name` và mạng Docker chung.
* **Vấn đề:** CORS (Cross-Origin Resource Sharing) khi các frontend UI (chạy trên các port khác nhau) gọi đến API backend.
    * **Giải pháp:** Cấu hình CORS trên các backend service. `BranchController` sử dụng `@CrossOrigin(origins = "*")` và `WarehouseController` sử dụng `@CrossOrigin` với danh sách các origin cụ thể, đồng thời có `WebConfig` để cấu hình CORS toàn cục cho các API.

* **Vấn đề:** Đảm bảo thứ tự khởi động các service phụ thuộc trong Docker Compose (ví dụ: service backend chỉ khởi động sau khi database sẵn sàng).
    * **Giải pháp:** Sử dụng `depends_on` kết hợp với `healthcheck` trong `docker-compose.yml` để kiểm soát thứ tự và điều kiện khởi động của các container.

### 9.2. Demo hoạt động của hệ thống


**Mô tả các kịch bản demo chính:**

1.  **Demo Quản lý Chi nhánh (Branch Manager UI & Branch Service):**
    * Truy cập `Branch Manager UI` (`http://localhost:8002`).
    * Thêm một chi nhánh mới (ví dụ: Mã CN_TEST, Tên Test Branch).
    * Xem chi nhánh vừa tạo trong danh sách.
    * Sửa thông tin chi nhánh đó.
    * Xóa chi nhánh.
    * *(Minh họa giao tiếp: Mở Developer Tools của trình duyệt để xem các request API đến `http://localhost:8081/api/branches`)*.

2.  **Demo Quản lý Sản phẩm (Admin UI & Warehouse Service):**
    * Truy cập `Admin UI` (`http://localhost:8000`).
    * Thêm sản phẩm mới (ví dụ: SP_DEMO, Tên Demo Product, Giá gốc 10000), đồng thời thêm tồn kho cho sản phẩm này tại CN_TEST (ví dụ: SL 50, Giá bán 12000).
    * Xem sản phẩm vừa tạo trong danh sách, kiểm tra thông tin tồn kho tại CN_TEST.
    * Sửa thông tin sản phẩm và tồn kho của nó.
    * *(Minh họa giao tiếp: Mở Developer Tools để xem các request API đến `http://localhost:8080/api/warehouse/products`)*.

3.  **Demo Bán Hàng (Branch POS UI, Branch Service & Warehouse Service):**
    * Truy cập `Branch POS UI` cho chi nhánh CN_TEST (ví dụ: `http://localhost:8003/pos/CN_TEST`).
    * Hệ thống hiển thị thông tin chi nhánh CN_TEST (lấy từ `Branch Service`).
    * Hệ thống hiển thị sản phẩm SP_DEMO với số lượng tồn kho là 50 (lấy từ `Warehouse Service`).
    * Thực hiện thao tác "Bán" 5 sản phẩm SP_DEMO.
    * Kiểm tra thông báo thành công và số lượng tồn kho của SP_DEMO giảm xuống còn 45.
    * *(Minh họa giao tiếp: Mở Developer Tools để xem request đến `Branch Service` để lấy thông tin chi nhánh, sau đó là các request đến `Warehouse Service` để lấy sản phẩm và cập nhật tồn kho)*.

4.  **Demo Replication/Sharding của Elasticsearch (Gián tiếp):**
    * *(Phần này khó demo trực tiếp qua UI nếu không có công cụ chuyên dụng như Kibana Dev Tools hoặc xem log của Elasticsearch).*
    * Mô tả: Sau khi thêm sản phẩm, dữ liệu được ghi vào cụm Elasticsearch 3 node. Dữ liệu này được sharded và replicated tự động. Nếu một node (ví dụ `es01`) bị dừng, hệ thống (cụ thể là `Warehouse Service`) vẫn có thể truy vấn và ghi dữ liệu sản phẩm thông qua các node còn lại (`es02`, `es03`) nhờ cơ chế replica và leader election của Elasticsearch.
    * Để demo, có thể thử dừng một container Elasticsearch (ví dụ `docker stop es01`) và sau đó thử truy cập các chức năng liên quan đến sản phẩm trên Admin UI hoặc POS UI để xem hệ thống có còn hoạt động không (lưu ý cấu hình client của `warehouse-service` phải trỏ đến nhiều node trong cụm).

### 9.3. Mã nguồn (Code Snippets)

*(Bạn đã yêu cầu chèn các đoạn code và giải thích vào các mục chi tiết ở trên. Các đoạn code đã được đánh dấu placeholder ở các mục 3.1, 3.2, và 7.1. Vui lòng tham khảo lại các mục đó để điền phần giải thích cho các đoạn code cụ thể).*

Dưới đây là một số ví dụ bổ sung về các đoạn code quan trọng:

* **Cấu hình `docker-compose.yml` cho một service (ví dụ `warehouse-service`):**
    ```yaml
    # Trích từ docker-compose.yml
    warehouse-service:
      build:
        context: ./warehouse-service
        dockerfile: Dockerfile
      container_name: warehouse_service_compose
      ports:
        - "8080:8080" # Map cổng 8080 của container ra cổng 8080 của host
      depends_on: # Khởi động sau khi các service này healthy
        es01:
          condition: service_healthy
        es02:
          condition: service_healthy
        es03:
          condition: service_healthy
        branch-service: # Giả sử có thể có tương tác trong tương lai
          condition: service_healthy
      environment: # Biến môi trường cho service
        - SPRING_ELASTICSEARCH_URIS=http://es01:9200,http://es02:9200,http://es03:9200
        - SERVER_PORT=8080
      networks: # Kết nối vào mạng chung
        - tiemtaphoa-network
      restart: unless-stopped # Tự khởi động lại nếu gặp lỗi
    ```
    **Chú thích:** Đoạn cấu hình này định nghĩa cách `warehouse-service` được build, các cổng được expose, các service phụ thuộc, biến môi trường (quan trọng là `SPRING_ELASTICSEARCH_URIS` trỏ đến cụm ES), mạng kết nối và chính sách khởi động lại.



### 9.4. Danh sách tính năng đã hoàn thành (Tóm lược từ mục 9.1)

* **Giao tiếp phân tán giữa các thành phần:**
    * Đã triển khai giao tiếp HTTP/REST giữa 3 Frontend UIs và 2 Backend Services.
    * **Ví dụ hoạt động:** Khi người dùng trên `Branch POS UI` (`http://localhost:8003`) thực hiện bán một sản phẩm tại chi nhánh "CN_HCM_1", UI này sẽ:
        1.  Gửi request đến `Branch Service` (`http://localhost:8081/api/branches/by-code/CN_HCM_1`) để xác nhận thông tin chi nhánh.
        2.  Sau đó, gửi request đến `Warehouse Service` (`http://localhost:8080/api/warehouse/products/inventory/decrement`) với payload chứa `productId`, `branchId: "CN_HCM_1"`, và số lượng bán.
    * **Mục tiêu đạt được:** Các thành phần độc lập có thể giao tiếp qua mạng (trong trường hợp này là mạng Docker nội bộ) để hoàn thành một nghiệp vụ.

* **Chia sẻ/Truy cập dữ liệu giữa các thành phần:**
    * `Branch Service` quản lý và cung cấp dữ liệu chi nhánh cho `Branch Manager UI` và `Branch POS UI`.
    * `Warehouse Service` quản lý và cung cấp dữ liệu sản phẩm/tồn kho cho `Admin UI` và `Branch POS UI`.
    * **Ví dụ hoạt động:** `Admin UI` thêm sản phẩm và tồn kho cho chi nhánh "CN_HN_1" thông qua `Warehouse Service`. Sau đó, khi `Branch POS UI` của chi nhánh "CN_HN_1" được tải, nó sẽ gọi đến `Warehouse Service` để lấy danh sách sản phẩm và hiển thị đúng thông tin tồn kho mà Admin đã nhập.
    * **Mục tiêu đạt được:** Dữ liệu được quản lý tập trung bởi service chuyên trách và được các service/UI khác truy cập khi cần thiết.

* **Sao chép (Replication) dữ liệu:**
    * Đã triển khai cho dữ liệu sản phẩm/tồn kho thông qua cụm Elasticsearch 3 node.
    * **Ví dụ hoạt động:** Khi `Warehouse Service` ghi một sản phẩm mới vào Elasticsearch, dữ liệu này (primary shard) sẽ được lưu trên một node và các bản sao (replica shards) của nó sẽ được Elasticsearch tự động tạo và phân bổ trên 2 node còn lại. Nếu node chứa primary shard gặp sự cố, một replica sẽ được chọn làm primary mới, đảm bảo `Warehouse Service` vẫn có thể đọc/ghi dữ liệu sản phẩm.
    * **Mục tiêu đạt được:** Tăng tính sẵn sàng và khả năng chịu lỗi cho dữ liệu quan trọng của kho hàng.

* **Xử lý lỗi cơ bản:**
    * Các controller trong backend service (ví dụ: `BranchController`, `WarehouseController`) có các khối `try-catch` để bắt các `IllegalArgumentException` từ service layer và trả về `ResponseEntity.badRequest()` hoặc `ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)` kèm thông điệp lỗi.
    * Frontend JavaScript có các khối `try-catch` khi gọi Fetch API và hiển thị thông báo lỗi cơ bản cho người dùng.
    * **Ví dụ hoạt động:** Khi `Branch POS UI` cố gắng bán một số lượng sản phẩm lớn hơn số lượng tồn kho, `ProductService` trong `Warehouse Service` sẽ ném ra `IllegalArgumentException("Không đủ hàng...")`. `WarehouseController` sẽ bắt lỗi này và trả về HTTP 400 Bad Request với message lỗi. `Branch POS UI` sẽ nhận được phản hồi lỗi này và hiển thị thông báo cho nhân viên.
    * **Mục tiêu đạt được:** Hệ thống có khả năng thông báo lỗi một cách cơ bản cho người dùng và không bị sập hoàn toàn khi có lỗi nghiệp vụ dự kiến.

* **Triển khai tự động hóa cơ bản bằng Docker Compose:**
    * Toàn bộ hệ thống có thể được khởi chạy bằng một lệnh `docker-compose up -d`.
    * **Ví dụ hoạt động:** Chạy lệnh `docker-compose up -d` trong thư mục gốc của dự án sẽ tự động build các image cần thiết (nếu chưa có hoặc có thay đổi trong Dockerfile) và khởi tạo tất cả các container (PostgreSQL, Elasticsearch cluster, 2 backend services, 3 frontend UIs) với cấu hình mạng và volume đã định sẵn.
    * **Mục tiêu đạt được:** Đơn giản hóa quá trình thiết lập môi trường và triển khai hệ thống cho mục đích phát triển và thử nghiệm.
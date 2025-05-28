---
title: "Deliverable 2"
date: "2025-5-28" # Lưu ý: Định dạng ngày có thể không hợp lệ (tháng 18?), bạn có thể cần sửa lại.
updated: "2025-5-28" # Tương tự, kiểm tra lại định dạng ngày.
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/kientruchpt.png"
coverWidth: 16
coverHeight: 9
excerpt:  Deliverable 2
---








# 1. Bản vẽ kiến trúc hệ thống

![ảnh ở đây](/images/System_Architecture_Diagram.png)




# 2. Mô tả chi tiết các thành phần trong hệ thống 

Phần này sẽ đi sâu vào vai trò của từng thành phần chính trong hệ thống "Quản Lý Tiệm Tạp Hóa", cách chúng tương tác, và các cơ chế phân tán dữ liệu được áp dụng.

---

## 2.1. Các Thành phần Chính và Vai Trò

### • Giao diện Người dùng (Frontend UIs):

* **Admin UI (`admin.html`):** Là giao diện web cho quản trị viên hệ thống.
    * **Vai trò:** Cung cấp các công cụ để quản lý toàn bộ danh mục sản phẩm, giá cả, và quan trọng nhất là quản lý tồn kho sản phẩm tại các chi nhánh khác nhau.
    * **Tương tác:** Tương tác trực tiếp với Warehouse Service thông qua API HTTP/REST để gửi yêu cầu tạo, đọc, cập nhật, xóa (CRUD) dữ liệu sản phẩm và tồn kho.

* **Branch Manager UI (`managerbranch.html`):** Giao diện web dành cho người quản lý từng chi nhánh cụ thể.
    * **Vai trò:** Cho phép quản lý thông tin chi tiết của một chi nhánh, bao gồm tạo mới, cập nhật thông tin (địa chỉ, tên, trạng thái hoạt động), và xóa chi nhánh.
    * **Tương tác:** Giao tiếp với Branch Service qua API HTTP/REST.

* **Branch POS UI (`branch.html`):** Giao diện Điểm Bán Hàng (Point of Sale) cho nhân viên tại các chi nhánh.
    * **Vai trò:** Hỗ trợ nhân viên xem sản phẩm có sẵn tại chi nhánh, giá bán, số lượng tồn và thực hiện giao dịch bán hàng.
    * **Tương tác:** Khi bán hàng, giao diện này sẽ gửi yêu cầu cập nhật (giảm) số lượng tồn kho đến Warehouse Service. Nó cũng tương tác với Branch Service để kiểm tra thông tin và trạng thái hoạt động của chi nhánh hiện tại.

### • Dịch vụ Backend (Microservices):

* **Branch Service:**
    * **Vai trò:** Là microservice chịu trách nhiệm hoàn toàn cho việc quản lý dữ liệu của các chi nhánh (thông tin, trạng thái). Nó cung cấp các API HTTP/REST để các frontend (chủ yếu là Branch Manager UI và Branch POS UI) có thể thực hiện thao tác CRUD trên dữ liệu chi nhánh.
    * **Hoạt động:** Service này sử dụng Spring Boot và Spring Data JPA để tương tác với cơ sở dữ liệu PostgreSQL. Khi nhận yêu cầu từ API, controller sẽ gọi đến service layer để xử lý logic nghiệp vụ (ví dụ, kiểm tra mã chi nhánh đã tồn tại chưa) và sau đó repository sẽ thực hiện thao tác với database.

* **Warehouse Service:**
    * **Vai trò:** Là microservice quản lý toàn bộ thông tin sản phẩm, bao gồm mô tả, giá gốc, danh mục, và quan trọng là dữ liệu tồn kho chi tiết của từng sản phẩm tại mỗi chi nhánh. Nó cung cấp API HTTP/REST cho Admin UI (quản lý sản phẩm) và Branch POS UI (xem sản phẩm, bán hàng).
    * **Hoạt động:** Service này sử dụng Spring Boot và Spring Data Elasticsearch để lưu trữ và truy vấn dữ liệu sản phẩm/tồn kho trong cụm Elasticsearch. Các yêu cầu API được controller tiếp nhận, chuyển qua service layer để xử lý logic (ví dụ: tính toán lại tồn kho khi bán hàng, đảm bảo số lượng bán không vượt quá tồn kho) và cuối cùng là tương tác với Elasticsearch thông qua repository.

### • Cơ sở dữ liệu:

* **PostgreSQL (cho Branch Service):**
    * **Vai trò:** Lưu trữ dữ liệu có cấu trúc và quan hệ của các chi nhánh. Do tính chất dữ liệu của chi nhánh (thông tin cố định, cần tính nhất quán cao), PostgreSQL là lựa chọn phù hợp.
    * **Hoạt động:** Branch Service sử dụng JDBC (thông qua Spring Data JPA) để kết nối và thực hiện các truy vấn SQL (SELECT, INSERT, UPDATE, DELETE) tới database PostgreSQL được định nghĩa trong `docker-compose.yml` với tên `postgres-db`.

* **Elasticsearch Cluster (cho Warehouse Service):**
    * **Vai trò:** Lưu trữ dữ liệu sản phẩm và thông tin tồn kho đa dạng tại các chi nhánh. Elasticsearch được chọn vì khả năng tìm kiếm mạnh mẽ (ví dụ: tìm sản phẩm theo tên, mô tả), linh hoạt trong cấu trúc dữ liệu (cho phép trường `branchesInventory` là một danh sách các đối tượng lồng nhau), và khả năng mở rộng, chịu lỗi tốt khi chạy ở chế độ cụm.
    * **Hoạt động:** Warehouse Service sử dụng client của Elasticsearch (thông qua Spring Data Elasticsearch) để lập chỉ mục (indexing), cập nhật và truy vấn các document sản phẩm trong index `warehouse_products`. Cụm Elasticsearch gồm 3 node (`es01`, `es02`, `es03`) được định nghĩa trong `docker-compose.yml`.

### • Giao thức giao tiếp:

* Chủ yếu là **HTTP/REST** giữa Frontend UIs và Backend Services. Các frontend sử dụng JavaScript Fetch API để gửi các request GET, POST, PUT, DELETE tới các endpoint được cung cấp bởi Branch Service và Warehouse Service.
* **JDBC** được Branch Service sử dụng để giao tiếp với PostgreSQL.
* Warehouse Service sử dụng **Elasticsearch client protocol** (thường là REST API qua HTTP trên cổng 9200) để giao tiếp với cụm Elasticsearch.

---

## 2.2. Sharding và Replication trong Hệ thống

### • Đối với Warehouse Service và Elasticsearch:

* **Replication (Sao chép dữ liệu):** Elasticsearch, khi được cấu hình thành một cụm (như trong dự án này với 3 node `es01`, `es02`, `es03`), tự động hỗ trợ replication.
    * **Cách thức hoạt động:** Mỗi index trong Elasticsearch được chia thành một hoặc nhiều shards (phân mảnh chính). Mỗi shard này có thể có một hoặc nhiều replicas (bản sao). Elasticsearch sẽ tự động phân bổ các replica shard này trên các node khác nhau trong cụm so với primary shard của nó.
    * **Logic:** Khi dữ liệu được ghi vào primary shard, thay đổi đó cũng sẽ được đồng bộ sang các replica shard tương ứng. Nếu node chứa primary shard gặp sự cố, một trong các replica shard trên một node khác sẽ được "promote" lên làm primary shard mới, đảm bảo tính sẵn sàng của dữ liệu và khả năng chịu lỗi.
    * **Thuật toán:** Elasticsearch sử dụng một mô hình nhất quán gọi là "primary-backup model" hoặc "quorum-based replication" cho việc ghi dữ liệu để đảm bảo dữ liệu được ghi an toàn vào một số lượng bản sao cần thiết trước khi xác nhận lại cho client. Việc đọc có thể được thực hiện từ cả primary hoặc replica shard.

* **Sharding (Phân mảnh dữ liệu):**
    * **Cách thức hoạt động:** Như đã đề cập, mỗi index (ví dụ: `warehouse_products`) được chia thành các primary shards. Dữ liệu của index sẽ được phân bổ đều trên các primary shards này. Ví dụ, nếu index có 3 primary shards, mỗi document sẽ được gán vào một shard dựa trên một thuật toán băm (hashing) theo ID của document (hoặc một routing key tùy chỉnh).
    * **Logic:** Điều này cho phép index có thể lưu trữ lượng dữ liệu lớn hơn khả năng của một node đơn lẻ và cũng giúp phân tán tải truy vấn trên nhiều node, cải thiện hiệu năng.
    * **Thuật toán:** Mặc định, Elasticsearch sử dụng một công thức dựa trên hàm băm của ID document để quyết định document đó thuộc về shard nào: `shard_num = hash(_routing) % num_primary_shards`. Giá trị `_routing` mặc định là ID của document.

### • Đối với Branch Service và PostgreSQL:

* **Hiện trạng:** Trong cấu hình hiện tại (`docker-compose.yml`), PostgreSQL chỉ chạy dưới dạng một instance đơn lẻ (`postgres-db`). Do đó, chưa có cơ chế sharding hay replication nào được triển khai cho PostgreSQL từ phía ứng dụng hay cấu hình Docker.

---

## 3. Công nghệ và Thư viện sử dụng (Giải thích lý do chọn)

* **Java 17 và Spring Boot 3.4.5 (cho Backend):**
    * **Lý do chọn:** Spring Boot là một framework mạnh mẽ và phổ biến để xây dựng các ứng dụng Java, đặc biệt là microservices, nhờ khả năng khởi tạo nhanh, cấu hình tự động, và hệ sinh thái thư viện phong phú. Java 17 là phiên bản LTS (Long-Term Support) mang lại sự ổn định và các tính năng ngôn ngữ hiện đại.
    * **Spring Web (Spring MVC):** Dùng để xây dựng các REST API một cách dễ dàng.
    * **Spring Data JPA (cho Branch Service):** Đơn giản hóa việc tương tác với cơ sở dữ liệu quan hệ (PostgreSQL) bằng cách cung cấp một tầng trừu tượng qua các Repository interface.
    * **Spring Data Elasticsearch (cho Warehouse Service):** Cung cấp các công cụ tương tự như Spring Data JPA nhưng dành cho việc tương tác với Elasticsearch, giúp việc lập chỉ mục và truy vấn document trở nên thuận tiện.
    * **Lombok:** Giảm thiểu code soạn sẵn (boilerplate code) như getters, setters, constructors, logger,... giúp code ngắn gọn và dễ đọc hơn.

* **HTML, CSS, JavaScript (Fetch API) (cho Frontend):**
    * **Lý do chọn:** Là các công nghệ web nền tảng, dễ tiếp cận và không yêu cầu môi trường build phức tạp cho các giao diện đơn giản như trong dự án hiện tại. Fetch API là một chuẩn hiện đại của JavaScript để thực hiện các yêu cầu HTTP. (Lưu ý: Việc sử dụng framework frontend như React, Vue, Angular sẽ có lợi hơn cho việc mở rộng và bảo trì sau này).

* **PostgreSQL (cho Branch Service):**
    * **Lý do chọn:** Là một hệ quản trị cơ sở dữ liệu quan hệ mã nguồn mở mạnh mẽ, đáng tin cậy, hỗ trợ tốt các giao dịch ACID, phù hợp cho việc lưu trữ dữ liệu chi nhánh vốn yêu cầu tính nhất quán cao.

* **Elasticsearch (cho Warehouse Service):**
    * **Lý do chọn:** Là một công cụ tìm kiếm và phân tích phân tán mạnh mẽ. Rất phù hợp để lưu trữ và truy vấn dữ liệu sản phẩm với yêu cầu tìm kiếm phức tạp (full-text search, filtering, aggregation) và khả năng xử lý cấu trúc dữ liệu JSON linh hoạt (nested objects cho `branchesInventory`). Khả năng mở rộng theo chiều ngang và chịu lỗi khi chạy trong cụm cũng là một lợi thế lớn.

* **Docker & Docker Compose (cho Triển Khai & Môi Trường):**
    * **Lý do chọn:** Docker cho phép đóng gói ứng dụng và các phụ thuộc của nó vào các container độc lập, đảm bảo tính nhất quán môi trường giữa phát triển, kiểm thử và sản xuất. Docker Compose đơn giản hóa việc định nghĩa và chạy các ứng dụng đa container, giúp dễ dàng thiết lập toàn bộ hệ thống microservices chỉ với một vài lệnh.

* **Apache Maven (Build Tool cho Backend):**
    * **Lý do chọn:** Là một công cụ quản lý dự án và build phổ biến trong cộng đồng Java. Nó giúp quản lý các dependency, biên dịch code, đóng gói ứng dụng (ví dụ: thành file JAR cho Spring Boot) một cách hiệu quả.

---

## 4. Mô hình dữ liệu (Database Model)

Phần này mô tả cấu trúc dữ liệu được sử dụng bởi các service.

### 4.1. Mô hình dữ liệu cho Branch Service (PostgreSQL)

Dữ liệu chi nhánh được lưu trong bảng `branches` trong PostgreSQL.

* **Bảng: `branches`** (Ánh xạ từ entity `Branch.java`)
    * `id` (BIGINT, Primary Key, Auto Increment): Khóa chính của bảng, tự động tăng.
    * `branch_code` (VARCHAR, Unique, Not Null): Mã định danh duy nhất cho mỗi chi nhánh (ví dụ: "CN_HCM_Q1").
    * `name` (VARCHAR, Not Null): Tên của chi nhánh.
    * `address` (VARCHAR): Địa chỉ của chi nhánh.
    * `city` (VARCHAR): Thành phố nơi chi nhánh tọa lạc.
    * `phone_number` (VARCHAR): Số điện thoại liên hệ của chi nhánh.
    * `active` (BOOLEAN, Not Null, Default: true): Trạng thái hoạt động của chi nhánh (true = đang hoạt động, false = không hoạt động).

### 4.2. Mô hình dữ liệu cho Warehouse Service (Elasticsearch)

Dữ liệu sản phẩm và tồn kho được lưu trữ dưới dạng các JSON document trong index `warehouse_products` của Elasticsearch.

* **Document: `Product`** (Ánh xạ từ class `Product.java`)
    * `_id` (Keyword, Elasticsearch tự sinh hoặc do ứng dụng cung cấp): ID duy nhất của document trong Elasticsearch. (Trong dự án, nếu `product.id` là null, ProductService sẽ tự sinh một UUID).
    * `productId` (Keyword): Mã sản phẩm tùy chỉnh do người dùng định nghĩa (ví dụ: "SP001").
    * `name` (Text, analyzer: standard): Tên sản phẩm, cho phép tìm kiếm full-text.
    * `description` (Text, analyzer: standard): Mô tả chi tiết về sản phẩm.
    * `basePrice` (Double): Giá gốc của sản phẩm.
    * `category` (Keyword): Danh mục của sản phẩm.
    * `branchesInventory` (Nested): Một mảng các đối tượng lồng nhau, mỗi đối tượng chứa thông tin tồn kho của sản phẩm tại một chi nhánh cụ thể.
        * **Đối tượng `BranchInventory` lồng nhau** (Ánh xạ từ class `BranchInventory.java`):
            * `branchId` (Keyword): Mã của chi nhánh (tham chiếu đến `branch_code` trong Branch Service).
            * `quantity` (Integer): Số lượng sản phẩm tồn kho tại chi nhánh đó.
            * `sellingPrice` (Double): Giá bán của sản phẩm tại chi nhánh đó.

---

## 5. Chiến lược triển khai và cấu hình hệ thống

Hệ thống "Quản Lý Tiệm Tạp Hóa" được thiết kế để triển khai bằng Docker và được điều phối bởi Docker Compose.

* **Đóng gói ứng dụng:**
    * Mỗi microservice backend (Branch Service, Warehouse Service) được build thành một file JAR thực thi bằng Maven. Sau đó, mỗi service có một `Dockerfile` riêng để đóng gói file JAR này cùng với môi trường Java Runtime cần thiết (ví dụ: OpenJDK) thành một Docker image.
        * **Nội dung chính của một `Dockerfile` (ví dụ: cho Warehouse Service):**
            ```dockerfile
            # Sử dụng một base image chứa Java Runtime
            FROM openjdk:17-jdk-slim
            
            # Thiết lập thư mục làm việc bên trong container
            WORKDIR /app
            
            # Sao chép file JAR đã được build (bởi Maven) vào container
            # Giả sử file JAR nằm trong thư mục target của project và có tên là warehouse-service.jar
            COPY target/warehouse-service.jar warehouse-service.jar
            
            # Định nghĩa cổng mà ứng dụng sẽ lắng nghe
            EXPOSE 8081 
            
            # Lệnh để chạy ứng dụng khi container khởi động
            ENTRYPOINT ["java", "-jar", "warehouse-service.jar"]
            ```
    * Các ứng dụng frontend (HTML/CSS/JS thuần) cũng được phục vụ thông qua một web server đơn giản (ví dụ: Nginx hoặc `httpd-alpine`) bên trong Docker container, được định nghĩa qua `Dockerfile` tương ứng của chúng.
    * Các cơ sở dữ liệu (PostgreSQL, Elasticsearch) sử dụng các Docker image chính thức từ Docker Hub.

* **Điều phối với Docker Compose:**
    * File `docker-compose.yml` định nghĩa tất cả các services (frontend UIs, backend microservices, databases), mạng nội bộ, volumes lưu trữ dữ liệu, port mappings, biến môi trường, và sự phụ thuộc khởi động (`healthchecks` và `depends_on`).
    * **Mạng (`tiemtaphoa-network`):** Một bridge network tùy chỉnh được tạo để cho phép các container giao tiếp với nhau bằng tên service của chúng.
    * **Volumes:** Dữ liệu của PostgreSQL (`postgres_data_compose`) và Elasticsearch (`esdata01`, `esdata02`, `esdata03`) được lưu trữ trên các volume của Docker host để đảm bảo dữ liệu không bị mất khi container khởi động lại hoặc bị xóa.
    * **Biến môi trường:** Các thông tin cấu hình quan trọng như chuỗi kết nối cơ sở dữ liệu, URI của Elasticsearch, port của server được truyền vào các container thông qua biến môi trường trong `docker-compose.yml`. Điều này giúp tách biệt cấu hình khỏi code.
    * **Khởi chạy hệ thống:** Toàn bộ hệ thống có thể được khởi chạy bằng lệnh `docker-compose up -d` và dừng bằng `docker-compose down`.


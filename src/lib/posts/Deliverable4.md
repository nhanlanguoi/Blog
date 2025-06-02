---
title: "Deliverable 4"
date: "2025-6-1" # Lưu ý: Định dạng ngày có thể không hợp lệ (tháng 18?), bạn có thể cần sửa lại.
updated: "2025-6-1" # Tương tự, kiểm tra lại định dạng ngày.
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/kientruchpt.png"
coverWidth: 16
coverHeight: 9
excerpt:  Deliverable 4
---

# Báo cáo Dự án: Ứng Dụng Phân Tán - Quản Lý Tiệm Tạp Hóa (Tập trung vào Elasticsearch)

## [Link GitHub Dự Án](https://github.com/nhanlanguoi/Managermaket)

### Trong link GitHub sẽ có bản báo cáo hoàn chỉnh file DOCX (hoặc PDF), mã nguồn, và hướng dẫn chi tiết trong file `README.md`.



## 1. Giới Thiệu Dự Án và Vai Trò Của Elasticsearch

### 1.1. Đề xuất đề tài và Mô tả vấn đề
Dự án **"Quản Lý Tiệm Tạp Hóa"** giải quyết bài toán quản lý tập trung cho chuỗi cửa hàng, đặc biệt là việc quản lý sản phẩm và tồn kho đa dạng, thay đổi liên tục. Vấn đề chính là làm sao để có một hệ thống linh hoạt, cho phép tìm kiếm sản phẩm nhanh chóng, quản lý tồn kho chính xác tại nhiều chi nhánh, và có khả năng mở rộng cũng như chịu lỗi tốt.

### 1.2. Lý do chọn Elasticsearch cho Quản lý Kho hàng và Sản phẩm
Việc quản lý hàng ngàn sản phẩm với các thuộc tính đa dạng, giá cả thay đổi, và lượng tồn kho biến động tại nhiều chi nhánh đặt ra yêu cầu cao về khả năng tìm kiếm và truy vấn dữ liệu. Các hệ quản trị cơ sở dữ liệu quan hệ truyền thống có thể gặp khó khăn trong việc đáp ứng các yêu cầu tìm kiếm toàn văn (full-text search) hiệu quả, cũng như xử lý linh hoạt các cấu trúc dữ liệu lồng nhau (như thông tin tồn kho của sản phẩm tại nhiều chi nhánh).

**Elasticsearch được chọn làm giải pháp lưu trữ và tìm kiếm cho `warehouse-service` vì những lý do chính sau:**

* **Khả năng tìm kiếm mạnh mẽ:** Elasticsearch nổi tiếng với khả năng tìm kiếm toàn văn cực kỳ nhanh và hiệu quả. Nó cho phép người dùng (qua Admin UI hoặc POS UI) tìm kiếm sản phẩm theo tên, mô tả, danh mục hoặc bất kỳ trường thông tin nào một cách linh hoạt, bao gồm cả các truy vấn phức tạp, gợi ý và xếp hạng kết quả.
* **Lưu trữ dữ liệu JSON linh hoạt:** Dữ liệu sản phẩm, bao gồm cả danh sách tồn kho tại các chi nhánh (`branchesInventory` là một mảng các đối tượng lồng nhau), có thể được mô hình hóa và lưu trữ một cách tự nhiên dưới dạng các document JSON trong Elasticsearch. Điều này phù hợp hơn so với việc phải thiết kế nhiều bảng quan hệ phức tạp.
* **Khả năng mở rộng theo chiều ngang (Scalability):** Khi lượng sản phẩm hoặc số lượng truy vấn tăng lên, cụm Elasticsearch có thể dễ dàng được mở rộng bằng cách thêm các node mới. Dữ liệu (shards) sẽ tự động được phân bổ lại, giúp tăng cường hiệu năng và khả năng lưu trữ.
* **Tính sẵn sàng cao và chịu lỗi (High Availability & Fault Tolerance):** Với việc triển khai dưới dạng cụm 3 node (`e1`, `e2`, `e3`) và cơ chế replication của Elasticsearch, hệ thống có thể tiếp tục hoạt động ngay cả khi một hoặc (trong một số trường hợp) nhiều node gặp sự cố. Dữ liệu được sao chép trên nhiều node, giảm thiểu nguy cơ mất mát dữ liệu.
* **Phân tích và tổng hợp dữ liệu (Analytics & Aggregations):** Mặc dù chưa được khai thác sâu trong dự án này, Elasticsearch cung cấp các công cụ mạnh mẽ để thực hiện phân tích và tổng hợp dữ liệu, ví dụ như thống kê sản phẩm bán chạy, phân tích xu hướng tồn kho, v.v., rất hữu ích cho việc phát triển các tính năng báo cáo trong tương lai.

### 1.3. Phân tích Elasticsearch (Điểm mạnh, điểm yếu, trường hợp áp dụng)

* **Điểm mạnh:**
    * **Tìm kiếm cực nhanh:** Tối ưu cho tìm kiếm toàn văn và các loại truy vấn phức tạp.
    * **Phân tán và Mở rộng:** Thiết kế để chạy trong một cụm, dễ dàng mở rộng theo chiều ngang.
    * **Schema-less / Schema-flexible:** Linh hoạt với cấu trúc dữ liệu JSON, dễ dàng thay đổi hoặc thêm trường mới.
    * **Replication và Sharding tự động:** Đảm bảo tính sẵn sàng cao và khả năng chịu lỗi.
    * **Hệ sinh thái phong phú:** Công cụ như Kibana để trực quan hóa, Logstash/Fluentd để thu thập log (ELK Stack).
    * **API RESTful:** Dễ dàng tương tác và tích hợp.
* **Điểm yếu:**
    * **Yêu cầu tài nguyên:** Thường yêu cầu nhiều RAM và CPU hơn so với các database truyền thống.
    * **Quản lý cụm:** Việc vận hành và bảo trì một cụm Elasticsearch có thể phức tạp hơn.
    * **Tính nhất quán (Consistency):** Là "eventually consistent", nghĩa là dữ liệu mới ghi có thể mất một khoảng thời gian ngắn (thường là mili giây) để được tất cả các node nhìn thấy. Điều này có thể không phù hợp với các ứng dụng yêu cầu tính nhất quán tức thời mạnh mẽ như giao dịch tài chính.
    * **Không hỗ trợ JOIN phức tạp như SQL:** Các mối quan hệ dữ liệu cần được thiết kế cẩn thận (ví dụ: sử dụng nested objects, parent-child relationships, hoặc denormalization).
* **Trường hợp áp dụng lý tưởng cho Elasticsearch trong dự án:**
    * Lưu trữ và quản lý danh mục sản phẩm lớn với nhiều thuộc tính.
    * Cung cấp chức năng tìm kiếm sản phẩm nhanh và linh hoạt cho người dùng.
    * Quản lý dữ liệu tồn kho thay đổi thường xuyên và cần truy vấn hiệu suất cao theo chi nhánh.
    * Xây dựng nền tảng cho các tính năng phân tích, báo cáo dữ liệu sản phẩm và bán hàng trong tương lai.

---

## 2. Thiết Kế Hệ Thống với Elasticsearch là Trung Tâm

### 2.1. Mô hình kiến trúc tổng quan
*Sơ đồ kiến trúc sẽ làm nổi bật vai trò của `warehouse-service` và cụm Elasticsearch là nơi xử lý chính các nghiệp vụ liên quan đến sản phẩm và tồn kho, trong khi `branch-service` và PostgreSQL tập trung vào quản lý thông tin chi nhánh.*

Hệ thống được thiết kế theo kiến trúc microservices. `Warehouse-service`, sử dụng cụm Elasticsearch 3 node (`e1`, `e2`, `e3`), là trái tim của việc quản lý sản phẩm và tồn kho. Các giao diện người dùng như `Admin UI` và `Branch POS UI` tương tác chủ yếu với service này cho các nghiệp vụ liên quan đến sản phẩm. `Branch-service` và PostgreSQL đóng vai trò hỗ trợ, quản lý thông tin chi nhánh.

### 2.2. Mô tả chi tiết các thành phần và sự tương tác với Elasticsearch

#### 2.2.1. Giao diện Người dùng (Frontend UIs)
* **`Admin UI`:** Gửi các yêu cầu tạo, cập nhật, xóa, và đọc thông tin sản phẩm (bao gồm cả tồn kho `branchesInventory`) đến `warehouse-service`. Các yêu cầu này sau đó được `warehouse-service` xử lý và lưu trữ/truy vấn từ Elasticsearch.
    * **Giải thích sơ qua code gọi API thêm sản phẩm:** JavaScript trong `admin.html` thu thập dữ liệu từ form, bao gồm cả mảng `branchesInventory`, tạo một đối tượng JSON và gửi yêu cầu `POST` đến `/api/warehouse/products` của `warehouse-service` bằng Fetch API.
* **`Branch POS UI`:**
    * Truy vấn `warehouse-service` (endpoint `/api/warehouse/products/branch/{branchCode}`) để lấy danh sách sản phẩm và thông tin tồn kho (số lượng, giá bán) của một chi nhánh cụ thể. Dữ liệu này được lấy từ Elasticsearch.
    * Khi bán hàng, gửi yêu cầu `POST` đến `/api/warehouse/products/inventory/decrement` của `warehouse-service` để cập nhật (giảm) số lượng tồn kho trong Elasticsearch.
    * **Giải thích sơ qua code gọi API lấy sản phẩm và bán hàng:** JavaScript trong `branch.html` dùng Fetch API. Để lấy sản phẩm, nó gọi `GET` đến `/branch/{branchCode}`. Để bán hàng, nó tạo JSON payload chứa `productId`, `branchId`, `quantityToDecrement` và gửi `POST` đến `/inventory/decrement`.

#### 2.2.2. Dịch vụ Kho hàng (`warehouse-service`) và Elasticsearch
* **Vai trò:** Service này là cầu nối chính giữa ứng dụng và cụm Elasticsearch. Nó tiếp nhận các yêu cầu từ frontend, xử lý logic nghiệp vụ (ví dụ: kiểm tra tồn kho, tính toán giá) và sau đó thực hiện các thao tác CRUD (Create, Read, Update, Delete) trên các document sản phẩm trong Elasticsearch thông qua `ProductRepository`.
* **Logic quan trọng (ví dụ: `decrementInventory`):**
    1.  Tìm sản phẩm dựa trên `productId` trong Elasticsearch.
    2.  Tìm mục `BranchInventory` tương ứng với `branchId` trong danh sách lồng nhau của sản phẩm đó.
    3.  Kiểm tra xem số lượng tồn kho hiện tại (`inventoryToUpdate.getQuantity()`) có đủ để trừ đi số lượng yêu cầu bán (`quantityToDecrement`) không.
    4.  Nếu không đủ, ném lỗi `IllegalArgumentException`.
    5.  Nếu đủ, cập nhật số lượng tồn kho (`inventoryToUpdate.setQuantity(...)`).
    6.  Lưu lại toàn bộ document sản phẩm đã được cập nhật vào Elasticsearch bằng `productRepository.save(product)`.
    

#### 2.2.3. Các thành phần khác (Branch Service, PostgreSQL)
* `Branch Service` và PostgreSQL chủ yếu quản lý thông tin tĩnh hơn của các chi nhánh. `Branch POS UI` có gọi đến `Branch Service` để xác nhận trạng thái hoạt động của chi nhánh trước khi cho phép thao tác. Hiện tại, chưa có sự tương tác trực tiếp giữa `warehouse-service` (Elasticsearch) và `branch-service` (PostgreSQL) ở tầng backend, nhưng mã chi nhánh (`branchId`) là cầu nối logic giữa hai hệ thống dữ liệu này.

#### 2.2.4. Giao thức giao tiếp
* Frontend UI giao tiếp với `warehouse-service` qua HTTP/REST API.
* `Warehouse-service` giao tiếp với cụm Elasticsearch qua REST API trên cổng 9200, được trừu tượng hóa bởi Spring Data Elasticsearch.

### 2.3. Công nghệ và thư viện sử dụng (liên quan đến Elasticsearch)
* **Spring Boot:** Cung cấp nền tảng cho `warehouse-service`.
* **Spring Data Elasticsearch:** Là thư viện chính giúp đơn giản hóa việc tương tác với Elasticsearch từ ứng dụng Spring Boot. Nó cung cấp các annotation như `@Document`, `@Field`, `@Query` và interface `ElasticsearchRepository` để dễ dàng định nghĩa model, mapping và thực hiện các thao tác dữ liệu.
* **Elasticsearch (Cụm 3 node):** Nơi lưu trữ và tìm kiếm dữ liệu sản phẩm.
* **Docker & Docker Compose:** Dùng để đóng gói và triển khai `warehouse-service` cùng với cụm Elasticsearch một cách nhất quán.

### 2.4. Mô hình dữ liệu cho Elasticsearch (`Product` và `BranchInventory`)
* **Document `Product` (trong index `warehouse_products`):**
    * `id` (String, Elasticsearch ID): Khóa chính của document.
    * `productId` (Keyword): Mã sản phẩm tùy chỉnh (ví dụ: SP001).
    * `name` (Text): Tên sản phẩm (cho phép tìm kiếm full-text).
    * `description` (Text): Mô tả sản phẩm.
    * `basePrice` (Double): Giá gốc.
    * `category` (Keyword): Danh mục.
    * `branchesInventory` (Nested Type): Một danh sách các đối tượng `BranchInventory`. Đây là điểm mấu chốt cho phép lưu trữ thông tin tồn kho đa chi nhánh trong cùng một document sản phẩm.
        * **Đối tượng `BranchInventory` (nested):**
            * `branchId` (Keyword): Mã chi nhánh.
            * `quantity` (Integer): Số lượng tồn.
            * `sellingPrice` (Double): Giá bán tại chi nhánh đó.


### 2.5. Triển khai và cấu hình (tập trung vào cụm Elasticsearch)
* **Docker Compose:** Cụm Elasticsearch 3 node (`e1`, `e2`, `e3`) được định nghĩa và khởi chạy thông qua `docker-compose.yml`.
    * Mỗi node Elasticsearch là một service riêng, sử dụng image `elasticsearch:8.18.1`.
    * **Cấu hình Cluster:**
        * `node.name`: Đặt tên cho từng node (ví dụ: `e1`, `e2`, `e3`).
        * `cluster.name`: Tất cả các node phải có cùng tên cluster (ví dụ: `taphoa-es-cluster`).
        * `discovery.seed_hosts`: Liệt kê các node khác trong cụm để node hiện tại có thể tìm thấy và kết nối.
        * `cluster.initial_master_nodes`: Xác định các node có thể trở thành master khi cụm khởi tạo lần đầu.
    * **Volumes:** Dữ liệu của mỗi node Elasticsearch được lưu trữ bền vững trên các Docker volume riêng biệt (`esdata01`, `esdata02`, `esdata03`).
    * **Networking:** Tất cả các node Elasticsearch và `warehouse-service` cùng thuộc mạng `tiemtaphoa-network`, cho phép giao tiếp nội bộ.
    * **Biến môi trường cho `warehouse-service`:** `SPRING_ELASTICSEARCH_URIS=http://e1:9200,http://e2:9200,http://e3:9200` chỉ định cho `warehouse-service` cách kết nối đến cả ba node của cụm Elasticsearch.


---

## 3. Triển Khai và Cài Đặt (Tập trung vào Elasticsearch)

### 3.1. Hướng dẫn cài đặt và cấu hình cụm Elasticsearch
*(Như đã mô tả trong mục 2.5, việc cài đặt và cấu hình cụm được thực hiện hoàn toàn thông qua file `docker-compose.yml`. Chỉ cần chạy `docker-compose up -d` là cụm sẽ được khởi tạo.)*
Các cấu hình quan trọng cho việc hình thành cụm đã được đề cập: `cluster.name`, `discovery.seed_hosts`, `cluster.initial_master_nodes`.

### 3.2. Demo ban đầu với Elasticsearch (Lưu, truy vấn dữ liệu sản phẩm)
* Sau khi hệ thống khởi chạy, truy cập `Admin UI` (`http://localhost:8000`).
* Thêm một sản phẩm mới với một vài thông tin tồn kho chi nhánh.
* Quan sát log của `warehouse-service` để thấy yêu cầu được xử lý.
* (Nâng cao) Sử dụng một công cụ như Postman hoặc Kibana Dev Tools để gửi request trực tiếp đến API của `warehouse-service` (ví dụ `GET http://localhost:8080/api/warehouse/products`) hoặc API của Elasticsearch (ví dụ `GET http://localhost:9200/warehouse_products/_search`) để xem document sản phẩm vừa được tạo.

---

## 4. Hiện Thực Hóa Hệ Thống và Tiến Độ

### 4.1. Tóm tắt tiến độ dự án
 * Đã hoàn thành

### 4.2. Demo hoạt động của hệ thống (Tương tác với Elasticsearch)
* **Demo thêm sản phẩm:** Admin UI gửi dữ liệu sản phẩm (bao gồm `branchesInventory`) đến `warehouse-service`, dịch vụ này sẽ tạo một document JSON và lập chỉ mục (index) nó vào Elasticsearch.
* **Demo xem sản phẩm theo chi nhánh:** POS UI gọi đến `warehouse-service` với `branchCode`. `warehouse-service` thực hiện một nested query lên Elasticsearch để lấy các sản phẩm có tồn kho tại chi nhánh đó, chỉ trả về phần `BranchInventory` của chi nhánh đó cho mỗi sản phẩm.
* **Demo bán hàng:** POS UI gửi yêu cầu giảm tồn kho. `warehouse-service` tìm document sản phẩm trong Elasticsearch, cập nhật số lượng trong `BranchInventory` tương ứng, và lưu lại document đó vào Elasticsearch.
* **Demo Fault Tolerance (gián tiếp):** Dừng một node Elasticsearch (ví dụ `docker stop e1`). Thử thực hiện các thao tác xem/tìm kiếm sản phẩm trên `Admin UI` hoặc `POS UI`. Hệ thống (thông qua `warehouse-service`) vẫn nên hoạt động được do dữ liệu đã được replicated trên các node `e2`, `e3`. `warehouse-service` (nếu client Elasticsearch được cấu hình đúng) sẽ tự động chuyển hướng yêu cầu sang các node còn lại.

### 4.3. Mã nguồn và giải thích các đoạn code quan trọng (liên quan đến Elasticsearch)
* **`Product.java`:** Định nghĩa cấu trúc document, đặc biệt là trường `@Field(type = FieldType.Nested)` cho `branchesInventory`.
* **`ProductRepository.java`:** Interface mở rộng `ElasticsearchRepository`, với các phương thức truy vấn như `findByProductId` và đặc biệt là `@Query` cho `findByBranchIdInInventory` sử dụng nested query.
* **`ProductService.java`:**
    * Logic `createProduct` và `updateProduct` sẽ gọi `productRepository.save()` để ghi/cập nhật document vào Elasticsearch.
    * Logic `getProductsByBranch` sử dụng `productRepository.findByBranchIdInInventory()` và sau đó xử lý để chỉ trả về `BranchInventory` của chi nhánh cụ thể.
    * Logic `decrementInventory` đọc document từ ES, thay đổi trường `quantity` trong nested object, rồi `save()` lại toàn bộ document.
* **Cấu hình Elasticsearch URI trong `docker-compose.yml` cho `warehouse-service`:** `SPRING_ELASTICSEARCH_URIS=http://e1:9200,http://e2:9200,http://e3:9200` đảm bảo client kết nối đến cả cụm.

---

## 5. Đánh Giá Theo Tiêu Chí Kỹ Thuật (Tập trung vào Elasticsearch)

### 5.1. Tiêu chí bắt buộc

#### 5.1.1. Fault Tolerance (với cụm Elasticsearch)
* **Hiện trạng:** Đạt được ở mức độ cao cho dữ liệu sản phẩm/tồn kho nhờ cụm Elasticsearch 3 node với cơ chế replication tự động. Nếu một node lỗi, các replica shard trên node khác sẽ đảm nhận, và `warehouse-service` (nếu client được cấu hình đúng với nhiều URI) vẫn có thể tiếp tục hoạt động.
* **Mô tả:** Khi một node chứa primary shard lỗi, Elasticsearch sẽ tự động promote một replica shard trên node khác thành primary. Client (Spring Data Elasticsearch trong `warehouse-service`) khi được cấu hình với danh sách các node trong cụm sẽ có khả năng tự động chuyển hướng (failover) sang các node còn hoạt động.

#### 5.1.2. Distributed Communication (Tương tác với Elasticsearch)
* **Hiện trạng:** `Warehouse-service` giao tiếp với cụm Elasticsearch thông qua các API RESTful của Elasticsearch (được trừu tượng hóa bởi Spring Data Elasticsearch) trên cổng 9200. Việc giao tiếp này diễn ra qua mạng Docker nội bộ `tiemtaphoa-network`.
* **Mô tả:** `ProductRepository` và các lời gọi đến nó trong `ProductService` là minh chứng cho việc giao tiếp này.

#### 5.1.3. Sharding và Replication trong Elasticsearch
* **Hiện trạng:** Đã triển khai.
    * **Replication:** Mặc định, Elasticsearch sẽ tạo ít nhất một replica cho mỗi primary shard và phân bổ chúng trên các node khác nhau trong cụm 3 node. Điều này đảm bảo dữ liệu không bị mất nếu một node gặp sự cố và tăng khả năng đọc.
    * **Sharding:** Dữ liệu của index `warehouse_products` được chia thành các primary shards (số lượng mặc định hoặc có thể cấu hình). Mỗi document sản phẩm được định tuyến đến một primary shard cụ thể dựa trên ID của nó. Điều này cho phép dữ liệu được phân tán và xử lý song song.
* **Mô tả:** Elasticsearch tự động quản lý việc này. Khi tạo index `warehouse_products` (thông qua `@Document(createIndex = true)`), Elasticsearch sẽ áp dụng các cài đặt mặc định cho sharding và replication (nếu không được chỉ định khác).

#### 5.1.4. Simple Monitoring / Logging (cho Elasticsearch và `warehouse-service`)
* **Hiện trạng:**
    * `Warehouse-service` ghi log hoạt động và lỗi ra console (có thể xem qua `docker logs warehouse_service_compose`).
    * Cụm Elasticsearch tự nó cũng tạo ra rất nhiều log chi tiết về hoạt động của từng node (có thể xem qua `docker logs e1`, `docker logs e2`, `docker logs e3`).
    * Elasticsearch cung cấp các API monitoring (ví dụ: `_cluster/health`, `_nodes/stats`) có thể được truy cập để kiểm tra trạng thái cụm.
* **Giải pháp/Hướng cải thiện:** Sử dụng Prometheus với Elasticsearch Exporter và Grafana để có dashboard giám sát trực quan các metrics của cụm Elasticsearch và `warehouse-service`. Sử dụng ELK stack để tập trung hóa và phân tích log.

#### 5.1.5. Basic Stress Test (tập trung vào `warehouse-service` và Elasticsearch)
* **Hiện trạng:** Chưa thực hiện.
* **Kế hoạch:** Thực hiện stress test bằng JMeter/k6 nhắm vào các API của `warehouse-service` liên quan đến tạo sản phẩm, tìm kiếm sản phẩm, và đặc biệt là cập nhật tồn kho (API bán hàng).
* **Quan sát:** Thời gian phản hồi của API, % lỗi, CPU/RAM của các container `warehouse-service` và các node Elasticsearch (`e1`, `e2`, `e3`), tốc độ indexing và search của Elasticsearch.





#### 5.2 System Recovery (Rejoin after Failure)
* **Hiện trạng:** Node Elasticsearch có khả năng tự động tham gia lại cụm sau khi gặp lỗi hoặc khởi động lại, nhờ vào cơ chế discovery và cluster state management của Elasticsearch. Chính sách `restart: unless-stopped` cho container `warehouse-service` cũng giúp nó tự khởi động lại và kết nối lại với cụm Elasticsearch.

---

## 6. Kết Luận và Hướng Phát Triển Tương Lai (liên quan đến Elasticsearch)

Việc sử dụng Elasticsearch làm nền tảng cho `warehouse-service` đã mang lại những lợi ích đáng kể về khả năng tìm kiếm, tính linh hoạt của mô hình dữ liệu, khả năng mở rộng và chịu lỗi cho việc quản lý sản phẩm và tồn kho. Cụm Elasticsearch 3 node đã hoạt động ổn định, hỗ trợ tốt các nghiệp vụ chính của hệ thống.

Hướng phát triển tương lai liên quan đến Elasticsearch có thể bao gồm:
* **Tối ưu hóa truy vấn và indexing:** Khi dữ liệu lớn hơn, cần xem xét kỹ hơn về mapping, analyzer, và các chiến lược indexing để đảm bảo hiệu năng.
* **Sử dụng các tính năng nâng cao của Elasticsearch:** Khai thác aggregations cho việc xây dựng báo cáo, gợi ý tìm kiếm (suggesters), hoặc các tính năng phân tích khác.
* **Nâng cấp phiên bản Elasticsearch:** Theo dõi và nâng cấp lên các phiên bản mới hơn để tận dụng các cải tiến về hiệu năng và tính năng.
* **Giám sát chuyên sâu cho Elasticsearch:** Triển khai đầy đủ giải pháp monitoring với Prometheus/Grafana và logging tập trung với ELK stack.
* **Backup và Restore cho Elasticsearch:** Thiết lập chiến lược sao lưu và phục hồi dữ liệu cho cụm Elasticsearch.

---
---
title: "A Markdown post with a Svelte component"
date: "2023-05-26"
updated: "2023-05-26"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/ontapcuoiky.png"
coverWidth: 16
coverHeight: 9
excerpt: This post demonstrates how to include a Svelte component in a Markdown post.
---



# Ôn tập cuối kỳ

# Mục lục

- [Câu 1: Hệ thống phân tán, tập trung, phi tập trung khác nhau như thế nào, nêu ví dụ về mỗi loại, làm thế nào để xác định sự khác biệt chính?](#câu-1hệ-thống-phân-tán-tập-trung-phi-tập-trung-khác-nhau-như-thế-nào-nêu-ví-dụ-về-mỗi-loạilàm-thế-nào-để-xác-định-sự-khác-biệt-chính)
- [Câu 2: Các đặc tính của hệ phân tán là gì? Giải thích cho từng đặc điểm thật kỹ (tìm trong slides)](#câu-2-các-đặc-tính-của-hệ-phân-tán-là-gì-giải-thích-cho-từng-đặc-điểm-thật-kỹ-tìm-trong-slides)
- [Câu 3: Mục đích của nút chủ trong một hệ phân tán là để làm gì? Điều gì sẽ xảy ra nếu nút chủ gặp sự cố?](#câu-3-mục-đích-của-nút-chủ-trong-một-hệ-phân-tán-là-để-làm-gì-điều-gì-sẽ-xảy-ra-nếu-nút-chủ-gặp-sự-cố)
- [Câu 4: Trong một mạng không gian, tại sao các máy thường giao tiếp với nhau qua gossip protocol mà không gửi thông tin đến tất cả các máy khác hoặc gửi về một nút trung tâm?](#câu-4-trong-một-mạng-không-gian-tại-sao-các-máy-thường-giao-tiếp-với-nhau-qua-gossip-protocol-mà-không-gửi-thông-tin-đến-tất-cả-các-máy-khác-hoặc-gửi-về-một-nút-trung-tâm)
- [Câu 5: Các yếu tố cốt lõi của một hệ phân tán là gì?](#câu-5-các-yếu-tố-cốt-lõi-của-một-hệ-phân-tán-là-gì)
- [Câu 6: Nêu những lí do sử dụng hệ phân tán?](#câu-6-nêu-những-lí-do-sử-dụng-hệ-phân-tán)
- [Câu 7: Nêu định nghĩa hệ phân tán?](#câu-7nêu-định-nghĩa-hệ-phân-tán)
- [Câu 8: Chụp và để lên blog các hình của thuật toán Cristian, Berkeley, RBS, Lamport, Bully, Ring](#câu-8-chụp-và-để-lên-blog-các-hình-của-thuật-toán-cristian-berkeley-rbs-lamport-bully-ring)
- [Câu 9: Kỹ thuật phân tán nào hỗ trợ lập trình thủ tục, lập trình web, hướng đối tượng?](#câu-9-kỹ-thuật-phân-tán-nào-hỗ-trợ-lập-trình-thủ-tục-lập-trình-web-hướng-đối-tượng)
- [Câu 10: Tiến trình nhẹ, tiến trình, luồng có những ưu điểm và nhược điểm gì, liệt kê. Khi một lời gọi hệ thống dừng thì đối với 3 loại như thế nào? Tiến trình nhẹ, tiến trình và luồng có mối quan hệ như thế nào với nhau và với chính nó?](#câu-10-tiến-trình-nhẹ-tiến-trình-luồng-có-những-ưu-điểm-và-nhược-điểm-gì-liệt-kê-khi-một-lời-gọi-hệ-thống-dừng-thì-đối-với-3-loại-như-thế-nào-tiến-trình-nhẹ-tiến-trình-và-luồng-có-mối-quan-hệ-như-thế-nào-với-nhau-và-với-chính-nó)
- [Câu 11: Mô hình client-server là gì, vai trò của máy chủ và máy khách là gì?](#câu-11-mô-hình-client-server-là-gì-vai-trò-của-máy-chủ-và-máy-khách-là-gì)
- [Câu 14: Sharding là gì?](#câu-14-sharding-là-gì)
- [Câu 15: Các gói luồng có thể làm những nhiệm vụ gì?](#câu-15-các-gói-luồng-có-thể-làm-những-nhiệm-vụ-gì)
- [Câu 16: Phân loại sự khác nhau giữa luồng kiểu người dùng và luồng kiểu nhân](#câu-16-phân-loại-sự-khác-nhau-giữa-luồng-kiểu-người-dùng-và-luồng-kiểu-nhân)
- [Câu 17: Nêu các hàm chính trong RPC và giải thích chức năng của nó](#câu-17-nêu-các-hàm-chính-trong-rpc-và-giải-thích-chức-năng-của-nó)
- [Câu 18: Định nghĩa tiến trình, thread, multithread client, multithread server](#câu-18-định-nghĩa-tiến-trình-thread-multithread-client-multithread-server)
- [Câu 19: Review lại kiến thức căn bản của Map, Reduce và mục đích trong một hệ phân tán](#câu-19-review-lại-kiến-thức-căn-bản-của-map-reduce-và-mục-đích-trong-một-hệ-phân-tán)
- [Câu 20: Ảo hóa (Virtualization) là gì, mục đích của ảo hóa trong một hệ phân tán dùng để làm gì?](#câu-20-ảo-hóa-virtualization-là-gì-mục-đích-của-ảo-hóa-trong-một-hệ-phân-tán-dùng-để-làm-gì)
- [Câu 21: Review lại các kiến trúc của server đa luồng](#câu-21-review-lại-các-kiến-trúc-của-server-đa-luồng)
- [Câu 22: Review lại các hướng tiếp cận cài đặt luồng](#câu-22-review-lại-các-hướng-tiếp-cận-cài-đặt-luồng)
- [Câu 23: Tại sao chúng ta sử dụng bảng băm phân tán? Mục đích của bảng băm phân tán là gì? Consistent Hashing là gì? Finger table để làm gì? Tại sao sử dụng finger table?](#câu-23-tại-sao-chúng-ta-sử-dụng-bảng-băm-phân-tán-mục-đích-của-bảng-băm-phân-tán-là-gì-consistent-hashing-là-gì-finger-table-để-làm-gì-tại-sao-sử-dụng-finger-table)
- [Câu 24: Không gian phẳng là gì? Định danh là gì? Liệt kê các đặc điểm của không gian phẳng](#câu-24-không-gian-phẳng-là-gì-định-danh-là-gì-liệt-kê-các-đặc-điểm-của-không-gian-phẳng)
- [Câu 25: Tại sao cần đồng bộ hóa đồng hồ logic? Tại sao đồng hồ vật lý không đảm bảo? Mục đích của đồng bộ hóa và các thuật toán đồng bộ hóa là gì?](#câu-25-tại-sao-cần-đồng-bộ-hóa-đồng-hồ-logic-tại-sao-đồng-hồ-vật-lý-không-đảm-bảo-mục-đích-của-đồng-bộ-hóa-và-các-thuật-toán-đồng-bộ-hóa-là-gì)
- [Câu 26: Đồng hồ Lamport giải quyết vấn đề gì? Nêu và giải thích các rules của đồng hồ Lamport](#câu-26-đồng-hồ-lamport-giải-quyết-vấn-đề-gì-nêu-và-giải-thích-các-rules-của-đồng-hồ-lamport)
- [Câu 27: Tham khảo lại các bài tập của đồng hồ logic Lamport trong slides chương 4-5](#câu-27-tham-khảo-lại-các-bài-tập-của-đồng-hồ-logic-lamport-trong-slides-chương-4-5)
- [Câu 28: Giao thức đồng bộ NTP là gì? PTP là gì? Được tính toán như thế nào?](#câu-28-giao-thức-đồng-bộ-ntp-là-gì-ptp-là-gì-được-tính-toán-như-thế-nào)

---


## Câu 1:Hệ thống phân tán, tập trung, phi tập trung khác nhau như thế nào, nêu ví dụ về mỗi loại,làm thế nào để xác định sự khác biệt chính?
- **Hệ thống phân tán tập trung**: là quyết định được tập trung hoá ,nhưng công việc vẫn chia đều cho mỗi node.
    - ví dụ:trong một công ti mỗi nhóm là một tổ chức và chia đều công việc cho mõi nhóm.thì các quyết định hay phê duyệt đều chịu sự quản lý cuả cấp trên.
- **Hệ thống phân tán phi tập trung**: là quyết định được sự đồng thuận giưã các node.mỗi node trong mạng có thể dữ vai trò xác thực ,đảm bảo đúng điều kiện.
    - ví dụ : trong một hội đồng quốc hội mỗi ban là một node mọi phê duyệt đều phải chịu sự đồng thuận của mọi người.

> => sự khác biệt chính ở đây là sự quản lý và kiểm duyệt .thường thì tập trung sẽ mang tính xác thực từ một node còn phi tập tủng phải thông qua xác thực nhiều node.



## Câu 2: Các đặc tính của hệ phân tán là gì? Giải thích cho từng đặc điểm thật kỹ (tìm trong slides)

Hệ phân tán có 4 đặc điểm chính:

### 1. Chia sẻ tài nguyên (Resource Sharing)
- Các tài nguyên như phần cứng, phần mềm, dữ liệu... có thể được sử dụng bởi nhiều người dùng hoặc tiến trình trên các máy khác nhau trong hệ thống.
- Ví dụ: Nhiều máy tính cùng sử dụng máy in mạng, truy cập vào một cơ sở dữ liệu chung.

### 2. Tính trong suốt (Transparency)
Tính trong suốt giúp người dùng không cần biết tài nguyên đang được xử lý như thế nào, đang ở đâu hoặc có bao nhiêu bản sao.

Các loại tính trong suốt gồm:
- **Access transparency**: Truy cập tài nguyên giống nhau dù ở cục bộ hay từ xa.
- **Location transparency**: Không cần biết vị trí thực của tài nguyên.
- **Replication transparency**: Không cần biết có bao nhiêu bản sao của tài nguyên.
- **Concurrency transparency**: Nhiều người dùng truy cập cùng lúc mà không ảnh hưởng nhau.
- **Failure transparency**: Hệ thống vẫn tiếp tục hoạt động khi có thành phần gặp lỗi.

### 3. Tính mở (Openness)
- Hệ thống phân tán sử dụng các giao thức chuẩn để các thành phần khác nhau có thể giao tiếp với nhau một cách linh hoạt.
- Cho phép mở rộng, tích hợp hoặc thay đổi thành phần dễ dàng.

### 4. Tính co giãn (Scalability)
- Hệ thống có khả năng mở rộng khi số lượng người dùng hoặc khối lượng công việc tăng lên.

Ba hướng mở rộng chính:
- **Kích thước**: Có thể thêm máy tính hoặc tài nguyên mới.
- **Địa lý**: Có thể triển khai hệ thống phân tán trên nhiều khu vực khác nhau.
- **Quản lý**: Dễ duy trì và quản lý khi mở rộng quy mô hệ thống.


## Câu 3: Mục đích của nút chủ trong một hệ phân tán là để làm gì? Điều gì sẽ xảy ra nếu nút chủ gặp sự cố?

### Mục đích của nút chủ (Master Node)
- **Quản lý tài nguyên**: Phân phối và giám sát tài nguyên trong hệ thống.
- **Điều phối hoạt động**: Điều khiển và điều phối các tác vụ giữa các nút khác.
- **Duy trì trạng thái hệ thống**: Theo dõi và cập nhật trạng thái của toàn hệ thống.
- **Xử lý yêu cầu**: Nhận và xử lý các yêu cầu từ người dùng hoặc các nút khác.

### Hậu quả khi nút chủ gặp sự cố
- **Gián đoạn dịch vụ**: Các dịch vụ phụ thuộc vào nút chủ có thể bị gián đoạn.
- **Mất khả năng điều phối**: Hệ thống không thể phân phối hoặc điều phối các tác vụ mới.
- **Nguy cơ mất dữ liệu**: Nếu nút chủ lưu trữ dữ liệu quan trọng mà không có bản sao dự phòng.
- **Giảm hiệu suất hệ thống**: Các nút khác có thể hoạt động kém hiệu quả hoặc không đồng bộ.

## Câu 4: Trong một mạng không gian, tại sao các máy thường giao tiếp với nhau qua gossip protocol mà không gửi thông tin đến tất cả các máy khác hoặc gửi về một nút trung tâm?

### Lý do sử dụng Gossip Protocol
- **Phân tán và không có điểm trung tâm**: Gossip protocol hoạt động theo mô hình peer-to-peer, không phụ thuộc vào nút trung tâm, giảm nguy cơ điểm lỗi đơn.
- **Khả năng mở rộng cao**: Thông tin được lan truyền dần dần qua các nút, phù hợp với hệ thống lớn.
- **Tăng tính chịu lỗi**: Nếu một số nút bị lỗi, thông tin vẫn có thể được truyền qua các nút khác.
- **Giảm tải mạng**: Thay vì gửi thông tin đến tất cả các nút cùng lúc, gossip protocol truyền thông tin một cách ngẫu nhiên, giảm tải cho mạng.
- **Đơn giản và hiệu quả**: Cơ chế hoạt động đơn giản nhưng hiệu quả trong việc đồng bộ hóa thông tin giữa các nút.


## Câu 5: Các yếu tố cốt lõi của một hệ phân tán là gì?

Hệ phân tán bao gồm các yếu tố cốt lõi sau:

- 1. Tập hợp các nút (Nodes)

- 2. Mạng truyền thông (Communication Network)


- 3. Phần mềm phân tán (Middleware)


- 4. Đồng bộ hóa và điều phối (Coordination and Synchronization)


- 5. Tính nhất quán và xử lý lỗi (Consistency and Fault Tolerance)


- 6. Bảo mật (Security)

## Câu 6: Nêu những lí do sử dụng hệ phân tán?
### 1: giúp xây dựng hệ phân tán quản lý công việc và dự án dễ dàng hơn.
### 2: có thể tính chịu lỗi,và linh hoạt cũng như mở rộng cao.
### 3: giúp cấu hình dễ dàng hơn


## Câu 7:Nêu định nghĩa hệ phân tán?
- Hệ phân tán là một tập hợp các máy tính độc lập mà, đối với người dùng, nó như thể một hệ thống đơn gắn kết.

## Câu 8: Chụp và để lên blog các hình của thuật toán Cristian, Berkeley, RBS, Lamport, Bully, Ring




## Câu 9: Kỹ thuật phân tán nào hỗ trợ lập trình thủ tục, lập trình web, hướng đối tượng?

Dưới đây là các kỹ thuật phân tán tương ứng với từng mô hình lập trình:

### 1. Hỗ trợ **lập trình thủ tục** (Procedural Programming)
- **RPC (Remote Procedure Call)**:  
  Cho phép một chương trình gọi thủ tục trên máy khác như gọi hàm nội bộ.  
  → Phù hợp với phong cách lập trình thủ tục (C, Pascal...).

### 2. Hỗ trợ **lập trình hướng đối tượng** (Object-Oriented Programming)
- **RMI (Remote Method Invocation)**:  
  Cho phép đối tượng này gọi phương thức của đối tượng khác qua mạng.  
  → Phù hợp với Java, C#, và các ngôn ngữ hướng đối tượng.
- **CORBA (Common Object Request Broker Architecture)**:  
  Cung cấp cơ chế để các đối tượng giao tiếp bất kể ngôn ngữ lập trình hay nền tảng.

### 3. Hỗ trợ **lập trình web**
- **SOA (Service-Oriented Architecture)**:
  Kiến trúc hướng dịch vụ, sử dụng các giao thức chuẩn như HTTP, XML, SOAP.  
  → Phù hợp với lập trình dịch vụ web (Web Services).
- **RESTful APIs**:
  Kiến trúc nhẹ, sử dụng giao thức HTTP để thực hiện các thao tác CRUD qua URL.  
  → Phổ biến trong lập trình web hiện đại.
- **GraphQL**:
  Ngôn ngữ truy vấn linh hoạt thường dùng trong các ứng dụng web phân tán hiện đại.



## Câu 10: Tiến trình nhẹ, tiến trình, luồng có những ưu điểm và nhược điểm gì, liệt kê. Khi một lời gọi hệ thống dừng thì đối với 3 loại như thế nào? Tiến trình nhẹ, tiến trình và luồng có mối quan hệ như thế nào với nhau và với chính nó?

### 1. Định nghĩa

- **Tiến trình (Process)** là một chương trình đang thực thi, có không gian địa chỉ riêng, quản lý tài nguyên riêng như bộ nhớ, tập tin, và thông tin tiến trình. Mỗi tiến trình độc lập với tiến trình khác.

- **Luồng (Thread)** là đơn vị nhỏ hơn tiến trình. Các luồng cùng tiến trình sẽ chia sẻ không gian địa chỉ và tài nguyên với nhau, nhưng có ngăn xếp riêng để lưu trữ trạng thái cục bộ.

- **Tiến trình nhẹ (Lightweight Process - LWP)** là một dạng thực thi gần giống thread, được hệ điều hành quản lý giống như process nhưng nhẹ hơn. Nó là cầu nối giữa luồng người dùng và luồng ở mức hệ thống.

---

### 2. Ưu điểm và nhược điểm

- **Tiến trình**:
  - *Ưu điểm*: Cách ly hoàn toàn giữa các tiến trình, giúp hệ thống an toàn hơn nếu một tiến trình bị lỗi.
  - *Nhược điểm*: Tốn nhiều tài nguyên hơn để tạo và quản lý. Việc giao tiếp giữa các tiến trình (IPC) phức tạp và chậm.

- **Luồng**:
  - *Ưu điểm*: Tạo nhanh, sử dụng ít tài nguyên hơn tiến trình. Các luồng trong cùng tiến trình chia sẻ tài nguyên nên giao tiếp nhanh.
  - *Nhược điểm*: Nếu một luồng bị lỗi có thể làm hỏng toàn bộ tiến trình. Việc đồng bộ giữa các luồng phức tạp hơn.

- **Tiến trình nhẹ (LWP)**:
  - *Ưu điểm*: Có thể kết hợp được hiệu quả giữa luồng người dùng và luồng nhân. Chuyển ngữ cảnh nhanh hơn tiến trình đầy đủ.
  - *Nhược điểm*: Tốn chi phí tạo và duy trì nếu quá nhiều LWP. Không kiểm soát chi tiết như luồng người dùng.

---

### 3. Khi một lời gọi hệ thống bị chặn

- Với **tiến trình**: Nếu một lời gọi hệ thống trong tiến trình bị chặn, toàn bộ tiến trình sẽ bị treo cho đến khi lời gọi hoàn tất.

- Với **luồng**: Nếu một luồng trong tiến trình gọi hệ thống và bị chặn, toàn bộ các luồng khác trong tiến trình đó cũng có thể bị ảnh hưởng nếu không được thiết kế để chạy song song độc lập.

- Với **tiến trình nhẹ (LWP)**: Nếu một LWP bị chặn, các LWP khác vẫn có thể tiếp tục chạy bình thường. Điều này giúp tận dụng đa lõi tốt hơn.

---

### 4. Mối quan hệ giữa tiến trình, luồng và tiến trình nhẹ

- Một tiến trình có thể chứa nhiều luồng. Các luồng trong cùng một tiến trình chia sẻ bộ nhớ và tài nguyên chung.

- Các luồng được ánh xạ với các tiến trình nhẹ (LWP) để hệ điều hành quản lý việc thực thi.

- LWP là đại diện của luồng ở cấp hệ điều hành, giúp ánh xạ giữa luồng người dùng và tài nguyên phần cứng.

- Như vậy, **tiến trình là vùng bao**, **luồng là đơn vị thực thi nhỏ bên trong tiến trình**, và **LWP là cầu nối giữa luồng và hệ điều hành**.


## Câu 11: Mô hình client-server là gì, vai trò của máy chủ và máy khách là gì?

### 1. Định nghĩa mô hình client-server

Mô hình **client-server** là một mô hình kiến trúc mạng phổ biến, trong đó các thiết bị (gọi là **client – máy khách**) gửi yêu cầu đến một máy tính trung tâm (**server – máy chủ**) để xử lý và trả về kết quả.

Mô hình này là mô hình **đa tầng**, trong đó:
- **Client** là tầng gửi yêu cầu và giao tiếp với người dùng.
- **Server** là tầng xử lý chính, lưu trữ dữ liệu, thực hiện logic nghiệp vụ và phản hồi lại client.


### 2. Vai trò

#### Máy chủ (Server):
- Lưu trữ và quản lý dữ liệu.
- Xử lý các yêu cầu từ client.
- Đảm bảo tính sẵn sàng và độ tin cậy cao.
- Có thể phục vụ đồng thời nhiều client.

#### Máy khách (Client):
- Gửi yêu cầu tới server (như lấy dữ liệu, thực hiện hành động).
- Hiển thị kết quả cho người dùng.
- Có thể là ứng dụng web, desktop, hoặc thiết bị di động.


## Câu 14: Sharding là gì?

Sharding là kỹ thuật phân chia cơ sở dữ liệu hoặc dữ liệu lớn thành nhiều phần nhỏ hơn, gọi là các shard, mỗi shard lưu trữ một phần dữ liệu độc lập trên các máy chủ khác nhau trong hệ phân tán. Mục đích của sharding là tăng khả năng mở rộng, cải thiện hiệu suất xử lý và giảm tải cho từng máy chủ.

---

## Câu 15: Các gói luồng có thể làm những nhiệm vụ gì?

Các gói liên quan đến luồng (threads) trong lập trình có thể thực hiện các nhiệm vụ như:
- Tạo và quản lý luồng (khởi tạo, bắt đầu, dừng luồng).
- Đồng bộ hóa giữa các luồng để tránh xung đột dữ liệu.
- Điều phối và lên lịch thực thi các luồng.
- Quản lý giao tiếp và truyền thông giữa các luồng.
- Quản lý pool luồng để tái sử dụng luồng hiệu quả.

---

## Câu 16: Phân loại sự khác nhau giữa luồng kiểu người dùng và luồng kiểu nhân

- **Luồng kiểu người dùng (User-level threads)**:
  - Được quản lý bởi thư viện hoặc runtime của ứng dụng, không cần hỗ trợ trực tiếp từ hệ điều hành.
  - Việc chuyển đổi giữa các luồng diễn ra rất nhanh và nhẹ.
  - Không tận dụng được đa lõi vì hệ điều hành chỉ thấy một tiến trình.
  - Nếu một luồng bị chặn, toàn bộ tiến trình bị chặn.

- **Luồng kiểu nhân (Kernel-level threads)**:
  - Được quản lý trực tiếp bởi hệ điều hành.
  - Hệ điều hành có thể lập lịch và quản lý từng luồng riêng biệt.
  - Tận dụng được đa lõi, cho phép chạy song song thực sự.
  - Tốn nhiều tài nguyên hơn do cần hỗ trợ hệ điều hành.

---

## Câu 17: Nêu các hàm chính trong RPC và giải thích chức năng của nó

- **Client Stub**: Đại diện cho client, gọi hàm từ client và gửi yêu cầu đến server.
- **Server Stub**: Nhận yêu cầu từ client, giải mã và gọi hàm thực thi trên server.
- **RPC Runtime**: Xử lý đóng gói (marshalling), gửi dữ liệu qua mạng và nhận dữ liệu phản hồi.
- **Binding**: Thiết lập kết nối giữa client và server, có thể là tĩnh hoặc động.
- **Serialization/Deserialization**: Biến đổi dữ liệu và tham số thành định dạng có thể gửi qua mạng và ngược lại.

## Câu 18: Định nghĩa tiến trình, thread, multithread client, multithread server

- **Tiến trình (Process)**: Là một chương trình đang chạy, có không gian bộ nhớ riêng biệt và tài nguyên riêng để thực thi.

- **Thread (Luồng)**: Là đơn vị thực thi nhỏ nhất trong tiến trình, chia sẻ không gian bộ nhớ và tài nguyên với các luồng khác trong cùng tiến trình.

- **Multithread Client**: Một client có khả năng tạo và xử lý nhiều luồng cùng lúc, cho phép thực hiện nhiều tác vụ song song (ví dụ: gửi nhiều yêu cầu đến server đồng thời).

- **Multithread Server**: Một server có khả năng xử lý nhiều yêu cầu client đồng thời qua nhiều luồng khác nhau, tăng khả năng đáp ứng và xử lý song song.

---

## Câu 19: Review lại kiến thức căn bản của Map, Reduce và mục đích trong một hệ phân tán

- **Map**: Bước xử lý đầu tiên trong mô hình MapReduce, nơi dữ liệu lớn được phân chia thành các phần nhỏ và xử lý song song trên nhiều node khác nhau trong hệ phân tán.

- **Reduce**: Bước tổng hợp kết quả từ các bước Map, gom lại thành kết quả cuối cùng.

- **Mục đích**:
  - Tăng khả năng xử lý song song dữ liệu lớn.
  - Giảm thời gian xử lý nhờ phân chia công việc.
  - Phù hợp cho các hệ thống phân tán lớn như Hadoop, Spark.

---

## Câu 20: Ảo hóa (Virtualization) là gì, mục đích của ảo hóa trong một hệ phân tán dùng để làm gì?

- **Ảo hóa (Virtualization)** là công nghệ tạo ra các phiên bản ảo của tài nguyên phần cứng như máy chủ, lưu trữ, mạng hoặc hệ điều hành, cho phép nhiều môi trường hoạt động độc lập trên cùng một phần cứng vật lý.

- **Mục đích trong hệ phân tán**:
  - Tăng hiệu quả sử dụng tài nguyên phần cứng.
  - Dễ dàng mở rộng và quản lý hệ thống.
  - Tạo môi trường cách ly an toàn cho các ứng dụng và dịch vụ.
  - Hỗ trợ sao lưu, phục hồi nhanh chóng.
  - Giúp thử nghiệm và triển khai phần mềm linh hoạt hơn.


## Câu 21: Review lại các kiến trúc của server đa luồng

- **One-thread-per-request**: Mỗi yêu cầu của client được xử lý bởi một luồng riêng biệt.
- **Thread pool (Pool luồng)**: Tạo sẵn một nhóm luồng cố định để xử lý các yêu cầu, tránh tạo/dừng luồng tốn kém.
- **Event-driven (Sự kiện)**: Server sử dụng một hoặc vài luồng để xử lý sự kiện bất đồng bộ, phù hợp với I/O.
- **Hybrid**: Kết hợp thread pool và event-driven để tận dụng ưu điểm của cả hai.

---

## Câu 22: Review lại các hướng tiếp cận cài đặt luồng

- **User-level threads**: Được quản lý ở mức thư viện người dùng, không cần hỗ trợ hệ điều hành.
- **Kernel-level threads**: Được quản lý bởi hệ điều hành, tận dụng đa lõi và lập lịch trực tiếp.
- **Hybrid threading**: Kết hợp cả hai kiểu trên, ví dụ nhiều luồng người dùng được ánh xạ tới ít luồng nhân.

---

## Câu 23: Tại sao chúng ta sử dụng bảng băm phân tán? Mục đích của bảng băm phân tán là gì? Consistent Hashing là gì? Finger table để làm gì? Tại sao sử dụng finger table?

- **Bảng băm phân tán (Distributed Hash Table - DHT)** được sử dụng để phân phối dữ liệu và tìm kiếm hiệu quả trong các hệ thống phân tán mà không cần máy chủ trung tâm.
- **Mục đích**: Cung cấp khả năng tìm kiếm và lưu trữ dữ liệu phân tán với chi phí thấp, mở rộng tốt, và khả năng chịu lỗi cao.
- **Consistent Hashing**: Thuật toán băm giúp giảm thiểu việc di chuyển dữ liệu khi thêm hoặc bớt node trong hệ thống, giữ ổn định hệ thống.
- **Finger table**: Là bảng tra cứu trong một số hệ thống DHT (như Chord), giúp định vị node nhanh hơn bằng cách rút ngắn đường đi trong vòng băm.
- **Tại sao dùng finger table**: Giảm thời gian tìm kiếm từ O(N) xuống O(log N), cải thiện hiệu quả truy xuất dữ liệu.

---

## Câu 24: Không gian phẳng là gì? Định danh là gì? Liệt kê các đặc điểm của không gian phẳng

- **Không gian phẳng (Flat namespace)**: Là một không gian đặt tên mà các đối tượng được định danh một cách duy nhất, không có cấu trúc phân cấp.
- **Định danh (Identifier)**: Một giá trị hoặc chuỗi dùng để nhận dạng duy nhất một đối tượng trong hệ thống phân tán.
- **Đặc điểm của không gian phẳng**:
  - Mỗi định danh là duy nhất trong toàn hệ thống.
  - Không có cấu trúc phân cấp hoặc quan hệ cha-con.
  - Đơn giản trong việc tìm kiếm, nhưng có thể khó quản lý nếu quy mô lớn.
  - Thường dùng trong các hệ thống DHT.

---

## Câu 25: Tại sao cần đồng bộ hóa đồng hồ logic? Tại sao đồng hồ vật lý không đảm bảo? Mục đích của đồng bộ hóa và các thuật toán đồng bộ hóa là gì?

- **Tại sao cần đồng bộ hóa đồng hồ logic**:
  - Để xác định thứ tự xảy ra các sự kiện trong hệ phân tán, nhất là khi không có đồng hồ vật lý chung.
  - Đảm bảo tính nhất quán trong xử lý dữ liệu và điều phối hoạt động.

- **Tại sao đồng hồ vật lý không đảm bảo**:
  - Đồng hồ vật lý có thể không đồng bộ do độ trễ mạng, sai số thiết bị, ảnh hưởng môi trường.
  - Không thể đảm bảo thứ tự chính xác tuyệt đối của các sự kiện phân tán.

- **Mục đích đồng bộ hóa**:
  - Tạo ra thứ tự nhất quán của các sự kiện.
  - Hỗ trợ điều phối và tránh xung đột trong hệ phân tán.

- **Các thuật toán đồng bộ hóa**:
  - **Đồng hồ Lamport**: Dùng giá trị số tăng dần để đánh dấu sự kiện và so sánh thứ tự.
  - **Đồng hồ vector**: Ghi nhớ thứ tự sự kiện chi tiết hơn, hỗ trợ phát hiện quan hệ xảy ra song song.
  - **Giao thức NTP (Network Time Protocol)** và **PTP (Precision Time Protocol)**: Đồng bộ hóa đồng hồ vật lý qua mạng.

## Câu 26: Đồng hồ Lamport giải quyết vấn đề gì? Nêu và giải thích các rules của đồng hồ Lamport

- **Đồng hồ Lamport** được tạo ra để giải quyết vấn đề **xác định thứ tự xảy ra các sự kiện** trong hệ thống phân tán, nơi không có đồng hồ vật lý đồng bộ. Nó cung cấp một cách để gán nhãn thời gian logic cho các sự kiện để thiết lập thứ tự tương đối giữa chúng.

- **Các quy tắc (rules) của đồng hồ Lamport:**
  1. **Rule 1 (Tăng nội bộ):** Mỗi tiến trình tự tăng giá trị đồng hồ cục bộ trước khi thực hiện một sự kiện.
  2. **Rule 2 (Gửi thông điệp):** Khi gửi thông điệp, tiến trình gắn giá trị đồng hồ hiện tại vào thông điệp.
  3. **Rule 3 (Nhận thông điệp):** Khi nhận thông điệp có giá trị timestamp Tm, tiến trình cập nhật đồng hồ của mình thành `max(giá trị đồng hồ hiện tại, Tm) + 1`.
  
- Nhờ các quy tắc trên, đồng hồ Lamport đảm bảo rằng nếu sự kiện A xảy ra trước sự kiện B (theo quan hệ "happen-before"), thì timestamp của A sẽ nhỏ hơn timestamp của B.

---

## Câu 27: Tham khảo lại các bài tập của đồng hồ logic Lamport trong slides chương 4-5

---

## Câu 28: Giao thức đồng bộ NTP là gì? PTP là gì? Được tính toán như thế nào?

- **NTP (Network Time Protocol):**
  - Là giao thức được sử dụng để đồng bộ hóa đồng hồ máy tính qua mạng Internet hoặc mạng LAN.
  - NTP hoạt động bằng cách gửi các gói tin đồng hồ từ client đến server và tính toán sự chênh lệch thời gian dựa trên thời gian gửi và nhận.
  - Công thức tính toán độ trễ và chênh lệch thời gian dựa trên thời điểm gửi/nhận của các gói tin.

- **PTP (Precision Time Protocol):**
  - Giao thức đồng bộ thời gian với độ chính xác cao hơn NTP, thường dùng trong các hệ thống yêu cầu đồng bộ nghiêm ngặt như tự động hóa, tài chính.
  - PTP sử dụng các bước trao đổi thông tin thời gian phức tạp hơn, tính toán độ trễ mạng và hiệu chỉnh để đồng bộ hóa đồng hồ với độ chính xác micro giây hoặc nanô giây.
  
- Cả hai giao thức đều dựa trên việc tính toán thời gian gửi và nhận để hiệu chỉnh đồng hồ cục bộ nhằm giảm thiểu sai số so với đồng hồ chuẩn.




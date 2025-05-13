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

Khi bạn gõ "www.motvidu.com" vào thanh địa chỉ của trình duyệt và nhấn Enter, một chuỗi các hoạt động phức tạp sẽ diễn ra để hiển thị trang web đó. Dưới đây là diễn giải chi tiết về quy trình này, bao gồm tra cứu DNS, resolving DNS và caching.

**Quy trình duyệt web tổng quát:**

1.  **Người dùng nhập URL:** Bạn gõ "www.motvidu.com" vào trình duyệt.
2.  **Trình duyệt phân tích URL:** Trình duyệt tách URL thành các thành phần: giao thức (thường là "http" hoặc "https"), tên miền ("www.motvidu.com"), và có thể có đường dẫn cụ thể đến một tài nguyên trên trang web đó.
3.  **Tra cứu DNS (DNS Lookup):**
    * **Mục đích:** Máy tính và mạng internet giao tiếp với nhau bằng địa chỉ IP (ví dụ: 192.168.1.1), không phải tên miền. Do đó, trình duyệt cần chuyển đổi tên miền "www.motvidu.com" thành một địa chỉ IP tương ứng. Quá trình này gọi là tra cứu DNS.
    * **Các bước trong tra cứu DNS:**
        * **Kiểm tra Cache của trình duyệt:** Trình duyệt sẽ kiểm tra xem nó đã từng truy cập trang này gần đây và lưu lại địa chỉ IP trong bộ nhớ đệm (cache) của mình chưa. Nếu có, nó sẽ sử dụng IP này và bỏ qua các bước tiếp theo của việc tra cứu DNS.
        * **Kiểm tra Cache của Hệ điều hành (OS Cache):** Nếu không tìm thấy trong cache của trình duyệt, hệ điều hành cũng có một bộ nhớ đệm DNS riêng. Trình duyệt sẽ yêu cầu hệ điều hành kiểm tra cache này.
        * **Kiểm tra Router Cache:** Một số router cũng có khả năng lưu trữ cache DNS.
        * **Truy vấn đến DNS Resolver (Recursive DNS Server):** Nếu tất cả các bộ nhớ đệm trên đều không có thông tin, trình duyệt sẽ gửi một yêu cầu đến một máy chủ DNS đặc biệt gọi là DNS Resolver. DNS Resolver thường được cung cấp bởi Nhà cung cấp dịch vụ Internet (ISP) của bạn hoặc các dịch vụ DNS công cộng như Google DNS (8.8.8.8) hay Cloudflare DNS (1.1.1.1).
4.  **Resolving DNS (Quá trình phân giải DNS bởi Resolver):**
    * **Recursive Query:** DNS Resolver nhận yêu cầu từ trình duyệt và bắt đầu quá trình tìm kiếm địa chỉ IP một cách đệ quy.
    * **Root Servers:** Nếu Resolver không có thông tin trong cache của nó, nó sẽ hỏi một trong các Root DNS Server. Root server không biết địa chỉ IP của "www.motvidu.com" nhưng nó biết nơi chứa thông tin về các tên miền cấp cao nhất (Top-Level Domain - TLD) như ".com", ".org", ".net". Root server sẽ trả về địa chỉ của TLD server cho ".com".
    * **TLD Servers:** Resolver sau đó sẽ hỏi TLD server cho ".com". TLD server này cũng không biết địa chỉ IP của "www.motvidu.com" nhưng nó biết máy chủ DNS nào chịu trách nhiệm cho tên miền "motvidu.com" (đây gọi là Authoritative Name Server). TLD server sẽ trả về địa chỉ của Authoritative Name Server đó.
    * **Authoritative Name Servers:** Cuối cùng, Resolver sẽ hỏi Authoritative Name Server của "motvidu.com". Máy chủ này chứa thông tin chính xác về tên miền "motvidu.com" và sẽ trả về địa chỉ IP của "www.motvidu.com" cho DNS Resolver.
5.  **Caching DNS:**
    * **Mục đích:** Để tăng tốc độ truy cập cho những lần sau và giảm tải cho các máy chủ DNS, kết quả của việc tra cứu DNS (tức là cặp tên miền - địa chỉ IP) sẽ được lưu trữ tạm thời trong các bộ nhớ đệm (cache).
    * **Các cấp độ caching:**
        * **Trình duyệt:** Lưu trữ trong một khoảng thời gian ngắn.
        * **Hệ điều hành:** Lưu trữ lâu hơn một chút.
        * **DNS Resolver:** Lưu trữ trong khoảng thời gian do bản ghi DNS quy định (thông qua giá trị Time-To-Live - TTL).
    * **Time-To-Live (TTL):** Mỗi bản ghi DNS đều có một giá trị TTL, cho biết thông tin đó có thể được lưu trong cache trong bao lâu. Sau khi hết TTL, lần truy cập tiếp theo sẽ phải thực hiện lại quá trình tra cứu đầy đủ để đảm bảo thông tin luôn được cập nhật.
6.  **Trình duyệt thiết lập kết nối TCP/IP:** Sau khi có được địa chỉ IP, trình duyệt sẽ thiết lập một kết nối TCP (Transmission Control Protocol) đến máy chủ web tại địa chỉ IP đó. Kết nối TCP đảm bảo việc truyền dữ liệu đáng tin cậy giữa trình duyệt và máy chủ. Quá trình này bao gồm "bắt tay ba bước" (three-way handshake).
7.  **Gửi yêu cầu HTTP/HTTPS:**
    * Khi kết nối TCP được thiết lập, trình duyệt sẽ gửi một yêu cầu HTTP (Hypertext Transfer Protocol) hoặc HTTPS (HTTP Secure) đến máy chủ web. Yêu cầu này thường là một lệnh `GET` để yêu cầu nội dung của trang "www.motvidu.com".
    * Yêu cầu này bao gồm các thông tin như phiên bản HTTP, loại trình duyệt, các cookies (nếu có), v.v.
8.  **Máy chủ web xử lý yêu cầu và gửi phản hồi:**
    * Máy chủ web (ví dụ: Apache, Nginx) nhận yêu cầu, xử lý nó (có thể liên quan đến việc truy vấn cơ sở dữ liệu, chạy các script phía máy chủ).
    * Sau đó, máy chủ gửi lại một phản hồi HTTP cho trình duyệt. Phản hồi này bao gồm:
        * **Mã trạng thái HTTP:** Ví dụ, `200 OK` (yêu cầu thành công), `404 Not Found` (không tìm thấy tài nguyên), `301 Moved Permanently` (chuyển hướng), v.v.
        * **Headers:** Chứa thông tin về phản hồi (loại nội dung, độ dài, v.v.).
        * **Nội dung trang web:** Thường là mã HTML, CSS, JavaScript, hình ảnh, v.v.
9.  **Trình duyệt hiển thị trang web:**
    * Trình duyệt nhận phản hồi từ máy chủ.
    * Nó bắt đầu phân tích mã HTML để xây dựng cấu trúc của trang (DOM - Document Object Model).
    * Khi gặp các liên kết đến các tài nguyên khác (CSS, JavaScript, hình ảnh), trình duyệt sẽ lặp lại các bước gửi yêu cầu HTTP cho từng tài nguyên đó (có thể sử dụng lại kết nối TCP hiện có hoặc tạo kết nối mới).
    * CSS được sử dụng để định dạng giao diện.
    * JavaScript được thực thi để thêm các chức năng tương tác cho trang web.
    * Cuối cùng, trang web hoàn chỉnh được hiển thị trên màn hình của người dùng.
10. **Đóng kết nối:** Sau khi các tài nguyên cần thiết đã được tải, kết nối TCP có thể được đóng lại, hoặc giữ lại để tái sử dụng cho các yêu cầu tiếp theo (HTTP Keep-Alive).

**Khái quát ngắn gọn về tra cứu DNS, resolving DNS, caching:**

* **Tra cứu DNS (DNS Lookup):** Là quá trình trình duyệt hoặc hệ thống tìm kiếm địa chỉ IP tương ứng với một tên miền. Nó bắt đầu bằng việc kiểm tra các bộ nhớ đệm cục bộ.
* **Resolving DNS (DNS Resolution):** Là quá trình mà một DNS Resolver (thường của ISP) thực hiện để tìm ra địa chỉ IP cho một tên miền bằng cách truy vấn lần lượt các máy chủ DNS từ Root Server, TLD Server đến Authoritative Name Server. Đây là một quá trình đệ quy.
* **Caching (DNS Caching):** Là việc lưu trữ tạm thời các kết quả tra cứu DNS (tên miền và địa chỉ IP tương ứng) ở nhiều cấp độ khác nhau (trình duyệt, hệ điều hành, DNS resolver) để tăng tốc độ truy cập cho những lần sau và giảm tải cho hệ thống DNS. Thời gian lưu trữ được quyết định bởi giá trị TTL của bản ghi DNS.

**Nguồn tìm hiểu:**

* **Cloudflare:** "What is DNS?" - [https://www.cloudflare.com/learning/dns/what-is-dns/](https://www.cloudflare.com/learning/dns/what-is-dns/)
* **Google Cloud:** "Общие сведения о DNS" (Tổng quan về DNS) - [https://cloud.google.com/dns/docs/overview?hl=vi](https://cloud.google.com/dns/docs/overview?hl=vi)
* **Mozilla Developer Network (MDN Web Docs):** "How the Web works" - [https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/How_the_Web_works](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/How_the_Web_works)
* **Wikipedia:** "Domain Name System" - [https://en.wikipedia.org/wiki/Domain_Name_System](https://en.wikipedia.org/wiki/Domain_Name_System)

---

# Bài tập 2: Viết thuật toán Chord bằng ngôn ngữ tự chọn (Python), viết test case cho thuật toán và viết thành báo cáo

## Báo cáo Thuật toán Chord

**1. Giới thiệu về Chord**

Chord là một giao thức và thuật toán cho một lớp các bảng băm phân tán (Distributed Hash Table - DHT). DHT là một hệ thống lưu trữ khóa-giá trị (key-value) được phân tán trên một mạng các nút (node) ngang hàng (peer-to-peer). Chord nổi bật với sự đơn giản, tính chứng minh được về độ chính xác và hiệu suất, cũng như khả năng tự phục hồi khi các nút tham gia hoặc rời khỏi mạng.

**Đặc điểm chính của Chord:**

* **Không gian định danh (Identifier Space):** Cả nút và khóa đều được gán một định danh (ID) trong một không gian định danh hình tròn có kích thước $2^m$ (ví dụ, sử dụng hàm băm SHA-1, $m=160$).
* **Successor (Nút kế tiếp):** Mỗi nút $n$ chịu trách nhiệm lưu trữ các khóa $k$ sao cho $ID(n)$ là nút đầu tiên có ID lớn hơn hoặc bằng $ID(k)$ theo chiều kim đồng hồ trên vòng tròn Chord. Nút này được gọi là `successor(k)`.
* **Finger Table (Bảng ngón tay):** Để tăng tốc độ tìm kiếm, mỗi nút $n$ duy trì một bảng định tuyến nhỏ gọi là "finger table". Bảng này chứa tối đa $m$ mục. Mục thứ $i$ trong finger table của nút $n$ là nút đầu tiên $s$ kế tiếp $n + 2^{i-1}$ trên vòng tròn Chord (với $1 \le i \le m$). Nút $s$ này được ký hiệu là $n.finger[i].node$.
* **Ổn định mạng (Stabilization):** Chord có các cơ chế để duy trì tính đúng đắn của các con trỏ `successor` và `finger table` khi các nút tham gia hoặc rời mạng.

**2. Ví dụ cụ thể về Chord**

Giả sử chúng ta có một vòng tròn Chord với $m=3$, nghĩa là không gian định danh từ 0 đến $2^3 - 1 = 7$.
Có các nút đang hoạt động với ID: N0, N1, N3, N6.

* **Successors:**
    * `successor(N0)` là N1
    * `successor(N1)` là N3
    * `successor(N3)` là N6
    * `successor(N6)` là N0 (do vòng tròn)

* **Trách nhiệm lưu trữ khóa (ví dụ):**
    * Khóa có ID 2 sẽ được lưu trữ tại N3 (vì N3 là nút đầu tiên $\ge 2$).
    * Khóa có ID 5 sẽ được lưu trữ tại N6.
    * Khóa có ID 7 sẽ được lưu trữ tại N0.

* **Finger Table (ví dụ cho Nút N0, $m=3$):**
    * $i=1$: Tìm nút kế tiếp $(0 + 2^{1-1}) \mod 8 = (0 + 1) \mod 8 = 1$. `N0.finger[1].node` = N1.
    * $i=2$: Tìm nút kế tiếp $(0 + 2^{2-1}) \mod 8 = (0 + 2) \mod 8 = 2$. Nút kế tiếp của 2 là N3. `N0.finger[2].node` = N3.
    * $i=3$: Tìm nút kế tiếp $(0 + 2^{3-1}) \mod 8 = (0 + 4) \mod 8 = 4$. Nút kế tiếp của 4 là N6. `N0.finger[3].node` = N6.

**Luồng tìm kiếm khóa (ví dụ: tìm khóa K5 từ nút N0):**

1.  N0 muốn tìm `successor(K5)`.
2.  N0 kiểm tra `finger table`:
    * `N0.finger[3].node` (N6) có ID là 6. $ID(N0) < ID(K5) \le ID(N6)$ (tức là $0 < 5 \le 6$).
    * N0 sẽ hỏi N6 để tìm `successor(K5)`.
3.  N6 kiểm tra xem K5 có nằm giữa `predecessor(N6)` (là N3) và N6 hay không. Có, $3 < 5 \le 6$.
4.  Vậy N6 là `successor(K5)`.

**3. Code thực nghiệm (Python)**

# [tại đây](https://github.com/namnguyenit/Smart_Park)
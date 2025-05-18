---
title: "Các kiến trúc HPT"
date: "2025-18-5"
updated: "2025-18-5"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/kientruchpt.png"
coverWidth: 16
coverHeight: 9
excerpt:  Các kiến trúc của HPT
---



Chào bạn, dựa trên nội dung tệp PDF bạn cung cấp ("Distributed System notes 7.pdf") và thông tin tìm kiếm được, dưới đây là giải đáp cho các bài tập:

### Bài tập 1: Tìm hiểu sự tương quan và khác biệt giữa các giao thức HTTP, TCP/IP, UDP, REST, GraphQL, SOAP, AJAX, RPC, gRPC.

**Mục đích sử dụng và mối quan hệ của các giao thức:**

#### 1. Các giao thức tầng Giao vận (Transport Layer):

* **TCP (Transmission Control Protocol):**
    * **Mục đích:** Là một giao thức hướng kết nối, đảm bảo việc truyền dữ liệu một cách đáng tin cậy, đúng thứ tự và có kiểm soát luồng. TCP thực hiện kiểm tra lỗi và gửi lại dữ liệu nếu có mất mát.
    * **Sử dụng:** Truyền tải tập tin (FTP), truy cập web (HTTP/HTTPS), email (SMTP).
    * **Mối quan hệ:** TCP là một phần cốt lõi của bộ giao thức TCP/IP. Nhiều giao thức ứng dụng (như HTTP, FTP, SMTP) hoạt động trên nền TCP.

* **UDP (User Datagram Protocol):**
    * **Mục đích:** Là một giao thức không kết nối, truyền dữ liệu nhanh chóng và hiệu quả mà không đảm bảo độ tin cậy, thứ tự gói tin hay kiểm soát luồng.
    * **Sử dụng:** Truyền tải âm thanh/video trực tiếp (streaming), game trực tuyến, DNS, VoIP.
    * **Mối quan hệ:** UDP cũng là một phần của bộ TCP/IP. Các ứng dụng cần tốc độ cao và chấp nhận mất một vài gói tin thường dùng UDP.

#### 2. Giao thức tầng Ứng dụng (Application Layer) và Kiến trúc/Mô hình giao tiếp:

* **HTTP (Hypertext Transfer Protocol):**
    * **Mục đích:** Là giao thức chính được sử dụng để truyền tải siêu văn bản (ví dụ: trang web) giữa client (trình duyệt) và server. HTTP hoạt động theo mô hình yêu cầu-phản hồi.
    * **Sử dụng:** Duyệt web, API web.
    * **Mối quan hệ:** HTTP thường chạy trên nền TCP để đảm bảo việc truyền dữ liệu đáng tin cậy. REST APIs thường sử dụng HTTP làm giao thức truyền tải.

* **TCP/IP (Transmission Control Protocol/Internet Protocol):**
    * **Mục đích:** Là một bộ giao thức truyền thông nền tảng của Internet, định nghĩa cách dữ liệu được đóng gói, định địa chỉ, truyền, định tuyến và nhận tại đích.
    * **Sử dụng:** Nền tảng cho hầu hết các giao tiếp mạng và Internet.
    * **Mối quan hệ:** TCP và UDP là các giao thức chính trong tầng giao vận của mô hình TCP/IP. IP (Internet Protocol) chịu trách nhiệm định địa chỉ và định tuyến gói tin ở tầng mạng.

* **REST (Representational State Transfer):**
    * **Mục đích:** Là một kiểu kiến trúc (architectural style) để thiết kế các ứng dụng mạng phân tán, đặc biệt là các dịch vụ web (web services). REST sử dụng các phương thức HTTP tiêu chuẩn (GET, POST, PUT, DELETE) để thao tác với tài nguyên được xác định bởi URI.
    * **Sử dụng:** Xây dựng API cho các ứng dụng web và di động, microservices.
    * **Mối quan hệ:** REST không phải là một giao thức mà là một tập hợp các ràng buộc kiến trúc. API REST thường sử dụng HTTP làm giao thức truyền tải và có thể sử dụng các định dạng dữ liệu như JSON hoặc XML.

* **GraphQL:**
    * **Mục đích:** Là một ngôn ngữ truy vấn cho API và một runtime phía máy chủ để thực thi các truy vấn đó. GraphQL cho phép client yêu cầu chính xác dữ liệu mình cần, tránh việc thừa hoặc thiếu dữ liệu như thường gặp ở REST API truyền thống.
    * **Sử dụng:** Các ứng dụng phức tạp với nhiều nguồn dữ liệu, ứng dụng di động cần tối ưu băng thông.
    * **Mối quan hệ:** GraphQL thường được truyền tải qua HTTP (thường là một endpoint duy nhất cho tất cả các truy vấn). Nó là một giải pháp thay thế hoặc bổ sung cho REST.

* **SOAP (Simple Object Access Protocol):**
    * **Mục đích:** Là một giao thức dựa trên XML để trao đổi thông tin có cấu trúc trong việc triển khai các dịch vụ web. SOAP có các tiêu chuẩn nghiêm ngặt về định dạng thông điệp và bảo mật (WS-Security).
    * **Sử dụng:** Các ứng dụng doanh nghiệp đòi hỏi tính bảo mật cao, giao dịch, và tích hợp với các hệ thống cũ đã sử dụng SOAP.
    * **Mối quan hệ:** SOAP thường sử dụng HTTP làm giao thức truyền tải, nhưng cũng có thể hoạt động trên các giao thức khác. Nó khác với REST ở chỗ REST là kiểu kiến trúc còn SOAP là một giao thức cụ thể.

* **AJAX (Asynchronous JavaScript and XML):**
    * **Mục đích:** Là một tập hợp các kỹ thuật phát triển web cho phép các ứng dụng web gửi và nhận dữ liệu từ máy chủ một cách không đồng bộ (trong nền) mà không cần tải lại toàn bộ trang.
    * **Sử dụng:** Tạo các ứng dụng web tương tác và động hơn.
    * **Mối quan hệ:** AJAX sử dụng đối tượng `XMLHttpRequest` (hoặc `Workspace API` hiện đại hơn) trong JavaScript để thực hiện các yêu cầu HTTP đến máy chủ. Dữ liệu trao đổi có thể là XML (như tên gọi ban đầu) nhưng ngày nay phổ biến hơn là JSON. AJAX thường được sử dụng trong các ứng dụng client-side để tương tác với REST API hoặc GraphQL API.

* **RPC (Remote Procedure Call):**
    * **Mục đích:** Là một mô hình cho phép một chương trình thực thi một thủ tục (hàm hoặc phương thức) trên một không gian địa chỉ khác (thường là trên một máy tính khác) như thể nó là một lời gọi thủ tục cục bộ.
    * **Sử dụng:** Giao tiếp giữa các thành phần trong hệ thống phân tán, microservices.
    * **Mối quan hệ:** RPC là một khái niệm tổng quát. Có nhiều hiện thực RPC khác nhau. RPC có thể sử dụng TCP hoặc UDP làm giao thức truyền tải. gRPC là một hiện thực cụ thể của RPC.

* **gRPC (Google Remote Procedure Call):**
    * **Mục đích:** Là một framework RPC hiện đại, hiệu năng cao, mã nguồn mở do Google phát triển. Nó sử dụng HTTP/2 để truyền tải, Protocol Buffers (Protobuf) làm ngôn ngữ mô tả giao diện (IDL) và định dạng tuần tự hóa dữ liệu nhị phân.
    * **Sử dụng:** Giao tiếp giữa các microservices hiệu suất cao, truyền dữ liệu streaming thời gian thực, các ứng dụng yêu cầu độ trễ thấp và thông lượng cao.
    * **Mối quan hệ:** gRPC là một hiện thực của RPC. Nó được xây dựng dựa trên HTTP/2 và Protobuf. So với REST, gRPC thường nhanh hơn và hiệu quả hơn cho giao tiếp nội bộ giữa các service do sử dụng định dạng nhị phân và HTTP/2.

**Tóm tắt sự tương quan và khác biệt chính:**

* **TCP/IP và UDP** là các giao thức tầng giao vận. TCP đảm bảo độ tin cậy, UDP ưu tiên tốc độ.
* **HTTP** là giao thức tầng ứng dụng, thường chạy trên TCP, dùng để duyệt web và làm nền tảng cho nhiều API.
* **REST** là một kiểu kiến trúc API, thường sử dụng HTTP và JSON/XML. Nó linh hoạt và phổ biến.
* **GraphQL** là một ngôn ngữ truy vấn API, cho phép client yêu cầu dữ liệu cụ thể, thường chạy trên HTTP.
* **SOAP** là một giao thức API dựa trên XML, có tiêu chuẩn chặt chẽ, thường dùng cho các ứng dụng doanh nghiệp yêu cầu bảo mật cao.
* **AJAX** là kỹ thuật phía client để giao tiếp bất đồng bộ với server (thường qua HTTP để gọi REST/GraphQL API).
* **RPC** là mô hình gọi thủ tục từ xa.
* **gRPC** là một framework RPC hiệu năng cao, sử dụng HTTP/2 và Protocol Buffers, rất phù hợp cho microservices.

Các giao thức này có thể được sử dụng kết hợp với nhau. Ví dụ, một ứng dụng web có thể sử dụng AJAX ở phía client để gọi một GraphQL API, API này được phục vụ qua HTTP, và HTTP lại chạy trên TCP/IP. Bên trong backend, các microservices có thể giao tiếp với nhau qua gRPC.

### Bài tập 2: Nghiên cứu về thư viện OpenMPI.

**Thư viện OpenMPI có tính năng gì và có những hàm nào để sử dụng?**

* **OpenMPI là gì?**
    * OpenMPI (Open Message Passing Interface) là một dự án mã nguồn mở cung cấp một hiện thực (implementation) chất lượng cao, đầy đủ tính năng của tiêu chuẩn MPI (Message Passing Interface). MPI là một đặc tả thư viện chuẩn cho việc lập trình song song sử dụng mô hình truyền thông điệp (message passing), cho phép các tiến trình (processes) chạy trên các máy tính khác nhau (hoặc các core khác nhau trên cùng một máy) trao đổi dữ liệu với nhau.
    * Nó được thiết kế để đạt hiệu năng cao, có thể mở rộng và linh hoạt trên nhiều nền tảng phần cứng và hệ điều hành khác nhau.

* **Tính năng chính của OpenMPI:**
    * **Tuân thủ tiêu chuẩn MPI:** Hỗ trợ đầy đủ các phiên bản của tiêu chuẩn MPI.
    * **Hiệu năng cao:** Tối ưu hóa cho nhiều loại mạng và kiến trúc hệ thống khác nhau.
    * **Khả chuyển (Portability):** Hoạt động trên nhiều hệ điều hành (Linux, macOS, Windows...) và kiến trúc phần cứng (32-bit, 64-bit).
    * **Khả năng mở rộng (Scalability):** Hỗ trợ chạy các ứng dụng song song trên số lượng lớn các tiến trình và nút mạng.
    * **Thiết kế dựa trên component:** Cho phép tùy chỉnh và mở rộng dễ dàng.
    * **Hỗ trợ nhiều loại mạng giao tiếp:** TCP/IP, InfiniBand, shared memory, v.v.
    * **Hỗ trợ lập trình lai (Hybrid Programming):** Kết hợp MPI với các mô hình lập trình song song khác như OpenMP.
    * **Công cụ gỡ lỗi và phân tích hiệu năng:** Tích hợp với các công cụ của bên thứ ba.

* **Một số hàm (functions) MPI cơ bản và thường dùng (OpenMPI cung cấp hiện thực cho các hàm này):**
    * **Khởi tạo và kết thúc môi trường MPI:**
        * `MPI_Init(int *argc, char ***argv)`: Khởi tạo môi trường MPI. Phải được gọi đầu tiên trong mọi chương trình MPI.
        * `MPI_Finalize()`: Kết thúc môi trường MPI. Phải được gọi cuối cùng.
    * **Quản lý tiến trình (Communicator Management):**
        * `MPI_Comm_size(MPI_Comm comm, int *size)`: Lấy tổng số tiến trình trong một communicator (ví dụ: `MPI_COMM_WORLD` là communicator chứa tất cả các tiến trình).
        * `MPI_Comm_rank(MPI_Comm comm, int *rank)`: Lấy định danh (rank) của tiến trình đang gọi hàm trong một communicator. Rank là một số nguyên từ 0 đến `size-1`.
    * **Truyền thông điệp điểm-điểm (Point-to-Point Communication):**
        * `MPI_Send(const void *buf, int count, MPI_Datatype datatype, int dest, int tag, MPI_Comm comm)`: Gửi một thông điệp từ tiến trình hiện tại đến một tiến trình đích (`dest`).
        * `MPI_Recv(void *buf, int count, MPI_Datatype datatype, int source, int tag, MPI_Comm comm, MPI_Status *status)`: Nhận một thông điệp từ một tiến trình nguồn (`source`).
    * **Truyền thông điệp tập thể (Collective Communication):**
        * `MPI_Bcast(void *buffer, int count, MPI_Datatype datatype, int root, MPI_Comm comm)`: Phát một thông điệp từ tiến trình `root` đến tất cả các tiến trình khác trong communicator.
        * `MPI_Scatter(const void *sendbuf, int sendcount, MPI_Datatype sendtype, void *recvbuf, int recvcount, MPI_Datatype recvtype, int root, MPI_Comm comm)`: Tiến trình `root` chia dữ liệu trong `sendbuf` thành các phần bằng nhau và gửi mỗi phần cho một tiến trình trong communicator (bao gồm cả chính nó).
        * `MPI_Gather(const void *sendbuf, int sendcount, MPI_Datatype sendtype, void *recvbuf, int recvcount, MPI_Datatype recvtype, int root, MPI_Comm comm)`: Mỗi tiến trình gửi dữ liệu từ `sendbuf` của mình đến tiến trình `root`. Tiến trình `root` tập hợp các dữ liệu này vào `recvbuf`.
        * `MPI_Reduce(const void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype, MPI_Op op, int root, MPI_Comm comm)`: Kết hợp dữ liệu từ tất cả các tiến trình bằng một phép toán (`op` như `MPI_SUM`, `MPI_MAX`) và lưu kết quả vào `recvbuf` trên tiến trình `root`.
        * `MPI_Allreduce(const void *sendbuf, void *recvbuf, int count, MPI_Datatype datatype, MPI_Op op, MPI_Comm comm)`: Tương tự `MPI_Reduce` nhưng kết quả được gửi đến tất cả các tiến trình.
    * **Đo thời gian:**
        * `MPI_Wtime()`: Trả về thời gian hiện tại (thường tính bằng giây). Dùng để đo thời gian thực thi.

**Suy nghĩ về giải pháp sử dụng hệ phân tán trong bài toán: Tính 10,000,000 số nguyên tố đầu tiên với 16 máy, mỗi máy có 2 core (tổng 32 core). Làm thế nào để có thể đưa ra đáp án đúng và nhanh nhất và có thể sử dụng linh hoạt số nhân, ví dụ 8 core, 10 core, 12 core đều đưa ra được kết quả tương tự.**

Bài toán này yêu cầu tìm N (ở đây là 10,000,000) số nguyên tố đầu tiên. Đây là một bài toán khác với việc tìm các số nguyên tố *trong một khoảng* nhất định (ví dụ từ 1 đến $M$). Để tìm N số nguyên tố đầu tiên, chúng ta không biết trước cận trên $M$ của khoảng cần xét.

**Ý tưởng giải pháp sử dụng Sàng Eratosthenes phân tán với MPI:**

Do chúng ta cần tìm *số lượng* số nguyên tố chứ không phải trong một khoảng cố định, thuật toán Sàng Eratosthenes truyền thống (cần biết cận trên $N$) sẽ cần điều chỉnh.

1.  **Ước lượng cận trên ($M$):**
    * Cần một ước lượng ban đầu cho giá trị $M$ sao cho khoảng từ 1 đến $M$ chứa ít nhất 10,000,000 số nguyên tố. Có các công thức xấp xỉ số lượng số nguyên tố nhỏ hơn $N$ ($\pi(N) \approx N/\ln(N)$). Từ đó, ta có thể ước lượng $P_n \approx n \ln(n) + n \ln(\ln(n))$ với $P_n$ là số nguyên tố thứ n. Ví dụ, số nguyên tố thứ 10,000,000 sẽ vào khoảng $1.79 \times 10^8$. Nên chọn một cận trên $M$ lớn hơn một chút giá trị này để đảm bảo.
    * Nếu sau khi sàng trong khoảng [2, $M$] mà chưa đủ 10,000,000 số nguyên tố, chúng ta cần mở rộng khoảng sàng (tăng $M$) và tiếp tục.

2.  **Phân chia công việc cho Sàng Eratosthenes:**
    * **Tiến trình chủ (Master - rank 0):**
        * Xác định cận trên $M$ ban đầu cần sàng.
        * Chia khoảng số [2, $M$] thành các đoạn con (sub-ranges) gần bằng nhau, mỗi đoạn cho một tiến trình thợ (worker) xử lý. Ví dụ, nếu có P tiến trình, mỗi tiến trình worker sẽ xử lý một đoạn có kích thước khoảng ($M$-1)/P.
        * Gửi thông tin về đoạn con (điểm bắt đầu, điểm kết thúc) cho từng tiến trình thợ.
        * **Thu thập kết quả:** Sau khi các thợ sàng xong đoạn của mình, tiến trình chủ sẽ thu thập danh sách các số nguyên tố tìm được từ mỗi thợ.
        * **Tổng hợp và kiểm tra:** Ghép các danh sách lại, sắp xếp (nếu cần) và đếm tổng số số nguyên tố. Nếu chưa đủ 10,000,000, tăng $M$ và lặp lại quá trình sàng cho khoảng mới (chỉ cần sàng phần mở rộng và cẩn thận với các số đã sàng). Hoặc, một cách tiếp cận khác là mỗi worker tiếp tục sàng các khối số tiếp theo cho đến khi tổng số lượng tìm được đủ.

    * **Các tiến trình thợ (Workers - rank 1 đến P-1):**
        * Nhận đoạn số \[start_i, end_i] từ tiến trình chủ.
        * Thực hiện thuật toán Sàng Eratosthenes trên đoạn số của mình. Để làm điều này hiệu quả:
            * Mỗi worker cần danh sách các số nguyên tố cơ sở để sàng (ví dụ, các số nguyên tố nhỏ hơn hoặc bằng $\sqrt{M}$). Danh sách này có thể được tính trước bởi tiến trình chủ và phát (broadcast) cho tất cả các worker, hoặc mỗi worker tự tính cho phần đầu của dải số.
            * Worker i sẽ đánh dấu các bội của các số nguyên tố cơ sở trong đoạn \[start_i, end_i] của nó.
        * Sau khi sàng xong, worker tạo danh sách các số nguyên tố tìm được trong đoạn của mình.
        * Gửi danh sách này về cho tiến trình chủ.

3.  **Cách tìm 10,000,000 số nguyên tố đầu tiên (thay vì trong khoảng cố định):**
    * **Cách 1: Sàng theo từng khối lớn, kiểm tra và mở rộng:**
        1.  Master chọn một cận trên ${M}_k$ ban đầu (ví dụ, $2 \times 10^8$).
        2.  Phân chia đoạn \[2, ${M}_k$] cho các worker để sàng song song.
        3.  Các worker gửi lại số lượng số nguyên tố và các số nguyên tố tìm được trong phần của mình.
        4.  Master tổng hợp lại. Nếu tổng số lượng đã đủ 10,000,000 thì lấy 10,000,000 số đầu tiên và kết thúc.
        5.  Nếu chưa đủ, Master tăng ${M}_k$ (ví dụ, ${M}_{k+1} = {M}_k + \Delta M$) và yêu cầu các worker sàng tiếp trong khoảng \[${M}_k+1$, ${M}_{k+1}$]. Quá trình này cần cẩn thận để các worker sử dụng các số nguyên tố đã tìm được ở bước trước để sàng hiệu quả.
    * **Cách 2: Phân phối động các khối nhỏ hơn:**
        1.  Master chia một khoảng số lớn (ví dụ, đến $2 \times 10^9$ hoặc hơn) thành nhiều khối nhỏ (chunks).
        2.  Master gửi từng khối cho các worker còn rảnh.
        3.  Mỗi worker sàng khối nhận được, tìm các số nguyên tố và gửi về cho Master.
        4.  Master thu thập, đếm tổng số nguyên tố tìm được. Khi đủ 10,000,000 thì báo cho các worker dừng và kết thúc. Cách này linh hoạt hơn nếu tốc độ xử lý của các core/máy khác nhau.

4.  **Đảm bảo tính đúng đắn và nhanh nhất:**
    * **Đúng đắn:** Thuật toán Sàng Eratosthenes là thuật toán chính xác. Việc chia nhỏ đoạn và tổng hợp kết quả cần được thực hiện cẩn thận để không bỏ sót hoặc tính trùng.
    * **Nhanh nhất:**
        * Phân chia công việc đều: Chia đoạn số [2, $M$] một cách hợp lý cho các core.
        * Giảm thiểu giao tiếp: Giao tiếp giữa các tiến trình (đặc biệt là `MPI_Send`, `MPI_Recv` nhiều lần) tốn thời gian. Cố gắng để mỗi worker làm nhiều việc nhất có thể trước khi gửi kết quả. Sử dụng các hàm tập thể như `MPI_Bcast` (để phát các số nguyên tố cơ sở), `MPI_Gather` hoặc `MPI_Reduce` (để thu thập số lượng/danh sách) có thể hiệu quả hơn.
        * Tối ưu Sàng Eratosthenes cục bộ: Mỗi worker nên thực hiện sàng hiệu quả trên đoạn của mình (ví dụ, chỉ xét các số lẻ, bắt đầu đánh dấu từ bình phương của số nguyên tố).

5.  **Sử dụng linh hoạt số nhân (8, 10, 12, ..., 32 cores):**
    * Chương trình MPI được viết để hoạt động với một số lượng tiến trình bất kỳ (trong giới hạn tài nguyên hệ thống).
    * Khi chạy chương trình MPI bằng lệnh `mpirun` (hoặc `mpiexec`), bạn có thể chỉ định số lượng tiến trình (tương ứng với số core muốn sử dụng) bằng tham số `-np`. Ví dụ:
        * `mpirun -np 8 ./prime_calculator` (chạy trên 8 core)
        * `mpirun -np 16 ./prime_calculator`
        * `mpirun -np 32 ./prime_calculator`
    * Bên trong mã nguồn MPI, các hàm `MPI_Comm_size()` và `MPI_Comm_rank()` sẽ tự động cung cấp thông tin về tổng số tiến trình đang chạy và rank của tiến trình hiện tại. Thuật toán phân chia công việc (ví dụ, chia đoạn [2, $M$]) sẽ dựa trên `size` này để chia đều công việc.
    * **Hostfile/Machinefile:** Để chạy trên 16 máy, mỗi máy 2 core, bạn cần cấu hình một hostfile cho `mpirun` để nó biết các máy nào có sẵn và số core (slots) trên mỗi máy có thể sử dụng. OpenMPI sẽ cố gắng phân bổ các tiến trình một cách tối ưu dựa trên thông tin này. Ví dụ, nếu hostfile chỉ định 16 máy, mỗi máy có `slots=2`, thì khi chạy với `-np 32`, OpenMPI sẽ cố gắng khởi chạy 2 tiến trình trên mỗi máy. Nếu bạn chạy với `-np 16`, nó có thể chạy 1 tiến trình trên mỗi máy.
    * **Binding processes to cores:** OpenMPI có các tùy chọn để kiểm soát cách các tiến trình MPI được gán (bind) vào các core cụ thể (ví dụ: `--bind-to core`). Điều này có thể quan trọng để đạt hiệu năng tối ưu, tránh việc các tiến trình di chuyển giữa các core hoặc bị tranh chấp tài nguyên cache.

**Các hàm MPI có thể sử dụng cho bài toán này:**

* `MPI_Init`, `MPI_Finalize`
* `MPI_Comm_size`, `MPI_Comm_rank`
* `MPI_Bcast` (để master gửi cận trên $M$, hoặc các số nguyên tố cơ sở cho các worker)
* `MPI_Scatter` (để master phân chia các đoạn con của khoảng [2,$M$] cho các worker)
* `MPI_Gather` (để các worker gửi danh sách số nguyên tố cục bộ của chúng về master) hoặc `MPI_Gatherv` (nếu số lượng số nguyên tố mỗi worker tìm được khác nhau nhiều).
* `MPI_Reduce` (với `MPI_SUM` để master tính tổng số lượng số nguyên tố mà các worker đã tìm được, hoặc với `MPI_PROD` để kiểm tra xem tất cả đã hoàn thành một giai đoạn chưa).
* `MPI_Send`, `MPI_Recv` (cho việc giao tiếp linh hoạt hơn nếu cần, ví dụ master gửi các khối công việc động).
* `MPI_Barrier` (để đồng bộ hóa các tiến trình tại một số điểm nếu cần, nhưng nên hạn chế vì có thể làm giảm hiệu năng).
* `MPI_Wtime` (để đo thời gian thực thi).

Bằng cách thiết kế thuật toán phân chia công việc dựa trên tổng số tiến trình (`size`) thu được từ `MPI_Comm_size`, chương trình có thể tự động điều chỉnh để chạy hiệu quả với số lượng core (tiến trình) khác nhau được chỉ định khi thực thi.
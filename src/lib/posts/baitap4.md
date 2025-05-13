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






# Bài tập 1: Diễn giải quy trình duyệt một trang web www.motvidu.com

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

```python
import hashlib

class ChordNode:
    def __init__(self, node_id, m):
        self.id = node_id
        self.m = m  # Số bit của không gian định danh
        self.finger_table = [None] * m
        self.successor = self
        self.predecessor = None
        self.data = {} # Lưu trữ key-value

    def __repr__(self):
        return f"Node({self.id})"

    def get_id_as_int(self):
        return self.id

    def _get_hash(self, key_str):
        """Tạo hash cho một key (chuỗi) và trả về giá trị int trong không gian ID."""
        if isinstance(key_str, int):
            return key_str % (2**self.m)
        sha1 = hashlib.sha1()
        sha1.update(key_str.encode('utf-8'))
        # hash_val = int(sha1.hexdigest(), 16)
        # return hash_val % (2**self.m)
        raise NotImplementedError("Hashing string keys not fully implemented for simplicity. Pass integer IDs.")


    def in_interval(self, key_id, start_id, end_id, include_start=False, include_end=True):
        """
        Kiểm tra xem key_id có nằm trong khoảng (start_id, end_id] trên vòng tròn Chord không.
        start_id và end_id là ID của các nút.
        """
        max_id = 2**self.m
        key_id = key_id % max_id
        start_id = start_id % max_id
        end_id = end_id % max_id

        if start_id == end_id:
            return include_start or include_end

        if start_id < end_id:
            if include_start and include_end:
                return start_id <= key_id <= end_id
            elif include_start:
                return start_id <= key_id < end_id
            elif include_end:
                return start_id < key_id <= end_id
            else:
                return start_id < key_id < end_id
        else: # start_id > end_id (vòng qua 0)
            if include_start and include_end:
                return (start_id <= key_id < max_id) or (0 <= key_id <= end_id)
            elif include_start:
                return (start_id <= key_id < max_id) or (0 <= key_id < end_id)
            elif include_end:
                 return (start_id < key_id < max_id) or (0 <= key_id <= end_id)
            else:
                return (start_id < key_id < max_id) or (0 < key_id < end_id)


    def find_successor(self, key_id_to_find):
        """Tìm nút chịu trách nhiệm cho key_id_to_find."""
        if self.predecessor and self.in_interval(key_id_to_find, self.predecessor.id, self.id, include_start=False, include_end=True):
            return self
        if self.in_interval(key_id_to_find, self.id, self.successor.id, include_start=False, include_end=True):
            return self.successor
        else:
            n_prime = self.closest_preceding_finger(key_id_to_find)
            if n_prime == self:
                return self.successor
            return n_prime.find_successor(key_id_to_find)

    def closest_preceding_finger(self, key_id_to_find):
        """Tìm nút trong finger table gần nhất và đứng trước key_id_to_find."""
        for i in range(self.m - 1, -1, -1):
            finger_node = self.finger_table[i]
            if finger_node:
                if self.in_interval(finger_node.id, self.id, key_id_to_find, include_start=False, include_end=False):
                    return finger_node
        return self

    def join(self, existing_node=None):
        """Nút hiện tại tham gia vào mạng Chord."""
        if existing_node:
            self.successor = existing_node.find_successor(self.id)
            if self.successor:
                 self.successor.notify(self)

    def stabilize(self):
        """Được gọi định kỳ để kiểm tra và cập nhật successor."""
        if not self.successor:
            self.successor = self
            self.predecessor = self
            for i in range(self.m):
                self.finger_table[i] = self
            return

        x = self.successor.predecessor
        if x and self.in_interval(x.id, self.id, self.successor.id, include_start=False, include_end=False):
            self.successor = x
        if self.successor:
            self.successor.notify(self)

    def notify(self, potential_predecessor):
        """Được gọi bởi potential_predecessor."""
        if self.predecessor is None or \
           self.in_interval(potential_predecessor.id, self.predecessor.id, self.id, include_start=False, include_end=False):
            self.predecessor = potential_predecessor

    def fix_fingers(self):
        """Được gọi định kỳ để làm mới các mục trong finger table."""
        if not self.successor :
            for i in range(self.m):
                self.finger_table[i] = self
            return

        for i in range(self.m):
            finger_start_id = (self.id + 2**i) % (2**self.m)
            self.finger_table[i] = self.find_successor(finger_start_id)

    def store_value(self, key, value):
        """Lưu trữ một cặp key-value. Key ở đây là ID đã được hash."""
        target_node = self.find_successor(key)
        target_node.data[key] = value

    def retrieve_value(self, key):
        """Truy xuất giá trị cho một key. Key ở đây là ID đã được hash."""
        target_node = self.find_successor(key)
        return target_node.data.get(key, None)

# --- Helper functions for simulation/testing ---
def create_ring(node_ids, m):
    """Tạo một vòng Chord với các nút đã cho và thiết lập successor/predecessor ban đầu."""
    if not node_ids:
        return []
    nodes = sorted([ChordNode(nid, m) for nid in node_ids])
    num_nodes = len(nodes)
    for i in range(num_nodes):
        nodes[i].successor = nodes[(i + 1) % num_nodes]
        nodes[i].predecessor = nodes[(i - 1 + num_nodes) % num_nodes]
    for node in nodes:
        node.fix_fingers()
    return nodes

def run_stabilization_rounds(nodes, rounds=3):
    """Chạy các vòng stabilize và fix_fingers."""
    if not nodes: return
    for r in range(rounds):
        for node in nodes:
            node.stabilize()
        for node in nodes:
            node.fix_fingers()

def print_chord_ring_state(nodes):
    if not nodes:
        print("Ring is empty.")
        return
    print("\n===== Chord Ring State =====")
    for node in sorted(nodes, key=lambda n: n.id):
        pred_id = node.predecessor.id if node.predecessor else "None"
        succ_id = node.successor.id if node.successor else "None"
        print(f"Node {node.id}:")
        print(f"  Successor: {succ_id}, Predecessor: {pred_id}")
        finger_str = ", ".join([f"{idx}:{(f.id if f else 'N')}" for idx, f in enumerate(node.finger_table)])
        print(f"  Finger Table ({node.m} bits): [{finger_str}]")
        print(f"  Data: {node.data}")
    print("==========================\n")

# ----------------- Test Cases -----------------
def run_chord_tests():
    print("--- Test Case 1: Basic Ring (m=3, nodes 0, 1, 3, 6) ---")
    m_bits = 3
    node_ids1 = [0, 1, 3, 6]
    sorted_node_ids1 = sorted(list(set(node_ids1)))
    nodes_map1 = {nid: ChordNode(nid, m_bits) for nid in sorted_node_ids1}
    nodes_list1 = [nodes_map1[nid] for nid in sorted_node_ids1]

    num_n = len(nodes_list1)
    for i in range(num_n):
        nodes_list1[i].successor = nodes_list1[(i + 1) % num_n]
        nodes_list1[i].predecessor = nodes_list1[(i - 1 + num_n) % num_n]

    for node in nodes_list1:
        node.fix_fingers()
    print_chord_ring_state(nodes_list1)

    print("--- Testing find_successor ---")
    start_node = nodes_map1[sorted_node_ids1[0]]

    key_to_find1 = 2
    print(f"Finding successor for key {key_to_find1} starting from {start_node}:")
    successor_node1 = start_node.find_successor(key_to_find1)
    print(f"  > Expected: Node 3, Got: {successor_node1}")
    assert successor_node1.id == 3

    key_to_find2 = 7
    print(f"Finding successor for key {key_to_find2} starting from {start_node}:")
    successor_node2 = start_node.find_successor(key_to_find2)
    print(f"  > Expected: Node 0, Got: {successor_node2}")
    assert successor_node2.id == 0

    key_to_find3 = 5
    print(f"Finding successor for key {key_to_find3} (should be Node 6) starting from Node {nodes_map1[1]}:")
    successor_node3 = nodes_map1[1].find_successor(key_to_find3)
    print(f"  > Expected: Node 6, Got: {successor_node3}")
    assert successor_node3.id == 6

    print("\n--- Testing store_value and retrieve_value ---")
    print(f"Storing key=2, value='data_for_2' from {start_node}")
    start_node.store_value(2, "data_for_2")
    assert nodes_map1[3].data.get(2) == "data_for_2"

    print(f"Storing key=7, value='data_for_7' from {start_node}")
    start_node.store_value(7, "data_for_7")
    assert nodes_map1[0].data.get(7) == "data_for_7"

    print(f"Retrieving key=2 from {nodes_map1[6]}")
    retrieved_val1 = nodes_map1[6].retrieve_value(2)
    print(f"  > Expected: 'data_for_2', Got: {retrieved_val1}")
    assert retrieved_val1 == "data_for_2"

    print(f"Retrieving key=7 from {nodes_map1[1]}")
    retrieved_val2 = nodes_map1[1].retrieve_value(7)
    print(f"  > Expected: 'data_for_7', Got: {retrieved_val2}")
    assert retrieved_val2 == "data_for_7"

    print(f"Retrieving non-existent key=4 from {start_node}")
    retrieved_val_none = start_node.retrieve_value(4)
    print(f"  > Expected: None, Got: {retrieved_val_none}")
    assert retrieved_val_none is None
    print_chord_ring_state(nodes_list1)

    print("\n--- Test Case 2: Larger Ring (m=5, nodes 3, 10, 15, 20, 28) ---")
    m_bits2 = 5
    node_ids2 = [3, 10, 15, 20, 28]
    sorted_node_ids2 = sorted(list(set(node_ids2)))
    nodes_map2 = {nid: ChordNode(nid, m_bits2) for nid in sorted_node_ids2}
    nodes_list2 = [nodes_map2[nid] for nid in sorted_node_ids2]

    num_n2 = len(nodes_list2)
    for i in range(num_n2):
        nodes_list2[i].successor = nodes_list2[(i + 1) % num_n2]
        nodes_list2[i].predecessor = nodes_list2[(i - 1 + num_n2) % num_n2]

    run_stabilization_rounds(nodes_list2, rounds=m_bits2)
    print_chord_ring_state(nodes_list2)

    start_node2 = nodes_map2[sorted_node_ids2[0]]

    key_to_find_tc2_1 = 12
    print(f"Finding successor for key {key_to_find_tc2_1} starting from {start_node2}:")
    successor_node_tc2_1 = start_node2.find_successor(key_to_find_tc2_1)
    print(f"  > Expected: Node 15, Got: {successor_node_tc2_1}")
    assert successor_node_tc2_1.id == 15

    key_to_find_tc2_2 = 30
    print(f"Finding successor for key {key_to_find_tc2_2} starting from {start_node2}:")
    successor_node_tc2_2 = start_node2.find_successor(key_to_find_tc2_2)
    print(f"  > Expected: Node 3, Got: {successor_node_tc2_2}")
    assert successor_node_tc2_2.id == 3

    key_to_find_tc2_3 = 0
    print(f"Finding successor for key {key_to_find_tc2_3} starting from {nodes_map2[28]}:")
    successor_node_tc2_3 = nodes_map2[28].find_successor(key_to_find_tc2_3)
    print(f"  > Expected: Node 3, Got: {successor_node_tc2_3}")
    assert successor_node_tc2_3.id == 3

    print(f"Storing key=18, value='data_for_18' from {start_node2}")
    start_node2.store_value(18, "data_for_18")
    assert nodes_map2[20].data.get(18) == "data_for_18"

    print(f"Retrieving key=18 from {nodes_map2[10]}")
    retrieved_val_tc2 = nodes_map2[10].retrieve_value(18)
    print(f"  > Expected: 'data_for_18', Got: {retrieved_val_tc2}")
    assert retrieved_val_tc2 == "data_for_18"
    print_chord_ring_state(nodes_list2)

    print("\n--- Test Case 3: Single Node Ring (m=3, node 5) ---")
    m_bits3 = 3
    node_ids3 = [5]
    nodes_map3 = {nid: ChordNode(nid, m_bits3) for nid in node_ids3}
    single_node = nodes_map3[5]

    single_node.successor = single_node
    single_node.predecessor = single_node
    single_node.fix_fingers()
    print_chord_ring_state([single_node])

    key_to_find_tc3_1 = 2
    print(f"Finding successor for key {key_to_find_tc3_1} starting from {single_node}:")
    successor_node_tc3_1 = single_node.find_successor(key_to_find_tc3_1)
    print(f"  > Expected: Node 5, Got: {successor_node_tc3_1}")
    assert successor_node_tc3_1.id == 5

    single_node.store_value(2, "data_single_2")
    assert single_node.data.get(2) == "data_single_2"
    retrieved_val_tc3 = single_node.retrieve_value(2)
    assert retrieved_val_tc3 == "data_single_2"
    print_chord_ring_state([single_node])

    print("\nAll tests completed.")

if __name__ == "__main__":
    run_chord_tests()
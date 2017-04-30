## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **30/04/2017**

### Mục lục

[I .Network layer](#I)

- [1. Design Issues](#1)

	- [1.1 Store-and-forward packet switching ](#1.1)
	- [1.2 Connectionless service – datagrams](#1.2)
	- [1.3 Connection-oriented service – virtual circuits](#1.3)
	- [1.4 Comparison of virtual-circuits and datagrams ](#1.4)

- [2. Routing Algorithms](#2)

	- [2.1 Routing Algorithms](#2.1)
	- [2.2. The Optimality Principle](#2.2)
	- [2.3. Shortest Path Algorithm ](#2.3)
	- [2.4 Flooding](#2.4)
	- [2.5 Distance Vector Routing ](#2.5)
	- [2.6. The Count-to-Infinity Problem](#2.6)
	- [2.7. Link State Routing ](#2.7)
	- [2.8. Hierarchical Routing](#2.8)
	- [2.9. Broadcast Routing](#2.9)
	- [2.10. Multicast Routing ](#2.10)
	- [2.11. Anycast Routing](#2.11)
	- [2.12. Routing for Mobile Hosts](#2.12)
	- [2.13. Routing in Ad Hoc Networks](#2.13)
	- [2.14. Why Routing matters](#2.14)
	- [2.15. First Class Test ](#2.15)

- [3. Congestion Control](#3)

	- [3.1. Approaches ](#3.1)
	- [3.2. Traffic-Aware Routing](#3.2)
	- [3.3. Admission Control](#3.3)
	- [3.4. Congestion Control Summary](#3.4)
	- [3.5. Traffic Throttling ](#3.5)
	- [3.6. Load Shedding ](#3.6)

- [4. Quality of Service](#4)

	- [4.1 Application requirements](#4.1)
	- [4.2. Traffic shaping](#4.2)
	- [4.3. Packet scheduling](#4.3)
	- [4.4. Admission control](#4.4)
	- [4.5. Integrated services](#4.5)
	- [4.6. Differentiated services](#4.6)

- [5. Internetworking](#5)

	- [5.1. How Networks Differ](#5.1)
	- [5.2. How Networks Can Be Connected](#5.2)
	- [5.3. Tunneling](#5.3)
	- [5.4. Packet Fragmentation](#5.4)

- [6. Network Layer of the Internet](#6)

	- [6.1. IP Version 4 Protocol](#6.1)
	- [6.2. IP Addresses](#6.2)
	- [6.3. IP Version 6](#6.3)
	- [6.4. Internet Control Protocols](#6.4)
	- [6.5. Label Switching and MPLS](#6.5)
	- [6.6. OSPF— Interior Routing Protocol](#6.6)
	- [6.7. BGP— Exterior Routing Protocol](#6.7) 
	- [6.8. Internet Multicasting](#6.8)
	- [6.9. Mobile IP](#6.9)
	- [6.10. Mobile IP Recap](#6.10)

[II. Tài liệu dịch](#II)

--------------------------------------------------------------------------

<a name="I"></a>
#### I. Network Layer:

**Spy Satellites**:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/1.png"></p>

**The Network Layer**:
- Chịu trách nhiệm phân phối các gói tin giữa nhiều điểm trên các liên kết
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/2.png"></p>

**The End to End Argument**:

- Có một số người cho rằng công việc của các bộ định tuyến là chuyển các gói tin đi xung quanh và không có gì khác. Theo quan điểm này, mạng lưới vốn đã không đáng tin cậy, dù nó được thiết kế như thế nào.
- Vì vậy, các máy chủ phải chấp nhận thực tế này và tự kiểm soát lỗi và dòng chảy.
- Lý luận này là một ví dụ the end-to-end argument.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/3.png"></p>

<a name="1"></a>
##### 1. Design Issues:

<a name="1.1"></a>
###### 1.1 Store-and-forward packet switching 

*Hosts* gui gói tin vào mang, các goi tin sẽ đuoc chuyen di bởi Routers.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/4.png"></p>

<a name="1.2"></a>
###### 1.2 Connectionless service – datagrams

Gói được chuyển đi sử dụng Des Address bên trong nó
- Các gói tin khác nhau có thể có các đường dẫn khác nhau
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/5.png"></p>

<a name="1.3"></a>
###### 1.3 Connection-oriented service – virtual circuits

Packet được chuuyển đi theo 1 mạch ảo bằng cách sử dụng thẻ bên trong nó.
- Virtual circuit (VC) được cài đặt  thời gian trước
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/6.png"></p>


<a name="1.4"></a>
###### 1.4 Comparison of virtual-circuits and datagrams 

| Issue     | datagram nework | VC network   |
| :-------:| :----: | :---: |
| Circuit setup | không cần |  càn thiết   |
| thông tin trạng thái   | Routers không giữ thông tin trạng thái kết nối  |  Mỗi VC cần có không gian bảng đinh tuyến cho mỗi kết nối  |
| Addressing     | mỗi gói tin cần pphải có du dia chi nguon va dia chi dich    |  mỗi VC cần có 1 VC number ngắn |
| Routing    | mỗi gói tin cần phải có dường đi độc lập   |  Route sẽ chọn khi VC cài đặt, tất cả gói tin theo nó |
| effect of router failures    | không tồn tại, trừ gói tin bị mất trên dường đi    |  tất cả gói tin đều pass mặc dù router bị lỗi được chấm dứt |
| chất lượng dịch vụ   | khó khăn    |  dễ dàng nếu qyền sử dụng có thể phân bổ trước cho mỗi VC |
| Điều khiển tắt ngẽn     | khó khăn    |   dễ dàng nếu qyền sử dụng có thể phân bổ trước cho mỗi VC  |

<a name="2"></a>
##### 2. Routing Algorithms

<a name="2.1"></a>
###### 2.1 Routing Algorithms

**Routing** là quá trình phát hiện các đường đi mạng:
- Mô hình mạng dưới dạng đồ thị của các nút và các liên kết
- Quyết định những gì để tối ưu hóa (ví dụ, công bằng với hiệu quả)
- Cập nhật các tuyến đường để thay đổi topology (ví dụ, failures)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/7.png"></p>

**Forwarding**: là việc gửi các gói tin dọc theo một con đường

Người ta có thể nghĩ đến một bộ định tuyến như có hai quy trình bên trong nó. Một trong số chúng xử lý mỗi gói khi nó đến, nhìn lên duong đi để sử dụng nó  cho bảng định tuyến.

Quá trình này được chuyển tiếp.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/8.png"></p>

<a name="2.2"></a>
###### 2.2. The Optimality Principle

Mỗi phần của một con đường tốt nhất cũng là một con đường tốt nhất; Sự kết hợp của chúng với một bộ định tuyến là một cây gọi là **sink tree**
trong ví dụ  có nghĩatốt nhất là ít hops 
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/9.png"></p>

Trong lý thuyết tối ưu, nếu router J nằm trên đường đi tối ưu từ router I tới router O thì đường đi tối ưu từ J tới O cũng rơi theo cùng một tuyến.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/10.png"></p>

<a name="2.3"></a>
###### 2.3. Shortest Path Algorithm 

Thuật toán của Dijkstra tính toán một sink tree trên đồ thị:
- Mỗi liên kết được gán một trọng lượng / khoảng cách không âm
- Con đường ngắn nhất là con đường có tổng trọng lượng thấp nhất
- Sử dụng trọng lượng của 1 cho đường đi với bước nhảy là ít nhất

Thuật toán:
- Bắt đầu với sink, đặt khoảng cách từ các nút khác đến vô cực
- Relax khoảng cách đến các nút khác
- Chọn nút khoảng cách thấp nhất, thêm nó vào sink tree
- Lặp lại cho đến khi tất cả các nút nằm trong sink tree

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/11.png"></p>

Network và năm bước đầu tiên trong việc tính các con đường ngắn nhất từ A đến D. Những mũi tên màu hồng cho thấy cái sink tree.

<a name="2.4"></a>
###### 2.4 Flooding

- Một phương pháp đơn giản để gửi một gói tin đến tất cả các nút mạng
- Mỗi nút ngập lụt của một gói tin mới nhận được trên một liên kết gửi đi bằng cách gửi nó ra tất cả các liên kết khác
- Các nút cần phải theo dõi các gói tin bị ngập lụt để ngăn chặn lũ lụt; Thậm chí sử dụng một giới hạn hop có thể thổi lên theo cấp số nhân.

<a name="2.5"></a>
###### 2.5 Distance Vector Routing 

**Distance vector** là một thuật toán định tuyến phân tán
- Tính toán đường đi ngắn nhất được phân chia qua các nút

**Thuật toán**:
- Mỗi nút đều biết khoảng cách liên kết đến các hàng xóm của nó
- Mỗi nút quảng cáo véc tơ với khoảng cách được biết đến thấp nhất với tất cả các hàng xóm
- Mỗi nút sử dụng vectơ nhận được để cập nhật của riêng mình
- Lặp lại định kỳ
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/12.png"></p>

<a name="2.6"></a>
###### 2.6. The Count-to-Infinity Problem

Các lỗi có thể gây ra lỗi "count to infinity" trong khi tìm kiếm một con đường đến một nút không thể truy cập được
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/13.png"></p>

<a name="2.7"></a>
###### 2.7. Link State Routing 

link state là một sự thay thế cho vector khoảng cách
- Tính toán nhiều hơn nhưng động lực đơn giản hơn
- Được sử dụng rộng rãi trên Internet (OSPF, ISIS)

Thuật toán:
- Mỗi nút ngập lụt thông tin về các láng giềng của nó trong LSPs (Link State Packets); Tất cả các nút học đồ thị mạng đầy đủ
- Mỗi nút chạy thuật toán của Dijkstra để tính toán đường đi cho mỗi điểm đến,.

**LSPs**(Link State Packet): cho một nút liệt kê các hàng xóm và trọng lượng của liên kết để tiếp cận chúng
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/14.png"></p>

**Reliable Flooding**: Seq số lượng và độ tuổi được sử dụng cho reliable Flooding
- Các LSP mới được ghi nhận trên các dòng họ nhận được và gửi đi trên tất cả các dòng khác
- Ví dụ thể hiện cơ sở dữ liệu LSP tại router B
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/15.png"></p>

<a name="2.8"></a>
###### 2.8. Hierarchical Routing

Hierarchical Routing làm giảm công việc tính toán tuyến đường nhưng có thể dẫn đến các đường dẫn dài hơn một chút so với tuyến phẳng
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/16.png"></p>

<a name="2.9"></a>
###### 2.9. Broadcast Routing

Broadcast gửi gói tin đến tất cả các nút
- RPF (Reverse Path Forwarding): gửi broadcast received  trên liên kết đến nguồn ra tất cả các liên kết còn lại
- Ngoài ra, có thể xây dựng và sử dụng sink tree ở tất cả các nút
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/17.png"></p>

<a name="2.10"></a>
###### 2.10. Multicast Routing 

**Dense Case**: Multicast gửi đến một tập con của các nút được gọi là một nhóm
- Sử dụng một cây khác cho mỗi nhóm và nguồn
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/18.png"></p>

**Sparse Case**: CBT (Core-Based Tree) sử dụng một cây duy nhất để multicast
- Cây là sink tree từ nút lõi đến các thành viên nhóm
- Multicast hướng đến lõi cho đến khi nó đạt tới CBT
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/19.png"></p>

<a name="2.11"></a>
###### 2.11. Anycast Routing

**Anycast** gửi gói tin đến một thành viên nhóm (gần nhất)
- Thất thoát khỏi định tuyến thường xuyên với một nút ở nhiều nơi
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/20.png"></p>

<a name="2.12"></a>
###### 2.12. Routing for Mobile Hosts

Mobile Hosts có thể được tiếp cận thông qua một đại lý tại nhà
- Cố định nhà đại lý đường hầm gói tin để đi đến các máy chủ di động; Trả lời có thể tối ưu hóa đường dẫn cho các gói tiếp theo
- Không có thay đổi đối với router hoặc máy chủ cố định
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/21.png"></p>

<a name="2.13"></a>
###### 2.13. Routing in Ad Hoc Networks

Cấu trúc liên kết mạng thay đổi khi các nút không dây di chuyển
- Các tuyến đường thường được thực hiện theo yêu cầu, ví dụ: AODV (bên dưới)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/22.png"></p>

<a name="2.14"></a>
###### 2.14. Why Routing matters

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/23.png"></p>

<a name="2.15"></a>
###### 2.15. First Class Test 

1. Định nghĩa chính xác nhất của wget là ....
 
**A. Wget là một chương trình dòng lệnh cho phép bạn tìm nạp một URL.**

B. Wget là một chương trình để hiển thị địa chỉ IP của bạn.

C. Wget là một giao thức http an toàn cho ngân hàng trực tuyến

D. Tất cả những điều trên.

2. Distributed denial-of-service (DDoS) attacks là nơi mà một máy tính rogue tấn công một tài nguyên mạng duy nhất (về cơ bản đưa nó đến đầu gối của nó với một loạt các gói tin).

a. True

**b. False**

3. Một gói sniffer là thụ động. Nó quan sát các tin nhắn đang được gửi và nhận được bởi các ứng dụng và các giao thức chạy trên máy tính của bạn, nhưng không bao giờ gửi các gói tin chính nó.

**a. True**

b. False


<a name="3"></a>
##### 3. Congestion Control
Handling congestion  là trách nhiệm của các lớp network và Transport làm việc cùng nhau
- Chúng ta nhìn vào phần Network ở đây
	- Traffic-aware routing
	- Admission control
	- Traffic throttlinga
	- Load shedding

Congestion results khi có quá nhiều giao thông được cung cấp; Hiệu suất làm giảm do loss/retransmissions
- Goodput (= gói tin hữu ích) được cung cấp tải
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/24.png"></p>

<a name="3.1"></a>
###### 3.1. Approaches 

Mạng phải làm tốt nhất với tải được cung cấp:
- Cách tiếp cận khác nhau ở các thời điểm khác nhau
- Nút cũng nên giảm tải được cung cấp (Vận tải)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/25.png"></p>

<a name="3.2"></a>
###### 3.2. Traffic-Aware Routing

Chọn các tuyến đường phụ thuộc vào lưu lượng truy cập, không chỉ topology
- Ví dụ: sử dụng EI cho lưu lượng từ Tây sang Đông nếu CF được tải
- Nhưng cẩn thận để tránh dao động
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/26.png"></p>

<a name="3.3"></a>
###### 3.3. Admission Control

KAdmission Control cho phép tải lưu lượng mới chỉ khi mạng có dung lượng đủ, ví dụ, với các mạch ảo
- Có thể kết hợp với tìm kiếm một tuyến đường không liên tỉnh
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/27.png"></p>

<a name="3.4"></a>
###### 3.4. Congestion Control Summary 

- Trừ phi một mạng lưới được thiết kế tốt, nó có thể gặp sự sụp đổ KHI tắc nghẽn, trong đó hoạt động giảm mạnh khi quá tải được cung cấp tăng vượt quá khả năng
- Trong một mạng mạch ảo , các kết nối mới có thể bị từ chối nếu họ sẽ làm cho mạng trở nên tắc nghẽn. Đây được gọi là *admission control*.
- Cách trực tiếp nhất để thông báo cho người gửi về tắc nghẽn là phải thông báo trực tiếp cho người gửi. Trong cách tiếp cận này, router chọn gói bị tắc nghẽn và gửi một Choke Packet trở lại host nguồn, cho nó đích đến tìm thấy trong gói tin

<a name="3.5"></a>
###### 3.5. Traffic Throttling 


Bộ định tuyến bị tắc nghẽn dẫncho  tín hiệu lưu trữ để làm chậm lưu lượng truy cập
- ECN (Explicit Congestion Notification) đánh dấu các gói tin và tín hiệu thu về người gửi đến người gửi  
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/28.png"></p>

<a name="3.6"></a>
###### 3.6. Load Shedding 

Khi tất cả  không thành công, mạng sẽ thả các gói tin (shed load)

Có thể thực hiện kết thúc để kết thúc hoặc liên kết theo liên kết

Link-by-link (bên phải) tạo ra sự cứu trợ nhanh chóng

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/29.png"></p>

<a name="I"></a>
##### 4. Quality of Service

<a name="4.1"></a>
##### 4.1 Application requirements

Các ứng dụng khác nhau quan tâm đến các thuộc tính khác nhau
- Chúng tôi muốn tất cả các ứng dụng có được những gì họ cần:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/30.png"></p>

Mạng cung cấp dịch vụ với các loại QoS (Quality of Service) khác nhau để đáp ứng yêu cầu ứng dụng

| Network Service  | Application | 
| :-------: | :----: | 
| các bit cố định | Telephony |  
| tốc độ bit biến đổi theo tg thực   | chương trình truyền hình  |  
| tốc độ bit không biến đổi theo tg thực    | Truyền hình trực tuyến phim   |
| Tốc độ bit khả dụng | chuyển tập tin |

Ví dụ về các loại QoS từ mạng lưới ATM

<a name="4.2"></a>
##### 4.2. Traffic shaping

Traffic shaping điều chỉnh tốc độ trung bình và sự bùng nổ của dữ liệu vào mạng
- Cho phép chúng tôi đảm bảo
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/31.png"></p>

Chuôi Token/Leaky giới hạn cả tốc độ trung bình (R) và ngắn (B) của lưu lượng truy cập
- Đối với token, kích thước thùng là B, nước đi vào tốc độ R và được lấy đi để gửi; Đối diện với sự rò rỉ.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/32.png"></p>

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/33.png"></p>
Kích thước xô nhỏ hơn làm chậm trễ lưu lượng truy cập và giảm bớt sự xáo trộn

<a name="4.3"></a>
##### 4.3. Packet scheduling

Packet scheduling chia các tài nguyên router/link giữa lưu lượng giao thông với các lựa chọn thay thế cho FIFO (First In First Out)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/34.png"></p>

Fair Queuing xấp xỉ mức độ công bằng bit với các kích thước gói tin khác nhau; Trọng lượng thay đổi mức mục tiêu
- Kết quả là WFQ (Weighted Fair Queuing)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/35.png"></p>

<a name="4.4"></a>
##### 4.4. Admission control

Admission control có đặc điểm lưu lượng lưu lượng truy cập và quyết định liệu mạng có thể mang nó
- Thiết lập  kế hoạch gói tin để đáp ứng QoS
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/36.png"></p>

Xây dựng để đảm bảo băng thông B và sự chậm trễ D:
- Định dạnglưu lượng nguồn truy cập vào xô token (R, B)
- Chạy WFQ có trọng lượng W / tất cả trọng lượng> R / capacity
- Giữ cho tất cả các lưu lượng truy cập, tất cả các cấu trúc liên kết
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/37.png"></p>

<a name="4.5"></a>
##### 4.5. Integrated services

Design với QoS cho mỗi luồng; Xử lý lưu lượng multicast.

Nhập học với RSVP (Resource ReSerVation Protocol):
- Người nhận gửi yêu cầu trở lại người gửi
- Mỗi router định tuyến các nguồn
- Bộ định tuyến kết hợp nhiều yêu cầu cho cùng một luồng
- Toàn bộ đường dẫn đã được thiết lập hoặc không thiết lập
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/38.png"></p>

<a name="4.6"></a>
##### 4.6. Differentiated services

Thiết kế với các lớp học của QoS; Khách hàng mua những gì họ muốn
- Lớp học cấp tốc được gửi đến lớp thường xuyên
- lưu thông nhanh ít  hơn nhưng chất lượng tốt hơn cho các ứng dụng
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/39.png"></p>

Thực hiện DiffServ:
- Khách hàng đánh dấu lớp học mong muốn trên gói
- ISP hình thành duong đi để đảm bảo đánh dấu được thanh toán
- Các router sử dụng WFQ để cung cấp các mức dịch vụ khác nhau
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/40.png"></p>

<a name="5"></a>
##### 5. Internetworking

<a name="5.1"></a>
##### 5.1. How Networks Differ

Sự khác biệt có thể lớn; Làm phức tạp mạng internetworking
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/41.png"></p>

<a name="5.2"></a>
##### 5.2. How Networks Can Be Connected

Internetworking dựa trên một lớp mạng chung - IP
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/42.png"></p>

<a name="5.3"></a>
##### 5.3. Tunneling

Kết nối hai mạng thông qua một mạng giữa
- Các gói được gói gọn ở giữa
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/43.png"></p>

Tunneling tương tự:
Đường hầm là một liên kết; Gói tin chỉ có thể vào / thoát ra ở cuối
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/44.png"></p>

<a name="5.4"></a>
##### 5.4. Packet Fragmentation 

Mạng có giới hạn kích thước gói tin khác nhau vì nhiều lý do
- Các gói tin lớn được gửi đi với sự phân mảnh & reassembly
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/45.png"></p>

Ví dụ về phân mảnh kiểu IP:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/46.png"></p>

Path MTU Discovery tránh sự phân mảnh mạng
- Router trả lại MTU (Max Transmission Unit) tới nguồn và loại bỏ các gói tin lớn
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/47.png"></p>

<a name="6"></a>
##### 6. Network Layer of the Internet

IP đã được định hình theo các nguyên tắc hướng dẫn:
- Đảm bảo hoạt động
- Giữ nó đơn giản
- Lựa chọn rõ ràng
- Khai thác mô đun
-  Các mong muốn không đồng nhất
- Tránh các tùy chọn và tham số tĩnh
- Tìm kiếm thiết kế tốt (không hoàn hảo)
- Gửi và tiếp nhận khoan dung
- khả năng mở rộng
- Xem xét hiệu suất và chi phí

Internet là một bộ sưu tập kết nối của nhiều mạng được tổ chức cùng nhau bởi giao thức IP
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/48.png"></p>

<a name="6.1"></a>
##### 6.1. IP Version 4 Protocol 

IPv4 (Internet Protocol) header được thực hiện trên tất cả các gói và có các trường cho các phần chính của giao thức:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/49.png"></p>

<a name="6.2"></a>
##### 6.2. IP Addresses 

**Prefixes**:

Địa chỉ được phân bổ trong các khối được gọi làPrefix
- Prefix được xác định bởi phần mạng
- Có địa chỉ 2L nằm trên ranh giới 2L
- Địa chỉ / chiều dài của văn bản, ví dụ: 18.0.31.0/24
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/50.png"></p>

**Subnets**:

Subnetting chia tách tiền tố IP để giúp quản lý
- Hình như một tiền tố duy nhất bên ngoài mạng
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/51.png"></p>

**Aggregation**:

Tập hợp kết hợp nhiều tiền tố IP vào một tiền tố lớn duy nhất để giảm kích thước bảng định tuyến
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/52.png"></p>

**Longest Matching Prefix**:

Các gói tin được chuyển tiếp tới mục nhập với longest matching prefix hoặc khối địa chỉ nhỏ nhất
- Soạn thảo chuyển tiếp nhưng thêm tính linh hoạt
c
**Classful Addresing**:

Địa chỉ cũ có các khối có kích thước cố định (A, B, C)
- Có kích thước như một phần của địa chỉ, nhưng thiếu linh hoạt
- Được gọi là địa chỉ xếp hạng (so với không có lớp)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/53.png"></p>

**NAT**:

NAT (Network Address Translation) ánh xạ một địa chỉ IP bên ngoài với nhiều địa chỉ IP nội bộ
- Sử dụng cổng TCP / UDP để chia sẻ các kết nối
- Vi phạm lớp; Rất phổ biến ở nhà, vv
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/54.png"></p>

<a name="6.3"></a>
##### 6.3. IP Version 6

Nâng cấp lớn trong những năm 1990 do kiệt sức địa chỉ gần đây, với nhiều mục đích khác:
- Hỗ trợ hàng tỷ máy chủ
- Giảm kích thước bảng định tuyến
- Đơn giản hóa giao thức
- An ninh tốt hơn
- Chú ý đến loại dịch vụ
- Viện trợ đa nhiệm
- Roaming host mà không thay đổi địa chỉ
- Cho phép tiến hóa trong tương lai
- Cho phép sự tồn tại của các giao thức cũ, mới,...

Triển khai đã chậm và khó khăn, nhưng có thể tăng tốc ngay bây giờ mà các địa chỉ là tất cả nhưng mệt mỏi

IPv6 protocol header có nhiều địa chỉ dài hơn (128 so với 32 bit) và đơn giản hơn (bằng cách sử dụng tiêu đề mở rộng)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/55.png"></p>

Tiêu đề mở rộng IPv6 xử lý các chức năng khác
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/56.png"></p>


<a name="6.4"></a>
##### 6.4. Internet Control Protocols 


IP hoạt động với sự trợ giúp của một số giao thức điều khiển:
- ICMP là người bạn đồng hành với IP trả về thông tin lỗi
	- Bắt buộc và được sử dụng theo nhiều cách, ví dụ: đối với traceroute
- ARP tìm địa chỉ Ethernet của địa chỉ IP cục bộ
	- Glue là cần thiết để gửi bất kỳ gói tin IP
	- Máy chủ lưu trữ truy vấn một địa chỉ và chủ sở hữu trả lời
- DHCP gán một địa chỉ IP cục bộ cho máy chủ lưu trữ
	- Bắt đầu máy chủ bắt đầu bằng cách tự động cấu hình nó
	- Máy chủ gửi yêu cầu tới máy chủ, cho phép thuê

Các loại  ICMP (Internet Control Message Protocol) chính
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/57.png"></p>
ARP (Address Resolution Protocol) cho phép các nút tìm địa chỉ đích của địa chỉ Ethernet [màu hồng] từ địa chỉ IP của chúng
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/58.png"></p>

<a name="6.5"></a>
##### 6.5. Label Switching and MPLS  

MPLS (Multi-Protocol Label Switching) gửi gói dữ liệu theo các đường dẫn đã được thiết lập; ISP có thể sử dụng cho QoS
- Đường dẫn được chỉ ra với nhãn bên dưới lớp IP
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/59.png"></p>

Nhãn được thêm vào dựa trên địa chỉ IP khi nhập mạng MPLS (ví dụ: ISP) và đã xoá khi rời khỏi mạng
- Chuyển tiếp chỉ sử dụng nhãn bên trong mạng MPLS
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/60.png"></p>

<a name="6.6"></a>
##### 6.6. OSPF— Interior Routing Protocol 

OSPF tính các tuyến đường cho một mạng đơn (ví dụ, ISP)
- Mô hình mạng như một đồ thị của các cạnh mạng
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/61.png"></p>

OSPF chia một mạng lớn (Hệ thống Tự trị) thành các khu vực kết nối với một khu vực xương sống
- Giúp quy mô; Tóm tắt đi qua biên giới khu vực
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/62.png"></p>

OSPF (Open Shortest Path First) là định tuyến trạng thái liên kết:
- Sử dụng các thông báo dưới đây để liên kết mô hình flood đáng tin cậy
- Sau đó chạy Dijkstra để tính toán các tuyến đường
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/63.png"></p>

<a name="6.7"></a>
##### 6.7. BGP— Exterior Routing Protocol 

BGP (Border Gateway Protocol) tính toán các tuyến đường thông qua các mạng lưới tự trị kết nối.
- Vai trò chính là tôn trọng những ràng buộc chính sách của mạng lưới
- ví dụ Các ràng buộc chính sách :
	- Không có lưu lượng truy cập thương mại cho mạng lưới giáo dục
	- Không bao giờ đặt Iraq trên tuyến đường bắt đầu từ Lầu Năm Góc
	- Chọn mạng rẻ hơn
	- Chọn mạng hoạt động tốt hơn
	- Không đi từ Apple đến Google với Apple

Sự khác biệt chính sách chung là chuyển đổi sang so sánh:
- Quá cảnh vận chuyển có trả tiền; peers vì lợi ích chung
- AS1 mang AS2↔AS4 (Transit) nhưng không AS3 (Peer)
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/64.png"></p>

<a name="6.8"></a>
##### 6.8. Internet Multicasting 

Các nhóm có dải địa chỉ IP dành riêng (class D)
- Thành viên trong một nhóm do IGMP quản lý (Internet Group Management Protocol) chạy trên các bộ định tuyến
Các tuyến được tính bằng các giao thức như PIM:
- Chế độ Dense sử dụng RPF với pruning
- Chế độ core-based sử dụng các cây dựa trên lõi
IP multicasting không được sử dụng rộng rãi ngoại trừ trong một mạng duy nhất, ví dụ: trung tâm dữ liệu, mạng truyền hình cáp.

<a name="6.9"></a>
##### 6.9. Mobile IP

Máy chủ di động có thể được truy cập tại IP cố định thông qua một đại lý tại nhà
- Các gói tin nhà khai thác đường hầm để tiếp cận với máy chủ di động; Trả lời có thể tối ưu hóa đường dẫn cho các gói tiếp theo
- Không có thay đổi đối với bộ định tuyến hoặc máy chủ cố định
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/65.png"></p>

<a name="6.10"></a>
##### 6.10. Mobile IP Recap 

Máy chủ lưu trữ di động khác với máy chủ lưu trữ không di chuyển.

Ý tưởng cơ bản được sử dụng cho định tuyến di động trong mạng Internet và mạng di động là cho máy chủ lưu trữ di động nói với một máy chủ ở vị trí chính nơi ở hiện tại.

Máy chủ này hoạt động thay mặt cho máy chủ lưu trữ di động được gọi là home agent.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/66.png"></p>

<a name="II"></a>
#### II. Tài liệu dịch:

Lecture 5: Network Layer: http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm

	
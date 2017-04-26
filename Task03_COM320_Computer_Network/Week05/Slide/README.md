## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **26/04/2017**

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

- [6. Network Layer of the Internet](#6)

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

**Distance vector ** là một thuật toán định tuyến phân tán
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
	- Traffic throttling
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

<a name="4.2"></a>
##### 4.2. Traffic shaping

<a name="4.3"></a>
##### 4.3. Packet scheduling

<a name="4.4"></a>
##### 4.4. Admission control

<a name="4.5"></a>
##### 4.5. Integrated services

<a name="4.6"></a>
##### 4.6. Differentiated services


<a name="5"></a>
##### 5. Internetworking


<a name="6"></a>
##### 6. Network Layer of the Internet


<a name="II"></a>
#### II. Tài liệu dịch:

Lecture 5: Network Layer: http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm

	
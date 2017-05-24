## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **24/05/2017**

--------------------------
### Mục lục

[1.Transport Service](#1)

- [1.1 Services Provided to the Upper Layer](#1.1)
- [1.2 Transport Service Primitives](#1.2)
- [1.3 Berkeley Sockets](#1.3)
- [1.4 Socket Example: Internet File Server](#1.4)

[2.Elements of Transport Protocols](#2)

- [2.1 Addressing](#2.1)
- [2.2 Connection establishment](#2.1)
- [2.3 Connection release](#2.1)
- [2.4 Error control and flow control](#2.1)
- [2.5 Multiplexing](#2.1)
- [2.6 Crash recovery](#2.1)

[3.Congestion Control](#3)

- [3.1 Desirable bandwidth allocation](#3.1)
- [3.2 Regulating the sending rate](#3.2)
- [3.3 Wireless issues](#3.3)

[4.Internet Protocols – UDP](#4)

- [4.1 Introduction to UDP](#4.1)
- [4.2 Remote Procedure Call](#4.2)
- [4.3 Real-Time Transport](#4.3)

[5.Internet Protocols – TCP](#5)

- [5.1 The TCP service model](#5.1)
- [5.2 The TCP segment header](#5.2)
- [5.3 TCP connection establishment](#5.3)
- [5.4 TCP connection state modeling](#5.4)
- [5.5 TCP sliding window](#5.5)
- [5.6 TCP timer management](#5.6)
- [5.7 TCP congestion control](#5.7)

[6.Performance Issues](#6)

- [6.1 Performance problems](#6.1)
- [6.2 Measuring network performance](#6.1)
- [6.3 Host design for fast networks](#6.1)
- [6.4 Fast segment processing](#6.1)
- [6.5 Header compression](#6.1)
- [6.6 Protocols for “long fat” networks](#6.1)

--------------------------------
<a name="1"></a>
### 1.Transport Service:

Tầng hịu trách nhiệm phân phối dữ liệu qua các mạng với độ tin cậy or chất lượng.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/1.png"></p>

<a name="1.1"></a>
#### 1.1 Services Provided to the Upper Layer

Transport layer thêm độ tin cậy vào lớp mạng:

- Cung cấp các dịch vụ không kết nối (ví dụ như UDP) và dịch vụ định hướng kết nối (ví dụ: TCP)
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/2.png"></p>
 
- Transport layer gửi các *segments* trong các gói tin (frames)
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/3.png"></p>

<a name="1.2"></a>
#### 1.2 Transport Service Primitives

Primitive mà các ứng dụng có thể gọi đến dữ liệu truyền tải cho một dịch vụ định hướng kết nối đơn giản:
- Các cuộc gọi của khách hàng kết nối, gửi, nhận, ngắt kết nối
- Các cuộc gọi máy chủ nghe, nhận, gửi, ngắt kết nối

| Primitive    | Segments gửi | ý nghĩa  |
| :------: | :---: | :---: |
| LISTEN| (none)| Chặn quá trình cố gắng kết nối   |
| CONNECT   | CONNECTION REQ  |  Chủ động cố gắng để thiết lập kết nối  |
| SENT    | DATA    |  Gửi thông tin  |
| RECEIVE     | (none)    |  chặn các gói dữ liệu đến  |
| DISCONNECT     | DISCONNECTION REQ    |  Bên này muốn phát hành kết nối  |

Sơ đồ trạng thái cho một dịch vụ định hướng kết nối đơn giản
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/4.png"></p>
 
- Các đường thẳng (bên phải) hiển thị dãy trạng thái máy khách 
- Đường nét đứt (trái) hiển thị trình tự trạng thái máy chủ
- Các chuyển tiếp bằng chữ nghiêng là do phân đoạn đến.

<a name="1.3"></a>
#### 1.3 Berkeley Sockets

Rất phổ biến sử dụng nguyên bản khi bắt đầu với TCP trên unix
- Ý nghĩa của *"Sockets"* là điểm cuối vận tải
- Giống như bộ đơn giản cộng với *socket*, *bind*, and *accept*

| Primitive    | ý nghĩa |
| :------:| :---: | 
| SOCKET  | Tạo mới 1 điềm kết thúc truyền thông   |
| BIND    | Liên kết địa chỉ cục bộ với socket   |
| LISTEN  | Thông báo sẵn sàng chấp nhận kết nối; Cho kích thước chờ  |
| ACCEPT  | Thiết lập  kết nối tự động   |
| CONNECT | Chủ động cố gắng để thiết lập kết nối  |
| SENT    |  Gửi thông tin qua các kết nối  |
| RECEIVE |  Nhận các gói dữ liệu từ các kết nối |
| LOSE    |  Ngắt kết nối |

<a name="1.4"></a>
#### 1.4 Socket Example: Internet File Server

Client code:
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/5.png"></p>
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/6.png"></p>

<a name="2"></a>
### 2.Elements of Transport Protocols

<a name="2.1"></a>
#### 2.1 Addressing

- Transport layer thêm TSAP
- Nhiều client và server có thể chạy trên máy chủ lưu trữ với một địa chỉ mạng (IP) duy nhất
- TSAPs là các port cho TCP / UDP

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/7.png"></p>

<a name="2.2"></a>
#### 2.2 Connection establishment

Vấn đề chính là đảm bảo độ tin cậy mặc dù các gói tin có thể bị lost(mất), corrupted(hỏng), *delayed*(trì hoãn), và *duplicated*(nhân bản)
- Không xử lý gói cũ hoặc gói tin trùng lặp như gói tin mới
- (Sử dụng ARQ và tổng kiểm tra loss/corruption)
 
Tiếp cận:
- Không sử dụng lại sequence numbers trong hai lần MSL (Maximum Segment Lifetime)  của 2T = 240 giây
	- Sử dụng một dãy số không gian đủ lớn mà nó sẽ không bọc, ngay cả khi gửi ở tỷ lệ đầy đủ. Đồng hồ (high bit) tiến bộ & giữ nhà trên vụ tai nạn.
	  <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/8.png"></p>
- Dùng bắt tay ba bước để kết nối
	- Bắt tay ba đường được sử dụng cho gói ban đầu
		- Vì không có tiểu bang nào từ kết nối trước
		- Cả hai máy chủ đều đóng góp phần mới. Số
		- CR = Connect Request
	 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/9.png"></p>
	- Bắt tay ba cách bảo vệ chống lại các trường hợp kỳ quặc:
		- Nhân đôi CR. Spurious ACK không kết nối
		 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/10.png"></p>
		- Nhân đôi CR và DATA. Cùng với DATA sẽ bị từ chối (sai ACK).
	     <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/11.png"></p>

<a name="2.3"></a>
#### 2.3 Connection release

- Vấn đề chính là đảm bảo độ tin cậy trong khi giải phóng
- Giải phóng bất đối xứng (khi một bên phá vỡ kết nối) là đột ngột và có thể bị mất dữ liệu

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/12.png"></p>

- Sự giải phóng đối xứng (cả hai bên đồng ý giải phóng) không thể được xử lý bởi transport layer
	- Hai vấn đề quân đội cho thấy pitfall của thỏa thuận
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/13.png"></p>

- Trình tự phát hành bình thường, do người vận chuyển khởi tạo trên Máy chủ lưu trữ 1
	- DR = Disconnect Request
	- Cả hai DR được ACKed bởi phía bên kia
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/14.png"></p>
 
- Các trường hợp lỗi được xử lý bằng timer và retransmission:
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/15.png"></p>

<a name="2.4"></a>
#### 2.4 Error control and flow control

Cơ sở để kiểm soát lỗi là một cửa sổ trượt (từ link layer) với checksums và retransmissions

Flow control  điều khiển bộ đệm ở người gửi / người nhận
- Vấn đề là dữ liệu đi đến / từ mạng và các ứng dụng vào các thời điểm khác nhau
- Cửa sổ báo cho người gửi có bộ đệm ở máy thu
- Tạo một cửa sổ trượt có thể thay đổi kích cỡ

Các chiến lược đệm khác nhau hiệu quả kinh tế / phức tạp.
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/16.png"></p>

Ví dụ kiểm soát dòng chảy: dữ liệu của một bị giới hạn bởi bộ đệm của B
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/17.png"></p>

<a name="2.5"></a>
#### 2.5 Multiplexing

Các loại transport / network  có thể xảy ra:
- Multiplexing: Các kết nối chia sẻ địa chỉ mạng
- Inverse multiplexing: các địa chỉ chia sẻ kết nối
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/18.png"></p>

<a name="2.6"></a>
#### 2.6 Crash recovery

Ứng dụng cần giúp phục hồi từ vụ tai nạn
- Transport có thể fail vì A(ck)/W(rite) không phải là nguyên tử
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/19.png"></p>

<a name="3"></a>
### 3.Congestion Control

Hai lớp chịu trách nhiệm kiểm soát tắc nghẽn:
- Transport layer, kiểm soát tải được cung cấp [ở đây]
- Network layer, trải nghiệm tắc nghẽn [trước]

<a name="3.1"></a>
#### 3.1 Desirable bandwidth allocation

Hiệu quả sử dụng băng thông cho phép tốt,độ chậm trễ thấp.
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/20.png"></p>

Sử dụng hợp lý cho phép băng thông đủ tất cả các dòng chảy (không thiếu)
- Sự công bằng tối đa cho các cổ phiếu có cổ phần bằng nhau
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/21.png"></p>

Chúng tôi muốn mức băng thông hội tụ một cách nhanh chóng khi các mẫu lưu lượng truy cập thay đổi
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/22.png"></p>

<a name="3.2"></a>
#### 3.2 Regulating the sending rate

Người gửi có thể cần tải chậm lại vì nhiều lý do khác nhau:
- Điều khiển luồng(Flow control), khi người nhận không đủ nhanh [phải]
- Tập trung(Congestion), khi mạng không đủ nhanh [trên]
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/23.png"></p>

Trọng tâm của chúng tôi là đối phó với vấn đề này - tắc nghẽn
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/24.png"></p>

Các tín hiệu tắc nghẽn khác nhau cho thấy mạng lưới có thể sử dụng để cho điểm kết nối cuối làm chậm (hoặc tăng tốc)

| Protocol    | Signal | explicit?  | Pricise |
| :------: | :---: | :---: | :---: |
| XCP | Tỉ lệ để sử dụng | YES   | YES |
| TCP with ECN   | Xung đột tắt ngẽn  |  YES  | NO  |
| FAST TCP  | Độ trễ đầu cuối    | NO  | YES |
| CUBIC TCP | Mất gói    |  NO  | NO  |
| TCP    |  Mất gói    |  NO  | NO  |

Nếu hai luồng tăng / giảm băng thông của chúng theo cùng một cách khi các tín hiệu mạng rảnh / bận, chúng sẽ không hội tụ đến phân bổ hợp lý
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/25.png"></p>

Đạo luật kiểm soát AIMD (Additive Increase Multiplicative Decrease) hội tụ đến một điểm công bằng và hiệu quả!
- TCP sử dụng AIMD vì lý do này
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/26.png"></p>

<a name="3.3"></a>
#### 3.3 Wireless issues

Các liên kết không dây bị mất các gói vì các lỗi truyền dẫn
- Không muốn nhầm lẫn sự mất mát này với tắc nghẽn
- Hoặc kết nối sẽ chạy chậm trên các liên kết không dây!
Chiến lược:
- Các liên kết không dây sử dụng ARQ, có mặt nạ lỗi
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/27.png"></p>

<a name="4"></a>
### 4.Internet Protocols – UDP

<a name="4.1"></a>
#### 4.1 Introduction to UDP

UDP (User Datagram Protocol) là một shim over IP
- Tiêu đề có cổng (TSAPs), chiều dài và tổng kiểm tra
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/28.png"></p>

<a name="4.2"></a>
#### 4.2 Remote Procedure Call


RPC kết nối các ứng dụng qua mạng với các thủ tục trừu tượng quen thuộc của các cuộc gọi thủ tục
- Các gói / gói kết quả / thông báo vào một tin nhắn
- UDP với retransmissions là một vận chuyển trễ thấp
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/29.png"></p>


<a name="4.3"></a>
#### 4.3 Real-Time Transport

RTP (Real-time Transport Protocol) cung cấp hỗ trợ truyền phương tiện thời gian thực qua UDP
- Thường được thực hiện như là một phần của ứng dụng
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/30.png"></p>

RTP header chứa các trường để mô tả loại phương tiện và đồng bộ hóa nó giữa nhiều luồng
- Giao thức của RTCP giúp với các nhiệm vụ quản lý
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/31.png"></p>

Bộ đệm tại máy thu được sử dụng để trì hoãn các gói dữ liệu và hấp thụ jitter để các phương tiện truyền thông được phát ra trơn tru
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/32.png"></p>

Jitter cao, hoặc nhiều biến thể trong sự chậm trễ, đòi hỏi một bộ đệm playout lớn hơn để tránh playout misses
- Sự chậm trễ lan truyền không ảnh hưởng đến kích thước bộ đệm
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/33.png"></p>

<a name="5"></a>
### 5.Internet Protocols – TCP

<a name="5.1"></a>
#### 5.1 The TCP service model

TCP cung cấp các ứng dụng với luồng byte tin cậy giữa các tiến trình; Nó là máy nghiền của Internet
- Các máy chủ phổ biến chạy trên các cổng nổi tiếng
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/34.png"></p>

Các ứng dụng sử dụng TCP chỉ thấy dòng byte [phải] chứ không phải các phân đoạn [trái] được gửi dưới dạng các gói tin IP riêng biệt
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/35.png"></p>

<a name="5.2"></a>
#### 5.2 The TCP segment header

TCP header bao gồm địa chỉ (port), cửa sổ trượt (seq./ack. number), điều khiển luồng (window), kiểm soát lỗi (checksum) và nhiều hơn nữa.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/36.png"></p>

<a name="5.3"></a>
#### 5.3 TCP connection establishment

TCP thiết lập kết nối với bắt tay ba cách
- Phát hành là đối xứng, cũng như mô tả trước
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/37.png"></p>

<a name="5.4"></a>
#### 5.4 TCP connection state modeling

Máy trạng thái kết nối TCP có nhiều trạng thái hơn

| state   | Miêu tả |
| :------:| :---: | 
| LISTEN  | Máy chủ sẽ chờ cuộc gọi đến  |
| SYN RCVD |  1 yêu cầu kết nối đến; đợi ACK   |
| SYN SENT   | Ứng dụng đã bắt đầu mở kết nối   |
| ESTABLISHED  | Trạng thái truyền dữ liệu bình thường |
| FIN WAIT 1  | Ứng dụng nói là đã kết thúc   |
| FIN WAIT 2 | Mặt khác đồng ý giải phóng  |
| TIME WAIT   |  Đợi tất cả gói tin die off  |
| CLOSING |  Cả 2 đã cố gắng đóng cùng lúc |
| CLOSE WAIT  |  Mặt khác bắt đầu giải phóng|
| LAST ACK  |  Đợi tất cả gói tin die off  |

- Đường nét đậm là đường dẫn bình thường cho khách hàng.
- Đường net đứt là đường dẫn bình thường cho một máy chủ.
- Đường nét mờ là những sự kiện bất thường.
- Chuyển tiếp được dán nhãn theo nguyên nhân và hành động, được tách bằng dấu gạch chéo.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/38.png"></p>

<a name="5.5"></a>
#### 5.5 TCP sliding window

TCP thêm điều khiển luồng vào cửa sổ trượt như trước
- ACK + WIN là giới hạn của người gửi
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/39.png"></p>

Cần thêm các trường hợp đặc biệt để tránh hành vi không mong muốn
- Ví dụ: Hội chứng ngớ ngẩn cửa sổ [bên dưới]
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/40.png"></p>

<a name="5.6"></a>
#### 5.6 TCP timer management

TCP ước tính retransmit hẹn giờ từ đoạn RTTs 
- Theo dõi trung bình và phương sai (đối với trường hợp Internet)
- Thời gian chờ được đặt thành trung bình cộng với độ lệch 4 x

<a name="5.7"></a>
#### 5.7 TCP congestion control

TCP sử dụng AIMD với tín hiệu mất mát để kiểm soát tắc nghẽn
- Thực hiện như một **congestion window (cwnd)**  cho số phân đoạn có thể có trong mạng
- Sử dụng một số cơ chế làm việc cùng nhau
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/41.png"></p>

| Name   | Cơ chế | Mục đích |
| :------:| :---: | :---: |
| ACK clock | Congestion window (cwnd)  | Xóa gói tin bị hư |
| Slow-start | Double cwnd each RTT  |Tốc độ gửi tăng nhanh để đạt đến mức cao hơn  |
| Additive Increase  | Tăng thêm 1 gói mỗi RTT | Tăng tốc độ gửi đi chậm lại ở mức đúng  |
| Fast retransmit / recovery  | Gửi lại gói bị mất sau 3 lần trùng lặp ACK; Gửi gói mới cho mỗi ACK mới | Khôi phục từ một gói bị mất mà không dừng đồng hồ ACK |

Congestion windown kiểm soát tốc độ gửi
- Giá cước/RTT; Cửa sổ có thể dừng người gửi nhanh chóng
- **ACK clock** (thường xuyên nhận ACK) sẽ chuyển hướng lưu lượng truy cập và sender bursts
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/42.png"></p>

Bắt đầu làm chậm phát triển congestion windown theo cấp số nhân
- Tăng gấp đôi mỗi RTT trong khi vẫn giữ đồng hồ ACK
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/43.png"></p>

Sự gia tăng Additive increase  tăng chậm dần dần
- Thêm 1 RTT
- Giữ ACK clock
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/44.png"></p>

Bắt đầu chậm  sau đó tăng thêm (TCP Tahoe)
- Ngưỡng là một nửa của tổn thất trước
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/45.png"></p>

Với phục hồi nhanh chóng, chúng tôi có được răng cưa cổ điển (TCP Reno)
- Retransmit gói bị mất sau khi 3 ACK trùng lặp
- Gói mới cho mỗi dup. ACK cho đến khi mất mát được sửa chữa
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/46.png"></p>

SACK (Selective ACKs) mở rộng ACK với một vector để mô tả các phân đoạn nhận được và do đó mất mát
- Cho phép tái truyền / phục hồi chính xác hơn
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/47.png"></p>

<a name="6"></a>
### 6.Performance Issues

Nhiều chiến lược để đạt được hiệu suất tốt đã được học hỏi qua thời gian:

<a name="6.1"></a>
#### 6.1 Performance problems

Các tải không mong muốn thường tương tác với các giao thức để gây ra sự cố về hiệu suất
- Cần tìm ra tình huống và cải tiến các giao thức
Ví dụ:
- Bão broadcast: một chương trình broadcasst gây nên sự cố.
- Đồng bộ hóa: một tòa nhà của tất cả các máy tính liên lạc với máy chủ DHCP sau khi mất điện
- Các gói tin nhỏ: Một số tình huống có thể gây ra TCP để gửi nhiều gói tin nhỏ thay vì một vài gói lớn

<a name="6.2"></a>
#### 6.2 Measuring network performance

Measurement(đo lường) là chìa khóa để biết được hiệu suất - nhưng có những cạm bẫy của nó.
Ví dụ về những cạm bẫy:
  - Bộ nhớ đệm: lấy các trang Web sẽ cho kết quả đáng ngạc nhiên nhanh chóng nếu chúng được lưu trữ không mong muốn
- Thời gian: đồng hồ có thể vượt quá / đánh giá thấp các sự kiện nhanh
- Sự can thiệp: có thể có khối lượng công việc cạnh tranh nhau

<a name="6.3"></a>
#### 6.3 Host design for fast networks

Phần mềm máy chủ nghèo có thể làm chậm rất nhiều mạng.
Quy tắc chung cho phần mềm máy chủ lưu trữ nhanh:
- Tốc độ máy chủ quan trọng hơn tốc độ mạng
- Giảm số gói tin để giảm chi phí
- Tối ưu hoá dữ liệu vào
- Giảm thiểu chuyển đổi ngữ cảnh
- Tránh tắc nghẽn hơn là hồi phục
- Tránh hết thời gian chờ

<a name="6.4"></a>
#### 6.4 Fast segment processing

Đẩy nhanh trường hợp thông thường với một con đường nhanh [màu hồng]
- Xử lý các gói với tiêu đề dự kiến; đồng ý để người khác chạy chậm
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/48.png"></p>

Trường tiêu đề thường giống nhau từ một gói tin đến gói kế tiếp cho luồng; copy/check để tăng tốc xử lý
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/49.png"></p>

<a name="6.5"></a>
#### 6.5 Header compression

Chi phí đầu vào có thể rất lớn cho các gói nhỏ
- 40 byte tiêu đề cho gói RTP/UDP/IP VoIP
- Có vấn đề với các liên kết chậm, đặc biệt là không dây

Tiêu đề nén làm giảm vấn đề này
- Chạy giữa các lớp Link và Network
- bỏ sót các lĩnh vực không thay đổi hoặc thay đổi có thể dự đoán
	- 40 byte tiêu đề TCP/IP --> 3 byte thông tin
- Cung cấp tiêu đề lớp đơn giản và liên kết hiệu quả

<a name="6.6"></a>
#### 6.6 Protocols for “long fat” networks

Mạng có băng thông cao ("Fat") và độ trễ cao ("Long") có thể lưu trữ nhiều thông tin bên trong mạng
- Yêu cầu các giao thức với bộ đệm phong phú và RTT ít, thay vì giảm các bit trên dây
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/50.png"></p>

Bạn có thể mua thêm băng thông nhưng không có độ trễ
- Cần phải thay đổi vị trí kết thúc (ví dụ như vào đám mây) để hạ thấp hơn nữa
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Slide/Image/51.png"></p>

---------------------------------------------------------------

### Tài liệu dịch

[1] Lecture 6: Transport Layer. http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm


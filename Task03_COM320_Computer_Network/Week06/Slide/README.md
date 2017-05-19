## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **19/05/2017**

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

[5.Internet Protocols – TCP](#5)

[6.Performance Issues](#6)

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


<a name="3.2"></a>
#### 3.2 Regulating the sending rate

<a name="3.3"></a>
#### 3.3 Wireless issues


------------------------

### Tài liệu dịch

[1] Lecture 6: Transport Layer. http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm
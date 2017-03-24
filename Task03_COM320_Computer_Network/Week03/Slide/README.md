## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **24/03/2017**

### Mục lục
[I. The Data link layer](#I)
[1. Data Link layer Design Issues](#1)

- [1.1. Frames](#1.1)
- [1.2. Possible services](#1.2)
- [1.3. Framing methods](#1.3)
- [1.4. Error control](#1.4)
- [1.5. Flow control](#1.5)
- [1.6. TWIT Resources](#1.6)

[2. Error Detection and Correction](#2)
- [2.1. Error correction codes](#2.1)
 
	- [2.1.1. Hamming codes](#2.1.1)
	- [2.1.2. Binary convolutional codes ](#2.1.2)
	- [2.1.3. Reed-Solomon and Low-Density Parity Check codes](#2.1.3)
	
- [2.2. Error detection codes](#2.2)
 
	- [2.2.1. Parity](#2.2.1)
	- [2.2.2. Checksums](#2.2.2)
	- [2.2.3. Cyclic redundancy codes ](#2.2.3)
	
[3. Elementary Data Link Protocols](#3)

- [3.1.Link layer environment](#3.1)
- [3.2.Utopian Simplex Protocol](#3.2)
- [3.3.Stop-and-Wait Protocol for Error-free channel](#3.3)
- [3.4.Stop-and-Wait Protocol for Noisy channel](#3.4)

[4. Sliding Window Protocols](#4)
- [4.1. Sliding Window concept](#4.1)
- [4.2. One-bit Sliding Window](#4.2)
- [4.3. Go-Back-N](#4.3)
- [4.4. Selective Repeat](#4.4)
- [4.5. Hak 5 Resources](#4.5)

[5. Example Data Link Protocols](#5)

- [5.1. Packet over SONET](#5.1)
- [5.2. PPP (Point-to-Point Protocol)](#5.2)
- [5.3. ADSL (Asymmetric Digital Subscriber Loop)](#5.3)

<a name=I></a>
### I. The Data Link layer
Chịu trách nhiệm phân phối các thông tin khung qua một liên kết:
- Xử lý lỗi truyền tải và điều chỉnh luồng dữ liệu.
- Data Link layer Chịu trách nhiệm kiểm soát việc truyền qua khung trên phương tiện.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/1.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/2.png"></p>

<a name="1"></a>
#### 1. Data Link Layer Design Issues
- Cuối cùng, data link layer sử dụng các dịch vụ của physical layer để gửi và nhận các bit thông qua các kênh truyền thông.
- Để hoàn thành các mục tiêu này, lớp data link lấy các gói dữ liệu nhận được từ lớp network và gói gọn chúng thành các *Frames* để truyền.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/3.png"></p>

<a name="1.1"></a>
	
  ##### 1.1. Frames
Link layer chấp nhận **Packet** từ lớp network và gói gọn chúng vào các **frames** mà nó gửi bằng lớp Physical; Tiếp nhận là quá trình đối diện

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/4.png"></p>

<a name="1.2"></a>
##### 1.2. Possible services
- Dịch vụ kết nối không được xác nhận
	- Frame được gửi không có kết nối /  lỗi phục hồi
	- Ethernet là ví dụ
- Dịch vụ kết nối không được chấp nhận
	- Frame được gửi đi với truyền lại nếu cần
	- Ví dụ là 802.11
- Dịch vụ kết nối được xác nhận
	- Kết nối được thiết lập; hiếm

<a name="1.3"></a>
##### 1.3. Framing methods
Để cho phép người nhận chuẩn bị cho một gói tin gửi đến, một khuôn mẫu chung được sử dụng cho Ethernet và 802.11 là có một khung bắt đầu với một mẫu được xác định rõ gọi là preamble.
**Byte count**
Frame bắt đầu với đếm số byte trong nó
- Đơn giản, nhưng khó để đồng bộ lại sau khi xảy ra lỗi.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/5.png"></p>

**Byte stuffing**
Đặc biệt cờ bytes trong khung; Sự xuất hiện của cờ trong dữ liệu phải được nhồi nhét (thoát)
- Dài hơn, nhưng dễ dàng đồng bộ lại sau khi lỗi.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/6.png"></p>
Satuffing ở mức bit:

- Frame flag có sáu liên tiếp 1s (không hiển thị)
- Khi truyền, sau năm bit 1 trong dữ liệu, một 0 được thêm vào
- Khi nhận được, một 0 sau năm bit 1 sẽ bị xóa
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/7.png"></p>

<a name="1.4"></a>
##### 1.4. Error control
Lỗi kiểm soát các khung sửa chữa được nhận khi lỗi:

- Yêu cầu phát hiện sai sót tại máy thu
- Thường truyền lại các khung không nhận diện
- Bộ đếm thời gian bảo vệ chống lại những phản hồi bị mất

Phát hiện lỗi và truyền lại là các chủ đề tiếp theo.

<a name="1.5"></a>
##### 1.5. Flow contro (Kiểm soát luồng)
Ngăn chặn người gửi nhanh khỏi máy thu chậm

- Người nhận phản hồi về dữ liệu có thể chấp nhận
- Khá trong lớp Link do các NIC chạy ở tốc độ "wire speed"
	- Người nhận có thể lấy dữ liệu nhanh như nó có thể được gửi
	
Flow contro là một chủ đề trong các lớp Liên kết và Vận tải

<a name="1.6"></a>
##### 1.6. TWIT Resources

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/8.png"></p>

LI-FI:  https://www.youtube.com/watch?v=yLCljViTkus

<a name="2"></a>
#### 2. Error Detection and Correction
Error code sự thêm thừa cấu trúc dữ liệu do đó các lỗi có thể được phát hiện, hoặc sửa chữa.
<a name="2.1"></a>
##### 2.1. Error correction codes

<a name="2.1.1"></a>
###### 2.1.1. Hamming codes
Mã chuyển dữ liệu của n bit thành các mã của n + k bit
Hamming distance là bit tối thiểu flips để biến một codeword thành  bất kỳ một trong valid khác.
- Ví dụ với 4 codewords của 10 bit (n = 2, k = 8):
	- 0000000000, 0000011111, 1111100000 và 1111111111
	- Hamming distance là 5
	
Giới hạn cho một mã với khoảng cách:
- 2d + 1 - có thể sửa lỗi d (ví dụ: 2 lỗi ở trên)
- d +1 - có thể phát hiện lỗi d (ví dụ: 4 lỗi ở trên)

<a name="2.1.2"></a>
###### 2.1.2. Binary convolutional codes
Hamming code cho một cách đơn giản để thêm kiểm tra bit và chính xác đến một lỗi bit đơn:
- Kiểm tra bit là chẵn lẻ trên tập con của codeword
- Tính lại các khoản chẵn lẻ (syndrome) cho biết vị trí của lỗi để flip, hoặc 0 nếu không có lỗi
- Mã số và Phát hiện Mã Hamming
<a name="2.1.3"></a>
###### 2.1.3. Reed-Solomon and Low-Density Parity Check codes
Toán học phức tạp, được sử dụng rộng rãi trong các hệ thống thực

<a name="2.2"></a>
##### 2.2. Error detection codes
<a name="2.2.1"></a>
###### 2.2.1. Parity

Parity bit được thêm vào như là tổng số modulo 2 của bit dữ liệu tương đương với XOR; Đây là chẵn lẻ:
- Ví dụ: 1110000 --> 11100001
- Phát hiện kiểm tra nếu tổng sai (lỗi)

Cách đơn giản để phát hiện một số lẻ của lỗi:
- Ví dụ: 1 lỗi, 11100101; Phát hiện, tổng là sai
- Ví dụ: 3 lỗi, 11011001; Tổng phát hiện sai
- Ví dụ: 2 lỗi, 11101101; Không phát hiện, tổng là đúng!
- Lỗi cũng có thể nằm trong bit chẵn lẻ
- Các lỗi ngẫu nhiên được phát hiện với xác suất ½

**Interleaving** của N bit chẵn lẻ phát hiện lỗi burst lên đến N:
- Mỗi khoản chẵn lẻ được thực hiện trên các bit không liên kết
- Ngay cả một burst đến lỗi N  sẽ không gây ra thất bại
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/9.png"></p>

<a name="2.2.2"></a>
###### 2.2.2. Checksums
 Checksum sử lý dữ liệu như các N-bit words và thêm N kiểm tra bit là tổng số modulo 2N của các từ:
- Ví dụ: Internet 16-bit 1s bổ sung checksum 

Tính chất:
- Tăng cường phát hiện lỗi trên bit chẵn lẻ
- Phát hiện ra burst đến N lỗi
- Phát hiện sai số ngẫu nhiên với xác suất 1-2N
- Dễ bị tổn hại đến lỗi hệ thống, ví dụ: số 0 được thêm vào

<a name="2.2.3"></a>
###### 2.2.3. Cyclic redundancy codes
Thêm các bit để khung truyền được xem như một đa thức được phân chia đều bởi một đa thức máy phát điện.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/10.png"></p>

- Bắt đầu bằng cách thêm 0 vào khung và thử chia
- Offset bởi lời nhắc để làm cho nó chia đều
<a name="3"></a>
#### 3. Elementary Data Link Protocols

- Một vấn đề thiết kế quan trọng xảy ra trong lớp data link là phải làm gì với người gửi muốn truyền khung nhanh hơn người nhận mà hệ thống có thể chấp nhận chúng.
- Trong kiểm soát lưu lượng dựa trên tỷ lệ, giao thức có một cơ chế tích hợp để hạn chế tốc độ mà người gửi có thể truyền dữ liệu mà không sử dụng phản hồi từ người nhận. Việc sử dụng các mã sửa lỗi thường được gọi là FEC (Forward Error Correction).

<a name="3.1"></a>
##### 3.1.Link layer environment

- Thường được thực hiện như các NICs và OS drivers; network layer (IP) thường là phần mềm Hệ điều hành.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/11.png"></p>

- Các triển khai giao thức lớp Link sử dụng các chức năng thư viện. Xem mã `(protocol.h)` để biết thêm chi tiết

| Group       | Library Function          | Description  |
| :-------------: |:-------------:| :-----:|
| Network Layer | from_network-layer(&packet) |Lấy gói tin từ lớp mạng để gửi  |
|				|to_network-layer(&packet)|Gửi gói tin nhận được đến lớp mạng|
|				|enable_network-layer() |Hãy để mạng gây ra các sự kiện "reaady" |
|				|disable_network-layer()|Ngăn chặn các sự kiện "ready" trên mạng|
|Physical layer | from_physical_layer(&frame)|Nhận một khung đến từ lớp vật lý|
|				|to_physical_layer(&frame)|Truyền khung đi tới lớp vật lý|
|Events&timers | wait_for_event(&event)|Chờ cho sự kiện gói/khung/hẹn giờ|
|				|start_timer(seq_nr)|Bắt đầu đếm ngược đếm ngược|
|				|stop_timer(seq_nr)|Ngừng đếm ngược từ khi chạy|
|				|start_ack_timer()|Bắt đầu bộ đếm ngược ACK|
|				|stop_ack_timer()|Ngừng đồng hồ đếm ngược ACK|

<a name="3.2"></a>
##### 3.2.Utopian Simplex Protocol

Một giao thức optimistic (p1) để giúp chúng tôi bắt đầu
- Giả sử không có lỗi, và nhận nhanh như người gửi
- Xem xét chuyển dữ liệu một chiều
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/12.png"></p>

Đó là nó, không có lỗi hoặc kiểm soát dòng chảy .

<a name=3.3"></a>
##### 3.3.Stop-and-Wait Protocol for Error-free channel

Giao thức (p2) đảm bảo người gửi không thể vượt qua người nhận:
- Người nhận trả về một khung giả (ACK) khi đã sẵn sàng
- Mỗi lần chỉ có một khung - được gọi là stop-and-wait
- Chúng thêm kiểm soát luồng!
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/13.png"></p>

<a name="3.4"></a>
##### 3.4.Stop-and-Wait Protocol for Noisy channel

ARQ (Automatic Repeat reQuest) cho biết thêm kiểm soát lỗi
- Các frame ACK người nhận được gửi đúng
- Người gửi bộ đếm thời gian và gửi lại khung nếu không ACK)

Đối với sự chính xác, khung và ACK phải được đánh số
- Người nhận khác không thể nói retransmission (do mất ACK hoặc early timer) từ khung mới
- Đối với dừng và chờ đợi, 2 số (1 bit) là đủ

Các giao thức trong đó người gửi chờ đợi một sự xác nhận tích cực trước khi chuyển sang mục dữ liệu tiếp theo thường được gọi là ARQ (*Automatic Repeat reQuest*) hoặc PAR (*Posceptative Acknowledgement with Retransmission*).

Sender loop (p3):
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/14.png"></p>

1: Gửi khung (hoặc truyền lại)
2: Đặt hẹn giờ cho truyền lại
3: Chờ ACK hoặc timeout
4: Nếu ACK trả lời tốt sau đó thiết lập cho khung tiếp theo để gửi (nếu khác khung cũ sẽ được retransmitted)

Receiver loop (p3):
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/15.png"></p>

1: Đợi Frame
2: Nếu mới, hãy lấy nó và dự phòng khung trước
3: Ack hiện hành

<a name="4"></a>
#### 4. Sliding Window Protocols
<a name="4.1"></a>
##### 4.1. Sliding Window concept

Người gửi duy trì cửa sổ của khung mà nó có thể gửi
- Cần đệm chúng để có thể truyền lại
- Cửa sổ advances với acknowledgements tiếp theo

Người nhận duy trì cửa sổ khung hình mà nó có thể nhận được
- Cần giữ không gian đệm cho khách đến
- Các advances của cửa sổ với yêu cầu đặt hàng

Một cửa sổ trượt tiến tới người gửi và người nhận
- Ví dụ: kích thước cửa sổ là 1, với một số thứ tự 3-bit.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/16.png"></p>

Các cửa sổ lớn hơn cho phép sử dụng **pipelining** hiệu quả hơn
- Stop-and-wait (w = 1) là không hiệu quả cho các liên kết dài
- Cửa sổ tốt nhất (w) phụ thuộc vào độ trễ băng thông (BD)
- Muốn w ≥ 2BD + 1 để đảm bảo sử dụng liên kết cao

**Pipelining** dẫn đến sự lựa chọn khác nhau cho lỗi / buffering
- Chúng ta sẽ xem xét *Go-Back-N* và *Selective Repeat*

Kỹ thuật tạm thời trì hoãn các acknowledgements gửi đi để chúng có thể được nối vào khung dữ liệu gửi đi tiếp theo được gọi là *piggybacking*

<a name="4.2"></a>
##### 4.2. One-bit Sliding Window

Truyền dữ liệu theo cả hai hướng với tính dừng và chờ
- Piggyback ACK trên khung dữ liệu ngược lại cho hiệu quả
- Xử lý lỗi truyền tải, điều khiển luồng, bộ đếm thời gian sớm

Each node is sender and receiver (p4):
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/17.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/18.png"></p>

Hai kịch bản cho thấy tương tác tinh tế tồn tại trong p4:
- Bắt đầu đồng thời [right] gây ra hoạt động chính xác nhưng chậm so với bình thường [left] do truyền lặp lại.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/19.png"></p>

<a name="4.3"></a>
##### 4.3. Go-Back-N

Người nhận chỉ chấp nhận / ACK khung đến có thứ tự:
- Loại bỏ các khung đi theo khung bị mất / bị lỗi
- Người gửi thời gian ra và gửi lại tất cả các khung hình nổi bật
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/20.png"></p>

Thương mại được thực hiện cho Go-Back-N:
- Chiến lược đơn giản cho người nhận; Chỉ cần 1 khung
- Lỗi liên kết băng thông cho các lỗi với cửa sổ lớn; Toàn bộ cửa sổ sẽ được truyền lại

Thực hiện như p5 (xem mã trong cuốn sách)

<a name="4.4"></a>
##### 4.4. Selective Repeat

Bộ nhận nhận khung bất cứ nơi nào trong cửa sổ nhận
- ACK tích lũy cho thấy khung đặt hàng cao nhất
-  NAK (negative ack)  gây ra người gửi truyền lại của một khung thiếu trước khi timeout bật trên cửa sổ
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/21.png"></p>

Thương mại được thực hiện cho Selective Repeat:
- Nên phức tạp hơn Go-Back-N do đệm ở bộ thu và nhiều bộ định ở người gửi
- Sử dụng băng thông liên kết hiệu quả hơn khi chỉ những khung hình bị mất mới bị phản bội (với tỷ lệ lỗi thấp)

Thực hiện như p6 (xem mã trong cuốn sách)

Để chính xác, chúng tôi yêu cầu:
- Số trình tự ít nhất hai lần cửa sổ (w)
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/22.png"></p>

<a name="4.5"></a>
##### 4.5. Hak 5 Resources

TCP Flow Control https://www.youtube.com/watch?v=McDNzBvRPHA

Using Wireshark https://www.youtube.com/watch?v=2ircAIQ7U2A

<a name="5"></a>
#### 5. Example Data Link Protocols
<a name="5.1"></a>
##### 5.1. Packet over SONET

Packet trên SONET là phương pháp được sử dụng để mang các gói tin IP qua đường kết nối sợi quang SONET
- Sử dụng PPP (Point-to-Point Protocol) để định khung
- giao thức phổ biến nhất được sử dụng trên các protocol over rộng diện tích tạo nên xương sống của mạng truyền thông
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/23.png"></p>

<a name="5.2"></a>
##### 5.2. PPP (Point-to-Point Protocol)

PPP (Point-to-Point Protocol) là một phương pháp chung để phân phối các gói tin qua các liên kết
- Khung hình sử dụng cờ (0x7E) và nhồi bưu
- "Unnumbered mode" (connectionless unacknow-ledged service) được sử dụng để mang các gói tin IP
- Lỗi được phát hiện bằng tổng kiểm tra
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/24.png"></p>

Một giao thức điều khiển liên kết mang lại kết nối PPP lên / xuống
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/25.png"></p>

<a name="5.3"></a>
##### 5.3. ADSL (Asymmetric Digital Subscriber Loop)

Được sử dụng rộng rãi cho Internet băng thông rộng qua các vòng lặp cục bộ
- ADSL chạy từ modem (khách hàng) sang DSLAM (ISP)
- Các gói tin IP được gửi qua PPP và AAL5 / ATM (over)
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/26.png"></p>

Dữ liệu PPP được gửi trong khung AAL5 trên các ô của ATM:
- ATM là một lớp liên kết sử dụng các tế bào có kích thước cố định, ngắn (53 byte); Mỗi tế bào có một bộ nhận dạng mạch ảo
- AAL5 là một định dạng để gửi các gói tin qua ATM
- PPP frame được chuyển thành khung AAL5 (PPPoA)
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/27.png"></p>

<a name="II"></a>
### II. Tài liệu dịch

Lecture 3: Data Link Layer  http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm
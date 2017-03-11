## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **11/03/2017**

### Mục lục

[1. OSI Physical Layer](#1)

- [1.1. Review OSI Layer Services](#1.1)
- [1.2. Physical Layer Protocols & Services](#1.2)
- [1.3. Physical Layer Standards](#3)
- [1.4. Data Carrying Capacity of a Network](#1.3)

[2. Signaling Methods](#2)

- [2.1 Non Return to Zero (NRZ) Signaling](#2.1)
- [2.2 Manchester Encoding ](#2.2)
- [2.3 NRZ vs Manchester Encoding](#2.3)
- [2.4. Encoding ](#2.4)
- [2.5. Code Groups ](#2.5)
- [2.6. Characteristics & Uses of Network Media ](#2.6)

[3. Copper Media – UTP, STP, Coaxial  ](#3)

- [3.1. Unshielded Twisted-Pair (UTP)  ](#3.1)
- [3.2. UTP Standards ](#3.2)
- [3.3. UTP Cable Types ](#3.3)
- [3.4. UTP Connectors  ](#3.4)
- [3.5. Shielded Twisted-Pair (STP) Cable ](#3.5)
- [3.6. Coaxial Cable ](#3.6)
- [3.7. Safety issues when working with copper cabling ](#3.7)
- [3.8. Fiber-optic Cabling](#3.8)
- [3.9. Two Types of Fiber Cable](#3.9)

[4. Wireless ](#4)

- [4.1. Wireless Media  ](#4.1)
- [4.2. Wireless Standards ](#4.2)
- [4.3. Wireless LANs (WLAN, Wi-fi) ](#4.3)
- [4.4. WLAN Standards ](#4.4)

[5. Tài liệu dịch ](#5)

<a name="1"></a>
### 1. OSI Physical Layer

<a name="1.1"></a>
#### 1.1. Review OSI Layer Services
![Imgur](http://i.imgur.com/aWwPArP.png)

<a name="1.2"></a>
#### 1.2. Physical Layer Protocols & Services
- Mục đích của lớp Vật lý là tạo ra tín hiệu điện, quang hoặc sóng đại diện cho các bit trong mỗi khung.
- Ba chức năng cơ bản là:
	- Data encoding (mã hóa dữ liệu): 
	*Phương pháp chuyển đổi một luồng dữ liệu thành đoạn 'code'*
	- Signaling (báo hiệu):
	*làm thế nào các bit được biểu diễn trên các phương tiện vật lý*
	- Các thành phần vật lý:
	*kết nối và cáp*

<a name="1.3"></a>
#### 1.3. Physical Layer Standards
- TCP/IP Standards set by:
	- IETF : Internet Engineering Task Force
- Standards set by:
	- ISO : International Organization for Standardization
	- IEEE : Institute of Electrical and Electronics Engineers
	- ANSI : American National Standards Institute
	- ITU :  International Telecommunication Union
	- EIA/TIA : Energy Information Administration/Transient Ischemic Attack
	- FCC :  Federal Communications Commission
![Imgur](http://i.imgur.com/1ji7xyl.png)

<a name="1.4"></a>
#### 1.4. Data Carrying Capacity of a Network (khả năng mang dữ liệu của một mạng):

Băng thông kỹ thuật số được đo bằng *bit / giây*: Bps, kbps, Mbps, Gbps, Tbps

<a name="2"></a>
### 2. Signaling Methods
Phương pháp đại diện cho các bit được gọi là **Signaling Methods**
	- Các chuẩn của lớp Vật lý phải xác định loại tín hiệu đại diện cho "1" và "0".
	- Non Return to Zero (NZR) là phương pháp đơn giản nhất sử dụng cho Signaling Methods.
	*Điện áp thấp đại diện cho logic 0, cao là logic 1.
	Không hiệu quả. Chỉ thích hợp cho các liên kết chậm.
	Vấn đề kéo dài của bit cá nhân - không đồng bộ .

<a name="2.1"></a>
#### 2.1. Non Return to Zero (NRZ) Signaling
![Imgur](http://i.imgur.com/l2ruIhw.png)
- Người nhận lấy mẫu vật liệu vào giữa bit-time.
- Trên mạng LAN, đồng hồ ở Người gửi và Người nhận được đồng bộ bằng cách ghi nhớ sự chuyển tiếp giữa điện áp cao và thấp.
- Nếu một số liên tiếp 1 hoặc 0 được truyền đi, các đồng hồ có thể trôi dạt khỏi đồng bộ và người nhận miss-read một chút.

<a name="2.2"></a>
#### 2.2 Manchester Encoding
- Người nhận miss-read một chút. Các phương pháp báo hiệu được sử dụng bởi 10BaseT Ethernet (10Mbps)
- Sự chuyển đổi từ điện áp thấp sang điện áp cao thể hiện một giá trị bit là 1.
- Sự chuyển đổi từ điện áp cao sang điện áp thấp thể hiện giá trị bit là 0.
- Vì mỗi bit liên quan đến quá trình chuyển đổi, các đồng hồ có thể sẽ được giữ nguyên.

<a name="2.3"></a>
#### 2.3 NRZ vs Manchester Encoding
![Imgur](http://i.imgur.com/MNGgOrt.png)

- Tín hiệu điện trên đường truyền cáp đồng:
![Imgur](http://i.imgur.com/r0JMbNe.png)
- Tín hiệu xung ánh sáng:
![Imgur](http://i.imgur.com/qmDBHoO.png)
- Tín hiệu sóng (Wireless):
![Imgur](http://i.imgur.com/T2SBAct.png)

<a name="2.4"></a>
#### 2.4. Encoding
![Imgur](http://i.imgur.com/ZpLQwpM.png)
- 1
	- 1. Mô hình tín hiệu vật lí cụ thể biểu thị bắt đầu của khung.
	- 1. Mẫu bit cụ thể biểu thị bắt đầu của khung.
- 2
	- 2. Các tín hiệu vật lí đại diện cho nội dung của khung.
	- 2. Mẫu bit mô tả nội dung khung truyền đến Data Link Layer.
- 3 
	- 3. Mô hình tín hiệu vật lí cụ thể biểu thị kết thúc của khung.
	- 3. Mẫu bit cụ thể biểu thị kết thúc của khung.
- 4
	- 4. Các tín hiệu phân giải ngẫu nhiên trên phương tiện vật lí
	do bị nhiễu
	- 4. Các tín hiệu không được giải mã và không truyền vào data link.

<a name="2.5"></a>
#### 2.5. Code Groups
- Một nhóm mã là một dãy liên tiếp các bit mã (symble) được giải thích và ánh xạ như các mẫu bit dữ liệu.
- Mặc dù việc sử dụng các nhóm mã giới thiệu ở trên dưới dạng các bit bổ sung để truyền, chúng cải thiện tính mạnh mẽ của một liên kết truyền.
- Ưu điểm sử dụng các nhóm mã bao gồm:
	- Giảm lỗi level bit
	- Hạn chế tiêu hao năng lượng truyền vào môi trường
	- Giúp phân biệt các bit dữ liệu từ các bit điều khiển
- Trang trình bày tiếp theo cho thấy việc lập bản đồ cho nhóm mã 4B / 5B. Các mã khác nói chung phức tạp hơn
![Imgur](http://i.imgur.com/999G13L.png)

<a name="2.6"></a>
#### 2.6. Characteristics & Uses of Network Media (đặc điểm và Sử dụng Mạng Truyền thông):
![Imgur](http://i.imgur.com/P8eoPcL.png)
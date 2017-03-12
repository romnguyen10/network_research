## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **12/03/2017**

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

<a name="3"></a>
### 3. Copper Media – UTP, STP, Coaxial:
- Các sóng vô tuyến điện và các thiết bị điện từ là thiết bị tiềm ẩn nguy cơ gây nhiễu.
- Loại cáp được thiết kế để giảm thiểu sự xuống cấp của tín hiệu do tiếng nhiễu điện.
 
![Imgur](http://i.imgur.com/W0ZY2e4.png)

<a name="3.1"></a>
#### 3.1. Unshielded Twisted-Pair (UTP):

- Đây là phương tiện phổ biến nhất được sử dụng cho mạng LAN.
- Tương đối dễ cài đặt
![Imgur](http://i.imgur.com/w27zcVS.png)
![Imgur](http://i.imgur.com/FxwnIm8.png)

<a name="3.2"></a>
#### 3.2. UTP Standards 
- TIA / EIA-568A quy định các tiêu chuẩn, cáp thương mại cho việc lắp đặt mạng LAN
- Chuẩn IEEE của Cáp UTP, Loại 5 (Cat5), Loại 5e (Cat5e), Loại 6 (Cat6).
- Nhiễu xuyên âm là nhiễu do từ trường xung quanh các cặp dây liền nhau trong cáp.
- Các cặp xoắn của dây dẫn giúp ngăn ngừa nhiễu xuyên âm
- Tiêu chuẩn xác định số vòng xoắn trên mét
- Sử dụng đầu RJ45 và đầu nối .

<a name="3.3"></a>
#### 3.3. UTP Cable Types
- Cáp thẳng:
	- Kết nối thiết bị với thiết bị chuyển mạch và hub
- Cáp chéo:  
	- Kết nối PC với PC,
	- Kết nối Switch với Switch
	- Kết nối PC với  Router
- Cáp console
	- Quyền sở hữu của Cisco - Đối với quản lý thiết bị

![Imgur](http://i.imgur.com/ZY4Gx9E.png)
![Imgur](http://i.imgur.com/gWOYppf.png)

<a name="3.4"></a>
#### 3.4. UTP Connectors 
- Đầu nối có kết nối kém là một nguyên nhân nghiêm trọng của lỗi mạng
![Imgur](http://i.imgur.com/4mYNXLA.png)

<a name="3.5"></a>
#### 3.5. Shielded Twisted-Pair (STP) Cable 
- Sử dụng trong cài đặt mạng Token Ring.
- Chuẩn 10 GB mới cho Ethernet có một điều khoản cho việc sử dụng cáp STP.
- Đắt hơn UTP, khó khăn hơn trong việc lắp đặt
![Imgur](http://i.imgur.com/AKNI229.png)

<a name="3.6"></a>
#### 3.6. Coaxial Cable 
- Cáp đồng trục được sử dụng để gắn ăng-ten với các thiết bị không dây
- Ban đầu được sử dụng bởi các mạng truyền hình cáp, bây giờ sử dụng sợi và lõi đưa tín hiệu từ đường vào nhà ở.
- Kết hợp sử dụng sợi và lõi được gọi là Hybrid Fiber Coax (HFC).
- Được thay thế bằng UTP và cáp quang trong các thiết bị Ethernet. dây dày, dây mỏng
- Đầu nối BNC
![Imgur](http://i.imgur.com/UJB7gGY.png)

<a name="3.7"></a>
#### 3.7. Safety issues when working with copper (vấn đề an toàn khi làm việc với cáp đồng):
- Nguy hiểm điện - nối đất.
- Nguy hiểm với Lửa - cáp dễ cháy, sản sinh ra hơi độc

	- việc tách dữ liệu và cáp phải tuân theo mã an toàn
	- Cáp phải được kết nối 1 cách chính xác
	- Việc lắp đặt phải được kiễm tra, tránh gây thiệt hại
	- thiết bị phải được nối đất đúng cách
	![Imgur](http://i.imgur.com/qtgwT2l.png)

<a name="3.8"></a>
#### 3.8. Fiber-optic Cabling
- Sử dụng sợi thủy tinh hoặc sợi nhựa để hướng các xung ánh sáng từ nguồn đến đích.
- Tỷ lệ khả năng  băng thông dữ liệu thô rất lớn.
- Miễn dịch với sự Nhiễu từ sóng điện từ và các vấn đề nối đất.
- Giảm tín hiệu thấp, hoạt động ở độ dài lớn hơn nhiều.
- Đắt hơn cáp đồng
- Các kỹ năng và thiết bị khác nhau cần thiết để ngắt và nối kết cơ sở hạ tầng cáp
- Cần xử lý cẩn thận hơn đối với cáp đồng

<a name="3.9"></a>
#### 3.9. Two Types of Fiber Cable
- Sợi được sử dụng chủ yếu cho
	- Đường trục cáp cho điểm lưu lượng truy cập cao điểm
	- Kết nối các tòa nhà trong tòa nhà nhiều tầng trường. (Không có vấn đề nối đất)
- Hai loại sợi: 

	- Multimode    50/125, 62.5/125
		- Rẻ hơn, sử dụng nguồn ánh sáng LED
		- Lõi lớn hơn, 50 micron hoặc hơn
		- Phân tán nhiều hơn và do đó gây mất tín hiệu
		- Được sử dụng cho khoảng cách dài ứng dụng lên đến khoảng 2 km
		- Sử dụng đèn LED làm ánh sáng nguồn

	- Singlemode 8/125, 10/125
		- Sử dụng laser, hoạt động trên khoảng cách dài hơn.
		- Lõi nhỏ
		- Ít phân tán
		- Thích hợp cho đường dài
		- Sử dụng (lên đến 100 km, 62 dặm)
		- Sử dụng laser làm  ánh sáng nguồn
	![Imgur](http://i.imgur.com/33ly9d6.png)

<a name="4"></a>
### 4. Wireless
<a name="4.1"></a>
#### 4.1. Wireless Media
- Cung cấp cho thiết bị di động cho người dùng
- Nhạy cảm với nhiễu
- Vấn đề an ninh
![Imgur](http://i.imgur.com/glLNcwo.png)

<a name="4.2"></a>
#### 4.2. Wireless Standards
-IEEE 802.11 - Wi-Fi: là một mạng LAN không dây (WLAN)
	- Công nghệ sử dụng là contention hoặc non-deterministic hệ thống với một Carrier Sense Multiple Access / Collision Avoidance (CSMA/CA) quá trình truy cập phương tiện truyền thông.
- IEEE 802.15 - Bluetooth, sử dụng quá trình ghép nối thiết bị để giao tiếp trên khoảng cách từ 1 đến 100 mét.
- IEEE 802.16 - WiMAX (Khả năng tương tác trên toàn thế giới (Microwave access), sử dụng một topo point-to-multipoint để cung cấp truy cập băng thông rộng không dây.
- Hệ thống toàn cầu cho truyền thông di động (GSM) - cung cấp truyền dữ liệu qua  điện thoại di động, mạng di động 
- Truyền thông vệ tinh.

<a name="4.3"></a>
#### 4.3. Wireless LANs (WLAN, Wi-fi)
- Mạng LAN không dây yêu cầu các thiết bị mạng sau:
	- Wireless Access Point (AP) - Tập trung các tín hiệu không dây từ người dùng và kết nối, thường là thông qua cáp đồng, với cơ sở hạ tầng mạng đồng sẵn có như Ethernet.
	- Wireless NIC adapters - Cung cấp khả năng truyền tín hiêu không dây cho từng máy chủ lưu trữ mạng.

<a name="4.4"></a>
#### 4.4. WLAN Standards
- IEEE 802.11a - Dãy tần số 5 GHz - lên đến 54 Mbps.
- IEEE 802.11b - Hoạt động ở băng tần 2,4 GHz và cung cấp tốc độ lên đến 11 Mbps. Đây là tiêu chuẩn được sử dụng phổ biến nhất
- IEEE 802.11g - Hoạt động ở băng tần 2,4 GHz và cung cấp tốc độ lên đến 54 Mbps.
- Chuẩn IEEE 802.11n hiện đang ở dạng dự thảo. 2,4 Ghz hoặc 5 GHz, tốc độ dữ liệu 100 Mbps đến 210 Mbps với khoảng cách khoảng 70 mét.
	

<a name="5"></a>
### 5. Tài liệu dịch
Slide http://www.scit.wlv.ac.uk/~in8297/cisco/expl1/lectures/Expl08.pdf
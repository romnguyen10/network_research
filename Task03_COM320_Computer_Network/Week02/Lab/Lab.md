## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **20/03/2017**

### Mục lục
[I. Ethernet](#I)

- [1. Mục tiêu](#1)

- [2. Yêu cẩu](#2)

	- [2.1. Wireshark](#2.1)
	- [2.2. Step 1: Capture a Trace](#2.2)
	- [2.3. Step 2: Inspect the Trace](#2.3)
	- [2.4. Step 3: Ethernet Frame Structure](#2.4)
	- [2.5. Step 4: Scope of Ethernet Addresses](#2.5)
	- [2.6. Step 5: Broadcast Frames](#2.6)
	- [2.7. Step 6 - IEEE 802.3 ](#2.7)

	
[II. Netstat](#II)

[III. NetInfo](#III)

[IV. Tài liệu dịch](#IV)

------------------ 

<a name="I"></a>
### I. Ethernet

<a name="1"></a>
#### 1. Mục tiêu

- Để tìm hiểu các chi tiết của khung Ethernet. Ethernet là một lớp liên kết các giao thức khá phổ biến. Các máy tính hiện đại kết nối với thiết bị switch Ethernet hơn là sử dụng Ethernet cổ điển(classic).
- File chứa tệp ở đây: http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-ethernet.pcap.

<a name="2"></a>
#### 2. Yêu cẩu

<a name="2.1"></a>
##### 2.1. Wireshark

**Wireshark**: trong bài lab này sử dụng công cụ phần mềm Wireshark để bắt và kiểm tra gói tin bắt được. Một gói tin được tìm thấy là một bản ghi của lưu lượng truy cập tại một vị trí trên mạng, như thể chụp nhanh tất cả các bit truyền qua một đường dây cụ thể. gói tin bắt được ghi lại dấu thời gian cho mỗi gói tin, cùng với các bit tạo nên gói tin, từ các tiêu đề lớp thấp đến các nội dung lớp cao hơn. Hướng dẫn trợ giúp nhanh cho bộ lọc hiển thị Wireshark là ở đây: http://openmaniak.com/wireshark_filters.php

- 1. Launching Wireshark:
	Bạn có thể nhập Wireshark trong hộp chạy của màn hình chính của Windows 8. Nó nên được tải nhưng có thể gặp Wireshark vấn đề với cấu hình Lab mới và trình điều khiển định dạng. Vì vậy, nếu điều này không làm việc thì hãy làm theo bước tiếp theo.
	![Imgur](http://i.imgur.com/2phGtOI.png)
- 2. Khởi chạy Wireshark như sau: Nhấp vào icon PC trên màn hình desktop và sử dụng tệp để browser đến C:\local Đĩa (C)\Program Files\Wireshark
	![Imgur](http://i.imgur.com/bGaImJf.png)
- 3. kế tiếp, click chuột phải vào Wireshark chọn **“Run as administrator”**
	![Imgur](http://i.imgur.com/2zd0jjR.png)
- 4. Sau đó bạn sẽ có được một màn hình khởi động, như được hiển thị tiếp theo:
	![Imgur](http://i.imgur.com/Lr54uYA.png)
- 5. Hãy nhìn vào phía trên bên trái của màn hình - bạn sẽ thấy một "Danh sách giao diện". Đây là danh sách các giao diện mạng trên máy tính của bạn. Một khi bạn chọn một giao diện, Wireshark sẽ nắm bắt tất cả các gói tin trên giao diện đó. Nhấp vào card mạng trên máy tính bạn đang làm việc trên. Trong ví dụ trên, nó là Trình điều khiển Ethernet để bắt đầu thu thập gói tin (ví dụ: đối với Wireshark để bắt đầu thu tất cả các gói được gửi đến / từ giao diện đó), một màn hình giống như dưới đây sẽ được hiển thị, hiển thị thông tin về các gói bị bắt . Một khi bạn bắt đầu chụp gói, bạn có thể dừng nó bằng cách sử dụng trình đơn kéo xuống Capture và chọn Stop \ Wireshark
	![Imgur](http://i.imgur.com/qq9s6Ix.png)

<a name="2.2"></a>
##### 2.2. Step 1: Capture a Trace
*Tiến hành như sau để nắm bắt một dấu vết của các gói tin ping. Nhấp chuột phải và chọn "Save Link As" và xuống các tập tin dấu vết sau đây 
http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-ethernet.pcap*

- 1. Mở tệp sau đây từ vị trí bạn đã tải xuống ví dụ: Local Disk (C):\downloads.
- 2. Bạn sẽ thấy một màn hình tương tự như sau:
	![Imgur](http://i.imgur.com/jvbkOfj.png)
- 3. Lọc **"icmp"** và nhấp vào apply.
	*Cửa sổ chụp của bạn phải giống với hình chụp bên dưới, trừ điểm nhấn của chúng tôi*
	![Imgur](http://i.imgur.com/VuV9lmK.png)

<a name="2.2"></a>
##### 2.3. Inspect the Trace
- *Chọn bất kỳ gói tin nào trong dấu vết (trong bảng trên cùng) để xem chi tiết về cấu trúc của nó (trong bảng điều khiển giữa) và các byte tạo thành gói tin (trong bảng dưới cùng)*. Bây giờ chúng ta có thể kiểm tra các chi tiết của các gói tin.
Trong hình, chúng ta đã chọn gói đầu tiên trong dấu vết. Lưu ý rằng chúng tôi đang sử dụng cụm từ "Packet" một cách lỏng lẻo. Mỗi bản ghi được bắt bởi Wireshark chính xác hơn tương ứng với một khung đơn trong định dạng Ethernet mang một gói như là tải trọng của nó; Wireshark lí giải càng nhiều cấu trúc càng tốt.
- *Trong bảng điều khiển trung, mở rộng trường tiêu đề Ethernet (sử dụng "+" trình mở rộng hoặc biểu tượng) để xem chi tiết của họ*.Quan tâm của chúng tôi là tiêu đề Ethernet, và bạn có thể bỏ qua các giao thức lớp cao hơn (đó là IP Và ICMP trong trường hợp này). Lưu ý những điều sau:
![Imgur](http://i.imgur.com/JZK4TJJ.png)
	- Các khung trong dấu vết này là DIX Ethernet, được gọi là "Ethernet II" trong Wireshark.
	![Imgur](http://i.imgur.com/EWnFqGA.png)
	- Không có lời mở đầu trong các lĩnh vực được hiển thị trong Wireshark. Lời mở đầu là một lớp cơ chế vật lý để giúp cho NIC xác định bắt đầu của một khung. Nó không chứa dữ liệu hữu ích và không nhận được như các lĩnh vực khác.
	- Có địa chỉ đích và địa chỉ nguồn. Wireshark giải mã một số bit này trong phần OUI (Organizationally Unique Identifier) của địa chỉ để cho chúng tôi biết nhà cung cấp NIC, ví dụ: Dell cho địa chỉ nguồn.
	-  Có một trường Type. Đối với các thông báo ping, loại Ethernet là IP, nghĩa là Ethernet payload mang một gói tin IP. (Không có trường độ dài như ở định dạng IEEE 802.3. Thay vào đó, độ dài của khung DIX Ethernet được xác định bởi phần cứng của máy nhận, trong đó tìm kiếm các khung bắt đầu bắt đầu bằng lời mở đầu và kết thúc bằng một tổng kiểm tra chính xác và Vượt qua các lớp cao hơn cùng với gói.)
	- Không có trường data field per se - dữ liệu bắt đầu với IP header ngay sau  Ethernet header.
	- Không có pad. Pad sẽ có mặt ở cuối khung nếu không sẽ nhỏ hơn 64 Byte, kích thước khung Ethernet tối thiểu.-
	- Không có kiểm tra trong hầu hết các dấu vết, mặc dù nó thực sự tồn tại. Thông thường, phần cứng Ethernet máy tính đang gửi hoặc nhận khung hoặc kiểm tra trường này và thêm hoặc phân giải nó. Do đó nó chỉ đơn giản là không hiển thị cho hệ điều hành hoặc Wireshark trong hầu hết các thiết lập bắt.
	- Cũng không có trường VLAN. Nếu VLAN được sử dụng, các thẻ VLAN thường được thêm vào và lấy ra bởi các switch port để chúng không hiển thị trên máy chủ lưu trữ sử dụng mạng.

**Questions**:
- Q1. Địa chỉ MAC nguồn của # 1 từ địa chỉ IP 128.208.2.151 là gì?
- Q2. Nhấp vào # 12 và mở rộng phần [+] Address Resolution Protocol ở phần giữa. Địa chỉ MAC mục tiêu là gì: 00: 00: 00: 00: 00: 00 nghĩa là gì?
- Q3. Nhấn lần nữa vào # 12 và mở rộng phần [+] Address Resolution Protocol ở khung giữa. Tại sao loại giao thức được liệt kê như IP khi nó không phải là một gói tin IP?

**Answers**:
- A1. Địa chỉ MAC là 00: 25: 64: d5: 10: 8b.
- A2. ARP sử dụng MAC broadcast address dành riêng 00: 00: 00: 00: 00: 00 trong yêu cầu ARP để tìm kiếm địa chỉ IP của 128.208.2.42. Sau đó lưu trữ thông tin đó trong một bộ nhớ  ARP Cache cục bộ cho phép truyền thông không giới hạn với 128.208.2.42 (trong một khoảng thời gian) mà không cần phải broadcast thêm nữa. Cũng lưu ý rằng nó đã biết địa chỉ IP nhưng nó cần một địa chỉ MAC để biết nó là máy thực tế.
- A3. Kiểu giao thức ARP được đặt thành 'IP' bởi vì chúng tôi đang yêu cầu ARP giải quyết một địa chỉ IP. ARP có thể được sử dụng để giải quyết các địa chỉ cho các giao thức mạng khác.

<a name="2.4"></a>
##### 2.4. Step 3: Ethernet Frame Structure

- Cố gắng hiểu định dạng khung Ethernet. Lưu ý phạm vi của Ethernet header và Ethernet payload. Xem cấu trúc khung bên dưới trong Hình 5.
*Để làm việc với kích thước, hãy quan sát rằng khi bạn nhấp vào khối giao thức trong bảng điều khiển trung tâm (chính khối đó, không phải trình mở rộng "+") thì Wireshark sẽ làm nổi bật các byte nó tương ứng trong gói tin ở bảng dưới và hiển thị chiều dài Ở cuối cửa sổ. Bạn cũng có thể sử dụng kích thước gói tổng thể được hiển thị trong ngăn Chiều dài hoặc Khối chi tiết khung*

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/8.png"></p>

Có một số tính năng cần lưu ý:
- Địa chỉ đích đến trước địa chỉ nguồn.
- Các pad không được hiển thị bởi vì các gói tin chúng tôi kiểm tra (ping) đủ lớn để không cần có pad.
- Không giống nhiều giao thức, Ethernet có một đoạn giới thiệu (checksum, và pad nếu có) cũng như header. Khoản kiểm tra được xử lý bởi phần cứng và không hiển thị đối với Wireshark.
- Ethernet header dài 14 byte.

**Lưu ý:** Các câu trả lời cho những câu hỏi này là ở cuối của các ghi chú trong bài lab:
- Q1. Nhấp vào #12 và mở rộng phần [+] Address Resolution Protocol ở phần giữa. Opcode(1) có ý nghĩa gì? Opcode(2) có ý nghĩa gì?
(Lưu ý: Trong một số phiên bản Wireshark, opcode(1) được liệt kê dưới dạng (0x0001) & opcode(2) được liệt kê dưới dạng (0x0002)
- Q2. Nhấp vào #12 và mở rộng [+] và đưa ra giá trị thập lục phân cho trường Ethernet 2 byte?

**Trả lời**:
- A1. Opcode (1) hoặc (0x0001) có nghĩa là ARP request và opcode (2) hoặc (0x0002) có nghĩa là ARP reply.
- A2. Giá trị hex cho trường Loại Ethernet frame là 0x0806, cho ARP.

<a name="2.5"></a>
##### 2.5. Step 4: Scope of Ethernet Addresses
Mỗi khung Ethernet mang một địa chỉ nguồn và đích. Một trong những địa chỉ này là địa chỉ PC của bạn. Nó là nguồn cho các khung được gửi, và đích đến cho các khung nhận được. Nhưng địa chỉ khác là gì? Giả sử bạn PING một máy chủ Internet từ xa, nó không thể là địa chỉ Ethernet của máy chủ từ xa bởi vì một khung Ethernet chỉ được gửi đến để đi trong một mạng LAN. Thay vào đó, nó sẽ là địa chỉ Ethernet của router hoặc default gateway, chẳng hạn như AP của bạn trong trường hợp của 802.11. Đây là thiết bị kết nối mạng LAN của bạn với phần còn lại của Internet. Ngược lại, các địa chỉ IP trong khối IP trong mỗi gói tin cho biết các điểm cuối nguồn và đích tổng thể. Đó là máy tính của bạn và máy chủ từ xa.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/1.png"></p>

- 1. Mở Wireshark và bắt đầu bắt mới. Bạn có thể muốn xóa bộ lọc hiện tại hoặc chỉ cần đóng và khởi động lại Wireshark để đảm bảo bắt lại.
- 2. Trong hộp bộ lọc, gõ ip.src sau đây == youripaddress ví dụ: Ip.src == 193.61.191.71 (Lưu ý .... Bạn có thể xem địa chỉ IP của bạn bằng cách chạy cmd 
	prompt và gõ ipconfig / all)
- 3. Yêu cầu đồng nghiệp của bạn tìm địa chỉ IP của họ, ví dụ: 193.61.191.71
- 4. Trong Windows 8, mở cửa sổ dòng lệnh bằng cách gõ <WINDOWS KEY> + R và gõ cmd trong hộp thoại run để bật lên.
- 5. Gõ ping youripaddress ví dụ: Ping 193.61.191.71
- 6. Trở lại Wireshark và dừng chụp bằng cách chọn dừng trong trình đơn Capture hoặc biểu tượng dừng chụp bên dưới nhãn của trình đơn chính

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/2.png"></p>
    <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/3.png"></p>
    <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/4.png"></p>

Có một số tính năng cần lưu ý:
- Địa chỉ Ethernet và địa chỉ IP sẽ thay đổi cho truy tìm của bạn vì có nhiều máy tính khác nhau tham gia, nhưng chúng sẽ có cùng một dạng, ví dụ: 6 byte theo định dạng thập lục phân hoặc 4 byte "dotted".
- Các địa chỉ Ethernet và IP tương ứng với máy tính của bạn và máy tính cá nhân đồng nghiệp của bạn.
- Một số địa chỉ Ethernet và IP không được biết đến khi truy tìm. Chúng được hiển thị là "??".

<a name="2.6"></a>
##### 2.6. Step 5: Broadcast Frames

- 1. Việc truy tìm của bạn thu thập được ở trên lưu lượng truy cập Ethernet unicast được gửi giữa một nguồn  và đích đến cụ thể, ví dụ: máy tính của bạn với bộ định tuyến. Cũng có thể gửi lưu lượng Ethernet multicast hoặc broadcast, tương ứng cho một nhóm máy tính hoặc tất cả các máy tính trên mạng Ethernet. Chúng ta có thể nói địa chỉ đó là unicast, multicast, hay broadcast. Broadcast traffic được gửi đến một địa chỉ Ethernet dành riêng có tất cả các bit bằng "1". Lưu lượng multicast được gửi đến các địa chỉ có bit đầu tiên bằng "1"  được gửi trên dây; broadcast là một trường hợp đặc biệt của multicast. Lưu lượng Broadcast và multicast được sử dụng rộng rãi cho các giao thức discovery, ví dụ: một gói tin được gửi tới tất cả mọi người trong nỗ lực tìm kiếm máy in cục bộ.- 1. Bắt đầu chụp cho khung Ethernet phát và multicast với một bộ lọc **"ether multicast"**. Bạn thực hiện việc này bằng cách chọn Capture trong menu chính và sau đó chọn Options. Không được nhầm lẫn với hộp lọc trên trang chụp trực tiếp sẽ không chấp nhận biểu thức lọc ở trên.

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/5.png"></p>

- 2. Chờ đến 30 giây để ghi lại lưu lượng truy cập nền và sau đó dừng chụp. Nếu bạn không bắt được bất kỳ gói nào với bộ lọc này thì hãy sử dụng dấu vết chúng tôi cung cấp 
	*Trên hầu hết các Ethernets, có một cuộc trò chuyện thẳng thắn về lưu lượng truy cập nền khi các máy tính trao đổi thông điệp để duy trì trạng thái mạng, đó là lý do tại sao chúng tôi cố gắng nắm bắt lưu lượng truy cập mà không chạy bất kỳ chương trình nào khác. Bộ lọc chụp của **"ether multicast"** sẽ nắm bắt cả hai khung multicast và broadcast Ethernet, nhưng không phải là các khung unicast thường xuyên. Bạn có thể phải đợi một lúc để bắt các gói tin, nhưng trên hầu hết các mạng LAN có nhiều máy tính bạn sẽ thấy ít nhất một gói tin mỗi vài giây

		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/6.png"></p>

- 3. Kiểm tra các gói tin multicast và broadcast mà bạn đã capture, xem xét các chi tiết của địa chỉ nguồn và đích. Hầu hết người ta có địa chỉ Ethernet broadcast, vì các Broadcast frame có xu hướng phổ biến hơn các Multicast frame. nhìn broadcast frame để xem địa chỉ nào được sử dụng để broadcast bằng Ethernet. Mở rộng các trường địa chỉ Ethernet broadcast hoặc multicast frames để xem bit nào được đặt để phân biệt lưu broadcast/multicast hoặc nhóm từ lưu lượng truy cập Unicast. Màn hình của bạn có thể trông như thế này.

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/7.png"></p>

**NOTE**: Trước khi tiếp tục, bạn nên xóa các bộ lọc chụp của **"ether multicast"** bằng cách chọn Stop từ Capture và sau đó  trên Capture menu, chọn options và delete the terms trong hộp lọc.

- 4. Trả lời các câu hỏi sau đây. (Lưu ý, câu trả lời là cuối cùng, hãy thử làm việc đầu tiên ....)
	- A. Địa chỉ Ethernet phát sóng, được viết bằng dạng chuẩn như Wireshark hiển thị nó?
	- B. Bit của địa chỉ Ethernet được sử dụng để xác định xem nó là unicast hoặc multicast / phát sóng?

	 **Trả lời**:
	- 1. Địa chỉ broadcast là ff: ff: ff: ff: ff: ff. Đây là 48 bit "tất cả 1" được viết bằng dạng chuẩn.
	- 2. Chuỗi broadcast/multicast hoặc "group" được Wireshark hiển thị là **".... ...1 .... .... .... ...."** hoặc low-order Bit của byte địa chỉ đầu tiên. Chúng tôi cũng có thể viết như thế này 01: 00: 00: 00: 00: 00. Bit này thực sự là bit đầu tiên được truyền trên dây bởi vì Ethernet xác định thứ tự truyền là bit quan trọng nhất của mỗi byte đầu tiên.

<a name="2.7"></a>
##### 2.7. Step 6 - IEEE 802.3
Chúng tôi trở lại với tệp tìm kiếm mà bạn đã tải xuống từ trước -
Http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-ethernet.pcap
Bạn có thể mở lại tệp truy tìm này từ vị trí bạn đã tải xuống ví dụ: ví dụ: Local Disk (C):\downloads hoặc chọn *File menu* and *Open Recent*. Các tập tin tìm thấy được liệt kê ở đó.
Có một IEEE 802.3 frame trong các dấu vết cung cấp. Để tìm các gói tin IEEE 802.3, hãy nhập một bộ lọc hiển thị (phía trên bảng trên cùng của cửa sổ Wireshark) của "llc" (chữ thường là "LLC") vì định dạng IEEE 802.3 có giao thức LLC trên đó (và không làm được hãy nhấp vào Apply) để áp dụng bộ lọc. LLC cũng hiện diện trên wireless IEEE 802.11, nhưng nó không có trên DIX Ethernet. Bây giờ bạn sẽ thấy ba gói như trong hình bên dưới.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/image/Ethernet/9.png"></p>

**Hãy xem các chi tiết của khung IEEE 802.3, bao gồm tiêu đề LLC chẳng hạn như 20 trong dấu vết được cung cấp.**
- Hình này cho thấy các chi tiết cho dấu vết của chúng tôi. Quan sát trường Type hiện nay là trường Length. Trong ví dụ của chúng tôi, khung này đủ ngắn để còn có thêm số không được xác định là một đoạn Trailer hoặc Padding.
- Những thay đổi dẫn đến một vài câu hỏi để bạn suy ngẫm:
	- 1. Liên kết IEEE 802.3 và LLC kết hợp bao lâu so với tiêu đề DIX Ethernet? Bạn có thể sử dụng Wireshark để làm việc này . Lưu ý rằng đoạn Trailer/Padding và Checksum có thể được hiển thị như một phần của tiêu đề, nhưng chúng xuất hiện ở cuối khung.
	- 2. Làm thế nào để nhận được máy tính biết liệu frame là DIX Ethernet hoặc IEEE 802.3?
	- 3. Nếu IEEE 802.3 không có trường Type, thì làm thế nào xác định được lớp cao hơn lớp kế tiếp? Sử dụng Wireshark để tìm khoá demultiplexing.

- Trả lời:
	- 1. Tiêu đề IEEE 802.3 là 14 byte, giống như DIX Ethernet. (Cả hai cũng có một trailer,checksum và padding nếu cần thiết). LLC bổ sung thêm 3 byte các header cho tổng số 17 byte header.
	- 2. Trường Loại Ethernet DIX và trường Length IEEE 802.3 có cùng vị trí. Nếu giá trị nhỏ hơn 0x600 (1536) thì nó được hiểu là độ dài Frame. Nếu giá trị lớn hơn 0x600 (1536) thì nó được hiểu là một trường Type.
	- 3. IEEE 802.3 thêm theader LLC ngay sau  IEEE 802.3 header để truyền tải giao thức lớp tiếp theo. LLC sử dụng một byte ban đầu được gọi là DSAP (destination service access point)  thay vì 2 byte trong trường Type.
	
<a name="II"></a>
### II. Netstat

 Lệnh netstat có sẵn trong Command Prompt trong hầu hết các phiên bản của Windows bao gồm Windows 8, Windows 7, Windows Vista, Windows XP, Windows Server và một số phiên bản Windows cũ.
 Netstat cho phép bạn hiển thị số liệu thống kê về giao diện Ethernet. Nếu có bất kỳ lỗi nào được chỉ ra trong màn hình, có thể bạn gặp sự cố với kết nối mạng đang làm chậm mạng của bạn xuống. Nếu các gói tin lỗi tiếp cận 1% tổng số các gói dữ liệu, cái gì đó có thể là sai với NIC hoặc giao diện physical của bạn.
- 1. Trong **command promt** hoặc **DOS prompt**
- 2. Nhập `netstat` để liệt kê tất cả các kết nối mạng hiện tại, không chỉ trong nước mà còn gửi ra nước ngoài.
- 3. Bạn sẽ thấy một danh sách các kết nối được liệt kê. Có ích cho việc tìm kiếm các cuộc tấn công trực tiếp.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/1.png"></p>

- 4. Nhập `netstat -?` Để xem các tùy chọn với lệnh này. Bạn sẽ thấy `-a`, `-e` và những lệnh khác.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/2.png"></p>

- 5. Bây giờ gõ `netstat -a`
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/3.png"></p>

- 6. Nhập `netstat -e`. Các thống kê này bao gồm số byte và gói tin nhận được và được gửi qua giao diện Ethernet.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/4.png"></p>

- 7. Nhập netstat -f. Thống kê này hiển thị cho tất cả các kết nối hoạt động.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/5.png"></p>

- 8. Để xem số liệu thống kê cho tất cả các giao thức, gõ `netstat -s` và nhấn `Enter`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/6.png"></p>

- 9. Để giới hạn hiển thị chỉ các thống kê IP, gõ `netstat -ps` IP và nhấn `Enter`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/7.png"></p>

- 10. Để xem thống kê mạng đang hoạt động cập nhật 5 giây một lần, gõ `netstat -e -t 5` và nhấn `Enter`. Nhấn `Ctrl + C` để dừng chương trình.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/8.png"></p>

- 11. Gõ `netstat -o`. Điều này cho thấy các kết nối TCP hoạt động, nhưng nó cũng hiển thị mã nhận dạng quá trình tương ứng [-o] cho mỗi kết nối để bạn có thể xác định chương trình nào trên máy tính của bạn đã khởi tạo.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/9.png"></p>

- 12. Chú ý đến cột PID. Trong một số trường hợp, PID đều giống nhau, có nghĩa là cùng một chương trình trên máy tính của bạn đã mở các kết nối này. Tuy nhiên, để xác định chương trình nào được đại diện bởi PID của năm 2948 trên máy tính của bạn, tất cả những gì bạn phải làm là mở Task Manager, nhấp vào tab Processes và lưu ý tên hình ảnh được liệt kê bên cạnh PID bạn đang tìm kiếm trong Cột PID. Hãy tiếp tục và thử điều này .... Ngoài ra, hãy lưu ý rằng việc sử dụng lệnh netstat với tùy chọn -o có thể rất hữu ích khi theo dõi chương trình nào đang sử dụng phần lớn băng thông của bạn. Nó cũng có thể giúp xác định vị trí nơi mà một số loại phần mềm độc hại, hoặc thậm chí một phần mềm hợp pháp khác, có thể gửi thông tin mà không có sự cho phép của bạn.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/10.png"></p>

Lưu ý: Mặc dù ví dụ này và ví dụ trước đây đã được chạy trên cùng một máy tính và chỉ trong vòng một phút của nhau, bạn có thể thấy rằng danh sách các kết nối TCP hoạt động khác biệt đáng kể. Điều này là bởi vì máy tính của bạn liên tục kết nối và ngắt kết nối, các thiết bị khác trong mạng của bạn và qua Internet.

- 13. Để hiển thị thông tin **ICMP**, gõ `netstat -ps ICMP` và nhấn `Enter`. Một loạt các loại tin nhắn ICMP được hiển thị cùng với số lượng mỗi loại tin nhắn đã được nhận và gửi đi. Hầu hết, nếu không phải tất cả, sẽ là Echo và Echo Reply messages.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/11.png"></p>

- 14. Yêu cầu một sinh viên làm với địa chỉ IP của họ. Sau đó sử dụng ví dụ đó Nhập `ping 193.61.191.71` và nhấn `Enter`. Lệnh này sẽ tạo ra các tin nhắn `ICMP Destination Unreachable`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/12.png"></p>

- 15. Để xem liệu số lượng các thông báo Destination Unreachable đã tăng lên, gõ netstat -ps ICMP và nhấn Enter. Thông báo ICMP TTL-Expired được sử dụng trong Tracert được gọi là Thông báo Thời gian Đã Xóa trong Netstat.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/13.png"></p>

- 16. Gõ `tracert www.ulster.ac.uk` và nhấn `Enter`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/14.png"></p>

- 17. Để xem liệu số lượng thông báo Time Exceeded đã tăng lên, gõ `netstat -ps ICMP` và nhấn `Enter`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/15.png"></p>

- 18. Để hiển thị bảng định tuyến của máy tính, gõ `netstat -r` và nhấn `Enter`. Mỗi máy tính đều có một bảng định tuyến mà nó sử dụng để quyết định giao diện nào để gửi các gói tin đến. Mục nhập đầu tiên liệt kê đích mạng là 0.0.0.0, đây là mục nhập cho cổng mặc định của bạn.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/16.png"></p>

- 19. Cuối cùng, gõ `netstat -s -p tcp -f`. Ở đây chúng ta muốn xem số liệu thống kê cụ thể của giao thức **[-s]** nhưng không phải tất cả chúng, chỉ số thống kê TCP **[-p tcp]**. Chúng tôi cũng muốn các địa chỉ nước ngoài được hiển thị ở định dạng FQDN **[-f]**. kéo lên trn6 trong cửa sổ lệnh để xem các thống kê TCP được hiển thị trước khi tạo danh sách kết nối đang hoạt động.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netstat/17.png"></p>

<a name="III"></a>
### III. NetInfo
Sử dụng Netinfo để Thu thập Thông tin Máy tính và Mạng:
ping 1 đống gói là chính xác những gì có thể tả nó. Một chương trình gửi một số lượng lớn các gói tin ping đến một máy chủ. nó làm cho các máy chủ phải trả lời, có liên quan đến chu kỳ CPU và băng thông. Một biến thể là tấn công smurf, trong đó ping được gửi đến một địa chỉ broadcast. Tất cả yêu cầu chứa địa chỉ nguồn giả mạo của máy chủ được smurf. Khi các máy tính trả lời ping broadcast, họ gửi trả lời cho máy chủ có địa chỉ giả mạo. Máy chủ sẽ bị lũ lụt ping, làm chậm hoặc thậm chí đóng băng trong khi xử lý tất cả các gói dữ liệu.Distributed denial-of-service (DDoS) sử dụng nhiều hệ thống để tấn công một tài nguyên mạng đơn lẻ. Thường thì các hệ thống tấn công không biết họ đang tham gia vì phần mềm tấn công được cài đặt như là phần mềm độc hại và thiết lập để kích hoạt vào một ngày và thời gian nhất định.
Trong dự án này, bạn tải về và cài đặt một phiên bản đánh giá của Netlnfo. NetInfo là một bộ sưu tập của 15 công cụ mạng state-of-the-art khác nhau trên một giao diện duy nhất, dễ sử dụng. Tệp tải xuống là một tệp cài đặt Microsoft (.msi) cần phải được trích xuất để chạy nó.
- 1. mở trình duyệt Web và [dowload](http://scisweb.ulster.ac.uk/~kevin/com320/labs/netinfo.msi) netinfo.msi
- 2. Làm theo hướng dẫn để tải về và cài đặt Netlnfo.
- 3. Yêu cầu một trong những bạn cùng lớp của bạn cho địa chỉ IP của họ, ví dụ: 193.61.191.72
- 4. Gõ `ping "computername"` (thay thế computername bằng tên của máy tính bạn chọn ví dụ 193.61.191.72) và nhấn `Enter`.
- 5. Để bắt đầu `Netlnfo`, nhấp đúp vào phím tắt trên màn hình `Netlnfo` hoặc nhấp vào `Start`, trỏ đến `All Programs`, trỏ đến `Netlnfo`, và nhấn `Netlnfo`. Nhấp vào `No` trong hộp thông báo cho biết bạn có thể thử Netlnfo trong 30 ngày, sau đó nhấp vào `I agree`. Nếu hộp thoại Mẹo của Ngày xuất hiện, bấm để bỏ chọn hộp kiểm Show tips at startup, sau đó kích `Close`.
- 6. Nhấp vào tab Services. Trong hộp văn bản Máy chủ lưu trữ, nhập địa chỉ IP của máy tính bạn bè bạn bè và nhấp vào Xác minh. (Nếu bạn đang làm dự án này cho mình, bạn có thể gõ 127.0.0.1 trong hộp văn bản Host để quét máy tính của riêng bạn).
- 7. Màn hình của bạn trông như sau.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netinfo/1.png"></p>

- 8. Tìm các cổng hiển thị trạng thái Open. Các cổng mở đại diện cho các dịch vụ mạng mà máy tính cung cấp nhưng cũng có thể biểu thị các lỗ hổng mà kẻ tấn công có thể khai thác. Viết tên và số của các cổng này: 135 139 443 445
- 9. Xóa đầu ra từ lệnh cuối cùng bằng cách kích chuột phải vào `Netlnfo`, trỏ vào `Clear`, và nhấn `All`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netinfo/2.png"></p>

- 10. Tiếp theo, bạn sẽ quét một phạm vi nếu địa chỉ IP để xem máy tính nào có sẵn trên mạng. Bạn thực hiện việc này bằng cách nhấp vào tab máy quét.
- 11. Trong hộp văn bản Địa chỉ, nhập ba octet đầu tiên của địa chỉ IP mà bạn đã sử dụng trước đó theo sau là 0 cho octet cuối. Ví dụ: nếu địa chỉ bạn sử dụng là 193.61.191.71, gõ 193.61.191.0. Cài đặt này quét tất cả các địa chỉ từ 193.61.191.0 đến 193.61.191.255.
- 12. Màn hình của bạn trông như sau.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netinfo/3.png"></p>

- 13. Nhấp vào Start. Viết ra tên và địa chỉ của ba máy tính đầu tiên mà Netlnfo đã chỉ ra trạng thái "Host is alive." (Bạn có thể sắp xếp kết quả bằng cách nhấp vào Status column.)
- 14. Trong cột Name, nhấn chuột phải vào một trong các máy tính, trỏ đến Send To, và nhấn Services. Trong tab Services, hãy nhấp vào Verify để xem danh sách các dịch vụ mà máy tính này cung cấp.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netinfo/4.png"></p>

- 15. Màn hình của bạn trông giống như sau.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week02/Lab/Image/Netinfo/5.png"></p>

- 16. Bây giờ hãy thử trở lại danh sách các máy chủ trước đó đang hoạt động và thử 'sent to' với các dịch vụ khác.

<a name="IV"></a>
### IV. Tài liệu dịch

Lab Week 2: http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm
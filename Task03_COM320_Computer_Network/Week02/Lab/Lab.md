## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **15/03/2017**

### Mục lục
[I. Ethernet](#I)

- [1. Mục tiêu](#1)

- [2. Yêu cẩu](#2)

	- [2.1. Wireshark](#2.1)
	- [2.2. Step 1: Capture a Trace](#2.2)
	- [2.3. Step 3: Ethernet Frame Structure](#2.3)
	- [2.4. Step 4: Scope of Ethernet Addresses](#2.4)
	- [2.5. Step 5: Broadcast Frames](#2.5)
	- [2.6. Step 6 - IEEE 802.3 ](#2.6)
	- [2.7. Answers](#2.7)
	
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
	-5. Hãy nhìn vào phía trên bên trái của màn hình - bạn sẽ thấy một "Danh sách giao diện". Đây là danh sách các giao diện mạng trên máy tính của bạn. Một khi bạn chọn một giao diện, Wireshark sẽ nắm bắt tất cả các gói tin trên giao diện đó. Nhấp vào card mạng trên máy tính bạn đang làm việc trên. Trong ví dụ trên, nó là Trình điều khiển Ethernet để bắt đầu thu thập gói tin (ví dụ: đối với Wireshark để bắt đầu thu tất cả các gói được gửi đến / từ giao diện đó), một màn hình giống như dưới đây sẽ được hiển thị, hiển thị thông tin về các gói bị bắt . Một khi bạn bắt đầu chụp gói, bạn có thể dừng nó bằng cách sử dụng trình đơn kéo xuống Capture và chọn Stop \ Wireshark

	![Imgur](http://i.imgur.com/qq9s6Ix.png)

<a name="2.2"></a>
##### 2.2. Step 1: Capture a Trace
*Tiến hành như sau để nắm bắt một dấu vết của các gói tin ping. Nhấp chuột phải và chọn "Save Link As" và xuống các tập tin dấu vết sau đây 
http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-ethernet.pcap*

	- 1. Mở tệp sau đây từ vị trí bạn đã tải xuống ví dụ: Local Disk (C):\downloads.
	- 2. Bạn sẽ thấy một màn hình tương tự như sau:
	![Imgur](http://i.imgur.com/jvbkOfj.png)
	- 3. lọc **"icmp"** và nhấp vào apply.
	*Cửa sổ chụp của bạn phải giống với hình chụp bên dưới, trừ điểm nhấn của chúng tôi*
	![Imgur](http://i.imgur.com/VuV9lmK.png)

<a name="2.3"></a>
##### 2.3. Step 3: Ethernet Frame Structure
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
##### 2.4. Step 4: Scope of Ethernet Addresses

<a name="2.5"></a>
##### 2.5. Step 5: Broadcast Frames

<a name="2.6"></a>
##### 2.6. Step 6 - IEEE 802.3

<a name="2.7"></a>
##### 2.7. Answers

<a name="II"></a>
### II. Netstat

<a name="III"></a>
### III. NetInfo

<a name="IV"></a>
### IV. Tài liệu dịch

Lab Week 2: http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm

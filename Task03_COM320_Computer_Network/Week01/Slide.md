﻿## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **01/03/2017**

### Mục lục

[1. Sử dụng mạng máy tính](#uses)

- [1.1. Thương mại ứng dụng](#thuongmai)

- [1.2. Trang chủ ứng dụng](#home)

- [1.3. Người dùng di động](#mobile)

- [1.4. Các vần đề mạng xã hội](#social)

- [1.5. Mạng trug lập](#neutrality)

[2. Mạng phần cứng](#hardware)

- [2.1. Mạng PAN](#pan)

- [2.1. Mạng LAN](#lan)

- [2.3. Mạng MAN](#man)

- [2.4. Mạng WAN](#wan)

[3. Mạng phần mềm ](#software)

- [3.1. Các lớp mạng](#layer)
- [3.2. Thiết kế các lớp mạng](#thietkemang)
- [3.3. Hướng kết nối vs kết nối](#ketnoi)
- [3.4. Nguyên dịch vụ](#dv)
- [3.5. Quan hệ giữa dịch vụ với giao thức](#quanhe)

[4. Mô hình mạng](#models)

- [4.1. Mô hình tham chiếu OSI](#OSI)
- [4.2. Mô hình tham chiếu TCP / IP](#TCP/IP)
- [4.3. Mô hình sử dụng trong sách này](#book)
- [4.4. Nhận xét OSI và TCP/IP](#nhanxet)

[5. Ví dụ về mạng](#example)

- [5.1. The Internet](#internet)
- [5.2. 3G mobile phone networks](#3g)
- [5.3. Wireless LANs](#wifi)
- [5.4. RFID and sensor networks](#RFID)
- [5.5. Peer to peer](#peer)

[6. Mạng tiêu chuẩn](#standardization)

[7. sercurity](#sercurity)

[8. An ninh Mạng](#anninh)

[9. Đơn vị Metric](#metric)

[10. Tài liệu dịch](#tailieu)

<a name="uses"></a>
### 1. Sử dụng mạng máy tính
<a name="thuongmai"></a>
#### 1.1. Thương mại ứng dụng:
- Các công ty sử dụng mạng và máy tính để *chia sẻ tài nguyên* với các *client-server*.
- ngoài ra còn sử dụng trong thông tin liên lạc như: mail, voiIP, thương mại điện tử.

<a name="home"></a>
#### 1.2 Trang chủ ứng dụng:
- Nhà chứa nhiều các thiết bị mạng. Ví dụ: máy tính, TV, kết nối với Internet bằng cáp, DSL, không dây,...
- Trang chủ người giao tiếp. Ví dụ như các trang mạng xã hội: zalo, facebook, viber,...; các giao dịch như mua bán, đấu giá,...
- Một số ứng dụng sử dụng các mô hình peer-to-peer, trong đó không có khách hàng cố định và máy chủ.
<a name="mobile"></a>
#### 1.3. Người dùng di động:
- Máy tính bảng, laptop và điện thoại là những thiết bị phổ biến; WiFi và 3G di động cung cấp kết nối không dây. 
- Người dùng sử di động trong giao tiếp, xem video,giải trí, truy cập Web và sử dụng cảm biến-GPS,...
- Mạng không dây (wireless) và điện thoại có sự liên quan nhưng khác nhau:

| Wireless | mobile  | ứng dụng tiêu biểu |
| :------: |:-------:| :-----:|
| no       | no		 | Máy tính để bàn sử dụng cho văn phòng |
| no       | yes     | Máy tính xách tay sử dụng trong phòng khách sạn |
| yes	   | no      | Mạng không dây ở các tòa nhà |
| yes	   | yes     |   Cửa hàng Máy tính cầm tay tồn kho|

<a name="social"></a>
#### 1.4. Các vần đề mạng xã hội:
- Trung lập mạng - mạng không hạn chế
- Quyền sở hữu nội dung, chỉ gỡ xuống theo DMCA  
- Sự nặc danh và kiểm duyệt
- Bảo mật. ví dụ: theo dõi Web và profiling
- Trộm cắp. ví dụ: botnet và phishing

<a name="neutrality"></a>
#### 1.5. Mạng trug lập:
- Một số nhà khai thác mạng chặn nội dung vì lý do riêng của họ.
- Đối thủ của việc này cho rằng peer-to-peer và những nội dung khác cần được giải quyết trong cùng một cách bởi vì họ chỉ bit tất cả chỉ vào mạng.
- Lập luận này cho rằng truyền thông không được phân biệt theo nội dung hoặc mã nguồn của họ hoặc những người đang cung cấp các nội dung đó được gọi là mạng trung lập
 
<a name="hardware"></a>
### 2. Mạng phần cứng:
- Mạng có thể được phân loại theo quy mô sau:
 
| quy mô  | kiểu mạng  | 
| :------: |:-------:| 
| lân cận      | PAN	 | 
| tòa nhà      | LAN     | 
| thành phố	   | MAN      | 
| nước   | WAN     | 
| thế giới   | The Internet     | 



<a name="pan"></a>
#### 2.1. Mạng PAN (Personnal Area Network):
- Kết nối các thiết bị trong phạm vi của một người,cá nhân.
- Ví dụ PAN không dây phổ biến: Bluetooth,...

![](http://i.imgur.com/GnChhDU.png)
    

<a name="pan"></a>
#### 2.2. Mạng LAN (Local Area Network):

- Kết nối các thiết bị trong nhà hay văn phòng.
- Gọi là mạng doanh nghiệp trong một công ty
- Hầu hết sử dụng dây đồng nhưng có 1 số trường hợp sử dụng cáp quang.

![](http://i.imgur.com/vcxY4NS.png)

<a name="man"></a>
#### 2.3. Mạng MAN (Metropolitan Area Network):

- Kết nối các thiết bị trong khu vực đô thị. Ví dụ MAN dựa trên truyền hình cáp.

![](http://i.imgur.com/3ASp8D4.png)

<a name="wan"></a>
#### 2.4. Mạng WAN (Wide Area Network):

- Kết nối các thiết bị trong trong nước,...Ví dụ WAN kết nối ba văn phòng chi nhánh.

![](http://i.imgur.com/ZMHjopz.png)

- Một ISP (Internet Service Provider) mạng cũng là một WAN. Khách hàng mua kết nối từ ISP để sử dụng.

![](http://i.imgur.com/gO4yyXi.png)

- VPN (Virtual Private Network) là một mạng WAN được xây dựng từ các liên kết ảo chạy trên Internet.

![](http://i.imgur.com/WKqY315.png)

<a name="software"></a>
### 3.Mạng phần mềm:
- Các lớp mạng
- Thiết kế các lớp mạng
- Hướng kết nối vs phi kết nối 
- Nguyên dịch vụ
- Quan hệ giữa dịch vụ với giao thức.

<a name="layer"></a>
#### 3.1. Các lớp mạng:

 Các lớp gia thức là phương pháp cấu trúc chính được sử dụng để phân chia chức năng mạng.
- Mỗi giao thức có thể nói là ngang với nhau.
- Mỗi lớp chỉ giao tiếp bằng cách sử dụng một trong những lớp dưới đây.
- Dịch vụ của tầng thấp hơn được truy cập bởi một giao diện.
- Ở phía dưới, tin nhắn được thực hiện bởi các phương tiện.

![](http://i.imgur.com/dKTaGYB.png)

Ví dụ: Các kiến trúc nhà triết học - thông dịch viên - thư ký
Mỗi giao thức ở lớp khác nhau phục vụ một mục đích khác nhau.

![](http://i.imgur.com/lbeEB95.png)

Mỗi lớp thấp thêm tiêu đề riêng của mình (với điều khiển inform-ation) vào tin nhắn để truyền và loại bỏ nó khi nhận được.

![](http://i.imgur.com/r5RyenB.png)

Lớp này cũng có thể chia tách và tham gia tin nhắn, vv

<a name="thietkemang"></a>
#### 3.3. Thiết kế các lớp mạng

Mỗi lớp giải quyết một vấn đề cụ thể nhưng phải có cơ chế để giải quyết một loạt các vấn đề thiết kế định kỳ :

| Vấn đề  | ví dụ cơ chế ở các lớp khác nhau  | 
| :------: |:-------:| 
| Độ tin cậy thất bai      | Code cho các lỗi hát hiện/sửa chữa ($3.2 3.3). Định tuyến xung quanh thất bại ($5.2)	 | 
| Mạng tăng trưởng và tiến hóa     | Phát biểu ($ 5.6) và đặt tên ($ 7.1) Nghị định phân lớp (S1.3)    | 
| phân bố các nguồn tài nguyên như băng thông	   |  Nhiều truy cập ($ 4.2) Kiểm soát tắc nghẽn (S5.3, 6.3)      | 
| An ninh chống lại các mối đe dọa khác   | Bảo mật các tin nhắn (S8.2, 8.6) xác thực của các bên giao tiếp ($ 8.7)   | 

 <a name="ketnoi"></a>
#### 3.3. Hướng kết nối vs phi kết nối

Dịch vụ cung cấp bởi một lớp có thể loại là:
- Hướng kết nối: phải được thiết lập để sử dụng liên tục (và phá bỏ sau khi sử dụng), ví dụ, gọi điện thoại.
- Phi kết nối: tin nhắn sẽ được xử lý riêng biệt, ví dụ, giao hàng bưu chính.

![](http://i.imgur.com/CG7LLnb.png)

** Máy điện báo kép**

Nhiều mạng thiết kế băng thông mạng chia sẻ tự động, tùy theo nhu cầu ngắn hạn của chủ nhà, chứ không phải bằng cách cho mỗi máy chủ một phần cố định của băng rộng mà nó có thể hoặc không thể sử dụng.
Thiết kế này được gọi là ghép kênh thống kê.

![](http://i.imgur.com/SVJncz2.png)

Giải thích:
Dữ liệu đến không đồng bộ từ nguồn. Cho các vào bộ đệm đầu vào . Tiêu đề chứa địa chỉ và các thông tin khác được thêm vào các gói dữ liệu . Sau đó cho ra ở bộ đệm đầu ra.Các gói từ các nguồn khác nhau sẽ được đặt kênh và cho ra cấu trúc của 1 goi dữ liệu điển hình.

**Switching**

- **Store & Forward Switching**: Được sử dụng trên một mạng gói, nhận gói tin và chuyển đi.
- **Cut-through switching** là một phương pháp cho các hệ thống chuyển mạch gói, trong đó chuyển đổi bắt đầu chuyển tiếp một khung hình (hoặc gói) trước khi toàn bộ khung đã được nhận, bình thường ngay khi địa chỉ đích được xử lý.
*So với lưu trữ và chuyển tiếp, kỹ thuật này làm giảm độ trễ thông qua chuyển đổi, nhưng làm giảm độ tin cậy; khung hình bị hư hỏng đang có khả năng chuyển tiếp.*
- **Adaptive Switching** tự động lựa chọn giữa cut-through and store and forward dựa trên các điều kiện mạng hiện tại.

**Làm thế nào để mất và sự chậm trễ xảy ra?**

Gói hàng đợi trong bộ đệm bộ định tuyến:
- Tỷ lệ gói tin đến để liên kết vượt quá khả năng liên kết đầu ra.
- Gói hàng đợi, chờ đợi đến lượt.

![](http://i.imgur.com/HYuNEFk.png)

Bộ đệm có sẳn: các gói tin đến giảm  nếu không có bộ đệm này( while)

**Bốn điều của sự chậm trễ gói**

![](http://i.imgur.com/1agYOri.png)

**d**nodal = **d**proc + **d**queue + **d**trans +  **d**prop

**d**proc: xử lý mối

- Lỗi kiểm tra bit
- Xác định liên kết đầu ra
- typically < msec >

**d**queue: xếp hàng chậm trễ
- Thời gian chờ đợi ở liên kết đầu ra để truyền
- Phụ thuộc vào mức độ tắc nghẽn của router

**d**trans: trễ truyền dẫn:
- L: chiều dài gói tin (bit)
- R: băng thông liên kết (bps)
- **d**trans = L / R

**d** prop: tuyên truyền chậm trễ:
- D: chiều dài của liên kết vật lý
- S: tốc độ lan truyền trong môi trường (~ 2x108 m / giây)
- **d**prop = d / s

***d**proc và **d**trans rất khác nhau.*

<a name="dv"></a>
#### 3.4. nguyên dịch vụ:

- Một dịch vụ được cung cấp cho các lớp trên như nguyên thủy

- ví dụ: giả thuyết của các nguyên dịch vụ có thể cung cấp một dòng byte đáng tin cậy dịch vụ (hướng kết nối):


|Nguyên thủy  | Ý nghĩa  | 
| :------: |:-------:| 
| Nghe      | Chờ kết nối đến	 | 
| Kết nối      | Thiết lập 1 mạng ngang hàng chờ đợi    | 
|Chấp nhận	   | Chấp nhận 1 kết nối đến từ mạng ngang hàng với nó      | 
| Gửi   | Gữi tin nhắn đến mang ngang hàng     | 
| Đứt kết nối   | Chấm dứt 1 kết nối     |


- ví dụ: giả thuyết về cách thức các nguyên thủy có thể được sử dụng cho một tương tác client-server:

![](http://i.imgur.com/If7vw8N.png)

Cơ chế:
Đầu tiên server sẽ lắng nghe. khi client muốn thiết lập 1 kết nối nó sẽ gữi 1 gói tin connect request sang cho con server. server nhận được sẽ đáp trả bằng gói accept response
.client nhận được gói phản hồi sẽ gửi tiếp gói tin Request for data chứa dữ liệu yêu cầu. server sẽ gửi lại dữ liệu client đang cần. sâu đó ngắt kết nối vs server. sau đó server cũng ngắt kết với client.

<a name="quanhe"></a>
#### 3.5. Quan hệ giữa dịch vụ với giao thức:

Tóm tắt:

- Một lớp cung cấp một dịch vụ cho một trong các lớp trên và dưới nó [đứng].

- Một lớp nói chuyện với đồng đẳng của nó sử dụng một giao thức [ngang].

![](http://i.imgur.com/BDsGgYK.png)

Các dịch vụ và giao thức là những khái niệm khác nhau. Một dịch vụ là một tập hợp các nguyên thủy (hoạt động) mà một lớp cung cấp cho các lớp phía trên nó.

Dịch vụ xác định những hoạt động của lớp được chuẩn bị để thực hiện thay mặt cho người sử dụng, nhưng nó nói gì cả về cách những hoạt động được thực hiện.

<a name="models"></a>
### 4. Mô hình mạng:

Mô hình tham khảo mô tả các lớp trong một kiến trúc mạng:
- Mô hình tham chiếu OSI
- Mô hình tham chiếu TCP / IP
- Mô hình sử dụng trong sách này 
- Nhận xét OSI và TCP/IP

<a name="OSI"></a>
#### 4.1. Mô hình tham chiếu OSI:
Tiêu chuẩn quốc tế có nguyên tắc mô hình tham chiếu OSI gồm có 7 tầng để kết nối các hệ thống khác nhau.

|   | Chức năng  | 
| :------: |:-------:| 
| Application      | Cung cấp các chức năng cần thiết cho người sử dụng	 | 
| Presentation      |   Chuyển đổi đại diện khác nhau   | 
| Session   | Quản lý hộp thoại nhiệm vụ    | 
| Transport | Cung cấp giao end-to-end    | 
| Network  |   Gửi các gói tin trên nhiều liên kết   | 
| Data link  | Gửi khung thông tin    | 
| Physical  |  Gửi bit như tín hiệu    | 


<a name="TCP/IP"></a>
#### 4.2. Mô hình tham chiếu TCP/IP:

Một mô hình bốn tầng có nguồn gốc từ thực nghiệm; bỏ qua một số tầng OSI và sử dụng IP là lớp mạng.

![](http://i.imgur.com/YhH92kg.png)

<a name="book"></a>
#### 4.3. Mô hình tham sử dụng trong sách này:

Nó được dựa trên mô hình TCP/IP nhưng chúng tôi gọi ra lớp vật lý và nhìn xa hơn các giao thức Internet.

![](http://i.imgur.com/xIiOZCz.png)

<a name="nhanxet"></a>
#### 4.4. Nhận xét OSI và TCP/IP:

**OSI:**
- Ưu: Mô hình rất có ảnh hưởng với các khái niệm rõ ràng.
- Nhược: Các mô hình, giao thức và áp dụng tất cả các sa lầy bởi chính trị và phức tạp

**TCP/IP:**
- Ưu: Giao thức rất thành công mà làm việc tốt và phát triển mạnh.
- Nhược: Mô hình yếu xuất phát sau thực tế từ các giao thức.

<a name="example"></a>
### 5. Ví dụ về Mạng:
- The Internet 
- 3G mobile phone networks 
- Wireless LANs 
- RFID and sensor networks 

<a name="internet"></a>
#### 5.1. The Internet:
- Trước Internet là ARPANET, một mạng chuyển mạch gói được phân cấp dựa trên ý tưởng của Baran.

![](http://i.imgur.com/VzEzmM9.png)

ARPANET topo trong tháng 9 1972.
Nút là IMP, hoặc router đầu, liên kết với các host,56 kbps liên kết.


- Internet trước đây sử dụng NSFNET (1985-1995) là xương sống của nó; các trường đại học được kết nối để có được trên Internet.
*NSFNET là một mạng lưới nghiên cứu học thuật phát triển ra khỏi CSNET đã được tạo ra để các trường đại học không có hợp đồng DoD có thể tham gia. Ban đầu nó được kết nối với mạng ARPANET bởi gateway, và sau đó, tiếp vai trò trung tâm là "xương sống của Internet", tức là mạng thông qua các gói dữ liệu truyền trên đường giữa các bên kết nối đến các bộ phận khác nhau của Internet.*

![](http://i.imgur.com/ihrZcx6.png)

- Internet hiện đại là phức tạp hơn:

  	- Mạng ISP phục vụ như là xương sống Internet.
	- ISP kết nối hoặc ngang nhau để trao đổi giao thông tại các IXP.
	- Trong mỗi mạng thì router chuyển gói tin.
	- Giữa các mạng, trao đổi lưu lượng được thiết lập bởi các hiệp định thương mại.
	- Khách hàng kết nối ở mép bằng nhiều phương tiện: Cable, DSL, Fiber-to-the-Home, 3G / 4G không dây, dialup.
	- Trung tâm dữ liệu tập trung nhiều máy chủ ( "đám mây").
	- Hầu hết các lưu thông là nội dung từ các trung tâm dữ liệu (đặc biệt là video).
	- Các cấu trúc tiếp tục phát triển.

- Kiến trúc của Internet:

![](http://i.imgur.com/9A1BBxD.png)

- Mạng lưới cung cấp dịch vụ Internet (ISP) có thể là khu vực, quốc gia hay quốc tế trong phạm vi.

- Nếu một gói là đích cho một máy chủ phục vụ trực tiếp bởi các ISP, gói tin được định tuyến qua xương sống và giao cho chủ nhà.

- Nếu không, nó phải được bàn giao cho ISP khác. ISP kết nối mạng của họ để lưu thông trao đổi tại các IXP (Internet eXchange Points).

	![](http://i.imgur.com/Pj4g7jH.png)
    
    
<a name="3g"></a>
#### 5.2. 3G mobile phone networks:

- Mạng 3G dựa trên các tế bào sóng trong không gian; mỗi tế bào cung cấp dịch vụ không dây cho điện thoại di động bên trong nó thông qua một trạm gốc.

![](http://i.imgur.com/hB9xp1B.png)

- Trạm cơ sở kết nối với mạng lõi để tìm điện thoại di động khác và gửi dữ liệu đến các mạng điện thoại và Internet.

![](http://i.imgur.com/LJPTlAh.png)

- Khi điện thoại di động di chuyển, trạm cơ sở sẽ giao cho một tế bào tiếp theo, và mạng lưới theo dõi vị trí của họ.

![](http://i.imgur.com/TW21Ixy.png)
    
<a name="wifi"></a>
#### 5.3. Wireless LAN

- Trong 802.11, khách hàng giao tiếp thông qua một AP (Access Point) có dây nối với phần còn lại của mạng.

![](http://i.imgur.com/kAwiwkH.png)

- Tín hiệu trong băng tần 2.4GHz ISM khác nhau về sức mạnh do nhiều tác dụng, chẳng hạn như do phản xạ - 
đòi hỏi các chương trình truyền phức tạp. ví dụ như OFDM.

![](http://i.imgur.com/n2QHNq9.png)

- Chương trình phát thanh can thiệp với nhau, và phạm vi radio có thể không đủ, chồng chéo lên nhau - CSMA (Carrier Sense Multiple Access) thiết kế được sử dụng.

![](http://i.imgur.com/9wEeOoz.png)

<a name="RFID"></a>
#### 5.4. RFID and sensor network:
- Đối tượng mạng thụ động UHF RFID hàng ngày:

	- Tags(dán không phải là một pin) được đặt trên các đối tượng.
	- Độc giả gửi tín hiệu rằng các thẻ phản ánh để giao tiếp.

![](http://i.imgur.com/mb5uFLv.png)

- Mạng cảm biến truyền cho các thiết bị nhỏ hơn diện tích:
Thiết bị gửi dữ liệu cảm nhận để thu thông qua bước nhảy dây.

![](http://i.imgur.com/VD2boeF.png)

<a name="peer"></a>
#### 5.5. Peer to peer:
- Một peer-to-peer (viết tắt là P2P) là một mạng máy tính trong đó mỗi máy tính trong mạng có thể hoạt động như một máy khách hoặc máy chủ cho các máy tính khác trong mạng, cho phép truy cập chia sẻ các nguồn tài nguyên khác nhau như các tập tin, thiết bị ngoại vi, và cảm biến mà không cần một máy chủ trung tâm.
- Mạng P2P được sử dụng để chia sẻ âm thanh, video, dữ liệu, hoặc bất cứ điều gì ở định dạng kỹ thuật số.
- Nhiều P2P hệ thống, chẳng hạn như BitTorrent, không có bất kỳ cơ sở dữ liệu trung tâm của nội dung. Thay vào đó, mỗi người dùng tự duy trì cơ sở dữ liệu riêng của mình tại địa phương và cung cấp một danh sách những người lân cận khác là thành viên của hệ thống.
- Nhung nguoi ngang hàng là những người tham gia đều có đặc quyền trong ứng dụng. Mỗi máy tính trong mạng được gọi là một nút.
- Chủ sở hữu của mỗi máy tính trên một mạng P2P sẽ dành riêng một phần của tài nguyên, chẳng hạn của nó như là sức mạnh xử lý, lưu trữ đĩa, hoặc mạng băng thông được thực hiện trực tiếp có sẵn để tham gia mạng lưới khác, không có nhu cầu phối hợp trung tâm bởi các máy chủ hoặc ổn định host.
- Với mô hình này, người tham gia là nhà cung cấp và người tiêu dùng là các nguồn lực. Ngược lại với mô hình client-server chỉ cung cấp máy chủ (gửi), và khách hàng tiêu thụ (nhận được).

<a name="standardization"></a>
### 6. Mạng tiêu chuẩn: 
- Tiêu chuẩn xác định những gì là cần thiết cho khả năng tương tác.Một số trong rất nhiều hệ thống tiêu chuẩn:

| Kiêu | khu vực  | kiểu mạng  | 
| :------:| :------: |:-------:| 
| ITU | Viễn thông      | G.992, ADSL; H264, MPEG4	 | 
| IEEE | truyền thông      | 802.3 Internet; 8.2.11 wifi    | 
| IETF | internet	   | RFC 2616, HTTP/1.1; RFC 1034/1035, DNS      | 
| W3C | web   | WAN     | HTML 5 standard ; CSS standard |

<a name="security"></a>
### 7. Security:

- Chúng ta bắt đầu từ đâu?

ví dụ. phising:
Giả mạo tin nhắn xuất xứ từ một bên đáng tin cậy. ví dụ như ngân hàng của bạn, để cố gắng lừa bạn tiết lộ thông tin nhạy cảm như số thẻ tín dụng,...

Công cụ sử dụng : Hacking, DDoS, Passwords, băm, PGP, Mật mã, chữ kí, tất cả bảo hiểm của bạn sau này.

<a name="anninh"></a>
### 8. An ninh Mạng:

- lĩnh vực an ninh mạng:
	- Rất nhiều kẻ xấu có thể tấn công mạng máy tính.
	- Làm thế nào chúng ta có thể bảo vệ mạng, chống lại các cuộc tấn công
	- làm thế nào thiết kế cấu trúc để được miễn dịch tấn công


- Trong suy nghĩ thì Internet không được thiết kế kết hợp với an ninh:

	- Tầm nhìn ban đầu: "một nhóm người dùng tin tưởng lẫn nhau gắn liền với một mạng lưới trong suốt".
	- Thiết kế giao thức Internet chơi "bắt kịp".
	- Cân nhắc an ninh trong tất cả các lớp.

**Kẻ xấu: đặt phần mềm độc hại vào máy chủ thông qua Internet:**
- phần mềm độc hại có thể có được trong máy chủ từ một loại virus, worm hoặc Trojan horse
- Phần mềm gián điệp, phần mềm độc hại có thể ghi lại thao tác bàn phím, trang web truy cập, tải lên thông tin của bộ sưu tập cho trang web.
- máy chủ bị nhiễm có thể được ghi danh vào mạng botnet, sử dụng cho các thư rác và tấn công DDoS.
- Phần mềm độc hại thường tự sao chép: từ một máy chủ bị nhiễm bệnh, tìm cách nhập vào máy chủ khác.

**Trojan horse**
- ẩn của một số phần mềm khác hữu ích.
- ngày nay thường chứa trong trang Web (Active-X, plugin)

**Virus:**
- Lây nhiễm bằng cách tiếp nhận đối tượng (ví dụ, tập tin đính kèm e-mail), tích cực thực hiện
- tự sao chép: tuyên truyền chính nó tới máy chủ khác, người sử dụng.

**Worm:**
- Lây nhiễm bằng cách thụ động tiếp nhận đối tượng mà được tự thực hiện.
- tự sao chép: tuyên truyền đến máy chủ khác, người sử dụng.

![](http://i.imgur.com/vbf4WkW.png)

**kẻ xấu: máy chủ bị tấn công, cơ sở hạ tầng mạng:
- Tấn công từ chối dịch vụ (DoS): kẻ tấn công làm cho tài nguyên (máy chủ, băng thông) không có sẵn để Truyen hợp pháp của nguồn áp đảo với Truyển không có thật.
	- 1. chọn mục tiêu
	- 2. đột nhập vào host trên mạng (xem botnet)
	- 3. gửi các gói tin để nhắm mục tiêu xâm nhập

![](http://i.imgur.com/xQV4oCP.png)

**Những kẻ xấu có thể tắt nghẽn gói tin**:
- sniffing gói:
	- phát sóng truyền thông (chia sẻ Ethernet, không dây)
	- giao diện mạng xáo trộn lần đọc / ghi lại tất cả các gói dữ liệu (ví dụ, bao gồm cả mật khẩu!) đi qua.
	
![](http://i.imgur.com/Wk4rFSW.png)

> phần mềm Wireshark sử dụng cho end-of-chapter các phòng thí nghiệm là một gói sniffer.

**Những kẻ xấu có thể giả mạo địa chỉ nguồn**

IP spoofing: gửi gói tin với địa chỉ nguồn giả:

![](http://i.imgur.com/LVmrx7H.png)

**Những kẻ xấu có thể ghi âm và phát lại**

- Ghi âm và phát lại: sniff thông tin nhạy cảm (ví dụ, mật khẩu), và sử dụng sau này.
	- người giữ mật khẩu là người dùng từ hệ thống tầm nhìn nhiều hơn nữa về an ninh sau của khoá học...

![](http://i.imgur.com/GDVrTYp.png)

<a name="metric"></a>
### 9. Đơn vị Metric:

 ![](http://i.imgur.com/QSmj72K.png)

Sử dụng quyền hạn của 10 cho giá trị, quyền hạn của 2 cho lưu trữ
Ví dụ: 1 Mbps = 1.000.000 bps, 1 KB = 1024 byte
"B" là dành cho byte, "b" là cho bit

**Sơ đồ hệ thống cáp internet biển trên thế giới**:

![Imgur](http://i.imgur.com/4A21qvN.png)

<a name="tailieu"></a>
### 10. Tài liệu dịch:

Lecrure 1: http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm 

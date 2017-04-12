## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **17/04/2017**

### Mục lục
[I. Medium Access Control Sublayer](#I)

- [1. Channel Allocation Problem](#1)


- [2. Multiple Access Protocols](#2)

	- [2.1. ALOHA](#2.1)
	- [2.2. CSMA (Carrier Sense Multiple Access)](#2.2)
	- [2.3. Collision-free protocols](#2.3)
	- [2.4. Limited-contention protocols](#2.4)
	- [2.5. Wireless LAN protocols](#2.5)

- [3. Ethernet](#3)

	- [3.1. Classic Ethernet](#3.1)
	- [3.2. Switched/Fast Ethernet](#3.2)
	- [3.3. Gigabit/10 Gigabit Ethernet](#3.3)

- [4. Wireless LANs](#4)

	- [4.1. 802.11 architecture/protocol stack](#4.1)
	- [4.2. 802.11 physical layer](#4.2)
	- [4.3. 802.11 MAC](#4.3)
	- [4.4. 802.11 frames](#4.4)

- [5. Broadband Wireless](#5)

	- [5.1. 802.16 Architecture / Protocol Stack](#5.1)
	- [5.2. 802.16 Physical Layer](#5.2)
	- [5.3. 802.16 MAC](#5.3)
	- [5.4. 802.16 Frames](#5.4)

- [6. Bluetooth](#6)

	- [6.1. Bluetooth Architecture](#6.1)
	- [6.2. Bluetooth Applications / Protocol](#6.2)
	- [6.3. Bluetooth Radio / Link Layers](#6.3)
	- [6.4. Bluetooth Frames](#6.4)

- [7. RFID](#7)
	- [7.1. Gen 2 Architecture](#7.1)
	- [7.2. Gen 2 Physical Layer](#7.2)
	- [7.3. Gen 2 Tag Identification Layer](#7.3)
	- [7.4. Gen 2 Frames](#7.4)

- [8. Data Link Layer Switching](#8)

	- [8.1. Uses of Bridges](#8.1)
	- [8.2. Learning Bridges](#8.2)
	- [8.3. Spanning Tree](#8.3)
	- [8.4. Repeaters, hubs, bridges, .., routers, gateways](#8.4)
	- [8.5. Virtual LANs](#8.5)

-------------------------------------------------------------------

<a name="I"></a>
### I. Medium Access Control Sublayer:

<a name="1"></a>
#### 1. Channel Allocation Problem:

Đối với kênh cố định và lưu lượng truy cập từ người dùng N.
- Chia băng thông bằng FTM, TDM, CDMA, v.v.
- Đây là phân bổ tĩnh, ví dụ: radio FM.
Phân bổ tĩnh này thực hiện kém đối với lưu lượng truy cập rất lớn.
- Phân bổ cho người dùng đôi khi sẽ không sử dụng
Phân bổ động cho phép kênh đến người dùng khi họ cần. Khả năng N lần hiệu quả đối với người dùng N.
Các phương án khác nhau với các giả định:

| Giả định   | Hàm ý | 
| :-------: | :----: |
| Giao thông độc lập | Thường không phải là một mô hình tốt, nhưng cho phép phân tích |
| Kênh đơn   | Không có cách nào khác để liên kết các người gửi   |
| Va chạm quan sát được    | Cần thiết cho độ tin cậy; Cơ chế khác nhau |
| Thời gian liên tục hoặc rãnh | Nơi có thể cải thiện vị trí |
| Ý nghĩa của nhà cung cấp | Có thể cải thiện hiệu suất nếu có |


<a name="2"></a>
#### 2. Multiple Access Protocols:

<a name="2.1"></a>
##### 2.1. ALOHA:

Trong ALOHA thuần túy, người dùng truyền khung bất cứ khi nào họ có dữ liệu; Người dùng thử lại sau một thời gian ngẫu nhiên sau xung đột
- Hiệu quả và độ chậm trễ thấp với tải trọng thấp.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/1.png"></p>

Sự va chạm xảy ra khi người dùng khác truyền tải cùng lúc 2 frame trong cùng 1 khoảng thời gian 
- Đồng bộ hóa người gửi đến các khe có thể làm giảm va chạm
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/2.png"></p>

Slotted ALOHA hiệu quả gấp đôi so với ALOHA thuần khiết
- Các khe rác hở thấp, tải trọng cao gây ra va chạm
- Hiệu quả đến 1 / e (37%) đối với các mô hình lưu lượng truy cập ngẫu nhiên.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/3.png"></p>


<a name="2.2"></a>
##### 2.2. CSMA (Carrier Sense Multiple Access):

CSMA cải thiện ALOHA bằng cách cảm nhận kênh!
- Người dùng không gửi nếu cảm thấy người khác đang gửi

Các biến thể về việc phải làm gì nếu kênh bận:
- 1 liên tục (tham lam) gửi ngay khi nhàn rỗi
- Không chờ đợi chờ một thời gian ngẫu nhiên, thử lại sau đó
- p-gửi liên tục với xác suất p khi nhàn rỗi.

CSMA hoạt động tốt hơn ALOHA, và ít bền bỉ hơn khi chịu tải trọng cao:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/4.png"></p>

Cải thiện của CSMA / CD là phát hiện / hủy bỏ sự xung đột
- Giảm thời gian tranh chấp giúp cải thiện hiệu suất.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/5.png"></p>

- Nếu hai máy trạm nhận thấy kênh không hoạt động và bắt đầu gửi đồng thời, tín hiệu của chúng sẽ vẫn bị xung đột
- Cải tiến là để các máy trạm nhanh chóng phát hiện ra xung đột và đột ngột ngừng truyền vì chúng không thể đảo ngược được.
- Chiến lược này tiết kiệm thời gian và băng thông. Giao thức này được gọi là CSMA/CD (CSMA with Collision Detection).
- Trong một hub, tất cả các trạm đều nằm trong cùng một miền Collision. Họ phải sử dụng thuật toán CSMA/CD để lập lịch trình truyền của họ.

<a name="2.3"></a>
##### 2.3. Collision-free protocols:
**Bitmap**:
- Các giao thức tránh va chạm hoàn toàn
	- Người gửi phải biết khi nào đến lượt họ
- Giao thức bit-map cơ bản:
	- Người gửi đặt một chút trong khe tranh chấp nếu họ có dữ liệu
	- Người gửi gửi lại; Mọi người đều biết ai có dữ liệu
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/6.png"></p>

**Token Ring**:
- Token gửi vòng tròn định nghĩa thứ tự gửi
	- Trạm có token có thể gửi khung trước khi qua
	- Ý tưởng có thể được sử dụng mà không có vòng, ví dụ: xe buýt token
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/7.png"></p>

**Countdown**:
- Bộ đếm nhị phân cải thiện trên giao thức bitmap:
	- Trạm gửi địa chỉ của họ trong khe tranh chấp (log N bit thay vì N bit)
	- Các bit ORs trung bình; Máy trạm bỏ khi họ gửi "0" nhưng nhìn thấy "1"
	- Máy trạm biết địa chỉ đầy đủ của nó.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/8.png"></p>

<a name="2.4"></a>
##### 2.4. Limited-contention protocols:

Ý tưởng là chia các máy trạm thành các nhóm trong đó chỉ có một số lượng rất nhỏ có thể muốn gửi
- Tránh lãng phí do thời gian nhàn rỗi và xung đột.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/9.png"></p>

**Adaptive Tree Walk**:
- Cây chia trạm thành các nhóm (nút) để thăm dò:
	- Tìm kiếm sâu đầu tiên dưới các nút với các xung đột.
	- Bắt đầu tìm kiếm ở các cấp thấp hơn nếu >1 máy trạm dự kiến.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/10.png"></p>

<a name="2.5"></a>
##### 2.5. Wireless LAN protocols:

<a name="3"></a>
#### 3. Ethernet:

<a name="3.1"></a>
**Physical Layer**:
- Một cáp đồng trục chia sẻ với tất cả 
##### 3.1. Classic Ethernet:
các máy chủ gắn liền
	- Tối đa 10 Mbps, với mã hóa Manchester
	- Các máy chủ chạy giao thức Ethernet cổ điển để truy cập
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/11.png"></p>

**MAC**:
- Giao thức MAC là một CSMA / CD kiên trì (trước đó)
	- Trễ ngẫu nhiên (backoff) sau va chạm được tính với BEB (Binary Exponential Backoff)
	- Định dạng khung vẫn được sử dụng với Ethernet hiện đại.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/12.png"></p>

- Sự xung đột có thể xảy ra và mất khoảng 2t để phát hiện
	- `t` là thời gian để truyền qua Ethernet
	- Dẫn đến kích thước gói tin tối thiểu để phát hiện đáng tin cậy
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/13.png"></p>

**Performance:**
- Hiệu quả cho các khung hình lớn, ngay cả với nhiều người gửi
	- Phân hủy các khung nhỏ (và LAN dài)
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/14.png"></p>

<a name="3.2"></a>
##### 3.2. Switched/Fast Ethernet:

Hubs wire kết nối tất cả các dòng vào một miền CSMA / CD đơn.

Swithches mỗi cổng vào một miền riêng biệt:
- Nhiều throughput lớn hơn cho nhiều cổng
- Không cần CSMA / CD với đường full-duplex đầy đủ
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/15.png"></p>

Các Switches có thể được nối tới máy tính, Hub và Switches
- Hubs tập trung lưu lượng truy cập từ máy tính
- Thêm vào cách làm thế nào để chuyển đổi các khung trong 4.8
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/16.png"></p>

Ethernet mở rộng Fast Ethernet từ 10 đến 100 Mbps
- Cặp xoắn đôi (với Cat 5) chiếm ưu thế trên thị trường
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/17.png"></p>

<a name="3.3"></a>
##### 3.3. Gigabit/10 Gigabit Ethernet:

Switched Gigabit Ethernet bây giờ là loại vườn;

- Với các đường full-duplex đầy đủ giữa các máy tính/thiết bị chuyển mạch
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/18.png"></p>
- Gigabit Ethernet thường chạy qua cặp xoắn
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/19.png"></p>
- 10 Gigabit Ethernet đang được triển khai khi cần thiết
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/20.png"></p>
- 40/100 Gigabit Ethernet đang được phát triển

**UCL Record**:
- 1,125 terabytes mỗi giây, một hệ thống truyền thông quang học mới được phát triển bởi UCL đã lập kỷ lục mới về tốc độ truyền dữ liệu nhanh nhất cho thông tin số.
- Theo tỷ lệ trích dẫn, toàn bộ loại HD của chương trình truyền hình Game of Thrones có thể được tải xuống trong vòng chưa đầy một giây.
- Họ sử dụng kỹ thuật giảm tiếng ồn thường thấy trong truyền thông không dây và áp dụng chúng vào truyền dẫn quang học.
- Dựa trên các công việc trước đó, nhóm nghiên cứu đã truyền tín hiệu quang học qua error-freee trên thế giới là 5.890 km, hệ thống mới sử dụng tổng cộng 15 kênh truyền dữ liệu, mỗi tín hiệu quang học mang các bước sóng khác nhau.
- Được điều chế bằng cách sử dụng định dạng 256QAM thường được sử dụng trong modem cáp, 15 tín hiệu được kết hợp và sau đó gửi đến một máy thu quang duy nhất để phát đi.

#### 4. Wireless LANs:
<a name="4"></a>

**Đặc điểm của các tiêu chuẩn liên kết không dây đã chọn:**
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/21.png"></p>

**Phân loại mạng không dây:**
| |single hop   | multiple hops | 
| :-------: | :----: |:----: |
| **infrastructure (e.g., APs)** | Máy chủ kết nối với trạm cơ sở (WiFi, WiMAX, di động) kết nối đến Internet lớn hơn | Máy chủ lưu trữ có thể phải chuyển tiếp qua một số nút không dây để kết nối với mạng lớn hơn Internet: mesh net | 
| **no infrastructure** |Không có trạm cơ sở, không có kết nối với lớn hơnInternet (Bluetooth, mạng cố định) | Không có trạm cơ sở, không có kết nối với Internet lớn hơn. Có thể phải chuyển tiếp để tiếp cận với một nút không dây nào đó MANET, VANET |

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Slide/Image/22.png"></p>

**Đặc điểm liên kết không dây:**

- Sự khác biệt từ liên kết có dây ....
	- Giảm cường độ tín hiệu: tín hiệu vô tuyến giảm khi nó truyền qua vật chất (path loss)
	- Sự can thiệp từ các nguồn khác: tần số mạng không dây chuẩn hóa (ví dụ: 2,4 GHz) được chia sẻ bởi các thiết bị khác (ví dụ: điện thoại); Các thiết bị (động cơ) cũng can thiệp vào
	- Sự truyền nhiều đường: tín hiệu radio phản ánh các vật thể trên mặt đất, đến điểm đích của quảng cáo ở những thời điểm khác nhau
.... Làm cho giao tiếp qua (thậm chí là một điểm đến điểm) liên kết không dây và nhiều hơn nữa gặp "khó khăn".

**Wireless & MAC** 

Một trạm trên mạng LAN không dây có thể không truyền được khung tới hoặc nhận các khung từ tất cả các trạm khác vì phạm vi vô tuyến của trạm.

Trong LAN có dây, khi một trạm gửi một khung, tất cả các trạm khác nhận được nó. *Sự vắng mặt của điều này trong các mạng LAN không dây gây ra một loạt các biến chứng*.

Trên một mạng không dây, vấn đề của một trạm không thể phát hiện ra đối thủ cạnh tranh tiềm năng cho môi trường bởi vì đối thủ cạnh tranh quá xa xôi được gọi là hidden terminal problem.

Ngoài ra còn có vấn đề thiết bị đầu cuối.

Các nút không thể phát hiện xung đột, tức là cảm nhận trong khi gửi
- Làm cho xảy ra xung đột tốn kém và tránh .


<a name="4.1"></a>
##### 4.1. 802.11 architecture/protocol stack:

<a name="4.2"></a>
##### 4.2. 802.11 physical layer:

<a name="4.3"></a>
##### 4.3. 802.11 MAC:

<a name="4.4"></a>
##### 4.4. 802.11 frames:

<a name="5"></a>
#### 5. Broadband Wireless:

<a name="5.1"></a>
##### 5.1. 802.16 Architecture / Protocol Stack:

<a name="5.2"></a>
##### 5.2. 802.16 Physical Layer:

<a name="5.3"></a>
##### 5.3. 802.16 MAC:

<a name="5.4"></a>
##### 5.4. 802.16 Frames:

<a name="6"></a>
#### 6. Bluetooth:

<a name="6.1"></a>
##### 6.1. Bluetooth Architecture:

<a name="6.2"></a>
##### 6.2. Bluetooth Applications / Protocol:

<a name="6.3"></a>
##### 6.3. Bluetooth Radio / Link Layers:

<a name="6.4"></a>
##### 6.4. Bluetooth Frames:

<a name="7"></a>
#### 7. RFID:

<a name="7.1"></a>
##### 7.1. Gen 2 Architecture:

<a name="7.2"></a>
##### 7.2. Gen 2 Physical Layer:

<a name="7.3"></a>
##### 7.3. Gen 2 Tag Identification Layer:

<a name="7.4"></a>
##### 7.4. Gen 2 Frames:

<a name="8"></a>
#### 8. Data Link Layer Switching:

<a name="8.1"></a>
##### 8.1. Uses of Bridges:

<a name="8.2"></a>
##### 8.2. Learning Bridges:

<a name="8.3"></a>
##### 8.3. Spanning Tree:

<a name="8.4"></a>
##### 8.4. Repeaters, hubs, bridges, .., routers, gateways:

<a name="8.5"></a>
##### 8.5. Virtual LANs:










	
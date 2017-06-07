## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **07/06/2017**

---------------------------------------------

### Mục lục

[1. DNS – Domain Name System](#1)

- [1.1. The DNS Name Space](#1.1)
- [1.2. Domain Resource Records](#1.2)
- [1.3. Name Servers](#1.3)

[2. Email](#2)

- [2.1. Architecture and Services](#2.1)
- [2.2. The User Agent](#2.2)
- [2.3. Message Formats](#2.3)
- [2.4. Message Transfer](#2.4)
- [2.5. Final Delivery](#2.5)

[3. WWW Architectural Overview](#3) 

- [3.1. Architectural Overview](#3.1) 
- [3.2. Static Web Pages](#3.2) 
- [3.3. Dynamic Pages & Web Applications](#3.3) 
- [3.4. HTTP](#3.4) 

[4. The Mobile Web](#4) 

- [4.1. Digital Audio](#4.1) 
- [4.2. Digital Video](#4.2) 
- [4.3. Streaming Stored Media](#4.3) 
- [4.4. Real-Time Conferencing-SIP](#4.4) 
- [4.5. Server Farms and Web Proxies](#4.5) 
- [4.6. CDNs – Content Delivery Networks](#4.6) 
- [4.7. Peer-to-Peer Networks](#4.7) 


---------------------------------------------
<a name="1"></a>
### 1. DNS – Domain Name System

- DNS giải quyết các tên người dùng có thể đọc cấp cao từ máy tính tới các địa chỉ IP cấp thấp - name space, Domain Resource records & Name servers
- DNS namespace có thứ bậc từ gốc xuống
	- Các bộ phận khác nhau được giao cho các tổ chức khác nhau
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/1.png"></p>

<a name="1.1"></a>
#### 1.1. The DNS Name Space

- Các tên miền cấp cao chung chung được kiểm soát bởi ICANN, người chỉ định các đăng ký để chạy chúng
- Hầu hết các công trình của nó liên quan đến Hệ thống tên miền toàn cầu của Internet, bao gồm phát triển chính sách cho việc quốc tế hóa hệ thống DNS, giới thiệu các tên miền cấp cao (TLDs) mới, và hoạt động của các root name server. Các cơ sở đánh số mà ICANN quản lý bao gồm không gian địa chỉ Giao thức Internet cho IPv4 và IPv6 và phân bổ các khối địa chỉ cho các đăng ký Internet khu vực. ICANN cũng duy trì đăng ký nhận dạng giao thức Internet.
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/2.png"></p>

<a name="1.2"></a>
#### 1.2. Domain Resource Records

- Các tài nguyên nguồn quan trọng trong không gian tên là IP address (A / AAAA) và các name server (NS), nhưng còn có các thứ khác (ví dụ: MX)

| Type    | Ý nghĩa 	   | Giá trị  |
| :-----: | :----------:   | :------: |
| SOA	  | quyền bắt đầu  |   Tham số của vùng |
| A   	  | IPv4 của host  |  32 bit số nguyên  |
| AAAA    | IPv6 của host  |  128 bit số nguyên |
| MX      | giao dich mail |  ưu tiên, tên miền mail được chấp nhận  |
| NS      | tên máy chủ    |  tên của máy chủ phân giải tên miền  |
| CNAME   | tên chuẩn      |  Tên miền  |
| PTR	  | Con trỏ		   |   Định danh của IP add |
| SPF	  | Gửi các chính sách về frame  |  mã hóa các văn bản về chính sách gửi  mail |
| SRV	  | Dịch vụ    	   |   Host cug cấp nó |
| TXT	  | text  |   mô tả văn bản bằng ASCII |

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/3.png"></p>
- Một phần của cơ sở dữ liệu DNS có thể cho cs.vu.nl

<a name="1.3"></a>
#### 1.3. Name Servers

- Name server chứa dữ liệu cho các phần của không gian tên gọi là zones (vòng tròn).
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/4.png"></p>

- Tìm địa chỉ IP cho một tên máy chủ được gọi là **Resolution** và được thực hiện với giao thức DNS.
	- Resolution: Máy tính yêu cầu  giải quyết từ local name server . Tiếp theo,local name server yêu cầu root name server, Root trả về tên máy chủ cho một vùng thấp hơn và cuối cùng là tiếp tục xuống vùng cho đến khi tên máy chủ có thể trả lời
	- Giao thức DNS: Chạy trên UDP port 53, truyền lại tin nhắn đã mất và lưu trữ các câu trả lời cho tên máy chủ để có hiệu suất tốt hơn
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/5.png"></p>

<a name="2"></a>
### 2. Email

Các thành phần chính và các bước (đánh số) để gửi email
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/6.png"></p>

<a name="2.1"></a>
#### 2.1. Architecture and Services

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/7.png"></p>

<a name="2.2"></a>
#### 2.2. The User Agent

Những gì người dùng nhìn thấy - giao diện các yếu tố của một tác nhân user agent
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/8.png"></p>

<a name="2.3"></a>
#### 2.3. Message Formats

- Trường Header liên quan đến Transport message; Header có thể đọc được văn bản ASCII

| Header   | Ý nghĩa 	   | 
| -----: | :----------:   |
| To:	  | Địa chỉ mail của người nhận chính  |   
| Cc:  	  | Địa chỉ mail của người nhận phụ  | 
| Bcc:    | Địa chỉ mail bản sao của người mù | 
| From:     | Người viết mail | 
| Sender:     | Địa chỉ mail của người gửi thực tế   |  
| Received:   | Dòng bổ sung của mỗi đại lý chuyển giao dọc theo tuyến đường đi  |  
| return-Path:	 | Xác định dường đi trở lại người gửi	   |  

- Các trường tiêu đề khác hữu ích cho user agent

| Header   | Ý nghĩa 	   | 
| :-----: | :----------:   |
| Date:	  | Ngày và thời gian tin được gửi đi  |   
| Reply-to:  	  | Địa chỉ email cái mà sẽ trả lời  | 
| Message Id:    | Số duy nhất để tham khảo thông báo này muộn | 
| In-Reply-to:     | Mess-Id của tin nhắn cái mà sẽ trả lời | 
| References:     | Mess-Id có liên quan khác   |  
| Keywords:   | Chọn key sử dụng  |  
| Subject:	 | Tóm tắt ngắn nội dung mess bằng 1 dòng   |  

- MIME Header được sử dụng để mô tả nội dung nào trong nội dung thư

| Header   | Ý nghĩa 	   | 
| :-----: | :----------:   |
| MIME Version:	  | Xác định phiên bản MIME  |   
| Content-Discription: | Người được phép đọc mess  | 
| Content-Id:    | Xác định số định danh | 
| Content-Transfer-Encoding:    |Phần bên ngoài gói tin sẽ truyền | 
| Content-Type:    | Loại và định dạng của nội dung | 

- Các loại nội dung MIME phổ biến và các phân nhóm phụ

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/9.png"></p>
 
- Đặt tất cả lại với nhau: một Message nhiều phần có chứa các lựa chọn HTML và audio.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/10.png"></p>

<a name="2.4"></a>
#### 2.4. Message Transfer

- Các tin nhắn được chuyển bằng SMTP (Simple Mail Transfer Protocol)
	- Các lệnh văn bản có thể đọc được
	- Gửi từ user agent đến MTA trên port 587
	- Một MTA cho MTA tiếp theo trên port 25
	- Các giao thức khác để phân phối cùng (IMAP, POP3)
- Gửi tin nhắn:
	- Từ Alice đến Bob
	- Các lệnh SMTP được đánh dấu [màu hồng]

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/11.png"></p>

- Các mở rộng SMTP thông thường (không phải trong ví dụ đơn giản)

| Keyword   | Description 	   | 
| :-----: | :----------:   |
| AUTH	  | Xác thực khách hàng |   
| BINARYMINE 	  | Máy chủ sẽ nhị phân tin nhắn  | 
| CHUNKING    | Máy chủ chấp nhận tin nhắn lớn trong khối | 
| SIZE    | Kiễm tra kích thước tin nhắn trươc khi gửi | 
| STARTTLS    | Chuyển sang vận chuyển an toàn(TLS)  |  
| UTF8SMTP   | Địa chỉ quốc tế  |  

<a name="2.5"></a>
#### 2.5. Final Delivery

- User agent sử dụng giao thức như IMAP để gửi cuối cùng
	- Có các lệnh để thao tác các folder/message
- Ngoài ra, một giao diện Web (với giao thức độc quyền) có thể được sử dụng

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/12.png"></p>

<a name="3"></a>
### 3. WWW Architectural Overview

<a name="3.1"></a>
#### 3.1. Architectural Overview

- HTTP chuyển các trang từ máy chủ sang trình duyệt

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/13.png"></p>

- Các trang được đặt tên với URL (Uniform Resource Locators)
	- Ví dụ: http://www.phdcomics.com/comics.php

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/14.png"></p>

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/15.png"></p>

- Các bước mà client (trình duyệt) phải thực hiện theo một liên kết:
	- Xác định giao thức (HTTP) -
	- Hỏi DNS cho địa chỉ IP của máy chủ
	- Thực hiện kết nối TCP với máy chủ
	- Gửi yêu cầu trang; Máy chủ gửi nó trở lại
	- Lấy các URL khác nếu cần để hiển thị trang
	- Đóng các kết nối TCP nhàn rỗi
- Các bước mà máy chủ cần để phục vụ các trang:
	- Chấp nhận kết nối TCP từ máy khách
	- Nhận yêu cầu trang và ánh xạ nó vào một tài nguyên (ví dụ: tên tệp)
	- Nhận tài nguyên (ví dụ: tệp từ đĩa)
	- Gửi nội dung của tài nguyên cho khách hàng.
	- Phát hành các kết nối TCP nhàn rỗi

- Loại nội dung được xác định bởi các loại MIME
	- Trình duyệt có hành động phù hợp để hiển thị
	- Các Plug-ins / helper  mở rộng trình duyệt cho các loại mới

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/16.png"></p>

- Để nâng cao hiệu suất, các áy chủ Web có thể sử dụng:
	- Bộ nhớ đệm, nhiều luồng và đầu giao diện người dùng

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/17.png"></p>

-Các bước của máy chủ, được xem xét lại:
	- Giải quyết các yêu cầu của trang Web
	- Thực hiện kiểm soát truy cập trên trang Web
	- Kiểm tra bộ nhớ cache
	- Tìm trang yêu cầu từ đĩa hoặc chạy chương trình
	- Xác định phần còn lại của phản hồi
	- Trả lời phản hồi cho khách hàng
	- Tạo mục nhập trong nhật ký máy chủ

- Cookie hỗ trợ tương tác máy khách / máy chủ
	- Máy chủ gửi cookie (trạng thái) với phản hồi trang
	- Khách hàng lưu trữ các cookie trên trang tìm nạp
	- Khách hàng gửi cookie trở lại máy chủ với yêu cầu

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/18.png"></p>

<a name="3.2"></a>
#### 3.2. Static Web Pages

- Các trang web tĩnh chỉ đơn giản là các tệp
	- Có cùng nội dung cho mỗi lần xem
- Có thể trực quan phong phú và tương tác:
	- HTML kết hợp văn bản và image-form thu thập dữ liệu người dùng nhập
	- Các tờ kiểu dáng phù hợp với trình bày và đồ họa Vector, video. . .
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/19.png"></p>

<a name="3.3"></a>
#### 3.3. Dynamic Pages & Web Applications 

- Các trang động được tạo ra bởi các chương trình chạy trên máy chủ (với cơ sở dữ liệu) và máy khách
	- Ví dụ, PHP ở máy chủ, JavaScript tại khách hàng
	- Trang thay đổi mỗi lần như sử dụng một ứng dụng

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/20.png"></p>

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/21.png"></p>

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/22.png"></p>

- Sự khác biệt giữa máy chủ và chương trình khách hàng

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/23.png"></p>

- Các ứng dụng web sử dụng một bộ công nghệ làm việc cùng nhau, ví dụ: AJAX:
	- *HTML*: trình bày thông tin dưới dạng các trang.
	- *DOM*: thay đổi các phần của trang trong khi chúng được xem.
	- *XML*: cho phép các chương trình trao đổi dữ liệu với máy chủ.
	- Cách gửi và truy xuất dữ liệu XML không đồng bộ.
	- JavaScript là một ngôn ngữ để ràng buộc tất cả những điều này với nhau.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/24.png"></p>

- XML nắm bắt cấu trúc tài liệu, không trình bày như HTML. Ví dụ:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/25.png"></p>

- Các ứng dụng Web sử dụng một bộ công nghệ, được xem xét lại:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/26.png"></p>

<a name="3.4"></a>
#### 3.4. HTTP

- HTTP (HyperText Transfer Protocol) là một giao thức request-response chạy trên TCP
	- Tìm trang từ server đến client
	- Máy chủ thường chạy trên port 80
	- Header được đưa ra trong ASCII dễ đọc
	- Nội dung được mô tả bằng các loại MIME
	- Giao thức đã hỗ trợ cho các yêu cầu đặt hàng
	- Giao thức có hỗ trợ bộ nhớ đệm
- HTTP sử dụng kết nối liên tục để cải thiện hiệu suất

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/27.png"></p>

- HTTP có 1 phương thức để yêu cầu

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/28.png"></p>

- Máy khách yêu cầu sẽ nói Response codes 

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/29.png"></p>

- nhiều header quan tâm đến key thông tin

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/30.png"></p>

- HTTP kiểm tra bộ nhớ để xem trình duyệt có bản sao mới, và nếu server không cập nhật trang
	- sử dụng tập hợp của header để kiểm tra
	- có thể sử dụng bộ nhớ lưu trử cao hơn (proxy)

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/31.png"></p>

<a name="4"></a>
### 4. The Mobile Web

- Điện thoại di động (điện thoại, máy tính bảng) rất khó khăn vì khách hàng:
	- Tương đối nhỏ màn hình
	- Khả năng đầu vào hạn chế, đầu vào dài.
	- Băng thông mạng bị hạn chế
	- Kết nối có thể bị gián đoạn.
	- Công suất máy tính bị hạn chế
- Các chiến lược để xử lý chúng:
	- Nội dung: máy chủ cung cấp các phiên bản thân thiện với điện thoại di động; Chuyển mã cũng có thể được sử dụng
	- Các giao thức: không cần thiết cho các giao thức chuyên biệt; HTTP với tiêu đề nén đầy đủ

<a name="4.1"></a>
#### 4.1 Digital Audio

- ADC (Analog-to-Digital Converter) sản xuất âm thanh từ một micro
	- Điện thoại: 8000 mẫu 8-bit / giây (64 Kbps); Âm thanh máy tính thường là chất lượng tốt hơn (ví dụ: 16 bit)
- Âm thanh số thường được nén trước khi gửi
	- Bộ mã hoá lossy (như AAC) khai thác nhận thức của con người
	- Tỷ lệ nén lớn (có thể> 10X)

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/32.png"></p>

<a name="4.2"></a>
#### 4.2. Digital Video

- Video được số hóa dưới dạng pixel (lấy mẫu, lượng tử)
	- Chất lượng truyền hình: 640x480 pixel, màu 24-bit, 30 lần / giây
- Video được gửi bị nén do băng thông lớn
	- Lossy nén khai thác nhận thức của con người
		- Ví dụ: JPEG cho ảnh tĩnh, MPEG, H.264 cho video
	- Tỷ lệ nén lớn (thường là 50X cho video)
	- Video thường> 1 Mbps, so với> 10 kbps cho phát âm và> 100 kbps cho âm nhạc

- Dãy nén JPEG lossy cho một ảnh:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/33.png"></p>

- Pixel được ánh xạ tới không gian màu luminance/chrominance (YCbCr) và chrominance được lấy mẫu phụ. Mắt ít nhạy cảm với chrominance

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/34.png"></p>

- MPEG nén trên một dãy khung hình, tiếp tục sử dụng theo dõi chuyển động để loại bỏ sự dư thừa thời gian
	- I (Intra-coded) khung được khép kín
	- P (Predictive) khung sử dụng các dự đoán chuyển động khối
	- Các khung B (Hai chiều) có thể dự đoán cơ sở trên khung trong tương lai

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/35.png"></p>

<a name="4.3"></a>
#### 4.3. Streaming Stored Media

- Một phương pháp đơn giản để truyền phương tiện lưu trữ, ví dụ: cho video theo yêu cầu, là tìm nạp video dưới dạng tệp tải xuống .... Nhưng có thời gian khởi động lớn, ngoại trừ tệp ngắn

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/36.png"></p>

- Truyền trực tuyến hiệu quả bắt đầu playout trong quá trình vận chuyển
	- Với RTSP(Real-Time Streaming Protocol) (Giao thức truyền thời gian thực)

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/37.png"></p>

- Vấn đề chính: làm thế nào để xử lý lỗi truyền

| Chiến lược | Lợi thế | Bất lợi |
| :-----: | :----------:   | :------: |
| Sử dụng tải tin cậy (TCP) | Sửa chữa tất cả lỗi | Tăng jitter đáng kể |
| Thêm FEC (ví dụ, Parity) | Sửa chữa lỗi | Tăng overhead, giải mã phức tạp và jitter  |
| Interleave phương tiện truyền thông | Masks hầu hết các lỗi | Tốc độ tăng độ phức tạp và sự phức tạp|

- Gói chẵn lẻ(Parity) có thể sửa chữa một gói tin bị mất trong một nhóm N
	- Giải mã được trì hoãn cho các gói tin N

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/38.png"></p>

- Interleaving lây lan các mẫu phương tiện truyền thông gần đó qua các truyền khác nhau để giảm tác động của sự loss

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/39.png"></p>

- Media có thể không đến đúng thời điểm phát sóng do băng thông thay đổi và truyền lại. Khách hàng đệm các phương tiện truyền thông để hấp thụ jitter; Chúng tôi vẫn cần phải chọn tốc độ truyền thông có thể đạt được

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/40.png"></p>

**Streaming Live Media:**
- Streaming media trực tiếp cũng tương tự như trường hợp được lưu trữ cộng với:
	- Không thể phát trực tuyến nhanh hơn "tỷ lệ trực tuyến" để tiến lên phía trước
		- Thông thường cần bộ đệm lớn hơn để hấp thụ jitter
- Thường có nhiều người dùng đang xem cùng một lúc
	- UDP với multicast cải thiện đáng kể hiệu quả. Nó hiếm khi có sẵn, do đó rất nhiều kết nối TCP được sử dụng.
	- Đối với rất nhiều người dùng, việc phân phối nội dung được sử dụng [sau]

<a name="4.4"></a>
#### 4.4. Real-Time Conferencing-SIP

- Hội thảo qua thời gian thực có hai hoặc nhiều luồng phương tiện trực tiếp được kết nối, ví dụ như thoại qua IP, cuộc gọi video Skype
- Vấn đề chính trong luồng trực tuyến là độ trễ thấp (tương tác)
	- Bạn muốn giảm sự chậm trễ để truyền gần
	- Lợi ích từ hỗ trợ mạng, ví dụ: QoS
	- Hoặc, lợi ích từ băng thông phong phú (không tắc nghẽn)

-**H.323 architecture**(kiến trúc H.323) cho điện thoại Internet hỗ trợ các cuộc gọi giữa các máy tính Internet và điện thoại PSTN. Cuộc gọi là audio/video qua RTP/UDP/IP

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/41.png"></p>

**SIP:**
- SIP (Session Initiation Protocol) là một sự thay thế cho H.323 để thiết lập các cuộc gọi theo thời gian thực
	- Giao thức đơn giản, dựa trên văn bản với URL dành cho địa chỉ
	- Dữ liệu được thực hiện với RTP / RTCP như trước

| Phương pháp  | Miêu tả 	   | 
| :-----: | :----------:   |
| INVITE  | Yêu cầu bắt đầu phiên làm việc |   
| ACK 	  | Xác nhận phiên làm vệc được bắt đầu  | 
| BYE    | Yêu cầu chấm dứt phiên làm việc  | 
| OPTIONS | Truy vấn  khả năng cũa một máy chủ | 
| CANCEL    | Hủy một yêu cầu đang chờ giải quyết  |  
| REGISTER   |Thông báo cho máy chủ chuyển hướng về vị trí hiện tại của người dùng |  

- Thiết lập một cuộc gọi bằng cách bắt tay SIP ba bước
	- Máy chủ proxy cho phép kết nối từ xa
	- Gọi dữ liệu trực tiếp giữa người gọi / người gọi

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/42.png"></p>

| Item | H.323 | SIP |
| :----- | :----------:   | :------: |
| Thiết kế bởi  | ITU | IETF |
| Tính tương thích với PSTN | Yes |Largely |
| Tính tương thích với Internet | Yes, over time | Yes |
| Kiến trúc | Monolithic | Mô-đun |
| Thương lượng thông tin | Xếp các giao thức đầy đủ | SIP chỉ xử lí thiết lập |
| Gọi tín hiệu | yes | yes |
| Định dạng tin | Q.931 over TCP | SIP over TCP or UDP |
| truyền thông | Binary | ASCII |
| vận tải | RTP/RTCP | RTP/RTCP |
| Cuộc gọi đa năng | Yes | Yes |
| Hội thảo đa phương tiện | Yes | No |
| Giải quyết | URL hoặc số điện thoại | URL |
| Chấm dứt cuộc gọi |  Rõ ràng hoặc TCP phát hành | Rõ ràng hoặc TCP chờ |
| Tin nhắn tức thời | No | Yes|
| Mã hóa   | Yes | Yes |
| kích thước các tiêu chuẩn | 1400 trang | 250 trang |
| Thực hiện | Lớn và phức tạp | Trung bình nhưng có vấn đề |
| Trang thái | Rộng rãi, vd: video | Thay thế, vd: tiếng nói |

<a name="4.5"></a>
#### 4.5. Server Farms and Web Proxies

- Server Farms cho phép các máy chủ Web quy mô lớn:
	- Yêu cầu cân bằng tải trên máy chủ
	- Các máy chủ truy cập cùng một cơ sở dữ liệu phụ trợ

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/43.png"></p>

- Lưu trữ Proxy giúp các tổ chức mở rộng nội dung-Máy chủ Cache trên máy khách cho hiệu suất và cũng thực hiện các chính sách của tổ chức (ví dụ: quyền truy cập)

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/44.png"></p>

<a name="4.6"></a>
#### 4.6. CDNs – Content Delivery Networks

- CDNs quy mô máy chủ bởi khách hàng có được nội dung từ một nút gần đó CDN (bộ nhớ cache)

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/45.png"></p>

- Chỉ đạo khách hàng đến các nút CDN ở gần với DNS:
	- Truy vấn là máy khách phản hồi trả về nút CDN cục bộ 
	- Nút cục bộ CDN lưu trữ nội dung cho các khách hàng gần đó và giảm tải trên máy chủ gốc

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/46.png"></p>

- Máy chủ gốc khởi tạo lại các trang để phục vụ nội dung thông qua CDN

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/47.png"></p>

<a name="4.7"></a>
#### 4.7. Peer-to-Peer Network

- P2P (Peer-to-Peer) là một kiến trúc CDN thay thế mà không có cơ sở hạ tầng chuyên dụng (nghĩa là máy chủ)
	- Khách hàng phục vụ nội dung với nhau như các đồng nghiệp

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/48.png"></p>

- Thử thách khi máy chủ bị xóa:
	- a. Làm thế nào để bạn bè tìm thấy nhau?
	- b. Làm thế nào để đồng nghiệp hỗ trợ tải nội dung nhanh?
	- c. Các bạn đồng trang khuyến khích nhau tải lên như thế nào?

- *BitTorrent* cho phép peer download torrents
	- Các đồng nghiệp tìm nhau thông qua Tracker trong tập tin torrent
	- Trao đổi các bộ phận (các phần của nội dung) với các đối tác, thích những người gửi nhanh nhất
	- Nhiều tốc độ tải về ngang hàng; giúp tải lên

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/49.png"></p>

- Kademlia được sử dụng trong BitTorrent
- Bảng Hash phân tán (Distributed Hash Tables - DHTs) được phân bổ đầy đủ chỉ số có quy mô cho nhiều khách hàng
	- Cần theo đường dẫn O (log N) cho N mục
	- Có thể sử dụng như Tracker để tìm các peers không có máy chủ
	- Tìm torrent (định danh) trong DHT để tìm IP của các peer
- Một Vòng Chord gồm 32 ký tự nhận dạng. Bàn tay [ở bên phải, và dưới dạng vòng cung] được sử dụng để điều hướng vòng tròn. Ví dụ: đường đi tìm kiếm 16 từ 1 là 1 --> 12 --> 15

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Slide/Image/50.png"></p>

----------------------------------------------

### Tài liệu dịch

[1] Slide Lecture 7: Application Layer 
 http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm



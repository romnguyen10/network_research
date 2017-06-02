## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **02/06/2017**

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

[3. WWW Architectural Overview](#2) 


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
| :-----: | :----------:   |
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


----------------------------------------------

### Tài liệu dịch

[1] Slide Lecture 7: Application Layer 
 http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm


## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **14/05/2017**

### Mục lục

[1. TCP (Transmission Control Protocol)](#1)

- [1.1. Requirements](#1.1)
- [1.2. Step 1: Capture a Trace](#1.2)
- [1.3. Step 2: Inspect the Trace](#1.3)
- [1.4. Step 3: TCP Segment Structure](#1.4)
- [1.5. Step 4: TCP Connection Setup/Teardown](#1.5)
- [1.6. Step 5: Connection Options](#1.6)
- [1.7. Step 6: FIN/RST Teardown](#1.7)
- [1.8. Step 7: TCP Data Transfer](#1.8)

[2. UDP (User Datagram Protocol)](#2)

- [2.1. Step 1: Capture a Trace](#2.1)
- [2.2. Step 2: Inspect the Trace](#2.2)
- [2.3. Step 3: UDP Message Structure](#2.3)
- [2.4. Step 4: UDP Usage](#2.4)

[3. Routing](#3)

[4. Tài liệu dịch](#4)
--------------------------------------------------------

<a name="1"></a>
### 1. TCP (Transmission Control Protocol):

<a name="1.1"></a>
#### 1.1. Requirements:

- Wireshark:

	- Bài lab này sử dụng Wireshark để nắm bắt hoặc kiểm tra một gói tin. Một gói tin bắt được là một bản ghi lưu lượng truy cập ở một vị trí trên mạng,
	 như thể chụp nhanh tất cả các bit truyền qua một đường dây cụ thể. lưu lượng gói tin  bắt đuoc ghi lại dấu thời gian cho 1 gói, cùng với các bit tạo nên 
	 gói tin, từ các tiêu đề lớp thấp đến các nội dung lớp cao hơn.
	- Wireshark chạy trên hầu hết các hệ điều hành, bao gồm Windows, Mac và Linux. Nó cung cấp một giao diện đồ họa cho người dùng giúp thấy chuỗi các gói tin 
	 và ý nghĩa của các bit khi được giải thích như các tiêu đề và dữ liệu của các giao thức. Các gói được mã hoá màu sắc để chuyển tải ý nghĩa của chúng
	- Wireshark bao gồm nhiều cách khác nhau để lọc và phân tích chúng để giúp bạn điều tra các khía cạnh khác nhau của 1 gói tin. Nó được sử dụng rộng rãi 
	 để khắc phục sự cố mạng. Bạn có thể tải Wireshark từ www.wireshark.org nếu nó chưa được cài đặt trên máy tính của bạn. Chúng tôi khuyên bạn nên xem đoạn 
	 video ngắn "Introduction to Wireshark" ngắn 5 phút trên trang web.

- wget / curl:

	- Bài Lab này sử dụng *wget* (Linux và Windows) và *curl* (Mac) để tìm nạp tài nguyên web. *Wget và curl* là các chương trình dòng lệnh cho phép bạn 
	 tìm nạp một URL. Không giống trình duyệt web,nó tìm nạp và thực hiện toàn bộ các trang, 
	- *wget và curl* cho phép bạn kiểm soát chính xác những URL nào bạn tìm nạp và khi bạn tìm nạp chúng. Trong Linux, wget có thể được cài đặt thông qua 
	 trình quản lý gói. Trong Windows, wget có sẵn dưới dạng nhị phân tại trang web của tôi http://scisweb.ulster.ac.uk/~kevin/com320/labs/wget.exe hoặc
	 tìm thông tin tải xuống trên http://www.gnu.org/ Phần mềm / wget /. Cả hai đều có nhiều tuỳ chọn (hãy thử `wget --help` hoặc `curl --help` để xem) 
	 nhưng một URL có thể được tìm nạp đơn giản chỉ với `wget URL` hoặc `curl URL`.

- Browser: Bài lab sử dụng trình dyệt để tìm và lấy các thông tin trang phục vụ cho công viiệc. Có thể sử dụng bất cứ trình duyệt nào.


<a name="1.2"></a>
#### 1.2. Step 1: Capture a Trace:

*Tiến hành như sau để bắt 1 gói tin của một kết nối TCP duy nhất mà nó sẽ gửi một lượng thông tin của dữ liệu; Cách khác, bạn có thể sử dụng dữ liệu được cung cấp.*
Nhiều ứng dụng sử dụng TCP như một phương tiện giao thông, bao gồm các trình duyệt web. Vì vậy,đơn giản  chúng tôi sẽ thực hiện tải xuống trên web để 
thực hiện kết nối TCP. Tuy nhiên, lưu ý rằng TCP có thể truyền dữ liệu theo cả hai hướng cùng một lúc nhưng với nội dung tải về chỉ được gửi từ máy chủ từ xa đến 
máy tính cục bộ (sau yêu cầu ban đầu).

- a. *Tìm URL của một tài nguyên có kích thước vừa phải và bạn có thể tải xuống bằng cách sử dụng HTTP (chứ không phải HTTPS)*. Bạn có thể sử dụng trình duyệt để 
tìm kiếm, có thể tìm kiếm hình ảnh (.jpg) hoặc tài liệu PDF (.pdf). Bạn muốn đảm bảo rằng đó là một tài nguyên chứ không phải trang web (ví dụ: .html) với
nhiều tài nguyên được liệt kê.

- b. *Tìm nạp URL bằng *wget* hoặc *curl* để kiểm tra xem bạn có thể truy xuất ít nhất 500 KB nội dung qua ít nhất vài giây mạng*. Ví dụ: sử dụng lệnh 
`wget http://scisweb.ulster.ac.uk/~kevin/com320/papers/macpaper.pdf` hoặc truy cập `http://conferences.sigcomm.org/sigcomm/2011/conf- Program.php`
trong trình duyệt của bạn và chọn PDF để tải xuống. Các ví dụ thành công về tìm nạp dữ liệu được hiển thị trong hình bên dưới.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/1.png"></p>

- c. Khởi động Wireshark và bắt đầu bắt gói với một bộ lọc là `tcp and host xx.xx.xx`, trong đó xx.xx.xx là tên của máy chủ từ xa mà bạn sẽ tìm nạp nội dung, 
ví dụ như *conferences.sigcomm. Org* trong hình minh họa ví dụ dưới đây.Ý tưởng ở đây là dùng bộ lọc để chỉ nắm bắt giao thông TCP giữa máy tính của bạn và máy chủ.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/2.png"></p>

- d. Sau khi capture bắt đầu, hãy lặp lại lệnh *wget / curl* ở trên. Lần này, các gói tin cũng sẽ được ghi lại bởi Wireshark.

- e. Khi lệnh hoàn tất, quay lại Wireshark và sử dụng các menu hoặc các nút để dừng dấu vết. Bây giờ bạn sẽ có một dấu vết tương tự như thể hiện trong 
hình bên dưới. Chúng tôi đã mở rộng chi tiết của tiêu đề TCP, vì đây là trọng tâm trong bài lab này.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/3.png"></p>

<a name="1.3"></a>
#### 1.3. Step 2: Inspect the Trace:

- Chọn một gói dữ liệu dài bất kỳ nơi nào giữa dấu vết của bạn mà giao thức có tên là TCP. Mở rộng phần giao thức TCP trong bảng điều khiển trung tâm 
(bằng cách sử dụng trình mở rộng hoặc biểu tượng **>**).
 Tất cả các gói tin ngoại trừ *HTTP GET* ban đầu và gói cuối cùng của *HTTP response* sẽ được liệt kê dưới dạng TCP. Chọn một gói tin dài đảm bảo rằng chúng ta
 đang tìm kiếm một gói tải xuống từ máy chủ đến máy tính của bạn. Nhìn vào các lớp giao thức, bạn sẽ thấy một khối IP trước khối TCP. Điều này là do đoạn 
 TCP được thực hiện trong một IP.

- bạn sẽ thấy các trường như sau:
	- Đầu tiên là *source port*, sau đó là *Destination port*. Đây là địa chỉ mà TCP thêm ngoài địa chỉ IP. source port có thể là 80 vì gói tin được gửi bởi web server
	 và port máy chủ web chuẩn là 80.
	- Sau đó ta quan sát tiếp trường *sequence number*. Nó cho vị trí trong bytestream của byte payload đầu tiên.
	- Tiếp theo là *acknowledgement*. Nó cho biết vị trí nhận được cuối cùng trong luồng byte đảo ngược.
	- *Header lenght* cho biết chiều dài của tiêu đề TCP.
	- Trường *flags* có nhiều bit cờ để chỉ ra kiểu phân đoạn TCP. Bạn có thể mở rộng nó và nhìn vào các cờ của nó.
	- Tiếp theo là *Checksum*, để phát hiện lỗi truyền dẫn.
	- Có thể có một trường *options* với các tùy chọn khác nhau. Bạn có thể mở rộng trường này và khám phá nếu bạn muốn, nhưng chúng tôi sẽ xem xét các tùy chọn
	 cụ thể hơn sau.
	- Cuối cùng, có thể có một TCP pay load, mang các byte đang được vận chuyển.

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/4.png"></p>
- Cũng như các trường ở trên, có thể có các đường dây thông tin khác mà Wireshark cung cấp để giúp bạn giải thích các gói tin.

#### 1.4. Step 3: TCP Segment Structure:

Hãy phác hoạ một hình ảnh của phân đoạn TCP mà bạn đã học. Nó sẽ hiển thị vị trí và kích thước theo byte của các trường  TCP header bạn có thể quan sát bằng
cách sử dụng Wireshark. Đừng phá vỡ trường Flags, hoặc bất kỳ trường Options, và nếu bạn thấy rằng một số trường TCP chia sẻ một byte sau đó nhóm chúng lại.
Như thường lệ, số liệu của bạn chỉ đơn giản thể hiện khung như một hình chữ nhật dài, mỏng. Cố gắng không nhìn vào hình, kiểm tra nó sau đó để lưu ý và thấy
bất kỳ sự khác biệt nào.

Để làm việc với kích thước, hãy quan sát rằng khi bạn nhấp vào khối giao thức trong bảng điều khiển trung tâm ( không phải là trình mở rộng "+"),
Wireshark sẽ làm nổi bật các byte tương ứng trong gói trong bảng dưới cùng và hiển thị chiều dài tại Dưới cùng của cửa sổ. Bạn cũng có thể sử dụng kích thước 
gói tổng thể được hiển thị trong ngăn Chiều dài hoặc Khối chi tiết khung. Lưu ý rằng phương pháp này sẽ không cho bạn biết các vị trí phụ byte.
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/5.png"></p>

**Answers to Step 3:**
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/6.png"></p>
    
- sơ đồ này khác với bản vẽ sơ đồ trong sách với các khía cạnh nhỏ:
	- Trường *Header length* và *Flags* được kết hợp thành 2 byte. Không dễ dàng xác định độ dài bit của chúng bằng Wireshark.
	- Trường *Urgent Pointer* được hiển thị như dấu chấm. Trường này thường không được sử dụng, và do đó không hiển thị trong Wireshark 
	 Tuy nhiên, bạn có thể nhận thấy sự tồn tại của nó trong Wireshark bằng cách quan sát các byte bằng không trong phân đoạn được bỏ qua khi bạn chọn 
	 các trường khác .
	- Trường *Options* được hiển thị dấu chấm, vì nó có thể hoặc không thể hiện diện trong các phân đoạn. Thông thường nó sẽ hiện diện, 
	 và khi nó được chiều dài của nó sẽ là một bội số của 4 byte.
	- *Payload* là tùy chọn. Nó hiện diện cho phân khúc mà bạn đã xem, chẳng hạn như không có mặt trên phân khúc *Ack-only*.

<a name="1.5"></a>
#### 1.5. Step 4: TCP Connection Setup/Teardown:

**Three-Way Handshake(bắt tay ba bước):**
*Để xem "Three-Way Handshake",hãy tìm kiếm một phân đoạn TCP với cờ SYN trên, rất có thể ở các gói tin đầu tiên của bạn, và các gói tin đi theo nó.*
Cờ SYN được ghi lại trong cột Thông tin. Bạn cũng có thể tìm kiếm các gói có cờ SYN bằng cách sử dụng BỘ lọc **tcp.flags.syn == 1**. Một **SYN packet**
là bắt đầu của bắt tay ba bước. Trong trường hợp này nó sẽ được gửi từ máy tính của bạn tới máy chủ từ xa. Máy chủ từ xa phải trả lời với một phân đoạn TCP
với cờ SYN và ACK, hoặc một gói **SYN ACK**. Khi nhận được, máy tính của bạn sẽ trả lời ACK, cân nhắc việc thiết lập kết nối và bắt đầu gửi dữ liệu, 
trong trường hợp này sẽ là yêu cầu HTTP.

*Vẽ sơ đồ chuỗi thời gian của bắt tay ba bước , bao gồm gói dữ liệu đầu tiên (yêu cầu HTTP GET) được gửi bởi máy tính của bạn khi 
kết nối được thiết lập.* Thông thường, thời gian chạy xuống trang, và các dòng trên trang cho biết phân đoạn. Kết quả sẽ tương tự như sơ đồ như hình bên dưới.
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/7.png"></p>

**Các tính năng**:
- Số Sequence và ACK, nếu có, trên mỗi phân đoạn. Số ACK chỉ được thực hiện nếu phân đoạn có cờ ACK được đặt.
- Thời gian tính bằng mili giây, bắt đầu từ 0, mỗi phân đoạn được gửi hoặc nhận ở máy tính của bạn.
- Thời gian khứ hồi cho máy chủ ước tính là sự khác nhau giữa các phân đoạn SYN và SYN-ACK.

**Answers to Step 4: TCP Connection Setup/Teardown**:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/8.png"></p>

Có một số tính năng cần lưu ý:
- SYN ban đầu không có số ACK, chỉ có một số thứ tự. Tất cả các gói tin tiếp theo đều có số ACK.
- Số thứ tự ban đầu được hiển thị bằng 0 trong mỗi hướng. Điều này là do Wireshark được cấu hình để hiển thị số thứ tự liên quan.Số thứ tự thực tế là một số lớn 
 32-bit số, và nó là khác nhau.
- Số ACK là số thứ tự tương ứng cộng với 1.
- Máy tính của sẽ gửi phần thứ ba của bắt tay (ACK) và sau đó gửi dữ liệu ngay trong một gói tin khác. Có thể kết hợp các gói tin này,tuy nhiên chúng thường
 riêng biệt (do một hệ thống được kích hoạt bởi hệ điều hành và một bởi ứng dụng).
- Đối với phân đoạn Dữ liệu, số thứ tự và ACK ở lại với các giá trị trước đó. Số thứ tự sẽ tăng lên khi người gửi gửi nhiều dữ liệu hơn.
 Số ACK sẽ tăng lên khi người gửi nhận được nhiều dữ liệu hơn từ máy chủ từ xa.
- Ba gói tin nhận được và gửi khoảng 88ms xảy ra rất gần với nhau so với khoảng cách giữa gói đầu tiên và gói thứ hai. Đó là bởi vì chúng là 
 hoạt động tại địa phương; Không có sự chậm trễ mạng liên quan.
- RTT là 88ms theo dấu vết của chúng tôi. Nếu bạn sử dụng máy chủ web cục bộ, RTT sẽ rất nhỏ, có thể là vài mili giây. Nếu bạn sử dụng một máy chủ web 
lớn có thể được cung cấp bởi mạng lưới phân phối, RTT có thể sẽ là hàng chục mili giây. Nếu bạn sử dụng một máy chủ từ xa, RTT có thể sẽ là hàng trăm 
mili giây.

<aname="1.6"></a>
#### 1.6. Step 5: Connection Options:

Cũng như thiết lập một kết nối, các gói TCP SYN thương lượng các tham số giữa hai đầu sử dụng Options. Mỗi kết thúc mô tả các khả năng của nó, nếu có,
để đầu kia bằng cách bao gồm các tùy chọn thích hợp trên SYN của nó.

**Trả lời câu hỏi sau:**
- a. Những gì TCP options được thực hiện trên các gói SYN cho các gói bắt được của bạn?
Tùy chọn chung bao gồm *Maximum Segment Size (MSS)* để nói phía bên kia là phân đoạn lớn nhất có thể nhận được, và *Timestamps* để đưa thông tin về các phân đoạn 
để ước lượng thời gian đi lại. Ngoài ra còn có các Tùy chọn như *NOP (No-operation)* và *End of Option list*  mà phục vụ để định dạng các Tùy chọn nhưng không 
quảng cáo vể khả năng. Tùy chọn cũng có thể được thực hiện trên các phân đoạn thông thường sau khi kết nối được thiết lập khi chúng đóng vai trò truyền dữ liệu.
Điều này phụ thuộc vào options. Ví dụ: tùy chọn MSS không được thực hiện trên mỗi gói bởi vì nó không chuyển tải thông tin mới; Timestamps có thể được bao gồm 
trong mỗi gói để giữ một ước tính mới của RTT; Và các tùy chọn như *SACK(Selectated Acknowledgment)* chỉ được sử dụng khi dữ liệu được nhận không đúng thứ tự.

**Answers to Step 5: Connection Option**:
1. Tùy chọn TCP là  Maximum Segment Size, Window Scale, SACK permitted, và Timestamps. Mỗi lựa chọn này được sử dụng theo cả hai hướng. Ngoài ra còn có các lựa chọn định dạng NOP và End of Option List.

Đây là một ví dụ của một FIN teardown:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/9.png"></p>

Những điểm cần lưu ý:

- Sự teardown được khởi tạo bởi máy tính; Nó cũng có thể được khởi xướng bởi máy chủ.
- Giống như SYN, cờ FIN chiếm một số thứ tự. Vì vậy, khi số thứ tự của FIN là 192, số Ack tương ứng là 193.
- Số thứ tự của bạn sẽ thay đổi. Số của chúng ta là tương đối (như được tính bởi Wireshark) nhưng rõ ràng phụ thuộc vào tài nguyên được tìm nạp. 
 Bạn có thể nói rằng nó dài khoảng 1 MB.
- RTT trong trao đổi FIN tương tự như trong trao đổi SYN, RTT của bạn sẽ khác nhau tùy thuộc vào khoảng cách giữa máy tính và máy chủ như trước.


<a name="1.7"></a>
#### 1.7. Step 6: FIN/RST Teardown:


<a name="1.8"></a>
#### 1.8. Step 7: TCP Data Transfer:


<a name="2"></a>
### 2. UDP (User Datagram Protocol):

<a name="2.1"></a>
#### 2.1. Step 1: Capture a Trace:


<a name="2.2"></a>
#### 2.2. Step 2: Inspect the Trace:


<a name="2.3"></a>
#### 2.3. Step 3: UDP Message Structure:


<a name="2.4"></a>
#### 2.4. Step 4: UDP Usage:


<a name="3"></a>
### 3. Routing:

<a name="4"></a>
### 4. Tài liệu dịch:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Slide/Image/1.png"></p>
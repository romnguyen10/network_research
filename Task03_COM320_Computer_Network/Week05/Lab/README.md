## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **17/05/2017**

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

<a name="1.6"></a>
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

- Cuối cùng, kết nối TCP được lấy xuống sau khi quá trình tải xuống hoàn tất. Điều này thường được thực hiện với các phân đoạn FIN (Finalize).
Mỗi bên gửi FIN đến người kia và xác nhận FIN họ nhận được; Nó cũng tương tự như sự bắt tay ba bước. Ngoài ra, kết nối có thể bị teardown đột ngột 
khi một đầu gửi RST (reset). Gói tin này không cần phải được thừa nhận từ phía bên kia.

- Vẽ hình ảnh của teardown trong dấu vết của bạn, bắt đầu từ khi FIN đầu tiên hoặc RST được phát hành cho đến khi kết nối hoàn tất. 
Như trước, hiển thị chuỗi và số ACK trên mỗi phân đoạn. Nếu bạn có FINs sau đó sử dụng sự khác biệt thời gian để ước tính thời gian khứ hồi

**Answers to Step 6: FIN/RST Teardown**:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/10.png"></p>

Những điểm cần lưu ý:

- Sự teardown được khởi tạo bởi máy tính; Nó cũng có thể được khởi xướng bởi máy chủ.
- Sự phá vỡ là đột ngột - một RST đơn lẻ trong trường hợp này, và sau đó nó được đóng lại, mà đầu kia phải chứa.
- Các chuỗi và số Ack không thực sự quan trọng ở đây. Họ chỉ đơn giản là các giá trị (tương đối Wireshark) vào cuối kết nối.
- Do không có chuyến đi khứ hồi, không thể ước tính RTT.

<a name="1.8"></a>
#### 1.8. Step 7: TCP Data Transfer:

- Phần giữa của kết nối TCP là truyền dữ liệu, hoặc tải về, để có được một cảm giác tổng thể về nó, trước hết chúng ta sẽ xem tỷ lệ tải về theo thời gian.
- *Trong menu Thống kê, chọn một *IO Graph*. Theo mặc định, biểu đồ này cho thấy tỷ lệ gói tin theo thời gian*. Tinh chỉnh nó để hiển thị tốc độ tải xuống 
với những thay đổi được đưa ra dưới đây. Bạn có thể bị cám dỗ để sử dụng các công cụ *TCP Stream Graph* dưới menu Thống kê để thay thế. Tuy nhiên, những công cụ 
này không hữu ích vì chúng được giả sử các gói tin bắt được được lấy gần máy tính gửi dữ liệu; còn máy chúng tôi các gói tin bắt được được lấy gần máy tính nhận 
dữ liệu.
	- *Trên trục x, điều chỉnh khoảng đánh dấu và điểm cho mỗi lần đánh dấu*. Khoảng cách đánh dấu phải đủ nhỏ để nhìn vào đó mà theo dõi, và không quá nhỏ. 
	0,1 giây là một lựa chọn tốt cho các dấu vết thứ hai. Các điểm ảnh trên mỗi lần đánh dấu có thể được điều chỉnh để làm cho đồ thị 
	rộng hơn hoặc hẹp hơn để lấp đầy cửa sổ.
	- *Trên trục y, thay đổi đơn vị thành Bits/Tick. Mặc định là Packet/Tick*. Bằng cách thay đổi nó, chúng ta có thể dễ dàng thực hiện các bit/giây 
	throughput bằng cách lấy giá trị trục y và độ rộng thích hợp, ví dụ, 10X cho các dấu tick của 0,1 giây.
	- Thêm một biểu thức lọc để chỉ xem các gói tải xuống. Cho đến nay chúng tôi đang xem xét tất cả các gói. Giả sử việc tải xuống từ cổng máy chủ web 
	thông thường là 80, bạn có thể lọc cho nó bằng bộ lọc *tcp.srcport == 80*. Đừng quên nhấn Enter, và bạn có thể cần phải nhấp vào nút *Graph* để làm cho 
	nó hiển thị lại.Nhịp 0.1 giây.
	-  Để xem biểu đồ tương ứng cho lưu lượng tải lên, hãy nhập một bộ lọc thứ hai vào hộp tiếp theo. Một lần nữa giả sử cổng máy chủ web thông thường, 
	bộ lọc là *tcp.dstport == 80*. Sau khi bạn nhấn Enter và nhấp vào nút Graph, bạn sẽ có hai dòng trên biểu đồ.

- chúng ta có thể thấy tốc độ download mẫu nhanh chóng tăng từ 0 lên một tốc độ ổn định, với một bit của hàm mũ. Đây là khởi đầu chậm. Tỷ lệ tải xuống khi kết nối
đang chạy là khoảng 2,5 Mbps. Bạn có thể kiểm tra tỷ lệ ước tính của bạn với thông tin từ *wget/curl*. Tỷ lệ tải lên là một lưu lượng truy cập ACK nhỏ và ổn định. 
Tải xuống của chúng tôi cũng tiến triển khá đều đặn cho đến khi hoàn thành. Đây là lý tưởng, nhưng nhiều lượt tải xuống có thể hiển thị nhiều hành vi thay đổi hơn, 
ví dụ như băng thông có sẵn thay đổi do tải xuống, tỷ lệ tải xuống được đặt bởi máy chủ chứ không phải mạng hoặc đủ gói bị mất để làm gián đoạn chuyển. 
Bạn có thể nhấp vào biểu đồ được đưa đến điểm gần nhất trong dấu vết nếu có tính năng bạn muốn điều tra.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/11.png"></p>

Trả lời các câu hỏi sau để thể hiện sự hiểu biết của bạn về việc truyền dữ liệu:
- a. Tỷ lệ dữ liệu thô trong hướng tải về trong các packets/second và bits/second  là gì khi kết nối TCP hoạt động tốt?
- b. Tỉ lệ phần trăm tải xuống này là nội dung gì? Hiển thị tính toán của bạn. Để tìm hiểu, nhìn vào một gói tải xuống điển hình; Cần có nhiều gói tải xuống 
tương tự. Bạn có thể xem nó được bao lâu, và bao nhiêu byte của TCP tải chứa nó.
- c. Tỷ lệ dữ liệu thô trong hướng tải lên trong các packets/second va bits/second do các gói tin ACK là gì?
- d. Nếu phân đoạn TCP nhận được gần đây nhất từ máy chủ có một chuỗi số X, thì số ACK nào sẽ thực hiện đoạn TCP truyền tiếp theo?

Kiểm tra các gói dữ liệu trong phần tải xuống ở giữa các dấu vết của bạn cho các tính năng này:
- Bạn sẽ thấy một mẫu của các phân đoạn TCP nhận dữ liệu và ACK được gửi lại cho máy chủ. Thông thường sẽ có một ACK mỗi cặp gói dữ liệu. Các ACK này được gọi 
là ACK Trì hoãn. Bằng cách trì hoãn một thời gian ngắn, số lượng ACKs sẽ giảm đi một nửa.
- Vì đây là tệp tải xuống, số thứ tự của các phân đoạn nhận được sẽ tăng lên; Số ACK của các phân đoạn truyền sau đó sẽ tăng tương ứng.
- Vì đây là tệp tải xuống nên số thứ tự của các đoạn truyền sẽ không tăng lên (sau khi nhận được lần đầu). Do đó số ACK trên các phân đoạn nhận được sẽ không tăng.
- Mỗi đoạn mang thông tin Window để cho biết đầu còn lại bao nhiêu không gian vẫn còn trong bộ đệm. Cửa sổ phải lớn hơn không, hoặc kết nối sẽ bị trễ bởi 
điều khiển luồng.

Cũng như phân đoạn TCP thông thường mang dữ liệu, bạn có thể thấy nhiều tình huống khác. Bạn có thể sắp xếp các gói bắt được trên cột Thông tin và duyệt các 
gói tin kiểu **[TCP xxx ...**. Tùy thuộc vào tải xuống, bạn có thể thấy các ACKs trùng lặp, dữ liệu không hợp lệ, truyền lại, không cửa sổ, cập nhật cửa sổ 
và hơn thế nữa. Các phân đoạn này thường không phân biệt bởi cờ trong tiêu đề TCP, như các phân đoạn SYN hoặc FIN. Thay vào đó, chúng là tên cho các tình huống
có thể xảy ra và được xử lý trong suốt quá trình vận chuyển.

**Answers to Step 7: TCP Data Transfer**:
- a. Tốc độ của chúng tôi đo được là 250 gói/giây và 2,5 Mbps. Tỷ lệ của bạn sẽ khác nhau, nhưng có thể gói tin và tỷ lệ bit sẽ khác nhau theo một khoảng 10.000 
cho các gói có kích thước khoảng 1000 byte.
- b. Các gói tải xuống của chúng tôi dài là 1434 byte , trong đó có 1368 byte là nội dung tải của gói tin TCP. Vì vậy 95% nội dung tải xuống là nội dung. 
Số của bạn nên tương tự cao đối với các gói lớn khoảng 1 KB, vì tiêu đề TCP chỉ có 20-40 byte.
- c. Tốc độ của chúng tôi đo được là 120 gói/giây và 60.000 bit/giây. Tốc độ của bạn sẽ thay đổi nhưng chúng tôi mong đợi tỷ lệ gói ACK là khoảng một nửa tốc độ 
gói dữ liệu cho mẫu điển hình của một ACK bị trì hoãn cho mỗi gói dữ liệu nhận được. Tốc độ bit ACK sẽ ít nhất là một mức độ lớn hơn tốc độ bit dữ liệu vì 
các gói tin nhỏ hơn nhiều, khoảng 60 byte.
- d. Số Ack cho biết số thứ tự mong đợi tiếp theo. Do đó nó sẽ là X cộng với số lượng byte tải trọng TCP trong phân đoạn dữ liệu.

<a name="2"></a>
### 2. UDP (User Datagram Protocol):

<a name="2.1"></a>
#### 2.1. Step 1: Capture a Trace:

Có nhiều cách để máy tính của bạn gửi và nhận tin nhắn UDP vì UDP được sử dụng rộng rãi như một giao thức truyền tải. Các lựa chọn dễ nhất là:
- Đừng làm gì ngoài chờ đợi một lúc. UDP được sử dụng cho nhiều *"system protocol"* thường chạy ở chế độ nền và tạo ra một lượng nhỏ lưu lượng truy cập, 
ví dụ: DHCP dành cấp địa chỉ IP động  được chỉ định cho đồng bộ hóa NTPime td.
- Sử dụng trình duyệt của bạn để truy cập trang web. UDP được sử dụng bởi DNS sẽ giải quyết các tên miền cho địa chỉ IP, do đó, ghé thăm các trang web mới 
sẽ tạo ra lưu lượng truy cập DNS được gửi đi. Cẩn thận đừng đến các trang web không an toàn; Chọn các trang web hoặc trang web được đề xuất mà bạn biết nhưng 
chưa truy cập gần đây. Đơn giản chỉ cần duyệt web có thể tạo ra sự lưu thông ổn định của DNS.
- Bắt đầu cuộc gọi thoại qua IP với khách hàng yêu thích của bạn. UDP được sử dụng bởi RTP, là giao thức thường được sử dụng để truyền các mẫu phương tiện 
trong cuộc gọi thoại hoặc video qua Internet.

Tiến hành như sau để nắm bắt gói tin của giao thông UDP; Cách khác, bạn có thể sử dụng các thông tin được cung cấp:
- a. *Khởi động Wireshark và bắt đầu bắt gói với một bộ lọc là **udp***.
- b. *Khi bắt đầu bắt gói, thực hiện một số hoạt động sẽ tạo ra lưu lượng UDP*. Chúng tôi đã mô tả một số tùy chọn ở trên, 
ví dụ: duyệt web hoặc bắt đầu cuộc gọi VoIP ngắn.
- c. *Chờ khoảng 60 giây sau đó bạn hãy dừng hoạt động của mình để quan sát lưu lượng UDP*. Rất có thể bạn sẽ quan sát một luồng 
lưu lượng UDP bởi vì hoạt động của hệ thống thường sử dụng UDP để giao tiếp.
- d. Dừng bắt gói lại. Bây giờ bạn sẽ có một lưu lượng với nhiều gói UDP. Ví dụ được hiển thị bên dưới. Chúng ta đã chọn một gói tin và mở rộng chi tiết của tiêu đề UDP.
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/12.png"></p>

<a name="2.2"></a>
#### 2.2. Step 2: Inspect the Trace:

Các máy tính khác nhau có khả năng nắm bắt các loại lưu lượng UDP khác nhau tùy thuộc vào thiết lập mạng và hoạt động cục bộ. Lưu ý rằng cột của giao thức 
có khả năng hiển thị nhiều giao thức,hoặc không có UDP nào. Điều này là do giao thức được liệt kê là một giao thức thuộc lớp ứng dụng được đặt trên đầu của UDP. 
Wireshark cho biết tên của giao thứclớp  ứng dụng chứ không phải giao thức truyền tải(transport) UDP, trừ khi Wireshark không thể xác định được giao thức lớp ứng dụng. 
Tuy nhiên, ngay cả khi các gói được liệt kê như là một giao thức ứng dụng, chúng sẽ có một tiêu đề giao thức UDP cho chúng ta nghiên cứu, sau các tiêu đề 
giao thức IP và lớp dưới.

*Chọn các gói khác nhau trong lưu lượng gói bắt được (trong bảng điều khiển trên cùng) và duyệt phần mở rộng UDP header (trong bảng điều khiển giữa)*. 
Bạn sẽ thấy nó chứa các trường sau
- a. **Source port**, port mà thông điệp UDP được gửi đi. Nó được đưa ra là 1 số và có thể là một tên văn bản; Tên được gán cho các giá trị cổng được đăng ký 
để sử dụng với một ứng dụng cụ thể.
- b. **Destination port**. Đây là số cổng và có thể là tên của thông điệp UDP . port là hình thức duy nhất của địa chỉ trong UDP. Có máy tính được xác định bằng cách 
sử dụng địa chỉ IP trong lớp IP thấp hơn.
- c. **Length**. Chiều dài của gói UDP
- d. **Checksum**. Tổng kiểm tra messenger được sử dụng để xác nhận nội dung của nó.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/13.png"></p>

UDP header có các giá trị khác nhau cho các tin nhắn khác nhau, nhưng như bạn thấy, nó ngắn và gọn. Phần còn lại của thông báo là tải trọng UDP 
thường được xác định là giao thức lớp cao hơn nó mang, ví dụ: DNS hoặc RTP.
<a name="2.3"></a>
#### 2.3. Step 3: UDP Message Structure:

Để kiểm tra sự hiểu biết của bạn về UDP, bạn có thể phác hoạ một cấu trúc gói UDP như bạn đã quan sát. Nó sẽ hiển thị vị trí của tiêu đề IP, phần đầu UDP 
và tải trọng UDP. Trong tiêu đề UDP, hiển thị vị trí và kích thước của từng trường UDP mà bạn có thể quan sát bằng Wireshark. Con số của bạn chỉ đơn giản 
có thể hiển thị thông báo dưới dạng một hình chữ nhật dài, mỏng.

Bằng cách nhìn vào các chi tiết của các tin nhắn UDP trong lưu lượng gói tin mà bạn đã bắt được, hãy trả lời những câu hỏi sau:
- 1. Trường Lenght bao gồm những gì? payload UDP, UDP payload và UDP header, hoặcd UDP payloa, UDP header và header lớp thấp hơn?
- 2. Số bits chiếm trong UDP checksum ?
- 3. Số  byte chiếm trong toàn bộ UDP header?

**Solutions – Step 3 UDP Message Structure**:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/14.png"></p>

Sơ đồ này cho thấy các trường UDP header giống như trong sách nhưng có định dạng hơi khác và với độ dài cho bằng byte chứ không phải các bit. 
Nó cũng cho thấy mối quan hệ của  IP header và UDP payload đến UDP header.
 
Câu trả lời cho các câu hỏi là:
- 1. Trường Lenght cung cấp chiều dài của UDP payload cộng với UDP header.
- 2. Checksum là 16 bit.
- 3. UDP header dài 8 byte.

<a name="2.4"></a>
#### 2.4. Step 4: UDP Usage:

Để hoàn thành sự hiểu biết của chúng ta về UDP, chúng ta sẽ xem UDP được sử dụng trong thực tế như thế nào khi vận chuyển bằng các ứng dụng. 
Bắt đầu với IP, lớp giao thức tiếp theo thấp hơn, có một số vấn đề chúng ta có thể xem xét. vấn đề đầu tiên là làm thế nào IP biết rằng lớp giao thức 
cao hơn kế tiếp là UDP. Câu trả lời là có một trường Giao thức trong tiêu đề IP có chứa thông tin này.
- 1. *Cung cấp giá trị của trường IP protocol xác định giao thức lớp trên là UDP*.

Một vấn đề thứ hai là làm thế nào thông điệp UDP thường được giải quyết tại lớp IP. Bạn có thể ngạc nhiên khi tìm thấy các tin nhắn UDP trong lưu lượng các gói
mà bạn bắt được mà không phải từ máy tính của bạn hoặc chỉ được gửi đến máy tính của bạn. Bạn có thể thấy điều này bằng cách sắp xếp trên các cột Nguồn và đích đến. 
Nguồn và đích đến sẽ là tên miền, nếu độ phân giải tên lớp mạng được bật, và nếu không địa chỉ IP. (Bạn có thể chuyển đổi cài đặt này bằng cách sử dụng 
*menu View* và chọn *Resolution name*) Bạn có thể tìm ra địa chỉ IP của máy tính của bạn bằng cách sử dụng lệnh **ipconfig** (Windows).

Lý do bạn có thể tìm thấy thư UDP mà không có địa chỉ IP của máy tính như là địa chỉ IP nguồn hoặc đích là UDP được sử dụng rộng rãi như là một phần của các 
giao thức hệ thống. Các giao thức này thường gửi tin nhắn đến tất cả các máy tính địa phương quan tâm đến chúng bằng cách sử dụng địa chỉ broadcast và multicast. 
Tong lưu lượng các gói chúng ta bắt được, DNS (domain name system), MDNS (multicast domain name system), NTP (để đồng bộ hóa thời gian), 
NBNS (lưu lượng NetBIOS), DHCP (cấp IP động), SSDP (phát hiện dịch vụ ), STUN (một giao thức đi qua NAT), RTP (để tải các mẫu âm thanh và video), 
và nhiều hơn nữa. Lưu lượng  của bạn có thể có các giao thức khác mà bạn chưa nghe ; Nó là chính xác, vì có rất nhiều giao thức trên mạng. Bạn có thể xem chúng trên web 
để biết nhiều hơn.

- 2. *Kiểm tra các tin nhắn UDP và cung cấp địa chỉ IP đích  được sử dụng khi máy tính của bạn không phải là địa chỉ IP nguồn hay địa chỉ IP đích*. (Nếu bạn chỉ có 
	máy tính của bạn là địa chỉ IP nguồn hoặc đích, sau đó bạn có thể sử dụng thông tin được cung cấp.)

Cuối cùng, chúng ta hãy nhìn vào độ dài của các gói UDP điển hình. Chúng ta biết rằng thông điệp UDP có thể lớn đến 64K bytes. Nhưng khi bạn duyệt, 
bạn sẽ thấy rằng hầu hết các tin nhắn UDP ngắn hơn nhiều so với tối đa này, do 
- 3. Kích thước điển hình của các tin nhắn UDP trong lưu lượng của bạn là gì?

**Solutions to Step 4: UDP Usage**:

Câu trả lời cho các câu hỏi là:
- 1. Giá trị trường IP protocol là 17 cho biết UDP.
- 2. Có thể tìm thấy nhiều địa chỉ broadcast và multicast. Chúng bao gồm địa chỉ broadcast Internet 255.255.255.255, địa chỉ broadcast subnet như 
192.168.255.255 (nơi phần 192.168 là số subnet và phần .255.255 nghĩa là broadcast), và các địa chỉ IP multicast như 224.0.xx.xx 
(như vậy Như là 224.0.0.251 cho DNS multicast).
- 3. Câu trả lời này sẽ thay đổi lưu lương theo dõi của bạn. Thường thì chúng là một vài trăm byte hoặc ít hơn, và thường có thể khoảng 100 byte. 
Đó là, nhiều tin nhắn là những gói tin tương đối ngắn.

<a name="3"></a>
### 3. Routing:

Ở đây, bạn sử dụng lệnh route để xem và thay đổi bảng định tuyến nội bộ máy tính của bạn. Mặc dù máy tính của bạn không phải là bộ định tuyến, 
nó vẫn duy trì một bảng định tuyến internet với các mục cho mạng giao diện mạng, mạng loopback, và các chi tiết của các mạng nội bộ khác.
- 1. Mở command prompt bằng cách gõ lệnh `cmd` trong hộp run.
- 2. Để xem bảng định tuyến của bạn, gõ `route print | more` và nhấn `Enter`. The | more sau khi lệnh *the route print* in kết quả đầu ra sẽ được 
hiển thị một màn hình cùng một lúc.
- 3. Tiếp theo, kiểm tra đầu ra  của *the route print *. Giao diện mạng máy tính của bạn được liệt kê ở trên cùng, và Bảng Tuyến đường IPv4 
liệt kê các mục trong bảng định tuyến, trong đó có năm cột:

	- **Network Destination** - Network Destination máy tính của bạn so sánh với địa chỉ IP đích của các gói tin gửi đi để xác định nơi gửi chúng.
	- **Netmask** - The subnet mask của đích mạng. Giá trị 255.255.255.255 chỉ ra rằng địa chỉ trong cột network destination là một địa chỉ IP cụ thể thay 
	vì địa chỉ mạng; Nó được gọi là *host route*. Một giá trị 0.0.0.0 được sử dụng khi network destination là 0.0.0.0, cho biết tuyến đường mặc định hoặc gateway.
	- **Gateway** - Địa chỉ hop kế tiếp hoặc liên kết trực tiếp, có nghĩa là mạng được kết nối trực tiếp tới một giao diện. Ghi lại giá trị trong 
	network destination 0.0.0.0.
	- **Interface** - Địa chỉ giao diện Windows sử dụng để gửi gói tin đến network destination.
	- **Metric** - the metric được gán cho route. Nếu có hai mục cho network destination, số liệu nào *thấp hơn* là tuyến được chọn.

Nhấn phím cách một hoặc nhiều lần để hiển thị phần còn lại của đầu ra. Bạn sẽ thấy một hàng đầu ra có gắn nhãn Persistent Routes. Nếu bạn tạo ra một 
tuyến đường thủ công và nó là để ở lại trong bảng giữa khởi động lại, nó được liệt kê ở đây. Bạn cũng sẽ thấy tuyến đường mặc định được liệt kê dưới 
Persistent Routes trong phần IPv4 của đầu ra.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/15.png"></p>

- 4. Để xác minh rằng bạn có thể giao tiếp với Internet, gõ `ping scisweb.ulster.ac.uk` nhấn `Enter`. Nếu ping thành công, mạng mặc định của bạn đang 
hoạt động đúng. Bạn sẽ thấy kết quả sau cho lệnh ping của bạn.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/16.png"></p>

- 5. Nhập `route delete 0.0.0.0` và nhấn `Enter` để xóa tuyến đường mặc định của bạn. Cố gắng `ping scisweb.ulster.ac.uk` một lần nữa. 
Ping sẽ không thành công (hoặc sẽ sử dụng địa chỉ IP khác với địa chỉ IP scisweb.ulster.ac.uk địa phương)
Để xem các tuyến đường đã hết, hãy vào trình duyệt của bạn và bạn sẽ thấy rằng bạn đã bị `hỏng` Kết nối Internet của bạn. Tiếp theo, trở lại *Command Prompt* 
và Type `route print | more` và nhấn `Enter` Bạn sẽ thấy rằng các điểm đến mạng 0.0.0.0 không còn trong bảng. Nhấn *spacebar* nhiều lần để hiển thị phần 
còn lại của Đầu ra.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/17.png"></p>

- 6. Để tạo mục nhập tuyến đường mặc định và khôi phục lại bảng định tuyến của bạn, gõ `route add -p 0.0.0.0 mask 0.0.0.0 default gateway` và nhấn `enter` 
(thay thế gateway mặc định bằng địa chỉ bạn đã lưu ý trong Bước 3). ví dụ. `Route add -p 0.0.0.0 mask 0.0.0.0 193.61.191.201` (như được hiển thị bên dưới):
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week05/Lab/Image/18.png"></p>

<a name="4"></a>
### 4. Tài liệu dịch:

[1] Lab Week05 TCP, UDP, Routing: http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm 
 



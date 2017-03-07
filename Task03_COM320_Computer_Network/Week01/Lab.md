## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **06/03/2017**

### Mục lục
[I. Protocol layer](#p1)

- [1. Mục tiêu](#muctieu)

- [2. Yêu cẩu](#yeucau)

	- [2.1 Wireshark](#wireshark)
	- [2.2 Wireshark & Packet Sniffing Backgroun](#sniffs)
	- [2.3 Step 1: Capture a Trace](#thaotac)
	- [2.4 Giao diện chính của Wireshark](#giaodien)
	- [2.5 Filtering Traffic](#traffic)
	- [2.6. Step 2: Inspect the Trace](#step2)
	- [2.7. Step 3: Inspect the Trace Again](#step3)
	- [2.8. Packet Structure](#structure)
	- [2.9. Step 5: Demultiplexing Keys](#step5)
	
[II.Command Line Tools](#p2)

[III. Tài liệu dịch](#tailieu)

<a name="p1"></a>
### I. Protocol layer

<a name="muctieu"></a>
#### 1. Mục tiêu 
Để tìm hiểu cách thức và lớp được biểu diễn trong các gói tin. Nó là những khái niệm quan trọng cho cơ cấu mạng được nêu trong các văn bản.
Các dấu vết cho các bài Lab này là ở đây:
 http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-protocol-layers.pcap
(Mặc dù các dấu vết chính bạn sẽ nhìn vào từ một trang web bạn chọn như www.ulster.ac.uk trong các ví dụ để làm theo).

<a name="yeucau"></a>
#### 2. Yêu cầu

<a name="wireshark"></a>
##### 2.1. Wireshark:

Bài Lab này sử dụng các công cụ phần mềm Wireshark để bắt và kiểm tra tìm các gói tin. Một dấu vết gói được ghi lại khi lưu thông ở một vị trí trên mạng, như được chụp ảnh chụp của tất cả các bit truyền trên một dây đặc biệt. Các dấu vết gói ghi dấu thời gian cho mỗi gói tin, cùng với các bit tạo nên các gói tin, từ các tiêu đề lớp thấp đến các nội dung lớp cao. 

Wireshark chạy trên hầu hết các hệ điều hành, bao gồm cả Windows, Mac và Linux. Nó cung cấp một giao diện người dùng đồ họa mà ta thấy trình tự của gói tin và ý nghĩa của các bit khi được giải thích tiêu đề giao thức và dữ liệu. Nó mã hóa các gói tin theo kiểu của nó, và có nhiều cách khác nhau để lọc và phân tích các gói tin để cho bạn điều tra hành vi của các giao thức mạng.

Wireshark được sử dụng rộng rãi để khắc phục sự cố mạng. Bạn có thể tải về từ www.wireshark.org cho máy tính cá nhân của bạn. Đây là một lý tưởng để phân tích dữ liệu  cho các Lab của chúng tôi - ổn định, có một cơ sở người dùng lớn và hỗ trợ cũng như các tài liệu bao gồm một người sử dụng hướng dẫn http://www.wireshark.org/docs/wsug_html_chunked), và một FAQ chi tiết, chức năng phong phú bao gồm các khả năng để phân tích hàng trăm giao thức, và một giao diện người dùng được thiết kế tốt. Nó hoạt động trong máy tính sử dụng Ethernet, nối tiếp (PPP và SLIP), 802,11 mạng LAN không dây, và nhiều công nghệ kết nối các lớp khác (nếu hệ điều hành mà nó đang chạy Wireshark cho phép làm như vậy). Nó đã được cài đặt trong các bài Lab.

Một sự giúp đỡ hướng dẫn nhanh chóng để lọc hiển thị Wireshark là ở đây: http://openmaniak.com/wireshark_filters.php



Wireshark là một công cụ cốt lõi đối với bất kỳ 'người đàn ông ở giữa' không dây hoặc tấn công snooping. Nó đơn giản là không thể thiếu cho những ai muốn kiểm tra các gói dữ liệu được chuyển qua mạng - tốt hay xấu ...

##### 2.2. Wireshark & Packet Sniffing Backgroun:
Các công cụ cơ bản để quan sát các thông điệp trao đổi giữa các đơn vị thực hiện giao thức được gọi là một gói sniffer.Theo như tên cho thấy, một ảnh chụp gói sniffer ( "sniffs") thông điệp được gửi /  được nhận từ / bởi máy tính của bạn; nó cũng sẽ thường lưu trữ và / hoặc hiển thị các nội dung của các giao thức khác nhau trong các thư  khi bị bắt. Một gói sniffer là thụ động. Nó quan sát các thông điệp được gửi và nhận bởi các ứng dụng và các giao thức chạy trên máy tính của bạn, nhưng không bao giờ gửi các gói dữ liệu riêng của mình. Tương tự như vậy, nhận được gói tin không bao giờ gửi rõ ràng địa chỉ đến các gói sniffer.Thay vào đó, một gói sniffer nhận được một bản sao của gói tin được gửi / nhận được từ / bởi ứng dụng và các giao thức thực hiện trên máy tính của bạn. 

Hình 1 cho thấy cấu trúc của một gói sniffer. Ở bên phải của Hình 1 là các giao thức (trong trường hợp này, là giao thức Internet) và các ứng dụng (chẳng hạn như một trình duyệt web hoặc FTP) mà thường chạy trên máy tính của bạn. Các gói sniffer, thể hiện trong hình chữ nhật nét đứt trong hình 1 là một sự bổ sung cho các phần mềm thông thường trong máy tính của bạn, và bao gồm hai phần. Các thư viện bắt gói dữ liệu nhận được một bản sao của mỗi khung link-layer được gửi từ hoặc được nhận bởi máy tính của bạn. Tin nhắn trao đổi giữa các giao thức lớp cao hơn như HTTP, FTP, TCP, UDP, DNS, hoặc IP tất cả cuối cùng đều được gói gọn trong khung link-layer được truyền qua phương tiện vật lý như một cáp Ethernet.

![](http://i.imgur.com/2OzVb7p.png)

Hợp phần thứ hai của một gói sniffer là phân tích dữ liệu, hiển thị các nội dung của tất cả các lĩnh vực trong một thông điệp giao thức. Để làm như vậy, gói tin phân tích  phải "hiểu" cấu trúc của tất cả các thư trao đổi của giao thức. Ví dụ, giả sử chúng ta quan tâm việc hiển thị các lĩnh vực khác nhau trong các gói tin trao đổi giữa các giao thức HTTP trong Hình 1. Các gói phân tích hiểu định dạng của khung Ethernet, và do đó có thể xác định các gói tin IP trong khung Ethernet. Nó cũng hiểu định dạng gói tin IP, để nó có thể xuất các phân đoạn TCP trong gói tin IP. Cuối cùng, nó hiểu được cấu trúc phân đoạn TCP, vì vậy nó có thể xuất các thông điệp HTTP chứa trong phân khúc TCP. Cuối cùng, nó hiểu các giao thức HTTP và như vậy, ví dụ,nó biết rằng các byte đầu tiên của thông điệp HTTP sẽ chứa chuỗi "GET", "POST", hoặc "HEAD".

<a name="sniffs"></a>
##### 2.3. Step 1: Capture a Trace 

- 1. **Launching Wireshark:**
Bạn có thể gõ Wireshark trong hộp chạy của chính màn hình khởi động Windows 8. Nhấn phím Windows trên bàn phím và gõ "Wireshark". Nếu sự cố khi chạy nó sau đó bạn có thể làm như sau:

![](http://i.imgur.com/nDiF5vv.png)

 *Nó tải về nhưng có thể gặp vấn đề với cấu hình bài lab mới cho Wireshark và trình điều khiển NPF. Vì vậy nếu điều này không làm việc .... sau đó hãy làm các bước tiếp theo. Khởi động Wireshark như sau. Nhấn vào biểu tượng máy tính để bàn trên cửa sổ màn hình chính & sử dụng các tập tin để duyệt đến C:\ Program Files\Wireshark. Cuối cùng, RIGHT CLICK vào Wireshark là "Run as administrator".*

- 2. Chỉ cần đóng hộp thoại sẽ nhắc bạn cài đặt một phiên bản mới. Sau đó bạn sẽ thấy một màn hình khởi động, như hiển thị bên cạnh.
 
 ![](http://i.imgur.com/OnV1L2c.png)
 
- 3. Hãy xem ở phía bên tay trái của màn hình - bạn sẽ thấy một danh sách "Giao diện". Đây là danh sách các giao diện mạng trên máy tính của bạn. Chọn Ethernet.

![](http://i.imgur.com/GLBZyLr.png)

- 4. Tiếp theo, nhấp vào Start.
- 5. Wireshark sẽ nắm bắt được tất cả các gói giao diện này. Nhấp chuột vào card mạng trên máy cụ thể bạn đang làm việc trên. Trong ví dụ trên, nó là điều khiển Ethernet để bắt đầu chụp gói (tức là, cho Wireshark để bắt đầu chụp tất cả các gói được gửi đến / từ giao diện đó), một màn hình như hình dưới đây sẽ được hiển thị, hiển thị thông tin về các gói tin bị bắt . Một khi bạn bắt đầu bắt gói dữ liệu, bạn có thể ngăn chặn nó bằng cách sử dụng Capture menu sổ xuống và chọn Stop.

*Chúng tôi muốn dấu vết này để nhìn vào cấu trúc giao thức của gói tin. Một Web đơn giản lấy một URL từ một máy chủ của sự lựa chọn của bạn để máy tính của bạn, đó là khách hàng, cũng có thể phục vụ như lưu thông.*

- 6. Mở trình duyệt của bạn, ví dụ Chrome và chọn một URL và lấy nó ví dụ http://www.ulster.ac.uk ".

- 7. Đóng các tab trình duyệt không cần thiết và cửa sổ. Bằng cách giảm thiểu hoạt động trình duyệt, bạn sẽ ngăn chặn máy tính của bạn từ lấy nội dung web không cần thiết, và tránh giao thông khác nhau trong các dấu vết.
- 8. Bây giờ quay trở lại Wireshark và bạn sẽ thấy một màn hình tương tự như dưới đây.

![](http://i.imgur.com/lb8qsS2.png)

Đó là tất cả cho bây giờ. Tiếp theo, bạn sẽ đọc thêm một chút về Wireshark và các gói tin truy tìm.

<a name="giaodien"></a>
##### 2.4. Giao diện chính của Wireshark:

Giao diện Wireshark có năm thành phần chính:
![](http://i.imgur.com/DbMICy5.png)

- Các menu lệnh là tiêu chuẩn kéo xuống menu nằm ở trên cùng của cửa sổ. Các menu File cho phép bạn lưu dữ liệu gói bắt hoặc mở một tập tin chứa dữ liệu gói chụp được trước đó. Các menu Capture cho phép bạn bắt đầu bắt gói dữ liệu.
- Cửa sổ  danh sách gói hiển thị tóm tắt thành một dòng cho mỗi gói tin bị bắt được, trong đó có số lượng gói tin (bởi Wireshark được giao; điều này một số gói tin không được  chứa trong phần đầu của bất cứ giao thức), thời gian mà tại đó các gói tin đã bị bắt, các gói tin có địa chỉ nguồn và địa chỉ đích, các loại giao thức, và các thông tin giao thức cụ thể chứa trong gói tin. Việc niêm yết gói tin có thể được sắp xếp theo bất kỳ bằng cách nhấp vào một tên cột. Các trường liệt kê các giao thức cấp độ cao nhất đã gửi hoặc nhận được gói tin này, nghĩa là các giao thức đó là nguồn hoặc chìm cuối cùng cho tài liệu này.
- Cửa sổ chi tiết gói tin tiêu đề cung cấp thông tin chi tiết về các gói tin được lựa chọn (đánh dấu) trong cửa sổ gói niêm yết. (Để chọn một gói tin trong cửa sổ gói niêm yết, đặt con trỏ trên bản tóm tắt một dòng của gói tin trong cửa sổ gói danh sách và nhấp chuột trái.). Những chi tiết này bao gồm thông tin về các khung Ethernet (giả sử các gói đã được gửi / nhận qua một giao diện Ethernet) và IP datagram có chứa gói tin này. Lượng Ethernet và chi tiết lớp IP hiển thị có thể được mở rộng hoặc giảm thiểu bằng cách nhấp vào hộp cộng-trừ bên trái của khung Ethernet hoặc dòng của gói tin IP trong cửa sổ chi tiết gói.
- Cửa sổ  nội dung gói hiển thị toàn bộ nội dung của khung bị bắt, trong cả hai ASCII và định dạng hệ thập lục phân. Phía trên cùng của giao diện người dùng đồ họa Wireshark, là khu vực lọc hiển thị gói, vào đó là một tên giao thức hoặc các thông tin khác có thể được nhập vào để lọc các thông tin hiển thị trong cửa sổ gói niêm yết.

<a name="traffic"></a>
##### 2.5. Filtering Traffic:

Bây giờ quaylại với Wireshark của bạn để bắt đầu. Chúng tôi sẽ xem xét để xem làm thế nào chúng ta có thể tách các trang web đang lưu thông từ các gói giao thức khác.
- 9. Bạn có hai lựa chọn. Bạn có thể chỉ cần gõ "tcp.port == 80" trong hộp lọc chính trên màn hình chính như dưới đây: 

![](http://i.imgur.com/OFGAqJY.png)
- 
10. Thay vì các phương pháp trên, bạn có thể lọc bằng cách gõ "port 80" trong bộ lọc như dưới đây. Bộ lọc này sẽ chỉ ghi lại  lưu lượng web tiêu chuẩn và không có các loại khác của các gói tin mà máy tính của bạn có thể gửi. Việc kiểm tra sẽ dịch các địa chỉ của máy tính gửi và nhận các gói tin dựa vào tên, sẽ giúp bạn nhận ra cho dù các gói tin sẽ đến hoặc từ máy tính của bạn. cửa sổ chụp của bạn sẽ tương tự như hình trong ảnh chụp màn hình tiếp theo.

![](http://i.imgur.com/qToeudw.png)

- 11. Khi  bắt đầu chụp, hãy truy cập một trang web sử dụng http (not https). Lần này, các gói tin sẽ được ghi lại bởi Wireshark đó là nội dung được chuyển. Hãy thử lại lần nữa, http://www.ulster.ac.uk trong trình duyệt của bạn.
- 
- 12. Sau khi bắt được thành công, trở lại Wireshark và sử dụng các menu hoặc nút để ngăn việc tìm kiếm lại . Nếu bạn đã thành công, cửa sổ Wireshark trên sẽ hiển thị nhiều gói tin, và có khả năng nó sẽ được đầy đủ. Nhiều gói dữ liệu được thu thập tùy thuộc vào kích thước của trang web, nhưng có ít nhất 8 gói trong các mục tìm thấy, và thường 20-100, và rất nhiều gói tin có màu xanh lá cây. Tôi khuyên bạn nên ngừng việc ghi nhận lại bằng cách nhấn vào nút đỏ Stop trên giao diện, như thế sẽ làm cho bạn dễ dàng hơn để di chuyển trở lại bắt đầu tìm "200 OK" gói. Một ví dụ đã được biểu diễn ở dưới. Xin chúc mừng, bạn đã bắt được gói cần tìm !

![](http://i.imgur.com/95ha9lr.png)


<a name="step2"></a>
##### 2.6. Step 2: Inspect the Trace:

- Chọn một gói tin mà cột Protocol là "HTTP" và cột thông tin nói rằng đó là GET. Đây là gói  web (HTTP) yêu cầu được gửi từ máy tính của bạn đến server. (Bạn có thể nhấp vào tiêu đề cột để sắp xếp theo giá trị đó, mặc dù không phải là khó khăn để tìm một gói tin HTTP bằng cách kiểm tra.) Chúng ta hãy nhìn gần hơn để xem cấu trúc gói tin phản ánh các giao thức được sử dụng. Vì chúng tôi lấy một trang web, chúng ta biết rằng các lớp giao thức được sử dụng như hiển thị dưới đây. Đó là, HTTP là giao thức lớp ứng dụng web sử dụng để lấy URL. Giống như nhiều ứng dụng Internet, nó chạy trên tầng transport va network của giao thức TCP/IP. Data link va physical phụ thuộc vào mạng của bạn nhưng thường được kết hợp trong các hình thức của Ethernet (hiển thị) nếu máy tính của bạn là có dây, hoặc 802.11 (không hiển thị) nếu máy tính của bạn là không dây.

![Imgur](http://i.imgur.com/NZYJiy5.png)

- Với các gói tin HTTP GET đã chọn, hãy nhìn kỹ để thấy những điểm tương đồng và khác biệt giữa nó và chồng giao thức của chúng tôi được mô tả tiếp theo. Các khối giao thức được liệt kê trong bảng điều khiển. Bạn có thể mở rộng mỗi khối (bằng cách nhấp vào dấu "+" giãn nở hoặc là các biểu tượng) để xem chi tiết về nó.

	-  Khối Wireshark đầu tiên là "Frame". Đây không phải là một giao thức, nó là một record  mô tả thông tin tổng thể về các gói tin, kể cả khi nó đã bị bắt và bit của nó rất dài.
	-  Khối thứ hai là "Ethernet". Lưu ý rằng bạn có thể có tìm thấy trên máy tính sử dụng 802.11 nhưng vẫn thấy một khối Ethernet thay vì một khối 802.11. Tại sao? Nó xảy ra bởi vì chúng tôi dùng Wireshark để bắt lưu lượng ở định dạng Ethernet vào các tùy chọn bắt gói, do đó nó được chuyển đổi thực 802,11 tiêu đề thành một tiêu đề giả Ethernet.
	-  Sau đó đến IP, TCP, HTTP, như chúng ta muốn. Lưu ý rằng thứ tự từ dưới cùng của giao thức sắp xếp lên trên. Điều này là bởi vì như các gói tin được truyền xuống theo thứ tự, thông tin tiêu đề của giao thức lớp thấp hơn được thêm vào phía trước của các thông tin của các giao thức lớp cao hơn, như trong hình. 1-15 . Đó là, các giao thức lớp thấp đi đầu tiên trong gói "trên đường truyền".

<a name="step3"></a>
##### 2.7. Step 3: Inspect the Trace Again:

- Bây giờ tìm thấy một gói tin HTTP, phản hồi từ máy chủ đến máy tính của bạn,nhìn vào cấu trúc của gói tin này thay sự khác biệt so với các gói tin HTTP GET. Gói này cần phải có "200 OK" trong thong tin, hiển thị khi tải thành công. Chúng tôi phát hiện, có hai khối phụ ở mặt chi tiết như đã thấy trong hình tiếp theo.

	- Khối phụ đầu tiên nói điều gì đó như “[... reassembled TCP segments …]”. Chi tiết trong khi chụp của bạn sẽ thay đổi, nhưng khối này được mô tả hơn các gói chính nó. Nhiều khả năng, phản ứng web đã được gửi qua mạng giống như là một loạt các gói tin đã được xếp lại với nhau sau khi họ đến máy tính. Cácgói HTTP dán nhãn là gói cuối cùng trong phản ứng web, và các gói block được nối lại với nhau để có được những phản ứng web hoàn chỉnh. Mỗi một gói tin được hiển thị như là có giao thức TCP mặc dù các gói mang theo là một phần của một phản ứng HTTP. Chỉ có các gói tin cuối cùng được hiển thị như là có giao thức HTTP khi thông điệp HTTP hoàn toàn có thể hiểu được, và nó sẽ liệt kê các gói tin được nối lại với nhau để cho các phản ứng HTTP.
	- Khối phụ thứ hai nói “Line-based text data …". Chi tiết trong chụp của bạn sẽ thay đổi, nhưng khối này mô tả nội dung của trang web đó là fetched. Trong trường hợp của chúng tôi nói nó là loại văn bản / html, mặc dù nó có thể dễ dàng hiểu được text / xml, image / jpeg, hoặc nhiều loại khác. Như với Frame, đây không phải là một giao thức thật sự. Thay vào đó, nó là một mô tả về nội dung gói tin Wireshark được tạo ra để giúp chúng tôi hiểu các lưu lượng mạng.

![Imgur](http://i.imgur.com/Aet3wZn.png)

- 1. Xác định vị trí các gói tin HTTP GET trong đó có "200 OK (text / html)" trong info feild, biểu thị đã tải thành công. Xem ví dụ dưới đây ở dòng thứ ba có màu trắng.

![Imgur](http://i.imgur.com/96FqKvW.png)

- 2. Di chuyển xuống ở phần giữa để **[+] Line-based text data: text/html**  và click chuột phải bằng con chuột của bạn. (Xem ở trên)

- 3. Từ menu đang xuất hiện, chọn **Copy --> Bytes --> Printable Text Only**  Bạn sẽ thấy một cửa sổ tương tự như cửa sổ popup dưới đây.

![Imgur](http://i.imgur.com/ANM0vm1.png)

- 4. Bản sao này là tất cả các mã cho trang chủ Ulster.

- 5. Mở một trình soạn thảo văn bản như Notepad ++ và dán mã HTML này vào một tài liệu mới. Save as **UlsterHomePage.html** trong một thư mục như W: downloads. Tiếp theo mở lên tìm hiểu và di chuyển đến nơi bạn đã lưu file và mở nó trong trình duyệt mặc định bằng cách nhấp vào nó.

- 6. Lưu ý có bao nhiêu trang chủ Ulster thực sự được gửi qua dây đến máy tính của bạn.

<a name="structure"></a>
##### 2.8. Packet Structure ( cấu trúc gói):

- Kiểm tra một gói GET HTTP cho thấy vị trí và kích thước  byte của TCP, IP và các tiêu đề giao thức Ethernet. Lưu ý khoảng cách Ethernet Header và payload Ethernet IP qua Ethernet để gửi qua mạng. Cũng Lưu ý phạm vi của tiêu đề IP và payload IP.
- Để làm việc với kích cỡ, quan sát rằng khi bạn click vào một khối giao thức trong bảng điều khiển (khối chính nó, không phải là "+" giãn nở) thì Wireshark sẽ làm nổi bật các byte tương ứng với nó trong các gói dữ liệu trong bảng dưới và hiển thị chiều dài ở dưới cùng của cửa sổ. Ví dụ, nhấp vào IP phiên bản 4 tiêu đề của một gói tin trong trace của chúng tôi cho chúng ta thấy rằng chiều dài là 20 byte. (Dấu vết của bạn sẽ khác nhau nếu nó là IPv6, và có thể khác nhau ngay cả với IPv4 tùy thuộc vào tùy chọn khác nhau.) Bạn cũng có thể sử dụng các gói kích thước tổng thể, thể hiện trong khối chi tiết cột, chiều dài hoặc Frame

![Imgur](http://i.imgur.com/VATkgz1.png)


![Imgur](http://i.imgur.com/Weil1HC.png)

- Có một số tính năng cần lưu ý:
	- Thứ tự của các header (Ethernet, IP, TCP, HTTP) là giao thức xếp từ dưới lên trên, vì các lớp thấp hơn là ngoài cùng trong gói tin khi nó di chuyển qua mạng.
	- Học sinh quan sát sẽ lưu ý một số khác biệt giữa các kích thước Ethernet header trong Wireshark và trong file text sẽ được nghiên cứu trong phòng thí nghiệm sau đó.
	- Kích thước của header IP và TCP là bình thường vào khoảng 20 byte, nhưng nó có thể lớn hơn trong một số trường hợp tùy thuộc vào hệ điều hành, ví dụ, IPv6 thay cho IPv4 và các lĩnh vực TCP header tùy chọn có thể tăng gấp đôi những con số này.
	- Kích thước của HTTP sẽ khác nhau tùy thuộc vào công cụ và URL gì được sử dụng để gửi các yêu cầu web. Đối với wget / curl, nó có khả năng là khoảng 100-300 byte.
	- Payload Ethernet bao gồm tất cả mọi thứ vượt ra ngoài  Ethernet header. Đó là, Ethernet không hiểu cấu trúc IP / TCP / HTTP ; nó đến lớp cao hơn để xác định header và ranh giới thông tin.
	- Tương tự như vậy, các Payload IP bao gồm tất cả mọi thứ vượt ra ngoài IP header. Lưu ý rằng không phải  IP hearder hay tải trọng bao gồm các Ethernet header.

<a name="step5"></a>
##### 2.9. Step 5: Demultiplexing Keys (Giải mã kênh):

- Khi một Ethernet frame tới một PC, lớp Ethernet phải giao các gói tin mà nó chứa đến lớp cao hơn kế tiếp để được xử lý. Các hành động của việc tìm kiếm các lớp cao hơn quyền xử lý các gói tin nhận được gọi là giải mã kênh. Chúng ta biết rằng trong trường hợp của chúng tôi các lớp cao hơn là IP. Nhưng làm thế nào các giao thức Ethernet biết điều này? Sau tất cả, các lớp cao hơn có thể là một giao thức khác hoàn toàn (như ARP). Chúng tôi có cùng một vấn đề ở lớp IP - IP phải có khả năng xác định nội dung của gói tin IP là một gói tin TCP để nó có thể giao cho các giao thức TCP để xử lý. Câu trả lời là các giao thức sử dụng thông tin trong phần đầu được biết đến như là một "demultiplexing key" để xác định các lớp cao hơn.
- Nhìn vào Ethernet header và IP header của một gói download  để trả lời các câu hỏi sau:
	- 1. Những Ethernet header là chìa khóa giải mã kênh mà với nó những lớp cao hơn tiếp theo là IP? giá trị nào được sử dụng trong lĩnh vực này để chỉ "IP"?
	
			*Câu trả lời:* Chìa khóa giải mã kênh cho Ethernet là trường Type. Nó chứa 				0x800 khi lớp cao hơn là IP.
	- 2. Những feild IP header là chìa khóa giải mã kênh mà với nó những lớp cao hơn tiếp theo là TCP? giá trị nào được sử dụng trong lĩnh vực này để chỉ "TCP"?

			*CâuTrả lời:* Chìa khóa giải mã kênh cho IP là lĩnh vực Protocol. Nó có giá 			trị 6 khi các lớp cao hơn là TCP.
            
<a name="p2"></a>            
### II.Command Line Tools

<a name="tailieu"></a>
### III. Tài liệu dịch

Slide:http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/lab-protocol-layers.pdf

Lab: http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm





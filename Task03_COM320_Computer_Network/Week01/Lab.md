## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **03/03/2017**

### Mục lục
[1. Mục tiêu](#muctieu)

[2. Yêu cẩu](#yeucau)

- [2.1 Wireshark](#wireshark)
- [2.2 Wireshark & Packet Sniffing Backgroun](#sniffs)
- [2.3 Step 1: Capture a Trace](#thaotac)
- [2.4 Step 1: Capture a Trace](#thaotac)
- [Giao diện chính của Wireshark](#giaodien)

[3. Tài liệu dịch](#tailieu)



<a name="muctieu"></a>
### 1. Mục tiêu 
Để tìm hiểu cách thức và lớp được biểu diễn trong các gói tin. Nó là những khái niệm quan trọng cho cơ cấu mạng được nêu trong các văn bản.
Các dấu vết cho các bài Lab này là ở đây:
 http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/trace-protocol-layers.pcap
(Mặc dù các dấu vết chính bạn sẽ nhìn vào từ một trang web bạn chọn như www.ulster.ac.uk trong các ví dụ để làm theo).

<a name="yeucau"></a>
### 2. Yêu cầu:

<a name="wireshark"></a>
#### 2.1. Wireshark:

Bài Lab này sử dụng các công cụ phần mềm Wireshark để bắt và kiểm tra tìm các gói tin. Một dấu vết gói được ghi lại khi lưu thông ở một vị trí trên mạng, như được chụp ảnh chụp của tất cả các bit truyền trên một dây đặc biệt. Các dấu vết gói ghi dấu thời gian cho mỗi gói tin, cùng với các bit tạo nên các gói tin, từ các tiêu đề lớp thấp đến các nội dung lớp cao. 

Wireshark chạy trên hầu hết các hệ điều hành, bao gồm cả Windows, Mac và Linux. Nó cung cấp một giao diện người dùng đồ họa mà ta thấy trình tự của gói tin và ý nghĩa của các bit khi được giải thích tiêu đề giao thức và dữ liệu. Nó mã hóa các gói tin theo kiểu của nó, và có nhiều cách khác nhau để lọc và phân tích các gói tin để cho bạn điều tra hành vi của các giao thức mạng.

Wireshark được sử dụng rộng rãi để khắc phục sự cố mạng. Bạn có thể tải về từ www.wireshark.org cho máy tính cá nhân của bạn. Đây là một lý tưởng để phân tích dữ liệu  cho các Lab của chúng tôi - ổn định, có một cơ sở người dùng lớn và hỗ trợ cũng như các tài liệu bao gồm một người sử dụng hướng dẫn http://www.wireshark.org/docs/wsug_html_chunked), và một FAQ chi tiết, chức năng phong phú bao gồm các khả năng để phân tích hàng trăm giao thức, và một giao diện người dùng được thiết kế tốt. Nó hoạt động trong máy tính sử dụng Ethernet, nối tiếp (PPP và SLIP), 802,11 mạng LAN không dây, và nhiều công nghệ kết nối các lớp khác (nếu hệ điều hành mà nó đang chạy Wireshark cho phép làm như vậy). Nó đã được cài đặt trong các bài Lab.

Một sự giúp đỡ hướng dẫn nhanh chóng để lọc hiển thị Wireshark là ở đây: http://openmaniak.com/wireshark_filters.php



Wireshark là một công cụ cốt lõi đối với bất kỳ 'người đàn ông ở giữa' không dây hoặc tấn công snooping. Nó đơn giản là không thể thiếu cho những ai muốn kiểm tra các gói dữ liệu được chuyển qua mạng - tốt hay xấu ...

#### 2.2. Wireshark & Packet Sniffing Backgroun:
Các công cụ cơ bản để quan sát các thông điệp trao đổi giữa các đơn vị thực hiện giao thức được gọi là một gói sniffer.Theo như tên cho thấy, một ảnh chụp gói sniffer ( "sniffs") thông điệp được gửi /  được nhận từ / bởi máy tính của bạn; nó cũng sẽ thường lưu trữ và / hoặc hiển thị các nội dung của các giao thức khác nhau trong các thư  khi bị bắt. Một gói sniffer là thụ động. Nó quan sát các thông điệp được gửi và nhận bởi các ứng dụng và các giao thức chạy trên máy tính của bạn, nhưng không bao giờ gửi các gói dữ liệu riêng của mình. Tương tự như vậy, nhận được gói tin không bao giờ gửi rõ ràng địa chỉ đến các gói sniffer.Thay vào đó, một gói sniffer nhận được một bản sao của gói tin được gửi / nhận được từ / bởi ứng dụng và các giao thức thực hiện trên máy tính của bạn. 

Hình 1 cho thấy cấu trúc của một gói sniffer. Ở bên phải của Hình 1 là các giao thức (trong trường hợp này, là giao thức Internet) và các ứng dụng (chẳng hạn như một trình duyệt web hoặc FTP) mà thường chạy trên máy tính của bạn. Các gói sniffer, thể hiện trong hình chữ nhật nét đứt trong hình 1 là một sự bổ sung cho các phần mềm thông thường trong máy tính của bạn, và bao gồm hai phần. Các thư viện bắt gói dữ liệu nhận được một bản sao của mỗi khung link-layer được gửi từ hoặc được nhận bởi máy tính của bạn. Tin nhắn trao đổi giữa các giao thức lớp cao hơn như HTTP, FTP, TCP, UDP, DNS, hoặc IP tất cả cuối cùng đều được gói gọn trong khung link-layer được truyền qua phương tiện vật lý như một cáp Ethernet.

![](http://i.imgur.com/2OzVb7p.png)

Hợp phần thứ hai của một gói sniffer là phân tích dữ liệu, hiển thị các nội dung của tất cả các lĩnh vực trong một thông điệp giao thức. Để làm như vậy, gói tin phân tích  phải "hiểu" cấu trúc của tất cả các thư trao đổi của giao thức. Ví dụ, giả sử chúng ta quan tâm việc hiển thị các lĩnh vực khác nhau trong các gói tin trao đổi giữa các giao thức HTTP trong Hình 1. Các gói phân tích hiểu định dạng của khung Ethernet, và do đó có thể xác định các gói tin IP trong khung Ethernet. Nó cũng hiểu định dạng gói tin IP, để nó có thể xuất các phân đoạn TCP trong gói tin IP. Cuối cùng, nó hiểu được cấu trúc phân đoạn TCP, vì vậy nó có thể xuất các thông điệp HTTP chứa trong phân khúc TCP. Cuối cùng, nó hiểu các giao thức HTTP và như vậy, ví dụ,nó biết rằng các byte đầu tiên của thông điệp HTTP sẽ chứa chuỗi "GET", "POST", hoặc "HEAD".

<a name="sniffs"></a>
#### 2.3. Step 1: Capture a Trace 

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
#### 2.4. Giao diện chính của Wireshark:

Giao diện Wireshark có năm thành phần chính:
![](http://i.imgur.com/DbMICy5.png)

- Các menu lệnh là tiêu chuẩn kéo xuống menu nằm ở trên cùng của cửa sổ. Các menu File cho phép bạn lưu dữ liệu gói bắt hoặc mở một tập tin chứa dữ liệu gói chụp được trước đó. Các menu Capture cho phép bạn bắt đầu bắt gói dữ liệu.
- Cửa sổ  danh sách gói hiển thị tóm tắt thành một dòng cho mỗi gói tin bị bắt được, trong đó có số lượng gói tin (bởi Wireshark được giao; điều này một số gói tin không được  chứa trong phần đầu của bất cứ giao thức), thời gian mà tại đó các gói tin đã bị bắt, các gói tin có địa chỉ nguồn và địa chỉ đích, các loại giao thức, và các thông tin giao thức cụ thể chứa trong gói tin. Việc niêm yết gói tin có thể được sắp xếp theo bất kỳ bằng cách nhấp vào một tên cột. Các trường liệt kê các giao thức cấp độ cao nhất đã gửi hoặc nhận được gói tin này, nghĩa là các giao thức đó là nguồn hoặc chìm cuối cùng cho tài liệu này.
- Cửa sổ chi tiết gói tin tiêu đề cung cấp thông tin chi tiết về các gói tin được lựa chọn (đánh dấu) trong cửa sổ gói niêm yết. (Để chọn một gói tin trong cửa sổ gói niêm yết, đặt con trỏ trên bản tóm tắt một dòng của gói tin trong cửa sổ gói danh sách và nhấp chuột trái.). Những chi tiết này bao gồm thông tin về các khung Ethernet (giả sử các gói đã được gửi / nhận qua một giao diện Ethernet) và IP datagram có chứa gói tin này. Lượng Ethernet và chi tiết lớp IP hiển thị có thể được mở rộng hoặc giảm thiểu bằng cách nhấp vào hộp cộng-trừ bên trái của khung Ethernet hoặc dòng của gói tin IP trong cửa sổ chi tiết gói.
- Cửa sổ  nội dung gói hiển thị toàn bộ nội dung của khung bị bắt, trong cả hai ASCII và định dạng hệ thập lục phân. Phía trên cùng của giao diện người dùng đồ họa Wireshark, là khu vực lọc hiển thị gói, vào đó là một tên giao thức hoặc các thông tin khác có thể được nhập vào để lọc các thông tin hiển thị trong cửa sổ gói niêm yết.

<a name="tailieu"></a>
### 3. Tài liệu dịch:

http://scisweb.ulster.ac.uk/~kevin/com320/labs/wireshark/lab-protocol-layers.pdf. 





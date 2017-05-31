## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **31/05/2017**

---------------------------------------------

### Mục lục

[1. HTTP](#1)

- [1.1 Step 1: Capture a Trace](#1.1)
- [1.2 Step 2: Inspect the Trace](#1.2)
- [1.3 Step 3: Content Caching](#1.3)
- [1.4 Step 4: Complex Pages](#1.4)
- [1.5 Homework - Explore Your Network](#1.5)

[2. Examining the HTTP protocol request in detail](#2)

- [2.1. Hướng dẫn](#2.1)
- [2.2. Những gì bạn sẽ thấy](#2.2)
- [2.3. Sử dụng](#2.3)
- [2.4. Mã nguồn](#2.4)
- [2.5. Các công cụ khác](#2.5)

---------------------------------------------
<a name="1"></a>
### 1. HTTP

<a name="1.1"></a>
#### 1.1 Step 1: Capture a Trace

*Bắt gói tin của trình duyệt của bạn với yêu cầu HTTP như sau; Cách khác, bạn có thể sử dụng được cung cấp.*Bây giờ chúng ta đã thấy cách gói GET hoạt động, chúng ta sẽ quan sát trình duyệt vì nó tạo ra yêu cầu HTTP. Hoạt động của trình duyệt có thể khá phức tạp, sử dụng nhiều tính năng HTTP hơn trao đổi cơ bản, vì vậy chúng tôi sẽ Thiết lập một kịch bản đơn giản. Chúng tôi giả định rằng trình duyệt của bạn sẽ sử dụng HTTP trong kịch bản đơn giản. So với các giao thức Web mới hơn như SPDY, và nếu đây không phải là trường hợp bạn cần phải tắt SPDY.

- 1.1.1. *Sử dụng trình duyệt của bạn để tìm hai URL để thử nghiệm, cả hai đều là các URL HTTP (không phải HTTPS) mà không có cổng đặc biệt*. URL đầu tiên phải là hình ảnh từ nhỏ đến vừa, Cho dù là *.jpg, .gif, hay .png*. Chúng tôi muốn một số nội dung tĩnh mà không có tài nguyên được nhúng. Bạn có thể tìm URL như vậy bằng cách nhấp chuột phải vào các hình ảnh không liên kết trong các trang web để trình duyệt của bạn. Mở trực tiếp URL của hình ảnh. URL thứ hai nên là trang chủ của một số trang chính trang web mà bạn muốn nghiên cứu. Nó sẽ phức tạp khi so sánh. Truy cập cả hai URL để kiểm tra, sau đó giữ chúng bên ngoài tiện dụng của trình duyệt để bạn có thể cắt và dán chúng.
- 1.1.2. *Chuẩn bị trình duyệt của bạn bằng cách giảm hoạt động HTTP và xóa bộ nhớ cache*. Ngoài một tab mới mà bạn sẽ sử dụng, hãy đóng tất cả các tab, cửa sổ khác để giảm thiểu lưu lượng truy cập HTTP.
- 1.1.3. *Khởi động Wireshark và bắt đầu bắt với một bộ lọc "tcp port 80"*. Chúng tôi sử dụng bộ lọc này bởi vì không có chữ viết tắt cho HTTP, nhưng HTTP thường được thực hiện trên cổng TCP 80.

- 1.1.4. *Tìm nạp các chuỗi URL sau đây, sau khi bạn đợi một lúc để kiểm tra xem không có lưu lượng truy cập HTTP*. Nếu có lưu lượng truy cập HTTP thì bạn cần tìm và đóng ứng dụng đang gây ra sự cố. Nếu không, lưu lượng bắt được của bạn sẽ có quá nhiều lưu lượng HTTP để bạn hiểu. Bạn sẽ dán từng URL vào thanh URL của trình duyệt và nhấn Enter để tìm nạp nó. Không gõ URL vì điều này có thể khiến trình duyệt tạo ra các yêu cầu HTTP bổ sung vì nó sẽ tự động hoàn tất việc nhập của bạn.*
	- a. *Tìm URL hình ảnh tĩnh đầu tiên bằng cách dán URL vào thanh trình duyệt và nhấn "Enter" hoặc bất cứ điều gì cần thiết để chạy trình duyệt của bạn.*
	- b. *Chờ 10 giây và lấy lại URL hình ảnh tĩnh. Thực hiện theo cách tương tự và không sử dụng nút "Tải lại" của trình duyệt để kích hoạt các hành vi khác.*
	- c. *Chờ thêm 10 giây và tìm nạp trang chủ của trang thứ hai.*
- 1.1.5. *Dừng chụp sau khi tìm nạp xong*. Bạn nên có một cửa sổ đầy các gói, trong đó giao thức của một số gói được liệt kê là HTTP - nếu bạn không có bất kỳ gói tin HTTP nào, có vấn đề với thiết lập như trình duyệt của bạn bằng cách sử dụng SPDY thay vì HTTP để tìm nạp các trang web.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/1.png"></p>

<a name="1.2"></a>
#### 1.2 Step 2: Inspect the Trace

- *Để tập trung vào lưu lượng truy cập HTTP, hãy nhập và áp dụng biểu thức bộ lọc của "http"*. Bộ lọc này sẽ hiển thị các yêu cầu và phản hồi HTTP, chứ không phải các gói tin riêng lẻ. Nhớ lại rằng một nội dung phản hồi HTTP sẽ được truyền tải thông qua nhiều gói dữ liệu. Khi gói cuối cùng trong phản hồi đến, Wireshark lắp ráp các phản ứng hoàn chỉnh và gắn thẻ gói với giao thức HTTP. Các gói tin trước đó chỉ đơn giản là các phân đoạn TCP mang dữ liệu; Gói tin cuối cùng được gán nhãn HTTP bao gồm một danh sách tất cả các gói tin trước đó được sử dụng để thực hiện phản hồi. Một quá trình tương tự xảy ra cho yêu cầu, nhưng trong trường hợp này phổ biến cho một yêu cầu để phù hợp trong một gói duy nhất. Với biểu thức lọc của *"http"* chúng ta sẽ ẩn các gói tin TCP trung gian và chỉ thấy các yêu cầu và phản hồi HTTP. Với bộ lọc này, màn hình Wireshark của bạn phải giống với hình minh họa ví dụ của chúng tôi
- *Chọn GET đầu tiên trong lưu lượng bắt được, và mở rộng khối HTTP của nó*. Điều này sẽ cho phép chúng ta kiểm tra các chi tiết của một yêu cầu HTTP. Quan sát thấy  HTTP header theo TCP header và IP, vì HTTP là một giao thức ứng dụng được vận chuyển bằng TCP/IP. Để xem nó, chọn tìm khối HTTP trong bảng điều khiển giữa và mở rộng nó (bằng cách sử dụng "+" expander or icon).
- *Khám phá tiêu đề được gửi cùng với yêu cầu*. Đầu tiên, bạn sẽ thấy phương thức GET khi bắt đầu yêu cầu, bao gồm các chi tiết như đường dẫn. Sau đó, bạn sẽ thấy một loạt các tiêu đề dưới dạng thông số được gắn thẻ. Có thể có nhiều tiêu đề và sự lựa chọn tiêu đề và giá trị của chúng khác nhau giữa trình duyệt và trình duyệt. Xem bạn có bất kỳ tiêu đề chung nào không:
	- *Host*. Đây là tiêu đề bắt buộc, nó xác định tên (và cổng) của máy chủ.
	- *User-Agent*. Các loại trình duyệt và khả năng của nó.
	- *Accept, Accept-Encoding, Accept-Charset, Accept-Language*. Mô tả các định dạng sẽ được chấp nhận trong phản hồi, ví dụ: text/html, bao gồm mã hoá của nó, ví dụ: gzip và ngôn ngữ.
	- *Cookie*. Tên và giá trị của cookie mà trình duyệt giữ cho trang web.
	- *Cache-Control*. Thông tin về cách phản ứng có thể được lưu trữ.
- Thông tin yêu cầu được gửi bằng một văn bản đơn giản và định dạng dựa trên dòng. Nếu bạn nhìn vào bảng dưới cùng, bạn có thể đọc nhiều yêu cầu trực tiếp từ gói chính nó!
- *Chọn phản hồi tương ứng với GET đầu tiên trong các lưu lương bắt được, và mở rộng khối HTTP của nó*. Thông tin gói tin này sẽ cho biết *"200 OK"* trong trường hợp chuyển thành công bình thường. Bạn sẽ thấy rằng câu trả lời tương tự như yêu cầu, với một loạt các tiêu đề tuân theo mã trạng thái *"200 OK"*. Tuy nhiên, tiêu đề khác nhau sẽ được sử dụng, và các tiêu đề sẽ được theo sau bởi nội dung yêu cầu. Xem bạn có bất kỳ tiêu đề chung nào:
	- *Server*. Loại máy chủ và khả năng của nó.
	- *Date, Last-Modified*. Thời gian phản hồi và thời gian nội dung thay đổi lần cuối.
	- *Cache-Control, Expires, Etag*. Thông tin về cách phản ứng có thể được lưu trữ.

**Trả lời các câu hỏi sau:**
- a. Định dạng của một dòng tiêu đề là gì? Cung cấp một mô tả đơn giản phù hợp với tiêu đề bạn nhìn thấy?
	- *Trả lời:* Mỗi dòng tiêu đề bao gồm tên của trường tiêu đề và giá trị của nó được phân cách bởi dấu hai chấm. Có thể có khoảng trắng trước (và sau) giá trị. Dòng kết thúc bằng cặp ký tự "carriage return, line feed", thường được viết bằng *CRLF* hoặc *"\r\n"*.
- b. Tiêu đề nào được sử dụng để chỉ ra loại và chiều dài của nội dung được trả lại trong một phản ứng?
	- *Trả lời:* Loại nội dung được cung cấp bởi Content-Type header và độ dài của nó thường được cung cấp bởi tiêu đề Content-Length. (Có thể nhưng không chắc rằng các tiêu đề này không có mặt).

<a name="1.3"></a>
#### 1.3 Step 3: Content Caching

Việc tìm nạp lần thứ hai trong dấu vết nên tìm nạp lại URL đầu tiên. Việc tìm nạp này cho thấy cơ hội để chúng ta xem xét bộ nhớ đệm đang hoạt động, vì rất có khả năng lưu hình ảnh hoặc tài liệu không thay đổi và do đó không cần tải xuống lại.
Bây giờ chúng ta sẽ thấy cách chúng hoạt động.

*Chọn GET là tìm nạp lại GET đầu tiên và mở rộng khối HTTP của nó*. Có khả năng, đây sẽ là GET thứ hai trong các lư lượng bắt được .Tuy nhiên, xem xét cẩn thận vì trình duyệt của bạn có thể yêu cầu HTTP khác cho lý do riêng. Ví dụ, bạn có thể thấy một GET cho /favicon.ico trong dấu vết. Đây là trình duyệt yêu cầu biểu tượng cho trang web sử dụng như là một phần của trình duyệt hiển thị. Tương tự, nếu bạn nhập vào thanh URL trình duyệt của bạn có thể đã ban hành GETs như một phần của thủ tục tự động hoàn thành. Chúng tôi không quan tâm đến hoạt động trình duyệt này tại thời điểm hiện tại.

*Bây giờ việc tìm kiếm tiêu đề sẽ cho phép máy chủ tìm ra nếu nó cần phải gửi nội dung mới*. Chúng tôi sẽ hỏi bạn về tiêu đề này ngay lập tức. Máy chủ sẽ chỉ cần gửi nội dung mới nếu nội dung có sẵn Thay đổi kể từ khi trình duyệt cuối cùng tải xuống. Để thực hiện điều này, trình duyệt bao gồm việc thực hiện timestamp từ lần tải xuống trước cho nội dung mà nó đã lưu trữ. Tiêu đề này không có trong GET đầu tiên kể từ khi chúng tôi xóa bộ nhớ cache của trình duyệt, vì vậy trình duyệt đã không tải nội dung trước đó nó có thể sử dụng được. Trong hầu hết các khía cạnh khác, yêu cầu này sẽ giống như yêu cầu đầu tiên.

*Cuối cùng, chọn phản hồi để tìm nạp lại, và mở rộng khối HTTP của nó*. Giả sử bộ nhớ đệm hoạt động như mong đợi, phản hồi này sẽ không chứa nội dung. Thay vào đó, mã trạng thái của phản hồi sẽ là *"304 Not Modified"*. Điều này nói với trình duyệt rằng nội dung không thay đổi từ bản sao trước của nó và nội dung đã lưu vào bộ nhớ cache có thể được hiển thị.

*Trả lời các câu hỏi sau (trả lời ở trang sau).*

- a. Tên của tiêu đề trình duyệt gửi đến để cho máy chủ biết xem có nên gửi nội dung mới?
	- *trả lời:* Tiêu đề được gọi là *"If-Modified-Since"*, tức là nó yêu cầu máy chủ gửi nội dung nếu nó đã được sửa đổi từ một thời điểm nhất định.
- b. Trường hợp chính xác giá trị timestamp được mang bởi tiêu đề đến từ đâu?
	- *trả lời:* Timestamp đến từ tiêu đề *“Last-Modified”* của nội dung tải xuống gần đây nhất. Đó là Timestamp của máy chủ khi nội dung thay đổi lần cuối - không phải là Timestamp theo đồng hồ của trình duyệt và không phải là Timestamp của thời gian tải xuống

<a name="1.4"></a>
#### 1.4 Step 4: Complex Pages

Bây giờ chúng ta hãy kiểm tra lấy lần thứ ba vào cuối lưu lượng. Việc tìm nạp này là dành cho một trang web phức tạp hơn có khả năng đã nhúng các tài nguyên. Vì vậy, trình duyệt sẽ tải xuống HTML ban đầu cộng với tất cả các tài nguyên được nhúng cần thiết để hiển thị trang, cộng với các tài nguyên khác được yêu cầu trong quá trình thực hiện các tập lệnh trang. Như chúng ta sẽ thấy, một trang đơn lẻ có thể liên quan đến nhiều GET!

*Để tóm tắt các GET cho trang thứ ba, đưa lên bảng Phân phối HTTP* . Bạn sẽ tìm thấy bảng này dưới *"Statistics"* và *"HTTP"*. Bạn có thể lọc cho các gói tin là một phần của lần tìm nạp thứ ba bằng cách loại bỏ các gói tin từ phần trước đó của dấu vết theo thời gian hoặc số. Ví dụ: sử dụng *"frame.number> 27"* hoặc *"frame.time_relative> 24"* để theo dõi của chúng tôi.

Để tóm tắt các GET cho trang thứ ba, đưa lên bảng Phân phối Tải HTTP. Bạn sẽ tìm thấy bảng này dưới * "Thống kê" và "HTTP" *. Bạn có thể lọc cho các gói tin là một phần của lần tìm nạp thứ ba bằng cách loại bỏ các gói tin từ phần trước đó của dấu vết theo thời gian hoặc số. Ví dụ: sử dụng *"frame.number> 27"* hoặc *"frame.time_relative> 24"* để theo dõi của chúng tôi....

Nhìn vào bảng điều khiển này sẽ cho bạn biết có bao nhiêu yêu cầu đã được thực hiện cho các máy chủ nào. Có khả năng là tìm kiếm của bạn sẽ yêu cầu nội dung từ các máy chủ khác mà bạn có thể không nghi ngờ xây dựng trang. Các máy chủ khác có thể bao gồm các bên thứ ba như mạng phân phối nội dung, mạng quảng cáo và mạng phân tích. Bảng điều khiển của chúng tôi được hiển thị bên dưới - trang tìm nạp đã yêu cầu 95 yêu cầu đến 4 máy chủ khác nhau!
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/2.png"></p>

*Đối với một loại tóm tắt khác của GETs, đưa lên một bảng truy cập HTTP Packet Counter*. Bạn cũng sẽ tìm thấy bảng này trong *"Statistics"* và *"HTTP"*, và bạn nên lọc cho các gói tin là một phần của lần tải thứ ba như trước. Bảng điều khiển này sẽ cho bạn biết các loại yêu cầu và phản hồi. Bảng điều khiển của chúng tôi được thể hiện trong hình phía dưới. Bạn có thể thấy rằng nó bao gồm hoàn toàn các yêu cầu GET được kết hợp bởi 200 OK phản ứng.
Tuy nhiên, có nhiều mã phản hồi khác mà bạn có thể quan sát thấy trong dấu vết của bạn, chẳng hạn như khi tài nguyên đã được lưu trữ....
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/3.png"></p>

Bạn có thể tò mò muốn biết nội dung nào đang được tải xuống bởi tất cả các yêu cầu này. Ngoài việc nhìn thấy các URL trong cột Thông tin, bạn có thể nhận được bản tóm tắt các URL trong bảng Yêu cầu HTTP dưới *"Statistics"* và *"HTTP"*. Mỗi yêu cầu riêng biệt và phản hồi có cùng một hình thức chúng ta đã thấy trong một bước trước đó. Nói chung, chúng được thực hiện trong quá trình tìm nạp một trang hoàn chỉnh với một URL nhất định.

Để có cái nhìn chi tiết hơn về quy trình tải trang tổng thể, hãy sử dụng một trang web như *PageSpeed hoặc webpagetest.org* của Google. Các trang web này sẽ kiểm tra URL bạn chọn và tạo báo cáo về hoạt động tải trang, nói yêu cầu được tìm nạp vào thời điểm nào và đưa ra các mẹo để giảm thời gian tải trang tổng thể. Chúng tôi đã cho thấy sự khởi đầu của sơ đồ *"waterfall"* cho tải trang tương ứng với dấu vết của chúng tôi trong hình bên dưới. Sau khi lấy nguồn tài nguyên HTML ban đầu, có rất nhiều lần tìm nạp nhanh sau đó cho các tài nguyên nhúng như các tập lệnh JavaScript, bảng định kiểu CSS, hình ảnh và hơn thế nữa.

<a name="1.5"></a>
#### 1.5 Homework - Explore Your Network

Khám phá HTTP một mình khi bạn hoàn thành lab này. Một số gợi ý:
- Nghiên cứu cách trang web dẫn đến mẫu yêu cầu HTTP. Nhiều trang web phổ biến có các trang tương đối phức tạp đòi hỏi nhiều yêu cầu HTTP để xây dựng. Hơn nữa, các trang này có thể tiếp tục phát hành các yêu cầu HTTP "không đồng bộ" khi chúng đã tải, tải các hiển thị tương tác hoặc chuẩn bị cho trang tiếp theo, vv Bạn sẽ thấy hoạt động này khi bạn tìm thấy các yêu cầu HTTP tiếp tục sau khi trang được tải .
- Xem lưu lượng truy cập HTTP của luồng video trực tuyến. Chúng tôi đã xem xét lưu lượng web HTTP, nhưng các ứng dụng khác cũng yêu cầu HTTP. Việc phổ biến các trình khách video được nhúng trong các trình duyệt như Netflix để tải nội dung bằng cách sử dụng HTTP sẽ tìm nạp nhiều đoạn "nhỏ" video. Nếu bạn nhìn vào các ứng dụng khác, bạn có thể thấy rằng nhiều người trong số họ sử dụng HTTP để thay đổi về nội dung, mặc dù thường xuyên trên một cổng khác với cổng 80.

**Tiến hành:**

- Đầu tiên mở wireshark với bộ lọc là http, sau đó thử mở URL là ola.vn trên trình duyệt của bạn, kết quả ta có 1 danh sách gói Http như hình bên dưới:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/6.png"></p>

- Bây giờ chúng ta sẽ tiến hành phân tích các gói tin bắt được.
	- Khi chúng ta truy cập ola.vn thì http request được gửi đến máy server để yêu cầu về nội dung cần:
		- Http request bắt đầu với một Request-Line, Request-Line chứa ba mục phân biệt, đó là method, uri, và phiên bản HTTP, mỗi mục được phân tách bởi một hay nhiều khoảng trống. Request-Line mà ta capture được là GET, POST,.. URI là */*, version *HTTP/1.1*. chúng ta có thể tim thấy name và pass đăng nhập vào ola.vn khi mở gói POST
		- Http Response trả lời Http request từ web client, trong bài lab chúng ta bắt được nhiều gói khác nhau như 200-OK, 204-No Content,....
		

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/7.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/8.png"></p>


- Http Response gồm:
	- 1xx - Informational
	- 2xx - Success (200 - OK, 202 - Accepted, 204 - No Content)
	- 3xx - Redirection (301 Moved Permanently: tài nguyên đã được chuyển hoàn toàn tới địa chỉ Location trong HTTP response. 303 See other: tài nguyên đã được chuyển tạm thời tới địa chỉ Location trong HTTP response. 304 Not Modified: tài nguyên không thay đổi từ lần cuối client request, nên client có thể sử dụng đã lưu trong cache.)
	- 4xx - Client Error (400 - Bad Request, 401 - Unauthorized, 403 - Forbidden, 404 - Not Found, 405 - Method Not Allowed, 408 - Request Timeout, 429 - Too many requests)
	- 5xx - Server Error (500 - Internal Server Error, 503 - Service Unavailable, 504 - Gateway Timeout, 509 - Bandwidth Limit Exceed)

<a name="2"></a>
### 2. Examining the HTTP protocol request in detail:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/4.png"></p>

<a name="2.1"></a>
#### 2.1. Hướng dẫn

Về cơ bản, chỉ cần nhập URL và sau đó nhấp vào nút **Submit** 

- *URL*: Phải bắt đầu bằng *http://* ; Chúng tôi không làm các máy chủ an toàn.
- *Request Type*:
	- *GET*  mặc định, hiển thị cả tiêu đề và nội dung.
	- *HEAD* chỉ hiển thị tiêu đề - một lựa chọn tốt nếu đó là tất cả những gì bạn quan tâm, hoặc nếu bạn dự đoán một lượng nội dung rất lớn.
	- *TRACE* được quan tâm hạn chế - nó chỉ nhắc lại yêu cầu.
- *Version*: Phiên bản HTTP có thể ảnh hưởng đến phản hồi của máy chủ. *HTTP/1.1* là phiên bản hiện đại hơn. Lưu ý rằng khi bạn sử dụng HTTP/1.1, máy chủ có thể phản ứng với dữ liệu "chunked" (được chỉ ra bởi Transfer-Encoding: chunked trong tiêu đề), nơi đáp ứng hoàn toàn được chia thành nhiều phần nhỏ hơn.
- *Display Format*:
	- *Auto-Detect* mặc định, nhìn vào dòng *Content-Type* trong tiêu đề và lựa chọn những gì nó nghĩ là loại hiển thị thích hợp.
	- *Text*  hiển thị văn bản, phù hợp với các tệp HTML.
	- *Hex* hexadecimal hiển thị, đó sẽ là thích hợp hơn cho các tập tin hình ảnh.
- *User-Agent*: Đây là tùy chọn. Đôi khi một máy chủ từ xa có thể trả về một phản ứng khác nhau tùy thuộc vào trình duyệt hoặc trình duyệt đã khởi tạo yêu cầu. Nếu bạn không chỉ định chuỗi xác định người sử dụng đại lý, chúng tôi sẽ sao chép một chuỗi mà trình duyệt hiện tại của bạn sử dụng.
- *Referer*: (Vâng, đây là lỗi chính tả - nên là *"referrer"*. Xem nguồn gốc *origin of the term referer*. ) Cũng tùy chọn. Cho máy chủ biết địa chỉ URL đã yêu cầu. Máy chủ có thể phản hồi khác với yêu cầu tùy thuộc vào tài nguyên giới thiệu. Nó cũng cho phép một máy chủ tạo ra các danh sách các liên kết ngược đến các tài nguyên, khai thác gỗ, tối ưu hóa bộ nhớ đệm, vv Nó cũng cho phép tải các liên kết quá cũ hoặc sai sót để được truy tìm để bảo trì. Trường giới thiệu không nên được gửi nếu URL yêu cầu được lấy từ một nguồn không có URL riêng của nó, chẳng hạn như đầu vào từ bàn phím người dùng.
- *Accept-Encoding*: Cũng tùy chọn. Tiêu đề này đôi khi được sử dụng để xác định rằng trình duyệt sẵn sàng chấp nhận các định dạng nhất định trong phản ứng của máy chủ. Một ví dụ sẽ được nén, gzip .
- *Auto-Follow Location*: Nếu máy chủ trả về một Địa điểm: dòng trong tiêu đề HTTP, nó sẽ hướng dẫn trình duyệt của bạn *"forward"* or *"redirect"* đến vị trí mới đó. Nếu lựa chọn này được chọn, **HttpView** sẽ tự động tiếp tục truy vấn các vị trí mới như vậy (tối đa 4 lần).

<a name="2.2"></a>
#### 2.2. Những gì bạn sẽ thấy

Phần **Header** hiển thị nội dung mà trình duyệt của bạn sẽ nhận được nhưng không hiển thị. Ví dụ:
- *Last-Modified*: cho biết khi nào tệp được sửa đổi gần đây nhất
- *Set-Cookie*: yêu cầu trình duyệt của bạn tạo một cookie
- *Location*: yêu cầu trình duyệt của bạn chuyển sang một URL khác

Phần **Nội dung** hiển thị dữ liệu mà trình duyệt của bạn sẽ hiển thị cho bạn - hơi giống như sử dụng tính năng *Nguồn Xem* của trình duyệt .

Trong một hiển thị văn bản, các ký tự không phải là văn bản được hiển thị như sau:
- *(LF)* = Linefeed, aka Newline (hex 0A)
- *(CR)* = Vận chuyển trở lại (hex 0D)
- *(HT)* = Tab ngang (hex 09)
- *(00)* = Hexadecimal 00

<a name="2.3"></a>
#### 2.3. Sử dụng

- Hãy thử nhập *http://www.amazon.com* dưới dạng URL trong biểu mẫu ở trên và chọn tùy chọn tự động theo dõi vị trí. Bạn sẽ thấy rằng Amazon chuyển hướng bạn hai lần trong khi thiết lập các cookie khác nhau.

Lưu ý rằng nếu bạn nhằm mục đích trình duyệt của bạn tại *http://www.amazon.com*, việc trao đổi có thể hơi khác nhau. Nếu bất kỳ giá trị cookie nào của *amazon.com* đã được đặt trên hệ thống của bạn, trình duyệt của bạn sẽ gửi chúng lại, và Amazon sẽ trả lời tương ứng (ví dụ như chào mừng bạn theo tên).

- *HttpView* có thể hữu ích nếu bạn muốn xem văn bản nguồn của các tệp JavaScript (.js) và Cascading Style Sheet (.css).

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week06/Lab/Image/5.png"></p>

<a name="2.4"></a>
#### 2.4. Mã nguồn

Trình xem HTTP của tôi rất hữu ích và hiển thị chất lượng công việc mà khách hàng có thể mong đợi từ tôi. Xin lỗi, nhưng mã nguồn không có sẵn - Tôi cho đi rất nhiều tài liệu trên trang web của tôi, nhưng không phải tất cả mọi thứ!

<a name="2.5"></a>
#### 2.5. Các công cụ khác

Xem *http://www.rexswain.com/index.html* cho các tóm tắt và trình diễn khác: APL, REXX, XEDIT, KEDIT, Perl, HTML, Màu RGB, Cookie HTTP, Mẫu Email, Các biến môi trường CGI, Bao gồm Bên Máy chủ, v.v ...

----------------------------------------------

### Tài liệu dịch

[1] Lab Week 6: HTTP/Examining the HTTP protocol request in detail.
 http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm


## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **24/05/2017**

---------------------------------------------

### Mục lục

[1. HTTP](#1)

- [1.1 Step 1: Capture a Trace](#1.1)
- [1.2 Step 2: Inspect the Trace](#1.2)
- [1.3 Step 3: Content Caching](#1.3)
- [1.4 Step 4: Complex Pages](#1.4)
- [1.5 Homework - Explore Your Network](#1.5)

[2. Examining the HTTP protocol request in detail](#2)

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

<a name="1.4"></a>
#### 1.4 Step 4: Complex Pages

<a name="1.5"></a>
#### 1.5 Homework - Explore Your Network

<a name="2"></a>
### 2. Examining the HTTP protocol request in detail

----------------------------------------------
### Tài liệu dịch

[1] Lab Week 6: HTTP/Examining the HTTP protocol request in detail.
 http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm


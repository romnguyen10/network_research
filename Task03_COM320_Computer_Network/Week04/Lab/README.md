## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **08/05/2017**

### Mục lục

[I .ARP](#I)

- [1. Yêu cầu](#1)
- [2. Network setup](#2)
- [3. Step 1: Capture a Trace](#3)
- [4. Step 2: Inspect the Trace](#4)
- [5. Step 3: Details of ARP over Ethernet](#5)


[II .ARPattack](#II)

[III. Tấn công ARP bằng Cain & Abel](#III)

- [1. Giới thiệu](#cain)
- [2. Demo](#demo)

[III. Tài liệu dịch](#III)

------------------------------------------------------

<a name="I"></a>
#### I .ARP

<a name="1"></a>
##### 1. Yêu cầu:

**Wireshark**: sử dụng phẩn mềm để bắt và xem lưu lượng gói tin. Một luu luong gói tin là một bản ghi của lưu lượng truy cập tại một vị trí trên mạng, 
như là bắt tất cả các bit truyền qua một đường dây cụ thể. lưu lượng gói ghi lại thời gian cho mỗi gói tin, cùng với các bit tạo thành gói, từ các tiêu đề 
lớp thấp đến các nội dung lớp cao hơn. Wireshark chạy trên hầu hết các hệ điều hành, bao gồm Windows, Mac và Linux. . Nó cung cấp một giao diện đồ hoạ cho 
thấy chuỗi các gói tin và ý nghĩa của các bit khi được giải thích như các Protocol header và data. . Nó mã hóa màu các gói theo loại của họ, và có nhiều cách
 khác nhau để lọc và phân tích các gói để cho phép bạn điều tra hoạt động của các giao thức mạng. Wireshark được sử dụng rộng rãi để khắc phục sự cố mạng. 
 Bạn có thể tải nó từ www.wireshark.org nếu nó chưa được cài đặt trên máy tính của bạn. Chúng tôi khuyên bạn nên xem đoạn video ngắn 5 phút
  "Giới thiệu về Wireshark"  trên trang web. 

**ARP**: Trong bài lab này sử dụng  dòng lệnh `arp` để kiểm tra và xóa bộ nhớ cache được sử dụng bởi giao thức ARP trên máy tính của bạn. *Arp* được 
cài đặt như một phần của hệ điều hành trên các máy tính Windows, Linux và Mac, nhưng sử dụng các đối số khác nhau. Yêu cầu cần quyền quản trị viên để 
xóa bộ nhớ cache.

**ifconfig / ipconfig**: Lab này sử dụng dòng lệnh `ipconfig` (Windows) để kiểm tra trạng thái của giao diện mạng máy tính của bạn. **Ipconfig** được 
cài đặt như một phần của hệ điều hành trên máy tính Windows.

**route / netstat**: Labnày sử dụngh dòng lệnh `route` hoặc `netstat` để kiểm tra các tuyến đường được sử dụng bởi máy tính của bạn. Một tuyến đườn
g chính là tuyến đường mặc định (hoặc tuyến đường tới tiền tố 0.0.0.0) sử dụng cổng mặc định để truy cap Internet từ xa. Cả hai "route" và "netstat"
 đều được cài đặt như một phần của hệ điều hành trên Windows và Mac / Linux, nhưng có nhiều biến thể trên các tham số dòng lệnh phải được sử dụng.

**Browser**: Lab này sử dụng một trình duyệt web để tìm hoặc lấy các trang như là một khối lượng công việc. Bất kỳ trình duyệt web sẽ làm.


<a name="2"></a>
##### 2. Network setup:

Chúng tôi muốn quan sát giao thức ARP đang hoạt động. Nhớ lại rằng ARP được sử dụng để tìm địa chỉ Ethernet tương ứng với địa chỉ IP cục bộ mà máy tính 
của bạn muốn gửi một gói tin. Một ví dụ điển hình về địa chỉ IP local là địa chỉ IP  router hoặc defauld gateway kết nối máy tính của bạn với phần của Internet. 
Máy tính của bạn lưu trữ các bản dịch này trong bộ nhớ cache ARP để giao thức ARP thỉnh thoảng được sử dụng có thể thực hiện việc dịch. Thiết lập từ 
quan điểm của máy tính bạn được thể hiện trong ví dụ dưới đây:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/1.png"></p>

<a name="3"></a>
##### 3. Step 1: Capture a Trace:

*Tiến hành như sau để bắt một lưu lương của gói tin ARP; Cách khác, bạn có thể sử dụng lưu lượng được cung cấp*. Để bắt được các gói tin ARP, chúng tôi sẽ
 làm cho máy tính của bạn gửi lưu lượng tới router khi không biết địa chỉ Ethernet của router - máy tính của bạn sẽ sử dụng ARP để phát hiện địa chỉ Ethernet.

- 1. *Tìm địa chỉ Ethernet của giao diện mạng chính của máy tính với lệnh `ifconfig / ipconfig`. Bạn muốn biết địa chỉ này để sau đó phân tích* . 
Trên Windows, đưa lên một dòng lệnh shell và gõ `ipconfig / all`. Trong số các đầu ra sẽ là một phần cho giao diện chính của máy tính 
(có thể là một giao diện Ethernet) và địa chỉ Ethernet của nó. Tên gọi chung của giao diện là "eth0", "en0", hoặc "Ethernet adapter".
 Một ví dụ được hiển thị bên dưới trong hình 2, được chung tôi to đậm.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image2.png"></p>

- 2. *Tìm địa chỉ IP của router hoặc defauld gateway mà máy tính của bạn sử dụng để tiếp cận với  Internet bằng lệnh `netstat / route`*. 
Bạn có thể sử dụng lệnh netstat (`netstat -r` trên Windows, Mac và Linux, dùng yêu cầu Ctrl-C để dừng lại). Ngoài ra, bạn có thể sử dụng lệnh route 
(`route print` trên **Windows**, `route` trên **Linux**, `route -n get default` trên **Mac**). Trong cả hai trường hợp, bạn đang tìm kiếm địa chỉ 
IP gateway tương ứng với đích đến mặc định hoặc 0.0.0.0. ví dụ được hiển thị trong hình 3 cho netstat, được tô đậm.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/3.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/4.png"></p>

- 3. *Khởi động Wireshark và bắt đầu bắt với bộ lọc là "arp"*. Cửa sổ chụp của bạn phải giống với hình chụp bên dưới, trừ điểm nhấn của chúng tôi. 
Chọn giao diện để bắt như giao diện có dây hoặc không dây chính được sử dụng bởi máy tính của bạn để kết nối với Internet. Nếu không chắc chắn, 
hãy đoán và xem lại bước này sau nếu việc bắt của bạn không thành công. Bỏ chọn "capture packets in promiscuous mode". Chế độ này hữu ích để bắt được
 các gói tin gửi đến/đi từ các máy tính khác trên mạng . Chúng tôi chỉ muốn ghi lại gói tin được gửi đến/đi từ máy tính của bạn. Để các tùy chọn khác
  ở các giá trị mặc định của chúng. capture fitter, nếu nó ton tai, nó được sử dụng để ngăn chặn việc chiếm giữ các lưu lượng truy cập khác mà máy tính
   của bạn có thể gửi hoặc nhận. Trên Wireshark 1.8, hộp bộ lọc bắt xuất hiện trực tiếp trên màn hình tùy chọn, nhưng trên Wireshark 1.9, 
   bạn đã thiết lập một bộ lọc chụp bằng cách nhấp đôi vào giao diện.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/5.png"></p>

- 4. *Khi capture bắt đầu, sử dụng lệnh `arp` để xóa defauld gateway từ bộ nhớ cache ARP*. Sử dụng lệnh `arp -a` sẽ cho bạn thấy nội dung của bộ nhớ cache ARP như một thao tác kiểm tra để bạn có thể chạy `arp`. Bạn sẽ thấy mục nhập cho địa chỉ IP của defauld gateway. Để xóa mục này, sử dụng lệnh arp với các đối số khác nhau (`arp -d` trên Windows). Việc sử dụng arp này sẽ cần quyền quản trị viên để chạy, vì vậy bạn có thể chạy như một người dùng được đặc quyền trên Windows. . Lưu ý rằng lệnh nên chạy mà không có lỗi nhưng mục ARP có thể không xuất hiện để được xóa nếu bạn kiểm tra với "arp-a". Điều này là do máy tính của bạn sẽ gửi các gói ARP để ghi lại mục nhập này ngay khi bạn cần gửi một gói tin tới một địa chỉ IP từ xa và điều đó có thể xảy ra rất nhanh do hoạt động nền trên máy tính.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/6.png"></p>

- 5. *Bây giờ bạn đã xóa bộ nhớ cache ARP của bạn, lấy một trang từ xa tới trình duyệt Web của bạn*. Điều này sẽ tạo ra gó ARP để tìm địa chỉ Ethernet của defauld gateway để các gói tin có thể được gửi đi. Các gói ARP này sẽ được bắt bởi Wireshark. Bạn có thể xóa bộ nhớ cache ARP và lấy tài liệu một vài lần. Hy vọng rằng sẽ có các gói tin ARP khác được gửi bởi các máy tính khác trên mạng cục bộ sẽ được bắt. Các gói này có thể sẽ có mặt nếu có các máy tính khác trên mạng cục bộ của bạn. Trong thực tế, nếu bạn có một máy tính bận rộn và mạng nội bộ rộng lớn sau đó bạn có thể nắm bắt nhiều gói ARP. Lưu lượng ARP của các máy tính khác sẽ bị bắt khi các gói tin ARP được gửi đến địa chỉ phát sóng, vì trong trường hợp này chúng được dành cho tất cả các máy tính kể cả máy tính mà bạn đang chạy Wireshark. Vì hoạt động của ARP diễn ra chậm, bạn có thể phải đợi đến 30 giây để quan sát một số lưu lượng truy cập ARP cơ bản này.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/7.png"></p>

- 6. Một khi bạn đã nắm bắt một số lượng ARP, dừng bắt lại. Bạn sẽ cần trace, cộng với địa chỉ Ethernet của máy tính của bạn và địa chỉ IP của defauld gateway cho các bước tiếp theo.

<a name="4"></a>
##### 4. Step 2: Inspect the Trace:

Bây giờ chúng ta có thể nhìn vào một giao dịch ARP! Vì có thể có nhiều gói ARP trong lưu lương bắt của bạn, trước tiên chúng ta sẽ thu hẹp chế độ xem của chúng tôi tới các gói ARP được gửi trực tiếp từ hoặc đến máy tính của bạn.

Đặt bộ lọc hiển thị cho các gói có địa chỉ Ethernet của máy tính của bạn. Bạn có thể thực hiện việc này bằng cách nhập một biểu thức vào hộp trống "Filter:" gần đầu cửa sổ Wireshark và nhấp vào "Apply". Bộ lọc để nhập phụ thuộc vào địa chỉ Ethernet của bạn. Ví dụ: nếu địa chỉ Ethernet của bạn là 01: 02: 03: 04: 05: 06 sau đó nhập một biểu thức lọc `eth.addr == 01: 02: 03: 04: 05: 06`. Lưu ý dấu hai bằng . Nếu bạn đang sử dụng các lưu lượng gói được cung cấp, nó đi kèm với một tập tin văn bản bổ sung cho địa chỉ Ethernet và địa chỉ IP defauld gateway . Sau khi áp dụng bộ lọc này, ảnh chụp của bạn sẽ trông giống như hình bên dưới, trong đó chúng tôi đã mở rộng các chi tiết giao thức ARP.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/8.png"></p>

*Tìm và chọn một **ARP request** cho cổng mặc định và kiểm tra các trường của nó*. Có hai loại gói tin ARP, **request va reply**, và chúng tôi sẽ xem xét từng lượt một. Dòng thông tin cho request sẽ bắt đầu bằng "Who has …". Bạn muốn tìm kiếm một trong những gói tin yêu cầu MAC address  của defauld gateway, ví dụ: "MAC address " trong đó xx.xx.xx.xx là defauld gateway của bạn. Bạn có thể nhấp vào biểu tượng + expander hoặc biểu tượng for the Address Resolution Protocol  để xem các trường:

- Hardware và Protocol được đặt thành hằng số cho biết phần cứng là Ethernet và giao thức là IP. Điều này phù hợp với bản dịch ARP từ IP sang địa chỉ Ethernet.
- Kích thước Hardware và Protocol được đặt lần lượt là 6 và 4. Đây là các kích cỡ của Ethernet và địa chỉ IP theo byte.
- Trường opcode cho chúng ta biết đây là request.
- Tiếp theo đến bốn trường chính, , the sender MAC (Ethernet) and IP and the target MAC (Ethernet) and IP. Các trường này được điền càng nhiều càng tốt. Đối với request, người gửi biết địa chỉ MAC và địa chỉ IP của họ và điền vào. Người gửi cũng biết địa chỉ IP mục tiêu - đó là địa chỉ IP mà một địa chỉ Ethernet được mong muốn. Nhưng người gửi không biết địa chỉ MAC mục tiêu, vì vậy nó không điền vào nó.

*Tiếp theo, chọn một trả lời ARP và kiểm tra các trường của nó*. the reply sẽ trả lời yêu cầu và có dòng thông tin có dạng "xx.xx.xx.xx is at yy:yy:yy:yy:yy:yy":
- Loại và kích cỡ của Hardware and Protocol  được đặt như trước.
- Trường opcode có một giá trị khác cho chúng ta biết đây là reply.
- Tiếp theo đến bốn trường chính, , the sender MAC (Ethernet) and IP and the target MAC (Ethernet) and IP giống như trước. Các trường này được đảo ngược từ yêu cầu tương ứng vì mục tiêu cũ là người gửi mới (và ngược lại). Các trường nên bây giờ được điền đầy đủ vì cả hai máy tính đều cung cấp địa chỉ của chúng.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/9.png"></p>

<a name="5"></a>
##### 5. Step 3: Details of ARP over Ethernet:

Các gói ARP được thực hiện trong các khung Ethernet, và các giá trị của các trường Ethernet header được chọn để hỗ trợ ARP. Ví dụ, bạn có thể tự hỏi làm thế nào một gói ARP request được gửi đến máy tính mục tiêu để nó có thể reply và nói với người yêu cầu địa chỉ MAC của nó. Câu trả lời là  ARP request là (thông thường) broadcast ở lớp Ethernet để nó được nhận bởi tất cả các máy tính trên mạng nội bộ bao gồm cả mục tiêu. Nhìn chi tiết địa chỉ Ethernet đích của một yêu cầu: nó được đặt thành ff: ff: ff: ff: ff: ff, địa chỉ broadcasst. Vì vậy, mục tiêu nhận được yêu cầu và nhận ra rằng nó là người nhận mong muốn của tin nhắn; Các máy tính khác nhận yêu cầu biết rằng nó không phải là của chúng. Chỉ có mục tiêu đáp ứng với một trả lời. Tuy nhiên, bất cứ ai nhận được một gói ARP có thể học một bản đồ từ nó: the sender MAC và sender IP pair.

Để xem thêm chi tiết về ARP, hãy kiểm tra một ARP request và ARP repplly để trả lời những câu hỏi sau:

- 1. Mã opcode được sử dụng để chỉ ra một request? Còn reply thì sao?
- 2. ARP header lớn như thế nào cho một request? Còn về reply thì sao?
- 3. Giá trị nào được thực hiện theo yêu cầu cho địa chỉ MAC đích chưa biết?
- 4. Giá trị Ethernet Loại nào cho biết ARP là giao thức lớp cao hơn?
- 5. ARP reply broadcast (như ARP request) tra loi hay không?

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/10.png"></p>

Có một số tính năng cần lưu ý:
• trên gói request, MAC cần tìm không được biết vì vậy nó thường được điền như là 00: 00: 00: 00: 00: 00.
• trên gói reply, mục tiêu yêu cầu trở thành người trả lời và ngược lại.
• trên gói reply, người gửi MAC trả về câu trả lời được tìm kiếm; Nó được đánh dấu.
• Tất cả các trường được hiển thị là trường tiêu đề ARP

Câu trả lời cho các câu hỏi:
- 1. Mã request là 1 và mã reply là 2.
- 2. Tiêu đề ARP là 28 byte cho cả request và reply cho IPv4.
- 3. Địa chỉ MAC mục tiêu của yêu cầu thường là tất cả các số 0, hoặc 00: 00: 00: 00: 00: 00.
- 4. Giá trị Loại Ethernet cho ARP là 0x806.
- 5. Phản hồi ARP thường không được broadcast. Nó được gửi trực tiếp tới đích sử dụng địa chỉ Ethernet của nó.

<a name="II"></a>
#### II .ARPattack:

- 1. Download Ettercap from http://scisweb.ulster.ac.uk/~kevin/com320/labs/ettercap.exe.
- 2. Theo sự hướng dẫn tiến hành cài đặt nó. Nhìn vào hình bên dưới.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/11.png"></p>

- 3. Vào nút Run ở dưới cùng bên trái và đánh **"ettercap"**. Bạn sẽ thấy nó xuất hiện như trong hình dưới đây. Tất nhiên, bạn cũng có thể chạy nó từ trình đơn Tất cả các chương trình trong Windows là tốt.


- 4. Tiếp theo chọn **Unified Sniffing** từ tùy chọn trình đơn **Sniff** như thể hiện trong hình 3.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/12.png"></p>

- 5. Chọn giao diện Ethernet đầu tiên (trong trường hợp này là giao diện mạng "netXtreme Gigabit Ethernet Driver" (xem hình 4).
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/13.png"></p>

	- 1. Tiếp theo bạn sẽ được trình bày với một loạt các tùy chọn menu bao gồm **Start, Targets, Hosts, View Mitm, Filters, Logging and Plugins**. Bạn nên chọn tùy chọn **Hosts** và chọn **Scan for Hosts**. Xem hình 5.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/14.png"></p>

	- 2. Khi bạn chọn **Scan for hosts**, bạn sẽ thấy một cửa sổ bật lên hiển thị tiến trình khi tất cả 255 máy trong mạng nội bộ được quét. Xem hình 6.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/15.png"></p>

	- 3. Tiếp theo bạn nên chọn **Hosts List**  từ menu Máy chủ. Sau đó, bạn sẽ thấy một màn hình tương tự như hình 7 với một danh sách các máy chủ đã được tìm thấy.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/16.png"></p>

	- 4. **Hãy yêu cầu sự đồng ý của đồng nghiệp bạn để cho phép bạn chọn máy tính của họ để được quét. Họ nên xác nhận địa chỉ IP của họ cho bạn **. Điều đó có thể được tìm thấy như trong những tuần trước bằng cách gõ lệnh cmd trong trình đơn khởi động của Windows và mở cửa sổ lệnh. Sau đó, trong cửa sổ lệnh, nhập **ipconfig** và lưu ý địa chỉ ipv4 được hiển thị. Bạn có thể cần phải cuộn lên để xem nó trong cửa sổ nhắc lệnh. Ở hình 8, máy chủ lưu trữ 193.61.190.73 đang được chọn để quét.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/17.png"></p>

	- 5.  Khi bạn đã chọn mục tiêu bằng chuột, sau đó chọn nút **Add to Target 1**. Xem hình 9.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/18.png"></p>

	- 6. Chọn tùy chọn Menu **Targets**  và sau đó chọn **Current Targets**  như thể hiện trong hình 10.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/19.png"></p>

	- 7. Bây giờ bạn chỉ nhìn thấy máy tính của bạn cùng lớp của bạn như thể hiện trong hình 11.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/20.png"></p>

	- 8. Bây giờ đi đến **mitm** tùy chọn như thể hiện trong hình 12. Chọn **Arp poisoning**
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/21.png"></p>

	- 9. Khi chọn **Arp poisoning**, bạn sẽ được trình bày với cửa sổ đối thoại như trong hình 13. Đơn giản chỉ cần nhấp OK.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/22.png"></p>

	- 10. Sau đó bạn sẽ được trình bày với một cửa sổ một lần nữa tương tự như hình 14. Cuộc tấn công ARP tuy nhiên đang xảy ra bên dưới. Giờ đây, bạn có quyền truy cập vào tất cả lưu lượng truy cập được định tuyến đến địa chỉ IP mà bạn đã nhập trước đó. Bây giờ chúng ta sẽ chuyển sang Wireshark để thấy sức mạnh của một cuộc tấn công mitro ARP độc.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/23.png"></p>

	- 11. Mở Wireshark bằng cách gõ Wireshark tại tùy chọn chương trình chạy. Sau đó, bạn sẽ chọn giao diện thông thường của Etternet Intel và **Start** chụp. Trong bộ lọc hiển thị, nhập vào sau: **ip.src == yourfriendsipaddress && tcp.port == 80** ví dụ: Ip.src == 193.61.191.88 && tcp.port == 80. Xem hình 15.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/24.png"></p>

	- 12. Lấy bạn bè của bạn để duyệt đến bất kỳ trang web. Trong ví dụ dưới đây, tôi đã đi đến một trang CNN bàn về nhận xét của Coca-Cola từ Giám đốc điều hành. Đó là tại http://edition.cnn.com/2013/02/05/business/coke-ceo-muhtar-kent-capitalism-evolve/
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/25.png"></p>

	- 13. Một khi bạn của bạn đã bắt đầu lướt, bạn sẽ bắt đầu thấy rất nhiều HTTP và TCP gói tin xuất hiện trong cửa sổ hộp thư gói của bạn. Sau một thời gian bạn có thể ngừng chụp. Bạn cũng có thể chọn để ngăn chặn cuộc tấn công mitm. Bạn luôn có thể tiếp tục cuộc tấn công để xem lưu lượng truy cập **'fresh'** từ xa. Sau đó, bạn nên chọn trang mà anh ấy lướt qua ví dụ: CNN và nhấp chuột phải vào nó như được hiển thị dưới đây và chọn Follow TCP Stream.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/26.png"></p>

	- 14. Dòng theo dõi TCP sẽ dẫn bạn đến một cửa sổ như được hiển thị bên dưới. Lưu ý nội dung của GET và HOST trên hai dòng đầu tiên. Khi chúng tôi đưa chúng lại với nhau, chúng tôi nhận vị trí của trang được truy cập là edition.cnn.com/2013/02/05/business/coke-ceo-muhtar-kent-capitalism-evolve/. Điều này sẽ cho bạn thấy rằng tất cả lướt sóng có thể được snooped trên một mạng LAN.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/27.png"></p>

	- 20. Bây giờ mời bạn của bạn đến một trang web yêu cầu thông tin đăng nhập hoặc thông tin như thời tiết tại http://edition.cnn.com/weather. Dưới đây là một thành phố như Belfast:
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/28.png"></p>

	- 21. Tiếp theo, kiểm tra luu lương dây, bạn sẽ thấy một gói tin bị bắt với **"citySearch / json / true HTTP / 1.1"** hiển thị **sensitive data**.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/29.png"></p>

	- 22. Cuối cùng, hãy trở lại chương trình ettercap và chọn **Mitm** và nhấn vào **Stop mitm attack(s)**. Điều này sẽ đảm bảo rằng các bảng ARP trở lại bình thường và không có snooping không cần thiết của một người mới đến máy của người bạn của bạn diễn ra. Xem hình 19.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/30.png"></p>

	- 23. Các cửa sổ bật lên sau đây sẽ xác nhận rằng tất cả người man trong các cuộc tấn công ở giữa đã dừng lại. Mọi người giờ đây an toàn trở lại lab
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/31.png"></p>

	 - 24. Cuối cùng, bạn có thể thoát khỏi chương trình.
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/32.png"></p>

<a name="III"></a>
#### III. Tấn công ARP bằng Cain & Abel:

<a name="cain"></a>
##### 1. Giới thiệu:

Cain & Abel là một công cụ khôi phục mật khẩu được sử dụng nhiều nhất trên hệ điều hành Microsoft. Công cụ này cho phép người dùng rất nhiều cách khôi phục 
các loại mật khẩu khác nhau thông qua các bắt các gói tin trong mạng , bẻ khóa mật khẩu mã hóa thông qua tấn công từ điển, vét cạn và phân tích mật mã.
 Cain có thể ghi lại hội thoại VoIP, giải mã mật khẩu, khôi phục khóa mạng không dây. Nó có thể bẻ khóa các mã băm bao gồm NTLM,MD2,MD5,SHA-1,SHA-2 … 
 Có rất nhiều tính năng khiến Cain and Abel là một trong những công cụ khôi phục mật khẩu hàng đầu.

Cain & Abel này không khai thác những lỗ hổng chưa được vá của bất kỳ phần mềm nào. Nó tập trung vào những khía cạnh/điểm yếu hiện có trong các chuẩn giao thức,
 các phương pháp đăng nhập và các kỹ thuật đệm; mục đích chính của công cụ này là tìm ra mật khẩu và những thông tin càn thiết từ nhiều nguồn, tuy vậy,
  nó cũng sử dụng nhiều công cụ “phi chuẩn” đối với người sử dụng Microsoft Windows.

<a name="demo"></a>
##### 2. Demo:

Bước 1: Download và cài đặt Cain & Abel .Link Download: http://www.oxid.it/cain.html.

Sau khi cài đặt xong ta khởi động và được màn hình như bên dưới:

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/33.png"></p>

Bước 2: Tiếp theo ta vào `configure` chọn `tab `sniffer`. Chọn carb mạng phù hợp sau đó tick vào `Dont use Promiscuous mode` và chọn `OK`. hình minh họa bên dưới
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/34.png"></p>

Bước 3: Tiếp theo bạn lick vào biểu tượng như hình bên dưới và lick `OK`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/35.png"></p>

Sau khi thực hiện xong ta có được danh sách Ip như hình bên dưới.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/36.png"></p>

bạn muốn biết tên máy tính ứng với IP nào thì chuột phải chọn `Resolve Host name`.

Bước 4: Chọn `ARP` sau đó chọn dấu cộng xanh phía trên ta được bảng bên dưới. Thực hiện chọn từng Ip bảng bên trái cho đến khi hết. khi cho 1 IP bảng bên kia 
ta cần tô đen hết bảng bên này và chon 'OK'. Mục đích là lấy thông tin 1 đỉa chỉ điền đầy đủ cho tất cả dịa chỉ còn lại và ngược lại.

Sau khi thực hiện ta sẽ có được bảng như hình bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/37.png"></p>

Bước 5: chọn 1 dòng và lick vào biểu tượng `Start/Stop Arp` như hình bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/38.png"></p>

Bước 6: Để show user/password của các người dùng trên máy khác ta chọn `password`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Image/39.png"></p>


<a name="II"></a>
#### II. Tài liệu dịch:


Lab Week04: http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm



	

	
## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **09/04/2017**

### Mục lục
[I. DHCP](#I)

- [1. Network Setup](#1)

- [2. Step 1: Capture a Trace](#2)
	
- [3. Step 2: Inspect the Trace](#3)

- [4. Step 3: Details of DHCP Messages](#4)

- [5. Step 4: DHCP Message Addressing](#5)

[II. Viewing DHCP Client and DNS Client Status](#II)

[III. Tài liệu dịch](#III)

<a name=I></a>
### I. DHCP:

<a name=1></a>
#### 1. Network Setup:

- Nhớ lại rằng DHCP dùng để cấp IP của nó cho máy tính, cũng như các thông số khác như địa chỉ của bộ định tuyến cục bộ. Máy tính của bạn, máy khách, sử dụng giao thức DHCP để giao tiếp với máy chủ DHCP trên mạng cục bộ. Các máy tính khác trên mạng cục bộ cũng tương tác với máy chủ DHCP. Trong triển khai, có một số biến thể. Ví dụ, các local agent có thể là một  DHCP relay chuyển tiếp tin nhắn giữa các máy tính và một máy chủ DHCP từ xa. Hoặc máy chủ DHCP có thể được sao chép cho độ tin cậy, do đó có hai hoặc nhiều máy chủ DHCP local. Với mục đích của chúng tôi, bạn chỉ cần suy nghĩ về một máy chủ DHCP duy nhất.
- Việc trao đổi DHCP hoàn thành bao gồm bốn loại gói tin: **Discover**, cho máy tính của bạn để xác định vị trí máy chủ DHCP; **Offer**, để máy chủ cung cấp một địa chỉ IP; **Request**, để máy tính của bạn yêu cầu một địa chỉ được cung cấp; Và **Ack**, để máy chủ cấp địa chỉ thuê. Tuy nhiên, khi một máy tính đang thiết lập lại địa chỉ IP của nó trên một mạng mà nó đã sử dụng trước đó, nó có thể thực hiện một trao đổi ngắn liên quan đến hai loại gói tin DHCP: **Request**, để yêu cầu địa chỉ IP giống từ cùng một máy chủ như đã được sử dụng trước; Và ACK cho máy chủ để cấp địa chỉ thuê.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/1.png"></p>

<a name=2></a>
#### 2. Step 1: Capture a Trace:

*Tiến hành như sau để làm mới địa chỉ IP của bạn và thu thập một dấu vết của lưu lượng truy cập DHCP. Tuy nhiên, lưu ý rằng thủ tục sau sẽ không hoạt động trong trường hợp không chắc chắn rằng địa chỉ IP của máy tính của bạn được gán tĩnh. Ngoài ra, bạn có thể sử dụng dấu vết đã cung cấp. Cẩn thận không thực hiện lab này từ xa, vì khi bạn cho máy tính tắt và khởi động lại giao diện mạng, bạn sẽ mất kết nối!*

- 1. Khởi động Wireshark và bắt đầu bắt gói với bộ lọc là "(udp port 67) or (udp port 68)". Không có viết tắt để cho biết DHCP, vì vậy chúng tôi lọc lưu lượng sử dụng các cổng UDP dành cho DHCP. (Lưu ý, trong bộ lọc hiển thị trên màn hình chính bạn cũng có thể gõ `udp.port == 67 II udp.port == 68`).

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/2.png"></p>

- 2. Khi chụp bắt đầu, hãy *release* và *renew* địa chỉ IP của bạn bằng lệnh dưới đây. Thủ tục này có thể làm máy tính của bạn bị mất kết nối mạng tạm thời, và tùy thuộc vào hệ điều hành nó có thể làm gián đoạn kết nối mạng. Để giảm thiểu sự gián đoạn, hãy đóng bất kỳ chương trình nào đang sử dụng máy chủ từ xa và nhập lệnh vào một cửa sổ local.

	- **Windows**: Gõ lệnh `ipconfig / release` tiếp theo `ipconfig / renew`. (Xem hình dưới đây)

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/3.png"></p>

	- Nếu trên **Linux**: Tìm tên của giao diện mạng chính bằng cách nhập `ifconfig` và quan sát đầu ra. Giao diện có thể được gọi là `eth0` hoặc cái gì đó khác. Bây giờ sử dụng lệnh `dhclient` để phát hành địa chỉ IP thuê và phát hành hợp đồng. Nhập, ví dụ: `sudo dhclient -r eth0` để làm bản phát hành tiếp theo` sudo dhclient eth0` để làm mới hợp đồng cho thuê.
- 3. Khi bạn đã nắm bắt một số lưu lượng truy cập DHCP, dừng bắt gói.

<a name=3></a>
#### 3. Step 2: Inspect the Trace:

*Trong bước này và các bước tiếp theo, chúng tôi sẽ chỉ kiểm tra ngắn sự trao đổi DHCP được mô tả ở trên*. Điều này là do lưu lượng truy cập bạn đã nắm bắt có thể khác nhau khi cài đặt. Bạn có thể có ít gói tin DHCP trên một mạng tĩnh hoặc nhiều gói tin DHCP trên một mạng bận (đặc biệt nếu một lớp đang chạy lab này!). Chi tiết các gói tin DHCP có thể khác nhau tùy thuộc vào cách các máy tính thực hiện DHCP. Có thể có nhiều gói tin của một loại duy nhất trong một trao đổi do máy chủ sao chép, và các loại khác nhau của gói tin DHCP quá.

*Tìm kiếm sự trao đổi DHCP ngắn (trong gói Yêu cầu DHCP và gói DHCP Ack) trong dấu vết của bạn. Chọn gói DHCP Request, và quan sát stack của giao thức để xem các thông điệp DHCP được thực hiện như thế nào*. Giao thức liên kết có thể là Ethernet, và giao thức cao hơn tiếp theo là IP. Sau đó đến UDP, do đó, mỗi tin nhắn DHCP được thực hiện trong một gói UDP. Trên đầu trang UDP, Wireshark có khả năng nói BOOTP (Giao thức Bootstrap) thay vì DHCP. Đây là một chút khó hiểu, nhưng DHCP được thực hiện như là một mở rộng của một giao thức cũ hơn được gọi là BOOTP. Bạn có thể nghĩ đến phần BOOTP dưới dạng header và thông báo của DHCP. Một ví dụ
Cửa sổ được hiển thị bên dưới.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/4.png"></p>

*Mở rộng phần BOOTP (DHCP) (sử dụng "+" trình mở rộng hoặc biểu tượng) để xem chi tiết DHCP Request*. Có rất nhiều lĩnh vực, và chúng tôi sẽ chỉ ra một vài thay vì bao gồm tất cả. Các trường này được thực hiện trong tất cả các tin nhắn DHCP mặc dù chúng có các giá trị khác nhau trong các tin nhắn khác nhau.

- Thông báo bắt đầu bằng một *Message Type*. Đó là *Boot Request* được sử dụng cho tất cả các thư DHCP được gửi từ máy tính của bạn đến máy DHCP server.
- Sau một vài trường có một trường *Transaction ID*. Tất cả các gói tin DHCP trong một trao đổi cụ thể giữa client và server mang cùng một Transaction ID; Đó là cách cả hai kết thúc biết rằng các gói tin thuộc về trao đổi chứ không phải là một hoạt động DHCP đồng thời.
- Có một số trường *IP address*. Các trường này được sử dụng để mang địa chỉ IP như địa chỉ mà máy tính đang được chỉ định.
- Có một trường *Cookie Magic* Nó mang một giá trị cho thấy phần còn lại của tin nhắn chứa một loạt các Options DHCP. Tức là, đây thực sự là một thông báo DHCP, không phải là một tin nhắn BOOTP.
- Mỗi DHCP option là độc lập, với một mã nó nói những gì nó đại diện, cùng với một chiều dài và giá trị. Tùy chọn đầu tiên là *DHCP Message Type* (Loại Thông báo DHCP) cho biết loại thông điệp DHCP đang được thực hiện. Các tùy chọn khác khác với loại tin nhắn DHCP. Ví dụ, một yêu cầu DHCP sẽ có một yêu cầu Địa chỉ IP tùy chọn để yêu cầu một địa chỉ cụ thể, mà một DHCP Ack sẽ có một địa chỉ IP Thời gian cho thuê để nói cho bao lâu các địa chỉ IP được chỉ định.

Bây giờ chọn một gói DHCP Ack và so sánh các lĩnh vực BOOTP

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/5.png"></p>

Chúng tôi sẽ đặt câu hỏi về các lĩnh vực này trong phần tiếp theo, nhưng bây giờ muốn bạn quan sát rằng DHCP Ack có định dạng chung giống nhau, nhưng giá trị khác nhau cho các lĩnh vực và mang tùy chọn DHCP khác nhau.

Bạn có thể duyệt các tùy chọn DHCP Request và Acks để tìm hiểu về DHCP. Ví dụ: bạn có thể thấy địa chỉ IP của máy chủ bao lâu, cho dù là giây, phút, giờ hay ngày. Bạn cũng sẽ thấy các tham số cấu hình khác được chỉ định bởi máy chủ DHCP, chẳng hạn như địa chỉ IP của domain name server and router, the subnet mask, the domain name cho máy chủ, và nhiều hơn nữa.

Bạn cũng có thể cố gắng tạo ra toàn bộ dãy các DHCP Messages được trao đổi để thiết lập mạng của bạn. Nếu có thể đơn giản như việc trao đổi ngắn gọn Request và Ack, hoặc nó có thể là sự trao đổi hoàn toàn của Discover, Offer, Request và Ack. Nó có thể có các tin nhắn bổ sung như Release, và nó có thể có nhiều message (ví dụ, hai hoặc nhiều đề nghị hoặc Acks) do nhiều máy chủ DHCP cục bộ. Làm phức tạp việc trao đổi với máy tính của bạn là các dấu vết có thể nắm bắt lưu lượng truy cập DHCP đồng thời từ các máy tính local khác. Bạn có thể sử dụng ID giao dịch để tách các trao đổi khác nhau và nhìn vào địa chỉ nguồn Ethernet để xem các máy tính của bạn đã gửi tin nhắn DHCP nào Có khả năng lưu lượng DHCP khác được trộn lẫn với trao đổi của bạn.

<a name=4></a>
#### 4. Step 3: Details of DHCP Messages:

Dành thời gian hiểu DHCP. Lưu ý vị trí của khối giao thức Ethernet, IP, UDP và BOOTP.
Trả lời các câu hỏi dưới đây dựa trên việc kiểm tra các trường BOOTP / DHCP cho cả DHCP Request và DHCP Ack.

- 1. Hai giá trị của BOOTP Message Type field là gì?
- 2. Trường Transaction ID là bao lâu? Cho biết liệu có khả năng các hoạt động DHCP đồng thời được thực hiện bởi các máy tính khác nhau sẽ xảy ra để chọn cùng một Transaction ID?
- 3. Tên của trường mang địa chỉ IP được gán cho khách hàng là gì? Bạn sẽ tìm thấy trường này được điền vào DHCP Ack.
- 4. Giá trị của Magic Cookie là viết tắt của gì trong DHCP?
- 5. Tùy chọn DHCP đầu tiên là DHCP Message Type. Giá trị tùy chọn cho loại này là gì?
- 6. DHCP Request thường sẽ có một tùy chọn Client Identifier. Xem giá trị của tùy chọn này. Làm thế nào để xác định client ? Hãy đoán.
- 7. DHCP Acks thường có tùy chọn Server Identifier. Xem giá trị của tùy chọn này. Nó xác định máy chủ như thế nào? Hãy đoán.
- 8. Giá trị tùy chọn nào là viết tắt của Requested IP Address option? Và IP Address Lease Time option?
- 9. làm thế nào người nhận thông điệp DHCP biết rằng nó đã đạt đến sự lựa chọn cuối cùng?

**ANSWER Step 3: Details of DHCP Messages**:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/6.png"></p>

- 1. Hai giá trị là Boot Request (1) và Boot Reply (2).
- 2. Transaction ID độ dài là 4 byte . Do đó rất khó có khả năng sẽ có va chạm tương đối một số ít hoạt động DHCP đồng thời (cho đến khi con số đó đến gần 216!)
- 3. Trường "Your (client) IP address" mang địa chỉ IP đang được thuê cho khách hàng.
- 4. Giá trị cookie Magic DHCP là 0x63825363.
- 5. Giá trị tùy chọn của 53 là viết tắt của DHCP Message Type.
- 6. Ðặc biệt là cho Client Identifier để mang địa chỉ Ethernet của máy khách, nhưng có thể sử dụng một số loại nhận dạng khác (ví dụ: tên máy chủ, số sêri).
- 7. Nó là điển hình cho máy chủ nhận dạng để mang địa chỉ IP của máy chủ DHCP, nhưng có thể sử dụng một số loại định danh khác.
- 8. Giá trị tùy chọn của 50 là viết tắt của Requested IP Address và giá trị của 51 là IP Address.
- 9. Kết thúc các tùy chọn DHCP được xác định với tùy chọn DHCP được gọi là End with value 255.

<a name=5></a>
#### 5. Step 4: DHCP Message Addressing:
Bây giờ chúng ta sẽ xem xét các DHCP Messages được gửi đến các máy tính ở các lớp UDP, IP và Ethernet như thế nào. Điều này rất thú vị bởi vì DHCP được sử dụng để chỉ định các địa chỉ IP - một máy tính yêu cầu một địa chỉ DHCP có thể không có địa chỉ IP riêng của nó cũng không biết địa chỉ IP của máy chủ DHCP.

Bắt đầu bằng cách chọn gói DHCP request và xem chi tiết UDP của nó trong bảng Wireshark ở giữa. Chúng ta sẽ chỉ nhìn vào thông báo yêu cầu DHCP để giữ mọi thứ đơn giản, như các chi tiết về địa chỉ khác nhau cho các tin nhắn DHCP khác.

- 1. *Số cổng nào mà DHCP client sử dụng, và số cổng nào mà DHCP server sử dụng*? Cổng có vấn đề bởi vì các tin nhắn UDP được xử lý bằng cổng. Cả hai số cổng này nằm trên Request trong các trường source and destination port (và bạn cũng sẽ thấy chúng trên Ack).

*Bây giờ hãy nhìn vào các địa chỉ IP trong IP protocol header của gói tin cho câu hỏi tiếp theo*. Đừng nhìn vào các trường BOOTP cho các tham số DHCP, vì chúng ta quan tâm đến cách các thư DHCP được giải quyết ở các lớp giao thức thấp hơn. Khi yêu cầu được gửi đi, máy tính của bạn không có địa chỉ IP và thậm chí không biết địa chỉ IP của máy chủ DHCP, do đó địa chỉ IP khác với gói IP thông thường.

- 2. *Địa chỉ source IP được đặt vào Request messages*? Đó là một giá trị đặc biệt có nghĩa là "this host on this network" được sử dụng để khởi tạo.

- 3. *Địa chỉ Destination IP nào được đặt vào Request messages*? Nó cũng là một giá trị dành riêng được thiết kế để truy cập vào máy chủ DHCP bất cứ nơi nào trên mạng nội bộ.

*Cuối cùng, nhìn vào các địa chỉ Ethernet cho câu hỏi tiếp theo*.

- 4. *Địa chỉ Source Ethernet nào được đặt trên Request messages, và địa chỉ Destination Ethernet nào được đưa vào Request messages*? Một trong những địa chỉ này là địa chỉ dành riêng.

Nhìn vào địa chỉ sẽ giúp bạn hiểu tại sao máy tính của bạn có thể ghi lại lưu lượng DHCP của các máy tính local khác trong dấu vết của bạn. Vì địa chỉ IP chưa được thiết lập nên nhiều tin nhắn DHCP được gửi tới tất cả các máy tính trên mạng nội bộ. Điều này đảm bảo rằng mọi máy tính đều nhận được các tin nhắn DHCP dành cho họ, nhưng nó đặt ra một khó khăn: một máy tính có thể nhận được các tin nhắn DHCP dành cho máy tính khác.

- 5. *Làm thế nào để một máy tính tìm ra cho dù một DHCP nó nhận được thông báo như là một DHCP Request message của nó, và không phải là một trả lời cho máy tính khác*? Gợi ý: nếu bạn không chắc chắn sau đó hãy đi qua các lĩnh vực mà bạn đã kiểm tra trước đây trong Bước 2 ở trên.

**ANSWER Step 4: DHCP Message Addressing**:

- 1. DHCP client (máy tính của bạn) sử dụng cổng UDP 68 và DHCP server sử dụng cổng UDP 67.

- 2. Địa chỉ IP nguồn là 0.0.0.0. Đây là một địa chỉ đặc biệt được sử dụng trong quá trình khởi tạo địa chỉ.

- 3. Địa chỉ IP đích là 255.255.255.255. Đây là địa chỉ broadcast, có nghĩa là message dành cho tất cả các máy tính trên mạng. (Không thể sử dụng chương trình subnet broadcast bị hạn chế hơn, ví dụ: 192.168.255.255, vì máy khách chưa xác định được subnet mask).

- 4. Địa chỉ nguồn Ethernet chỉ đơn giản là địa chỉ Ethernet của máy tính của bạn, vì nó đã được gán cho NIC của bạn. Địa chỉ đích của Ethernet là ff: ff: ff: ff: ff: ff, địa chỉ Ethernet broadcast, để gói tin đến tất cả các máy tính trên mạng nội bộ.

- 5. Các tin nhắn DHCP trong một trao đổi duy nhất mang cùng một ID Transacsion. Do đó một máy tính sẽ tìm một DHCP relay như Ack với một ID Transacsion khớp với giá trị nó đặt trên DHCP trước đó như là một Request. (Đây là bổ sung cho  lọc bất kỳ địa chỉ Ethernet: nếu trả lời là unicast thì nó sẽ có địa chỉ Ethernet của máy tính như là điểm đến của nó.)

<a name=II></a>
### II. Viewing DHCP Client and DNS Client Status:

Trong project  này, bạn sử dụng Services control pane để xem trạng thái của DNS client và các dịch vụ DHCP Client, và sau đó sử dụng dòng lệnh để xem cùng một thông tin.

- 1. Giữ phím "Windows" và nhấn chữ "R". Trong hộp thoại, gõ **services.msc**, và nhấn **Enter** để bắt đầu Services control panel. The Services control panel khác với tab Services trong Task Manager, cho phép bạn dừng hoặc bắt đầu một dịch vụ và xem trạng thái của nó nhưng không thay đổi các thuộc tính khác, chẳng hạn như kiểu khởi động hoặc cách đăng nhập vào hệ thống.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/7.png"></p>

- 2. Cuộn xuống cho đến khi bạn tìm thấy dịch vụ DHCP client. Lưu ý rằng trạng thái của nó là Bắt đầu. Bấm đúp vào DHCP Client để mở thuộc tính của nó.
 
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/8.png"></p>

- 3. Nhấp vào  Startup type  để xem các tùy chọn có sẵn. Bạn không nên tắt hoặc dừng (trừ khi bạn khởi động lại nó) DHCP Client bởi vì nó được sử dụng để đăng ký và cập nhật bản ghi DNS máy tính của bạn. Vì vậy, ngay cả khi bạn không nhận được một địa chỉ IP thông qua DHCP, DHCP Client sẽ vẫn chạy. Ở phía trên danh sách loại Khởi động, chú ý đường dẫn đến tệp tin thực thi. Khi tìm kiếm DHCP Client trong tab Processes trong Task Manager, bạn nên tìm đường dẫn này.

- 4. Nhấp vào tab Log On. Hầu hết các dịch vụ được bắt đầu bằng cách sử dụng một tài khoản đặc biệt: Local Service, Local System, hoặc Network Service. Mật khẩu được tự động thay đổi theo định kỳ vì lý do bảo mật, vì vậy bạn không cần phải thay đổi mật khẩu.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/9.png"></p>

- 5. Nhấp vào tab Recovery. Bạn sử dụng tab này để chỉ định điều gì sẽ xảy ra nếu dịch vụ không thành công. Trong hầu hết các trường hợp, dịch vụ cố gắng khởi động lại hai lần. Bạn có thể chỉ định hành động để máy tính thực hiện (chẳng hạn như khởi động lại) nếu dịch vụ gặp lỗi khi cố gắng bắt đầu.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/10.png"></p>

- 6. Nhấp vào tab Dependencies, nơi bạn có thể xem các quy trình hoặc dịch vụ khác mà dịch vụ này phụ thuộc vào chạy và các quy trình hoặc dịch vụ khác phụ thuộc vào dịch vụ này. Trước khi ngừng một dịch vụ mà bạn nghĩ rằng bạn không cần, hãy kiểm tra các tính năng phụ thuộc để đảm bảo một dịch vụ khác mà bạn cần không bị ảnh hưởng. Nhấp Cancel.

  <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/11.png"></p>

- 7. Tiếp theo, kiểm tra thuộc tính của DNS client. Chúng chủ yếu giống với DHCP Client, ngoại trừ một lệnh **svchost.exe** khác được sử dụng để bắt đầu DNS. Cũng lưu ý rằng tên của dịch vụ được hiển thị dưới dạng Dnscache. Khi bạn hoàn tất, hãy đóng bảng điều khiển Dịch vụ.

- 8. Trên Windown mở một command prompt. Để xem trạng thái của các dịch vụ từ dòng lệnh, bạn sử dụng lệnh **sc query** và nhấn Enter để xem trạng thái của các dịch vụ allrunning.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/12.png"></p>

 Để xem trạng thái của DHCP, gõ **sc query dhcp** và nhấn Enter, và để xem trạng thái của DNS, gõ lệnh truy vấn dnscache và nhấn Enter.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/13.png"></p>

- 9. Đôi khi khởi động lại dịch vụ là cần thiết. Một máy tính khởi động lại thực hiện điều này, nhưng bạn cũng có thể làm điều đó trong Services control panel hoặc từ command line. Bạn sẽ có thể gõ **sc stop dhcp** và nhấn Enter. Ở đây trạng thái DHCP được hiển thị là STOP-PENDING (tuy nhiên điều này dường như không hoạt động trong phòng MF124). Nó sẽ làm việc ở nhà hoặc tại các địa điểm khác. Một lần nữa, nếu ở trên họ đã làm việc, bạn cũng có thể nhập truy vấn **sc dhcp** và nhấn Enter để thấy DHCP đã bị dừng lại. Loại sc start dhcp và nhấn Enter để bắt đầu dịch vụ một lần nữa.

## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **09/04/2017**

### Mục lục
[I. DHCP](#I)

- [1. Network Setup](#1)

- [2. Step 1: Capture a Trace](#2)
	
- [3. Step 2: Inspect the Trace](#3)

- [4. Step 3: Details of DHCP Messages](#4)

- [5. Step 4: DHCP Message Addressing](#5)

[II. Viewing DHCP Client and DNS Client Status](#II)

[III. Tài liệu dịch](#III)

<a name=I></a>
### I. DHCP:

<a name=1></a>
#### 1. Network Setup:

- Nhớ lại rằng DHCP dùng để cấp IP của nó cho máy tính, cũng như các thông số khác như địa chỉ của bộ định tuyến cục bộ. Máy tính của bạn, máy khách, sử dụng giao thức DHCP để giao tiếp với máy chủ DHCP trên mạng cục bộ. Các máy tính khác trên mạng cục bộ cũng tương tác với máy chủ DHCP. Trong triển khai, có một số biến thể. Ví dụ, các local agent có thể là một  DHCP relay chuyển tiếp tin nhắn giữa các máy tính và một máy chủ DHCP từ xa. Hoặc máy chủ DHCP có thể được sao chép cho độ tin cậy, do đó có hai hoặc nhiều máy chủ DHCP local. Với mục đích của chúng tôi, bạn chỉ cần suy nghĩ về một máy chủ DHCP duy nhất.
- Việc trao đổi DHCP hoàn thành bao gồm bốn loại gói tin: **Discover**, cho máy tính của bạn để xác định vị trí máy chủ DHCP; **Offer**, để máy chủ cung cấp một địa chỉ IP; **Request**, để máy tính của bạn yêu cầu một địa chỉ được cung cấp; Và **Ack**, để máy chủ cấp địa chỉ thuê. Tuy nhiên, khi một máy tính đang thiết lập lại địa chỉ IP của nó trên một mạng mà nó đã sử dụng trước đó, nó có thể thực hiện một trao đổi ngắn liên quan đến hai loại gói tin DHCP: **Request**, để yêu cầu địa chỉ IP giống từ cùng một máy chủ như đã được sử dụng trước; Và ACK cho máy chủ để cấp địa chỉ thuê.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/1.png"></p>

<a name=2></a>
#### 2. Step 1: Capture a Trace:

*Tiến hành như sau để làm mới địa chỉ IP của bạn và thu thập một dấu vết của lưu lượng truy cập DHCP. Tuy nhiên, lưu ý rằng thủ tục sau sẽ không hoạt động trong trường hợp không chắc chắn rằng địa chỉ IP của máy tính của bạn được gán tĩnh. Ngoài ra, bạn có thể sử dụng dấu vết đã cung cấp. Cẩn thận không thực hiện lab này từ xa, vì khi bạn cho máy tính tắt và khởi động lại giao diện mạng, bạn sẽ mất kết nối!*

- 1. Khởi động Wireshark và bắt đầu bắt gói với bộ lọc là "(udp port 67) or (udp port 68)". Không có viết tắt để cho biết DHCP, vì vậy chúng tôi lọc lưu lượng sử dụng các cổng UDP dành cho DHCP. (Lưu ý, trong bộ lọc hiển thị trên màn hình chính bạn cũng có thể gõ `udp.port == 67 II udp.port == 68`).

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/2.png"></p>

- 2. Khi chụp bắt đầu, hãy *release* và *renew* địa chỉ IP của bạn bằng lệnh dưới đây. Thủ tục này có thể làm máy tính của bạn bị mất kết nối mạng tạm thời, và tùy thuộc vào hệ điều hành nó có thể làm gián đoạn kết nối mạng. Để giảm thiểu sự gián đoạn, hãy đóng bất kỳ chương trình nào đang sử dụng máy chủ từ xa và nhập lệnh vào một cửa sổ local.

	- **Windows**: Gõ lệnh `ipconfig / release` tiếp theo `ipconfig / renew`. (Xem hình dưới đây)

	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/3.png"></p>

	- Nếu trên **Linux**: Tìm tên của giao diện mạng chính bằng cách nhập `ifconfig` và quan sát đầu ra. Giao diện có thể được gọi là `eth0` hoặc cái gì đó khác. Bây giờ sử dụng lệnh `dhclient` để phát hành địa chỉ IP thuê và phát hành hợp đồng. Nhập, ví dụ: `sudo dhclient -r eth0` để làm bản phát hành tiếp theo` sudo dhclient eth0` để làm mới hợp đồng cho thuê.
- 3. Khi bạn đã nắm bắt một số lưu lượng truy cập DHCP, dừng bắt gói.

<a name=3></a>
#### 3. Step 2: Inspect the Trace:

*Trong bước này và các bước tiếp theo, chúng tôi sẽ chỉ kiểm tra ngắn sự trao đổi DHCP được mô tả ở trên*. Điều này là do lưu lượng truy cập bạn đã nắm bắt có thể khác nhau khi cài đặt. Bạn có thể có ít gói tin DHCP trên một mạng tĩnh hoặc nhiều gói tin DHCP trên một mạng bận (đặc biệt nếu một lớp đang chạy lab này!). Chi tiết các gói tin DHCP có thể khác nhau tùy thuộc vào cách các máy tính thực hiện DHCP. Có thể có nhiều gói tin của một loại duy nhất trong một trao đổi do máy chủ sao chép, và các loại khác nhau của gói tin DHCP quá.

*Tìm kiếm sự trao đổi DHCP ngắn (trong gói Yêu cầu DHCP và gói DHCP Ack) trong dấu vết của bạn. Chọn gói DHCP Request, và quan sát stack của giao thức để xem các thông điệp DHCP được thực hiện như thế nào*. Giao thức liên kết có thể là Ethernet, và giao thức cao hơn tiếp theo là IP. Sau đó đến UDP, do đó, mỗi tin nhắn DHCP được thực hiện trong một gói UDP. Trên đầu trang UDP, Wireshark có khả năng nói BOOTP (Giao thức Bootstrap) thay vì DHCP. Đây là một chút khó hiểu, nhưng DHCP được thực hiện như là một mở rộng của một giao thức cũ hơn được gọi là BOOTP. Bạn có thể nghĩ đến phần BOOTP dưới dạng header và thông báo của DHCP. Một ví dụ
Cửa sổ được hiển thị bên dưới.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/4.png"></p>

*Mở rộng phần BOOTP (DHCP) (sử dụng "+" trình mở rộng hoặc biểu tượng) để xem chi tiết DHCP Request*. Có rất nhiều lĩnh vực, và chúng tôi sẽ chỉ ra một vài thay vì bao gồm tất cả. Các trường này được thực hiện trong tất cả các tin nhắn DHCP mặc dù chúng có các giá trị khác nhau trong các tin nhắn khác nhau.

- Thông báo bắt đầu bằng một *Message Type*. Đó là *Boot Request* được sử dụng cho tất cả các thư DHCP được gửi từ máy tính của bạn đến máy DHCP server.
- Sau một vài trường có một trường *Transaction ID*. Tất cả các gói tin DHCP trong một trao đổi cụ thể giữa client và server mang cùng một Transaction ID; Đó là cách cả hai kết thúc biết rằng các gói tin thuộc về trao đổi chứ không phải là một hoạt động DHCP đồng thời.
- Có một số trường *IP address*. Các trường này được sử dụng để mang địa chỉ IP như địa chỉ mà máy tính đang được chỉ định.
- Có một trường *Cookie Magic* Nó mang một giá trị cho thấy phần còn lại của tin nhắn chứa một loạt các Options DHCP. Tức là, đây thực sự là một thông báo DHCP, không phải là một tin nhắn BOOTP.
- Mỗi DHCP option là độc lập, với một mã nó nói những gì nó đại diện, cùng với một chiều dài và giá trị. Tùy chọn đầu tiên là *DHCP Message Type* (Loại Thông báo DHCP) cho biết loại thông điệp DHCP đang được thực hiện. Các tùy chọn khác khác với loại tin nhắn DHCP. Ví dụ, một yêu cầu DHCP sẽ có một yêu cầu Địa chỉ IP tùy chọn để yêu cầu một địa chỉ cụ thể, mà một DHCP Ack sẽ có một địa chỉ IP Thời gian cho thuê để nói cho bao lâu các địa chỉ IP được chỉ định.

Bây giờ chọn một gói DHCP Ack và so sánh các lĩnh vực BOOTP

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/5.png"></p>

Chúng tôi sẽ đặt câu hỏi về các lĩnh vực này trong phần tiếp theo, nhưng bây giờ muốn bạn quan sát rằng DHCP Ack có định dạng chung giống nhau, nhưng giá trị khác nhau cho các lĩnh vực và mang tùy chọn DHCP khác nhau.

Bạn có thể duyệt các tùy chọn DHCP Request và Acks để tìm hiểu về DHCP. Ví dụ: bạn có thể thấy địa chỉ IP của máy chủ bao lâu, cho dù là giây, phút, giờ hay ngày. Bạn cũng sẽ thấy các tham số cấu hình khác được chỉ định bởi máy chủ DHCP, chẳng hạn như địa chỉ IP của domain name server and router, the subnet mask, the domain name cho máy chủ, và nhiều hơn nữa.

Bạn cũng có thể cố gắng tạo ra toàn bộ dãy các DHCP Messages được trao đổi để thiết lập mạng của bạn. Nếu có thể đơn giản như việc trao đổi ngắn gọn Request và Ack, hoặc nó có thể là sự trao đổi hoàn toàn của Discover, Offer, Request và Ack. Nó có thể có các tin nhắn bổ sung như Release, và nó có thể có nhiều message (ví dụ, hai hoặc nhiều đề nghị hoặc Acks) do nhiều máy chủ DHCP cục bộ. Làm phức tạp việc trao đổi với máy tính của bạn là các dấu vết có thể nắm bắt lưu lượng truy cập DHCP đồng thời từ các máy tính local khác. Bạn có thể sử dụng ID giao dịch để tách các trao đổi khác nhau và nhìn vào địa chỉ nguồn Ethernet để xem các máy tính của bạn đã gửi tin nhắn DHCP nào Có khả năng lưu lượng DHCP khác được trộn lẫn với trao đổi của bạn.

<a name=4></a>
#### 4. Step 3: Details of DHCP Messages:

Dành thời gian hiểu DHCP. Lưu ý vị trí của khối giao thức Ethernet, IP, UDP và BOOTP.
Trả lời các câu hỏi dưới đây dựa trên việc kiểm tra các trường BOOTP / DHCP cho cả DHCP Request và DHCP Ack.

- 1. Hai giá trị của BOOTP Message Type field là gì?
- 2. Trường Transaction ID là bao lâu? Cho biết liệu có khả năng các hoạt động DHCP đồng thời được thực hiện bởi các máy tính khác nhau sẽ xảy ra để chọn cùng một Transaction ID?
- 3. Tên của trường mang địa chỉ IP được gán cho khách hàng là gì? Bạn sẽ tìm thấy trường này được điền vào DHCP Ack.
- 4. Giá trị của Magic Cookie là viết tắt của gì trong DHCP?
- 5. Tùy chọn DHCP đầu tiên là DHCP Message Type. Giá trị tùy chọn cho loại này là gì?
- 6. DHCP Request thường sẽ có một tùy chọn Client Identifier. Xem giá trị của tùy chọn này. Làm thế nào để xác định client ? Hãy đoán.
- 7. DHCP Acks thường có tùy chọn Server Identifier. Xem giá trị của tùy chọn này. Nó xác định máy chủ như thế nào? Hãy đoán.
- 8. Giá trị tùy chọn nào là viết tắt của Requested IP Address option? Và IP Address Lease Time option?
- 9. làm thế nào người nhận thông điệp DHCP biết rằng nó đã đạt đến sự lựa chọn cuối cùng?

**ANSWER Step 3: Details of DHCP Messages**:
	<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/6.png"></p>

- 1. Hai giá trị là Boot Request (1) và Boot Reply (2).
- 2. Transaction ID độ dài là 4 byte . Do đó rất khó có khả năng sẽ có va chạm tương đối một số ít hoạt động DHCP đồng thời (cho đến khi con số đó đến gần 216!)
- 3. Trường "Your (client) IP address" mang địa chỉ IP đang được thuê cho khách hàng.
- 4. Giá trị cookie Magic DHCP là 0x63825363.
- 5. Giá trị tùy chọn của 53 là viết tắt của DHCP Message Type.
- 6. Ðặc biệt là cho Client Identifier để mang địa chỉ Ethernet của máy khách, nhưng có thể sử dụng một số loại nhận dạng khác (ví dụ: tên máy chủ, số sêri).
- 7. Nó là điển hình cho máy chủ nhận dạng để mang địa chỉ IP của máy chủ DHCP, nhưng có thể sử dụng một số loại định danh khác.
- 8. Giá trị tùy chọn của 50 là viết tắt của Requested IP Address và giá trị của 51 là IP Address.
- 9. Kết thúc các tùy chọn DHCP được xác định với tùy chọn DHCP được gọi là End with value 255.

<a name=5></a>
#### 5. Step 4: DHCP Message Addressing:
Bây giờ chúng ta sẽ xem xét các DHCP Messages được gửi đến các máy tính ở các lớp UDP, IP và Ethernet như thế nào. Điều này rất thú vị bởi vì DHCP được sử dụng để chỉ định các địa chỉ IP - một máy tính yêu cầu một địa chỉ DHCP có thể không có địa chỉ IP riêng của nó cũng không biết địa chỉ IP của máy chủ DHCP.

Bắt đầu bằng cách chọn gói DHCP request và xem chi tiết UDP của nó trong bảng Wireshark ở giữa. Chúng ta sẽ chỉ nhìn vào thông báo yêu cầu DHCP để giữ mọi thứ đơn giản, như các chi tiết về địa chỉ khác nhau cho các tin nhắn DHCP khác.

- 1. *Số cổng nào mà DHCP client sử dụng, và số cổng nào mà DHCP server sử dụng*? Cổng có vấn đề bởi vì các tin nhắn UDP được xử lý bằng cổng. Cả hai số cổng này nằm trên Request trong các trường source and destination port (và bạn cũng sẽ thấy chúng trên Ack).

*Bây giờ hãy nhìn vào các địa chỉ IP trong IP protocol header của gói tin cho câu hỏi tiếp theo*. Đừng nhìn vào các trường BOOTP cho các tham số DHCP, vì chúng ta quan tâm đến cách các thư DHCP được giải quyết ở các lớp giao thức thấp hơn. Khi yêu cầu được gửi đi, máy tính của bạn không có địa chỉ IP và thậm chí không biết địa chỉ IP của máy chủ DHCP, do đó địa chỉ IP khác với gói IP thông thường.

- 2. *Địa chỉ source IP được đặt vào Request messages*? Đó là một giá trị đặc biệt có nghĩa là "this host on this network" được sử dụng để khởi tạo.

- 3. *Địa chỉ Destination IP nào được đặt vào Request messages*? Nó cũng là một giá trị dành riêng được thiết kế để truy cập vào máy chủ DHCP bất cứ nơi nào trên mạng nội bộ.

*Cuối cùng, nhìn vào các địa chỉ Ethernet cho câu hỏi tiếp theo*.

- 4. *Địa chỉ Source Ethernet nào được đặt trên Request messages, và địa chỉ Destination Ethernet nào được đưa vào Request messages*? Một trong những địa chỉ này là địa chỉ dành riêng.

Nhìn vào địa chỉ sẽ giúp bạn hiểu tại sao máy tính của bạn có thể ghi lại lưu lượng DHCP của các máy tính local khác trong dấu vết của bạn. Vì địa chỉ IP chưa được thiết lập nên nhiều tin nhắn DHCP được gửi tới tất cả các máy tính trên mạng nội bộ. Điều này đảm bảo rằng mọi máy tính đều nhận được các tin nhắn DHCP dành cho họ, nhưng nó đặt ra một khó khăn: một máy tính có thể nhận được các tin nhắn DHCP dành cho máy tính khác.

- 5. *Làm thế nào để một máy tính tìm ra cho dù một DHCP nó nhận được thông báo như là một DHCP Request message của nó, và không phải là một trả lời cho máy tính khác*? Gợi ý: nếu bạn không chắc chắn sau đó hãy đi qua các lĩnh vực mà bạn đã kiểm tra trước đây trong Bước 2 ở trên.

**ANSWER Step 4: DHCP Message Addressing**:

- 1. DHCP client (máy tính của bạn) sử dụng cổng UDP 68 và DHCP server sử dụng cổng UDP 67.

- 2. Địa chỉ IP nguồn là 0.0.0.0. Đây là một địa chỉ đặc biệt được sử dụng trong quá trình khởi tạo địa chỉ.

- 3. Địa chỉ IP đích là 255.255.255.255. Đây là địa chỉ broadcast, có nghĩa là message dành cho tất cả các máy tính trên mạng. (Không thể sử dụng chương trình subnet broadcast bị hạn chế hơn, ví dụ: 192.168.255.255, vì máy khách chưa xác định được subnet mask).

- 4. Địa chỉ nguồn Ethernet chỉ đơn giản là địa chỉ Ethernet của máy tính của bạn, vì nó đã được gán cho NIC của bạn. Địa chỉ đích của Ethernet là ff: ff: ff: ff: ff: ff, địa chỉ Ethernet broadcast, để gói tin đến tất cả các máy tính trên mạng nội bộ.

- 5. Các tin nhắn DHCP trong một trao đổi duy nhất mang cùng một ID Transacsion. Do đó một máy tính sẽ tìm một DHCP relay như Ack với một ID Transacsion khớp với giá trị nó đặt trên DHCP trước đó như là một Request. (Đây là bổ sung cho  lọc bất kỳ địa chỉ Ethernet: nếu trả lời là unicast thì nó sẽ có địa chỉ Ethernet của máy tính như là điểm đến của nó.)

<a name=II></a>
### II. Viewing DHCP Client and DNS Client Status:

Trong project  này, bạn sử dụng Services control pane để xem trạng thái của DNS client và các dịch vụ DHCP Client, và sau đó sử dụng dòng lệnh để xem cùng một thông tin.

- 1. Giữ phím "Windows" và nhấn chữ "R". Trong hộp thoại, gõ **services.msc**, và nhấn **Enter** để bắt đầu Services control panel. The Services control panel khác với tab Services trong Task Manager, cho phép bạn dừng hoặc bắt đầu một dịch vụ và xem trạng thái của nó nhưng không thay đổi các thuộc tính khác, chẳng hạn như kiểu khởi động hoặc cách đăng nhập vào hệ thống.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/7.png"></p>

- 2. Cuộn xuống cho đến khi bạn tìm thấy dịch vụ DHCP client. Lưu ý rằng trạng thái của nó là Bắt đầu. Bấm đúp vào DHCP Client để mở thuộc tính của nó.
 
 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/8.png"></p>

- 3. Nhấp vào  Startup type  để xem các tùy chọn có sẵn. Bạn không nên tắt hoặc dừng (trừ khi bạn khởi động lại nó) DHCP Client bởi vì nó được sử dụng để đăng ký và cập nhật bản ghi DNS máy tính của bạn. Vì vậy, ngay cả khi bạn không nhận được một địa chỉ IP thông qua DHCP, DHCP Client sẽ vẫn chạy. Ở phía trên danh sách loại Khởi động, chú ý đường dẫn đến tệp tin thực thi. Khi tìm kiếm DHCP Client trong tab Processes trong Task Manager, bạn nên tìm đường dẫn này.

- 4. Nhấp vào tab Log On. Hầu hết các dịch vụ được bắt đầu bằng cách sử dụng một tài khoản đặc biệt: Local Service, Local System, hoặc Network Service. Mật khẩu được tự động thay đổi theo định kỳ vì lý do bảo mật, vì vậy bạn không cần phải thay đổi mật khẩu.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/9.png"></p>

- 5. Nhấp vào tab Recovery. Bạn sử dụng tab này để chỉ định điều gì sẽ xảy ra nếu dịch vụ không thành công. Trong hầu hết các trường hợp, dịch vụ cố gắng khởi động lại hai lần. Bạn có thể chỉ định hành động để máy tính thực hiện (chẳng hạn như khởi động lại) nếu dịch vụ gặp lỗi khi cố gắng bắt đầu.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/10.png"></p>

- 6. Nhấp vào tab Dependencies, nơi bạn có thể xem các quy trình hoặc dịch vụ khác mà dịch vụ này phụ thuộc vào chạy và các quy trình hoặc dịch vụ khác phụ thuộc vào dịch vụ này. Trước khi ngừng một dịch vụ mà bạn nghĩ rằng bạn không cần, hãy kiểm tra các tính năng phụ thuộc để đảm bảo một dịch vụ khác mà bạn cần không bị ảnh hưởng. Nhấp Cancel.

  <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/11.png"></p>

- 7. Tiếp theo, kiểm tra thuộc tính của DNS client. Chúng chủ yếu giống với DHCP Client, ngoại trừ một lệnh **svchost.exe** khác được sử dụng để bắt đầu DNS. Cũng lưu ý rằng tên của dịch vụ được hiển thị dưới dạng Dnscache. Khi bạn hoàn tất, hãy đóng bảng điều khiển Dịch vụ.

- 8. Trên Windown mở một command prompt. Để xem trạng thái của các dịch vụ từ dòng lệnh, bạn sử dụng lệnh **sc query** và nhấn Enter để xem trạng thái của các dịch vụ allrunning.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/12.png"></p>

 Để xem trạng thái của DHCP, gõ **sc query dhcp** và nhấn Enter, và để xem trạng thái của DNS, gõ lệnh truy vấn dnscache và nhấn Enter.

 <p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Lab/Image/13.png"></p>

- 9. Đôi khi khởi động lại dịch vụ là cần thiết. Một máy tính khởi động lại thực hiện điều này, nhưng bạn cũng có thể làm điều đó trong Services control panel hoặc từ command line. Bạn sẽ có thể gõ **sc stop dhcp** và nhấn Enter. Ở đây trạng thái DHCP được hiển thị là STOP-PENDING (tuy nhiên điều này dường như không hoạt động trong phòng MF124). Nó sẽ làm việc ở nhà hoặc tại các địa điểm khác. Một lần nữa, nếu ở trên họ đã làm việc, bạn cũng có thể nhập truy vấn **sc dhcp** và nhấn Enter để thấy DHCP đã bị dừng lại. Loại sc start dhcp và nhấn Enter để bắt đầu dịch vụ một lần nữa.

<a name=III></a>
### III. Tài liệu dịch :

Lab Week 03: http://scisweb.ulster.ac.uk/~kevin/com320/labs.htm
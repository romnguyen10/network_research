## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **12/05/2017**

### Mục lục

[I. Tấn công ARP bằng Cain & Abel](#I)

- [1. Giới thiệu](#cain)
- [2. Chuẩn bị ](#chuanbi)
- [3. Demo tấn công](#demo)

[II. Tài liệu tham khảo](#II)

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


<a name="chuanbi"></a>
##### 3. Chuẩn bị:

- Cần có 2 máy PC:
	- Máy 1 gán IP là 192.168.1.200, default gateway là 192.168.1.1 như hình bên dưới:
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/1.png"></p>

	- Máy 2 gán IP là 192.168.1.100, default gateway là 192.168.1.1 như hình bên dưới:
		<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/2.png"></p>

- Phần mềm Cain & Abel .Link Download: http://www.oxid.it/cain.html.

<a name="demo"></a>
##### 3. Demo tấn công:

Bước 1: Cài đặt Cain & Abel trên PC2

Sau khi cài đặt xong ta khởi động và được màn hình như bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/3.png"></p>

Bước 2: Tiếp theo ta vào `configure` chọn tab `sniffer`. Chọn carb mạng phù hợp sau đó tick vào `Dont use Promiscuous mode` và chọn `OK`. hình minh họa bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/4.png"></p>

Bước 3: Tiếp theo bạn lick vào biểu tượng `Start/Stop Sniffer`. kế tiếp bạn lick chuột vào `Add to list` như hình bên dưới.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/5.png"></p>

Sau khi lick vào Add to list sẽ xuất hiện bảng `MAC address Scanner`. Chọn tick vào ` All host in my subnet` và nhấn OK.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/6.png"></p>

Quá trình Scanning sẽ bất đầu.Sau khi thực hiện xong ta có được danh sách Ip như hình bên dưới.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/7.png"></p>

bạn muốn biết tên máy tính ứng với IP nào thì chuột phải chọn `Resolve Host name`.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/8.png"></p>

Bước 4: Chọn `ARP` sau đó chọn Biểu tượng `Add to list` .
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/9.png"></p>

Xuất hiện bảng `New ARP Poison Routing` Thực hiện chọn từng Ip bảng bên trái cho đến khi hết. khi chọn 1 IP bảng bên trái ta cần tô đen hết bảng bên phải 
và lick 'OK'. Mục đích là lấy thông tin 1 đỉa chỉ điền đầy đủ cho tất cả dịa chỉ còn lại và ngược lại.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/10.png"></p>

Sau khi thực hiện ta sẽ có được bảng như hình bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/11.png"></p>

Bước 5: Tiếp theo ta  lick vào biểu tượng `Start/Stop Arp` ta được kết quả như hình bên dưới:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/12.png"></p>

Bước 6: Để thấy kết quả ta đã làm được gì... 

Vào PC1 mở 1 trình duyệt web truy cập 1 trang web. vd : ola.vn
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/13.png"></p>

Bạn hãy nhập Username và Passsword vào :
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/14.png"></p>

Bước 7: Quay lại với Cain & Abel ở PC2 Bạn hãy chọn `Passwords`. chọn `HTTP` ta sẽ thấy kết quả xuất hiện username, password và URL khi ta truy cấp máy PC1
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/15.png"></p>

Khi bạn nhập sai username và password thì PC2 vẩn bắt được thông tin:
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/16.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week04/Lab/Cain & Abel/Image/17.png"></p>

<a name="II"></a>
#### II. Tài liệu tham khảo:

- https://www.youtube.com/watch?v=m_XW12Ax-lo
- http://vforum.vn/diendan/showthread.php?47386-Huong-dan-download-va-su-dung-cain-and-Abel-de-hack-trong-mang-LAN


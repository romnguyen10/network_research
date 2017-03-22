## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **22/03/2017**

### Mục lục
[I. The Data link layer](#I)
[1. Data Link layer Design Issues](#1)

- [1.1. Frames](#1.1)
- [1.2. Possible services](#1.2)
- [1.3. Framing methods](#1.3)
- [1.4. Error control](#1.4)
- [1.5. Flow control](#1.5)
- [1.6. TWIT Resources](#1.6)

[2. Error Detection and Correction](#2)
- [2.1. Error correction codes](#2.1)
 
	- [2.1.1. Hamming codes](#2.1.1)
	- [2.1.2. Binary convolutional codes ](#2.1.2)
	- [2.1.3. Reed-Solomon and Low-Density Parity Check codes](#2.1.3)
	
- [2.2. Error detection codes](#2.2)
 
	- [2.2.1. Parity](#2.2.1)
	- [2.2.2. Checksums](#2.2.2)
	- [2.2.3. Cyclic redundancy codes ](#2.2.3)
	
[3. Elementary Data Link Protocols](#3)

- [3.1.Link layer environment](#3.1)
- [3.2.Utopian Simplex Protocol](#3.2)
- [3.3.Stop-and-Wait Protocol for Error-free channel](#3.3)
- [3.4.Stop-and-Wait Protocol for Noisy channel](#3.4)

[4. Sliding Window Protocols](#4)
- [4.1. Sliding Window concept](#4.1)
- [4.2. One-bit Sliding Window](#4.2)
- [4.3. Go-Back-N](#4.3)
- [4.4. Selective Repeat](#4.4)
- [4.5. Hak 5 Resources](#4.5)

[5. Example Data Link Protocols](#5)

- [5.1. Packet over SONET](#5.1)
- [5.2. PPP (Point-to-Point Protocol)](#5.2)
- [5.3. ADSL (Asymmetric Digital Subscriber Loop)](#5.3)

<a name=I></a>
### I. The Data Link layer
Chịu trách nhiệm phân phối các thông tin khung qua một liên kết:
- Xử lý lỗi truyền tải và điều chỉnh luồng dữ liệu.
- Data Link layer Chịu trách nhiệm kiểm soát việc truyền qua khung trên phương tiện.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/1.png"></p>
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/2.png"></p>

<a name="1"></a>
#### 1. Data Link Layer Design Issues
- Cuối cùng, data link layer sử dụng các dịch vụ của physical layer để gửi và nhận các bit thông qua các kênh truyền thông.
- Để hoàn thành các mục tiêu này, lớp data link lấy các gói dữ liệu nhận được từ lớp network và gói gọn chúng thành các *Frames* để truyền.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/3.png"></p>

<a name="1.1"></a>
	
  ##### 1.1. Frames
Link layer chấp nhận **Packet** từ lớp network và gói gọn chúng vào các **frames** mà nó gửi bằng lớp Physical; Tiếp nhận là quá trình đối diện

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/4.png"></p>

<a name="1.2"></a>
##### 1.2. Possible services
- Dịch vụ kết nối không được xác nhận
	- Frame được gửi không có kết nối /  lỗi phục hồi
	- Ethernet là ví dụ
- Dịch vụ kết nối không được chấp nhận
	- Frame được gửi đi với truyền lại nếu cần
	- Ví dụ là 802.11
- Dịch vụ kết nối được xác nhận
	- Kết nối được thiết lập; hiếm

<a name="1.3"></a>
##### 1.3. Framing methods
Để cho phép người nhận chuẩn bị cho một gói tin gửi đến, một khuôn mẫu chung được sử dụng cho Ethernet và 802.11 là có một khung bắt đầu với một mẫu được xác định rõ gọi là preamble.
**Byte count**
Frame bắt đầu với đếm số byte trong nó
- Đơn giản, nhưng khó để đồng bộ lại sau khi xảy ra lỗi.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/5.png"></p>

**Byte stuffing**
Đặc biệt cờ bytes trong khung; Sự xuất hiện của cờ trong dữ liệu phải được nhồi nhét (thoát)
- Dài hơn, nhưng dễ dàng đồng bộ lại sau khi lỗi.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/6.png"></p>
Satuffing ở mức bit:

- Frame flag có sáu liên tiếp 1s (không hiển thị)
- Khi truyền, sau năm bit 1 trong dữ liệu, một 0 được thêm vào
- Khi nhận được, một 0 sau năm bit 1 sẽ bị xóa
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/7.png"></p>

<a name="1.4"></a>
##### 1.4. Error control
Lỗi kiểm soát các khung sửa chữa được nhận khi lỗi:

- Yêu cầu phát hiện sai sót tại máy thu
- Thường truyền lại các khung không nhận diện
- Bộ đếm thời gian bảo vệ chống lại những phản hồi bị mất

Phát hiện lỗi và truyền lại là các chủ đề tiếp theo.

<a name="1.5"></a>
##### 1.5. Flow contro (Kiểm soát luồng)
Ngăn chặn người gửi nhanh khỏi máy thu chậm

- Người nhận phản hồi về dữ liệu có thể chấp nhận
- Khá trong lớp Link do các NIC chạy ở tốc độ "wire speed"
	- Người nhận có thể lấy dữ liệu nhanh như nó có thể được gửi
	
Flow contro là một chủ đề trong các lớp Liên kết và Vận tải

<a name="1.6"></a>
##### 1.6. TWIT Resources

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/8.png"></p>

LI-FI:  https://www.youtube.com/watch?v=yLCljViTkus

<a name="2"></a>
#### 2. Error Detection and Correction
Error code sự thêm thừa cấu trúc dữ liệu do đó các lỗi có thể được phát hiện, hoặc sửa chữa.
<a name="2.1"></a>
##### 2.1. Error correction codes

<a name="2.1.1"></a>
###### 2.1.1. Hamming codes
Mã chuyển dữ liệu của n bit thành các mã của n + k bit
Hamming distance là bit tối thiểu flips để biến một codeword thành  bất kỳ một trong valid khác.
- Ví dụ với 4 codewords của 10 bit (n = 2, k = 8):
	- 0000000000, 0000011111, 1111100000 và 1111111111
	- Hamming distance là 5
	
Giới hạn cho một mã với khoảng cách:
- 2d + 1 - có thể sửa lỗi d (ví dụ: 2 lỗi ở trên)
- d +1 - có thể phát hiện lỗi d (ví dụ: 4 lỗi ở trên)

<a name="2.1.2"></a>
###### 2.1.2. Binary convolutional codes
Hamming code cho một cách đơn giản để thêm kiểm tra bit và chính xác đến một lỗi bit đơn:
- Kiểm tra bit là chẵn lẻ trên tập con của codeword
- Tính lại các khoản chẵn lẻ (syndrome) cho biết vị trí của lỗi để flip, hoặc 0 nếu không có lỗi
- Mã số và Phát hiện Mã Hamming
<a name="2.1.3"></a>
###### 2.1.3. Reed-Solomon and Low-Density Parity Check codes
Toán học phức tạp, được sử dụng rộng rãi trong các hệ thống thực

<a name="2.2"></a>
##### 2.2. Error detection codes
<a name="2.2.1"></a>
###### 2.2.1. Parity

Parity bit được thêm vào như là tổng số modulo 2 của bit dữ liệu tương đương với XOR; Đây là chẵn lẻ:
- Ví dụ: 1110000 --> 11100001
- Phát hiện kiểm tra nếu tổng sai (lỗi)

Cách đơn giản để phát hiện một số lẻ của lỗi:
- Ví dụ: 1 lỗi, 11100101; Phát hiện, tổng là sai
- Ví dụ: 3 lỗi, 11011001; Tổng phát hiện sai
- Ví dụ: 2 lỗi, 11101101; Không phát hiện, tổng là đúng!
- Lỗi cũng có thể nằm trong bit chẵn lẻ
- Các lỗi ngẫu nhiên được phát hiện với xác suất ½

**Interleaving** của N bit chẵn lẻ phát hiện lỗi burst lên đến N:
- Mỗi khoản chẵn lẻ được thực hiện trên các bit không liên kết
- Ngay cả một burst đến lỗi N  sẽ không gây ra thất bại
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/9.png"></p>

<a name="2.2.2"></a>
###### 2.2.2. Checksums
 Checksum sử lý dữ liệu như các N-bit words và thêm N kiểm tra bit là tổng số modulo 2N của các từ:
- Ví dụ: Internet 16-bit 1s bổ sung checksum 

Tính chất:
- Tăng cường phát hiện lỗi trên bit chẵn lẻ
- Phát hiện ra burst đến N lỗi
- Phát hiện sai số ngẫu nhiên với xác suất 1-2N
- Dễ bị tổn hại đến lỗi hệ thống, ví dụ: số 0 được thêm vào

<a name="2.2.3"></a>
###### 2.2.3. Cyclic redundancy codes
Thêm các bit để khung truyền được xem như một đa thức được phân chia đều bởi một đa thức máy phát điện.
<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week03/Slide/Image/10.png"></p>

- Bắt đầu bằng cách thêm 0 vào khung và thử chia
- Offset bởi lời nhắc để làm cho nó chia đều

<a name="II"></a>
### II. Tài liệu dịch

Lecture 3: Data Link Layer  http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm
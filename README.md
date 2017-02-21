## Git and Github

> Tài liệu: Git and Github
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **21/02/2017**

### Mục lục

[1. Giới thiệu và cách thức hoạt động github](#gtvact)

[2. Cài đặt Git, Generate, add key SHH...](#setup)

- [2.1. Cài đặt Git](#caidat)

- [2.2. Các thiết lập ban đầu](#thietlap)

- [2.3. Liên kết tài khoản github bằng SSH (Add SSH key)](#addKey)

- [2.4. Caching your Github password](#caching)


---------

<a name="gtvact"></a>
###  1. Giới thiệu và cách thức hoạt động github:

- GitHub là một dịch vụ cung cấp kho lưu trữ mã nguồn Git dựa trên nền web cho các dự án
phát triển phần mềm. GitHub cung cấp cả phiên bản trả tiền lẫn miễn phí cho các tài khoản.Các dự án mã nguồn mở sẽ được cung cấp kho lưu trữ miễn phí.

- GitHub chủ yếu được sử dụng để lưu trữ mã nguồn phần mềm, nhưng cũng thường được sử dụng với nhiều loại tập tin như Final Cut hoặc các tài liệu Word

- Một người sử dụng phải tạo ra một tài khoản cá nhân để đóng góp nội dung lên Github, 
nhưng các kho mã nguồn công cộng có thể được duyệt và tải về với bất cứ ai. Với một người dùng đã đăng ký tài khoản, họ có thể thảo luận, quản lý, tạo ra các kho, đóng góp cho kho của người dùng khác, và xem xét thay đổi mã.

- Để sử dụng bạn cần vào trang này [đăng ký](https://github.com/join?source=header-home).
Sau đó tạo repository và bắt đầu. 

<a name="setup"></a>
### 2. Cài đặt Git, Generate, add key SHH,... :
<a name="caidat"></a>
#### 2.1. Cài đặt Git:
Trước tiên bạn cần tải Git về máy của bạn:

- Tải git về cho Windows:
https://git-for-windows.github.io/

Để cài đặt trên windown ta tiến hành cài đặt bình thường, yêu cầu phải có .NET 4.5.

- Tải git về cho Linux:
https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

Để cài đăt trên linux bạn sử dụng lệnh sau:
>	- Với HĐH là Ubuntu, Debian:
	
			apt-get install git
                
>	- Với HĐH là Fedora, CentOS:
 	
			yum install git
                
>	- Với Arch:
 
	 		pacman -S git
<a name="thietlap"></a>
#### 2.2. Các thiết lập ban đầu:
- Bạn cần thiết tập tên và email của mình để khi commit lên server sẽ nhận biết được ai đang commit lên 1 repo (vì có thể nhiều người tham gia) 

		git config --global user.name "tên/username của bạn"
		git config --global user.email "email của bạn"

- Lựa chọn trình soạn thảo mặc định (có thể không cần) như nano, vi, emacs,...
	
 		git config --global core.editor nano

- Có thể xem lại các thiết lập
 		git config --list


<a name="addkey"></a>
#### 2.3. Liên kết tài khoản github bằng SSH (Add SSH key):

vào terminal gõ lệnh:

		ssh-keygen -t rsa
		ls ~/.ssh/
		
Bạn sẽ thấy hiển thị dòng như thế này: `id_rsa       id_rsa.pub   known_hosts`

Tiếp theo gõ:

		ssh-agent -s
		ssh-add ~/.ssh/id_rsa
		cat ~/.ssh/id_rsa.pub

Truy cập đường dẫn sau https://github.com/settings/ssh (đảm bảo bạn đã đăng nhập vào github), chọn Add SSH key, đặt tên cho key này tại Title và paste nội dung vừa copy vào ô Key.

<img src="http://imgur.com/a41Bzfh" >

Kết quả ta được:

<img src="http://imgur.com/kI2jNS9" >
<a name="caching"></a>
#### 2.4. Caching your Github password:

có 2 cách: 

- Nếu bạn clone repo sử dụng HTTP thì có thể sử dụng 1 helper để lưu user/pass tài khoản github để tiện việc commit những thay đổi (sẽ không cần đánh user/pass lại). Để sử dụng helper bạn dùng lệnh sau: 

	 	git config --global credential.helper cache
		git config --global credential.helper 'cache --timeout=1800'
        
> Lưu ý: Nếu bạn không thiết lập thời gian cho helper thì mặc định là 15 phút.
       
- Bạn có thể xác thực bằng các phím SSH thay vì một tên người dùng và mật khẩu. Để giúp thiết lập một kết nối SSH bạn vào xem ở mục [2.3](#addkey)







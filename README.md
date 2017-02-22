## Git and Github

> Tài liệu: Git and Github
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **22/02/2017**

### Mục lục

[1. Giới thiệu và cách thức hoạt động github](#gtvact)

[2. Cài đặt Git, Generate, add key SHH...](#setup)

- [2.1. Cài đặt Git](#caidat)

- [2.2. Các thiết lập ban đầu](#thietlap)

- [2.3. Liên kết tài khoản github bằng SSH (Add SSH key)](#addKey)

- [2.4. Caching your Github password](#caching)

[3. Add, Remove, Commit, Push, Pull, Fetch, Clone,...](#cackhainiem)

- [3.1. Add](#add)

- [3.2. Remove](#remove)

- [3.3. Commit](#commit)

- [3.4. Push](#push)

- [3.5. Fetch](#fetch)

- [3.6. Clone](#clone)

- [3.7. Fork](#fork)

- [3.8. Star](#star)

- [3.9. Watch](#watch)

- [3.10. Pull](#pull)
 
[4. Tài liệu tham khảo](#tailieuthamkhao)



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

- Tải github về cho Windows:
https://windows.github.com/

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

<img src="http://i.imgur.com/a41Bzfh.png" >

Kết quả ta được:

<img src="http://i.imgur.com/kI2jNS9.png" >

<a name="caching"></a>
#### 2.4. Caching your Github password:

có 2 cách: 

- Nếu bạn clone repo sử dụng HTTP thì có thể sử dụng 1 helper để lưu user/pass tài khoản github để tiện việc commit những thay đổi (sẽ không cần đánh user/pass lại). Để sử dụng helper bạn dùng lệnh sau: 

	`git config --global credential.helper cache`

 	`git config --global credential.helper'cache --timeout=1800'`
        
> Lưu ý: Nếu bạn không thiết lập thời gian cho helper thì mặc định là 15 phút.
       
- Bạn có thể xác thực bằng các phím SSH thay vì một tên người dùng và mật khẩu. Để giúp thiết lập một kết nối SSH bạn vào xem ở mục [2.3](#addkey)
 
<a name="cackhainiem"></a>
### 3. Add, Remove, Commit, Push, Pull, Fetch, Clone, ...

**Trước tiên ta cần tạo Repository:**

- Trên windown: 

Click vào tool and options (hình bánh răng cạnh biểu tượng Sync) chọn options, Add account. Khai báo username và password trên github.

<img src="http://i.imgur.com/jid85Ph.png">

 tiếp theo:
 
<img src="http://i.imgur.com/KS0QQRf.png">

- Trên linux:

  Bạn vào trang github.com tao mới 1 repo:
  
  <img src="http://i.imgur.com/RrZ01Q3.png">

<a name="add"></a>
#### 3.1. Add

Để thực hiện hành động add ta sử dụng lệnh sau

 `git add README.md` để add file README.md

hoặc `git add *` or `git add --all` để add tất cả các file hiện có.

<a name="remove"></a>
#### 3.2. Remove

Nếu muốn xóa repo bạn vào repo đó trên server và chọn Delete this repository ở phần Setting

 <img src="http://i.imgur.com/mCG2AQU.png">
 
 <img src="http://i.imgur.com/XFaUm0f.png">
 
<a name="commit"></a>
#### 3.3. Commit

Để thự hiện hành động commit file README.md ta thực hiện lệnh

`git commit README.md -m "cap nhat moi"`

hoặc `git commit *` để commit tất cả.

<a name="push"></a>
#### 3.4. Push

 Để đồng bộ lên server Github ta thực hiện lệnh:

 `git push origin master`
 
<a name="fetch"></a>
#### 3.5. Fetch

Bạn sẽ truy cập vào dự án từ xa nào đó và cập nhật dữ liệu mà bạn chưa có trên repo đó. Sau khi Fetch xong bạn có thể tham chiếu đến toàn bộ các nhánh của dự án đó.

<a name="clone"></a>
#### 3.6. Clone

Để clone một repo về ta có thể chọn Clone or Download và nhấn Download Zip hoặc copy đường dẫn (bạn có thể chọn clone sử dụng SSH hoặc HTTP) và thực hiện với lệnh sau:

`git clone "đường dẫn vừa copy thư mục chứa repo trên local"`

<a name="cfork"></a>
#### 3.7. Fork

- Ta muốn phân phối hay sử dụng một project hay repo của ai đó để bắt đầu đồng nghĩa là ta sẽ Fork một repo về. Sau khi Fork về thì repo đó sẽ tồn tại trên github của chúng ta.

- Sau khi một repo được được clone, nó sẽ có một remote origin trỏ đến repo mà chúng ta đã Fork về chứ không phải là repo gốc. Để theo dõi repo gốc mà chúng ta đã Fork, ta thực hiện:

`git remote add upstream "link repo gốc"`

`git fetch upstream`

<a name="star"></a>
#### 3.8. Star

- Bạn có thể Star một repo bất kỳ và khi đó bạn có thể truy cập nhanh chóng và dể dàng theo dõi repo mà bạn quan tâm.

- Để thực hiện bạn chỉ cần nhấn vào Star trên repo đã chọn

<a name="watch"></a>
#### 3.9. Watch

Khi bạn chọn Watch trên repo bạn sẽ nhận được thông báo cho các yêu cầu mới hay vấn đề gì xảy ra với repo đó.

<a name="pull"></a>
#### 3.10. Pull

Giả sử trên server github của bạn có những thay đổi mà máy local chưa cập nhật những thay đổi đó. Bạn thực hiện lệnh sau:

`cd cd /opt/demo1/` chú ý vào phải đúng nơi chứa repo cần pull.

`git pull`

<a name="tailieuthamkhao"></a>
### 4. Tài liệu tham khảo

[1] http://rogerdudler.github.io/git-guide/index.vi.html

[2] https://github.com/hocchudong/git-github-for-sysadmin

[3] https://help.github.com/articles/set-up-git/

[4] https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

[5] https://help.github.com/articles/caching-your-github-password-in-git/




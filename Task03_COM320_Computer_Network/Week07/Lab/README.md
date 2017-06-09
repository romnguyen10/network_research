## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **09/06/2017**

---------------------------------------------

### Mục lục

[1. xHTML-XML-DTDs](#1)

- [1.1. Create a basic HTML Page](#1.1)
- [1.2. Exercise 2 - Creating a HTML file without all required Tags](#1.2)
- [1.3. Exercise 3 - Creating an XML Document that contains your mailing address](#1.3)
- [1.4. Exercise 4 - Creating an XML Document that stores data](#1.4)

---------------------------------------------

<a name="1"></a>
### 1. xHTML-XML-DTDs

<a name="1.1"></a>
#### 1.1. Create a basic HTML Page

- a. Bắt đầu trình soạn thảo văn bản của bạn và tạo một tài liệu mới, nếu cần
- b.  Nhập các thẻ sau đây để bắt đầu tài liệu HTML. Hãy nhớ rằng tất cả các tài liệu HTML phải bắt đầu và kết thúc bằng cặp thẻ `<html>...</html>`.

`<html>`

`</html>`

- c. 3. Thêm các thẻ `<head> và <title>` sau đây giữa cặp thẻ `<html>...<html>`. Tiêu đề sẽ xuất hiện trên thanh tiêu đề của trình duyệt Web của bạn. Hãy nhớ rằng cặp thẻ `<head>...</head>` phải bao gồm cặp thẻ `<title>...</title>`.

`<head>`

`<title>Web Page Example</title>`

`</head>`


- d. Tiếp theo, thêm các thẻ body sau đây trên thẻ đóng `</html>`:

`<body>`

`</body>`

- e. Nhập các thẻ sau và văn bản giữa cặp thẻ `<body>...</body>` để tạo phần thân của tài liệu HTML.

`<h1>This line uses the heading 1 tag</h1>`

`<p>This line includes <br> a line break</p>`

`<p>The following line is a horizontal rule</p>`

`<hr>`

`<h2>This line uses the heading 2 tag</h2>`

`<h3>This line uses the heading 3 tag</h3>`

`<p>This <b>line</b> <i>contains</i> <sup>text</sup>`

`<sub>formatting</sub></p>`

- f. Lưu tệp là **FirstWebPage.html** vào thư mục của bạn. Một số biên tập văn bản tự động thêm phần mở rộng của riêng họ vào một tài liệu. Notepad chẳng hạn, thêm một phần mở rộng của **.txt**. Đảm bảo tài liệu của bạn được lưu với phần mở rộng là **.html**.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/1.png"></p>

- g. Đóng tệp **FirstWebPage.html** và mở nó trong Firefox hoặc trình duyệt yêu thích của bạn bằng cách chọn Open File từ thực đơn File hoặc bằng cách nhấp vào tệp tin trong thư mục của bạn. Hình dưới đây cho thấy nó trông như thế nào.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/2.png"></p>

- h. Đóng trình duyệt web của bạn lại.

<a name="1.2"></a>
#### 1.2. Exercise 2 - Creating a HTML file without all required Tags (Tạo tệp HTML mà không cần tất cả các thẻ bắt buộc)

- a. Bắt đầu trình soạn thảo văn bản và tạo một tài liệu mới.
- b. Nếu không bao gồm bất kỳ thẻ `<html>, <head> hoặc <body>`, hãy gõ như sau các câu lệnh. Lưu ý rằng các thẻ đóng không dành cho các thẻ <p> và cuối nhãn <b>.

`<H1> Hiểu Kiến trúc Client/Server </h1>`
`<P> Để thành công trong việc phát triển Web, bạn cần phải hiểu về cơ bản của kiến trúc client/server. Có rất nhiều định nghĩa về thuật ngữ`
`<i>client</i> và <i>server</i>. Trong client/server truyền thống thì kiến trúc, <b>server</b> thường là một số loại cơ sở dữ liệu mà khách hàng yêu cầu thông tin.`
`<P>từ <i>JavaScript 5th Edition</i> <br>`
`Bởi <b> Don Gosselin`

- c. Lưu tệp là **Architecture.html** trong thư mục của bạn

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/3.png"></p>

- d. Đóng tệp **Architecture.html** và mở nó trong Firefox hoặc trình duyệt ưa thích của bạn. Mặc dù tài liệu HTML không bao gồm tất cả các thẻ được yêu cầu, trình duyệt web hiển thị nó đúng, như hình dưới đây cho thấy.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/4.png"></p>

- e. Đóng trình duyệt web của bạn lại.

#### 1.3. Exercise 3 - Creating an XML Document that contains your mailing address(Bài tập 3 - Tạo một tài liệu XML có chứa địa chỉ gửi thư của bạn)

- a. Bắt đầu trình soạn thảo văn bản và tạo một tài liệu mới.
- b. Thêm các khai báo XML sau đây bao gồm version (phiên bản), encoding (mã hóa), và standalone (các thuộc tính độc lập):

`<?xml version="1.0" encoding="iso-8859-1" standalone="yes"?>`

- c. Gõ mở thẻ sau đây để bắt đầu tài liệu:

`<Mailing_Address>`

- d. Tiếp theo thêm các yếu tố sau đây có chứa địa chỉ gửi thư của bạn. Chắc chắn rằng thay thế văn bản trong mỗi cặp thẻ với thông tin của riêng bạn.

`<Name> tên của bạn </Name> <Address> Địa chỉ của bạn </Address>`

`<City> Thành phố của bạn </City> <State> Tiểu bang của bạn </State>`

`<Zip> mã zip của bạn </Zip>`

- e. Gõ thẻ đóng địa chỉ hộp thư, như sau:

`</Mailing_Address>`

- f. Lưu tệp dưới dạng **MailingAddress.xml** trong thư mục của bạn.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/5.png"></p>

- g. Đóng tệp trong trình soạn thảo văn bản của bạn.

#### 1.4 Exercise 4 - Creating an XML Document that stores data(bài tập 4 - Tạo một tài liệu XML lưu dữ liệu)

- a. Bắt đầu trình soạn thảo văn bản và tạo một tài liệu mới.
- b . Gõ khai báo XML, như sau:

`<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>`

- c. Kiểu tiếp theo là các thẻ mở và đóng cho một phần tử gốc có tên <books>:

`<Boook>`

`</ Books>`

- d. Lưu tập tin dưới dạng **Books.xml** trong thư mục *Chapter 1*.

- e. Mở tập tin trong trình duyệt của bạn. Nó sẽ xuất hiện như hình dưới đây cho thấy

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/6.png"></p>

- f. Đóng trình duyệt web của bạn lại.

----------------------------------------------

### Tài liệu dịch

[1] Lab Week 07: HTML5-XML-DTDs - Javascript
 http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm

 

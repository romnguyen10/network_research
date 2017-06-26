## COM320 Computer Network

> Tài liệu: COM320 Computer Networks and Operating Systems
>
> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **26/06/2017**

---------------------------------------------

### Mục lục

[1. xHTML-XML-DTDs](#1)

- [1.1. Create a basic HTML Page (tạo 1 trang HTML cơ bản)](#1.1)
- [1.2. Exercise 2 - Creating a HTML file without all required Tags (tạo tệp HTML mà không cần tất cả các thẻ được yêu cầu)](#1.2)
- [1.3. Exercise 3 - Creating an XML Document that contains your mailing address (tạo một Tài liệu XML có chứa địa chỉ gửi thư của bạn)](#1.3)
- [1.4. Exercise 4 - Creating an XML Document that stores data (tạo một Tài liệu XML lưu dữ liệu)](#1.4)
- [1.5. Exercise 5 - Introducing a case error into the books.xml document (giới thiệu một lỗi trường hợp trong tài liệu books.xml)](#1.5)
- [1.6. Exercise 6 - To add two <book> elements to the books.xml file (để thêm hai yếu tố <book> vào tệp books.xml)](#1.6)
- [1.7. Exercise 7 - To modify the books.xml file to include nested elements (sửa đổi tệp books.xml để bao gồm các phần tử lồng nhau)](#1.7)
- [1.8. Exercise 8 - To add a publisher attribute to each of the <book> elements (để thêm thuộc tính publisher vào mỗi phần tử <book>)](#1.8)
- [1.9. Exercise 9 - To add a publisher attribute to each of the <book> elements (để thêm thuộc tính publisher vào mỗi phần tử <book>)](#1.9)
- [1.10. Exercise 10 - To create a document that uses the Transitional DTD (để tạo một tài liệu sử dụng Transitional DTD)](#1.10)
- [1.11. Exercise 11 - To start creating the home page for the Don’s Pizza Web Site (để bắt đầu tạo trang chủ cho Trang web Don's Pizza)](#1.11)
- [1.12. Exercise 12 -To start creating the home page for the Don’s Pizza Web Site (để bắt đầu tạo trang chủ cho trang web Don's Pizza)](#1.12)
- [1.13. Exercise 13 -To add comments to the DonsPizza.html file (để thêm ý kiến vào tệp DonsPizza.html)](#1.13)
- [1.14. Exercise 14 - To validate a file (để xác nhận hợp lệ một file)](#1.14)

---------------------------------------------

<a name="1"></a>
### 1. xHTML-XML-DTDs

<a name="1.1"></a>
#### 1.1. Create a basic HTML Page (tạo 1 trang HTML cơ bản)

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
#### 1.2. Exercise 2 - Creating a HTML file without all required Tags (tạo tệp HTML mà không cần tất cả các thẻ bắt buộc):

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

<a name="1.3"></a>
#### 1.3. Exercise 3 - Creating an XML Document that contains your mailing address (tạo một tài liệu XML có chứa địa chỉ gửi thư của bạn):

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

<a name="1.4"></a>
#### 1.4 Exercise 4 - Creating an XML Document that stores data (tạo một tài liệu XML lưu dữ liệu):

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

<a name="1.5"></a>
#### 1.5. Exercise 5 - Introducing a case error into the books.xml document (giới thiệu một lỗi trường hợp trong tài liệu books.xml):

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở lại sách.xml
- b. Chỉnh sửa thẻ đóng `</books>` để nó là chữ hoa. Tệp của bạn sẽ xuất hiện như sau:

`<?xml version="1.0" encoding="ISO-8859-1" standalone="true"?>`

`<books>`

`</BOOKS>`

- c. Lưu tệp dưới dạng **Books.xml** và mở trong trình duyệt. Bạn sẽ nhận được một lỗi như thể hiện dưới đây. Như bạn thấy, thẻ đóng `</BOOKS>`không khớp với thẻ bắt đầu.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/9.png"></p>

- d. Trở lại tệp Books.xml trong trình soạn thảo văn bản của bạn và thay đổi thẻ `</BOOKS>` trở lại chữ cái thường và lưu tệp.

- e. Trở lại cửa sổ trình duyệt web hiển thị tệp **books.xml** và làm mới lại cửa sổ. Các tập tin nên mở một cách chính xác.

- f. Đóng cửa sổ trình duyệt web của bạn.

<a name="1.6"></a>
#### 1.6. Exercise 6 - To add two <book> elements to the books.xml file (để thêm hai yếu tố <book> vào tệp books.xml):

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở lại sách.xml và sửa đổi tài liệu như sau để bao gồm hai phần tử <book>. Đảm bảo thêm các phần tử trong phần tử gốc <books>. Hiện tại, không bao gồm thẻ đóng </ book>.

`<? Xml version = "1.0" encoding = "ISO-8859-1" standalone = "có"?>`

`<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>`

`<books>`

	`<book>A Farewell to Arms`

	`<book>Of Mice and Men`

`</books>`

- b. Lưu tệp dưới dạng **Books.xml** và mở trong trình duyệt. Bạn sẽ nhận được một lỗi như thể hiện dưới đây. Như bạn thấy, lỗi được nâng lên vì trình duyệt không thể tìm thấy thẻ kết thúc cho các phần tử <book>.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/7.png"></p>

- c. Quay lại tệp **Books.xml** trong trình soạn thảo văn bản của bạn và thêm thẻ đóng `</book>` vào mỗi phần tử `<book>` và lưu tệp.

`<? Xml version = "1.0" encoding = "ISO-8859-1" standalone = "có"?>`

`<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>`

`<books>`

	`<book>A Farewell to Arms</book>`

	`<book>Of Mice and Men</book>`

`</books>`

- d. Trở lại cửa sổ trình duyệt web hiển thị tệp **books.xml** và làm mới lại cửa sổ. Các tập tin nên mở một cách chính xác như dưới đây.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/8.png"></p>

<a name="1.7"></a>
#### 1.7. Exercise 7 -To modify the books.xml file to include nested elements (sửa đổi tệp books.xml để bao gồm các phần tử lồng nhau):

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở lại **Books.xml**

2. Thay thế phần tử `<book>` cho `A Farewell to Arms` với các phần tử lồng nhau sau có chứa thông tin về tên tác giả và tác giả của cuốn sách. Lưu ý rằng

`<title>` và `<author>` được đặt trong phần tử `<book>` và phần tử `<first_name>` và `<last_name>` được lồng trong phần tử author.

`<book>`

	`<title>A Farewell to Arms</title>`

	`<author>`

		`<first_name>Ernest</first_name>`

		`<last_name>Hemingway</last_name>`

	`</author>`

`</book>`

- c. Tiếp theo, thay thế phần tử `<book>` cho `Of Mice and Men` với các phần tử lồng nhau sau:

`<book>`

	`<title>Of Mice and Men</title>`

	`<author>`

		`<first_name>John</first_name>`

		`<last_name>Steinbeck</last_name>`

	`</author>`
	
`</book>`

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/10.png"></p>

<a name="1.8"></a>
#### 1.8. Exercise 8 - To add a publisher attribute to each of the <book> elements (để thêm thuộc tính publisher vào mỗi phần tử <book>):

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở lại **Books.xml**

- b. Sửa đổi thẻ mở cho phần tử *A Farewell to Arms*<book>  để nó bao gồm thuộc tính của nhà xuất bản với một giá trị được chỉ định là *"Scribner"*:

`<Book publisher = 'Scribner'>`

- c. Sửa đổi thẻ mở đầu của *Of Mice and Men*<book> để nó bao gồm thuộc tính của nhà xuất bản với giá trị được chỉ định là *"Penguin"*:

`<Book publisher = 'Penguin'>`

- d. Lưu tệp **Books.xml** và sau đó mở tệp đó trong trình duyệt. Màn hình của bạn trông giống như hình dưới đây.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/11.png"></p>

- e. Đóng cửa sổ trình duyệt của bạn lại.

<a name="1.9"></a>
#### 1.9. Exercise 9 - To add a publisher attribute to each of the <book> elements (để thêm thuộc tính publisher vào mỗi phần tử <book>):

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở lại **Books.xml**
- b. Thêm một phần tử ấn phẩm rỗng lồng vào phần *A Farewell to Arms* `<book>` như sau:

`<book publisher='Scribner'>` 

`<publication year='1929'/>`

`<title>A Farewell to Arms</title>` 

`<author>`

`<first_name>Ernest</first_name> <last_name>Hemingway</last_name>` 

`</author>` 

`</book>` 

- c. Bây giờ thêm một phần tử ấn phẩm rỗng lồng vào phần tử *Of Mice and Men* `<book>` như sau:

`<book publisher='Penguin'>`

`<publication year='1937'/>` 

`<title>Of Mice and Men</title>`

`<author>`

`<first_name>John</first_name>` 

`<last_name>Steinbeck</last_name>`

`</author>`

`</book>` 

- d. Save the **Books.xml** file and then open it in a browser. Your screen should look like the figure below.
- e. Đóng cửa sổ trình duyệt của bạn lại.

<a name="1.10"></a>
#### 1.10. Exercise 10 - To create a document that uses the Transitional DTD (để tạo một tài liệu sử dụng Transitional DTD):

- a. Bắt đầu trình soạn thảo văn bản của bạn và tạo một tài liệu mới


- b. Gõ khai báo mở <!DOCTYPE> sử dụng DTD chuyển tiếp, như sau:

`<!DOCTYPE html PUBLIC "- // W3C // DTD XHTML 1.0 Transitional // EN"`

`"Http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">`

- c. Gõ phần tử `<html>` như sau. Hãy nhớ rằng tất cả các trang Web phải bắt đầu và kết thúc bằng cặp thẻ `<html> ... </ html>`.

`<Html>`

`</Html>`

- d. Trong phần tử `<html>`, thêm các phần tử `<head>` và `<title>` sau đây vào tài liệu. Tiêu đề xuất hiện trong thanh tiêu đề của Trình duyệt Web. Hãy nhớ rằng phần tử `<head>` phải bao gồm một phần tử `<title>`. Phần tử `<title>` không thể tồn tại bên ngoài phần tử `<head>`

`<head>`

`<title>Great American Novel</title>`

`</head>`

- e. Tiếp theo, thêm phần tử `<body>` sau thẻ đóng `</html>`.

`<Body>`

`</Body>`

- f. Gõ các phần tử và văn bản sau đây giữa cặp thẻ `<body> ... </body>` để tạo phần thân của tài liệu.

`<p>It was a <s>dark and stormy night</s> <u>bright and sunny day</u>. <s>Lightning streaked the sky, followed by an angry explosion of thunder.</s> <u>High, soft clouds accented the sky and a soft wind gently swayed the trees.</u></p>`

- g. Lưu tệp là **Novel.html** và sau đó mở tệp đó trong trình duyệt. Màn hình của bạn trông như hình sau.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/12.png"></p>

- h. Đóng cửa sổ trình duyệt của bạn lại.

<a name="1.11"></a>
#### 1.11. Exercise 11 - To start creating the home page for the Don’s Pizza Web Site (để bắt đầu tạo trang chủ cho Trang web Don's Pizza)

- a. Bắt đầu trình soạn thảo văn bản của bạn và tạo một tài liệu mới và gõ khai báo <! DOCTYPE> đang mở sử dụng DTD nghiêm ngặt như sau:

`<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">`
`<html xmlns="http://www.w3.org/1999/xhtml">`

- b. Gõ phần tử `<html>` như sau. Hãy nhớ rằng tất cả các trang Web phải bắt đầu và kết thúc bằng cặp thẻ `<html> ... </html>`.

`<html>`
`<html>`

- c. Trong phần tử `<html>`, thêm phần tử `<head>` và `<title>` vào tài liệu. Tiêu đề xuất hiện trong thanh tiêu đề của Trình duyệt Web. Hãy nhớ rằng phần tử `<head>` phải bao gồm một phần tử `<title>`. Phần tử `<title>` không thể tồn tại bên ngoài phần tử `<head>`

`<head>`

`<title>Don’s Pizza Home Page</title>`

`</head>`

- d. Tiếp theo, thêm phần tử `<body>` sau thẻ đóng `</html>`.

`<body>`

`</body>`

- e. Gõ các phần tử và văn bản sau đây giữa cặp thẻ `<body> ... </body>` để tạo phần thân của tài liệu.

`<p><b>Today's special</b>: buy a large meat lover's or vegetarian pizza and receive a free Caesar salad and two liters of Diet Pepsi! Out meat lover's pizza is covered with loads of pepperoni, savory Italian sausage, smoked bacon, hamburger, mushrooms, and extra cheese. Our vegetarian pizza has lots of mushrooms, black olives, bell peppers, onions, artichoke hearts, and fresh tomatoes. </p>`

- f. Lưu tệp là **DonsPizza.html** và sau đó mở tệp đó trong trình duyệt. Màn hình của bạn trông giống như hình dưới đây.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/13.png"></p>

- g. Đóng cửa sổ trình duyệt của bạn lại.

<a name="1.12"></a>
#### 1.12. Exercise 12 -To start creating the home page for the Don’s Pizza Web Site (để bắt đầu tạo trang chủ cho trang web Don's Pizza)


- a. Bắt đầu trình soạn thảo văn bản của bạn và tạo một tài liệu mới và gõ khai báo `<!DOCTYPE>` đang mở sử dụng DTD nghiêm ngặt như sau:

`<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">`
`<html xmlns="http://www.w3.org/1999/xhtml">`

- b. Gõ phần tử `<html>` như sau. Hãy nhớ rằng tất cả các trang Web phải bắt đầu và kết thúc bằng cặp thẻ `<html> ... </html>`.

`<html>`
`<html>`

- c. Trong phần tử `<html>`, thêm phần tử `<head>` và `<title>` vào tài liệu. Tiêu đề xuất hiện trong thanh tiêu đề của Trình duyệt Web. Hãy nhớ rằng phần tử `<head>` phải bao gồm một phần tử `<title>`. Phần tử `<title>` không thể tồn tại bên ngoài phần tử `<head>`

`<head>`

`<title>Don’s Pizza Home Page</title>`

`</head>`

- d. Tiếp theo, thêm phần tử `<body>` sau thẻ đóng `</html>`.

`<body>`

`</body>`

- e. Gõ các phần tử và văn bản sau đây giữa cặp thẻ `<body> ... </body>` để tạo phần thân của tài liệu.

`<p><b>Today's special</b>: buy a large meat lover's or vegetarian pizza and receive a free Caesar salad and two liters of Diet Pepsi! Out meat lover's pizza is covered with loads of pepperoni, savory Italian sausage, smoked bacon, hamburger, mushrooms, and extra cheese. Our vegetarian pizza has lots of mushrooms, black olives, bell peppers, onions, artichoke hearts, and fresh tomatoes.</p>`

- f. Lưu tệp là **DonsPizza.html** và sau đó mở tệp đó trong trình duyệt. Màn hình của bạn trông giống như hình dưới đây.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/13.png"></p>

- g. Đóng cửa sổ trình duyệt của bạn lại.

<a name="1.13"></a>
#### 1.13. Exercise 13 -To add comments to the DonsPizza.html file (để thêm ý kiến vào tệp DonsPizza.html)

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở DonsPizza.html.


- b. Trên đầu tập tin, phía trên tờ khai <! DOCTYPE>, hãy thêm các nhận xét sau. Hãy chắc chắn sử dụng tên của bạn và ngày hôm nay.

`<!- -
Home page for Don’s Pizza : Pizza Hut
Your name : romnguyen
Today’s date: 26/06 - - >`

CHÚ Ý: Những dấu gạch ngang ở trên nên là dấu gạch ngang trên chữ cái bàn phím p lặp lại hai lần ... ..

- c. Lưu **DonsPizza.html** và sau đó mở nó trong trình duyệt để xác nhận ý kiến của bạn không xuất hiện.

- d. Đóng cửa sổ trình duyệt web của bạn.

<a name="1.14"></a>
#### 1.14. Exercise 14 - To validate a file (để xác nhận hợp lệ một file)

- a. Bắt đầu trình soạn thảo văn bản của bạn và mở **DonsPizza.html**.

- b. Thêm phần tử `<meta>` sau đây ngay phía trên thẻ đóng `</head>`

`<meta http-equiv="Content-Type(nội dung)"
    content="text/html; charset=iso-8859-1" />`

- c. Khởi động trình duyệt Web của bạn và nhập URL cho trang Tải lên Dịch vụ Xác nhận Đánh dấu Mã W3C trong hộp địa chỉ:

http://validator.w3.org/#validate_by_upload

- d. Nhấp vào nút duyệt để hiển thị hộp thoại Choose file.

- e. Trong hộp thoại Chọn tệp, điều hướng đến vị trí bạn đã lưu tệp **DonsPizza.html**. Định vị và mở tệp. Đường dẫn thư mục ổ đĩa và tên tệp sẽ xuất hiện trong hộp Tệp tin trên trang tải lên.

- f. Nhấp vào nút **Validate This File**. Dịch vụ Xác nhận Đánh dấu của W3C xác nhận hợp lệ tài liệu và trả kết quả hiển thị bên dưới.

<p align="center"><img src="https://github.com/romnguyen10/network_research/blob/master/Task03_COM320_Computer_Network/Week07/Lab/Image/13.png"></p>

- g. Đóng cửa sổ trình duyệt web của bạn.

----------------------------------------------

### Tài liệu dịch

[1] Lab Week 07: HTML5-XML-DTDs - Javascript
 http://scisweb.ulster.ac.uk/~kevin/com320/notes.htm

 

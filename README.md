#**Markdown**

> Tài liệu: Markdown

> Thực hiện: **Nguyễn Tấn Phát**
> 
> Cập nhật lần cuối: **20/02/2017**

## Mục lục

[1. Tìm hiểu về Markdown](#timhieu)

- [1.1 Markdown là gì?](#gt)

- [1.2 Markdown dùng để làm gì?](#ud)

- [1.3 Xu hướng sử dụng Markdown](#xuhuong)

[2. Các cú pháp thường sử dụng:](#cuphap)

- [2.1. Header](#Header)

- [2.2. Bold](#Bold)

- [2.3. Italic](#Italic)

- [2.4. Table](#Table)

- [2.5. Image](#Image)

- [2.6. Link](#Link)

- [2.7. Trích dẫn](#td)



...

[3. Các công cụ viết Markdown:](#congcu)

[4. Tổng kết:](#tongket)

[5. Tài liệu tham khảo:](#thamkhao)

---


<a name="timhieu"></a>
### **1. Tìm hiểu về Markdown**

<a name="gt"></a>
#### 1.1. Markdown là gì?

Aaron Swartz và John Gruber đã tạo ra ngôn ngữ Markdown năm 2004 với mục tiêu tạo ra 
một định dạng văn bản thô "dễ viết, dễ đọc, dễ dàng chuyển thành XHTML (hoặc HTML).
Một số trang web như GitHub, reddit, Diaspora, Stack Exchange, OpenStreetMap,
SourceForge sử dụng các biến thể của Markdown trong hệ thống của mình nhằm đơn giản
hóa ngôn ngữ XHTML hoặc HTML,...

<a name="ud"></a>
#### 1.2. Markdown dùng để làm gì?

- Chuyển đổi đoạn văn bản đã đánh dấu theo chuẩn Markdown sang XHTML hoặc HTML 
một cách dễ dàng, Markdown rất dễ sử dụng.
- Viết sách, báo, truyện, tin tức, blog,...
- Ứng dụng trên một số trang web như Github,...

<a name="xuhuong"></a>
####1.3 Xu hướng sử dụng Markdown:

Ngày nay HTML là ngôn ngữ lập trình Web rất phổ biến, nhưng rất khó để có thể rút
ngắn thời gian thành thạo nó vì cú pháp HTML không đơn giản. Để thuận lợi cho 
công việc ngta chọn Markdown ngày một nhiều hơn. markdown cũng ngày càng được cải tiến.

<a name="cuphap"></a>
### **2. Các cú pháp thường sử dụng**

<a name="Header"></a>
#### 2.1. Header

Tiêu đề được thiết lập bằng cách sử dụng dấu # phía trước. Số lượng dấu 
thăng thể hiện độ to nhỏ của tiêu đề. Dấu thăng càng nhiều tiêu đề càng nhỏ.
Tối đa 6 dấu.
ví dụ:
```
H1 : # Header 1
H2 : ## Header 2
H3 : ### Header 3
H4 : #### Header 4
H5 : ##### Header 5
H6 : ###### Header 6
```
hiển thị:

Header 1
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6

<a name="Bold"></a>
#### 2.2. Bold

Để in đậm 1 đoạn text ta chỉ cần thêm 2 dấu ** vào đầu và 2 dấu ## vào cuối 
đoạn text đó.
vd: 

`**Nguyễn Tấn Phát**`

hiển thị:

**Nguyễn Tấn Phát**

<a name="Italic"></a>
#### 2.3. Italic

Để in nghiêng 1 đoạn text ta chỉ cần thêm 1 dấu * vào đầu và 1 dấu # vào cuối
đoạn text đó.
vd:

`*Nguyễn Tấn Phát*`

hiển thị:

*Nguyễn Tấn Phát*

<a name="Table"></a>
#### 2.4. Table

Bạn có thể sử dụng cú pháp sau để tạo bảng:
vd: 
```
| Item     | Value | Qty   |
| :------- | ----: | :---: |
| Computer | $1600 |  5    |
| Phone    | $12   |  12   |
| Pipe     | $1    |  234  |'
```

hiển thị: 

| Item     | Value | Qty   |
| :------- | ----: | :---: |
| Computer | $1600 |  5    |
| Phone    | $12   |  12   |
| Pipe     | $1    |  234  |

<a name="Image"></a>
#### 2.5. Image

Để chèn link ảnh có 3 cách:

c1 <img src="link_ảnh" >

c2 ![chú_thích](link_ảnh)

c3 ![chú_thích](/đường_dẫn_tới_vị_trí_lưu_ảnh)

<a name="Link"></a>
#### 2.6. Link

Để gán link vào, rất đơn giản chỉ cần paste đường link vào thôi.

vd : https://github.com

Nếu đường link quá dài bạn có thể rút ngắn bằng cách:

[tên_rút_ngắn](https://github.com)

<a name="td"></a>
#### 2.7. trích dẫn

-- Có thể sử dụng cặp dấu `` hoặc `````` để tạo trích dẫn:



   `trích dẫn `

<a name="congcu"></a>
### **3.Các công cụ viết Markdown**

bạn có thể viết markdown online qua các trang web:

- https://stackedit.io/editor


- https://jbt.github.io/markdown-editor/


- http://www.tablesgenerator.com/markdown_tables


- https://markable.in/editor/

Bên cạnh đó bạn cũng có thể viết trên **notepad**, **vi**, **sublime**,...

<a name="tongket"></a>
### **5.Tổng kết**

##### Ưu điểm.


Đây là một ngôn ngữ cơ bản dễ dùng giúp ta có thể sử dụng rất nhiều nơi 
với cú pháp cơ bản. Mất khoảng 2 giờ là ta có thể học cách sử dụng.

##### Nhược điểm.


Nhược điểm lớn nhất của Markdown có lẽ là khả năng cộng tác trong Markdown 
và theo giỏi những thay đổi. Vì đơn giản nên chỉ có thể dùng cho các dự án nhỏ lẻ,
bài blog và tất nhiên những dự án lớn hay những quyển sách cần nhiều hơn những thứ
mà Markdown hỗ trợ.

<a name="thamkhao"></a>
### **5.Tài liệu tham khảo**

[1] https://nguyenthethang.com/2013/08/16/keyword-ngon-ngu-markdown-la-gi-what-is-markdown/

[2] https://github.com/hocchudong/git-github-for-sysadmin

[3] https://help.ghost.org/hc/en-us/articles/224410728-Markdown-Guide

[4] https://en.wikipedia.org/wiki/Markdown




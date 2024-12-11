
## [Lab 11: Reflected XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

![Yêu cầu lab 11](../image/lab11/0.png)

main web

![Alt text](../image/lab11/01.png)

có 3 chức năng

1. `Home`
2. `Search` --> test

![Alt text](../image/lab11/02.png)

search gì trả về y chang --> Reflected XSS

![Alt text](../image/lab11/03.png)

result trong thẻ `h1`

![Alt text](../image/lab11/04.png)

--> add: `<script>alert(1)</script>`

![Alt text](../image/lab11/05.png)

xuất hiện cảnh báo

![Alt text](../image/lab11/06.png)

solve the lab

![Alt text](../image/lab11/07.png)

3. `View post`

> **Test bằng Active Scan**

![Alt text](../image/lab11/08.png)

## [Lab 12: Stored XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

![Yêu cầu lab 12](../image/lab12/0.png)

main web

![Alt text](../image/lab12/01.png)

2 chức năng

1. `Home`

2. `View post` --> có thêm chức năng `Post comment`

![Alt text](../image/lab12/02.png)

các thông tin của comment đều nằm trong thẻ html

![Alt text](../image/lab12/03.png)

add alert

![Alt text](../image/lab12/04.png)

![Alt text](../image/lab12/05.png)

solve the lab

![Alt text](../image/lab12/06.png)

## [Lab 18: Stored XSS into anchor href attribute with double quotes HTML-encoded](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded)

- Mô tả lab: Lỗi XSS ở chức năng comment

- Mục tiêu: thực hiện submit comment gọi hàm alert khi click vào author name

![Alt text](../image/lab18/0.png)

main web

![Alt text](../image/lab18/01.png)

Có 2 chức năng

1. Home

2. View post, khi truy cập ta có thêm Chức năng comment --> liên quan đến database --> Stored XSS

![Alt text](../image/lab18/02.png)

Test thử XSS bằng cách chèn script `<script>alert(1)</script>`

![Alt text](../image/lab18/03.png)

thực hiện không thành công, vì ký tự `<` đã bị encode

![Alt text](../image/lab18/04.png)

![Alt text](../image/lab18/05.png)

Ta sẽ tìm cách khác để chèn XSS, chú ý rằng khi click vào author name thì nó sẽ chuyển ta đến website mà ta đã comment

![Alt text](../image/lab18/06.png)

![Alt text](../image/lab18/07.png)

Ta biết đến có protocol có thể thực hiện javascript `javascript:alert(1)`

![Alt text](../image/lab18/08.png)![Alt text](../image/lab18/09.png)

thực hiện comment

![Alt text](../image/lab18/10.png)![Alt text](../image/lab18/11.png)

submit và solve lab

![Alt text](../image/lab18/12.png)
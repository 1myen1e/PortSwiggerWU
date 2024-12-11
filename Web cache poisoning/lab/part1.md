
## [Lab 1: Web cache poisoning with an unkeyed header](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-an-unkeyed-header)

```
- Mô tả lab: Lỗi Web cache poisoning xử lý đầu vào từ header không khóa theo cách không an toàn.

- Mục tiêu: đầu độc cache bằng thực hiện (document.cookie).

- Hint: sử dụng (X-Forwarded-Host).
```
![Yêu cầu lab 1](../image/lab1/0.png)

![main web](../image/lab1/01.png)

Khi truy cập lần 1: ta sẽ gặp header `X-Cache: miss`

![Alt text](../image/lab1/02.png)

**X-Cache: miss:** Ngược lại, khi bạn thấy thông báo này, nó cho biết rằng yêu cầu của bạn không có sẵn trong cache của máy chủ. Do đó, máy chủ phải thực hiện các xử lý bổ sung, như truy vấn cơ sở dữ liệu hoặc tạo trang web từ đầu trước khi trả về kết quả cho bạn. Điều này có thể mất thời gian hơn và tăng tải cho máy chủ.

Khi truy cập lần 2, `miss` sẽ đổi thành `hit`

![Alt text](../image/lab1/03.png)

**X-Cache: hit:** Khi bạn thấy thông báo này trong tiêu đề HTTP response từ máy chủ web, nó có nghĩa rằng yêu cầu của bạn đã được tìm thấy trong cache và máy chủ đã trả về nội dung từ cache thay vì tạo yêu cầu mới đối với máy chủ hoặc cơ sở dữ liệu. Điều này thường xảy ra khi trang web đã được truy cập gần đây và nó vẫn còn trong bộ nhớ cache của máy chủ.

![Alt text](../image/lab1/04.png)

![Alt text](../image/lab1/05.png)

xem file tracking.js

![Alt text](../image/lab1/06.png)

thực hiện gọi đến file `tracking.js` mới, tạo file mới trên `Exploit server`

![Alt text](../image/lab1/07.png)

sửa đổi X-Forwarded-Host và send đến khi gặp `X-Cache: hit`

![Alt text](../image/lab1/08.png)![Alt text](../image/lab1/09.png)

F5 kiểm tra xem có alert thành công không

![Alt text](../image/lab1/10.png)

solve lab

![Alt text](../image/lab1/11.png)

> **Test bằng Insertion Point**

![Alt text](../image/lab1/12.png)

![Alt text](../image/lab1/13.png)

![Alt text](../image/lab1/14.png)

![Alt text](../image/lab1/15.png)

![Alt text](../image/lab1/16.png)


## [Lab 2: Web cache poisoning with an unkeyed cookie](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-an-unkeyed-cookie)

![Yêu cầu lab 2](../image/lab2/0.png)

```
- Mô tả lab: 

- Mục tiêu:

```

![main web](../image/lab2/01.png)

![Alt text](../image/lab2/02.png)![Alt text](../image/lab2/03.png)

dấu gạch ngang ("-") được sử dụng để bao gồm chuỗi "alert(1)" bên trong chuỗi lớn hơn, mà không cần phải sử dụng dấu escape hoặc đổi loại dấu nháy. Điều này giúp bạn xây dựng một chuỗi chứa JavaScript code nhúng (cross-site scripting, XSS) mà không cần phải trốn thoát các dấu nháy.

![Alt text](../image/lab2/04.png)![Alt text](../image/lab2/05.png)

![Alt text](../image/lab2/06.png)

solve

![Alt text](../image/lab2/07.png)

> **Chưa test tool ra :)**

## [Lab 3: Web cache poisoning with multiple headers](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-multiple-headers)

![Yêu cầu lab 3](image.png)

```
- Mô tả lab:

- Mục tiêu:
```

![main web](image-1.png)

![Alt text](image-2.png)![Alt text](image-3.png)

test thêm `X-Forwarded-Host` thì không thấy có gì,  tuy nhiên khi thêm  `X-Forwarded-Scheme` thì status code thay đổi thành `302`

![Alt text](image-4.png)![Alt text](image-5.png)

![Alt text](image-6.png)

![Alt text](image-7.png)![Alt text](image-8.png)

![Alt text](image-9.png)

![Alt text](image-10.png)

# [Lab 1: CSRF vulnerability with no defenses](https://portswigger.net/web-security/csrf/lab-no-defenses)

![Yêu cầu lab 1](../image/lab1/0.png)

> - **Mô tả lab:** Lỗi `CSRF` ở chức năng thay đổi email.
>
> - **Mục tiêu:** tạo `HTML` thực hiện tấn công `CSRF` để thay đổi email của người dùng và tải lên exploit server.

Đăng nhập `wiener:peter`, ta thấy có chức năng `Update email`  (1, 3)

![Alt text](../image/lab1/01.png)

Quan sát Request, ta thấy không hề có `csrf token` để xác nhận với mỗi lần thay đổi email (2)

![Alt text](../image/lab1/02.png)

→ Đủ điều kiện để thực hiện tấn công CSRF, do không thể để email trùng với tài khoản khác → dùng email khác `b@test`

![Alt text](../image/lab1/03.png)

`Delivery to victim`

![Alt text](../image/lab1/04.png)

Solve lab

![Alt text](../image/lab1/05.png)

# [Lab 2: CSRF where token validation depends on request method](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)

![Yêu cầu lab 2](../image/lab2/0.png)

> - **Mô tả lab:** Vẫn lỗi như **lab 1**, tuy nhiên có cố gắng chặn các cuộc tấn công CSRF nhưng chỉ áp dụng biện pháp phòng vệ cho một số loại request.
>
> - **Mục tiêu:** cũng như **lab 1**.

Đăng nhập với `wiener:peter`, ta thấy có chức năng `Update email` (1, 3)

![Alt text](../image/lab2/01.png)

Quan sát Request gửi đi thì ta thấy đã có `CSRF token` xác nhận

![Alt text](../image/lab2/02.png)

Ta sẽ kiểm tra xem có thực sự cần đến `CSRF token`. Vì sử dụng `POST` nhưng bỏ tham số `csrf` đi thì không thành công do thiếu tham số nên ta sẽ thực hiện bằng cách đổi `method` thành `GET`

![Alt text](../image/lab2/03.png)

Và kết quả vẫn `Update email` thành công (2)

![Alt text](../image/lab2/04.png)

→ Tấn công CSRF thôi

![Alt text](../image/lab2/05.png)

`Delivery to victim`

![Alt text](../image/lab2/06.png)

Solve lab

![Alt text](../image/lab2/07.png)

# [Lab 3: CSRF where token validation depends on token being present](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-token-being-present)

![Yêu cầu lab 3](../image/lab3/0.png)

> - **Mô tả lab:** cũng lỗi như 2 lab trên.
>
> - **Mục tiêu:** và mục tiêu cũng vẫn vậy.

Đăng nhập với `wiener:peter`, ta thấy có chức năng `Update email` (1, 3)

![Alt text](../image/lab3/01.png)

Request có chứa `CSRF Token`

![Alt text](../image/lab3/02.png)

Tuy nhiên bỏ đi thì vẫn hoàn toàn `Update email` thành công (2)

![Alt text](../image/lab3/03.png)

→ Tấn công CSRF thôi

![Alt text](../image/lab3/04.png)

Gửi cho nạn nhân

![Alt text](../image/lab3/05.png)

SOLVE

![Alt text](../image/lab3/06.png)

# [Lab 4: CSRF where token is not tied to user session](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session)

![Yêu cầu lab 4](../image/lab4/0.png)

> - **Mô tả lab:** Lỗi `CSRF` ở chức năng thay đổi email, sử dụng token để ngăn chặn tấn công này nhưng được tích hợp xử lý cùng session.
>
> - **Mục tiêu:** Vẫn như các lab trên thôi.

Đăng nhập với `wiener:peter`, ta thấy có chức năng `Update email` (1, 3)

![Alt text](../image/lab4/02.png)

Request có chứa `CSRF token` bảo vệ

![Alt text](../image/lab4/03.png)

Đăng nhập với `carlos:montoya`

![Alt text](../image/lab4/04.png)

Do token không được xử lý cùng với session nên ta sẽ tiến hành đổi CSRF token của `wiener` và `carlos` với nhau xem session của wiener có thay đổi email được của carlos không

![Alt text](../image/lab4/05.png)

![Alt text](../image/lab4/06.png)

thành công

![Alt text](../image/lab4/07.png)

thử ngược lại lấy CSRF của carlos cho wiener xem có đổi được không và đương nhiên là vẫn thành công

![Alt text](../image/lab4/08.png)![Alt text](../image/lab4/09.png)

→ Tấn công CSRF

![Alt text](../image/lab4/10.png)

vì mỗi khi F5 sẽ thay đổi CSRF token nên trước khi delivery cho victim ta đổi CSRF token đã

![Alt text](../image/lab4/11.png)

![Alt text](../image/lab4/12.png)

delivery solve lab

![Alt text](../image/lab4/13.png)

# [Lab 5: CSRF where token is tied to non-session cookie](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie)

![Yêu cầu lab 5](../image/lab5/0.png)

> - **Mô tả lab:**
>
> - **Mục tiêu:**

main web

![Alt text](../image/lab5/01.png)

login `wiener:peter`

![Alt text](../image/lab5/02.png)

có cả CSRF token và key

![Alt text](../image/lab5/03.png)

![Alt text](../image/lab5/04.png)

đổi cả 2 cái ở 2 account cho nhau xem

![Alt text](../image/lab5/05.png)

vẫn thay được bình thường

![Alt text](../image/lab5/06.png)

![Alt text](../image/lab5/07.png)

![Alt text](../image/lab5/08.png)

→ Tấn công CSRF

`Search` không có CSRF bảo vệ → chèn cookies vì `csrfKey` ở Cookie

![Alt text](../image/lab5/09.png)

`/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None`


→ đổi script thành thẻ img dẫn đến src là endpoint trên thì tự động thực hiện submit

`
<img src="https://0aa50085048405c88502a0580056007a.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=ZYhZvnlxhRclyG8Yfz6BuXMuxgpY9l6P%3b%20SameSite=None" onerror="document.forms[0].submit()">
`

![Alt text](../image/lab5/10.png)

View exploit để xem có thay đổi thành công không

![Alt text](../image/lab5/11.png)

solve lab thôi

![Alt text](../image/lab5/12.png)


# [Lab 6: CSRF where token is duplicated in cookie](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie)

![Yêu cầu lab 6](../image/lab6/0.png)

> - **Mô tả lab:**
>
> - **Mục tiêu:**

![main web](../image/lab6/01.png)

login `wiener:peter`, `Update email`

![Alt text](../image/lab6/02.png)

Request, cả Session và body đều có csrf token giống nhau

![Alt text](../image/lab6/03.png)

thay cả 2 thì mới thay đổi thành công

![Alt text](../image/lab6/04.png)

![Alt text](../image/lab6/05.png)

Search

![Alt text](../image/lab6/06.png)

→ thay đổi script auto submit

![Alt text](../image/lab6/07.png)

![Alt text](../image/lab6/08.png)
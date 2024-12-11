## [Lab 1: HTTP request smuggling, basic CL.TE vulnerability](https://portswigger.net/web-security/request-smuggling/lab-basic-cl-te)

![Lab 1](../image/lab1/lab.png)

Mô tả lab:
- có FE và BE, FE Không hỗ trợ chunked encoding
- FE từ chối request không sử dụng method GET hoặc POST

Goal:
- chuyển lậu một yêu cầu đến BE, để yêu cầu tiếp theo được xử lý bởi BE dường như sử dụng phương thức `GPOST`.

main web

![Alt text](../image/lab1/0.png)

không sử dụng method khác GET và POST

![Alt text](../image/lab1/1.png)

lấy request POST test

![Alt text](../image/lab1/2.png)

![Alt text](../image/lab1/3.png)

test, send lần 1 chưa thì ra `Invalid blog post ID`

![Alt text](../image/lab1/9.png)

nhưng send lần 2 thì lỗi rồi

![Alt text](../image/lab1/4.png)

![Alt text](../image/lab1/5.png)

solve the lab

![Alt text](../image/lab1/6.png)

![Alt text](../image/lab1/7.png)

![Alt text](../image/lab1/8.png)

> **Test bằng Active Scan**

![Alt text](../image/lab1/10.png)

![Alt text](../image//lab1/11.png)

![Alt text](../image/lab1/12.png)


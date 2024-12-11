# [Lab 1: Reflected XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

![Yêu cầu lab 1](../image/lab1/0.png)

> - **Mô tả lab:** Lỗ hổng Reflected XSS trong chức năng `Search`.
> 
> - **Mục tiêu:** Thực hiện tấn công gọi chức năng `alert`.

`Search`: khi search gì thì kết quả trả về ngay lập tức giống như đã search → ta nghĩ đến `Reflected XSS`

![search=a](../image/lab1/01.png)

add script alert

![Alt text](../image/lab1/02.png)

solve the lab

![Alt text](../image/lab1/03.png)

> **Test bẳng Active Scan**

![req](../image/lab1/04.png)

# [Lab 2: Stored XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

![Yêu cầu lab 2](../image/lab2/0.png)

> - **Mô tả lab:** Lỗ hổng `Stored XSS` trong chức năng `Comment`
> 
> - **Mục tiêu:** gửi `comment` gọi chức năng `alert` khi bài đăng trên blog được xem.

Khi `View post`: xem blog post, trong này có chức năng mới `Post comment`

![Alt text](../image/lab2/01.png)

nhất định comment sẽ được lưu lại rồi → `Stored XSS`, test ở một paramater bất kỳ

![Alt text](../image/lab2/02.png)

Mỗi khi truy cập post đó ta sẽ luôn thấy thông báo `1` được hiển thị

![Alt text](../image/lab2/03.png)

solve lab luôn

![Alt text](../image/lab2/04.png)

> **Test bẳng New Scan**

![Alt text](../image/lab2/05.png)

# [Lab 3: DOM XSS in `document.write` sink using source `location.search`](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

![Yêu cầu lab 3](../image/lab3/0.png)

> - **Mô tả lab:** Lỗi `DOM-based XSS` ở chức năng `Search`. Sử dụng `document.write` để ghi dữ liệu ra trang. Và nó được gọi với dữ liệu từ `location.search` mà có thể kiểm soát bnawgf cách sử dụng URL.
> 
> - **Mục tiêu:** Thực hiện tấn công gọi hàm `alert`.

- `Search`:

khi send request search

![Alt text](../image/lab3/02.png)

xem response, ta thấy có đoạn `script` thực hiện searcg có sử dụng sink `document.write` và source `window.location` (`location.search`)

![Alt text](../image/lab3/03.png)

chú ý query để test

ta nhận query chính là chuỗi tìm kiếm mà ta nhập, chú ý kết thúc thẻ → payload: `'"><script>alert(1)</script>`

![Alt text](../image/lab3/04.png)

xuất hiện cảnh báo

![Alt text](../image/lab3/05.png)

solve the lab

![Alt text](../image/lab3/06.png)

> **Test bằng Active Scan**

bị DOM-based XSS

![Alt text](../image/lab3/07.png)

# [Lab 4: DOM XSS in `document.write` sink using source `location.search` inside a select element](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element)

![Yêu cầu lab 4](../image/lab4/0.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

![main web](../image/lab4/01.png)

có 2 chức năng

- Home

- `View details`: xem thông tin sản phẩm, chứa chức năng mới `Check stock`

![Alt text](../image/lab4/02.png)

view details 1 sản phẩm bất kỳ

![Alt text](../image/lab4/03.png)

ta thấy xuất hiện đoạn script checkstock using `window.location.search` để tìm tên store và sử dụng `document.write` với thể `select` để chọn ra store

![Alt text](../image/lab4/04.png)

→ payload: "></select><script>alert(1)</script>

thêm storeId để check

![Alt text](../image/lab4/05.png)

add alert

![Alt text](../image/lab4/06.png)

xuất hiện cảnh báo

![Alt text](../image/lab4/07.png)

![Alt text](../image/lab4/08.png)

solve the lab

![Alt text](../image/lab4/09.png)

> **Test bằng Active Scan**

# [Lab 5: DOM XSS in `innerHTML` sink using source `location.search`](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink)

![Yêu cầu lab 5](../image/lab5/0.png)

> - **Mô tả lab:** chứa lỗ hổng DOM XSS trong chức năng tìm kiếm, nó sử dụng `innerHTML` để thay đổi nội dung HTML của phần tử div, sử dụng dữ liệu từ `location.search`.
> 
> - **Mục tiêu:** Thực hiện tấn công gọi hàm alert.

![main web](../image/lab5/01.png)

3 chức năng

1. `Home`
2. `Search`: test

search 1 cái gì đó

![Alt text](../image/lab5/02.png)

ta thấy đoạn script sử dụng sink `innerHTML` lấy chuỗi message nhập vào và sử dụng source `window.location.search` để thực hiện search

![Alt text](../image/lab5/03.png)

thay thế message thành script alert → thử `script`  thì không thấy có phản hổi gì vì nó nằm trong thẻ `span` mà thẻ `span` chỉ là một thẻ chứa văn bản hoặc nội dung phụ thuộc vào nhu cấu và không phải là một phẩn của DOM → payload `<img src=1 onerror=alert(1)>`

![Alt text](../image/lab5/04.png)

xuất hiện cảnh báo

![Alt text](../image/lab5/05.png)

solve lab

![Alt text](../image/lab5/06.png)

3. `View post` → khỏi test luôn :v

> **Test bằng Active Scan**

![Alt text](../image/lab5/07.png)

# [Lab 6: DOM XSS in jQuery anchor `href` attribute sink using `location.search` source](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink)

![Yêu cầu lab 6](image.png)

![main web](../image/lab6/01.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

có 3 chức năng

1. `Home`
2. `Submit feedback` → test

khi vào trang ta sẽ thấy đoạn script có sử dụng attr `href` để chuyển trang và `window.location.search`

![Alt text](../image/lab6/02.png)

giờ ta thay đổi `href` coi nó có back ta đến trang khác không

![Alt text](../image/lab6/03.png)

click `back` thôi

kết quả sẽ chuyển → giờ test JavaScript, các trình duyệt có hỗ trợ method `javascript` sử dụng trên URL → href lúc này sẽ là `javascript:alert(1)`

ví dụ trên trình duyệt `Edge`

![Alt text](../image/lab6/04.png)![Alt text](../image/lab6/05.png)

thử href với `alert(1)` thử xem sao, hiện cảnh báo rồi

![Alt text](../image/lab6/06.png)

test `alert(1)` mà solve luôn rồi

![Alt text](../image/lab6/07.png)

3. `View post` → khỏi test

> **Test bằng Active Scan**

mỗi lần quét 1 kiểu =((((

![Alt text](../image/lab6/08.png)

![Alt text](../image/lab6/09.png)

# [Lab 7: DOM XSS in jQuery selector sink using a hashchange event](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event)

![Yêu cầu lab 7](../image/lab7/0.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

![main web](../image/lab7/01.png)

các chức năng

- `Exploit server`: 

![Alt text](../image/lab7/02.png)

- `Home`

- `View post` → test

tại trang chủ của web ta có thấy đoạn `script` sink selector `blog-list` và source `window.location.hash` cho ` scrollIntoView` để tự động cuộn đến một thành phẩn cụ thể trên trang

![Alt text](../image/lab7/03.png)

`hash` có thể được người dùng kiểm soát → có thể chèn vào sink selecter `$()` → đưa vòa bằng cách bắt đầu bằng ký tự hash `#` → payload: `<iframe width="940" height="940" src="https://vulnerable-website.com#" onload="this.src+='<img src=1 onerror=alert(1)>'">`

go to exploit tạo `iframe` độc hại

![Alt text](../image/lab7/04.png)

view exploit coi kết quả, thành công

![Alt text](../image/lab7/05.png)

add `print()`, nên `Store` lại

![Alt text](../image/lab7/06.png)

view exploit xem thử kết quả

![Alt text](../image/lab7/07.png)

ok, thành công, now `Deliver exploit to victim` and solve lab

![Alt text](../image/lab7/08.png)

> **Test bằng Active Scan**

![Alt text](../image/lab7/09.png)

![Alt text](../image/lab7/10.png)

![Alt text](../image/lab7/11.png)

![Alt text](../image/lab7/12.png)

# [Lab 8: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression)

![Yêu cầu lab 8](../image/lab8/0.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

![main web](../image/lab8/01.png)

3 chức năng

1. `Home`
2. `Search`

![Alt text](../image/lab8/02.png)

![Alt text](../image/lab8/03.png)

quan sát response ta thấy `<` đã bị encode

![Alt text](../image/lab8/04.png)

dấu `'` cũng bị encode

![Alt text](../image/lab8/05.png)

![Alt text](../image/lab8/06.png)

![Alt text](../image/lab8/07.png)

![Alt text](../image/lab8/08.png)

![Alt text](../image/lab8/06.png)

3. `View post`

> **Test bằng Active Scan**


# [Lab 9: Reflected DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected)

![Yêu cầu lab 9](../image/lab9/0.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

![main web](../image/lab9/01.png)

3 chức năng

1. `Home`
2. `Search`

khi ta search

![Alt text](../image/lab9/02.png)

![Alt text](../image/lab9/03.png)

ta thấy response có trả về y chang ta search → Reflected XSS, ngoài ra nó còn gọi đến `search-result` → DOM-based XSS.

ta xem file xem có gì

![Alt text](../image/lab9/04.png)

![Alt text](../image/lab9/05.png)

sau đó sẽ là kết quả nhận được

![Alt text](../image/lab9/06.png)

ta bắt đầu test thì thấy `"` đã bị lược bỏ do chuỗi của ta đã bị bắ đầu bởi `"` → ta sẽ đóng chuỗi lại bằng `\"` và nên nhớ vẫn còn đoạn thừa ở cuối nên ta sẽ dùng `//` để comment nó lại

![Alt text](../image/lab9/07.png)

solve the lab thôi

![Alt text](../image/lab9/08.png)

![Alt text](../image/lab9/09.png)

![Alt text](../image/lab9/10.png)

3. `View post` → vẫn là khỏi phải test

> **Test bằng Active Scan**

![Alt text](../image/lab9/11.png)

![Alt text](../image/lab9/12.png)

![Alt text](../image/lab9/13.png)

# [Lab 10: Stored DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored)

![Yêu cầu lab 10](../image/lab10/0.png)

> - **Mô tả lab:**
> 
> - **Mục tiêu:**

![main web](../image/lab10/01.png)

2 chức năng

1. `Home`

2. `View post`, trong đây có chức năng mới `Post comment` → chắc chắn là lưu vào database → Stored XSS

![Alt text](../image/lab10/02.png)

quan sát các Request ta thấy có các request chứa soure `window.location.search`

![Alt text](../image/lab10/03.png)

→ dấu `<` đã bị mã hóa, tuy nhiên khi đối số đầu tiên là một chuỗi, thì nó chỉ replace lần xuất hiện đầu tiên

và 1 vài sink `innerHtml`

![Alt text](../image/lab10/04.png)

![Alt text](../image/lab10/05.png)![Alt text](../image/lab10/06.png)

→ thêm `<>` bổ sung vòa đầu comment, cặp này sẽ bị encode nhưng các dấu ngoặc tiếp theo sẽ không bị ảnh hưởng

→ payload bypass: `<><img src=1 onerror=alert(1)>`

![Alt text](../image/lab10/07.png)

![Alt text](../image/lab10/09.png)

solve the lab

![Alt text](../image/lab10/08.png)

> **Test bằng Active Scan**


# 1. Định nghĩa

- kẻ tấn công khai thác hành vi của máy chủ web và bộ đệm để cung cấp phản hồi HTTP có hại cho những người dùng khác.

- 2 giai đoạn

    - Kẻ tấn công phải tìm ra cách gợi ra phản hồi từ máy chủ phụ trợ vô tình chứa một số loại tải trọng nguy hiểm.

    - Sau khi thành công, họ cần đảm bảo rằng phản hồi của họ được lưu vào bộ nhớ đệm và sau đó được gửi đến các nạn nhân dự định.

-  khai thác chèn XSS, Javascript, ...

# 2. Cách hoạt động

- Nếu máy chủ phải gửi phản hồi mới cho từng yêu cầu HTTP riêng lẻ thì điều này có thể sẽ làm máy chủ bị quá tải, dẫn đến vấn đề về độ trễ và trải nghiệm người dùng kém, đặc biệt là trong thời gian bận rộn. Bộ nhớ đệm chủ yếu là một phương tiện để giảm bớt những vấn đề như vậy.

- Bộ đệm nằm giữa máy chủ và người dùng, nơi nó lưu (lưu trữ) các phản hồi cho các yêu cầu cụ thể, thường trong một khoảng thời gian cố định. Sau đó, nếu một người dùng khác gửi một yêu cầu tương đương, bộ nhớ đệm chỉ đơn giản cung cấp một bản sao của phản hồi được lưu trong bộ nhớ đệm trực tiếp cho người dùng mà không có bất kỳ tương tác nào từ phía back-end. Điều này giúp giảm tải đáng kể cho máy chủ bằng cách giảm số lượng yêu cầu trùng lặp mà nó phải xử lý.

## Cache keys

Khi bộ đệm nhận được yêu cầu HTTP, trước tiên nó phải xác định xem có phản hồi được lưu trong bộ nhớ đệm nào mà nó có thể phân phát trực tiếp hay không hoặc liệu nó có phải chuyển tiếp yêu cầu để máy chủ phụ trợ xử lý hay không. Bộ nhớ đệm xác định các yêu cầu tương đương bằng cách so sánh một tập hợp con được xác định trước gồm các thành phần của yêu cầu, được gọi chung là "khóa bộ đệm". Thông thường, điều này sẽ chứa dòng yêu cầu và Hosttiêu đề. Các thành phần của yêu cầu không có trong khóa bộ đệm được cho là "không có khóa".

Nếu khóa bộ đệm của yêu cầu đến khớp với khóa của yêu cầu trước đó thì bộ đệm sẽ coi chúng là tương đương. Do đó, nó sẽ cung cấp một bản sao của phản hồi được lưu trong bộ nhớ đệm đã được tạo cho yêu cầu ban đầu. Điều này áp dụng cho tất cả các yêu cầu tiếp theo có khóa bộ nhớ đệm phù hợp cho đến khi phản hồi được lưu trong bộ nhớ đệm hết hạn.

Điều quan trọng là các thành phần khác của yêu cầu đều bị bộ nhớ đệm bỏ qua hoàn toàn. Chúng ta sẽ khám phá tác động của hành vi này chi tiết hơn sau.

# 3. Ảnh hưởng

phụ thuộc vào 2 yếu tố:

- Kẻ tấn công có thể lưu vào cache thành công những gì?

- Lưu lượng truy cập bị ảnh hưởng?

# 4. Cách xây dựng tấn công Web cache poisoning

## 4.1. Xác định và đánh giá các đầu vào không khóa

## 4.2. Gây ra phản ứng có hại

## 4.3. Nhận phản hồi được lưu trữ trong bộ nhớ đệm

# 5. Khai thác

## [5.1. Khai thác lỗi thiết kế cache](./lab/part1.md)

- Sử dụng Web cache poisoning để khai thác gửi tấn công XSS

- Sử dụng Web cache poisoning để khai thác xử lý nhập khẩu tài nguyên không an toàn (lab 1)

    - Sử dụng header không khóa để tự động tạo URL nhằm nhập tài nguyên, chẳng hạn như tệp JS được lưu trữ bên ngoài. -->> có thể thao túng URL để trỏ đến tệp JS độc hại.

    - Nếu phản hồi chứa URL độc hại này được lưu vào bộ đệm, tệp JavaScript của kẻ tấn công sẽ được nhập và thực thi trong phiên trình duyệt của bất kỳ người dùng nào có yêu cầu có khóa bộ đệm phù hợp.

- Sử dụng Web cache poisoning để khai thác lỗ hổng xử lý cookie (lab 2)

- Sử dụng nhiều header để khai thác lỗ hổng ngộ độc bộ đệm web (lab 3)

- TMI - Vary header (lab 4)

- Khai thác DOM-based (EXPERT lab 5, 6)

## [5.2. Khai thác các lỗi triển khai bộ đệm](./lab/part2.md)


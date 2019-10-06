
# Các tính năng của Hyperledger Fabric

Hyperledger Fabric là nền tảng blockchain mang lại sự bảo mật, khả năng mở rộng, hiệu năng cao dành cho doanh nghiệp, với kiến trúc thiết kế dạng mô-đun. Nó cung cấp cho người dùng một loạt tính năng đặc biệt như sau"

## Quản lý danh tính

Hyperledger Fabric cung cấp dịch vụ định danh (membership identity service) giúp quản lý ID và xác thực tất cả người tham gia trên mạng. Tính năng định danh người dùng này là tiền đề cho việc phân quyền người dùng trên hệ thống. Ví dụ: Một ID người dùng cụ thể có thể được phép gọi đến các hàm trong chaincode, nhưng không được phép deploy chaincode mới.

## Tính riêng tư và bảo mật

Để đảm bảo tính riêng tư và bảo mật, Fabric đã đề xuất một khái niệm gọi là kênh (channel). Trong một kênh, tất cả dữ liệu, bao gồm thông tin giao dịch, thành viên và kênh là vô hình và không thể truy cập được đối với bất kỳ thành viên nào không được cấp quyền truy cập vào kênh đó.

## Hiệu năng (Efficient processing)

Mạng Fabric gồm nhiều loại nút có vai trò khác nhau. Với việc xử đồng thời và song song trên mạng, quá trình thực thi giao dịch được tách biệt quá trình ordering và commitment. Thực hiện các giao dịch trước khi ordering cho phép mỗi nút ngang hàng xử lý đồng thời nhiều giao dịch. Việc này sẽ làm tăng hiệu quả xử lý trên mỗi nút và đẩy nhanh việc phân phối các giao dịch đến ordering service.

## Chaincode

Hyperledger Fabric có 2 loại chaincode:

- Chaincode ứng dụng chứa logic nghiệp vụ của các giao dịch trong kênh. Ví dụ, Chaincode xác định các tham số để thay đổi quyền sở hữu tài sản, đảm bảo rằng tất cả các giao dịch chuyển quyền sở hữu phải tuân theo cùng một quy tắc và yêu cầu được định nghĩa trong chaincode. 
- Chaincode hệ thống có vai trò định nghĩa, xác định tham số vận hành cho toàn bộ kênh, cùng với đó là đưa ra các quy tắc cho xác nhận giao dịch trong kênh.

## Thiết kế mô-đun

Hyperledger Fabric được thiết kế theo kiến ​​trúc mô đun, cung cấp cho nhà phát triển các tùy chọn khác nhau trong việc cấu hình mạng. Các thuật toán định danh, ordering (đồng thuận), mã hóa, đều có thể được tùy biến. Kết quả là một kiến ​​trúc blockchain linh hoạt mà bất kỳ ngành công nghiệp hoặc doanh nghiệp nào cũng có thể áp dụng, với sự đảm bảo rằng các mạng Fabric riêng của mỗi doanh nghiệp, tổ chức có thể tương tác qua lại với nhau.
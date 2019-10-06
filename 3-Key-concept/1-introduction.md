
# Giới thiệu

Hyperledger Fabric là một nền tảng số cái phân tán với kiến trúc mô-đun đem lại mức độ bảo mật, khả năng phục hồi, tính linh hoạt và khả năng mở rộng cao. Nó được thiết kế để có thể hỗ trợ triển khai với nhiều thành phần tùy biến khác nhau (pluggable) và phù hợp với sự phức tạp của nhiều vấn đề khác nhau trong kinh doanh.

Phần này chúng tôi sẽ giới thiệu bên dưới các khái niệm căn bản để làm quen với cách thức hoạt động của blockchain, các tính năng và thành phần cụ thể của Hyperledger Fabric.

# Blockchain là gì ?

## Một sổ cái phân tán

Trái tim của mạng blockchain đó là một sổ cái phân tán ghi lại tất cả các giao dịch diễn ra trên mạng.

Một sổ cái blockchain thường được mô tả là phi tập trung vì nó được duy trì, cập nhật bởi nhiều người tham gia mạng. Chúng tôi nhận thấy rằng phi tập trung hóa và hợp tác là những đặc điểm phản ánh cách các doanh nghiệp trao đổi hàng hóa và dịch vụ trong thế giới thực.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/basic_network.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/basic_network.png)

Ngoài việc được phi tập trung, thông tin được ghi vào blockchain sử dụng các kỹ thuật mã hóa đảm bảo rằng một khi giao dịch đã được thêm vào sổ cái, nó không thể được sửa đổi (chính xác hơn là không thể sửa đổi trái phép mà không bị phát hiện). Thuộc tính này giúp đơn giản việc xác định nguồn gốc thông tin vì người tham gia có thể chắc chắn thông tin không bị thay đổi so với thực tế. 

## Hợp đồng thông minh

Để hỗ trợ cập nhật thông tin một cách nhất quán - và viếc sử dụng một loạt các tương tác với sổ cái (giao dịch, truy vấn, v.v.) - mạng blockchain sử dụng hợp đồng thông minh để cung cấp quyền truy cập có kiểm soát vào sổ cái.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/Smart_Contract.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/Smart_Contract.png)

Hợp đồng thông minh cũng chỉ là một chương trình phần mềm, giúp các bên giao dịch với nhau theo một quy ước chung đã định sẵn, nhằm loại bỏ các gian lận.

## Tính đồng thuận

Việc lưu trữ các giao dịch trên sổ cái được đồng bộ hóa trên mạng - Đảm bảo rằng sổ cái chỉ cập nhật khi các giao dịch được chấp thuận bởi những bên tham gia, các bên tham gia sẽ lưu trữ những sổ cái giống nhau. Đó được gọi là sự đồng thuận.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/consensus.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/consensus.png)

Chúng tôi sẽ đề cập nhiều hơn về sổ cái, hợp đồng thông minh và sự đồng thuận ở các phần sau. Đến thời điểm hiện tại, chúng ta có thể hiểu khái quát blockchain là một dạng cơ sở dữ liệu phân tán, được cập nhật trạng thái qua các hợp đồng thông minh, việc cập nhật dữ liệu vào sổ cái cần được sự đồng thuận của các bên tham gia.

# Những lợi ích mà Blockchain đem lại

## Các mạng lưới hiện nay

Về phần cốt lõi, các mạng lưới giao dịch ngày nay không khác cách mạng lưới giao dịch đã tồn tại từ hàng thế kỷ trước bao nhiêu. Các thành viên của một mạng lưới kinh doanh giao dịch không tồn tại một cơ sở dữ liệu chung, họ chỉ trao đổi thông tin với nhau, mỗi bên có một cơ sở dữ liệu riêng cho mình.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/current_network.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/current_network.png)

Công nghệ hiện đại đã đưa quá trình này từ sấp giấy dày cục sang ổ cứng và nền tảng đám mây, nhưng cấu trúc bên dưới là như nhau. Các hệ thống để quản lý danh tính của những người tham gia mạng không tồn tại, quá trình thực hiện và thời gian giao dịch mất rất nhiều thời gian, các hợp đồng phải được ký tay, và mỗi cơ sở dữ liệu tập trung và do đó tồn tại rủi do khi bị tấn công hay hư hỏng.

## Sự khác biệt của blockchain

Điều gì sẽ xảy ra nếu, các mạng lưới kinh doanh có các phương pháp tiêu chuẩn để thiết lập danh tính trên mạng, thực hiện giao dịch và lưu trữ dữ liệu? Điều gì sẽ xảy ra nếu việc thiết lập nguồn gốc của một tài sản có thể được xác định bằng cách xem qua danh sách các giao dịch mà sau khi được viết, không thể thay đổi và do đó có thể được tin cậy?

Mạng lưới kinh doanh đó sẽ trông giống như thế này:

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/future_net.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/future_net.png)

Đây là một mạng blockchain, trong đó mọi người tham gia đều lưu giữ bản sao của sổ cái. Ngoài thông tin sổ cái được chia sẻ, các quy trình cập nhật sổ cái cũng được chia sẻ. Không giống như các hệ thống tập trung, nơi các mỗi bên, mỗi doanh nghiệp có một sổ cái riêng của họ, một hệ thống blockchain sẽ chia sẻ các thông tin chung để cập nhật sổ cái, hướng tới một nền kinh tế chia sẻ trong tương lai.

Với khả năng điều phối mạng lưới kinh doanh của thông qua một sổ cái chung, mạng blockchain có thể giảm thời gian, chi phí và rủi ro liên quan đến thông tin cá nhân. 

# Hyperledger Fabric là gì ?

Linux Foundation đã thành lập dự án Hyperledger vào năm 2015 nhằm mục đích phát triển công nghệ blockchain để phục vụ cho các vấn đề doanh nghiệp. Thay vì tuyên bố một tiêu chuẩn blockchain duy nhất, nó khuyến khích cách tiếp cận hợp tác để phát triển các công nghệ blockchain thông qua cộng đồng.

Hyperledger Fabric là một trong những dự án blockchain trong Hyperledger. Giống như các công nghệ blockchain khác, nó có có sổ cái, sử dụng hợp đồng thông minh và là một hệ thống mà người tham gia quản lý các giao dịch của họ.

Hyperledger Fabric là một nền tảng blockchain riêng tư, cần sự cấp phép để tham gia vào mạng. Thay vì một hệ thống blockchain công khai cho phép mọi người ai cũng có thể tham gia và tương đối ẩn danh, các thành viên của mạng Hyperledger Fabric cần phải đăng ký thông qua Nhà cung cấp dịch vụ thành viên (Membership Service Provider - MSP).

Hyperledger Fabric cho phép tùy biến các thiết lập cài đặt trong mạng. Dữ liệu sổ cái có thể được lưu trữ ở nhiều định dạng, các cơ chế đồng thuận có thể được thay đổi.

Hyperledger Fabric có một tính năng quan trọng, đó là **kênh**, cho phép một nhóm người tham gia vào kênh để giao dịch với nhau. Các giao dịch chỉ có thể được nhìn thấy bởi các thành viên trong kênh, người ngoài không hè biết đến chúng. 

## Sổ cái chung

Sổ cái bao gồm hai thành phần: trạng thái (world state) và nhật ký giao dịch (transaction log). Mỗi người trong mạng sẽ có sổ cái cho mỗi kênh Hyperledger Fabric mà họ tham gia.

Trạng thái của sổ cái là duy nhất tại một thời điểm. Nhật ký giao dịch ghi lại tất cả các giao dịch dẫn đã xảy ra, là thứ làm thay đổi trạng thái của sổ cái. 

Dữ liệu được lưu trong sổ cái dưới dạng key-value. 

## Hợp đồng thông minh

Hợp đồng thông minh trong Hyperledger Fabric được gọi là chaincode, nó sẽ được gọi bởi các ứng dụng client để tương tác với sổ cái. Trong hầu hết các trường hợp, chaincode chỉ tương tác với dữ liệu trạng thái trong sổ cái (ví dụ truy vấn nó) chứ không tương tác với nhật ký giao dịch.

Chaincode trong Fabirc có thể được viết bằng Golang, NodeJS và Java.

## Riêng tư

Những mô hình kinh doanh doanh nghiệp với doanh nghiệp (B2B) có thể cực kỳ nhạy cảm về lượng thông tin họ chia sẻ. Hyperledger Fabric hỗ trợ quyền riêng tư đối với thông tin (với tính năng kênh) .

## Sự đồng thuận

Các giao dịch phải được ghi vào sổ cái theo thứ tự xảy ra, sổ cái của các bên tham gia phải nhất quán vào nhau và tránh các gian lận trái phép. Để thực hiện điều này, Fabric có những cơ chế đồng thuận giúp các bên xác thực giao dịch, loại bỏ các giao dịch trái phép.

Hyperledger Fabric đã được thiết kế để cho phép người quản trị có thể tùy chọn cơ chế đồng thuận phù hợp nhất với nhu cầu của mạng giao dịch khác nhau.

Chúng ta sẽ tìm hiểu thêm về các cơ chế đồng thuận của Hyperledger Fabric ở phần sau, bao gồm SOLO, Kafka và Raft.







# Những điểm mới trong phiên bản 1.4

## Phiên bản đầu tiên của Hyperledger Fabric sẽ được hỗ trợ dài hạn

Hyperledger Fabric đã trưởng thành kể từ phiên bản v1.0 ban đầu. Các nhà phát triển Fabric đã làm việc để cung cấp v1.4 với trọng tâm là sự ổn định và hỗ trợ các ứng dụng thực tế . Như vậy, v1.4.x sẽ là bản phát hành hỗ trợ dài hạn đầu tiên của chúng tôi.

Chính sách của chúng tôi cho đến nay là cung cấp các bản phát hành sửa lỗi (bản vá) cho bản phát hành chính hoặc phụ gần đây nhất của chúng tôi cho đến khi bản phát hành chính hoặc phụ tiếp theo được xuất bản. Chúng tôi dự định tiếp tục chính sách này cho các phiên bản tiếp theo. Tuy nhiên, đối với Hyperledger Fabric v1.4, bên Fabric sẽ cam kết cung cấp các bản sửa lỗi trong khoảng thời gian một năm kể từ ngày phát hiện. Điều này có thể sẽ dẫn đến một loạt các bản phát hành bản vá (v1.4.1, v1.4.2, v.v.), trong đó nhiều bản sửa lỗi được gói vào một bản phát hành bản vá.

Nếu bạn đang chạy với Hyperledger Fabric v1.4.x, bạn có thể yên tâm rằng bạn các bản vá sẽ được cập nhật thường xuyên. Trong trường hợp cần có một số nâng cấp để khắc phục một khiếm khuyết, chúng tôi sẽ cung cấp hướng dẫn cho bản vá đó.

## Raft ordering service

Được giới thiệu trong v1.4.1, Raft là ordering service dựa trên việc triển khai giao thức Raft trong [etcd](https://coreos.com/etcd/). Raft theo mô hình của "leader" vaf "follower", trong đó một nút leader được bầu (trên mỗi kênh) và các quyết định của nó được nhân rộng cho các follower. Raft dễ dàng thiết lập và quản lý hơn các ordering service dựa trên Kafka, thiết kế của chúng cho phép các tổ chức trải rộng trên toàn thế giới để đóng góp các nút cho ordering service phi tập trung.

## Khả năng phục vụ và cải tiến hoạt động

Khi nhiều mạng Hyperledger Fabric được chạy trên môi trường prduction, khả năng phục vụ và hoạt động rất được quan tâm. Fabric v1.4 có một bước tiến vượt bậc với cải tiến đăng nhập, kiểm tra trạng thái và số liệu vận hành. Như vậy, Fabric v1.4 là bản phát hành được khuyến nghị phù hợp cho các sản phầm thực tế.

## Cải tiến môi trường lập trình để phát triển ứng dụng

Viết các ứng dụng phi tập trung đã trở nên dễ dàng hơn. Cải tiến môi trường lập trình cho các hợp đồng thông minh (chaincode) và SDK làm cho việc phát triển các ứng dụng phi tập trung trở nên trực quan hơn, cho phép bạn tập trung vào logic ứng dụng của mình. Các cải tiến môi trường lập trình có sẵn cho Node.js (kể từ Fabric v1.4.0) và Java (kể từ Fabric v1.4.2). Các SDK hiện tại vẫn có sẵn để sử dụng và các ứng dụng hiện tại sẽ tiếp tục hoạt động. Chúng tôi khuyên các nhà phát triển nên chuyển sang SDK mới, cung cấp một lớp trừu tượng để cải thiện năng suất của nhà phát triển và dễ sử dụng hơn.

Tài liệu mới giúp bạn hiểu các khía cạnh khác nhau của việc tạo một ứng dụng phi tập trung cho Hyperledger Fabric.

- Kịch bản: Mô tả một mạng lưới kinh doanh giả định liên quan đến sáu tổ chức muốn xây dựng một ứng dụng để giao dịch với nhau.
- Phân tích: Mô tả cấu trúc của một commercial paper và cách các giao dịch ảnh hưởng đến nó theo thời gian. 
- Thiết kế quy trình và dữ liệu: Hiển thị cách thiết kế các quy trình và cấu trúc dữ liệu liên quan của chúng.
- Xử lý hợp đồng thông minh: Ví dụ một hợp đồng thông minh điều chỉnh quy trình kinh doanh phi tập trung về việc phát hành, mua và đổi commercial paper nên được thiết kế như thế nào.
- Ứng dụng mô tả ứng dụng client sẽ hoạt đồng như nào để gọi đến và xử lý hợp đồng thông minh.
- Thiết kế ứng dụng: Mô tả chi tiết xung quanh các namespace như hợp đồng, bối cảnh giao dịch, xử lý giao dịch, hồ sơ kết nối, tùy chọn kết nối, ví và cổng.

Và cuối cùng, một hướng dẫn và mẫu mang kịch bản ứng dụng trên vào cuộc sống:
- [Commercial paper tutorial](https://hyperledger-fabric.readthedocs.io/en/release-1.4/tutorial/commercial_paper.html)

## Những hướng dẫn mới trong tài liệu
- [Viết ứng dụng đầu tiên](https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html): Hướng dẫn này đã được cập nhật, nó có các ví dụ Java, JavaScript và Typecript của ứng dụng client và chaincode.
- Hướng dẫn về commericial paper: Như đã đề cập ở trên.
- Nâng cấp lên phiên bản Fabric mới nhất: Từ bài hướng dẫn *Xây dựng network đầu tiên* để mô tả việc nâng cấp từ v1.3 lên v1.4.x. Bao gồm cả tập lệnh (có thể dùng làm mẫu để nâng cấp), cũng như các lệnh riêng lẻ để bạn có thể hiểu từng bước nâng cấp.

## Cải tiến dữ liệu riêng tư (Private data enhancements)

[Private Data](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data-arch.html): Dữ liệu riêng tư là tính năng xuất hiện từ bản 1.2, đến bản này thì có 2 sự cải tiến mới.

-   **Reconciliation**: cho phép các peer trong tổ chức được có một document dữ liệu riêng tư để truy xuất dữ liệu riêng tư cho các giao dịch mà họ được hưởng.
-   **Client access control**  để tự động thực thi việc kiểm soát truy cập trong chaincode dựa trên tư cách thành viên của client organization collection membership mà không phải viết logic chaincode cụ thể.

## Hỗ trợ Node UO

Nhà cung cấp dịch vụ thành viên (MSP): Bắt đầu từ v1.4.3, các Node OU hiện được hỗ trợ để phân loại danh tính người quản trị (admin) và orderer (mở rộng hỗ trợ Node OU hiện tại cho client và peer). Các đơn vị tổ chức cho phép các tổ chức phân loại thêm danh tính thành quản trị viên và orderer dựa trên OUs chứng chỉ x509 của họ.

## Ghi chú phát hành

Ghi chú phát hành cung cấp thêm chi tiết cho người dùng chuyển sang bản phát hành mới.

-   [Fabric v1.4.0 release notes](https://github.com/hyperledger/fabric/releases/tag/v1.4.0).
-   [Fabric v1.4.1 release notes](https://github.com/hyperledger/fabric/releases/tag/v1.4.1).
-   [Fabric v1.4.2 release notes](https://github.com/hyperledger/fabric/releases/tag/v1.4.2).
-   [Fabric v1.4.3 release notes](https://github.com/hyperledger/fabric/releases/tag/v1.4.3).
-   [Fabric CA v1.4.0 release notes](https://github.com/hyperledger/fabric-ca/releases/tag/v1.4.0).
-   [Fabric CA v1.4.1 release notes](https://github.com/hyperledger/fabric-ca/releases/tag/v1.4.1).
-   [Fabric CA v1.4.2 release notes](https://github.com/hyperledger/fabric-ca/releases/tag/v1.4.2).
-   [Fabric CA v1.4.3 release notes](https://github.com/hyperledger/fabric-ca/releases/tag/v1.4.3).


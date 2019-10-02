## Giới thiệu

Nói chung, blockchain là cơ sở dữ liệu phân tán, rất khó để sửa đổi trái phép, được duy trì trong một mạng lưới phân tán của các nút ngang hàng. Mỗi nút trong mạng duy trì một bản sao của cơ sở dữ liệu thông qua giao thức đồng thuận.

Ứng dụng đầu tiên và cũng là ứng dụng nổi tiếng nhất của blockchain là Bitcoin. Kế đến là Ethereum, một nền tảng blockchain với cách tiếp cận khác, nhiều đặc điểm giống như Bitcoin nhưng thêm các hợp đồng thông minh để tạo ra một nền tảng phát triển cho các ứng dụng phân tán. Bitcoin và Ethereum nói ở trên thuộc loại nền tảng blockchain công khai (public blockchain hay permissionless blockchain). Về cơ bản, đây là các mạng công khai, bất kỳ ai, cũng có thể tham gia, nơi những người tham gia tương tác là tương đối ẩn danh.

Với sự thành công ban đầu của Bitcoin, Ethereum và các nền tảng blockchain công khai khác. Nền tảng blockchain nhận được sự quan tâm rất lớn từ cộng đồng và các doanh nghiệp, từ đó các nhu cầu áp dụng blockchain vào các hoạt động doang nghiệp ngày càng tăng cao. Tuy nhiên, các nền tảng blockchain công khai chưa đáp ứng được nhu cầu của doanh nghiệp trong xử lý các vấn đề kinh doanh (tốc độ giao dịch chậm, dữ liệu hoàn toàn công khai, vấn để ẩn danh...).

Để sử dụng cho doanh nghiệp, chúng ta cần xem xét các yêu cầu sau:
- Các bên tham gia cần phải được định danh rõ ràng.
-  Việc tham gia vào mạng cần được cấp phép
-  Thông lượng giao dịch cao
-  Độ trễ giao dịch thấp
-  Quyền riêng tư và bảo mật của các giao dịch và dữ liệu liên quan đến các giao dịch kinh doanh.

Trong khi nhiều nền tảng blockchain hiện đang được điều chỉnh để phù hợp sử dụng cho doanh nghiệp, Hyperledger Fabric được thiết kế từ ban đầu nhằm sử dụng cho các doanh nghiệp. Các phần sau đây sẽ phân biệt Hyperledger Fabric (Fabric) với các nền tảng blockchain khác và nói sơ qua về cách thiết kế kiến trúc.

## Hyperledger Fabric

Hyperledger Fabric là một nền tảng private blockchain mở nguồn mở, được thiết kế để sử dụng cho các hoạt động doanh nghiệp, nó cung cấp một số tính năng khác biệt so với các nền tảng blockchain phổ biến khác.

Nói qua về Hyperledger, nó được thành lập bởi Linux Foundation, nơi có lịch sử lâu dài và rất thành công trong việc phát triển các dự án nguồn mở. Hyperledger Fabric là một dự án trong hệ sinh thái Hyperledger bởi một nhóm các nhà bảo trì đa dạng từ nhiều tổ chức và cộng đồng.

Fabric có kiến ​​trúc mô đun và tùy chỉnh cao, cho phép đổi mới, linh hoạt và tối ưu hóa với nhiều dịch vụ như ngân hàng, tài chính, bảo hiểm, y tế, nguồn nhân lực, chuỗi cung ứng và thậm chí cả âm nhạc kỹ thuật số. 

Fabric là nền tảng blockchain đầu tiên hỗ trợ việc viết các hợp đồng thông minh bằng các ngôn ngữ lập trình phổ biến như Java, Go và Node.js, thay vì các ngôn ngữ dành riêng cho từng nền tảng (Vyper, Solidity cho Ethereum là 1 ví dụ). Điều này có nghĩa là các nhà phát triển sẽ không cần phải học thêm một ngôn ngữ mới để có thể viết hợp đồng thông minh.

Fabric là nền tảng private blockchain (permission blockchain), có nghĩa là những người tham gia vào mạng được định danh, thay vì ẩn danh như trong các nền tảng public blockchain.

Một trong những điều đặc biệt của nền tảng này là việc hỗ trợ tùy biến giao thức đồng thuận (pluggable consensus protocols), cho phép linh hoạt hơn để phù hợp với các vấn đề và mô hình khác nhau. Ví dụ, khi được triển khai trong một doanh nghiệp, hoặc được điều hành bởi một cơ quan đáng tin cậy, thuật toán đồng thuận fully byzantine fault tolerant có thể được coi là không cần thiết và nó sẽ làm giảm hiệu suất của mạng. Trong các tình huống như vậy, [crash fault-tolerant](https://en.wikipedia.org/wiki/Fault_tolerance) có thể là đủ. Trong khi đó, các trường hợp nhiều bên tham gia, phi tập trung, giao thức đồng thuận [byzantine fault tolerant](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance) (BFT) có thể được yêu cầu.

Fabric sử các giao thức đồng thuận không yêu cầu tiền mã hóa riêng để tránh việc hao tổn tài nguyên để khai thác. Việc Fabric không có đồng tiền mã hóa giúp giảm rủi ro bị tấn công một cách đáng kể, cùng với đó là việc nền tảng có thể được triển khai với chi phí hoạt động gần như tương đương với bất kỳ hệ thống phân tán nào khác.

Với kiến trúc được thiết kế, Fabric trở thành một trong những nền tảng blockchain có hiệu năng tốt nhất hiện nay cả về xử lý giao dịch và độ trễ trong việc xác thực giao dịch, đem lại sự riêng tư và bảo mật.

Hãy cùng khám phá những tính năng khác biệt này một cách chi tiết hơn.

## Tính mô đun (Modularity)

Hyperledger Fabric được thiết kế theo một kiến ​​trúc dạng mô-đun. Cho dù đó là cơ chế đồng thuận hay các giao thức quản lý danh tính đều có thể tùy biến (pluggable) được như LDAP hoặc OpenID Connect.

Ở mức độ trửu tượng cao, Fabric bao gồm các mô-đun sau:

-   Một _ordering service_  thiết lập sự đồng thuận về thứ tự của các giao dịch và sau đó phát tán (broadcast) các block lên mạng cho các peer.
-   Một _membership service provider_ chịu trách nhiệm liên kết các thực thể trong mạng thông qua danh tính sử dụng mật mã.
-   Một tùy chọn _peer-to-peer gossip service_  để xác định cách truyền thông tin giữa các nút trong mạng.
-   Hợp đồng thông minh (chaincode) chạy độc lập trong môi trường container (vd: Docker). Nó có thể được viết bằng các ngôn ngữ như Java, Golang, Node.js nhưng không có quyền thay đổi trực tiếp trạng thái của sổ cái.
-   Sổ cái (blockchain) chứa dữ liệu có thể được sử dụng với các hệ quản trị cơ sở dữ liệu khác nhau (CouchDB, LevelDB).
-   A pluggable endorsement and validation policy enforcement that can be independently configured per application.
-  Một endorsement chứng thực và chính sách xác thực (validation policy) có thể được tùy biến và cấu hình cho mỗi ứng dụng.

Một phương thuốc không thể trị được bách bệnh. Hyperledger Fabric có thể được cấu hình theo nhiều cách để đáp ứng các yêu cầu khác cho nhiều trường hợp sử dụng.

## Blockchain công khai và blockchain riêng tư

Trong một blockchain công khai, ai cũng có thể tham gia vào mạng và tương đối ẩn danh. Các nút không cần tin tưởng lẫn nhau, họ chỉ cần tin tưởng vào dữ liệu trên blockchain là xác thực và cực kỳ khó để các thay đổi gian lận không bị phát giác. Dữ liệu đưa vào blockchain được xác thực thông qua các thuật toán đồng thuận dựa trên đồng tiền mã hóa.

Mặt khác, các blockchain riêng tư, các bên tham gia vào mạng được định danh và xác thực. Một blockchain riêng tư cung cấp một cách để bảo đảm các tương tác giữa một nhóm các thực thể có một mục tiêu chung nhưng có thể không hoàn toàn tin tưởng lẫn nhau. Bằng cách dựa vào danh tính của những người tham gia, một blockchain riêng tư có thể sử dụng các giao thức đồng thuận truyền thống như (CFT) hoặc byzantine fault tolerant (BFT) mà không yêu cần phải tiêu tốn quá nhiều tài nguyên.

Trong bối cảnh như vậy, nguy cơ người tham gia mạng blockchain riêng tư cố tình thực thi mã độc thông qua hợp đồng thông minh sẽ giảm bớt. Đầu tiên, những người tham gia biết nhau và tất cả các hành động, cho dù gửi giao dịch ứng dụng, sửa đổi cấu hình của mạng hoặc triển khai hợp đồng thông minh đều được ghi lại trên blockchain theo chính sách chứng thực được thiết lập cho mạng và loại giao dịch có liên quan. Thay vì hoàn toàn ẩn danh, bên có gây thiệt hại có thể dễ dàng được xác định và vụ việc được xử lý theo các điều khoản của mô hình quản trị.

## Hợp đồng thông minh

Trong Fabric, hợp đồng thông minh được gọi dưới cái tên là `chaincode`, một chương trình phần mềm tương tác với sổ cái blockchain với sự đồng thuận đến từ các nút. Chaincode chứa nghiệp vụ logic của một ứng dụng blockchain.

Có ba điểm chính của hợp đồng thông minh:
- Nhiều hợp đồng thông minh được cài đặt trong mạng
- Chúng có thể được triển khai bởi bất cứ ai trong mạng
- Mã nguồn hợp đồng có thể không đáng tin cậy, thậm chí là có thể chứa mã độc

Hầu hết các nền tảng blockchain có tính năng hợp đồng thông minh hiện có đều tuân theo kiến ​​trúc **order-execute** trong đó giao thức đồng thuận:
- Xác thực và thực hiện giao dịch sau đó truyền chúng đến tất cả các nút ngang hàng.
- Mỗi nút sau đó sẽ xác thực và thực thi giao dịch

Kiến trúc order-execute có thể được tìm thấy trong hầu hết tất cả các hệ thống blockchain hiện có, từ các nền tảng công khai như [Ethereum](https://ethereum.org/) (với thuật toán đồng thuận PoW) đến các nền tảng blockchain riêng tư như [Tendermint](http://tendermint.com/), [Chain](http://chain.com/), và [Quorum](http://www.jpmorgan.com/global/Quorum).

Việc thực thi hợp đồng thông minh trong một nền tảng blockchain hoạt động với kiến ​​trúc order-execute cần phải được xác định (deterministic);  mặt khác, sự đồng thuận đôi khi có thể không bao giờ đạt được. Để giải quyết vấn đề này, nhiều nền tảng yêu cầu các hợp đồng thông minh phải được viết bằng ngôn ngữ riêng (như Solidity) để có thể loại bỏ các hoạt động không xác định. Điều này có một chút bất tiện vì các nhà phát triển phải học thêm ngôn ngữ mới và ngôn ngữ đấy khi mới đó cũng tiềm ẩn nhiều lỗ hổng chết người (thời gian phát triển chưa lâu).

Hơn nữa, vì tất cả các giao dịch được thực hiện tuần tự bởi tất cả các nút, dẫn đến hiệu suất và quy mô bị hạn chế. Thực tế là thực thi hợp đồng thông minh trên các nút trong hệ thống đòi hỏi phải thực hiện các biện pháp phức tạp để bảo vệ hệ thống khỏi các hợp đồng chứa mã độc nhằm đảm bảo khả năng phục hồi của toàn bộ hệ thống khi xảy ra sự cố.

## Một cách tiếp cận mới

Fabric giới thiệu một kiến ​​trúc mới cho các giao dịch mà chúng ta gọi là **execute-order-validate**. Nó giải quyết các thách thức về khả năng phục hồi, tính linh hoạt, khả năng mở rộng, hiệu suất và bảo mật mà mô hình **order-execute**  phải đối mặt bằng cách tách luồng giao dịch thành ba bước:
- Thực thi một giao dịch và kiểm tra tính đúng đắn của nó, qua đó chứng thực tính hợp lệ của nó.
- Order giao dịch thông qua thuật toán đồng thuận
- Xác thực lại các giao dịch dựa trên chính sách chứng thực dành riêng cho ứng dụng trước khi đưa chúng vào sổ cái.

Thiết kế này bắt nguồn hoàn toàn từ mô hình order-execute trong đó Fabric thực hiện các giao dịch trước khi đạt được thỏa thuận cuối cùng.

Trong Fabric, chính sách chứng thực dành riêng cho ứng dụng chỉ định các nút ngang hàng nào, hoặc bao nhiêu trong số chúng, cần phải chứng minh để giao dịch được coi là xác thực. Do đó, mỗi giao dịch chỉ cần được thực hiện (xác nhận) bởi tập hợp con của các nút ngang hàng cần thiết để đáp ứng chính sách chứng thực của giao dịch. Điều này cho phép thực hiện song song, tăng hiệu suất và quy mô tổng thể của hệ thống. Giai đoạn đầu tiên này cũng sẽ loại bỏ bất kỳ sự không xác định nào, vì các kết quả không nhất quán có thể được lọc ra trước khi trung chuyển giao dịch.

## Tính riêng tư và bảo mật

Như chúng ta đã thảo luận, một mạng blockchain công khai sử dụng PoW, các giao dịch được thực thi trên mọi nút. Điều này có nghĩa là không có sự bảo mật, riêng của chính các hợp đồng cũng như dữ liệu giao dịch mà họ xử lý. Mọi giao dịch và mã nguồn thực đều hiển thị cho mọi nút trong mạng. 

Công khai mọi thứ sẽ là vấn đề lớn khi áp dụng vào các mô hình kinh doanh/doanh nghiệp. Ví dụ, trong một mạng lưới các đối tác trong chuỗi cung ứng, một số người tiêu dùng có thể được ưu đãi để củng cố mối quan hệ hoặc thúc đẩy doanh số bán hàng chẳng hạn. Nếu mọi người tham gia có thể thấy mọi hợp đồng và giao dịch, mọi người ai cũng sẽ muốn có mức giá ưu đãi!

Để giải quyết việc thiếu sự riêng tư và bảo mật cho các mục đích cung cấp hướng doanh nghiệp, các nền tảng blockchain đã áp dụng nhiều cách tiếp cận khác nhau. Tất cả đều có sự đánh đổi.

Mã hóa dữ liệu là một cách tiếp cận để cung cấp tính bảo mật; tuy nhiên, trong một mạng blockchain sử dụng PoW, dữ liệu được mã hóa nằm trên mỗi nút. Nếu có đủ thời gian và tài nguyên tính toán, lớp mã hóa có thể bị phá vỡ. Với các doanh nghiệp, việc thông tin của họ có thể bị xâm phạm là không thể chấp nhận được.

Zero knowledge proofs (ZKP) là một lĩnh vực nghiên cứu khác nhằm giải quyết vấn đề này, việc tính toán ZKP đòi hỏi thời gian và nguồn lực tính toán đáng kể. Do đó, sự đánh đổi trong trường hợp này là hiệu suất để bảo mật.

Hyperledger Fabric, là một nền tảng blockchain riêng tư, cho phép bảo mật thông qua kiến ​​trúc kênh (channel) của nó. Về cơ bản, những người tham gia trên mạng Fabric có thể thiết lập một kênh riêng giữa các nhóm người tham gia nên để thực thi một nhóm các giao dịch cụ thể. Do đó, chỉ những nút tham gia vào kênh mới có quyền truy cập vào hợp đồng thông minh (chaincode) và dữ liệu được giao dịch.

Để cải thiện khả năng riêng tư và bảo mật của mình, Fabric đã bổ sung tính năng hỗ trợ cho [dữ liệu riêng tư](https://hyperledger-fabric.readthedocs.io/en/release-1.4/private-data/private-data.html) và đang làm việc để có thể đưa các (ZKP) vào nền tảng trong tương lai.

## Tùy biến thuật toán đồng thuận

Thứ tự của các giao dịch được do phần mô-đun cho đồng thuận phụ trách thực hiện giao dịch và duy trì trạng thái sổ cái, được gọi dưới cái tên *ordering service*. 

Fabric hiện cung cấp hai triển khai dịch vụ *ordering* Đầu tiên dựa trên thư viện [etcd](https://etcd.io/) của [giao thức Raft](https://raft.github.io/raft.pdf). Một *ordering service* khác là [Kafka](https://kafka.apache.org/)(sử dụng [Zookeeper](https://zookeeper.apache.org/). Để biết thông tin về các *ordering service* hiện có, hãy xem mục *ordering service* ở phần sau của tài liệu. 

Lưu ý răng, mạng Fabric có thể có nhiều *ordering service* hỗ trợ các ứng dụng, yêu cầu khác nhau.

## Hiệu năng và khả năng mở rộng

Hiệu năng của nền tảng blockchain có thể bị ảnh hưởng bởi nhiều yếu tố như kích thước giao dịch, kích thước block, kích thước mạng, cũng như giới hạn của phần cứng, v.v. Cộng đồng Hyperledger hiện đang phát triển một [bộ dự thảo](https://docs.google.com/document/d/1DQ6PqoeIH0pCNJSEYiw7JVbExDvWh_ZRVhWkuioG4k0/edit#heading=h.av4vusatnjg6) các biện pháp bảo đảm yếu tố hiệu năng và quy mô, cùng với việc triển khai tương ứng một khung đánh giá được gọi là [Hyperledger Caliper](https://wiki.hyperledger.org/projects/caliper).

Một nhóm từ IBM Research đã xuất bản một [bài báo](https://arxiv.org/abs/1801.10228v1) đánh giá đánh giá kiến ​​trúc và hiệu năng của Hyperledger Fabric. Bài viết cung cấp một cuộc thảo luận chuyên sâu về kiến ​​trúc của Fabric và sau đó đưa đánh giá hiệu năng bằng cách sử dụng bản phát hành sơ bộ của Hyperledger Fabric v1.1.

Những nỗ lực của nhóm nghiên cứu đã mang lại một số cải tiến hiệu suất đáng kể cho bản phát hành Fabric v1.1.0, tăng hơn gấp 2 lần hiệu suất tổng thể của nền tảng từ các bản v1.0.0.

## Kết luận

Với kiến trúc khác biệt của Fabric làm cho nó trở thành một hệ thống có khả năng mở rộng cao, hỗ trợ giải quyết một loạt các vấn đề từ chính phủ, tài chính, hậu cần, chuỗi cung ứng, đến chăm sóc sức khỏe..v.v

Hyperledger Fabric đang là dự án hoạt động tích cực nhất trong số mười dự án (hiện tại) của Hyperledger. Việc xây dựng cộng đồng xung quanh nền tảng đang phát triển ổn định và sự đổi mới trong những bản nâng cấp hứa hện vượt xa bất kỳ nền tảng blockchain doanh nghiệp nào khác.



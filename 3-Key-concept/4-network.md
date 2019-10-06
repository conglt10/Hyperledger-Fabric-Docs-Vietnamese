
[<- Phần trước: Mô hình](./3-model.md)

[-> Phần sau: Định danh](./5-indentity.md)

# Mạng blockchain

Phần này chúng ta sẽ cùng tìm hiểu kiến trúc, cấu tạo của một mạng Hyperledger Fabric ở mức khái niệm. Đọc xong phần này, các bạn có thể biết được những thành phần nào tham gia cấu tạo nên một mạng fabric, vai trò của các thành phần đó trong mạng và cách chúng tương tác với nhau.

# Một mạng blockchain là gì ?

Một mạng blockchain là nơi người tham gia để cùng duy trì một sổ cái chung với nhau qua các giao dịch. Người tham gia có thể tương tác với các hợp đồng thông minh để tạo ra các giao dịch và sau đó được phát tán trong mạng đến các bên khác để xác thực, cuối cùng giao dịch sẽ được lưu trữ vào sổ cái nếu nó hợp lệ.

Trong một mạng blockchain riêng tư, nhiều tổ chức kết hợp để tạo thành mạng và các quyền của họ được xác định bởi một tập hợp các chính sách được các bên đồng ý khi mạng được cấu hình ban đầu. Hơn nữa, các chính sách của mạng có thể thay đổi theo thời gian tùy theo thỏa thuận của các tổ chức bên, như chúng ta tìm hiểu chi tiết hơn về chính sách sửa đổi (modification policy) ở phần sau của tài liệu này.

## Một mạng điển hình (Sample network)

Trước khi chúng ta bắt đầu tìm hiểu chi tiết về từng phần trong mạng Farbic, hãy cùng tìm hiểu xem những thành phần cần có của một mạng Fabric là gì ?

Có thể bạn đầu các bạn sẽ có chút bối rối về sự lằng nhằng của mạng Fabirc. Nhưng đừng lo lắng, phần tới chúng ta sẽ tìm hiểu từng bước hình thành của một mạng Fabic.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.1.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.1.png)

- 4 tổ chức, R1, R2, R3 và R4 đã cùng quyết định và một thỏa thuận với nhau sẽ tham gia, thiết lập và sử dụng một mạng Hyperledger Fabric. R4 được chỉ định làm tổ chức khởi tạo mạng - nó đã được trao quyền để thiết lập phiên bản cấu hình ban đầu của mạng. 
- R4 không có ý định thực hiện việc giao dịch trên mạng. R1 và R2 có nhu cầu trao đổi thông tin riêng với nhau (trên kênh C1), R2 và R3 cũng có nhu cầu tương tự (trên kênh C2). Tổ chức R1 có một ứng dụng client A1 có thể thực hiện các giao dịch trên kênh C1. Tổ chức R2 có một ứng dụng client A2 để thực hiện giao dịch trên cả 2 kênh C1 và C2. Tổ chức R3 ứng dụng client A3 có thể thực hiện các giao dịch trên kênh C2.
- Nút  P1 duy trì một bản sao của sổ cái L1 của kênh C1. Nút P2 duy trì một bản sao của sổ cái L1 cũng của kênh C1 và một bản sao của sổ cái L2 của kênh C2. Nút P3 duy trì một bản sao của sổ cái L2 của kênh C2.
- Các quy tắc, chính sách của mạng được thiết lập trong cấu hình mạng NC4, mạng nằm dưới sự kiểm soát của các tổ chức R1 và R4.
- Cấu hình, chính sách kênh C1 được thiết lập và chỉ định trong CC1; kênh nằm dưới sự kiểm soát của các tổ chức R1 và R2. Tương tự trên kênh C2 là  CC2; kênh nằm dưới sự kiểm soát của các tổ chức R2 và R3.
- Ordering service O4 có vai trò như một điểm quản trị mạng, nó được sử dụng bởi các kênh trên hệ thống. Ordering service hỗ trợ các kênh với mục đích đồng thuận. Mỗi tổ chức trong 4 tổ chức có một cơ quan chứng thực (Certificate Authority - CA).

## Tạo Mạng

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.2.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.2.png)

Mạng được hình thành khi một Ordered được khởi tạo. Trong ví dụ của chúng tôi, ordering service bao gồm một nút O4, được cài đặt theo cấu hình mạng NC4, cung cấp quyền quản trị cho tổ chức R4. Ở cấp độ mạng, Tổ chức phát hành Chứng chỉ CA4 được sử dụng để phân phối danh tính cho quản trị viên và các nút mạng thuộc tổ chức R4.

Chúng ta có thể thấy để thiết lập một mạng N, đầu tiên cần một ordering service O4. O4 ban đầu được lưu trữ trong R4, cấu hình và chạy bởi một quản trị viên trong tổ chức đó. Ban đầu, chính sách được thiết lập để chỉ cung cấp quyền cho R4 trên mạng. Điều này sẽ thay đổi, như chúng ta sẽ thấy sau, nhưng hiện tại, R4 là thành viên duy nhất của mạng.

## Cơ quan cấp chứng chỉ (CA)

CA có vai trò cấp chứng chỉ cho quản trị viên và các nút trong mạng. Trong ví dụ, CA4 đóng một vai trò quan trọng, nó cung cấp các chứng chỉ X.509 để xác định các thành viên thuộc tổ chức R4. Chứng chỉ do CA cấp cũng có thể được sử dụng để ký các giao dịch. Hãy cùng xem quan hai khía cạnh của một CA.

Thứ nhất, các thành phần khác nhau của mạng blockchain sử dụng chứng chỉ để định danh xem nó đến từ tổ chức nào. Đó là lý do tại sao thường có nhiều hơn một CA trên một mạng Fabric - các tổ chức khác nhau thường sử dụng các CA khác nhau. Trong ví dụ minh họa sử dụng 4 CA, mỗi tổ chức có một CA. CA rất quan trọng đến mức Hyperledger Fabric cung cấp cho bạn một công cụ tích hợp (được gọi là Fabric-CA), mặc dù trong thực tế, các tổ chức sẽ chọn sử dụng CA của riêng họ.

Việc ánh xạ chứng chỉ tới các thành viên trong tổ chức đạt được thông qua một cấu trúc gọi là Nhà cung cấp dịch vụ thành viên (Membership Services Provider - MSP). Cấu hình mạng NC4 sử dụng MSP để xác định các thuộc tính của chứng chỉ được phân phối bởi CA4, liên kết chủ sở hữu chứng chỉ với tổ chức R4. NC4 sau đó có thể sử dụng MSP này thiết lập quyền hạn của các chứng chỉ trong tổ chức R4. Ví dụ, xác định admin trong R4, người có quyền thêm người dùng vào tổ chức đó. Chúng tôi mô tả MSP trên sơ đồ, vì chúng sẽ làm nó trở nên rất phức tạp,.

Thứ hai, chứng chỉ do CA cấp là trung tâm của quá trình tạo và xác thực giao dịch. Cụ thể, chứng chỉ X.509 được sử dụng trong việc khởi tạo, ký và xác thực giao dịch ở ứng dụng client. Sau đó, các nút mạng lưu trữ các bản sao của sổ cái xác minh rằng chữ ký giao dịch là hợp lệ trước khi chấp nhận đưa giao dịch vào sổ cái.

Tóm tắt lại, cấu trúc sơ khai của một mạng blockchain N có:
- Một cơ quan cung cấp chứng chỉ (CA4)
- Cấu hình mạng NC4 thiết lập các chính sách với các tài nguyên trong mạng
- Nút ordering service O4

## Thêm admin vào mạng

NC4 ban đầu được cấu hình để chỉ cho phép người dùng thuộc tổ chức R4 quyền quản trị trên mạng. Trong mục này, chúng ta sẽ cho phép người dùng từ tổ chức R1 quản trị mạng. Hãy xem quá trình diễn ra như thế nào.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.2.1.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.2.1.png)


Tổ chức R4 cập nhật cấu hình mạng để biến tổ chức R1 thành quản trị viên. Sau thời điểm này, R1 và R4 có quyền như nhau.

Cơ quan cấp chứng chỉ CA1 đã được thêm vào - nó có thể được sử dụng để xác định người dùng từ tổ chức R1. Sau dó, người dùng từ cả R1 và R4 có thể quản trị mạng.

R1 đã chia sẻ quyền quản trị đối với R4. Điều đó có nghĩa là R1 hoặc R4 có thể cập nhật cấu hình mạng NC4 để cho phép tổ chức R2 tham gia vào mạng. Mặc nút ordered O4, đang chạy trên cơ sở hạ tầng R4, nhưng R1 có toàn quyền quản trị đối với nó.

Ở dạng đơn giản nhất, ordering service chỉ có một nút duy nhất trong mạng. Ordering service thường gồm nhiều nút và có thể được cấu hình để các nút khác nhau thuộc các tổ chức khác nhau. Ví dụ: chúng ta có thể chạy O4 trong R4 và kết nối nó với O2. Theo cấu trúc này, chúng ta sẽ có một cấu trúc quản trị đa tổ chức.

Chúng ta sẽ thảo luận chi tiết hơn về ordering serivice ở phần sau của tài liệu, bây giờ chúng ta chỉ cần hiểu đơn ordering serivice như nơi (administration point) cung cấp cho các tổ chức khác nhau quyền truy cập vào mạng.

## Xác định một hiệp hội (Defining a Consortium)

Mặc dù hiện tại mạng có thể được quản lý bởi R1 và R4, nhưng có rất ít việc có thể được thực hiện. Điều đầu tiên chúng ta cần làm là xác định một hiệp hội. 

Hãy để xem cách một hiệp hội được định nghĩa như thế nào:

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.3.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.3.png)
 
Một quản trị viên tạo lập một hiệp hội X1 có chứa hai thành viên R1 và R2. Thông tin về hiệp hội này được lưu trữ trong cấu hình mạng NC4. CA1 và CA2 là Cơ quan cấp chứng chỉ tương ứng cho các tổ chức này.

Do cách cấu hình NC4, chỉ có R1 hoặc R4 mới có thể tạo ra hiệp hội mới. Một hiệp hội có thể có rất nhiều tổ chức, để cho đơn giản, trong ví dụ này hiệp hội X1 chỉ có 2 thành viên là R1 và R2.

Vai trò của hiệp hội là gì ? Chúng ta có thể thấy rằng một hiệp hội xác định tập hợp các tổ chức trong mạng có chung nhu cầu giao dịch với nhau - trong trường hợp này là R1 và R2. Nó cũng như các hiệp hội doanh nghiệp, tổ chức ngoài thế giới thực, hợp tác cùng nhau giao dịch, làm ăn, phát triển.

Mạng Fabirc ở trên, mặc dù ban đầu chỉ có một tổ chức duy nhất, nhưng hiện được kiểm soát bởi một nhóm các tổ chức lớn hơn. 

Bây giờ chúng ta sẽ cùng xem hiệp hội X1 gắn liền với một phần thực sự quan trọng của Hyperledger Fabric - đó là kênh.

## Tạo kênh mới từ hiệp hội

Kênh là một cơ chế truyền thông chính mà theo đó các thành viên của một hiệp hội có thể giao tiếp với nhau. Có thể có nhiều kênh trong một mạng, nhưng hiện tại, chúng ta sẽ bắt đầu với một kênh.

Hãy để xem cách kênh đầu tiên được thêm vào mạng:


![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.4.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.4.png)


Kênh C1 đã được tạo cho R1 và R2 từ hiệp hội X1. Kênh được điều chỉnh bởi cấu hình kênh CC1, tách biệt hoàn toàn với cấu hình mạng NC4. CC1 được quản lý bởi R1 và R2, 2 tổ chức này có quyền như nhau trên C1. R4 không có quyền gì trong CC1.

Chúng ta có thể thấy kênh C1 đã được kết nối với ordering service O4 nhưng ngoài nó ra chưa có thêm thành phần nào liên kết với kênh cả. Dần dần, chúng ta sẽ kết nối thêm các phần như ứng dụng client và nút ngang hàng vào kênh.

Mặc dù kênh C1 là một phần của mạng N, nhưng nó gần như không chịu sự chi phối từ mạng. Kênh C1 có cấu hình CC1 hoàn toàn riêng biệt với cấu hình mạng NC4. CC1 chứa các chính sách quản lý các quyền mà R1 và R2 có trên kênh C1, với các tổ chức khác như R3 và R4 sẽ không có quyền trên kênh này. R3 và R4 chỉ có thể tương tác với C1 nếu chúng được thêm bởi R1 hoặc R2 trong cấu hình kênh CC1 (tùy thuộc vào quy định những ai được thêm tổ chức mới vào kênh được định nghĩa trong NC1).

Các kênh rất hữu ích vì chúng cung cấp một cơ chế cho thông tin liên lạc riêng tư và dữ liệu riêng tư giữa các thành viên của một hiệp hội. Nó giúp chia sẻ hiệu quả về cơ sở hạ tầng trong khi duy trì quyền riêng tư dữ liệu và truyền thông.

Mọi cập nhật cho cấu hình mạng NC4 từ thời điểm này trở đi sẽ không có ảnh hưởng trực tiếp đến cấu hình kênh CC1; ví dụ: nếu định nghĩa hiệp hội X1 bị thay đổi, nó sẽ không ảnh hưởng đến các thành viên của kênh C1. Do đó, các kênh rất hữu ích vì chúng cho phép liên lạc một cách riêng tư giữa các tổ chức trực thuộc kênh. Hơn nữa, dữ liệu trong một kênh được cách ly hoàn toàn với phần còn lại của mạng, bao gồm các kênh khác.

Ngoài ra, còn có kênh hệ thống (system channel) để sử dụng cho ordering service. Nó hoạt động giống như một kênh thông thường, đôi khi nó còn được gọi là kênh ứng dụng (application channel) vì lý do trên. Chúng ta sẽ thảo luận vào kênh hệ thống ở phần kế tiếp.

## Nút (Peers) và Sổ cái (Ledger)

Trong phần này, chúng ta sẽ tìm hiểu 2 phần mới được thêm vào mạng N, đó là nút P1 và sổ cái L1.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.5.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.5.png)

Nút P1 đã tham gia kênh C1. Host P1 lưu trữ một bản sao của sổ cái L1. P1 và O4 có thể giao tiếp với nhau qua kênh C1.

Các nút là một thành phần của mạng, nó lưu trữ các bản sao của sổ cái blockchain. Dữ liệu sổ cái được lưu trên P1 có thể được truy vấn bởi các thành phần khác trong kênh.

Một phần quan trọng trong cấu hình P1 là định danh X.509 do CA1 cấp, nhằm xác thực P1 thuộc tổ chức R1. Khi P1 được tạo ra, nó có thể tham gia kênh C1 bằng cách gọi đến O4. Khi O4 nhận được yêu cầu tham gia này, nó sử dụng cấu hình kênh CC1 để xác định quyền P1 trên kênh. Ví dụ, CC1 xác định xem P1 có đọc hay ghi vào sổ cái L1 hay không ?

Chúng ta vừa biết quá trình một nút tham gia vào kênh đại khái như thế nào, chúng ta cũng sẽ được biết cách nhiều nút tham gia vào nhiều kênh như nào ở phần sau.

## Ứng dụng và hợp đồng thông minh (chaincode)

Phần này chúng ta sẽ xem cách một ứng dung client kết nối vào kênh để tương tác với sổ cái qua chaincode như thế nào.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.6.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.6.png)

Một hợp đồng thông minh S5 được cài đặt trên P1. Ứng dụng client A1 trong tổ chức R1 có thể sử dụng S5 để truy cập vào sổ cái thông qua nút P1. A1, P1 và O4 đều tham gia vào kênh C1.

Ứng dụng client A1 có thể sử dụng kênh C1 để kết nối cả nút P1 và nút orderer O4. Cũng giống như các nút và các nút orderer, một ứng dụng client sẽ cần có một định danh liên kết nó với một tổ chức. Trong ví dụ, ứng dụng client A1 được liên kết với tổ chức R1; và mặc dù nó nằm ngoài mạng blockchain Fabric, nó được kết nối với tổ chức thông qua kênh C1.

Bây giờ có vẻ như A1 có thể truy cập vào sổ cái L1 trực tiếp thông qua P1, nhưng trên thực tế, tất cả quyền truy cập được quản lý thông qua một chương trình đặc biệt gọi là hợp đồng thông minh S5. Logic của hợp đồng thông minh S5 quy định cách mà A1 có thể tương tác với dữ liệu trong sổ cái, ví dụ như chỉ có thể lấy ra một số trường thông tin nhất định từ sổ cái. Nói tóm lại, ứng dụng client A1 phải thông qua hợp đồng thông minh S5 để có thể tương tác với sổ cái L1.

Chaincode có thể được viết bởi các nhà phát triển ứng dụng trong mỗi tổ chức để thực hiện quy trình kinh doanh được chia sẻ bởi các thành viên trong hiệp hội. Chaincode được sử dụng để giúp tạo các giao dịch trong mạng. Để sử dụng được chaincode trong kênh, hai thao tác phải được thực hiện đầu tiền là cài đặt (installed) và khởi tạo (instantiated).

### Cài đặt chaincode

Mặc dù P1 đã cài đặt S5, các thành phần khác được kết nối với kênh C1 vẫn chưa biết về nó; đầu tiên nó phải được khởi tạo trên kênh C1. Trong ví dụ, một quản trị viên trong tổ chức R1 sẽ khởi tạo S5 trên kênh C1 bằng cách sử dụng P1. Sau khi khởi tạo, mọi thành phần trên kênh C1 đều biết về sự tồn tại của S5; điều đó có nghĩa là bây giờ S5 có thể được gọi bởi A1!

Lưu ý rằng rắng, mặc dù mọi thành phần trên kênh hiện có thể truy cập S5, nhưng chúng không thể thấy logic chương trình của nó. Điều này vẫn riêng tư đối với những nút đã cài đặt nó. Về mặt khái niệm, chúng ta cần phân biệt rõ ràng giữa cài đặt và khởi tạo. Cài đặt một chaincode có thể hiểu là cách lưu trữ chaincode đó tại nút được cài đặt, trong khi việc khởi tạo một chaincode như là cách thông báo sự tồn tài của nó trên kênh với các bên tham gia.


### Chính sách chứng thực (Endorsement policy)

Chính sách chứng thực mô tả quy định tổ chức nào cần phải phê duyệt giao dịch trước để chúng có thể được lưu vào sổ cái. Ở ví dụ, các giao dịch chỉ có thể được lưu vào sổ cái L1 nếu R1 hoặc R2 chứng thực chúng.

Chính sách chứng thực được quy định trong cấu hình kênh CC1.

### Gọi đến chaincode

Khi một chaincode đã được cài đặt trên một nút và được khởi tạo trên một kênh, nó có thể được gọi bởi ứng dụng client. Các ứng dụng client gửi đề xuất giao dịch cho các nút thuộc sở hữu của các tổ chức được chỉ định bởi chính sách chứng thực và nhận kết quả trả về sau khi giao dịch được hoàn tất.

## Một mạng hoàn chỉnh

Ở phần trên trong kênh C1, chỉ mới có một nút P1 thuộc R1 cùng với ứng dụng client A1. Phần này chúng ta sẽ có thêm các thành phần khác của tổ chức R2 trên kên C1.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.7.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.7.png)

R2 đã thêm nút ngang hàng P2, nơi lưu trữ một bản sao của sổ cái L1 và chaincode S5 và có ứng dụng client A2. A2 và P2 được định danh bằng các chứng chỉ từ CA2. Bây giờ, cả hai ứng dụng A1 và A2 đều có thể gọi S5 trên C1 bằng cách sử dụng nút P1 hoặc P2.

Cũng tương tự như P1, P2 được tạo và thêm vào kênh C1 bởi một quản trị viên trong tổ chức của nó.

Chúng ta đã có một kênh trong đó các tổ chức R1 và R2 có thể giao dịch với nhau. Cụ thể, các ứng dụng A1 và A2 có thể tạo giao dịch thông qua hợp đồng thông minh S5 và sổ cái L1 trên kênh C1.

### Khởi tạo và xác thực giao dịch

Có thể chia ra 2 loại nút: có cài đặt và không cài đặt chaincode. Các nút không được cài đặt chaincode chỉ có thể biết về giao diện (interface) của chaincode  bằng cách được kết nối với kênh thay vì có thể thực thi chaincode như các nút được cài đặt.

Các nút có cài đặt hợp đồng chaincode là nơi khởi tạo ra các giao dịch. Lưu ý rằng, tất cả các nút có thể xác nhận (validate) và sau đó chấp nhận hoặc từ chối việc giao dịch được thêm vào sổ cái. Tuy nhiên, chỉ các nút có cài đặt chaincode mới có thể tham gia vào quá trình chứng thực giao dịch (endorsement).

### Các loại nút (Types of peers)

Trong Hyperledger Fabric các nút tuy giống nhau nhưng có thể đảm nhận nhiều vai trò tùy thuộc vào cách cấu hình mạng. 

-   **Committing peer**: Mỗi nút trong một kênh là một nút committing. Nó nhận được các block chưa các giao dịch được tạo, sau đó được xác thực trước khi chúng được thêm vào chuỗi.
    
-   **Endorsing peer**: Nút endorsing là nút được cài đặt chaincode. Tuy nhiên, để thực sự là một nút endorsing, chaincode trên nút phải được ứng dụng client sử dụng tạo một giao dịch được ký số.
    
Chính sách chứng thực cho chaincode xác định các tổ chức có nút nên ký điện tử một giao dịch được tạo trước khi có thể được chấp nhận trên một bản sao ngang hàng cam kết của sổ cái.

Ở trên là hai loại nút chính; có hai vai trò khác mà nút có thể đảm nhận là:

-   **Leader peer**: Khi một tổ chức có nhiều nút trong một kênh, nút leader là nút chịu trách nhiệm chuyển tiếp các giao dịch từ orderer đến các các nút commit khác trong tổ chức. Có 2 kiểu thiết lập nút leader là tĩnh (static) và động (dynamic).
    
Đối với tùy chọn leader là tĩnh, nhiều nút được cấu hình làm người lãnh đạo. Đối với tùy chọn động, một nút sẽ được bầu làm leader theo tập hợp, nếu một nút leader bị lỗi, thì các nút còn lại sẽ bầu lại một leader mới.
    
Điều đó có nghĩa là một tập hợp các nút trong một tổ chức có thể có một hoặc nhiều nhà leader được kết nối với ordering service. Điều này có thể giúp cải thiện khả năng phục hồi và mở rộng trong các mạng lớn với khối lượng giao dịch cao.
    
-   **Anchor peer**. Nếu một nút cần liên lạc với các nút trong một tổ chức khác, thì nó có thể sử dụng một trong các nút anchor được định nghĩa trong cấu hình kênh của tổ chức đó. Một tổ chức có thể có 0 hoặc nhiều nút anchor.

Lưu ý rằng, một nút trên kênh có thể vừa là một nút committing, một nút endorsing, một nút leader và một nút anchor cùng lúc! Trong một kênh luôn phải có ít nhất một nút committing, nút leader và nút endorsing, nút anchor là tùy chọn tùy theo nhu cầu giao tiếp trong kênh.

### Cài đặt chứ không khởi tạo (Install not instantiate)

Quay lại việc tương tác với chaincode thông qua ứng dụng, R2 phải cài đặt chaincode S5 lên nút của nó P2 nếu muốn các ứng dụng A1 hoặc A2 sử dụng S5 trên nút P2 để tạo giao dịch. Sau khi cài đặt S5, P2 hiện đang lưu trữ mã nguồn của chaincode và dữ liệu sổ cái. Giống như P1, nó có thể tạo và xác nhận các giao dịch với bản sao của sổ cái L1.

Tuy nhiên, R2 không cần khởi tạo chaincode S5 trên kênh C1. Là vì S5 đã được tổ chức R1 khởi tạo trên kênh. Khởi tạo chỉ cần xảy ra một lần; bất kỳ nút nào sau đó tham gia kênh đều biết rằng chaincode S5 đã có trong kênh. Các bản sao của chaincode S5 thường sẽ được triển khai giống hệt nhau bằng cùng một ngôn ngữ lập trình, nếu không, ít nhất chúng phải tương đương về mặt ngữ nghĩa.

## Đơn giản hóa sơ đồ một chút

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.8.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.8.png)

Sơ đồ hiển thị các sự kiện liên quan đến kênh C1 trong mạng N như sau: Ứng dụng client A1 và A2 có thể sử dụng kênh C1 để kết nối với các nút P1 và P2 và ordered O4. Các nút P1 và P2 có thể sử dụng các dịch vụ liên lạc của kênh C1. Ordering serive O4 có thể sử dụng các dịch vụ truyền thông của kênh C1. Cấu hình kênh CC1 áp dụng cho kênh C1.

Sơ đồ trên đã được đơn giản hóa bằng cách thay thế các đường nối bằng các vòng tròn màu xanh bên trong chứa số của kênh. Điều này giúp sơ đồ đơn giản, dễ nhìn hơn nhất là khi thêm nhiều kênh và nhiều nút khác vào mạng.

## Thêm một hiệp hội khác

Trong phần này, chúng ta sẽ có thêm tổ chức R3. Chúng ta sẽ tạo ra một kênh cho các tổ chức R2 và R3 giao dịch với nhau. Kênh này sẽ hoàn toàn tách biệt với kênh được xác định trước đó.

Hiệp hội X2, bao gồm R2 và R3:

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.9.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.9.png)

Một admin (_network administrator_) từ tổ chức R1 hoặc R4 là người thêm hiệp hội X2 vào mạng N. 

Một kênh mới chỉ có thể được tạo bởi những tổ chức được chỉ định trong cấu hình mạng NC4, trong ví dụ là R1 và R4. 

## Thêm một kênh mới

Sử dụng định nghĩa từ hiệp hội X2, để tạo một kênh mới C2.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.10.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.10.png)

Kênh C2 có cấu hình kênh CC2, tách biệt hoàn toàn với cấu hình mạng NC4 và cấu hình kênh CC1. Kênh C2 được quản lý bởi R2 và R3. R1 và R4 không có quyền với CC2.

Cấu hình kênh CC2 chứa các chính sách về việc chi phối tài nguyên kênh, gán quyền quản lý cho các tổ chức R2 và R3 qua kênh C2. Nó được quản lý độc quyền bởi R2 và R3; R1 và R4 không có quyền trên kênh C2. Cấu hình kênh CC2 sau này có thể được cập nhật để thêm các tổ chức để hỗ trợ khác, nhưng điều này chỉ có thể được thực hiện bởi R2 hoặc R3.

Khi mạng và các kênh phát triển, cấu hình mạng và kênh cũng cần có sự điều chỉnh. Mọi thay đổi cấu hình đều dẫn đến tạo ra một giao dịch, chúng sẽ được xác thực và đưa vào sổ cái, đều này thuận lợi cho việc giám sát sự thay đổi của cấu hình kênh.

### Cấu hình mạng và kênh 

Các cấu hình cho mạng và kênh rất quan trọng vì chúng gói gọn các chính sách được các thành viên trực thuộc đồng thuận, cung cấp một quy định chung để kiểm soát truy cập vào tài nguyên trong mạng hoặc kênh. Chúng cũng chứa thông tin về thành phần khác, chẳng hạn như tên của hiệp hội và các tổ chức trong đó.

Trong ví dụ, khi mạng được hình thành ban đầu với nút orderer O4, hành vi của nó bị chi phối bởi cấu hình mạng NC4. Cấu hình ban đầu của NC4 chỉ chứa các chính sách cho phép tổ chức R4 quản lý tài nguyên mạng. NC4 sau đó được cập nhật để cho phép thêm R1 quản lý. Khi thay đổi này được thực hiện, bất kỳ admin nào từ tổ chức R1 hoặc R4 kết nối với O4 sẽ có quyền quản lý mạng vì đó là chính sách đã được quy đinh trong NC4. Mỗi nút orderer ghi lại từng kênh trong cấu hình mạng, sao cho có một bản ghi của từng kênh được tạo ở cấp độ mạng.

Điều đó có nghĩa là mặc dù nút orderer O4 là tác nhân tạo ra hiệp hội X1 và X2 và các kênh C1 và C2, trí thông minh của mạng được chứa trong cấu hình mạng NC4 mà O4 đang tuân theo. Miễn là O4 hoạt động như một diễn viên giỏi và thực hiện đúng các chính sách được xác định trong NC4 bất cứ khi nào nó xử lý tài nguyên mạng, mạng của chúng tôi sẽ hoạt động như tất cả các tổ chức đã đồng ý. Theo nhiều cách, NC4 có thể được coi là quan trọng hơn O4 bởi vì, cuối cùng, nó kiểm soát truy cập mạng.

Trong ví dụ, khi các nút P1 và P2 tương tác với các ứng dụng client A1 hoặc A2, mỗi nút dựa theo các chính sách được quy định trong cấu hình kênh CC1 để kiểm soát quyền truy cập vào tài nguyên kênh C1.

Ví dụ: nếu A1 muốn truy cập chaincode S5 trên các nút P1 hoặc P2, mỗi nút sẽ đối chiếu với chính sách để xem các hoạt động mà A1 có thể thực hiện. Ví dụ, A1 có thể được phép đọc hoặc ghi dữ liệu từ sổ cái L1 theo các chính sách được quy định trong CC1. Tương tự với kênh C2.

Mặc dù mỗi kênh hoặc mỗi mạng có một cấu hình duy nhất, nhưng nó thực sự được nhân bản và lưu giữ bởi mọi nút trong mạng hoặc kênh. Ví dụ, trong các nút P1 và P2 của đều có bản sao cấu hình kênh CC1, tương tự thì P2 và P3 có bản sao cấu hình CC2 của kênh C2 . Nút ordered O4 cũng lưu giữ bản sao cấu hình mạng - kênh.

Để thay đổi cấu hình mạng hoặc kênh, quản trị viên phải gửi giao dịch để thay đổi cấu hình mạng hoặc kênh. Nó phải được ký bởi các tổ chức được chỉ định trong chính sách về việc thay đổi cấu hình của kênh - mạng. Chính sách này được gọi là `mod_policy` và chúng ta sẽ thảo luận về nó sau.

Các nút ordering service có một **mini blockchain**, được kết nối thông qua kênh hệ thống (system channel).Mini blockchain này cùng với các giao dịch diễn ra nhằm duy trì một bản sao nhất quán của cấu hình mạng tại mỗi nút orderer.


## Thêm nút mới

Ở phần này, chúng ta sẽ thêm nút P3 thuộc R3 vào kênh C2, cùng với đó là cài đặt chaincode S6 và sổ cái L2 lên P3.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.11.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.11.png)

Sơ đồ hiển thị các sự kiện liên quan đến các kênh C1 và C2 trong mạng N như sau: Ứng dụng client A1 và A2 có thể sử dụng kênh C1 để giao tiếp với các nút P1, P2 và ordering service O4; ứng dụng khách A3 sử dụng kênh C2 để giao tiếp với P3 và ordering service O4. Ordering service O4 tham gia cả vào kênh C1 và C2. 

Kênh C2 có sổ cái L2 và chaincode S6 riêng của nó, ứng dụng A3 có thể gọi chaincode S6 để tương tác với sổ cái L2 thông qua kênh C2. S6 và L2 hoàn toàn độc lập với L1 và S5 trên kênh C1.

## Thêm nút vào nhiều kênh khác nhau

Như chúng ta đã biết, tổ chức R2 trực thuộc 2 hiệp hội X1 và X2. Kênh C1 là nơi giao tiếp của các tổ chức trong X1, tương tự là kênh C2 thuộc hiệp hội X2. Nút P2 thuộc R2 đã tham gia vào kênh C1, bây giờ nó cũng có thể tham gia vào kênh C2 !


![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.12.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.12.png)


Giờ đây, khi đã thêm P2 vào kênh C2, nó có thể thực hiện các giao dịch riêng tư với các nút thuộc R1 ở kênh C1 và nhảy sang kênh C2 nếu muốn giao dịch với các nút từ tổ chức R3.

Nút P2 tham gia cả 2 kênh vào hiện có 2 sổ cái L1 và L2, cùng với đó là 2 chaincode S5 và S6.

Khi giao dịch trên kênh C1, nút P2 sẽ tuân thủ các chính sách, quy tắc được chỉ định trong cấu hình kênh CC1. Khi khác, P2 thực hiện các giao dịch trên kênh C2 thì nó sẽ tuân theo CC2, CC1 ở thời điểm đó sẽ không có ý nghĩa gì cả.

Tương tự như vậy, chúng ta có thể thấy ứng dụng client A2 hiện có thể giao dịch trên các kênh C1 và C2. Và tương tự P2, nó cũng sẽ bị chi phối bởi các chính sách trong các cấu hình kênh tương ứng.

### The ordering service

Bạn đọc quan sát có thể nhận thấy rằng ordering service O4 dường như là một thành phần tập trung; nó được sử dụng để tạo mạng ban đầu và kết nối với mọi kênh trong mạng. Mặc dù chúng ta đã thêm R1 và R4 vào chính sách cấu hình mạng NC4 để quản lý orderer, nút O4 vẫn đang chạy trên cơ sở hạ tầng R4. Trong một hệ thống phi tập trung, điều này có vẻ không đúng lắm !

Đừng lo lắng, trong ví dụ của chúng ta mô tả một ordering service đơn giản để chúng ta dễ làm quen khi mới bắt đầu. Trong thực tế, ordering service có thể tự nó hoàn toàn phi tập trung! Phần trước chúng ta đã biết rằng, một ordering service có thể bao gồm nhiều nút riêng lẻ thuộc sở hữu của các tổ chức khác nhau.

Hãy cùng xem một cấu trúc mạng có nhiều hơn một nút orderer:

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.15.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.15.png)

Ở hình trên, ordering service bao gồm các nút O1 và O4. O1 thuộc R1 và O4 là thành viên của R4. 

Chúng ta có thể thấy rằng ordering service này hoàn toàn phi tập trung - các nút orderer thuộc nhiều tổ chức khác nhau. Chính sách cấu hình mạng của NC4, cho phép quyền bình đẳng của R1 và R4 đối với tài nguyên mạng. Các ứng dụng client và các nút từ các tổ chức R1 và R4 có thể quản lý tài nguyên mạng bằng cách kết nối với nút O1 hoặc nút O4, vì cả hai nút hoạt động theo cùng một cách, được xác định bởi các chính sách trong cấu hình mạng NC4. Trong thực tế, các bên từ một tổ chức cụ thể có xu hướng sử dụng cơ sở hạ tầng do tổ chức của họ cung cấp, nhưng không chắc chắn lúc nào cũng như vậy.

### Phân phối giao dịch phi tập trung (De-centralized transaction distribution)

Ngoài việc là một điểm quản lý trên mạng, ordering service còn có một vai trò khác - đó là điểm phân phối các giao dịch. Ordering service là thành phần tập hợp các giao dịch được chứng thực từ các ứng dụng và đưa chúng vào các block, sau đó được phân phối cho mọi nút trong kênh. Tại mỗi nút, các giao dịch được ghi lại, cho dù hợp lệ hay không hợp lệ và bản sao sổ cái địa của chúng được cập nhật.

Vai trò của nút ordering service là rất khác nhau ở cấp độ mạng và kênh.Khi hoạt động ở cấp kênh, vai trò của O4 là thu thập các giao dịch, đưa chúng vào các block và phân phối đến các nút bên trong kênh C1. Nó thực hiện điều này theo các chính sách được xác định trong cấu hình kênh CC1. Ngược lại, khi hoạt động ở cấp độ mạng, vai trò của O4 là cung cấp một điểm quản lý tài nguyên mạng theo các chính sách được xác định trong cấu hình mạng NC4.

### Thay đổi chính sách

Suốt từ đầu đến giờ, chúng ta cứ thao thao bắt tuyệt về các chính sách được cấu hình trong kênh hoặc mạng mà chưa mục kích sở thị nó như nào. Phần này chúng ta sẽ đi tìm hiểu, thảo luận một vài chính sách để chúng ta hiểu rõ hơn.

Hyperledger Fabric cung cấp một chính sách cho phép các admin của mạng và kênh tự quản lý việc thay đổi chính sách! Triết lý cơ bản là sự thay đổi chính sách là một hằng số, cho dù nó xảy ra trong hoặc giữa các tổ chức, hoặc liệu nó được áp đặt bởi các cơ quan quản lý bên ngoài. Ví dụ: các tổ chức mới có thể tham gia một kênh hoặc các tổ chức hiện tại có thể tăng hoặc giảm quyền của họ. Hãy để điều tra thêm một chút về cách thực hiện chính sách thay đổi trong Hyperledger Fabric.

Điểm quan trọng trong chính sách của Fabric là việc thay đổi chính sách được quản lý bởi một chính sách khác - nói cách khác thì nó là chính sách cốt lõi quyết định các chính sách khác. Chính sách sửa đổi, tiếng anh viết tắt là `mod_policy`, là chính sách cốt lõi trong cấu hình mạng hoặc kênh. Chúng ta hãy xem qua hai ví dụ ngắn gọn về cách sử dụng `mod_policy `để quản lý thay đổi trong mạng của mình.

Ví dụ đầu tiên là khi mạng được thiết lập ban đầu. Tại thời điểm này, chỉ có tổ chức R4 được phép quản lý mạng. Trong thực tế, điều này đã đạt được bằng cách biến R4 thành tổ chức duy nhất được xác định trong cấu hình mạng NC4 có quyền đối với tài nguyên mạng. Hơn nữa, `mod_policy` cho NC4 chỉ đề cập đến tổ chức R4 - chỉ có R4 được phép thay đổi cấu hình này.

Sau đó, chúng ta đã phát triển mạng N để cho phép tổ chức R1 quản trị mạng. R4 đã thêm R1 vào các chính sách để tạo kênh và tạo hiệp hội. Nhờ điều này, R1 đã có thể tạo X1, X2 và tạo các kênh C1, C2. R1 có quyền quản trị tương đương với R4 trong việc tạo kênh, hiệp hội.

Tuy nhiên, R4 vẫn đang có nhiều thẩm quyền hơn R1! R4 có thể thêm R1 vào `mod_policy `sao cho R1 cũng có thể quản lý thay đổi chính sách mạng. Khi đó, quyền của 2 tổ chức là ngang nhau trong mạng.

Giờ đây, R1 có toàn quyền kiểm soát cấu hình mạng NC4! Điều này có nghĩa là về nguyên tắc, R1 có thể loại bỏ quyền quản lý R4 khỏi mạng. Trong thực tế, R4 sẽ cấu hình `mod_policy` các sự thay đổi trong đó cần được R4 chấp nhận để thành công. 

## Cùng xem lại cấu trúc mạng hoàn chỉnh


![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.14.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/network.diagram.14.png)

*Trong sơ đồ này, chúng ta thấy rằng mạng blockchain Fabric bao gồm hai kênh ứng dụng và một kênh ordering. Các tổ chức R1 và R4 chịu trách nhiệm cho kênh ordering, R1 và R2 chịu trách nhiệm cho kênh ứng dụng màu xanh trong khi R2 và R3 chịu trách nhiệm cho kênh ứng dụng màu đỏ. Ứng dụng client A1 là một thành phần của tổ chức R1 và CA1 là cơ quan cấp chứng chỉ của nó. Lưu ý rằng, nút P2 của tổ chức R2 tham gia cả 2 kênh ứng dụng màu xanh và màu đỏ. Mỗi kênh ứng dụng có cấu hình kênh riêng, trong trường hợp này là CC1 và CC2. Cấu hình kênh của kênh hệ thống là một phần của cấu hình mạng, NC4.*

## Tóm tắt các thành phần mạng

-   [Sổ cái](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#ledger)
-   [Hợp đồng thông minh](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#smart-contract)  (aka chaincode)
-   [Nút - Peers node](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#peer)
-   [Ordering service](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#ordering-service)
-   [Kênh](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#channel)
-   [Cơ quan cấp chứng chỉ](https://hyperledger-fabric.readthedocs.io/en/release-1.4/glossary.html#hyperledger-fabric-ca)

<br>


[<- Phần trước: Mô hình](./3-model.md)

[-> Phần sau: Định danh](./5-indentity.md)



[<- Phần trước: Mạng](./3-network.md)

[-> Phần sau: Membership](./6-membership.md)

# Định danh (Identity)

## Định danh là gì ?

Như chúng ta đã biết, có rất nhiều thành phần tham gia, tương tác với mạng Fabric bao gồm các nút (peers), orderers, ứng dụng client, admin của các tổ chức..v.v. Mỗi thành phần này đều có một danh tính theo chuẩn X.509. Danh tính này giúp xác định các quyền đối với tài nguyên và quyền truy cập vào thông tin của từng thành phần.

Ngoài ra, danh tính số còn có một số thuộc tính bổ sung mà Fabric sử dụng để xác định quyền truy cập, đó là **principal**. Principal giống như userID hoặc groupID, nhưng linh hoạt hơn một chút vì chúng có thể bao gồm một loạt các thuộc tính khác như tên tổ chức trực thuộc, thuộc đơn vị nào trong tổ chức, vai trò hoặc thậm chí là danh tính cụ thể.

Để một danh tính có thể kiểm chứng được, nó phải được đến từ một cơ quan đáng tin cậy. Nhà cung cấp dịch vụ thành viên (Membership service provider - MSP) là thành phần đảm nhiệm vai trò đó. Cụ thể hơn, MSP là có nhiệm vụ cung cấp các danh tính hợp lệ cho các tổ chức. Theo mặc định, MSP trong Fabric sử dụng các chứng chỉ X.509 làm định danh, áp dụng mô hình phân cấp cơ sở hạ tầng khóa công khai (PKI) truyền thống (chúng ta sẽ nói rõ hơn về PKI ở phần sau).

## Ví dụ đơn giản giải thích việc sử dụng danh tính

Hãy tưởng tượng rằng bạn đi siêu thị và mua một số hàng hóa cần thiết. Khi thanh toán, quầy chỉ chấp nhận thanh toán bằng các loại thẻ Visa, Mastercard hoặc AMEX. Bạn chỉ có thẻ ImagineCard chẳng hạn, dù thẻ này có bao nhiều tiền trong tài khoản đi nữa, nó cũng không được chấp nhận thanh toán tại quầy.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.6.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.6.png)

Có một thẻ tín dụng hợp lệ là chưa đủ - nó cần phải được cửa hàng chấp nhận nữa! PKI và MSP cũng tương tự như ví dụ trên - PKI cung cấp danh sách các định danh và MSP cho biết ai trong số này là thành viên của một tổ chức nhất định tham gia vào mạng.

PKI giống như một nhà cung cấp thẻ - nó phân phối nhiều loại nhận dạng có thể kiểm chứng khác nhau. Còn MSP giống như danh sách các nhà cung cấp thẻ được cửa hàng chấp nhận, xác định danh tính nào là thành viên liên kết (được hỗ trợ) của cửa hàng.

Hãy cũng tìm hiểu chi tiết hơn về các khái niệm này một chút.

## PKIs là gì ?

Cơ sở hạ tầng khóa công khai (public key infrastructure - PKI) là tập hợp các công nghệ cung cấp sự an toàn, bảo mật khi giao tiếp trên mạng. 

Có thành phân chính của PKI:
-   **Digital Certificates** (Chứng thư số)
-   **Public and Private Keys** (Khóa công khai và khóa bí mật)
-   **Certificate Authorities** (Cơ quan cấp chứng chỉ)
-   **Certificate Revocation Lists** (Danh sách các chứng chỉ bị thu hồi)

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.7.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.7.png)


Các cơ quan cấp chứng chỉ (CA) có nhiệm vụ cấp cấp chứng chỉ cho các bên liên quan (ví dụ: người dùng dịch vụ, nhà cung cấp dịch vụ). Danh sách thu hồi chứng chỉ CA (CRL) chứa danh sách các chứng chỉ không còn hiệu lực. Việc thu hồi chứng chỉ có thể xảy ra vì một số lý do. Ví dụ: một chứng chỉ có thể bị thu hồi khóa bí mật dùng để mã hóa đã bị lộ.

Hyperledger Fabric dựa trên tiêu chuẩn PKI để đảm bảo liên lạc an toàn giữa những người tham gia mạng và đảm bảo rằng các thông điệp được truyền đi trên mạng blockchain được xác thực chính xác. 

### Chứng thư số (Digital Certificates)

Chứng thư số là một tài liệu bao gồm một tập hợp các thuộc tính liên quan đến người giữ chứng chỉ. Loại chứng chỉ số phổ biến nhất là loại chứng thư tuân thủ theo tiêu chuẩn X.509.

Ví dụ: Mary Morris trong bộ phận sản xuất của Mitchell Cars ở Detroit, Michigan có thể có chứng chỉ kỹ thuật số với thuộc tính `SUBJECT` là `C = US`, `ST = Michigan`, `L = Detroit`, `O = Mitchell Cars`, `OU = Manufacturing`, `CN = Mary Morris / UID = 123456`. Chứng thư số cung cấp các thông tin về Mary mà cô ấy có thể dùng để chứng minh chức vụ công tác của mình. Có nhiều thuộc tính khác trong chứng thư X.509, nhưng bây giờ hãy tập trung vào những thứ này.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.8.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.8.png)

Chứng thư chứa rất nhiều thông tin, như bạn có thể thấy trên hình. Trong chứng thư, chúng ta thấy có trường thông tin về khóa công khai của Mary có ở trong chứng thư, trong khi khóa bí mật của cô ấy thì không. Khóa bí mật chỉ nên được biết bởi một mình Mary.

Chứng thư số sử dụng hệ mật mã toán học để chống việc giả mạo chứng thư. Hệ mật mã cho phép Mary xuất trình chứng thư của mình cho người khác để chứng minh danh tính của mình miễn là bên kia tin tưởng vào cơ quan cấp chứng chỉ (CA). Miễn là private key của Mary không bị lộ ra ngoài, thì bất cứ ai xem thông tin trên chứng thư số đều sẽ chắc chắn rằng thông tin về Mary là xác thực, không bị giả mạo.

### Xác thực, khóa công khai và khóa bí mật

Xác thực và toàn vẹn dữ liệu là các khái niệm quan trọng trong an toàn thông tin. Xác thực yêu cầu các bên trao đổi thông điệp được đảm bảo về danh tính của bên trao đổi. Một thông điệp để có tính toàn vẹn có nghĩa là không thể sửa đổi nó trong quá trình truyền tin. Ví dụ, bạn có thể muốn chắc chắn rằng bạn đang giao tiếp với Mary Morris thực sự chứ không phải là một kẻ mạo danh. Hoặc nếu Mary đã gửi cho bạn một tin nhắn, bạn có muốn chắc chắn rằng nó đã bị sửa đổi bởi bất kỳ ai khác trong quá trình truyền tin.

Các cơ chế xác thực truyền thống dựa trên chữ ký số. Chữ ký số đảm bảo được về cả tính xác thực và tính toàn vẹn (kết hợp thêm với hàm băm).

Để áp dụng chữ ký số trong giao tiếp trên mạng, mỗi bên tham gia cần có 1 khóa công khai và 1 khóa bí mật. 2 khóa này là 1 cặp và tương ứng với nhau. Khi thực hiện ký số, bên gửi sẽ mã hóa thông điệp bằng khóa bí mật (chỉ người đó biết) và gửi đi. Khi nhận được thông điệp, bên nhận sẽ dùng khóa công khai của bên gửi và giải mã thông điệp, nếu giải mã thành công thì chính xác thông điệp không bị giả mạo vì chỉ bên gửi mới có khóa bí mật để mã hóa.


![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.9.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.9.png)

Trong ví dụ trên, Mary sử dụng khóa riêng của mình để ký tin nhắn. Chữ ký có thể được xác nhận bởi bất cứ ai có khóa công khai của cô ấy.

### Cơ quan cấp chứng chỉ (Certificate Authorities)

Như chúng ta đã biết, các thành phần tham gia vào mạng Fabric bằng định danh riêng của mình. Định danh được cung cấp ở dạng chứng thư số theo chuẩn X.509 và được cấp bởi Cơ quan cấp chứng chỉ (CA).

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.11.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.11.png)

CA có một cặp khóa công khai - bí mật. Các chứng thư được CA ký số và ánh xạ với khóa công khai của bên được cấp chứng thư. Kết quả là, nếu một người tin tưởng CA, họ có thể tin tưởng rằng khóa công khai các chứng thư do CA cấp chính xác là khóa công khai của chủ sở hữu chứng thư.

Các CA cũng có một chứng thư mà họ cung cấp rộng rãi. Điều này cho phép người tiêu dùng nhận dạng do một CA cụ thể cấp để xác minh họ bằng cách kiểm tra rằng chứng chỉ chỉ có thể được tạo bởi chủ sở hữu khóa riêng tương ứng (CA).


### Root CAs, Intermediate CAs and Chains of Trust)

CA có 2 loại:
- CA gốc (Root CA)
- CA trung gian (Intermediate CA)

Một CA chịu trách nhiệm cung cấp một lớn lớn chứng thư cho người dùng tìm ẩn rủi ro cao, nếu lỡ bị lộ khóa bí mật của CA, hậu quả sẽ khôn lường. Do đó, người ta đề xuất ra mô hình cung cấp chứng thư gồm có CA gốc và các CA trung gian nhằm phân phối chứng thư một cách an toàn, phân tán hơn. Một CA trung gian có thể được cấp quyền bởi CA gốc hoặc một CA khác, từ đó sẽ tạo thành một chuỗi các CA có tính tin cậy cao. Khi một CA trung gian bị lộ khóa bí mật thì rủi rõ cũng giảm đi rất nhiều.

Các CA trung gian 

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.1.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.1.png)

Các CA trung gian cung cấp sự linh hoạt rất lớn khi phát hành chứng thư trên nhiều tổ chức và điều đó rất hữu ích trong một hệ thống blockchain riêng tư (như Fabric). Ví dụ, các tổ chức khác nhau có thể sử dụng các CA gốc khác nhau hoặc cùng một CA gốc với các CA trung gian khác nhau - điều này thực sự phụ thuộc vào nhu cầu của mạng.

### Fabric CA

Hyperledger Fabric cung cấp một thành phần CA tích hợp trong hệ thống giúp bạn có thể tạo ra các CA riêng cho mạng của mình - được gọi là Fabric CA. Fabric CA không có khả năng cung cấp chứng chỉ SSL để trên trình duyệt.

Các bạn có thể đọc thêm về Fabric CA ở [đây](https://hyperledger-fabric-ca.readthedocs.io/en/release-1.4/)

## Danh sách thu hồi chứng thư (Certificate Revocation Lists)

Danh sách thu hồi chứng thư (CRL) rất dễ hiểu - nó đơn giản chỉ là một danh sách chứng thư mà CA đã thu hồi.

Khi một bên thứ ba muốn xác minh danh tính của một bên khác, trước tiên, họ sẽ kiểm tra CRL của đang phát hành để đảm bảo rằng chứng thư chưa bị thu hồi. Các chứng thư bị thu hồi có thể đến từ nhiều lý do khác nhau, ví dụ như bị lộ khóa bí mật chẳng hạn.

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.12.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/identity.diagram.12.png)

Lưu ý rằng chứng chỉ bị thu hồi rất khác với chứng thư hết hạn.

Qua bài này, chúng ta đã hiểu được phần nào các PKI xây dựng danh tính trên mạng truyền thông, bước tiếp chúng ta sẽ xem cách các danh tính, định danh sử dụng để đại diện cho các thành viên trong mạng blockchain như thế nào ? Đó là nội dung của phần tiếp theo khi chúng ta cùng tim hiểu về nhà cung cấp dịch vụ thành viên (MSP).

[<- Phần trước: Mạng](./3-network.md)

[-> Phần sau: Membership](./6-membership.md)




 
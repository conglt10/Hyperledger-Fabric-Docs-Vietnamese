# Tư cách thành viên (Membership)

Ở phần trước, chúng ta đã cùng tìm hiểu PKI và biết cách một định danh có thể được cung cấp và xác thực như thế nào. Ở phần này, chúng ta hãy xem cách các định danh được sử dụng như thế nào trong mạng blockchain Fabric.

Nhà cung cấp dịch vụ thành viên (Membership Service Provider - MSP) có nhiệm vụ xác định các CA gốc và CA trung gian nào đáng tin cậy nhằm xác định các thành viên của một tổ chức, bằng cách liệt kê danh tính của các thành viên trong một tổ chức hoặc xác định CA nào được ủy quyền cấp danh tính hợp lệ cho tổ chức đó, hay đơn giản hơn là kết hợp cả 2 cách trên.

Vai trò của MSP không chỉ đơn giản là liệt kê ai là người tham gia mạng hoặc thành viên của kênh. MSP có thể xác định các vai trò cụ thể của thực thể trong tổ chức mà MSP đại diện (ví dụ: quản trị viên hoặc là thành viên bình thường), đặt cơ sở để xác định các đặc quyền truy cập trong  mạng và kênh (ví dụ: quản trị viên kênh, chỉ đọc, có thể ghi).

Cấu hình của MSP được quảng bá cho tất cả các kênh nơi các thành viên của tổ chức tương ứng với MSP tham gia (dưới dạng kênh MSP). Ngoài MSP kênh, các nút (peers), orderers và ứng dụng client cũng duy trì MSP cục bộ để xác thực các thông báo thành viên bên ngoài ngữ cảnh của kênh và để xác định các quyền đối với một thành phần cụ thể (ví dụ người có thể cài đặt chaincode trên các peer).

Ngoài ra, MSP có thể cho phép xác định danh sách các đinh danhđã bị thu hồi - như đã thảo luận trong phần định danh.


# Ánh xạ MSP đến các tổ chức

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.3.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.3.png)


## Đơn vị tổ chức và MSP

## Local and Channel MSPs

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.4.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.4.png)


## MSP Levels

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.2.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.2.png)


## MSP Structure

![https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.5.png](https://hyperledger-fabric.readthedocs.io/en/release-1.4/_images/membership.diagram.5.png)





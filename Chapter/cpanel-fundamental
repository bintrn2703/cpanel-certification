# cPanel Fundamental
## System
### So sánh CPanel và WHM? 
Giống như một tòa nhà chung cư. Mỗi giao diện cPanel sẽ tồn tại như một căn hộ trong tòa nhà. WHM giống như tòa nhà và là giao diện dành cho admin. Quản trị viên đăng nhập vào WHM bằng tài khoản root cho hệ thống - đây là tài khoản có thể làm bất cứ điều gì họ muốn trên máy chủ mà không bị hạn chế. 
### Resource là gì? 
Là các thành phần hệ thống như RAM, đisk (cả hiệu suất và dung lượng ổ đĩa), sức mạnh xử lý của CPU và băng thông/thông lượng. 
### Raid
So sánh raid 0, raid 1 và raid 10
| Loại RAID      | Đặc điểm chính                                                    | Ưu điểm                                                     | Nhược điểm                                                  | Dùng cho mục đích nào                  |
|----------------|------------------------------------------------------------------|------------------------------------------------------------|-------------------------------------------------------------|----------------------------------------|
| **RAID 0**     | Chia nhỏ dữ liệu ra các ổ đĩa để tăng tốc độ đọc/ghi            | Tốc độ cao                                                | Không có dự phòng (nếu một ổ đĩa hỏng, toàn bộ dữ liệu sẽ mất) | Khi cần tốc độ cao và không quan trọng về dự phòng |
| **RAID 1**     | Sao chép dữ liệu đồng nhất lên hai hoặc nhiều ổ đĩa             | Độ tin cậy và khả năng dự phòng tốt                        | Hiệu quả sử dụng dung lượng thấp (cần gấp đôi số ổ đĩa)    | Khi cần bảo vệ dữ liệu và dự phòng  |
| **RAID 10**    | Kết hợp RAID 0 và RAID 1 (sao chép và chia nhỏ dữ liệu)         | Tốc độ cao và khả năng dự phòng tốt                        | Cần nhiều ổ đĩa hơn (ít nhất 4 ổ đĩa)                      | -Khi cần tốc độ cao và bảo vệ dữ liệu |

## DNS
### DNS là gì?
DNS là hệ thống để chuyển đổi (phân giải) những tên miền dễ nhớ thành những địa chỉ IP không dễ nhớ. 
### Resolver là gì? 
Resolver (Resolving namespace) là một máy chủ phản hồi các yêu cầu DNS đối với các tên miền mà nó không có thẩm quyền. Nameserver có thẩm quyền có nghĩa là nameserver đó là nơi tốt nhất để tìm thông tin hiện tại cho tên miền đó. 
### TTL number là gì? 
TTL number là khoảng thời gian tồn tại của 1 DNS Record được tính bằng giây, lưu trong cache zone (vùng nhớ cache). 
### Cách hoạt động của DNS? 
1. Nhập một tên miền vào thanh địa chỉ của trình duyệt và nhấn Enter.
2. Trình duyệt sẽ kiểm tra bộ nhớ cache của nó để xem liệu đã có thông tin DNS cho tên miền đó chưa. Nếu đã có, nó sẽ dùng thông tin này để kết nối với server mà không cần tiếp tục các bước sau.
3. Nếu trình duyệt không có thông tin, yêu cầu sẽ được gửi đến hệ điều hành để kiểm tra bộ nhớ cache của nó.
4. Nếu hệ điều hành không có thông tin, yêu cầu sẽ được gửi đến DNS Resolver.
5. DNS Resolver sẽ kiểm tra bộ nhớ cache của nó. Nếu không có thông tin, nó sẽ bắt đầu quá trình truy vấn các server DNS khác.
6. DNS Resolver sẽ liên hệ với một trong các Root Server để tìm thông tin về các server DNS cấp cao hơn (TLD - Top-Level Domain servers).
7. Root Server sẽ trả về địa chỉ IP của TLD Server cho miền cấp cao nhất (như .com, .org, .net).
8. DNS Resolver sẽ tiếp tục liên hệ với TLD Server, server này sẽ trả về địa chỉ của Authoritative DNS Server cho tên miền cụ thể.
9. Authoritative DNS Server sẽ cung cấp địa chỉ IP chính xác cho tên miền đó. DNS Resolver sau đó sẽ lưu trữ thông tin này trong bộ nhớ cache của nó và gửi lại cho trình duyệt.
10. Trình duyệt sẽ sử dụng địa chỉ IP nhận được để kết nối với server và tải trang web yêu cầu.
### DNS Zone là gì?
DNS Zone là một phần của không gian tên miền mà các cơ quan quản lý hoặc các máy chủ DNS cụ thể có thẩm quyền kiểm soát và quản lý. Một DNS Zone có thể chứa một hoặc nhiều tên miền và các record, bao gồm cả bản ghi các tài nguyên (Resource Records) như địa chỉ IP, bản ghi MX (mail exchange), bản ghi CNAME (canonical name) và nhiều loại bản ghi khác.
### Nameserver
Là máy chủ có vai trò tiếp nhận các yêu cầu về tên miền và phản hồi bằng địa chỉ thích hợp. Vd: ns1.vietnix.net; ns2.vietnix.net;... 
#### Record
CPanel có 4 loại record chính:  A, MX, NS, CNAME. 
##### A Record
Là một loại bản ghi trong hệ thống DNS được sử dụng để ánh xạ tên miền tới một địa chỉ IP cụ thể.
```
cpanel.com. IN A 208.74.123.68
ftp         IN A 208.74.123.58
```
Lưu ý: Dấu "." ở cuối "cpanel.com." không phải là lỗi đánh máy. Đối với ftp nó có nghĩa là bản ghi ftp IN A 208.74.123.58 sẽ tương đương với bản ghi fpt.cpanel.com IN A  208.74.123.58. 
##### CNAME Record
Là một loại bản ghi trong hệ thống DNS được sử dụng để ánh xạ domain này tới một domain khác. Như khi ai đó truy cập vào "www.cpanel.com", hệ thống DNS sẽ chuyển hướng tới "cpanel.com", và sau đó lấy địa chỉ IP từ A Record của "cpanel.com" để kết nối tới server.
```
www IN CNAME cpanel.com
```
Lưu ý: Bản ghi www vẫn có khả năng trỏ đến một địa chỉ IP khác với tên miền gốc, dẫn bạn đến một máy chủ và/hoặc trang web hoàn toàn khác, tuy nhiên thực tế đã ít sử dụng. 
##### MX Record
Là một loại bản ghi DNS được sử dụng để xác định email server nào chịu trách nhiệm nhận email cho một domain cụ thể.
```
cpanel.com. IN MX 0 mx1.cpanel.com
mx1.cpanel.com. IN A 208.74.121.68
```
Lưu ý:  Số 0 trong record được gọi là mức độ ưu tiên (prority) của MX record đó. Điều này có nghĩa là có thể có nhiều bản ghi MX cho một tên miền -> tạo ra một hệ thống dự phòng dựa trên DNS cho các mail server. 
##### NS Record
Là một loại bản ghi DNS được sử dụng để xác định máy chủ tên nào chịu trách nhiệm cho một vùng DNS cụ thể. NS Record chỉ ra các nameserver có thẩm quyền và giúp định hướng các truy vấn DNS tới đúng nameserver để trả lời. Cấu trúc của một NS Record bao gồm hai thành phần chính: Tên miền hoặc tên phụ mà bản ghi NS này áp dụng (ví dụ: "example.com"), tên máy chủ tên có thẩm quyền cho tên miền đó (ví dụ: "ns1.example.com"). 
## Web
### Domain
Một domain bao gồm 3 phần chính: Subdomain, Domain Name (tên miền), và Top-Level Domain (miền cấp cao).
![Screenshot 2025-01-10 at 10-56-17 Domain - Domain pdf](https://github.com/user-attachments/assets/a2e6f005-0c19-4b5b-8071-d73b60401b06)

Trong đó:
* Protocol: Protocol là một tập hợp các quy tắc chuẩn cho phép hai hoặc nhiều thực thể trong cùng một hệ thống để trao đổi thông tin liên lạc, dữ liệu qua các kênh truyền thông.
* Subdomain: Subdomain là một phần tùy chọn và nằm phía trước tên miền chính. Nó giúp chia nhỏ và tổ chức trang web hoặc ứng dụng của bạn thành các phần khác nhau.
* Domain Name (Tên miền): Đây là phần chính của tên miền và thường là từ hoặc cụm từ mô tả nội dung hoặc thương hiệu của trang web.
* Second Level Domain: Một thành phần quan trọng của tên miền giúp phân biệt tên miền của bạn với các tên miền khác, giúp người dùng hiểu rõ hơn về nội dung hoặc lĩnh vực hoạt động của trang web.
* Top-Level Domain (TLD - Miền cấp cao): Miền cấp cao là phần cuối cùng của tên miền và thường là các phần mở rộng như .com, .net, .org, .edu, .vn và nhiều loại khác. Miền cấp cao giúp xác định loại hình trang web hoặc địa chỉ trực tuyến mà tên miền đề cập đến.
* Page - Path: Đường dẫn trang cho biết cách di chuyển trong cấu trúc trang web. Mỗi phần của đường dẫn trang thường thể hiện một thư mục hoặc một trang cụ thể trên trang web.
#### Phân biệt addon domain, subdomain, alias domain, parked domain
| Loại Domain      | Định nghĩa                                          | Ví dụ                              | Mục đích sử dụng                      |
|------------------|-----------------------------------------------------|------------------------------------|---------------------------------------|
| **Subdomain**    | Một phần mở rộng của tên miền chính                 | `blog.yourdomain.com`              | Phân chia các phần khác nhau của website chính  |
| **Addon Domain** | Tên miền mới thêm vào tài khoản hosting            | `newdomain.com`                    | Quản lý nhiều website trên một tài khoản hosting |
| **Alias Domain** | Tên miền thay thế cho tên miền chính               | `yourdomain.net` trỏ về `yourdomain.com` | Sử dụng nhiều tên miền để trỏ về cùng một trang web |
| **Parked Domain**| Tên miền được đăng ký nhưng không có nội dung      | `parkeddomain.com`                 | Giữ chỗ cho tên miền trong tương lai hoặc hiển thị quảng cáo |
#### Các cấp domain
* Cấp 1: .com,.org, .net, …
* Cấp 2: tên miền quốc gia: .vn, .us, .cn, …
* Cấp 3: là sự kết hợp giữa tên miền cấp 1 và cấp 2: .com.vn, .edu.vn, ...
### Protocol
#### IP (Internet protocol) 
* Là giao thức để các máy tính tìm thấy nhau trên mạng.
* IP Address là số được gán cho máy tính để máy tính khác có thể tìm thấy nó. Có 2 loại là IPv4 và IPv6.
* Để các IP ko bị trùng thì IANA đã được sinh ra để quản lí chúng.
#### HTTP (Hypertext Transfer Protocol) 
Là một giao thức truyền tải siêu văn bản được sử dụng để truyền tải trên World Wide Web. HTTP là nền tảng của việc trao đổi thông tin giữa các trình duyệt web và web server. 
#### HTTPS (Hypertext Transfer Protocol Secure) 
Là phiên bản bảo mật của HTTP. HTTPS sử dụng SSL/TLS để bảo vệ dữ liệu truyền tải giữa trình duyệt web và web server. 
#### SSL
Là một giao thức cho phép thiết lập kết nối được mã hóa an toàn giữa máy chủ và trình duyệt web của máy khách.
##### SSL gồm những gì?
Khi khởi tạo SSL, cần tạo CSR và private key. Sau khi CA chứng nhận xác thực, sẽ nhận được SSL certificate và certificate chain. Bộ SSL hoàn chỉnh sẽ bao gồm SSL certificate, public key, private key và certificate chain. 
## File System
### Permission
![markdown](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRLjKiogu44Ovo3J1USgpx0-XpM4-5oHtbgWg&s)
### File System
![markdown](https://cdn.hashnode.com/res/hashnode/image/upload/v1609555594482/fJlVaulJb.png?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp)
## Email
### Email Travel 
Có 6 bước email được gửi và nhận:  Soạn và gửi email trên ứng dụng -> Máy chủ SMTP gửi email  -> Máy chủ DNS tra cứu  -> Truyền tải qua Internet  ->Máy chủ SMTP nhận email  -> Người nhận nhận email thông qua imap/pop3. 
### Email header
Thông tin văn bản chứa dữ liệu bổ sung về email và người gửi được thêm vào mỗi email được gửi. 
### Email encryption
Được sử dụng để đảm bảo rằng chỉ những người được ủy quyền (authorize) mới có thể đọc dữ liệu của nó. 
### HELO
Lệnh văn bản được đưa ra giữa các máy chủ thư khi email được gửi là HELO. 
### Giao thức trong email
* SMTP: Gửi email đi. 
* IMAP: nhận mail bằng cách truy cập và quản lý email trực tiếp trên máy chủ, đồng bộ hóa giữa các thiết bị. 
* POP3: nhận mail bằng cách tải về email từ máy chủ về thiết bị cá nhân. 
## Database
Là thuật ngữ được định nghĩa là một tập hợp dữ liệu có cấu trúc. 
### Table
Core structure of a relational database. 
### Engine
*Là term được sử dụng để xác định thành phần xử lý logic trên bảng. 
*Có 2 engines cho MySQL/MariaDB thường được sử dụng trên máy chủ cPanel & WHM là InnoDB(default) và MyISAM. 
### Index
Thuật ngữ được sử dụng để xác định cấu trúc dữ liệu cho phép việc tra cứu được thực hiện nhanh chóng (quick lookup) ngay cả trên cơ sở dữ liệu lớn. 
### Grant
MySQL gồm các quyền được cấp cho database, host, user. 


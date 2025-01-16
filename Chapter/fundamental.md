# Fundamental
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
#### Domain Status
##### Trạng thái tên miền tại Đơn vị Cấp phát tên miền (Registry)
| Trạng thái         | Ý nghĩa                                                                                                                                  | Bạn nên làm gì khi tên miền ở trạng thái này?                                                                                                                                                     |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **OK / active**     | Trạng thái thể hiện tên miền hoạt động bình thường sau khi đăng ký.                                                                      | Yêu cầu nhà đăng ký của bạn thực hiện các trạng thái hạn chế như clientTransferProhibited cấm chuyển đổi NĐK, clientDeleteProhibited cấm xóa và clientUpdateProhibited cấm cập nhật để giúp ngăn chặn chuyển đổi (transfer), xóa hoặc cập nhật trái phép vào tên miền của bạn. |
| **addPeriod**       | Đây là trạng thái sau khi tên miền mới vừa được đăng ký.                                                                                | Đây là trạng thái được đặt trong vài ngày đầu sau khi tên miền của bạn được đăng ký. Không có vấn đề gì với tên miền của bạn.                                                                      |
| **autoRenewPeriod** | Thời gian đăng ký tự động gia hạn tên miền. Trạng thái này cho phép nhà đăng ký hủy việc gia hạn (duy trì) nhưng phải trả một khoản phí cho nhà cung cấp.                     | Đây là trạng thái được đặt trong một khoảng thời gian giới hạn sau khi đăng ký tự động gia hạn tên miền của bạn. Nếu bạn không muốn giữ nó (tức là trả phí gia hạn) nữa, bạn nên liên hệ với NĐK ngay lập tức để thương thảo theo chính sách riêng của họ.                  |
| **inactive**        | Tên miền đã được đăng ký nhưng Name Server chưa thể liên kết với tên miền của bạn.                                                      | Nếu tên miền của bạn vẫn ở trạng thái này trong vài ngày, bạn có thể liên hệ với nhà đăng ký để yêu cầu xử lý về sự chậm trễ trong quá trình đưa tên miền vào hoạt động.                               |
| **pendingCreate**   | Đang chờ Đăng ký                                                                                                                         | Yêu cầu tạo tên miền của bạn đã được nhận và đang được xử lý.                                                                                                                                      |
| **pendingDelete**   | Tên miền hết hạn đăng ký. Chuẩn bị xóa.                                                                                                  | Chờ tên miền trở về trạng thái tự do và đăng ký lại sau đó theo chính sách của cơ quan đăng ký.                                                                                                   |
| **pendingRenew**    | Đang chờ Gia hạn                                                                                                                          | Yêu cầu gia hạn tên miền của bạn đã được tiếp nhận và đang được xử lý.                                                                                                                             |
| **pendingRestore**  | Một tên miền đã hết hạn đang được chờ khôi phục (về trạng thái Active). Nếu trong thời gian này NĐK không thực hiện yêu cầu khôi phục nào, tên miền sẽ trở về trạng thái redemptionPeriod. | Theo dõi tên miền trong khoảng thời gian 07 (bảy) ngày để xác thực việc NĐK đã thực hiện yêu cầu khôi phục tên miền cho bạn. Nếu tên miền trở về trạng thái redemptionPeriod, hãy liên hệ ngay với NĐK để được giải quyết.           |
| **pendingTransfer** | Đang chờ Chuyển đổi nhà đăng ký.                                                                                                         | Nếu bạn không chuyển đổi tên miền của mình, bạn hãy liên hệ với nhà đăng ký ngay lập tức để yêu cầu họ từ chối yêu cầu chuyển tên miền và đưa về trạng thái clientTransferProhibited.             |
| **pendingUpdate**   | Đang chờ Cập nhật                                                                                                                         | Nếu bạn không yêu cầu cập nhật bất cứ thông tin gì liên quan đến tên miền của mình, bạn hãy liên hệ với nhà đăng ký ngay lập tức để được xử lý.                                                   |
| **redemptionPeriod**| Tên miền đã hết hạn và rơi vào trạng thái cần đóng phí chuộc nếu muốn tiếp tục sử dụng. Thời gian này thường sẽ kéo dài 30 ngày.                                               | Nếu bạn muốn giữ tên miền của mình, bạn phải liên hệ với nhà đăng ký của mình để giải quyết trước khi tên miền của bạn bị xóa. Bạn sẽ phải đóng một khoản phí chuộc tên miền (gia hạn trễ) để nhà đăng ký khôi phục tên miền cho bạn.       |
| **renewPeriod**     | Tên miền được gia hạn                                                                                                                     | Đây là trạng thái được đặt trong một khoảng thời gian giới hạn cho việc xác nhận gia hạn tên miền của bạn với nhà đăng ký.                                                                         |
| **serverDeleteProhibited** | Trạng thái ngăn tên miền bị xóa.                                                                                                  | Đây là một trạng thái không phổ biến, thường được ban hành trong các trường hợp tranh chấp pháp lý, theo yêu cầu của bạn (khi đăng ký Registry Lock) hoặc khi có trạng thái redemptionPeriod. Để gỡ bỏ trạng thái này, bạn phải liên hệ với NĐK tên miền để được hỗ trợ.  |
| **serverHold**      | Tên miền không được kích hoạt trong DNS                                                                                                  | Bạn phải liên hệ với nhà đăng ký của mình để kiểm tra thông tin.                                                                                                                               |
| **serverRenewProhibited** | Trạng thái không thể được gia hạn. Nó là trạng thái không thông dụng vì nó có hiệu lực trong quá trình tranh chấp pháp lý.                                      | Bạn phải liên hệ với Nhà đăng ký của mình và yêu cầu họ làm việc với Đơn vị cấp phát để xóa mã trạng thái này. Quá trình này có thể mất nhiều thời gian hơn so với clientRenewProhibited vì nhà đăng ký của bạn phải chuyển tiếp yêu cầu của bạn đến cơ quan đăng ký tên miền và chờ họ gỡ bỏ trạng thái.            |
| **serverTransferProhibited** | Trạng thái không cho phép transfer tên miền.                                                                                    | Đây là một trạng thái không phổ biến, thường được ban hành trong các trường hợp tranh chấp pháp lý, theo yêu cầu của bạn (khi đăng ký Registry Lock). Để gỡ bỏ trạng thái này, bạn phải liên hệ với NĐK tên miền để được hỗ trợ.                |
| **serverUpdateProhibited** | Trạng thái không cho phép cập nhật tên miền                                                                                       | Đây là một trạng thái không phổ biến, thường được ban hành trong các trường hợp tranh chấp pháp lý, theo yêu cầu của bạn (khi đăng ký Registry Lock). Để gỡ bỏ trạng thái này, bạn phải liên hệ với NĐK tên miền để được hỗ trợ.                |
| **transferPeriod**  | Trạng thái cho phép sau khi tranfer tên miền thành thông thì nhà đăng ký mới có thể yêu cầu nhà cung cấp xóa tên miền                                                          | Đây là trạng thái được đặt trong một khoảng thời gian giới hạn sau khi chuyển tên miền của bạn sang nhà đăng ký mới. Nếu bạn không yêu cầu chuyển tên miền của mình, bạn nên liên hệ với Nhà đăng ký ban đầu để kiểm tra, tránh việc mất tên miền.  |
##### Trạng thái tên miền tại Đơn vị Quản lý (Nhà đăng ký) tên miền (Registrar)
| Trạng thái                  | Ý nghĩa                                                                            | Bạn nên làm gì khi tên miền ở trạng thái này?                                                                                                                                 |
|-----------------------------|------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **clientDeleteProhibited**  | Trạng thái không cho phép xóa tên miền (Cấm hủy domain)                             | Trạng thái này cho biết rằng không thể xóa tên miền, điều này có thể ngăn chặn việc xóa trái phép do chiếm quyền điều khiển và / hoặc gian lận.                                   |
| **clientHold**              | Trạng thái suspend tên miền (Tạm ngừng tên miền)                                    | DNS tên miền của bạn không hoạt động. Đối với TMVN, có thể bạn chưa hoàn thành hồ sơ đăng ký nên bị khóa ở cấp NĐK. Hãy liên hệ với NĐK để được hỗ trợ gỡ bỏ trạng thái này.       |
| **clientRenewProhibited**   | Trạng thái không cho phép gia hạn tên miền. (Cấm Gia hạn tên miền)                  | Đây là trạng thái không phổ biến, thường được ban hành trong các tranh chấp pháp lý. Nếu vậy, bạn nên liên hệ với Nhà đăng ký của bạn để giải quyết vấn đề hoặc bạn chỉ muốn gia hạn nó hãy yêu cầu đăng ký của mình xóa bỏ trạng thái này.            |
| **clientTransferProhibited**| Trạng thái không cho phép transfer tên miền (Cấm chuyển đổi nhà đăng ký).           | Trạng thái này cho biết rằng không thể chuyển đổi nhà đăng ký tên miền, điều này sẽ giúp ngăn chặn việc chuyển đổi trái phép do chiếm quyền điều khiển và / hoặc lừa đảo. Nếu bạn muốn chuyển đổi tên miền của mình, bạn phải liên hệ với Nhà đăng ký và yêu cầu họ xóa bỏ trạng thái này.          |
| **clientUpdateProhibited**  | Trạng thái không cho phép cập nhật thông tin tên miền (Cấm cập nhật thông tin)      | Trạng thái tên miền này cho biết rằng không thể cập nhật tên miền, điều này có thể giúp ngăn chặn các cập nhật trái phép do gian lận. Nếu bạn muốn cập nhật tên miền của mình, bạn phải liên hệ với Nhà đăng ký và yêu cầu họ xóa bỏ trạng thái này.    |

### Web server
#### Virtual host
Virtual Hosts là một tính năng trong web server (Apache, NginX,...) cho phép nhiều trang web hoặc tên miền hoạt động trên cùng một máy chủ vật lý hoặc một địa chỉ IP duy nhất. Đây là giải pháp hữu ích giúp tối ưu hóa tài nguyên máy chủ, giảm chi phí vận hành và đơn giản hóa việc quản lý hosting cho nhiều website.
![image](https://github.com/user-attachments/assets/0e6ac3dd-b371-43c9-9741-c8b17ea744fa)
##### Xác định các thông tin của Virtual Host
Mỗi Virtual Host sẽ chứa các thông tin như:
* Tên miền: Để nhận diện và định tuyến đúng yêu cầu.
* Thư mục gốc: Nơi lưu trữ tệp của trang web.
* Địa chỉ IP (nếu cần): Áp dụng trong trường hợp sử dụng IP-Based Virtual Hosts.
#### Phân biệt các loại Virtual Hosts
* Name-Based Virtual Host: Cho phép nhiều tên miền sử dụng chung một địa chỉ IP.
* IP-Based Virtual Host: Gán mỗi tên miền một địa chỉ IP riêng biệt.
* Port-Based Virtual Host: Sử dụng số cổng (Port) để phân biệt các website trên cùng một địa chỉ IP.

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
* Là term được sử dụng để xác định thành phần xử lý logic trên bảng. 
* Có 2 engines cho MySQL/MariaDB thường được sử dụng trên máy chủ cPanel & WHM là InnoDB(default) và MyISAM. 
### Index
Thuật ngữ được sử dụng để xác định cấu trúc dữ liệu cho phép việc tra cứu được thực hiện nhanh chóng (quick lookup) ngay cả trên cơ sở dữ liệu lớn. 
### Grant
MySQL gồm các quyền được cấp cho database, host, user. 


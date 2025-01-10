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
#### Record
CPanel có 4 loại record chính:  A, MX, NS, CNAME. 
##### A Record
Là một loại bản ghi trong hệ thống DNS được sử dụng để ánh xạ tên miền tới một địa chỉ IP cụ thể.
'''
cpanel.com. IN A 208.74.123.68
ftp         IN A 208.74.123.58
'''

# EMail Doanh Nghiệp
cPanel servers sử dụng:
* Exim: Mail Transfer Agent (MTA).
* Dovecot: IMAP/POP3 daemon.
* Mailman: mailing lists.
* SpamAssassin: spam control.
# Giao thức
## SMTP (send)
Là giao thức dùng để gửi mail. Nó thiết lập kênh kết nối giữa mail client và mail server, email sẽ được đẩy từ mail client lên mail server và từ mail server nó sẽ được server này gửi đi đến mail server nhận.
## IMAP (receive)
là giao thức nhận mail được dùng để kéo emails về emails client, tuy nhiên khác biệt với POP3 là nó chỉ kéo email headers về, nội dung email vẫn còn trên server.
## POP3 (receive)
POP3 là một giao thức chuẩn dùng để truy cập và tải email từ máy chủ thư điện tử về máy tính cá nhân của bạn. Khi sử dụng POP3, email sẽ được tải xuống và lưu trữ trên thiết bị của bạn, và thường sẽ bị xóa khỏi máy chủ sau khi tải xong (tuy nhiên, tùy vào cài đặt, email có thể vẫn giữ lại trên máy chủ). 
## Protocol Port
![protocol port](https://images.articulate.com/f:jpg%7Cpng,a:retain,b:fff/rise/courses/rtdwELwWKP55ZIBfGnf-TTLkF_4QaeUy/_TJx14qbqq8sSqqh.png)
# DNS Record
## DKIM Record (send)
### DKIM Record là gì?
DKIM Record là một bản ghi giúp xác nhận Email thông qua chữ ký số giúp tránh email giả mạo.
DKIM cho phép người nhận kiểm tra xem email được xác nhận từ một tên miền cụ thể có thực sự được chủ sở hữu uy quyền hay không? Nó sẽ gắn chữ ký điện tử, được liên kết với tên miền vào mỗi email gửi đi. Hệ thống người nhận có thể xác minh điều này bằng cách tra cứu mã khóa công khai (Public-key cryptography) của người gửi được xuất bản trong DNS.
### Cách hoạt động
Ở bên gửi:
* Bước 1: Tạo ra cặp khóa private/public, phần mềm OpenSSL có hỗ trợ.
* Bước 2: Chuyển khóa Public lên khai báo bản ghi TXT trên DNS, ứng đúng với domain gửi email.
* Bước 3: Cấu hình Mail server sử dụng khóa Private để ký vào email trước khi gửi email (Lưu ý: Khóa này chỉ lưu trên Mail server nên không thể giả mạo).

Ở bên nhận:
* Bước 1: Nhận email từ bên gửi và kiểm tra email có thông điệp được mã hóa do cấu hình DKIM.
* Bước 2: Query DNS để lấy khóa Public của Domain bên gửi rồi giải mã, khi giải mã đúng thì xác nhận nguồn gửi và email đảm bảo, khi giải mã không thấy đúng thì phụ thuộc vào chính sách bên nhận để từ chối hoặc vẫn nhận email.
## SPF Record (send)
### SPF Record là gì?
SPF là record liệt kê tất cả các tên máy chủ / địa chỉ IP được ủy quyền được phép gửi email thay mặt cho miền của bạn.
### Cách tạo SPF record
Tạo SPF record của bạn bằng cách làm theo các bước sau:
1. Thu thập tất cả các địa chỉ IP được sử dụng để gửi email.
2. Tạo bản ghi SPF của bạn. Ví dụ: v = spf1 ip4: 34.243.61.237 ip6: 2a05: d018: e3: 8c00: bb71: dea8: 8b83: 851e
3. Xuất bản SPF record của bạn vào DNS của bạn
### Cơ chế của SPF record
| Cơ chế   | Mô tả và các giá trị được phép                                                                                                              |
|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| v        | Phiên bản SPF. Thẻ này là bắt buộc và phải là thẻ đầu tiên trong bản ghi. Cơ chế này phải là: `v=spf1`                                       |
| ip4      | Cấp quyền cho máy chủ thư theo địa chỉ IPv4 hoặc dải địa chỉ. Giá trị phải là địa chỉ IPv4 hoặc dải ô ở định dạng chuẩn, ví dụ: `ip4:192.168.0.1` hoặc `ip4:192.0.2.0/24` |
| ip6      | Cấp quyền cho máy chủ thư theo địa chỉ IPv6 hoặc dải địa chỉ. Giá trị phải là địa chỉ IPv6 hoặc dải ô ở định dạng chuẩn, ví dụ: `ip6:3FFE:0000:0000:0001:0200:F8FF:FE75:50DF` hoặc `ip6:2001:db8:1234::/48`  |
| a        | Cấp phép máy chủ thư theo tên miền, ví dụ: `a:solarmora.com`                                                                                 |
| mx       | Cho phép một hoặc nhiều máy chủ thư theo bản ghi MX miền, ví dụ: `mx:mail.solarmora.com` Nếu cơ chế này không có trong SPF record của bạn, giá trị mặc định là bản ghi MX của miền nơi SPF record được sử dụng. |
| include  | Cho phép người gửi email của bên thứ ba theo miền, ví dụ: `include:servers.mail.net`                                                         |
| all      | Chỉ định rằng tất cả các tin nhắn đến đều phù hợp. Chúng tôi khuyên bạn nên luôn đưa cơ chế này vào hồ sơ SPF của mình. Đây phải là cơ chế cuối cùng trong SPF record. Bất kỳ cơ chế nào xuất hiện sau `all` cơ chế trong SPF record đều bị bỏ qua.      |

## PTR Record (send)
### PTR Record là gì?
PTR Record, với PTR là viết tắt của “pointer” hay “con trỏ”, là một loại bản ghi DNS có tác dụng trỏ một địa chỉ IP đến một tên miền. Hiểu đơn giản, PTR record giống như một phiên bản ngược của A record: nếu A record trỏ tên miền vào một địa chỉ IP thì PTR Record trỏ một địa chỉ vào một hostname. Tuy nhiên cả 2 bản ghi này làm việc hoàn toàn độc lập với nhau.

Kiểm tra PTR Record bằng cách Sử dụng tool online: http://mxtoolbox.com/SuperTool.aspx?action=mx%3a&run=toolpage
## MX Record (receive)
### MX record là gì?
MX Record là viết tắt của Mail Exchanger Record được định nghĩa là một bản ghi trong DNS zone dùng để định vị Mail Server cho một Domain. Một tên miền có thể được gán bởi nhiều bản ghi MX.

Bản ghi MX phải được sử dụng cùng với bản ghi A. Bản ghi A sẽ trỏ đến (các) máy chủ thư.
### Các bước trỏ tên miền về email hosting
* Bước 1: Truy cập vào cPanel.
* Bước 2: Tìm và click chọn biểu tượng MX Entry.
* Bước 3: Trong danh sách tên miền xổ ra, bạn chọn domain muốn trỏ MX record.
* Bước 4: Click vào mục “Automatically Detect Configuration”, rồi nhấn nút Change.
* Bước 5: Trong phần “Add New Record”, bạn nhập mail.thedomainname.com (hoặc thông tin mà máy chủ cung cấp cho bạn) cho giá trị Đích. Phần lựa chọn Ưu tiên (Priority) thông thường để giá trị bằng 0.
* Bước 6: Click chọn nút “Add New Record” để hoàn tất.
Lưu ý: Nếu muốn đặt lại giá trị thì rất đơn giản. Bạn chỉ việc lưu giá trị Đích làm tên miền (chú ý là tên miền không chứa http hoặc www).
Tham khảo cách dùng với portal Vietnix: https://huongdan.vietnix.vn/huong-dan-tro-ten-mien-ve-email-hosting/
# Dovecot
Dovecot là mail server IMAP/POP3 được sử dụng trong cPanel & WHM. MUA bao gồm Microsoft Outlook, Mozilla Thunderbird, và Apple Mail.
## Primary Storage Option 
Có 2 tùy chọn lưu trữ chính của thư trong *NIX: mdbox và Maildir:
## Authentication Daemons
* Authenticaion Daemons là những chương trình đăng nhập người dùng và thực hiện công việc để đảm bảo sử dụng đúng mật khẩu.
* Trên Panel, có thể điều chỉnh Authentication Daemons trong giao diện *WHM » Service Configuration » Mailserver Configuration.* 
## Dọn rác
Dovecot không dọn rác theo mặc định -> để bật Tự động dọn sạch thùng rác: *WHM » Service Configuration » Mailserver Configuration.*
## Chuyển đổi giữa Maildir/Mdbox
Để chuyển đổi giữa 2 định dạng có sẵn (mdbox/maildir): *WHM » Email » Mailbox Conversion*.
## Time move backward 
Sử dụng giao diện *WHM >> Server Configuration >> Server Time*, sau đó nhấn *Sync Time with Time Server*. 
## System Mail Reference 
Có 3 tài khoản hệ thống không nhận được thư nhưng có thể được sử dụng để nhận thông báo và cảnh báo hệ thống: root, cpanel, nobody - > để thiết lập: Home » Server Contacts » Edit System Mail Preferences. 
# Exim
Exim là một phần mềm MTA (Mail Transfer Agent) được sử dụng để chuyển giao email trên các hệ thống UNIX. Mỗi tin nhắn do Exim xử lý đều được cấp một id tin nhắn dài 16 ký tự. Nó được chia thành ba phần, cách nhau bằng dấu gạch nối. ví dụ: 16VDhn-0001bo-D3.
## Config exim
Cấu hình tại */etc/exim.conf* hoặc thông qua Exim Configuration Manager.
## Các câu lệnh dùng trên exim
$ exiwhat: Lệnh này hiển thị các kết nối đang hoạt động đang được xử lý.

$ ps -C exim wwwu: xem những tiến trình exim đang chạy.

$ lsof -c exim: Lệnh này hiển thị danh sách các file đang được Exim truy cập.

$ openssl s_client -connect IP:port : test IMAP với OpenSSL

$ Zcat: view zipped files without unzipping them. 

$ Exigrep: read Exim logs. 

$ exim -bpc để xem số mail trong queue. 

$ exim-bp: xem toàn bộ hàng đợi thư với nhiều chi tiết hơn. 

$ cwd: xem đường dẫn kích hoạt việc gửi tin nhắn. 

$ exiqgrep -f [user]@domain.tld : xem message theo người gửi.

$ exiqgrep -r [user]@domain.tld : xem message theo người nhận.

$ exiqgrep -o 172800 (older); exiqgrep -y 1800 (younger) : xem message theo thời gian (older/younger).

$ exim -Mvh <exim-id> : xem msg theo header. 

$ exim -Mvb <exim-id> : xem msg theo body.

$ exiqgrep -r user@domain.tld -i | xargs exim -M : Resending a Message.

$ exim -Mrm <exim-id>: Deleting a Message.

$ exim -bt <email address> : check routing info.
## Mail Storage Formats
### Maildir
* MailDir lưu trữ từng email trong file riêng. 
* Mỗi thư mục trong client có một thư mục tương ứng trên server. 
* Các thư mục có 2 chuẩn new (no-read) và cur (read). 
* Các thư mục được gán tên theo chức năng như: .sent (thư Đã gửi), .Draft (thư Nháp), .Trash (đã xóa). 
* Bên trong domain directory, mỗi acc email sẽ có 1 folder. Ví dụ: trong ảnh trên, các địa chỉ email kia@cars.test và vw@cars.test tồn tại, vì vậy chúng ta thấy các thư mục Kia và vw.
* Message của mỗi domain được lưu trong một folder được đặt theo tên domain, vd: cars.test/
* Thư mục subcription được webmail sử dụng và được kiểm soát bởi webmail client.
* Các file dovecot.* được dovecot sử dụng để theo dõi thư.
* File maildirsize được dovecot sử dụng để theo dõi kích thước hộp thư.
### Mdbox
* mdbox lưu trữ nhiều mail trong một file.
* Các file dovecot, maildirsize và subscription của mdbox giống maildir.
* Từng folder trong mailboxes là user mailbox.
* Thư được lưu trữ trong tệp có tên “m.1”. 
# Log file chứa ở đâu?
![logfile path](https://images.articulate.com/f:jpg%7Cpng,a:retain,b:fff/rise/courses/rtdwELwWKP55ZIBfGnf-TTLkF_4QaeUy/3T1uw8p0pDtilh5d.png)

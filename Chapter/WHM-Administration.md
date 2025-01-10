# Mail Server
cPanel servers sử dụng:
* Exim: their Mail Transfer Agent (MTA).
* Dovecot: IMAP/POP3 daemon.
* Mailman: mailing lists.
* SpamAssassin: spam control.
## Giao thức
### SMTP (send)
Là giao thức dùng để gửi mail. Nó thiết lập kênh kết nối giữa mail client và mail server, email sẽ được đẩy từ mail client lên mail server và từ mail server nó sẽ được server này gửi đi đến mail server nhận.
### IMAP (receive)
là giao thức nhận mail được dùng để kéo emails về emails client, tuy nhiên khác biệt với POP3 là nó chỉ kéo email headers về, nội dung email vẫn còn trên server.
### POP3 (receive)
POP3 là một giao thức chuẩn dùng để truy cập và tải email từ máy chủ thư điện tử về máy tính cá nhân của bạn. Khi sử dụng POP3, email sẽ được tải xuống và lưu trữ trên thiết bị của bạn, và thường sẽ bị xóa khỏi máy chủ sau khi tải xong (tuy nhiên, tùy vào cài đặt, email có thể vẫn giữ lại trên máy chủ). 
#### Protocol Port
![protocol port](https://exams.cpanel.net/getfile/TK_w0BHMRvieYBThQhuts-lAA.M012Yk14RmlyaENIaG55VVQxWGdXNUc1MFFETHNHMHF2eEZBd1pxdit0TjBQMzc4S3d4RVBRSTVoOXNHdllhdg/cpanel/1670441040_introduction-mail-server-overview-cmi5-_rcfho4w/scormcontent/assets/YzJk4s5rJOk16bTq__TJx14qbqq8sSqqh.png)
## Dovecot
Dovecot là mail server IMAP/POP3 được sử dụng trong cPanel & WHM. MUA bao gồm Microsoft Outlook, Mozilla Thunderbird, và Apple Mail.
### Primary Storage Option 
Có 2 tùy chọn lưu trữ chính của thư trong *NIX: mdbox và Maildir:
### Authentication Daemons
* Authenticaion Daemons là những chương trình đăng nhập người dùng và thực hiện công việc để đảm bảo sử dụng đúng mật khẩu.
* Trên Panel, có thể điều chỉnh Authentication Daemons trong giao diện *WHM » Service Configuration » Mailserver Configuration.* 
### Dọn rác
Dovecot không dọn rác theo mặc định -> để bật Tự động dọn sạch thùng rác: *WHM » Service Configuration » Mailserver Configuration.*
### Chuyển đổi giữa Maildir/Mdbox
Để chuyển đổi giữa 2 định dạng có sẵn (mdbox/maildir): *WHM » Email » Mailbox Conversion*.
### Time move backward 
Sử dụng giao diện *WHM >> Server Configuration >> Server Time*, sau đó nhấn *Sync Time with Time Server*. 
### System Mail Reference 
Có 3 tài khoản hệ thống không nhận được thư nhưng có thể được sử dụng để nhận thông báo và cảnh báo hệ thống: root, cpanel, nobody - > để thiết lập: Home » Server Contacts » Edit System Mail Preferences. 
## Exim
Exim là một phần mềm MTA (Mail Transfer Agent) được sử dụng để chuyển giao email trên các hệ thống UNIX. Mỗi tin nhắn do Exim xử lý đều được cấp một id tin nhắn dài 16 ký tự. Nó được chia thành ba phần, cách nhau bằng dấu gạch nối. ví dụ: 16VDhn-0001bo-D3.
### Config exim
Cấu hình tại */etc/exim.conf* hoặc thông qua Exim Configuration Manager.
### Các câu lệnh dùng trên exim
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
### Mail Storage Formats
#### Maildir
* MailDir lưu trữ từng email trong file riêng. 
* Mỗi thư mục trong client có một thư mục tương ứng trên server. 
* Các thư mục có 2 chuẩn new (no-read) và cur (read). 
* Các thư mục được gán tên theo chức năng như: .sent (thư Đã gửi), .Draft (thư Nháp), .Trash (đã xóa). 
* Bên trong domain directory, mỗi acc email sẽ có 1 folder. Ví dụ: trong ảnh trên, các địa chỉ email kia@cars.test và vw@cars.test tồn tại, vì vậy chúng ta thấy các thư mục Kia và vw.
* Message của mỗi domain được lưu trong một folder được đặt theo tên domain, vd: cars.test/
* Thư mục subcription được webmail sử dụng và được kiểm soát bởi webmail client.
* Các file dovecot.* được dovecot sử dụng để theo dõi thư.
* File maildirsize được dovecot sử dụng để theo dõi kích thước hộp thư.
#### Mdbox
* mdbox lưu trữ nhiều mail trong một file.
* Các file dovecot, maildirsize và subscription của mdbox giống maildir.
* Từng folder trong mailboxes là user mailbox.
* Thư được lưu trữ trong tệp có tên “m.1”. 
## Log file chứa ở đâu?
![logfile path](https://exams.cpanel.net/getfile/TK_w0BHMRvieYBThQhuts-lAA.M012Yk14RmlyaENIaG55VVQxWGdXNUc1MFFETHNHMHF2eEZBd1pxdit0TjBQMzc4S3d4RVBRSTVoOXNHdllhdg/cpanel/1670441040_introduction-mail-server-overview-cmi5-_rcfho4w/scormcontent/assets/3nm7-PNLjbW04bII_3T1uw8p0pDtilh5d.png)

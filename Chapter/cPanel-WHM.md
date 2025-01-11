# cPanel

## Giao diện
Sau khi đăng nhập vào hosting cPanel có 4 vùng cần nắm rõ như sau:
* Thanh tìm kiếm
* Thống kê
* Tính năng
## Chi tiết từng tính năng

### Email
Chức năng chính: Tạo email, xóa email, kiểm tra email, quản lý email, cấu hình email cho mail client.

#### Email Account
Giao diện khởi tạo Email Account

#### Forwarder
Dùng để forward Email đến 1 email khác. Ví dụ forward các email gửi đến test1@hosting.com (email trên hosting) → tech@vietnix.vn

#### Email Routing
Luôn luôn là Local Mail Exchanger. Chỉnh sang bất kì giá trị nào khác đều sẽ không gửi mail được.

#### Autoresponder
Cấu hình trả lời Email tự động.

#### Default Address
Nơi cấu hình Catch-all Email. Thay vì khi nhận Hosting nhận được một email đến 1 địa chỉ không tồn tại trên hosting thì nó sẽ trả về cho người gửi thông báo "No Such User Here", thì khi cấu hình Default Address Hosting sẽ gửi các email đó đến email default này.

#### Mail listing
Tạo một group tên "tech@vietnix.vn". Sau đó add nhiều email vào đây như tech1@vietnix.vn, tech2@vietnix.vn. Chức năng của Mailling List là khi có một email gửi tới tech@vietnix.vn thì sẽ được gửi đồng thời đến tất cả email trong group đó.

#### Track delivery
Theo dõi trạng thái của email gửi ra.

#### Global emial filter
Filter email với toàn bộ email account trên Hosting

#### Email Filter
Filter email với từng email account trên Hosting

#### Email Deliverable
Kiểm tra, lấy cấu hình DKIM, SPF, PTR đối với domain email trên Hosting

#### Address importer
Import danh sách email account lên Hosting. Bạn có thể tạo nhanh 1 list email trên hosting bằng cách tạo 1 file .csv có nội dung như sau và Import vào cPanel:

```
user1@example.com, Password, 10
user2@example.com, Password, 10
user3@example.com, Password, 10
```

#### Spam Filter
Cho phép cấu hình cài đặt lọc thư rác (được cung cấp bởi Apache SpamAssassin™) cho tài khoản email. Bộ lọc thư rác xác định và sắp xếp hoặc xóa email không mong muốn. Cấu hình cài đặt danh Whitelist, blacklist.
→ email hosting không sử dụng spam filters này.

#### BoxTrapper
- Xác thực người gửi: Khi ai đó gửi email đến địa chỉ email của bạn, BoxTrapper yêu cầu họ xác minh rằng họ là người thật bằng cách thực hiện một thao tác xác minh.
- Blacklist & Whitelist: Người dùng có thể xác định danh sách whitelist và blacklist cho phép hoặc chặn các người gửi cụ thể.
- Xử lý thư rác: BoxTrapper kiểm tra email đến và tự động loại bỏ thư rác hoặc chuyển nó vào thư mục rác tạm thời để bạn kiểm tra sau.
- Quản lý danh sách liên hệ: BoxTrapper có khả năng tự động cập nhật danh sách liên hệ dựa trên những người gửi đã được xác minh.
→ BoxTrapper không có trên email hosting

#### Email Disk Usage
Thống kê disk của từng email.

#### ASSP Antispam
* Spam Scoring: Điều chỉnh giá trị spam score, từ lowest → highest. Hoặc bật tắt tính năng này cho từng domain email.
* Bộ lọc trì hoãn: Khi nhận được 1 email thì email hosting sẽ lưu lại 3 thông tin là email address, domain, ip. Sau đó email hosting sẽ trả lại 1 thông báo cho người gửi mail với mã lỗi 451 error (spf soft failure). Khi sever của người gửi nhận được mã này thì nó sẽ retry lại email ban đầu 1 lần nữa. Lúc này email này sẽ bị whitelist. Việt làm này tương tự cơ chế Syn Proxy. Mặc định tính năng này bị tắt trên mail hosting.
* Bộ lọc địa chỉ không cục bộ: Chỉ cho phép nhận các email mà người nhận có tồn tại trên hosting (email account có tạo). Khi bật tính năng này thì tính năng catch all email của cpanel sẽ không sử dụng được.
* Bảo vệ virus: Quét email và filter các email có virus.

Ngoài ra các tính năng này đều có log, nên trace log trước khi điều chỉnh một tính năng.

### File

#### File Manager
Upload file, xóa, sửa file, nén, giải nén. Ngoài ra để hiển thị file ẩn (.htaccess, .env...).

#### Directory Privacy
Cài đặt user/pass cho các thư mục trên cPanel → Tương tự htpasswd

#### Disk Usage
Thống kê disk đang sử dụng

#### Web Disk
Quản lý dữ liệu trên web, tương tự như google drive, onedrive. Web disk hỗ trợ giao thức webdav để truyền tải.

#### FTP Account
Tạo tài khoản ftp account, hỗ trợ phân quyền tài khoản cho thư mục.

#### Backup & Backup wizard
Backup của cPanel → Không sử dụng

#### Git Version Control
Làm việc với github, tự động pull code khi có update code mới trên repo

#### JetBackup 5
Ba lựa chọn quan trọng:
- Sao lưu toàn bộ: Đây là các bản backup full, khi restore lại sẽ restore toàn bộ hosting, bao gồm database, source, ssl,...
- Thư mục Home: Đây là backup file, có thể lựa chọn riêng từng file để restore
- Cơ sở dữ liệu: Restore database

### Database

#### phpMyAdmin
Đăng nhập phpMyAdmin, tài khoản login là tài khoản MySQL

#### MySQL Database
- Tạo database
- Tạo User
- Add user vào database
- Grant quyền user

#### MySQL Database Wizard
Hỗ trợ tạo Database step-by-step. Giúp người tạo không bị quên các bước như tạo user, add user vào database, grant quyền.

#### Remote MySQL
Bật remote MySQL đối với database.

### Metric
* Visitors: Access-logs. Có thể dùng để xác định hosting đang bị đánh.
* Errors: Apache Error Logs.
* Bandwidth: Thống kê traffic từng ngày theo từng domain.
* Raw Access: Cho phép download access log dạng file text.
* Resource Usage:
  - SPEED: CPU Hosting
  - PMEM: Ram Hosting
  - IO: I/O Hosting
  - EP: Số lượng connect tối đa
  - NPROC: Số lượng Process tối đa
  - IOPS: I/O per second Hosting
### Domain
#### WP Toolkit
- Cài wordpress.
- Cài themes.
- Cài plugin.

#### Site Publisher
Tạo nhanh 1 website bằng template có sẵn của cPanel.

#### Domain
Thêm, xóa domain.

#### Redirector
Redirect domain.

#### Zone Editor
Sau khi trỏ NS về Hosting thì có thể điều chỉnh các record ở đây. NS của hosting có dạng, ví dụ host212.vietnix.vn:
```
ns1.host212.vietnix.vn
ns2.host212.vietnix.vn
```

#### Dynamic DNS
Sau khi tạo cPanel sẽ cấp cho mình 1 Url. Khi muốn cập nhật NS cho subdomain này thì chỉ cần curl đến URL này.

#### IP Management (chỉ có trên Hosting SEO)
Dùng để đổi IP cho các domain.

### Security

#### SSH Access
SSH lên hosting, có thể cho phép add ssh key.

#### IP Blocker
Block ip không cho truy cập vào website của bạn.

#### SSL/TLS
Quản lý SSL Server
- Khóa riêng tư (KEY): Tạo Private key.
- Yêu cầu ký chứng chỉ (CSR): Tạo CSR.
- Chứng chỉ (CRT): Thêm, xóa, sửa SSL của Domain.
- Cài đặt và Quản lý SSL cho trang web của bạn (HTTPS): Quản lý SSL của Domain.

#### SSL/TLS Status
Cài đặt AutoSSL.

#### Hotlink & Leech Protection
* Hotlink Protection: Giúp chặn các website khác chèn các directlink hình ảnh, file
download của mình trên website của họ.
* Leech Protection: Tính này liên quan đến phần Directory Privacy ở trên. Ví dụ sau khi
tạo user/pass được phép truy cập vào 1 folder nào đó trên hosting. Mà user đó bị lộ
pass và bị truy cập nhiều lần vào folder đó thì sẽ bị chặn và redirect đến 1 link khác
hoặc thông báo cho admin.

### Software

* Imunify360: Quét virus, quá trình quét virus là tự động.

* MultiPHP Manager: Có thể tùy chọn các phiên bản PHP khác nhau cho từng website.

* MultiPHP INI Editor: Bật tắt các biến môi trường php ở đây.

* Softaculous App Installer: Cài đặt app bằng 1 click. Ví dụ: Wordpress, Laravel, Moodle, NextCloud,...

* Setup Node.js App: Cài đặt nodeJS App.

### Advanced

* LiteSpeed Web Cache Manager: Nếu khách có dùng LSCache plugin thì mình có thể hỗ trợ khách flush cache từ giao diện cPanel.

* Terminal: Được dùng để chạy các lệnh terminal.

* Cron jobs: Các nhiệm vụ lặp đi lặp lại được tự động hóa vào thời gian đã lên lịch. Ví dụ: tạo hóa đơn vào 12:00 hàng ngày.

* Track DNS: Truy tìm tuyến đường từ PC đến máy chủ nhằm kiểm tra cài đặt DNS.

* Error Page: Giúp định cấu hình cách của các trang lỗi xuất hiện cho khách khi truy cập.

* Apache Handle: là các lựa chọn xử lý của Apache.

* MIME Types: Dùng để hướng dẫn để xử lý với các phần mở rộng tệp khác nhau, chẳng hạn như: .html, .htm.

# WHM

## Đổi Primary Domain

1. Modify an Account → Tìm kiếm User → Modify
2. Tại giao diện Modify → đổi Primary Domain → bấm Save

Có 2 trường hợp xảy ra:
- Save thành công
- WHM báo đã có domain này tồn tại trên hệ thống → Check domain này khách hàng có add trước đó là add-on domain hay không, nếu đã add thì báo khách chủ động remove ra.

## Migrate và Transfer

1. Từ server cần migrate đến, vào Transfer Tool → Điền IP của server cũ vào ô Remote Server Address.
2. Chọn Authentication Method là SSH Public Key và chọn key "transfer"
3. Scan Remote Server và tìm user cần transfer, thực hiện copy.

Sau khi transfer hosting ở bên cũ sẽ tự suspend.

## Terminal

### Reload Hosting
```bash
cagefs -m <user>
```

### Check domlogs
File log của domain nằm tại:
```bash
Domain không có SSL: /var/log/apache2/domlogs/<domain>
Domain có SSL: /var/log/apache2/domlogs/<domain>-ssl_log
```

### Check process đang chạy của một user
```bash
ps aux | grep <user>
```

## Kiểm tra hosting đang kết nối mail relay server bằng port nào?

Ctrl + F để tìm từ khóa POSTMAILCOUNT

## Tìm một add-on domain đang thuộc user nào?
### Dùng terminal
```bash
cat /etc/userdatadomains | grep "conheo.com"
abc.conheo.com:
```

### Dùng giao diện
```
khanhtest==root==sub==khanhtest.com==/home/khanhtest/abc.conheo.com==103.200.23.68:80==103.200.23.68:443====0==
conheo.com.khanhtest.com:
khanhtest==root==sub==khanhtest.com==/home/khanhtest/conheo.com==103.200.23.68:80==103.200.23.68:443====0==
conheo.com:
khanhtest==root==addon==conheo.com.khanhtest.com==/home/khanhtest/conheo.com==103.200.23.68:80==103.200.23.68:443====0==
```

## PHP X-Ray

PHP x-ray dùng để trace cụ thể thời gian thực thi các function php, giúp phát hiện các func nào gây chậm website khách hàng.

1. Vào plugin Cloudlinux Manager → X-ray → Start Tracing
2. URL: điền URL cần tracing, url này là trang chủ hoặc url khách báo vào bị chậm
3. Client's IP: Điền IP máy của tech vào, hoặc để * thì mọi ip request đến url này đều được trace
4. Record for: Có thể chọn Time Period để trace trong 1 khoảng thời gian hoặc Request để trace dựa theo số lần request.
5. Sau khi thiết lập các thông số xong, tech tiến hành request vào đường link trên 1 vài lần để x-ray phân tích

# Triển khai và cấu hình VPS
1. Truy cập vào đường dẫn portal.vietnix.com, tạo tài khoản mới.
2. Đăng ký và tạo VPS với hệ điều hành/cấu hình mong muốn và thanh toán. ![image](https://github.com/user-attachments/assets/d671a438-0df0-4e8e-8248-4eabde78da7d) 
![image](https://github.com/user-attachments/assets/1ddf5bf5-d36b-4b32-8dc1-77bf0dba825e)
3. Sau khi đăng ký thành công, sẽ hiển thị VPS bạn vừa đăng ký trong mục My Service, để ý ở mục IP Address chính là IP dùng để kết nối vào bằng terminal. ![image](https://github.com/user-attachments/assets/afa7867b-e5fc-4e5a-9538-d14eb80a27d2)

4. Mở terminal, kết nối VPS bằng lệnh:
```
$ ssh root@<IP>
```
4. Màn hình hiển thị "Welcome..." là login vô VPS thành công.
  ![image](https://github.com/user-attachments/assets/eb1382b9-3eb4-4ba5-823f-e0a29bbab622)
5. Cài đặt cPanel lên server bằng cách mở terminal và nhập lệnh
```
cd /home && curl -o latest -L https://securedownloads.cpanel.net/latest && sh latest
```
6. Đăng nhập vào hệ thống bằng url được cung cấp sau quá trình cài đặt.
7. Tiếp theo, đăng nhập vào cPanel Customer Portal để cấp quyền truy cập máy chủ. Nếu không có tài khoản ID cPanel thì tạo một cái. 
   ![image](https://github.com/user-attachments/assets/e0322bfb-4532-441d-bb05-17e42d82faf6)
8. Khi đã xác nhận email và xác minh tài khoản của mình, bạn sẽ sẵn sàng để kích hoạt bản dùng thử của bạn và tiến hành thiết lập máy chủ.
9. Bây giờ WHM đã được cài đặt, có thể bắt đầu tạo và quản lý tài khoản cPanel trên máy chủ của mình.
10. Nếu muốn triển khai web lên cPanel, cần trỏ domain về IP của VPS bằng record A.
    ![image](https://github.com/user-attachments/assets/3c35cd6c-c412-41c0-a3d3-e54162ac985c)

# WordPress
## Setup website WordPress
1. Từ giao diện cPanel » Home » Domains » WordPress Management. Click vào nút Install WordPress
   ![image](https://github.com/user-attachments/assets/11bcb324-a83f-4145-8557-243ccf0c9869)
2. Nhập các trường thông tin phù hợp và bấm Install.
   ![image](https://github.com/user-attachments/assets/41fbc07b-2401-42fe-a62d-5e127cd1c07d)
## Cài đặt plugin liên quan, kích hoạt license
1. Từ giao diện cPanel » Home » Domains » WordPress Management.
2. Vô tab Plugin, chọn Install.
   ![image](https://github.com/user-attachments/assets/5bfcc48a-d65c-4a69-a204-98fdbd338e30)
3. Tìm những plugin mà khách hàng yêu cầu, bấm Install (Nếu trường hợp đã mua license thì nhập key vào).
   ![image](https://github.com/user-attachments/assets/2d76cf51-bc19-4f4c-bfe2-53c920d93fb8)
4. Nếu plugin chưa được active thì active nó lên.
![image](https://github.com/user-attachments/assets/a58b5e4a-8639-4726-be69-269d58be6013)
5. Ấn login để truy cập quản trị website.
   ![image](https://github.com/user-attachments/assets/d47b1057-7d24-49a2-b93f-e873913ae332)
6. Website đã được cài đặt thành công, ấn vào đây để xem thử website.
   ![image](https://github.com/user-attachments/assets/ba59132e-c09e-465b-b507-b257391a3c9f)
 
# Chuyển dữ liệu website
1. **Trên host source:** Cài plugin All-in-one WP Migration. ![image](https://github.com/user-attachments/assets/3c9fc500-d99f-4b66-b4f5-44be2aaca19e)
2. **Trên host source:** Sau khi cài xong thì Active nó lên. ![image](https://github.com/user-attachments/assets/0d07623a-1d2b-40c3-9860-ec7694944b72)
3. **Trên host source:** Sau khi Active thành công thì chọn Export Site To > File và tải về máy File vừa export được. ![image](https://github.com/user-attachments/assets/74169c1a-95b8-4aeb-909a-0ef6a7512d14)

4. **Trên host đích:** Cài plugin All-in-one WP Migration. ![image](https://github.com/user-attachments/assets/3c9fc500-d99f-4b66-b4f5-44be2aaca19e)
5. **Trên host đích:** Sau khi cài xong thì Active nó lên. ![image](https://github.com/user-attachments/assets/0d07623a-1d2b-40c3-9860-ec7694944b72)
6. **Trên host đích:** Sau khi Active thành công thì chọn Import From > File và upload File vừa export ra được từ server source. ![image](https://github.com/user-attachments/assets/d3c441e3-6617-49da-8bcb-0676cdc456b4)

# Setup Mail Server thủ công mà không sử dụng terminal

Thiết lập mail server với **Exim** làm MTA (Mail Transfer Agent), **Dovecot** để xử lý POP/IMAP, và **Roundcube** là giao diện webmail.

## Bước 1: Cập Nhật Hệ Thống
Cập nhật và nâng cấp hệ thống để đảm bảo tất cả các gói phần mềm đều mới nhất:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Bước 2: Cài Đặt Exim
Exim sẽ xử lý việc gửi và nhận email.

1. **Cài đặt Exim**:
   ```bash
   sudo apt install exim4 -y
   ```

2. **Cấu hình Exim**:
   Chạy lệnh sau để cấu hình Exim:
   ```bash
   sudo dpkg-reconfigure exim4-config
   ```
   Chọn các tùy chọn sau trong quá trình cấu hình:
   - **General type of mail configuration**: Internet site; mail is sent and received directly using SMTP.
   - **System mail name**: `phattrn.site`.
   - **IP addresses to listen on**: Giữ nguyên `127.0.0.1; ::1`.
   - **Domains to relay mail for**: Để trống.
   - **Machines to relay mail for**: Để trống.
   - **Keep number of DNS-queries minimal**: No.
   - **Delivery method for local mail**: mbox format.
   - **Split configuration into small files**: Yes.

3. **Khởi động lại Exim**:
   ```bash
   sudo systemctl restart exim4
   ```

---

## Bước 3: Cài Đặt Và Cấu Hình Dovecot
Dovecot sẽ xử lý các giao thức IMAP và POP3 để truy xuất email.

1. **Cài đặt Dovecot**:
   ```bash
   sudo apt install dovecot-core dovecot-imapd dovecot-pop3d -y
   ```

2. **Cấu hình Dovecot**:
   Mở tệp cấu hình Dovecot:
   ```bash
   sudo nano /etc/dovecot/dovecot.conf
   ```
   Đảm bảo các dòng sau được đặt:
   ```plaintext
   protocols = imap pop3 lmtp
   mail_location = maildir:~/Maildir
   ```

3. **Bật Xác Thực**:
   Mở tệp `/etc/dovecot/conf.d/10-auth.conf` và đảm bảo các dòng sau:
   ```plaintext
   disable_plaintext_auth = no
   auth_mechanisms = plain login
   ```

4. **Khởi động lại Dovecot**:
   ```bash
   sudo systemctl restart dovecot
   ```

---

## Bước 4: Cài Đặt Roundcube
Roundcube cung cấp giao diện webmail để quản lý email.

1. **Cài đặt Apache, PHP và MariaDB**:
   ```bash
   sudo apt install apache2 php php-mysql mariadb-server -y
   ```

2. **Thiết lập MariaDB**:
   ```bash
   sudo mysql_secure_installation
   ```
   - Đặt mật khẩu cho root.
   - Xóa người dùng ẩn danh.
   - Không cho phép root đăng nhập từ xa.
   - Xóa cơ sở dữ liệu kiểm tra.

3. **Tạo Cơ Sở Dữ Liệu Cho Roundcube**:
   ```bash
   sudo mysql -u root -p
   CREATE DATABASE roundcube;
   CREATE USER 'roundcubeuser'@'localhost' IDENTIFIED BY 'securepassword';
   GRANT ALL PRIVILEGES ON roundcube.* TO 'roundcubeuser'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

4. **Cài đặt Roundcube**:
   ```bash
   sudo apt install roundcube roundcube-core roundcube-mysql -y
   ```

5. **Cấu hình Roundcube**:
   Mở tệp cấu hình:
   ```bash
   sudo nano /etc/roundcube/config.inc.php
   ```
   Cập nhật thông tin kết nối cơ sở dữ liệu:
   ```php
   $config['db_dsnw'] = 'mysql://roundcubeuser:securepassword@localhost/roundcube';
   ```

6. **Khởi động lại Apache**:
   ```bash
   sudo systemctl restart apache2
   ```

7. **Truy cập Roundcube**:
   Mở trình duyệt và truy cập `http://yourdomain.com/roundcube`.

---

## Bước 5: Cấu Hình Bản Ghi DNS
Để đảm bảo email của bạn được gửi và nhận đúng cách, hãy cấu hình các bản ghi DNS sau cho tên miền của bạn:

1. **MX Record**:
   ```plaintext
   Type: MX
   Host: @
   Value: mail.yourdomain.com
   Priority: 10
   ```

2. **A Record**:
   ```plaintext
   Type: A
   Host: mail
   Value: [Địa chỉ IP của VPS]
   ```

3. **SPF Record**:
   ```plaintext
   Type: TXT
   Host: @
   Value: "v=spf1 mx ~all"
   ```

4. **DKIM và DMARC** (Tuỳ Chọn):
   - Sử dụng công cụ như OpenDKIM để cấu hình DKIM.
   - Thêm bản ghi DMARC:
     ```plaintext
     Type: TXT
     Host: _dmarc
     Value: "v=DMARC1; p=none; rua=mailto:dmarc@yourdomain.com"
     ```

---

## Bước 6: Kiểm Tra Máy Chủ Email
1. Sử dụng một ứng dụng email như Thunderbird hoặc Outlook để thử gửi và nhận email.
2. Sử dụng các công cụ như [Mail Tester](https://www.mail-tester.com/) để kiểm tra cấu hình DNS và máy chủ.

---

## Tuỳ Chọn: Bảo Mật Máy Chủ Email Với SSL/TLS
Sử dụng Let's Encrypt để bảo mật máy chủ email với SSL/TLS:

1. **Cài đặt Certbot**:
   ```bash
   sudo apt install certbot -y
   ```

2. **Lấy Chứng Chỉ SSL**:
   ```bash
   sudo certbot certonly --standalone -d mail.yourdomain.com
   ```

3. **Cấu hình SSL cho Exim và Dovecot**:
   Cập nhật các tệp cấu hình của chúng để sử dụng chứng chỉ và khóa được tạo.

4. **Khởi động lại Dịch Vụ**:
   ```bash
   sudo systemctl restart exim4 dovecot
   ```

---

Máy chủ email của bạn đã sẵn sàng! Để có thêm các tính năng nâng cao hoặc hỗ trợ xử lý lỗi, tham khảo tài liệu chính thức của Exim, Dovecot và Roundcube.


# Reverse Proxy
## Reverse Proxy là gì?
Reverse Proxy là một hệ thống được đặt trước các nhóm Server, đóng vai trò như người trung gian để phục vụ việc giao tiếp giữa Client và Web Server. Cụ thể, Reverse Proxy sẽ chặn yêu cầu từ Client (như trình duyệt Web), sau đó giao tiếp với Web Server thay cho Client đó.
![image](https://github.com/user-attachments/assets/2b1942a1-6eb2-46bc-9f3e-2594544d7846)

Trong các giao tiếp Internet tiêu chuẩn, Client sẽ trực tiếp kết nối với Web Server, chúng gửi yêu cầu và chờ đợi kết quả phản hồi trực tiếp từ Web Server. Nhưng với hệ thống có Reverse Proxy, thì Reverse Proxy sẽ tiếp nhận yêu cầu từ Client, sau đó gửi yêu cầu này đến Web Server. Kết quả phản hồi từ Web Server được gửi trả về lại cho Reverse Proxy, sau đó mới được truyền đến Reverse Proxy.
## LAMP stack
## Setup Reverse Proxy
### Cài đặt Nginx
1. Sử dụng giao diện NGINX Manager của WHM: WHM » Home » Software » NGINX Manager.
2. Vô lại trang web đang host trên hosting, bấm "F12" trên bàn phím, vô tab Network, chọn web của mình, ở phần Respond Header nếu để server: nginx là đã thiết lập thành công.
![image](https://github.com/user-attachments/assets/ebf6a8a1-83d9-4f35-8ee8-1237228cdf25)
### Cấu hình Reverse Proxy
NGINX sử dụng file /etc/nginx/conf.d/ea-nginx.conf để cấu hình trực tiếp. Ngoài ra còn có thể cấu hình qua 2 file này nếu có sử dụng gói ea-nginx:
* /etc/nginx/ea-nginx/settings.json
* /etc/nginx/ea-nginx/cache.json
#### Configuration Setting
Có thể điều chỉnh Directive thông qua giao diện WHM (WHM » Home » Service Configuration » Apache Configuration » Global Configuration) hoặc /etc/nginx/ea-nginx/settings.json. Có 3 directive:
* Keep-Alive: Nếu giá trị này là On, NGINX sẽ sử dụng giá trị 32.
* Keep-Alive Timeout: NGINX chỉ sử dụng giá trị được đặt trong WHM’s Global Configuration.
* Max Keep-Alive Requests: NGINX chỉ sử dụng giá trị được đặt trong WHM’s Global Configuration.
#### Global Configurations
* Config toàn cục bằng cách đặt file .conf trong /etc/nginx/conf.d/.
* Đối với server block, tạo file .conf tại etc/nginx/conf.d/server-includes/ 
#### User Configuration
* Để cấu hình đối với toàn bộ server block, tạo file .conf tại /etc/nginx/conf.d/users/username
* Để cấu hình đối với server block của domain cụ thể, tạo file .conf tại /etc/nginx/conf.d/users/username/domainname/



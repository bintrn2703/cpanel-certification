# Setup Mail Server thủ công mà không sử dụng control panel

Thiết lập mail server với **Exim** làm MTA (Mail Transfer Agent), **Dovecot** để xử lý POP/IMAP, và **Roundcube** là giao diện webmail.

## Bước 1: Cập Nhật Hệ Thống
Cập nhật và nâng cấp hệ thống để đảm bảo tất cả các gói phần mềm đều mới nhất:

```bash
sudo apt update && sudo apt upgrade -y
```

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


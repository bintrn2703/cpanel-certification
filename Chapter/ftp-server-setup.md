# Cài Đặt FTP Server thủ công không sử dụng Control Panel

## Bước 1: Cập Nhật Hệ Thống
Trước khi bắt đầu cài đặt, cần cập nhật hệ thống của mình để đảm bảo tất cả các gói phần mềm đều mới nhất.

```bash
sudo apt update
sudo apt upgrade -y
```
## Bước 2: Cài Đặt vsftpd
vsftpd là một trong những FTP server phổ biến và bảo mật của Ubuntu Server. Để cài đặt vsftpd, chạy lệnh sau:
```
sudo apt install vsftpd -y
```
### Bước 3: Kiểm Tra Trạng Thái vsftpd
Sau khi cài đặt, kiểm tra xem dịch vụ vsftpd đã được kích hoạt và đang chạy chưa:
```
sudo systemctl status vsftpd
```
Nếu dịch vụ chưa chạy, có thể khởi động nó bằng lệnh:
```
sudo systemctl start vsftpd
```
Để chắc chắn dịch vụ tự động khởi động khi hệ thống khởi động lại, bạn có thể kích hoạt:
```
sudo systemctl enable vsftpd
```
### Bước 4: Cấu Hình vsftpd
Để cấu hình FTP server, bạn cần chỉnh sửa file cấu hình /etc/vsftpd.conf. Bạn có thể mở file này bằng trình soạn thảo văn bản như nano:
```
sudo nano /etc/vsftpd.conf
```
Dưới đây là một số cài đặt quan trọng bạn có thể thay đổi:

* Cho phép người dùng đăng nhập bằng tài khoản hệ thống:
```
local_enable=YES
```
* Cho phép người dùng tải lên dữ liệu (upload):
```
write_enable=YES
```
* Chế độ passive để giúp qua firewall: Thêm vào cuối file cấu hình:
```
    pasv_min_port=10000
    pasv_max_port=10100
```
### Bước 5: Khởi Động Lại Dịch Vụ
Sau khi cấu hình xong, cần khởi động lại dịch vụ vsftpd để áp dụng các thay đổi:
```
sudo systemctl restart vsftpd
```
### Bước 6: Mở Cổng Firewall
Nếu đang sử dụng UFW (Uncomplicated Firewall) trên Ubuntu, cần mở các cổng FTP (cổng 21 và phạm vi cổng passive nếu có cấu hình).
Mở cổng FTP:
```
sudo ufw allow 21/tcp
```
Mở phạm vi cổng passive (10000-10100):
```
sudo ufw allow 10000:10100/tcp
```
Kiểm tra lại trạng thái firewall:
```
sudo ufw enable
sudo ufw status
```
### Bước 7: Tạo Người Dùng FTP

Để tạo người dùng FTP, cần tạo một tài khoản hệ thống mới hoặc sử dụng tài khoản hiện có.

Tạo tài khoản người dùng mới:
```
sudo adduser ftpuser
```
Khi tạo xong tài khoản, có thể chỉ định quyền truy cập cho tài khoản này vào thư mục FTP, ví dụ:
```
sudo mkdir /home/ftpuser/ftp
sudo chown nobody:nogroup /home/ftpuser/ftp
sudo chmod a-w /home/ftpuser/ftp
```
Tạo thư mục con để người dùng có thể tải lên:
```
sudo mkdir /home/ftpuser/ftp/files
sudo chown ftpuser:ftpuser /home/ftpuser/ftp/files
```
### Bước 8: Kiểm Tra Kết Nối FTP

Dùng lệnh FTP từ máy tính cá nhân:
```
ftp <IP của VPS>
```
Đăng nhập bằng tên người dùng và mật khẩu đã tạo. Nếu kết nối thành công, bạn sẽ thấy dấu nhắc FTP và có thể tải lên/tải xuống tập tin.
![image](https://github.com/user-attachments/assets/4f15a130-9862-4794-b192-86de016f8e40)






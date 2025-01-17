# Reverse Proxy
## Reverse Proxy là gì?
Reverse Proxy là một hệ thống được đặt trước các nhóm Server, đóng vai trò như người trung gian để phục vụ việc giao tiếp giữa Client và Web Server. Cụ thể, Reverse Proxy sẽ chặn yêu cầu từ Client (như trình duyệt Web), sau đó giao tiếp với Web Server thay cho Client đó.
![image](https://github.com/user-attachments/assets/2b1942a1-6eb2-46bc-9f3e-2594544d7846)

Trong các giao tiếp Internet tiêu chuẩn, Client sẽ trực tiếp kết nối với Web Server, chúng gửi yêu cầu và chờ đợi kết quả phản hồi trực tiếp từ Web Server. Nhưng với hệ thống có Reverse Proxy, thì Reverse Proxy sẽ tiếp nhận yêu cầu từ Client, sau đó gửi yêu cầu này đến Web Server. Kết quả phản hồi từ Web Server được gửi trả về lại cho Reverse Proxy, sau đó mới được truyền đến Reverse Proxy.
## LAMP stack
LAMP stack là một bộ công cụ mã nguồn mở được sử dụng để tạo và phát triển ứng dụng web. Để hoạt động tốt, bộ công cụ này cần có hệ điều hành, web server, database và ngôn ngữ lập trình. ![image](https://github.com/user-attachments/assets/fb715ba7-a455-47c5-b91f-f0a60c7da6d9)

Tên LAMP là từ viết tắt của các program sau:
* Hệ điều hành Linux.
* Apache HTTP Server.
* Hệ quản trị database MySQL.
* Ngôn ngữ lập trình PHP.

Mỗi program đại diện cho một layer của stack, và chúng cùng tạo ra một trang web động và database-driven.
## Setup Reverse Proxy
Để setup reverse proxy, trước tiên ta cần 2 VPS: 1 VPS chạy Nginx cho reverse proxy, 1 VPS chạy LAMP để làm web server. Mục tiêu của là sẽ sử dụng Reverse Proxy để ẩn đi IP của web server giúp bảo mật, tránh cho web server trước các cuộc tấn công DDOS.
### Trên VPS chạy Reverse Proxy
1. Cài Nginx trên terminal bằng lệnh:
```
sudo apt install nginx
```
2. Mở file cấu hình Nginx
```
sudo nano /etc/nginx/conf.d/nginx.conf
```
3. Thêm hoặc chỉnh sửa các dòng sau để cấu hình Reverse Proxy:
```
server {
    listen 80;
    server_name reverse_proxy_domain_or_ip;

    location / {
        proxy_pass http://web_server_domain_or_ip;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
4. Lưu file và thoát khỏi trình chỉnh sửa. Kiểm tra cấu hình Nginx:
```
sudo nginx -t
```
5. Sau đó, khởi động lại Nginx:
```
sudo systemctl restart nginx
```
### Trên VPS chạy webserver
VPS này sẽ được cài đặt LAMP Stack phục vụ cho việc chạy web server.
1. Cài đặt Apache:
```
sudo apt install apache2
```
2. Cài đặt MySQL:
```
sudo apt install mariadb-server
sudo mysql_secure_installation
```
3. Cài đặt PHP:
```
sudo apt install php libapache2-mod-php php-mysql
```
4. Kiểm tra cấu hình:
   * Truy cập vào http://your_server_ip để kiểm tra trang mặc định của Apache.
   * Truy cập vào http://your_server_ip/info.php để kiểm tra xem PHP đã hoạt động chưa.
5. Chuyển source web vào.
### Kiểm tra xem đã thành công chưa?
Nhập địa chỉ IP của VPS chạy Reserve proxy vô trình duyệt, nếu nội dung hiển thị là của VPS chạy web server là đã thành công.
![image](https://github.com/user-attachments/assets/16251228-b9d1-4b90-bd88-d4885b1be086)

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

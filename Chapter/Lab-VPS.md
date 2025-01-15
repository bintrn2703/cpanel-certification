# Triển khai và cấu hình VPS
1. Truy cập vào đường dẫn portal.vietnix.com
2. Đăng ký và tạo VPS với hệ điều hành/cấu hình mong muốn.
3. Mở terminal, kết nối VPS bằng lệnh:
```
$ ssh root@<IP>
```
4. Màn hình hiển thị "Welcome..." là login vô VPS thành công.
  ![image](https://github.com/user-attachments/assets/eb1382b9-3eb4-4ba5-823f-e0a29bbab622)
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
   
# Chuyển dữ liệu website

# Reverse Proxy
## Reverse Proxy là gì?
Reverse Proxy là một hệ thống được đặt trước các nhóm Server, đóng vai trò như người trung gian để phục vụ việc giao tiếp giữa Client và Web Server. Cụ thể, Reverse Proxy sẽ chặn yêu cầu từ Client (như trình duyệt Web), sau đó giao tiếp với Web Server thay cho Client đó.
![image](https://github.com/user-attachments/assets/2b1942a1-6eb2-46bc-9f3e-2594544d7846)

Trong các giao tiếp Internet tiêu chuẩn, Client sẽ trực tiếp kết nối với Web Server, chúng gửi yêu cầu và chờ đợi kết quả phản hồi trực tiếp từ Web Server. Nhưng với hệ thống có Reverse Proxy, thì Reverse Proxy sẽ tiếp nhận yêu cầu từ Client, sau đó gửi yêu cầu này đến Web Server. Kết quả phản hồi từ Web Server được gửi trả về lại cho Reverse Proxy, sau đó mới được truyền đến Reverse Proxy.
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

# LAMP stack
# LEMP Stack
# lamp/lemp stack multi vHosts

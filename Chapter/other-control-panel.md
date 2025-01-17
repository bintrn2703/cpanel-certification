# Cài đặt các loại Control Panel khác nhau
## So sánh các loại Control Panel khác nhau
| STT | Tiêu Chí              | DirectAdmin         | aaPanel            | CyberPanel         | VestaCP                  |
|-----|------------------------|---------------------|--------------------|--------------------|--------------------------|
| 1   | WebPanel Miễn Phí      | Không               | Miễn Phí/ Có Phí  | Miễn Phí/ Có Phí  | Miễn Phí                |
| 2   | Giới hạn users/domains | Giới hạn theo gói   | 1 user            | Nhiều users/domains | Nhiều users/domains      |
| 3   | WebPanel Mặc Định      | Apache              | Apache/Nginx      | OpenLiteSpeed      | Apache/Nginx             |
| 4   | Hỗ trợ SSL             | Có                  | Có                | Có                | Có - Không ổn định       |
| 5   | File Manager           | Có                  | Có                | Có                | Không - phải active thủ công |
| 6   | Hỗ trợ FTP             | Có                  | Có                | Có                | Có                      |
| 7   | Hỗ trợ PHPMyAdmin      | Có                  | Có                | Có                | Có                      |
| 8   | DNS Server             | Có                  | Có                | Có                | Có                      |
| 9   | Email Server           | Có                  | Không             | Có                | Có                      |
| 10  | Backup - Restore       | Setup thủ công      | Setup thủ công    | Setup thủ công    | Đã có predefined - có thể custom |
| 11  | Hỗ trợ Docker          | Không               | Có                | Có                | Không                   |
| 12  | Hỗ trợ Multi PHP       | Có - phải build thêm| Có - phải build thêm | Có - Mặc định    | Có - phải build thêm thủ công |
| 13  | Reseller               | Có                  | Không             | Không             | Không                   |
| 14  | Hỗ trợ NodeJS/ Python  | ONLY in PRO pack    | Có                | Không             | Không                   |
| 15  | Thao tác cài đặt, sửa đổi gói/plugins | Dễ                 | Dễ               | Khó               | Khó                     |
| 16  | Firewall CSF/LFD                       | Có + GUI         | FW cơ bản   | Có                | Có                      |
| 17  | Terminal in GUI                        | Không            | Có          | Không             | Không                   |
| 18  | Hỗ trợ Packages - Chia gói Hosting     | Có               | Không       | Có                | Có                      |
| 19  | Hỗ trợ chuyển qua sử dụng Litespeed    | Có               | Không - chỉ có Openlitespeed | Có        | Không                   |
| 20  | Các chức năng trả phí nâng cao         | Chỉ mua theo gói | Mua theo từng plugins | Mua theo từng plugins | Mua theo từng plugins   |
| 21  | Hỗ trợ cấu hình qua API                | Có               | Có          | Không - chỉ có github | Không                   |

## cPanel
1. Mở terminal, kết nối VPS bằng lệnh:
```
$ ssh root@<IP>
```
2. Màn hình hiển thị "Welcome..." là login vô VPS thành công.
  ![image](https://github.com/user-attachments/assets/eb1382b9-3eb4-4ba5-823f-e0a29bbab622)
3. Cài đặt cPanel lên server bằng cách mở terminal và nhập lệnh
```
cd /home && curl -o latest -L https://securedownloads.cpanel.net/latest && sh latest
```
4. Đăng nhập vào hệ thống bằng url được cung cấp sau quá trình cài đặt.
5. Tiếp theo, đăng nhập vào cPanel Customer Portal để cấp quyền truy cập máy chủ. Nếu không có tài khoản ID cPanel thì tạo một cái. 
   ![image](https://github.com/user-attachments/assets/e0322bfb-4532-441d-bb05-17e42d82faf6)
6. Khi đã xác nhận email và xác minh tài khoản của mình, bạn sẽ sẵn sàng để kích hoạt bản dùng thử của bạn và tiến hành thiết lập máy chủ.
7. Bây giờ WHM đã được cài đặt, có thể bắt đầu tạo và quản lý tài khoản cPanel trên máy chủ của mình.
8. Nếu muốn triển khai web lên cPanel, cần trỏ domain về IP của VPS bằng record A.
    ![image](https://github.com/user-attachments/assets/3c35cd6c-c412-41c0-a3d3-e54162ac985c)
## aaPanel
1. Khởi chạy terminal với quyền root và chạy lệnh sau để tải xuống và cài đặt phần mềm trên server:
```
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh 15960f3a
```
2. Sau khi cài đặt xong, trên termianl sẽ hiển thị URL đăng nhập aaPanel, tên người dùng và mật khẩu với định dạng như sau:
```
=============================================================================
aaPanel default info!
=============================================================================
aaPanel Internet Address: https://YourServerIPaddress:port/948a07ef
aaPanel Internet Address: https://YourServerIPaddress:port/948a07ef
username: ********
password: ********
Warning:
If you cannot access the panel,
release the following port (26886|888|80|443|20|21) in the security group
=============================================================================
```
3. Sao chép URL đăng nhập aaPanel vào thanh địa chỉ trình duyệt, điền vào tài khoản và mật khẩu. ![image](https://github.com/user-attachments/assets/d197b7a7-7f67-4bd4-9f69-a1767bdd818e)
4. Chọn cài đặt mô hình LNMP/LAMP sau khi cài đặt.
5. Bây giờ aaPanel đã được cài đặt thành công, có thể bắt đầu tạo và quản lý trang web trên máy chủ. ![image](https://github.com/user-attachments/assets/33c57e58-8b42-4600-bd38-f09fd6740f74)

## DirectAdmin
Do DirectAdmin tốn phí nên sử dụng DirectAdmin cung cấp sẵn trong OS image của Vietnix
1. Vô trang quản lí VPS, chọn Reinstall. ![image](https://github.com/user-attachments/assets/879ad830-24d8-4f82-b5e6-c3a5452d662f)
2. Chọn OS image có chữ "DirectAdmin" và bấm Reinstall. ![image](https://github.com/user-attachments/assets/1c230dc7-f574-465a-a918-ff672cbdfa5b)

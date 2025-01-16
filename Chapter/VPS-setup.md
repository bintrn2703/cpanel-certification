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


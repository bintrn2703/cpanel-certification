# Windows Server
## Allow/Block/Limit port/IP bằng Windows Firewall
1. Đăng nhập vào VPS, từ Start menu > tìm và mở Windows Defender Firewall with Advanced Settings. ![image](https://github.com/user-attachments/assets/47cff32e-025f-4478-a5a8-76fbb341388f)
2. Để áp dụng firewall rule theo hướng từ ngoài Internet vào máy, chọn Inbound > New Rule. ![image](https://github.com/user-attachments/assets/97e09c1b-b4a4-42ab-bf3c-c7710874c265)
3. Chọn Custom > Next. <br>![image](https://github.com/user-attachments/assets/6f388b56-fbf4-4490-881a-f812f72edf6e)
4. Chọn All Program để áp dụng rule cho toàn hệ thống > Next. <br> ![image](https://github.com/user-attachments/assets/45bff499-326f-45dc-b201-5fb083a1ae79)
5. Chọn giao thức mong muốn ở phần Protocol Type (vd: TCP,...), chọn port mong muốn (vd: port 1433 cho SQLServer). <br> ![image](https://github.com/user-attachments/assets/a5fbe9e0-df8c-4050-8749-c991514860a9)
6. Chọn Add để thêm Ip/dải IP muốn áp dụng rule. <br> ![image](https://github.com/user-attachments/assets/aa04b92c-b7f0-46cc-99d6-690327854282)
7. Chọn Allow hoặc Block tùy theo nhu cầu. <br> ![image](https://github.com/user-attachments/assets/e0bf92b7-f539-4bb4-b711-5cd7006c65ed)
8. Chọn profile muốn áp dụng rule. <br> ![image](https://github.com/user-attachments/assets/74f4458e-1d0b-459c-953e-761c3d76b625)
9. Đặt tên cho rule mới tạo > Finish.<br> ![image](https://github.com/user-attachments/assets/d60e2f33-c41b-4ee8-b6ea-1c51bbd6f57a)









## Cài đặt và triển khai website qua IIS WebServer
## Cài đặt và triển khai website WordPress
## Cài đặt SQL Server

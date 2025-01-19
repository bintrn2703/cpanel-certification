![image](https://github.com/user-attachments/assets/840206c6-8d5e-4fec-b318-89b3c832a32e)# Windows Server
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
1. Từ Start Menu > tìm và mở Server Manager. <br> ![image](https://github.com/user-attachments/assets/abed9c93-2d07-4e95-87a2-3cd17ae6ecfe)
2. Chọn Mange > Add Roles and Features. <br> ![image](https://github.com/user-attachments/assets/a5409872-f0d0-405f-b5df-f5578d501728)
3. Chọn Role-based and feature-based installation > Next. <br> ![image](https://github.com/user-attachments/assets/e4d43d54-cef1-4e98-8999-8857197ba3fd)
4. Chọn server của mình. <br> ![image](https://github.com/user-attachments/assets/cc078974-1a19-4766-b83c-ac7238a6ff05)
5. Tìm role Web Server (IIS) và chọn nó. <br> ![image](https://github.com/user-attachments/assets/5893e212-b733-428b-925e-e8e7980f8f74)
6. Chọn 2 features .NET framwork > Install. <br> ![image](https://github.com/user-attachments/assets/d772a987-5b23-42fb-99e1-b112a11f3313)
7. Chờ hoàn tất quá trình Install.
8. Sau khi Install hoàn tất, vào Start Menu tìm IIS Manager. ![image](https://github.com/user-attachments/assets/4596c73f-9a7e-4323-9a1b-29d6c8a74bc4)
9. IIS Manager đã được cài đặt thành công. <br> ![image](https://github.com/user-attachments/assets/9bff8622-dde4-4e42-929a-9ab684697348)
10. Dùng trình duyệt truy cập vào IP của VPS, nếu hiển thị màn hình chào mừng Windows Server như vầy là đã thành công. ![image](https://github.com/user-attachments/assets/8fcda3f0-3c5a-4b7c-bfb2-57d6ab977d2f)
## Cài đặt và triển khai website WordPress
## Cài đặt SQL Server

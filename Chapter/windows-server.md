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
1. Đăng nhập vào bằng tải khoản Administrator, tải file .iso của SQL Server về, chuột phải vào file iso chọn Mount để gắn file .iso vào máy. <br> ![image](https://github.com/user-attachments/assets/f8496c37-e842-4c3a-8683-fc29e2baeb1f)
2. Vào ổ đĩa vừa được Mount từ file .iso, click chuột phải vào Setup.exe > Run as Administrator. <br> ![image](https://github.com/user-attachments/assets/57f0e1d7-3188-4c70-8ee1-38eafa2dae71)
3. Chọn New SQL Server standalone installation ... <br> ![image](https://github.com/user-attachments/assets/fb7e864c-8bca-45c9-9302-e8c7ea10bb73)
4. Nhập Key và ấn Next. <br> ![image](https://github.com/user-attachments/assets/cd58251e-230e-449c-b5f5-bf47dd60f66a)
5. Chọn ô I accept the ... <br> ![image](https://github.com/user-attachments/assets/bbc359d4-0cc7-494e-ad2b-abbb1cb45af8)
6. Next > Next > Next.
7. Để trống và Next. <br> ![image](https://github.com/user-attachments/assets/a4e53b91-e741-42a1-b3fe-da527ea4b29a)
8. Chọn Database Engine Service và Next. <br> ![image](https://github.com/user-attachments/assets/6491d24f-e818-4a3c-846b-570ef03ffa49)

9. Để mặc định và Next. <br> ![image](https://github.com/user-attachments/assets/eaf799e0-030f-4b6e-8076-42d60759cab4)
10. Để mặc định và Next. <br> ![image](https://github.com/user-attachments/assets/ca3dfc62-cebe-424c-b8d9-97a1a3cb500b)
11. Chọn Add Current User để thêm account Admin, sau đó chọn Next. <br> ![image](https://github.com/user-attachments/assets/6e3bf464-3835-472e-9a2d-c7fa75216b98)
12. Review lại và ấn Install. <br> ![image](https://github.com/user-attachments/assets/b5338e7f-2dfb-49ab-8ed2-d1b822c20966)
13. Quá trình cài đặt bắt đầu diễn ra. <br> ![image](https://github.com/user-attachments/assets/fe469cd2-6d6c-4778-a595-b99dca618cd2)
14. Sau khi cài đặt xong, chọn Close. ![image](https://github.com/user-attachments/assets/4ac874a9-226e-40fe-85b1-51b413720f70)
15. Sau khi cài xong SQL Server, để có thể truy cập và quản lí Database, nên cài thêm SSMS. <br> ![image](https://github.com/user-attachments/assets/3bb96cf7-8867-4d00-9d0e-2838315e4d2e)
16. Chọn Install. <br> ![image](https://github.com/user-attachments/assets/1ee2fc30-7b30-49cd-a71f-bfa35267662b)
17. Quá trình cài SSMS được diễn ra. <br> ![image](https://github.com/user-attachments/assets/c4007e15-1eac-4e14-b596-196121f9005c)
18. Cài đặt SSMS thành công, chọn Close.<br>![image](https://github.com/user-attachments/assets/6848afba-a0ba-48d0-bc71-40e3fb8a0631)
19. Truy cập vào SSMS từ Start Menu. <br> ![image](https://github.com/user-attachments/assets/d530992a-f6c3-4948-993a-191661ac34d6)
20. Để mặc định và Connect.<br> ![image](https://github.com/user-attachments/assets/693e383d-34f8-4c43-917c-9368526c25aa)


  


















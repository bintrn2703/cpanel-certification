# cPanel Fundamental
## System
### So sánh CPanel và WHM? 
Giống như một tòa nhà chung cư. Mỗi giao diện cPanel sẽ tồn tại như một căn hộ trong tòa nhà. WHM giống như tòa nhà và là giao diện dành cho admin. Quản trị viên đăng nhập vào WHM bằng tài khoản root cho hệ thống - đây là tài khoản có thể làm bất cứ điều gì họ muốn trên máy chủ mà không bị hạn chế. 
### Resource là gì? 
Là các thành phần hệ thống như RAM, đisk (cả hiệu suất và dung lượng ổ đĩa), sức mạnh xử lý của CPU và băng thông/thông lượng. 
### Raid
| Loại RAID      | Đặc điểm chính                                                    | Ưu điểm                                                     | Nhược điểm                                                  | Dùng cho mục đích nào                  |
|----------------|------------------------------------------------------------------|------------------------------------------------------------|-------------------------------------------------------------|----------------------------------------|
| **RAID 0**     | - Chia nhỏ dữ liệu ra các ổ đĩa để tăng tốc độ đọc/ghi            | - Tốc độ cao                                                | - Không có dự phòng (nếu một ổ đĩa hỏng, toàn bộ dữ liệu sẽ mất) | - Khi cần tốc độ cao và không quan trọng về dự phòng |
| **RAID 1**     | - Sao chép dữ liệu đồng nhất lên hai hoặc nhiều ổ đĩa             | - Độ tin cậy và khả năng dự phòng tốt                        | - Hiệu quả sử dụng dung lượng thấp (cần gấp đôi số ổ đĩa)    | - Khi cần bảo vệ dữ liệu và dự phòng  |
| **RAID 10**    | - Kết hợp RAID 0 và RAID 1 (sao chép và chia nhỏ dữ liệu)         | - Tốc độ cao và khả năng dự phòng tốt                        | - Cần nhiều ổ đĩa hơn (ít nhất 4 ổ đĩa)                      | - Khi cần tốc độ cao và bảo vệ dữ liệu |


# Bai3_MaNguonMo
Bài tập 03 của sinh viên: K225480106083 - Trương Văn Quyến  - Môn Phát triển ứng dụng với mã nguồn mở-TEE0421

Lớp: 58KTPM

Bài tập 03:

SỬ DỤNG WORDPRESS ĐỂ TẠO WEB SITE
deadline : 23h59 ngày 12 tháng 5 năm 2026.
SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ TẠO docker ccompose chứa:
Mariadb: sử dụng image: mariadb:latest để làm hệ quản trị csdl cho wordpress
Phpmyadmin: sư dụng image: phpmyadmin:latest để đăng nhập vào mariadb rồi tạo csdl trống (chỉ để xem, ko cần tạo bảng từ đây, wordpress sẽ làm hết)
WordPress: Sử dụng image: wordpress:latest, truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin
Yêu cầu: sau khi có 3 service này trong file docker-compose.yml :
Cấu hình để hệ thống chạy
Sử dụng cloudflare tunnel để public web này lên 1 sub-domain
Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...
Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...
Nhận xét việc sử dụng mã nguồn mở wordpress để tạo website (tốn công sức thế nào, dễ/khó dùng ra sao, tốn kém tài nguyên(ssh/ram) của máy chủ ra sao,....)
Bài Làm:
PHẦN 1: GIỚI THIỆU
Mục tiêu bài tập: xây dựng một hệ thống web gồm 3 thành phần:
MariaDB → hệ quản trị cơ sở dữ liệu
phpMyAdmin → giao diện quản lý database
WordPress → hệ thống website blog
Tất cả chạy bằng Docker Compose trên Ubuntu

Sau đó dùng Cloudflare Tunnel để public ra internet

PHẦN 2: CÀI ĐẶT MÔ HÌNH DOCKER COMPOSE
Chúng ta sẽ bỏ qua bước cấu hình máy ảo (VM) và ssh do không thuộc bài tập.

Bước 1: Cài Docker và Tạo thư mục project
sử dụng lệnh sudo apt install docker.io docker-compose -y để cài đặt docker và docker-compose:
<img width="1916" height="932" alt="Screenshot 2026-06-14 164325" src="https://github.com/user-attachments/assets/47263936-be08-4f27-8621-fa6c4ba2d307" />
kiểm tra xem cài đặt thành công chưa:
<img width="637" height="127" alt="Screenshot 2026-06-14 165333" src="https://github.com/user-attachments/assets/6317e022-ce9a-4be6-9232-0586be75d115" />
Bước 2: Tạo file docker-compose.yml
<img width="1046" height="528" alt="image" src="https://github.com/user-attachments/assets/73d7cca9-2627-42eb-afeb-651e997dbda8" />
<img width="1916" height="932" alt="Screenshot 2026-06-14 164325" src="https://github.com/user-attachments/assets/f6f4b612-2eb1-497c-b7c3-9c0a31d93fa0" />
chạy hệ thống:
<img width="687" height="533" alt="image" src="https://github.com/user-attachments/assets/e71e44d5-a41b-4c1e-94a6-aede27bfbfbf" />
Kiểm tra: docker ps
<img width="1661" height="141" alt="Screenshot 2026-06-14 164355" src="https://github.com/user-attachments/assets/ce04825a-1197-4af8-9701-d17e690c28d4" />
Truy cập các trang hệ thống:
<img width="1862" height="868" alt="Screenshot 2026-06-14 164200" src="https://github.com/user-attachments/assets/aac5d755-b746-402f-9113-802c92bdc483" />
phpMyAdmin:
<img width="1907" height="886" alt="Screenshot 2026-06-14 164100" src="https://github.com/user-attachments/assets/589d32c3-e18d-493f-abaa-0f03c5a7ddc2" />
đăng nhập vào phpMyAdmin bằng tài khoản root, password rootpassword:
<img width="508" height="442" alt="image" src="https://github.com/user-attachments/assets/7316c9b8-c0c7-4170-aabb-ed33aca352dc" />
<img width="1892" height="853" alt="Screenshot 2026-06-14 164823" src="https://github.com/user-attachments/assets/572a2564-5a24-4e7c-b84e-53cfdac3b819" />
Bước 3: CLOUDFLARE TUNNEL (PUBLIC WEBSITE):
<img width="1782" height="898" alt="image" src="https://github.com/user-attachments/assets/1eed5b1a-85b9-4d6d-a73e-319aa55f5b2a" />
tiếp theo, tạo tunnel: cloudflared tunnel create wordpress-tunnel
Config tunnel: mkdir -p ~/.cloudflared nano ~/.cloudflared/config.yml
<img width="575" height="218" alt="image" src="https://github.com/user-attachments/assets/5134f762-6516-4a26-ab6b-fc6022d1dea8" />
lệnh tạo DNS tự động: cloudflared tunnel route dns wordpress-tunnel blog.truongquyen.io.vn
sau đó chạy tunnel bằng lệnh: cloudflared tunnel run wordpress-tunnel
<img width="1027" height="407" alt="image" src="https://github.com/user-attachments/assets/194c381d-33b7-450f-88f7-72130c5cc6fa" />
kết quả:
<img width="978" height="476" alt="image" src="https://github.com/user-attachments/assets/247d3dc7-4816-49e7-8f68-3fddfbe76e1e" />
Tạo bài viết trên wordpress:
<img width="1778" height="942" alt="Screenshot 2026-06-14 172124" src="https://github.com/user-attachments/assets/4a9c038b-2308-4cb8-a2a1-61e89429c2fa" />
<img width="1640" height="958" alt="Screenshot 2026-06-14 173215" src="https://github.com/user-attachments/assets/00ff879d-4305-4f4a-ac25-3488a37ba9bd" />
<img width="1800" height="947" alt="Screenshot 2026-06-14 173222" src="https://github.com/user-attachments/assets/0853531d-1a0f-4cad-88a6-084ca9850590" />
Nhận xét:
WordPress là một mã nguồn mở phổ biến, dễ sử dụng và phù hợp cho việc tạo website nhanh chóng. Nhờ có giao diện quản trị trực quan và nhiều plugin hỗ trợ, người dùng không cần biết quá nhiều về lập trình vẫn có thể xây dựng website hoàn chỉnh. Khi kết hợp với Docker Compose, việc triển khai trở nên thuận tiện và dễ quản lý hơn.









Thư viện Aws SNS: Amazon SNS Mobile Push Notifications
1. Mục đích: 
- Tạo ra thư viện chung có thể sử dụng cho nhiều dự án
- Hướng dẫn chi tiết để có thể maintain sau này (important)

2. Mô tả
- Project demo này sử dụng cakephp 3.2.8
- Sử dụng aws-sdk-php v2:
Requirment: http://docs.aws.amazon.com/aws-sdk-php/v2/guide/requirements.html
+) PHP 5.3.3+ compiled with the cURL, JSON, and XML extensions
+) A recent version of cURL 7.16.2+ compiled with OpenSSL and zlib
+) Install: http://docs.aws.amazon.com/aws-sdk-php/v2/guide/installation.html
- Cài đặt: Khuyến khích sử dụng composer để cài đặt (có thể sử dụng file zip).
Sử dụng composer:
B1. Add vào file composer.json ở thư mục root của project nếu chưa có thì tạo:
    "require": {
        "aws/aws-sdk-php": "2.*",
    },
B2: Cài đặt (dùng command: composer update hoặc composer install)

- Chức năng push notification là một chức năng quan trọng và không thể thiếu trong ứng dụng mobile. Vì vậy khi thực chiện chức năng này cần test thật cẩn thận. Tránh push notifications nhầm trên môi trường live (môi trường thật) gây phản cảm cho user.
- Ngoài ra còn cần chú ý chức năng này phải chạy tốt khi số lượng user trong database nhiều. 
- Cần phải có cơ chế ghi log riêng cho phần này để khi có lỗi thì có thể tracking được
- Để tránh push notifcation nhầm giữa các môi trường:
+) Config database: 
a. Đọc config từ database: sẽ định nghĩa config trong database: database thật chứa config thật, database dev chưa config dev
b. Đọc config từ file config
+) Nhận diện môi trường push theo IP Address 
+) Đặt trên topic push khác nhau giữa hai môi trường
- Về việc tối ưu push:
+) Giới hạn số lượng user được push trong một topic. Một topic nên chứa 10.000 end point của user
+) Khi thêm endpoint vào một topic thì nên thêm theo batch (lô). Nên add 1.000 endpoint user vào topic với một lần
+) Với trường hợp có quá nhiều end point thì có thể push thẳng cho các user thông qua end point không cần tạo topic để push
+) Lấy process pid qua lệnh "pa aux | grep *" => để chạy crontab mình ko bị dẫm chân lên nhau

3. Implementation



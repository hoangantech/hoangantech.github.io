---
layout: post
author: Tien Cao-hoang
tag: Raspberry Pi
---

Chạy một chương trình trên Raspbery Pi khi khởi động (sử dụng SYSTEMD)

Giả sử bạn có một chương trình python (1 file sample.py trong thư mục /home/pi/ ). Để chạy được file này khi khởi động Raspberry Pi, ta có thể sử dụng file systemd. systemd cung cấp một chuẩn xử lý cho phép điều khiển một chương trình có thể chạy trong hệ thống Linux khi khởi động. Lưu ý: systemd chỉ có từ phiên bản Jessie của Raspbian OS.

#### Step 1– Tạo một Unit file

Tạo một unit file có tên sample.service bằng lệnh:

`sudo nano /lib/systemd/system/sample.service`

Thêm các dòng lệnh bên dưới vào file :

>
    [Unit]
    Description=My Sample Service
    After=multi-user.target

    [Service]
    Type=idle
    ExecStart=/usr/bin/python /home/pi/sample.py

    [Install]
    WantedBy=multi-user.target

Lưu và thoát khỏi nano.

Cấu hình cho systemd chạy một chương trình khi khởi động.

File này sẽ tạo một dịch vụ mới (new service) có tên “Sample Service” và dịch vụ này được thực thi sau khi môi trường multi-user được khởi tạo. “ExecStart” xác định lệnh mà chúng ta muốn chạy. “Type” được cài là “idle” để chắc chắn rằng lệnh ExecStart được chạy khi tất cả các dịch vụ khác đã được khởi tạo.

Để lưu output của chương trình (script) vào file log bạn có thể đổi ExecStart thành:

`ExecStart=/usr/bin/python /home/pi/sample.py > /home/pi/sample.log 2>&1`

Chọn permission cho unit file là 644 :

`sudo chmod 644 /lib/systemd/system/sample.service`

#### Step 2 – Cấu hình cho systemd

Sau khi đã định nghĩa file unit bạn có thể bật dịch vụ mình vừa mới tạo bằng lệnh sau:

>
   ` sudo systemctl daemon-reload`
    `sudo systemctl enable sample.service`


Reboot lại Raspberry Pi, lúc này chương trình của bạn sẽ được chạy khi khởi động:

```
sudo reboot
```


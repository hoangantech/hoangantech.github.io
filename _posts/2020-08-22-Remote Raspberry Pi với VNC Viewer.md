### Cài đặt VNC server trên Raspberry Pi

`sudo apt install realvnc-vnc-server realvnc-vnc-viewer`

### Cài đặt VNC Viewer trên máy tính (Windows, Mac, IOS, Android,...

Sau khi cài đặt xong, mở phần mềm VNC Viewer trên máy tính để truy cập vào Raspberry bằng địa chỉ IP nội bộ.
Sau đó đăng nhập với username và password (mặc định: pi và raspberry). Khi đó bạn đã remote được vào Raspberry qua mạng nội bộ.

![](/images/vnc1.PNG)
### Remote Raspberry Pi qua internet

Để remote raspberry qua internet, cần tạo tài khoản VNC miễn phí (có thể remote tối đa 5 máy).
Lúc này cả VNC Server (đang chạy trên Raspberry Pi) và VNC viewer đều phải đăng nhập cùng một tài khoản VNC.
 


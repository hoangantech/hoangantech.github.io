---
layout: post
author: Tien Cao-hoang
categories: [LoRa technology]
tag: LoRa
---
LoRa - Truyền nhận dữ liệu giữa Arduino và Raspberry Pi sử dụng LoRa


|Arduino Zero |Ra-02|
|-------------|-----|
|GND          |GND  |
|3.3V         |3.3V |
|D9           |RESET|
|D2           |DIO0 |
|D10          |NSS  |
|MOSI         |MOSI |
|MISO         |MISO |
|SCK          |SCK  |


|Raspberry Pi|	Lora Ra-02|
|------------|------------|
|3.3V	     |3.3V|
|Ground	     |Ground|
|GPIO 10	 |MOSI|
|GPIO 9	     |MISO|
|GPIO 11	 |SCK|
|GPIO 8	     |Nss / Enable|
|GPIO 4	     |DIO 0|
|GPIO 17     |DIO 1|
|GPIO 18	 |DIO 2|
|GPIO 27	 |DIO 3|
|GPIO 22	 |RST|

![](/images/rasp-pin.png)

### PyLoRa cho Raspberry Pi

Bài viết này chủ yếu là giao tiếp Peer to Peer giữa 2 module lora (Raspberry Pi và Arduino). Đối với Raspberry Pi sử dụng thư viện PyLoRa.

- Cấu hình cho Raspberry Pi

Mô đun LoRa Ra-02 kết nối với Raspberry Pi bằng chuẩn giao tiếp SPI, nên ta cần cấu hình cho Raspberry Pi bật giao tiếp SPI, sau  đó cài đặt  pylora package.

`sudo raspi-config

Di chuyến đến mục Interfacing Options sau đó enable SPI

- Kiểm tra pip và python đã được update

- Cài đặt RPi.GPIO

`pip install RPi.GPIO

package này giúp chúng ta điều khiển các chân GPIO của Raspberry Pi

- Cài đặt spidev
`pip install spidev

package này giúp điều khiển SPI

![](/images/lora_pip.JPG)

- Download và cài đặt  python-rpi.gpio package và spidev package

`sudo apt-get install python-rpi.gpio python3-rpi.gpio

`sudo apt-get install python-spidev python3-spidev



https://circuitdigest.com/microcontroller-projects/raspberry-pi-with-lora-peer-to-peer-communication-with-arduino
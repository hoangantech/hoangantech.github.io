---
layout: post
author: Tien Cao-hoang
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

https://circuitdigest.com/microcontroller-projects/raspberry-pi-with-lora-peer-to-peer-communication-with-arduino
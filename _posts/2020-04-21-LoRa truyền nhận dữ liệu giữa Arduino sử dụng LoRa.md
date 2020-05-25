---
layout: post
author: Tien Cao-hoang
categories: [LoRa technology]
tag: LoRa
---
LoRa - Truyền nhận dữ liệu giữa Arduino sử dụng LoRa

Arduino <-> Arduino

Sử dụng công nghệ LoRa, các thiết bị có thể giao tiếp trong phạm vi 13-20Km với khả năng đi xa tới 80KM khi cài đặt ở chế độ light-of-signt. Phạm vi này đạt được ở mức năng lượng rất thấp giúp LoRa phù hợp hơn các giao thức truyền thông khác, đối với các thiết bị IoT chạy bằng pin, từ xa, có khả năng chạy trong nhiều tháng (hoặc nhiều năm) trong một lần sạc pin.

![lora](/images/LoRa-COmpared-to-others.png)

LoRa có thể được sử dụng theo 2 phương án:

- Truyền thông Peer to peer

- Low Power Wide Area NetWork

Peer to peer cho phép 2 thiết bị có mô đun LoRa giao tiếp với nhau như cách hai thiết bị Bluetooth giao tiếp với nhau nhưng khoảng cách tăng đáng kể và mức tiêu thụ năng lượng thấp.

Để triển khai như một mạng diện rộng LPWAN. LoRaWAN là một chuẩn mạng công suất thấp, phạm vi rộng, dựa trên công nghệ LoRa.

![cấu trúc mạng LPWAN](/images/LoRaWAN-Network-Architecture.png) 

Demo này sử dụng giao tiếp Peer to Peer giữa hai thiết bị Arduino + mô đun LoRa Ra-02 Ai-Thinker

![Ra-02](/images/ra-02.png)

### Thiết bị sử dụng

1. Arduino Zero x 1

2. Arduino Leonardo x 1

3. Mô đun Lora Ra-02 x 2

### Mô tả

Trong demo này bao gồm 2 thiết bị gửi và nhận. Thiết bị gửi là Arduino Zero + Ra-02. Thiết bị nhận là Arduino Leonardo + Ra-02

### Nối dây

1. Thiết bị gửi

Arduino Zero được kết nối với mô đun Ra-02 qua chuẩn  giao tiếp ISP. Lưu ý đối với Arduino Zero các chân ISP phải được nối với header ICISP, không nối qua các chân 10, 11, 12, 13

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

2. Thiết bị nhận

Arduino Leonardo được kết nối với mô đun Ra-02 qua chuẩn  giao tiếp ISP.

|Arduino Leonardo |Ra-02|
|-------------|-----|
|GND          |GND  |
|3.3V         |3.3V |
|D9           |RESET|
|D2           |DIO0 |
|D10          |NSS  |
|MOSI         |MOSI |
|MISO         |MISO |
|SCK          |SCK  |

### Code

- Cài đặt library: Mở Arduino IDE -> vào Tool/library manager -> gõ từ khóa LoRa -> Cài đặt gói thư viện LoRa by Sandeep Mistry

![thu viện lora](/images/thu-vien-lora.PNG)

1. Code cho Lora sender (Thiết bị gửi)

~~~

#include <SPI.h>
#include <LoRa.h>

int counter = 0;

void setup() {
  SerialUSB.begin(9600); //code cho Arduino Zero

  SerialUSB.println("LoRa Sender");

// cài đặt tần số LoRa 433 MHz

  if (!LoRa.begin(433E6)) {
    SerialUSB.println("Starting LoRa failed!");
    while (1);
  }
}

void loop() {
  SerialUSB.print("Sending packet: ");
  SerialUSB.println(counter);

  // send packet
  LoRa.beginPacket();
  LoRa.print("hello ");
  LoRa.print(counter);
  LoRa.endPacket();

  counter++;

  delay(5000);
}

~~~

2. Code cho LoRa Receiver (thiết bị nhận)

~~~

#include <SPI.h>
#include <LoRa.h>

void setup() {
  Serial.begin(9600);
  while (!Serial);

  Serial.println("LoRa Receiver");

  if (!LoRa.begin(433E6)) {
    Serial.println("Starting LoRa failed!");
    while (1);
  }
}

void loop() {
  // try to parse packet
  int packetSize = LoRa.parsePacket();
  if (packetSize) {
    // received a packet
    Serial.print("Received packet '");

    // read packet
    while (LoRa.available()) {
      Serial.print((char)LoRa.read());
    }

    // print RSSI of packet
    Serial.print("' with RSSI ");
    Serial.println(LoRa.packetRssi());
  }
}

~~~

### Kết quả


![ket qua](/images/lora-ket-qua.PNG)




Arduino LowPower Library

Sleep mode cho phép người dùng dừng hoặc tắt một số mô đun trong Microcontroller để giảm điện năng tiêu thụ.
Arduino UNO, Arduino Nano and Pro-mini với ATmega328P có Brown-out Detector (BOD) (theo dõi điện áp ngõ vào khi ở chế độ sleep mode)

Có 6 chế độ sleep modes trong chip ATmega328P:

![](/images/Six-Sleep-modes-in-ATmega328P.png)

### Idle Mode

`LowPower.idle(SLEEP_8S, ADC_OFF, TIMER2_OFF, TIMER1_OFF, TIMER0_OFF, SPI_OFF, USART0_OFF, TWI_OFF);`

### ADC Noise Reduction Mode

Power-Down Mode

`LowPower.powerDown(SLEEP_8S, ADC_OFF, BOD_OFF); `

### Power-Save Mode

Standby Mode

Extended Standby Mode

## Refference
1. https://www.arduino.cc/en/Reference/LowPowerDeepSleep
2. https://circuitdigest.com/microcontroller-projects/arduino-sleep-modes-and-how-to-use-them-to-reduce-power-consumption
<center> <font size=10> User Manual for ESP-01s </font></center>

<center> from SZDOIT </center>

# 1. Introduction

ESP-12F WiFi module is a low-power and cost-effective embedded wireless network control module. It can meet the needs of Internet of Things applications such as smart grid, building automation, security, smart home, telemedicine and so on.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image002.jpg)

The core processor ESP8266 integrates the industry-leading Tensilica L106 ultra-low power 32-bit micro MCU with 16-bit streamlined mode, main frequency of 80 MHz and 160 MHz, supports RTOS, integrates Wi-Fi MAC/BB/RF/PA/LNA, and on-board antenna.

This module supports standard IEEE802.11 b/g/n protocol and complete TCP/IP protocol stack. Users can use this module to add networking functions to existing devices, or to build independent network controllers.

# 2. Main Features

# 2.1 Structure

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/esp-12f.jpg)

Figure Module Structure

# 2.2 Hardware parameters

* Operating voltage: 3.3V (3.0-3.6V)
* Work environment temperature: - 40 - 85 degrees C
* CPU Tensilica L106
  * RAM 50KB (available)
  * Flash 32Mbit
* System
* 802.11 b/g/n
* Frequency Range 2.4 GHz to 2.5 GHz (2400 MHz to 2483.5 MHz)
* Built-in Tensilica L106 ultra-low power 32-bit micro MCU with 16-bit streamlined mode, main        frequency support 80 MHz and 160 MHz
* RTOS support
* WIFI@2.4 GHz, supporting WPA/WPA2 security mode
* Support UART, I2C, GPIO, PWM, SDIO, SPI, ADC, PWM, IR
* Built-in 10 bit high precision ADC
* Support TCP, UDP, HTTP, FTP
* Built-in TR switches, balun, LNA, power amplifiers and matching networks
* Output power of + 20 dBm in 802.11b mode with built-in PLL, regulator and power management      module
* Average working current 80 mA, deep sleep holding current 20 uA, turn-off current less than 5        uA
* Can be used as application processor SDIO 2.0, SPI, UART
* Wake up, connect and transfer data packets within o 2ms
* Standby state power consumption is less than 1.0 mW (DTIM3)
* Support local serial port burning, cloud upgrade, host download burning
* Supporting Station/SoftAP/SoftAP+Station Wireless Network Mode

# 3 Pins Definition

# 3.1  Interface Definition

 

 

Table 2.2 Pins Function

| **pin**       **name** | **illustration** |                                                              |
| ---------------------- | ---------------- | ------------------------------------------------------------ |
| 1                      | RST              | reset                                                        |
| 2                      | ADC              | ADC , input voltage scope: 0 - 1V, value: 0 - 1024           |
| 3                      | EN               | Chip enabling high level:  effective, module working properly; low level: chip off, low current; |
| 4                      | IO16             | GPIO16；Wake up deep  sleep when receiving RST pins          |
| 5                      | IO14             | GPIO14；HSPI_CLK                                             |
| 6                      | IO12             | GPIO12；HSPI_MISO                                            |
| 7                      | IO13             | GPIO13； HSPI_MOSI；UART0_CTS                                |
| 8                      | VCC              | 3.3V  Power Supply (VDD) Note: The maximum output current of external power supply  is recommended to be more than 500 mA. |
| 9                      | CS0              | Chip selected                                                |
| 10                     | MISO             | Slave  output host input                                     |
| 11                     | IO9              | GPIO9                                                        |
| 12                     | IO10             | GPIO10                                                       |
| 13                     | MOSI             | Host  output slave input                                     |
| 14                     | SCLK             | Clock                                                        |
| 15                     | GND              | GND                                                          |
| 16                     | IO15             | GPIO15；MTDO；HSPICS；UART0_RTS                              |
| 17                     | IO2              | GPIO2；UART1_TXD                                             |
| 18                     | IO0              | GPIO0                                                        |
| 19                     | IO4              | GPIO4                                                        |
| 20                     | IO5              | GPIO5                                                        |
| 21                     | RXD              | UART0_RXD； GPIO3                                            |
| 22                     | TXD              | UART0_TXD；GPIO1                                             |

 

 

# 3.2 Shape and Size

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image005.jpg)

Fig 3.1 Shape of ESP-12F

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image007.jpg)

Fig. 3.2 Size for ESP-12F

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image009.jpg)

Table 3.1 Size for ESP-12F

 

| Length | Width | Height | PAD (two sides) | Pins distance |
| ------ | ----- | ------ | --------------- | ------------- |
| 24mm   | 16mm  | 3.15mm | 0.9 mm x 1.7mm  | 2.54mm        |

 

# 4. Function

# 4.1 MCU 

ESP8266EX built-in Tensilica L106 ultra-low power 32-bit micro MCU, with 16-bit streamlined mode, main frequency support 80MHz and 160MHz, support RTOS. At present, the WiFi protocol stack only uses 20% processing power, the rest can be used for application development. The MCU can work together with other parts of the chip through the following interfaces:

- Connect storage controllers, and can also be used to access the external Flash encoding RAM/ROM interface (iBus);

- Data RAM interface (dBus) connecting storage controller;

- The AHB interface of the access controller.


# 4.2 Store 

# 4.2.1 Built-in SRAM 与 ROM 

Based on the use of SRAM in Demo SDK, users can use the remaining SRAM space as follows:

- RAM < 50 kB (Heap + Data area can be approximately 50 kB after routing in Station mode).

- At present, there is no programmable ROM on ESP8266EX chip, and user programs are stored in SPI Flash.


# 4.2.2 SPI Flash 

- ESP8266EX chip supports external FLASH using SPI interface, and theory supports 16MB SPI Flash.

- ESP-01 module is equipped with 8Mbit SPI Flash, which can meet the needs of general customers.


# 4.3 Interface Definition

Table Interface definition

| **Interface** | **Pin**                                                      | **Illustrations**                                            |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SPI           | IO12(MISO),IO13(MOSI), IO14(CLK),IO15(CS)                    | It  can be used as a host to read and write SPI slave device, or as a slave to  communicate with external MCU. In overlap mode, you can share SPI pins with  Flash and switch through different CS |
| PWM           | IO12(R),IO15(G),IO13(B)                                      | Official  demo provides 4-way PWM (user-expandable 8-way), which can be used to control  color lights, buzzers, relays and motors. |
| IR            | IO14(IR_T), IO5(IR_R)                                        | The interface of IR  Remote Control is realized by software. The interface uses NEC coding and  modem, and uses 38KHz modulated carrier. |
| ADC           | TOUT                                                         | It  can be used to detect the supply voltage of VDD3P3 (Pin3, Pin4) and the input  voltage of TOUT (Pin6) (both can not be used simultaneously). It can be used in  sensor and other applications. |
| I2C           | IO14(SCL), IO2(SDA)                                          | External  sensors and display screens, etc.                  |
| UART          | UART0:   TXD(U0TXD),RXD(U0RXD)  ,IO15(RTS),IO13(CTS)         | Device  with External UART Interface  Download:  U0TXD + U0RXD or GPIO2 + U0RXD communication (UART0): U0TXD, U0RXD, MTDO  (U0RTS), MTCK (U0CTS) Debug: UART1_TXD (GPIO2) can be used as debug  information printing. |
|               | UART1:  IO2(TXD)                                             | UART0  will output some printing information by default when it is powered on  ESP8266-12S. For this sensitive application, the internal pin switching  function of UART can be used to exchange U0TXD and U0RXD with U0RTS and U0CTS  respectively during initialization. Hardware Connect MTDOMTCK to Serial Port  Import Communication of Corresponding External MCU |
| I2S           | I2S  input:  IO12 (I2SI_DATA);   IO13 (I2SI_BCK ); IO14  (I2SI_WS);   ![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image010.gif)  I2S output  IO15 (I2SO_BCK );   IO3 (I2SO_DATA);   IO2 (I2SO_WS ); | It  is mainly used for audio acquisition, processing and transmission. |



 

# 5. Electrical characteristics

## 5.1 Power Consumption

 

| Deep Sleep                                     | 20uA  |
| ---------------------------------------------- | ----- |
| Off                                            | 0.5uA |
| Normally  work(average)                        | 80mA  |
| Transmit   801.11b，CCK 11Mbps，Pout=+17 dBm   | 170mA |
| Transmit   801.11g，OFDM 54Mbps，Pout=+15 dBm  | 140mA |
| Transmit   801.11n，MCS7，Pout=+13 dBm         | 120mA |
| Transmit   801.11b，package 1024 byte，-80 dBm | 50mA  |
| Transmit  801.11g，package 1024 byte，-70 dBm  | 56mA  |
| Transmit   801.11n，package 1024 byte，-65 dBm | 56mA  |

**Note**

①: Modem-Sleep mode can be used for the case that CPU is always working, e.g., PWM or I2S etc. If WiFi is connected and no data is to transmitted, in this case, WiFi modem can be closed to save power energy. For example, if at DTIM3 status, keep asleep at 300ms, Then, the module can wake up to receive the Beacon package within 3ms and the current being 15mA.

②: Light-Sleep mode can used for the case that CUP can stop the application temporally, e.g., Wi-Fi Switch . If Wi-Fi is connected and there is no data packet to transmitted, by the 802.11 standard (e.g., U-APSD), module can close Wi-Fi Modem and stop CPU to save power. For example, at DTIM3, keep up sleeping at 300ms, it would receive the Beacon package from AP after each 3ms, then the whole average current is about 0.9mA.

③ Deep-Sleep mode is applied to the case that Wi-Fi is not necessary to connect all the time, just send a data packet after a long time (e.g., transmit one temperate data each 100s) . it just need 0.3s-1s to connect AP after each 300s, and the whole average current is much smaller 1mA.

# 5.2 RF  Features 

Table RF parameters

| **Item**                         | **Min** | **Classical**                   | **Max** | **Unite** |
| -------------------------------- | ------- | ------------------------------- | ------- | --------- |
| Input frequency                  | 2400    | /                               | 2483.5  | MHz       |
| Input impedance value            | /       | 50                              | /       | ohm       |
| Input reflection value           | /       | /                               | -10     | dB        |
| PA output power 72.2 Mbps        | 15.5    | 16.5                            | 17.5    | dBm       |
| 11b mode, PA output power        | 19.5    | 20.5                            | 21.5    | dBm       |
|                                  |         | **Sensitivity**                 |         |           |
| CCK，1Mbps                       | /       | -98                             | /       | dBm       |
| CCK，11Mbps                      | /       | -91                             | /       | dBm       |
| 6Mbps（1/2 BPSK）                | /       | -93                             | /       | dBm       |
| 54Mbps（3/4 64-QAM）             | /       | -75                             | /       | dBm       |
| HT20，MCS7（65Mbps，  72.2Mbps） | /       | -72                             | /       | dBm       |
|                                  |         | **Lead  frequency suppression** |         |           |
| OFDM，6Mbps                      | /       | 37                              | /       | dB        |
| OFDM，54Mbps                     | /       | 21                              | /       | dB        |
| HT20，MCS0                       | /       | 37                              | /       | dB        |
| HT20，MCS7                       | /       | 20                              | /       | dB        |

 

# 5.3 Digital Port Characteristics

| **Rating** **value** | **condition**       |              | **value** |      | **unite** |      |
| -------------------- | ------------------- | ------------ | --------- | ---- | --------- | ---- |
| Store temperature    | /                   | -40 to 125   | °C        |      |           |      |
| Max sold temperature | /                   | 260          | °C        |      |           |      |
| voltage              | IPC/JEDEC J-STD-020 | +3.0 to +3.6 | V         |      |           |      |
|                      |                     |              |           |      |           |      |

  

# 5.4 Digital Port Characteristics 

Table Digital Port Characteristics

| **port**                 | **classical**        | **min**      |      | **max**   | **unite** |      |
| ------------------------ | -------------------- | ------------ | ---- | --------- | --------- | ---- |
| Low input logic  level   | VIL                  | -0.3         |      | 0.25 VDD  | V         |      |
| High input  logic level  | VIH                  | 0.75 VDD     |      | VDD + 0.3 | V         |      |
| Low output  logic level  | VOL                  | N            |      | 0.1 VDD   | V         |      |
| High output  logic level | VOH                  | 0.8 VDD      |      | N         | V         |      |
| power                    | IPC/JEDEC  J-STD-020 | +3.0 to +3.6 | V    |           |           |      |
|                          |                      |              |      |           |           |      |

 

# 5.5 Ramp Up

Table ramp up

| **Interface**                                                | **Illustration**                   |
| ------------------------------------------------------------ | ---------------------------------- |
| Inclined heating rate（Ts Max. to TL）                       | max 3°C/s                          |
| Preheat  Min temperature （Ts Min.）  Classical temperature （Ts Typ.）  Max temperature（Ts Max.）  Time （Ts ） | 150°C   175°C   200°C   60 ~ 180 s |
| Inclined heating rate（TL to Tp）                            | Max  3°C/s                         |
| The above  duration：temperature （TL）/ time（TL）          | 270°C / 60 ~ 150 s                 |
| Temperature peak（Tp）                                       | Maximum  temperature 260 °C，10 s  |
| Target  temperature peak（Tp  target）                       | 260°C + 0 / -5°C                   |
| The duration  within the duration peak（Tp）5°C              | 20 ~ 40 s                          |
| Inclined  cooling rate（TsMax. To  TL）                      | Max  6°C / s                       |
| Time required  for peak modulation temperature from  25°C (t) | Max  8 minutes                     |

 

# 6. Schematic Diagram

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image013.jpg)

Figure ESP-12F Schematic Diagram

# 7. Minimum System

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image015.jpg)

Figure Minimum system

 Note

l The maximum output current of module IO is 12 mA.

l The typical value of module power supply is 3.3 V DC.

l Module low level reset is effective;

l Module firmware online upgrade needs to meet 3) conditions, IO0 pull down and reset module; after firmware upgrade is completed, IO0 is released.

l And reset module;

l RXD of module is connected with TXD of MCU, TXD of module is connected with RXD of MCU;

# 8. Peripheral Routing Suggestions

ESP-07 module can be welded to PCB board. In order to obtain the best RF performance of the terminal product, please pay attention to the reasonable design of the module and antenna placement on the bottom board in accordance with this guide.

# 9. Peripheral Routing Suggestions

 

ESP-01 integrates high-speed GPIO and peripheral interfaces, which may cause serious switching noise. If some applications are for power consumption and EMI features require higher requirements. It is recommended that 10 - 100 ohms of resistance be connected in series on digital I / O lines. This can suppress the overshoot and make the signal smooth when switching on the power supply. Series resistance can also prevent ESD to some extent.

 

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image017.jpg)

It is suggested that the module be placed along the edge of PCB board, and the antenna be placed outside or along the edge of the board and hollowed out below, with reference to scheme 1 and scheme 2.

PCB antenna is also allowed on the floor, as long as there is no copper under the antenna, reference scheme 3.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image019.jpg)

 Scheme 1: The antenna is outside the frame. 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image021.jpg) 

 Scheme 2: Antennas are placed along the edge of the plate and hollowed underneath.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image023.jpg)

Solution 3: Antennas are placed along the edge of the plate and not covered with copper underneath. 



# 10.  The Recommended Sold Temperature Curve

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESP12F/clip_image025.jpg)

Fig. 7.1 Temperature Curve when Sold

  # Contact Us

- E-mails: [yichone@doit.am](mailto:yichone@doit.am), [yichoneyi@163.com](mailto:yichoneyi@163.com)
- Skype: yichone
- WhatsApp:+86-18676662425
- Wechat: 18676662425
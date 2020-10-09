<center> <font size=10> User Manual for ESP-F </font></center>

 <center> from SZDOIT </center>

![clip_image030](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image030.jpg)

 **SOC characteristics**

* Built-in Tensilica L106 ultra-low power consumption 32-bit cpu, the main frequency can be 80MHz and 160MHz, also support RTOS;

* Built-in TCP/IP protocol stack;

* Built-in 1 channel 10-bit high precision ADC;

* The outside interfaces have HSPI, UART, I2C, I2S, IR Remote Control, PWM, GPIO;

* The deep-sleep current is about 10uA, and the cut-off current is smaller than 5uA;

* Can be wake-up within 2 ms, and connect to transmit data package;

* the consume power is smaller than 1.0mW (DTIM3) when at standby status;

  **Wi-Fi characteristics**

* Support 802.11 b/g/n/e/i

* Support three modes: Station, SoftAP, and SoftAP+STA;

* SupportWi-Fi Direct(P2P);

* Support hardware acceleration for CCMP (CBC-MAC, computation mode), TKIP (MIC, RC4), WAPI(SMS4), WEP(RC4), CRC;

* P2P find, P2P GO mode/GC mode and P2P power management;

* WPA/PA2 PSK and WPS;

* Support 802.11 i security: pre-certification and TSN;

* Support 802.11n (2.4 GHz);

* 802.1h/RFC1042 frame encapsulation;

* Support seamless roam; 

* Support AT remote updation and cloud OTA updation;

* Support SmartConfig function for Android and iOS device SmartConfig.


**Peripheral for Module**

* 2\*UART;

* 1\*En;

* 1\*ADC

* 1\*wakeup pin

* 1\*HSPI

* 1\*I2C

* 1\*I2S

* 4M byte Flash

* MAX 11\* GPIOs;

 **Working temperature:** -40℃-85℃

 **Module size**: 16mm*24mm;

 

**Applications**

* Serial Transparent transmission;              
* WiFi prober;
* Smart power plug/Smart LED light;          
* Mesh networks;
* Sensor networks;    

* Wearable electronics;

* Securit ID label;    

* Wireless location recognition;

* Wireless location system beacon; 

* Industrial wireless control.

**Module Type**

| Name  | Antenna Type         |
| ----- | -------------------- |
| ESP-F | PCB on board antenna |

**Module Structure**

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image002.gif)



 

# 1. Introduction

The WiFi module ESP-F is manufactured by using a high-performance chip ESP8266EX. This small chip is encapsulated an enhanced Tensilica’sL106 diamond series 32-bit kennel CPU with a SRAM. Thus, ESP8266 has the complete function Wi-Fi function; it not only can be applied independently, but can be used as a slaver working with other host CPU. When ESP8266 is applied as a slaver, it can start from the onboard Flash. The built-in high-speed buffer is not only benefit to improve the system performance, but optimize the store system. In addition, ESP8266 can be used as Wi-Fi adapter by SPI/SDIO or I2C/UART interface, when it is applied to other MCU design.

The ESP-F module supports the standard IEEE802.11 b/g/n/e/i protocol and the complete TCP/IP protocol stack. User can use it to add the WiFi function for the installed devices, and also can be viewed as a independent network controller. Anyway, ESP-F module provides many probabilities with the best price.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image003.gif)

 

Fig. 1.1Module Structure



Parameters for ESP-F are listed as follows.

Table 1.1 Parameters for ESP-F

| Types                      | Items                                     | Parameters                    |
| -------------------------- | ----------------------------------------- | ----------------------------- |
| Wi-Fi                      | Frequency scope                           | 2.4G~2.5G(2400M~2483.5M)      |
| Transmit power             | 802.11b: +20 dBm                          |                               |
| 802.11g: +17 dBm           |                                           |                               |
| 802.11n: +14 dBm           |                                           |                               |
| Receiving sensitivity      | 802.11b: -91 dbm (11Mbps)                 |                               |
| 802.11g: -75 dbm（54Mbps） |                                           |                               |
| 802.11n: -72 dbm（MCS7）   |                                           |                               |
| Antenna                    | PCB onboard antenna                       |                               |
| Hardware                   | CPU                                       | Tensilica L106 32 bit MCU     |
| Perpherl                   | UART/SDIO/SPI/I2C/I2S/IR  control         |                               |
| GPIO/ADC/PWM/SPI/I2C/I2S   |                                           |                               |
| Working voltage            | 2.5V ~ 3.6V                               |                               |
| Working current            | Average current: 80 mA                    |                               |
| Working temperature        | -40°C ~85°C                               |                               |
| Environment temperature    | -40°C ~ 85°C                              |                               |
| Size                       | 16mm x 24mm x 3mm                         |                               |
| Software                   | Wi-Fi mode                                | Station/SoftAP/SoftAP+Station |
| Security mode              | WPA/WPA2                                  |                               |
| Encryption type            | WEP/TKIP/AES                              |                               |
| Update firmware            | UART Download/OTA (by internet)           |                               |
| Software develop           | Non-RTOS/RTOS/Arduino IDE  etc.           |                               |
| Network protocol           | IPv4,  TCP/UDP/HTTP/FTP/MQTT              |                               |
| User configuration         | AT+ command/cloud sever/  Android/iOS APP |                               |

 

# 2. Interface Definition

 

Interface definition of ESP-F can be shown in the following.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image005.gif)

Fig. 2.1 ESP-F Definition for Pins

 

Working mode and definition of pins:

Table 2.1 Pin Modes

| Mode           | GPIO15 | GPIO0 | GPIO2 |
| -------------- | ------ | ----- | ----- |
| UART download  | low    | low   | high  |
| FlashBoot mode | low    | high  | high  |



Table 2.2 Function Definition of Module Pins



| Num  | Pin  | Type | Function                                                     |
| ---- | ---- | ---- | ------------------------------------------------------------ |
| 1    | RST  | I    | Reset the signal outside (enable with low), Reset module     |
| 2    | ADC  | I    | A/D pin.  Input voltage 0~1V,   value: 0~1024                |
| 3    | EN   | I    | Enable, high level: chip work normally; low level: chip closes with small  current. |
| 4    | IO16 | I/O  | deep sleep/wakeup                                            |
| 5    | IO14 | I/O  | GPIO14; HSPI_CLK                                             |
| 6    | IO12 | I/O  | GPIO12;HSPI_MISO                                             |
| 7    | IO13 | I/O  | GPIO13;HSPI_MOSI;UART0_CTS                                   |
| 8    | VCC  | P    | Module working voltage: 3.3V                                 |
| 9    | CS0  | I/O  | GPIO11; SD_CMD; SPI_CS0                                      |
| 10   | MISO | I/O  | GPIO7; SD_D0, SPI_MSIO                                       |
| 11   | IO9  | I/O  | GPIO9; SD_D2 PIHD; HSPIHD                                    |
| 12   | IO10 | I/O  | GPIO10; SD_D3;SPIWP; HSPIWP1                                 |
| 13   | MOSI | I/O  | GPIO8; SD_D1;SPI_MOSI1                                       |
| 14   | SCLK | I/O  | GPIO6; SD_CLK; SPI_CLK                                       |
| 15   | GND  | P    | GND                                                          |
| 16   | IO15 | I/O  | GPIO15; MTDO;HSPICS;UART0_RTS                                |
| 17   | IO2  | I/O  | GPIO2; UART1_TXD                                             |
| 18   | IO0  | I/O  | GPIO0;SPI_CS2                                                |
| 19   | IO4  | I/O  | GPIO4                                                        |
| 20   | IO5  | I/O  | GPIO5                                                        |
| 21   | RXD  | I/O  | GPIO3; used to build  in Flash as UART Rx                    |
| 22   | TXD  | I/O  | GPIO1; used to build in Flash as UART Tx                     |

  

# 3. Shape and Size

 

Shape and size for this module can be shown as follows. Its size is 16mm\*24mm\*3mm, and the Flash is 4M bytes (32Mbits).

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image007.jpg)
![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image009.jpg)

 

Fig. 3.1 Shape for ESP-F

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image011.jpg)

(a) Vertical View

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image013.jpg)

(b) Side View

Fig. 3.2 Size for ESP-F

 

Table 3.1Size for ESP-F

 

| Length | Width | Height | Pin  | Distance between Pins |
| ------ | ----- | ------ | ---- | --------------------- |
| 24.5mm | 14mm  | 3mm    | 4 x2 | 2.54                  |

# 4. Electronical Characteristics

 

Table 4.1 Electronics

| Parameters                                    | Condition            | Min      | Classical    | Max      | Unite       |      |
| --------------------------------------------- | -------------------- | -------- | ------------ | -------- | ----------- | ---- |
| Store  Temperature                            | -                    | -40      | Normal       | 125      | ℃           |      |
| Sold  Temperature                             | IPC/JEDEC  J-STD-020 | -        | -            | 260      | ℃           |      |
| Working  Voltage                              | -                    | 2.5      | 3.3          | 3.6      | V           |      |
| I/O                                           | VIL/VIH              | -        | -0.3/0.75VIO | -        | 0.25VIO/3.6 | V    |
| VOL/VOH                                       | -                    | N/0.8VIO | -            | 0.1VIO/N |             |      |
| IMAX                                          | -                    | -        | -            | 12       | mA          |      |
| Electrostatic  release quantity (Human model) | TAMB=25℃             | -        | -            | 2        | KV          |      |
| Electrostatic  release quantity (Human model) | TAMB=25℃             | -        | -            | 0.5      | KV          |      |

 

# 5. Power Consumption

Table 5.1 Power Consumption

| Parameters                             | Min  | Classical | Max  | Unite |
| -------------------------------------- | ---- | --------- | ---- | ----- |
| Tx802.11b, CCK 11Mbps,  POUT=+17dBm    | -    | 170       | -    | mA    |
| Tx802.11g, OFDM 54 Mbps,  POUT =+15dBm | -    | 140       | -    | mA    |
| Tx802.11n,MCS7,POUT =+13dBm            | -    | 120       | -    | mA    |
| Rx 802.11b，1024 Bytes,  -80dBm        | -    | 50        | -    | mA    |
| Rx 802.11g，1024 Bytes,  -70dBm        | -    | 56        | -    | mA    |
| Rx 802.11n，1024 Bytes,  -65dBm        | -    | 56        | -    | mA    |
| Modem-sleep①                           | -    | 15        | -    | mA    |
| Light-sleep②                           | -    | 0.9       | -    | mA    |
| Deep-sleep③                            | -    | 20        | -    | μA    |
| close                                  | -    | 0.5       | -    | μA    |

 

**Note**

①: Modem-Sleep mode can be used for the case that CPU is always working, e.g., PWM or I2S etc. If WiFi is connected and no data is to transmitted, in this case, WiFi modem can be closed to save power energy. For example, if at DTIM3 status, keep asleep at 300ms, Then, the module can wake up to receive the Beacon package within 3ms and the current being 15mA.

②: Light-Sleep mode can used for the case that CUP can stop the application temporally, e.g., Wi-Fi Switch . If Wi-Fi is connected and there is no data packet to transmitted, by the 802.11 standard (e.g., U-APSD), module can close Wi-Fi Modem and stop CPU to save power. For example, at DTIM3, keep up sleeping at 300ms, it would receive the Beacon package from AP after each 3ms, then the whole average current is about 0.9mA.

③ Deep-Sleep mode is applied to the case that Wi-Fi is not necessary to connect all the time, just send a data packet after a long time (e.g., transmit one temperate data each 100s) . it just need 0.3s-1s to connect AP after each 300s, and the whole average current is much smaller 1mA.

# 6. Wi-Fi RF Characteristics

The data in the following Table is gotten when voltage is 3.3V and1.1V in the indoor temperature environment. 

 

Table 6.1 Wi-Fi RF Characteristics

| Parameters                                    | Min  | Classical | Max  | Unite |
| --------------------------------------------- | ---- | --------- | ---- | ----- |
| Input  frequencey                             | 2412 | -         | 2484 | MHz   |
| Input  impedance                              | -    | 50        | -    | Ω     |
| Input reflection                              | -    | -         | -10  | dB    |
| At 72.2Mbps,  output power consumption for PA | 15.5 | 16.5      | 17.5 | dBm   |
| At  11b mode, output power consumption for PA | 19.5 | 20.5      | 21.5 | dBm   |
| Sensibility                                   | -    | -         | -    | -     |
| DSSS,  1Mbps                                  | -    | -98       | -    | dBm   |
| CCK11,  Mbps                                  | -    | -91       | -    | dBm   |
| 6Mbps(1/2  BPSK)                              | -    | -93       | -    | dBm   |
| 54Mbps(3/4  64-QAM)                           | -    | -75       | -    | dBm   |
| HT20,  MCS7(65 Mbps, 72.2 Mbps)               | -    | -72       | -    | dBm   |
| Adjacent  Inhibition                          |      |           |      |       |
| OFDM,  6Mbps                                  | -    | 37        | -    | dB    |
| OFDM,  54Mbps                                 | -    | 21        | -    | dB    |
| HT20,  MCS0                                   | -    | 37        | -    | dB    |
| HT20,  MCS7                                   | -    | 20        | -    | dB    |

 

# 7.  The Recommended Sold Temperature Curve

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image015.jpg)

Fig. 7.1 Temperature Curve when Sold

 

 

 

# 8. Schematics for ESP-F

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image017.jpg)

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image019.jpg)

Fig. 8.1 Schematics for ESP-F

# 9. Minimum System

 

This module can work just at 3.3V working voltage.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image021.jpg)

Fig.9.1 Minimum System

 

**Note**

(1) the working voltage for module is DC 3.3V;

(2) the max current from IO of this module is 12mA;

(3) RST Pin is enabled when it is low level; and EN pin is enabled when it is high level;

(4) WiFi module is at update mode: GPIO0 is low level, then module reset to power; Wi-Fi module is at working mode: GPIO0 is at high level, and then reset to power; 

(5) Wi-Fi module is connected to RXD of the other MCU, and TXD is connected to RXD of the other MCU.



# 10. The Recommended PCB Design

Wi-Fi module can be inserted into the PCB board directly. For the high RF performance for the end device, please note the placement for the antenna and the module. 

  It is suggested that the module is placed along with PCB side, the antenna is placed outside the board, or along with the PCB side, and the below board is blank, please refer to the scheme 1 and scheme 2; if the PCB antenna must placed on the board, please do not cover the copper at the bottom of PCB antenna, as can be shown at scheme 3.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image023.gif)

Fig. 10.1 scheme1: Antenna is at the outside of the board

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image025.gif)

Fig. 10.2 Scheme 2: Antenna is placed along with side of the board, and it is blank at the bottom of the board.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPF/clip_image027.gif)

Fig. 10.3 Scheme 3: Antenna is placed along with the side of the board, and don’t cover copper under the module

 

# 11. Peripheral Line Suggestion

Wi-Fi module is already integrated into high-speed GPIO and Peripheral interface, which may be generated the switch noise. If there is a high request for the power consumption and EMI characteristics, it is suggested to connect a serial 10~100 ohm resistance, which can suppress overshoot when switching power supply, and can smooth signal. At the same time, it also can, to a certain extent, prevent electrostatic discharge (ESD).

# Contact Us

- Email: yichoneyi@163.com
- WhatsApp: 008618676662425
- WeChat: itchenve
- Skype: yichone
- Online Shop: [vvdoit](https://www.vvdoit.com/), [SpoSmart](https://www.sposmart.com/)

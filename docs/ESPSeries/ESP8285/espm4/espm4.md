<center> <font size=10> User Manual for ESP-M4 </font></center>

<center> from SZDOIT </center>

# **Features**

##  **SOC characteristics**

* Built-in Tensilica L106 ultra-low power consumption 32-bit cpu, the main frequency can be 80MHz and 160MHz, also support RTOS;
* Built-in TCP/IP protocol stack;
* Built-in 1 channel 10-bit high precision ADC;
* The outside interfaces have HSPI, UART, I2C, I2S, IR Remote Control, PWM, GPIO;
* The deep-sleep current is about 10uA, and the cut-off current is smaller than 5uA;
* Can be wake-up within 2 ms, and connect to transmit data package;
* the consume power is smaller than 1.0mW (DTIM3) when at standby status;
* built-in 1M byte for SPI Flash.
##  **Wi-Fi characteristics**
* Support 802.11 b/g/n/e/i
* Support three modes: Station, SoftAP, and SoftAP+STA;
* Support Wi-Fi Direct(P2P);
* Support hardware acceleration for CCMP (CBC-MAC, computation mode), TKIP (MIC, RC4), WAPI(SMS4), WEP(RC4), CRC;
* P2P find, P2P GO mode/GC mode and P2P power management;
* WPA/PA2 PSK and WPS;
* Support 802.11 i security: pre-certification and TSN;
* Support 802.11n (2.4 GHz);
* 802.1h/RFC1042 frame encapsulation;
* Support seamless roam; 
* Support AT remote updation and cloud OTA updation;
* Support SmartConfig function for Android and iOS device SmartConfig.

## **Peripheral for Module**

* 2\*UART;

* 1\*En;

* 1\*ADC;

* 1\*wakeup pin;

* 1\*HSPI;

* 1\*I2C;

* 1\*I2S;

* MAX 10\* GPIOs;

 **Working temperature:** -40℃-125℃

 **Module size**: 

* 12.3*mm*15mm; (M1 version)

* 12.3*mm*20mm; (M2 version)

## **Application**

* Serial Transparent transmission;               

* Smart power plug/Smart LED light;            

* Sensor networks;    

* Wearable electronics;

* Securit ID label;    

* Wireless location recognition;

* Wireless location system beacon; 

* Industrial wireless control.
* WiFi prober;
* Mesh networks;

## **Module Type**

| Name   | Antenna Type         |
| ------ | -------------------- |
| ESP-M4 | PCB on board antenna |
|        |                      |



# 1. Introduction

The WiFi module ESP-M is manufactured by using a high-performance chip ESP8285. This small chip is encapsulated an enhanced Tensilica’s L106 diamond series 32-bit kennel CPU with a SRAM. Thus, ESP8285 has the complete function Wi-Fi function; it not only can be applied independently, but can be used as a slaver working with other host CPU. When ESP8285 is applied as a slaver, it can start from the onboard Flash. The built-in high-speed buffer is not only benefit to improve the system performance, but optimize the store system. In addition, ESP8285 can be used as Wi-Fi adapter by SPI/SDIO or I2C/UART interface, when it is applied to other MCU design.

The ESP-M module supports the standard IEEE802.11 b/g/n/e/i protocol and the complete TCP/IP protocol stack. User can use it to add the WiFi function for the installed devices, and also can be viewed as a independent network controller. Anyway, ESP-M module provides many probabilities with the best price.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image004.gif)

 

Fig. 1.1 Module Structure



**The main parameters can be shown as follows.**

Table 1.1  Parameters 

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
| Working temperature        | -40°C ~125°C                              |                               |
| Environment temperature    | -40°C ~ 125°C                             |                               |
| Size                       | 16mm x 24mm x 3mm                         |                               |
| Software                   | Wi-Fi mode                                | Station/SoftAP/SoftAP+Station |
| Security mode              | WPA/WPA2                                  |                               |
| Encryption type            | WEP/TKIP/AES                              |                               |
| Update firmware            | UART Download/OTA (by  internet)          |                               |
| Software develop           | Non-RTOS/RTOS/Arduino IDE  etc.           |                               |
| Network protocol           | IPv4, TCP/UDP/HTTP/FTP/MQTT               |                               |
| User configuration         | AT+ command/cloud sever/  Android/iOS APP |                               |

# 2.  Interface Definition

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image006.jpg)

Fig. 2.1 Pins of ESP-M4

 

Working mode and definition of pins:

 

Table 2.1 working modes

| Mode          | GPIO0 | GPIO2(Pull-up  resistance) |
| ------------- | ----- | -------------------------- |
| UART download | low   | high                       |
| Flash Boot    | high  | high                       |



 

Table 2.2 Pins Function

| Num   | Pin Name | Type | Function Illustration                                        |
| ----- | -------- | ---- | ------------------------------------------------------------ |
| 1     | IO16     | I/O  | GPIO16, wake up from deep sleep                              |
| 2     | GND      | P    | GND                                                          |
| 3,18  | IO0      | I/O  | Selected pin for module download                             |
| 4,14  | VCC      | P    | Power: 3.3V/250mA                                            |
| 5,15  | IO14     | I/O  | GPIO14;                                                      |
| 6     | IO12     | I/O  | GPIO12;                                                      |
| 7     | IO13     | I/O  | GPIO13;                                                      |
| 8     | IO5      | I/O  | IO5;                                                         |
| 9,17  | RXD      | I/O  | GPIO3; used to  built-in Flash as  UART Rx                   |
| 10    | IO4      | I/O  | IO4;                                                         |
| 11,16 | TXD      | I/O  | GPIO1; used  to built-in Flash as  UART Tx                   |
| 12    | IO15     | I/O  | IO15, pull-down, has 100us high level after  power, unsuitable for relay control |
| 13    | RST      | I    | Reset(effective for low level) with pull-up resistance       |

 

# 3. Shape and Size

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image008.jpg)

Fig 3.1 Shape of ESP-M4

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image010.jpg)

Fig. 3.2 Size for ESP-M4

 

Table 3.1 Size for ESP-M4

 

| Length  | Width   | Height | PAD (two sides) | PAD  (bottom) |
| ------- | ------- | ------ | --------------- | ------------- |
| 21.44mm | 18.06mm | 2.3mm  | 0.9 mm x 1.3mm  | 1.5mm*3.1mm   |

 



 



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
| Input  reflection                             | -    | -         | -10  | dB    |
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

 

 

 



# 7. The Recommended Sold Temperature Curve

 

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image012.jpg)

Fig. 7.1 Temperature Curve when Sold

 

 



 

# 8. Minimum System

This module can work just at 3.3V working voltage.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image014.jpg)

Fig. 8. 1 Minimum System

 

**Note**

(1) the working voltage for module is DC 3.3V;

(2) the max current from IO of this module is 12mA;

(3) RST Pin is enabled when it is low level; and EN pin is enabled when it is high level;

(4) WiFi module is at update mode: GPIO0 is low level, then module reset to power; Wi-Fi module is at working mode: GPIO0 is at high level, and then reset to power; 

(5) Wi-Fi module is connected to RXD of the other MCU, and TXD is connected to RXD of the other MCU.

**
**

# 9. The Recommended PCB Design

Wi-Fi module can be inserted into the PCB board directly. For the high RF performance for the end device, please note the placement for the antenna and the module. 

Especially, since the antenna is external for ESP-M1, the antenna can be placed by the project requirements. The connector for external antenna is shown in the following.

![img](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8285/espm4/clip_image016.jpg)

Fig. 9. 1 Connector for the external antenna

 

  It is suggested that the module is placed along with PCB side, the antenna is placed outside the board, or along with the PCB side, and the below board is blank.



# 10. Peripheral Line Suggestion

Wi-Fi module is already integrated into high-speed GPIO and Peripheral interface, which may be generated the switch noise. If there is a high request for the power consumption and EMI characteristics, it is suggested to connect a serial 10~100 ohm resistance, which can suppress overshoot when switching power supply, and can smooth signal. At the same time, it also can, to a certain extent, prevent electrostatic discharge (ESD).



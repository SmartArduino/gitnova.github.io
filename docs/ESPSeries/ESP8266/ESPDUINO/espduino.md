<center> <font size=10> User Manual for ESPduino </font></center>

<center> from SZDOIT </center>


# 1. Introduction

ESPduino is developed by Doit company based on the ESP8266 ESP-13, which can be compatible with Arduino UNO R3 developmen board; i.e., ESPduino=WiFi+Arduino UNO R3.
By using the ESP8266 WiFi Chip and MCU, ESPduino can work with the support of WiFi. Compared to the traditional Arduino UNO development baord, users don't have to buy another WiFi development board when developing some WiFi applications. Now, This ESPduino can be gotten by [the link](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPDUINO/http://www.smartarduino.com/view.php?id=94894) from [vvdoit](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPDUINO/www.vvdoit.com). ESPduino is shaped by the following Figure.

![espduino](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPDUINO/espduino.jpg)

# 2. Features

- Compatible with Arduino UNO R3;
- With WiFi;
- with chip ESP8266;
- [schematics pdf](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPDUINO/https://github.com/SmartArduino/ESPboard/blob/master/espduino_shematic.pdf)

# 3. Download IDE and Drivers

**(1) Download the compatible-Arduino IDE**

http://en.doit.am/espduino.php, or

https://github.com/esp8266/Arduino/

and install it.

**(2) Install the CH340 chip driver by the following choices.**

- **Widowns & MAC**

http://bbs.smartarduino.com/showthread.php?tid=2038

- **Ubuntu**

[https://github.com/esp8266/Arduino%20for%20Ubuntu](https://github.com/SmartArduino/document/raw/master/docs/ESPSeries/ESP8266/ESPDUINO/https://github.com/esp8266/Arduino for Ubuntu)

(3) After installation of Arduino and CH340 driver. Open the Arduino IDE, and choose the development board type " ESPDuino (ESP-13 module) ".

Note that, if you get the **new version** ESPduino (order it after Sep. 30, 2016), please further confirm whether the "Reset Method" is "ESPduino-V2" (which is also the default setting); if you get the **old version** (order it before Sep. 30, 2016), please choose the "Reset Method" is "ESPduino-V1".

# 4. How to Use

This section is just for the installation and use the Arduino IDE, and download the code into the ESPduino development board. Especially, for convenience, we have already improved the ESPduino since Sep. 30, 2016, and now you DO NOT need to press any button, when you download the code. Note that, the old version must press the button when download the code.

If you order this board after Sep. 30, 2016, then don't need to press any button, but the old version still need to press the button. About the new version, to download the code, just by the following two methods:

(1) Change the **boards.txt** file.

Search the **boards.txt** file within the installation Arduino files in your PC by using the txt file downloaded in the following link: http://8266.doit.am/boards.txt, and then, you can choose the board type as "**ESPduino (ESP-13 Module)**", and the "**Reset Method**" is "**ESPduino-V2**".

(2) Select the development board type as "**Generic ESP8266 Module**", and choose the " **Reset Method**" as "**nodemcu**", as shown in the following picture. Then you can download the code into the board.

(3) Test the Arduino IDE

After building the Arduino IDE, we should test whether the Arduino IDE for ESPduino board is normal by a example, the Blink, which is provided by the standard Arduino IDE.

If it is successful, then the Arduino IDE for ESPduino IDE is ok.

# In Summary

- Download the right software by the given links;
- Install the CH340 driver;
- Choose the development board type as "ESPduino(ESP-13 module)";
- Confirm whether the "Reset Method" is "ESPduino-V2" OR "ESPduino-V1";
- Test the Arduino IDE for ESPduino development board.



# Contact Us

- E-mails: [yichone@doit.am](mailto:yichone@doit.am), [yichoneyi@163.com](mailto:yichoneyi@163.com)
- Skype: yichone
- WhatsApp:+86-18676662425
- Wechat: 18676662425
<center><font size=10>W600 Arduino Getting Started Guide</center></font>
<center> From SZDOIT</center>

# 1. Introduction

[Arduino](https://baike.baidu.com/item/Arduino) is a convenient, flexible and easy to use open source electronic prototype platform. Now, W600 chip can directly support the development of Arduino environment. Developers can use familiar Arduino functions and libraries to write code and run directly on W600 without external microcontroller. Make it easier for developers to design products.

# 2. Preparation

-  -1 x W600 development board ([TB-01](http://shop.thingsturn.com) is recommended)
-  -1 × Micro USB B cable
-  -1 × PC (currently only available in Windows environment)

# 3. Environment setup

1. Download the Arduino IDE development environment through https://www.arduino.cc/en/Main/Software. It is recommended to use the latest version.
2. Start Arduino and open the "Preferences" window. Add `http://arduino.w600.fun/package_w600_index.json` in the URL of the additional development board manager
   ![](1556334078542.png)
3. Open the menu [Tools]-"[Development Board]-"[Development Board Manager]

![1556334412321](1556334412321.png)

4. Fill in the keyword `w600` in the input box, select the latest version (`currently 0.2.4`), click [install]

![1556334650002](1556334650002.png)

![1556335438851](1556335438851.png)

5. Select the TB-01 development board and configure the development board parameters (pay attention to selecting the correct communication port and rate)
   ![1556335475972](1556335475972.png)

**Port: **You can check the computer device manager for correspondence

**Upload Speed: **The communication speed during programming, the default is 2Mbps, if the download fails, you can choose 115200.

**Upload Files: **Download file format (default is IMG, if download fails or needs to update secboot, select FLS)

 ![](28194943723.jpeg)

6. Select [File]-"[Examples], you can try some examples for burning test, such as [Blink]

   ![1556335587121](1556335587121.png)

7. Click Upload to download the firmware

   ![1556438775082](1556438775082.png)

8. The effect after running is as follows

![1556415104023](1556415104023.png)

 At the same time, you can see that the indicator light on the development board is constantly flashing.
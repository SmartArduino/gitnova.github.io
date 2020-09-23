<center> <font size=10> User Manual for HomeKit of Relay </font></center>

<center> from SZDOIT </center>

# 1. Introduction

![IMG_0476](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image002.jpg)

| name             | HomeKit relay switch Development  board |
| ---------------- | --------------------------------------- |
| size             | 30mm * 30mm * 15mm                      |
| weight           | 13.5g                                   |
| Working voltage  | 5V                                      |
| Working current  | 150mA                                   |
| Relay DC voltage | 30V                                     |
| Relay DC current | 5A                                      |
| Relay AC voltage | 250V                                    |
| Relay AC current | 10A                                     |



# **2.**   Hardware

**pins**

there are 8 pcs pins from this board, as shown in the following picture. From left to right: 

\1. MODE for download, 

\2. MODE for download, 

\3. RX, 

\4. TX

\5. 5V,

\6. GND

\7. BUTTON

\8. BUTTON

![IMG_0466_WPS图片](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image004.jpg)

**About relay**

The relay controls two outputs (as shown in the following picture): when the relay is powering, interfaces 1 and 2 are closed, and the relay is off power, then this two interfaces are off.

![IMG_0472_WPS图片](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image006.jpg)

**Button**

If need the out-connected button to control the relay, then can connected a button at pins 7 and 8.

**Download Mode**

If you want to download the firmware, please use jumper cap to pins 1 and 2, then connected the pins RX and TX, respectively. One can download the firmware to the board.

**How to reset to factory mode**

Short the pins 7 and 8 by using a jumper cap or other tools.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image008.jpg)

 

# **3.**  How to Use the Homekit

The default mode of the device is homekit.

 

**HomeKit (ONLY for Apple users):**

Step 1: Please open the WLAN setting page of your iPhone (as Fig. 1), find and connect the WiFi hotspot named as Homekit_xxxx. After about 3s, WiFi configuration interface will pop up automatically.

Note: If the interface doesn’t pop up automatically, please open your phone browser and input http://192.168.4.1. And then, please wait for entering the interface of configuration.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image010.jpg)

 

 

Fig.1 Connect your iPhone or iPad to the new wifi network Homekit_xxxx hotspot

Step 2: Wait for the Captive Portal and select your WiFi network in the pop-up window, and insert your password and click “join” (as Fig. 2). Please make sure that the indicator always lights (the WiFi account information in the pictures is only for reference).

Note: If you don't find your router or smart plug at other states. Please look over the Frequent Problems and reconfigure the smart socket.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image012.jpg)

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image013.png)

Fig. 2 Wait for the Captive Portal and select your WiFi network

Step 3: Please check if you have installed Home APP.

If not, please download it in the App Store. (as Fig. 3). If it is already installed, go to step 4.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image015.jpg)

Fig. 3 Download the Home App

Step 4: Please connect your phone with your home WiFi network (as Fig. 4)

Note: Please ensure that the IPhone and the smart plug are in the same network.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image017.jpg)

 

 

 

Fig. 4 Connect your phone with your home WiFi network

 

Step 5: 

1)Open the Home app

 2)Click the + symbol

 3)Click I don't have the code.

 4) Select the Switch-xxx. When the Switch-xxx does not appear on top of the page, if you have a dual-band router, please turn off the 5GHZ Wi-Fi network and ensure that yu are using 2.4GHz Wi-Fi network.

 5)Confirm that you want to add the device

 6)Insert the Password that is 12345678

 7) After waiting for the encryption check (about 30s-50s), you have added the switch successfully. Please rename the smart device for convenient operation in the later, and enjoy it.

![5](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image019.jpg)

![IMG_256](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image021.jpg)

![IMG_256](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image023.png)

![clip_image025](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image025.jpg)

![clip_image027](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image027.jpg)

![clip_image029](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image029.png)

![IMG_256](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image031.png)![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/file:///C:/Users/ADM

![clip_image033](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image033.jpg)

Fig. 4 How to Pair HomeKit

 

Step 6: if you only use the homekit function, this is all. If you use timer, remote control, Alexa, Google assistant, please download the dohome app by scanning the code.

 

**For DoHome Model:**

If there is no IOS device, you need to switch the smart socket device to **DoHome** model.

Step 1: Please power on the plug and check that the indicator light is blinking slowly (1 time every second). Long press the button of smart plug for 5s and observe that the indicator light blinks quickly (10 times every second).

Step 2: Use your phone to scan the following QR code and download DoHome APP.

![clip_image035](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image035.jpg)

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image037.jpg)

 

Step 3: Open DoHome APP, register your account using your name and password, and then login the DoHome APP.

 

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image039.jpg)

 

 

Step 4: Click the“+”in the upper right corner to add the device according to the hint.

Note: If you still have a doubt, please click the menu in the upper right corner to look for help.

 ![clip_image041](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image041.jpg)

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image043.jpg)![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/file:///

 ![clip_image045](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image045.jpg)

 

Step 5: If want to use the smart speaker, e.g., Alexa, google assistant, Tmall or Xiaomi, please click the“≡”in the upper right corner to look for the corresponding instructions.

 

 

Frequent Problems

Q1: How do Homekit users use timer, remote control and smart audio devices such as Alexa, Google Assistant, Tmall genie or XiaoMi audio. 

\1. Scan the QR code in the following and download DoHome APP.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image046.jpg) 

 ![clip_image048](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image048.jpg)

\2. Register and login your account information of DoHome. Pull down and refresh the interface to look for your smart device.

Note: The phone and the smart plug must be connected in the same WiFi network.

 ![clip_image049](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image049.jpg)

!![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image050.jpg)![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/file:///C:/Users/AD

![clip_image051](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image051.jpg)

\3. Please open the menu in the upper left corner, click “Manager” and find your device. And then, choose it and click “Bind device”. 

Note: (1). You must login the 3rd platform to login your DoHome account before using it.

(2). If you want to use the smart audio, please click the corresponding icon to check the user manual. If you need help, please click the option of help; 

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image052.jpg)

 ![clip_image053](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image053.jpg)

![clip_image055](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image055.jpg)

![clip_image057](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image057.jpg)

![clip_image059](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image059.jpg)

Q4: How to reset the socket to the factory mode?

A: Long press the button of the smart plug (5s) and the indicator light will blink slowly.

 

# 4 How to Update the firmware by ourself

Firmware and download tool:

 https://github.com/SmartArduino/DoHome/tree/master/DoHome_HomeKit_Firmware

 

Step 1: download the tool named as flash_download_tools

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image060.png)

 

Step 2: select the plug folder on the interface, click enter to download the latest version of the development board firmware to the local. Select the bootloader folder on the interface and click enter to download the boot firmware of the development board to the local.

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image062.jpg)

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image064.jpg)

Step 3: after the firmware and tools are downloaded to the local area, double-click to open the flash download tools tool, select the type of development board download tool as esp8285 download tool, open the tool, select the relevant firmware, and the download address of the firmware is as shown in the right figure (Note: only one of them needs to be downloaded for U1 and U2, and the address cannot be interchanged)

![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image066.jpg) 

![clip_image068](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image068.jpg)

Step 4: after connecting the development board to the PC, select the appropriate serial port, fill in the correct firmware and download address, and then use the shorting cap to short connect the 1 and 2 mode pins to enter the download mode. Then use the download tool to connect the 5V power pin, GND pin, RX pin and TX pin respectively. Click the start button to complete the download, as shown in the figure on the right below is the rendering of the successful download.

![clip_image069](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image069.png)

​     ![img](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/homekit2relay/clip_image070.png)

 

 

 

 

 

 
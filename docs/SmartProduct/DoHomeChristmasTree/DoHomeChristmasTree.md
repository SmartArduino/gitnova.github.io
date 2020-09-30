# DoHome Christmas Tree

# ***1. Product Introduction***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree0.jpg)

The software and hardware of this product are independently developed by our company. It supports multiple control modes such as voice, hardware, and software. There are 56 fixed lighting effects and microphone dynamic lighting effects.Therefore, the product is colorful. 

We uses NodeMcu as the control module of the product, simple and applicable which is very suitable for DIY.

# ***2. Burning Program*** 

Download The official download tool flash_download_tool_v3.8.5: https://www.gitnova.com/software-tools/

Unzip it after downloading

①　Double click to open flash_download_tool_v3.8.5.exe
![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree2.jpg)

②　Select Developer Mode

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree3.jpg) 

③select ESP8266 DownloadTool

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree4.jpg) 

④　Set the parameters and port number, click START to download

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree5.jpg) 

# **3.** Control Instructions

## ***3.1*** ***Instructions For Hardware Configuration***

The hardware is designed to be controlled by pressing the Flash button on the NodeMCU. There are 56 light switching modes. The specific operation methods are as follows:

### 3.11.Short press the button once to switch the fixed lighting effect

If you continue to press the key within 5 seconds, then the item continues to switch to the next mode,

If you press the key after 5 seconds, the Christmas lights will be turned off.

### 3.12. If you press and hold the button long, it will enter the microphone dynamic lighting effect mode

When you enter the microphone mode, you cannot use short press to switch the fixed lighting effect.

To exit the microphone mode, long press the button again.

 

## 3.2.***coftware control instructions***

The software is controlled through the DoHome APP, which is developed by our company and supports Apple and Android systems. You can scan the QR code with your mobile phone, or search for "DoHome" in the App Store or application market to download and install. And register and log in to the "DoHome" APP.

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree6.jpg) 

 

### ***3.2.1*** ***Binding device***

***A.Make sure that the mobile phone is connected to the home WiFi (only 2.4G WiFi network is supported),*** 

***Open Dohome App***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree7.jpg) 

**B.** ***click the "+" icon in the upper right corner of the homepage.***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree8.jpg) 

***C.*** ***Select the product icon(LED Strip).***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree9.jpg) 

***D.Enter the router password.***

![https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree20](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree20.jpg)

**E.** ***Please supply power (5V) to the Christmas tree lights. Please make sure that the Christmas lights are in the factory mode (red-green-blue-white-flashing).***

**F.** ***Open the phone WiFi settings. Connect to the "DoHome_XXXX" WiFi hotspot.***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree12.jpg) 

 

 

**G.** ***Return to "DoHome APP" and wait for the network configuration to be completed.***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree13.jpg) 

 

 

 

***Tip: How to restore the Christmas lights to factory mode***

***Power off and on the Christmas lights three times, and check the if it is flashing red-green-blue-white-flashing***

 

### 3.2.2Configuring the device to Apple

***1. Turn on HomeKit mode***

***(1) Make sure the device is bound to the DoHome APP***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree14.jpg) 

***(2) Enter the properties interface and click to turn on HomeKit mode.***

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree15.jpg) 

(3) Open Home. Please put the setting code in Figure 6 (123-45-678) in the viewfinder frame, and choose to add it anyway.

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree16.jpg) 

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree17.jpg) 

![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree18.jpg) 

If the iPhone does not display the device, please confirm whether the phone and the device are on the same WiFi network. If the addition fails, please check the following FAQ, if you have any questions, please contact technical support.



![DoHomeChristmasTree0](https://github.com/SmartArduino/document/raw/master/docs/SmartProduct/DoHomeChristmasTree/DoHomeChristmasTree19.jpg) 

Note: Before using the speaker, please log in to your platform account on the smart speaker device platform such as Alexa, Google Assistant, Tmall Elf, and Xiao Ai.

 

# ***4. program update and problem solving***

You can download the program to update yourself on our GitHub website: https://github.com/SmartArduino/DoHome/tree/master/DoHome_HomeKit_Christmas_Light

After-sales technical forum:

https://github.com/SmartArduino/DoHome/tree/master/DoHome_HomeKit_Moon_Light

FAQ: https://support.doiting.com/
<center><font size=10> W600 FAQ</center></font>
<center> From SZDOIT</center>

# Basic concepts

## What is W600?

​        W600 is a new generation of Lianshengde wireless local area network 802.11n (1T1R) low-power WLAN SoC chip that supports multiple interfaces and multiple protocols. The chip has built-in Cortex-M3 CPU processor and Flash, integrated radio frequency transceiver front-end RFTransceiver, CMOSPA power amplifier, baseband processor/media access control, integrated power management circuit, supports rich peripheral interfaces, and supports multiple encryption and decryption protocols. W600 provides customers with more space for secondary development, fewer chip peripheral circuits, easier development, and more cost-effective advantages.

## What is the difference between W601 and W600?

W601 and W600 belong to the W600 series WiFi chips of Lianshengde, the main differences are as follows:

| Attributes   | W600      | W601      |
| ------------ | --------- | --------- |
| Package      | QFN32 5*5 | QFN68 7*7 |
| Available IO | 17        | 48        |
| ADC          | no        | 8 pcs     |
| LCD          | no        | 1 pcs     |
| I2S          | no MCLK   | complete  |

## What is the relationship between Lianshengde and Xingtong Zhilian?

　　Lianshengde is the chip design and manufacturer of W600, and Starcom is the chip agent and solution supplier of Lianshengde.

## What is TW-01, TW-02?

　    TW01\~TW-03 is a W600 series module developed and produced by Shenzhen Xingtong Zhilian Technology Co., Ltd. Based on the W600 chip, the layout of peripheral components and antenna optimization are improved, and compatibility with existing ones on the market is considered when designing Module, convenient for everyone to replace and test.

## What is T-Cloud?

　　 T-Cloud is a global intelligent cloud service provided by Xingtong Zhilian. With TW series modules, there are many mature PCBA solutions.

## Does W600 have to rely on a remote server to develop?

　　This is determined according to your needs. If you only need a local area network to meet the product needs, then no server is needed, and you can also use W600 for development.

## How to develop products based on T-Cloud?

　　 T-Cloud is not open for the time being. If you need to use it, you can contact our company via [support@thingsturn.com](mailto:support@thingsturn.com). Later we will open the transparent transmission of the firmware, which can be externally connected to the MCU to achieve any customized functions.

## How to buy W600 modules and test boards?

　　 The official Taobao shop of Starcom Smart Link: http://shop.thingsturn.com, it is strongly recommended that novices buy the TB-01 development board.

## Which W600 module should I choose?

　　The difference between the module hardware is mainly the package difference, you can choose according to your needs, if you have any questions, please contact us.

## Should I choose AT development or SDK development?

SDK method:

*   Advantage: Minimize system cost and volume
* Disadvantages: Novices need a week to half a month to familiarize themselves with the code study

AT method:

* Advantage: Only need to know a few AT commands to realize network communication with external MCU! The development speed is fast.
* Disadvantage: Increased external CPU cost

You can evaluate which plan is suitable for you accordingly.

## During development, how do I seek help if I encounter problems?

- -If you are an enterprise user, we will appoint an engineer to be responsible for the connection of your company;
- -If you are an individual user, you can post in the forum or email to
      <support@thingsturn.com>, we will also have a dedicated engineer to handle it.

# Hardware connection

## How to build W600 minimum system

　　 The periphery of W600 is extremely simple, please refer to the module schematic diagram given by us.

## How many UARTs does W600 have?

　　 W600 has 2 complete UARTs with a maximum rate of 2Mbps. By default, the AT firmware uses serial port 0 for command control and serial port 1 for log printing.

## Can GPIO be directly connected to 5V?

　　 No! GPIO can only withstand 3.6V at most. A level conversion circuit must be passed, otherwise the GPIO will be permanently damaged.

## W600 Voltage and current requirements?

　　The voltage range of the digital part of W600 is 1.8V \~ 3.3V, and the operating voltage of the analog part is 3.0V\~ 3.6V, and the minimum is 3.0V. The peak value of analog power is 350 mA, and the peak value of digital power is 200 mA.

## When designing the power supply of W600, what issues should be paid attention to?

Please note the following points:

1. If you are using LDO transformation, please ensure that the input voltage and output voltage are large enough.
2. The decoupling capacitor on the power supply side must be placed close to W600, and the equivalent resistance must be low enough.
3. W600 cannot be directly connected to 5V voltage.
4. If power is supplied to W600 through DC-DC, add LC filter circuit if necessary.

## W600 has a large current when it is powered on. What is the reason?

　　 The RF and digital circuits of W600 have a high degree of integration. After power on, RF self-calibration will require a large current. The maximum limit circuit of the analog circuit may reach 500 mA; the maximum current of the digital circuit may reach 200 mA. In general operation, the average current is about 100 mA. Therefore, W600 needs to be powered up to 500 mA to ensure that there will be no instantaneous voltage drop.

## Can I use lithium batteries or 2 AA button batteries to directly power W600?

　　Theoretically, 2 AA button batteries can power W600. However, the voltage drop when discharging the lithium battery is relatively large, which is not suitable for directly supplying power to W600. The RF circuit of W600 is affected by temperature and voltage fluctuations. It is not recommended to directly supply power to W600 without any calibration power supply. It is recommended to use DC-DC or LDO to power W600.

## How is the RAM of W600 divided?

The entire RAM space is 288 KB, the current RAM space division:

|  Classification   | Starting address | Size（K Byte） |
| :---------------: | :--------------: | :------------: |
|  Available space  |    0x20000000    |      240       |
| Wi-Fi usage space |    0x2003C000    |       48       |

## How is W600's Flash allocated?

The total capacity of the built-in Flash is 1M Bytes, and the specific allocation method is as follows

|    Classification    | Starting address | Size（K Byte） |
| :------------------: | :--------------: | :------------: |
|  System parameters   |    0x8000000     |       8        |
| Secondary BOOT area  |    0x8002000     |       32       |
|     IMAGE1 head      |    0x800A000     |       4        |
|     IMAGE2 head      |    0x800B000     |       4        |
|   Parameter 1 area   |    0x800C000     |       4        |
|   Parameter 2 area   |    0x800D000     |       4        |
| IMAGE operating area |    0x800E000     |      450       |
|  IMAGE upgrade area  |    0x807E800     |      450       |
|      User area       |    0x80EF000     |       64       |



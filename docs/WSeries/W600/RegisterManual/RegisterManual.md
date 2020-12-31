<center><font size=10> W600 Register Manual </center></font>
<center> From SZDOIT</center>

# 1. Introduction

## 1.1 Writing purpose

The W600 chip is an embedded Wi-Fi SoC chip launched by Lianshengde Microelectronics. The chip is highly integrated, requires less peripheral components, and
The price ratio is high. Applicable to various smart products in the IoT (Smart Home) field. Highly integrated Wi-Fi function is its main function; in addition, the
The chip integrates Cortex-M3 core, built-in QFlash, SDIO, SPI, UART, GPIO, I²C, PWM, I²S, 7816 and other interfaces, and supports multiple hardware encryption and decryption algorithms.

This document mainly describes the internal structure of the W600 chip, the information of each function module and the detailed register usage information; it is the main reference material for developers to develop drivers and applications. There are open source implementations of various functions in the SDK provided by Lianshengde Microelectronics. Developers can refer to the corresponding drivers and application examples to increase their understanding of chip functions and register descriptions. This document does not describe the registers of the Wi-Fi part.

## 1.2 Reference Materials

For W600 chip packaging parameters, electrical characteristics, radio frequency parameters and other information, please refer to "W600 Chip Product Specification";
The W600 chip integrates a ROM program. The ROM program provides functions such as downloading firmware, reading and writing MAC addresses, and reading and writing Wi-Fi parameters.
For more information, please refer to "WM_W600_ROM Function Brief";

The W600 chip has a built-in 1Mbytes QFlash memory as a storage space for codes and parameters. This document provides basic operation information of QFlash. If you have requirements beyond the scope of this document, you need to refer to the QFlash manual;

W600 chip adopts ARM Cortex-M3 core, M3 related function introduction and development materials can refer to the information released by ARM;

# 2. Features

![image-20201026113703907](image-20201026113703907.png)
![image-20201026113736015](image-20201026113736015.png)

# 3. Overview

This chip is a SOC chip that supports multi-interface, multi-protocol wireless local area network 802.11n (1T1R). The SOC chip integrates RF Transceiver, CMOS PA power amplifier, baseband processor/media access control, SDIO, SPI, UART, GPIO and other low-power WLAN chips.

W600 chip supports GB15629.11-2006, IEEE802.11 b/g/n protocol, and supports STBC, Green Field, Short-GI, reverse transmission, RIFS frame interval, AMPDU, AMSDU, T-immediate Compressed Block Ack, normal Rich protocols and operations such as ACK, no ACK, and CTS to self.

The W600 chip integrates a radio frequency transceiver front end, A/D and D/A converters. It supports DSSS (Direct Sequence Spread Spectrum) and OFDM (Orthogonal Frequency Division Multiplexing) modulation modes, has data descrambling capabilities, and supports multiple different data transmission rates. The transceiver AGC function equipped in the analog front end of the transceiver enables the chip system to obtain the best performance. The W600 chip also includes a built-in enhanced signal monitor, which can largely eliminate the impact of multipath effects.

In terms of security, the W600 chip not only supports the national standard WAPI encryption, but also supports the international standards WEP, TKIP, and CCMP encryption. These hardware components enable the data transmission system based on this chip to perform confidential communication and still be able to obtain similar to the non-encrypted communication. Data transfer performance.

In addition to supporting the energy-saving operations specified by IEEE802.11 and Wi-Fi protocols, the W600 chip also supports user-customized energy-saving solutions. The chip supports four working modes: work, sleep, standby, and shutdown, so that the entire system can achieve low power consumption, and it is convenient for users to define different energy-saving solutions according to their own usage scenarios.

The W600 chip integrates a high-performance 32-bit embedded processor, a large amount of memory resources, and a rich peripheral interface, which is convenient for users
It is easy to apply the chip to the secondary development work of a specific product.

The W600 chip supports the AP function, which can realize the simultaneous establishment of 5 SSID networks and the function of 5 independent APs. Support the establishment of multiple multicast network functions. It can realize the function of establishing a BSS network as an AP while joining other networks as an STA.
W600 chip supports WPS mode, so that users can realize an encrypted complete network with one-click operation to ensure information security
Sex.

The multi-function and high integration of W600 chip ensure that the WLAN system does not require too many off-chip circuits and external memory.

# 4. Chip structure

## 4.1 Chip structure

The following figure describes the overall structure of the W600 chip. The core part includes Cortex-M3 CPU, 288KB SRAM and 16KB ROM storage space. As the constant power supply module of the chip, the PMU part provides power-on sequence management, start-up clock, and real-time clock functions. Provides a wealth of peripheral functions and hardware encryption and decryption functions. The Wi-Fi part integrates MAC, BB and RF.

![image-20201026114002581](image-20201026114002581.png)

## 4.2 Bus structure

The W600 chip is composed of two-level buses, as shown in the figure below:

![image-20201026114038813](image-20201026114038813.png)

(1) AHB-1 bus
This level of bus has four master devices-namely Cortex-M3, DMA, GPSEC and 5 slave devices.

Cortex-M3 is designed based on the ARMV7-M architecture, uses Thumb-2 instruction set, adopts Harvard structure, and has independent instruction bus and data bus. The bus clock can work at 80MHz at the fastest frequency and can be configured to 40MHz or lower. For details of clock configuration, please refer to the clock division part.

![image-20201026114120218](image-20201026114120218.png)

![image-20201026114142451](image-20201026114142451.png)

2) AHB-2 bus
This bus has 4 master devices and 3 slave devices. Using the crossbar connection structure, different master devices can access different slave devices simultaneously, thereby increasing bandwidth. The bus clock works at the fastest frequency of 40MHz, and can be configured to be lower as required.

![image-20201026114252834](image-20201026114252834.png)

Each master device uses a fixed priority, and the priority decreases from top to bottom.

![image-20201026114329401](image-20201026114329401.png)

## 4.3 Clock structure

![image-20201026114552379](image-20201026114552379.png)
![image-20201026114958672](image-20201026114958672.png)

## 4.4 Address Space

Cortex-M3 can address 4G space, which are code area, memory area, on-chip peripherals, off-chip storage area, off-chip peripherals and system peripheral area.

![image-20201026115106583](image-20201026115106583.png)
![image-20201026115136892](image-20201026115136892.png)

### 4.4.1 SRAM

W600 built-in 288KB SRAM. Among them, 160KB is mounted on the first-level AHB bus, and 128KB is mounted on the second-level AHB bus. Primary bus devices such as CPU can access all memory areas, but devices on the secondary bus can only access 128KB of memory on the secondary bus.

### 4.4.2 Flash

#### 4.4.2.1 QFlash

W600 integrates 1MBytes QFlash. Through the integrated 32KB cache inside the chip, the program can be executed on QFlash in XIP mode. When the program is running, the CPU first reads instructions from the Cache. When the instructions cannot be fetched, they read the instructions from QFlash in a row of 8Bytes and store them in the Cache. Therefore, when the continuously running code size is less than 32K, the CPU will not need to read instructions from QFlash, and the CPU can run at a higher frequency. The above method is a read instruction operation method, and the RO segment of the entire Image will be operated in this way. The user does not need to intervene in this process.

QFlash can also store data. When the user program needs to read and write data in QFlash, it needs to be operated through the built-in QFlash controller. QFlash provides corresponding addresses, instructions and other registers to assist users in achieving the desired operation. For detailed description, please refer to the corresponding chapter of QFlash controller.

Users need to pay attention to that when the program reads or writes data, there is no need to perform state judgment, waiting, etc., because the QFlash control
The controller itself will make a judgment. When the QFlash controller returns, it indicates that the reading or writing has been completed.

#### 4.4.2.2 SPI Flash

In addition to the 6PIN QFlash interface (built-in PIN, unpackaged), W600 chip also supports low-speed SPI interface access. The SPI interface has a maximum operating frequency of up to 20MHz and supports master-slave functions. For detailed description, please refer to the corresponding chapter of the SPI interface.
The W600 chip program can only be executed in the space corresponding to QFlash. But when users need more storage space, they can
Expand Flash on the SPI interface. User data, parameters, OTA Image, etc. can all be placed in the external SPI Flash space.

### 4.4.3 Bit Band

W600 supports Bit-Band Operations.

#### 4.4.3.1 Bit Band Operation

Bit-band operations use ordinary load/store instructions to read and write a single BIT, which is equivalent to assigning an alias to each BIT in the bit-band area, and access to the alias is used to replace the specified BIT access. The mapping process between the designated BIT and the alias is directly completed by the kernel without manual intervention.

#### 4.4.3.2 Cortex-M3 bit band operation area

- -SRAM's lowest 1M range
- -The lowest 1M range of the on-chip peripheral area

#### 4.4.3.3 The relationship between bit-band address and bit-band alias

For a bit in the SRAM area, record the address of the byte where it is located as A, and the bit number is n (0<=n<=7), then the mapped alias area address is:

AliasAddr = 0x220000 + ((A-0x20000000)*8+n)*4 = 0x22000000 + (A-0x20000000)*32 + nx4 For a bit of the on-chip peripheral bit band, record the address of the byte where it is located as A , The bit sequence number is n(0<=n<=7), then the mapped alias area
The address is:
AliasAddr = 0x42000000+((A-0x40000000)*8+n)*4 = 0x42000000 + (A-0x40000000)*32 + nx4 In the above formula, "*4" means that a word is 4 bytes, and "*8" means There are 8 bits in a byte.
The following figure shows the mapping relationship between the address of the memory bit band area and the address of the bit band alias area

![image-20201026115621574](image-20201026115621574.png)

#### 4.4.3.4 W600 bit band operable area

- 0X2000_0000 - 0X2004_8000

- 0X4000_0000 - 0X4001_3C00

## 4.5 Start configuration

After the W600 chip is powered on, the CPU will start to execute the firmware in the ROM and load the user Image at the specified address in the Flash.

The ROM firmware reads the BootMode (PA0) pin when it starts running, and judges to enter the startup state according to the signal of the pin: ![image-20201026115717796](https://github.com/SmartArduino/zhdocs/raw/master/W600Series /DateSheet/image-20201026115717796.png)

Generally, the BootMode pin should be used in the production or debugging stage. In the production stage, the user can quickly burn the Flash by pulling the BootMode pin down for more than 30ms to enter the functional mode.

In the scenario of product rework or repair, the chip does not enter the "highest security level" (for the description of the security level, please refer to
"WM_W600_ROM Function Brief"), you can enter the function mode through this pin, erase the old Image, and write the new Image.

In the debugging stage, regardless of any fault in the firmware, you can continue to pull the BootMode pin down for more than 30ms to enter the serial port download function and burn the new firmware.

# 5. Clock and reset module

## 5.1 Function overview

The clock and reset module completes the software control of the chip clock and reset system. Clock control includes clock frequency conversion, clock shutdown and adaptive gating; reset control includes soft reset control of the system and sub-modules.

## 5.2 Main Features

- -Support each module clock shutdown
- -Support some module clock adaptive shutdown
- -Support software reset of each module
- -Support CPU frequency setting
- -Support ADC/DAC loopback test
- -Support I2S clock setting

## 5.3 Function description

### 5.3.1 Clock Gating

By configuring the clock gating enable register CLK_GATE_EN, you can control the clock shutdown of the specified function to turn off a certain module
The purpose of the function.

In order to provide the flexibility of firmware to control system power consumption, the clock and reset module provides the clock gating function of each module in the system. When the clock of the corresponding module is turned off, the digital logic and clock tree of the module will stop working, which can reduce the dynamic power consumption of the system.

The specific switches of each module correspond to the detailed description of the register SW_CLKG_EN.

### 5.3.2 Clock adaptive shutdown

The chip adaptively turns off the clock of some functional modules according to the transition of some internal states.

Please do not change the configuration, otherwise it may cause system abnormality when configuring PMU function.

### 5.3.3 Function reset

The chip provides the soft reset function of each subsystem. The subsystem can be reset by setting the corresponding BIT of SW_RST_CTRL to 0.
However, the reset state will not be automatically cleared. To restore normal operation, the corresponding BIT bit of SW_RST_CTRL must be set to 1.
The soft reset function does not reset the CPU and WatchDog.

In this register, the reset operation of APB/BUS1/BUS2 (corresponding to APB bus, system bus and data bus) is not recommended, which will cause system access device abnormality.

### 5.3.4 Clock division

The W600 system uses a 40MHz crystal as the system clock source, the system has a built-in DPLL, and a fixed output of 160MHz clock is used as the system clock source.
Clock source (as shown below).

![image-20201026133101774](image-20201026133101774.png)

The system bus clock is consistent with the CPU clock, and the data bus clock is fixed at 1/4 of the WLAN root clock.

The WLAN root clock is also the clock source of the entire WLAN system.

This module provides functions to set the CPU clock and WLAN root clock for the firmware to adjust system performance and power consumption.

Set the BIT[3:0] of the SYS_CLK_DIV register to adjust the CPU clock division factor. The source clock for CPU clock division is DPLL
The output is fixed at 160MHz. The default value of the CPU clock division coefficient is 2, that is, the default CPU operating frequency is divided by 2 of 160MHz, that is, 80MHz. When you need to adjust the clock required by the CPU, you can reconfigure this parameter.

Set BIT[7:4] of SYS_CLK_DIV register to adjust the WLAN clock frequency division factor. The default frequency division factor is 1, which means that DPLL is not correct
The 160MHz output frequency is divided to obtain the 160MHz clock, which is sent to the WLAN as the root node clock (the WLAN continues to divide the frequency to obtain a more detailed low-frequency clock for the WLAN system).

Note: If you want the WLAN system to work normally, the WLAN root clock needs to be kept at 160MHz, otherwise the WLAN system will fail.
When the WLAN system is not required to work, the WLAN root clock can be reduced to reduce the dynamic power consumption of the system.

The CPU/WLAN clock frequency division factor in W600 cannot be arbitrarily configured, otherwise, the configuration may not take effect. The following table shows the available frequency division configuration and the corresponding system clock:

![image-20201026133211759](image-20201026133211759.png)

When changing the system clock configuration, you need to pay attention: the ratio of the system bus to the data bus needs to be maintained at M:1, where M is an integer and the minimum is 1. When changing the system clock configuration, you also need to update the BIT [11:8] of the register SYS_CLK_DIV at the same time to set the correct scale factor. Otherwise, access to the data bus will get abnormal data.

[27:12] of SYS_CLK_DIV provides the frequency division factor to set the working frequency of SAR_ADC, which is divided by 40M as the clock source. Minute
The frequency coefficient is the assigned frequency division value.

BIT[28] of SYS_CLK_DIV is to configure the clock frequency selection of the core operation of the RSA module, which can be 40MHz or 80MHz.
When you need to reconfigure cpu_clk_divider, wlan_clk_divider, bus2_syncdn_factor, sdadc_fdiv, you need to set BIT[31] of SYS_CLK_DIV, the hardware will automatically update the above four parameters to the divider, and then clear BIT[31].

I2S_CLK_CTRL provides the clock configuration function of the I2S module.

### 5.3.5 Debug function control

The user can set DEBUG_CTRL value BIT5 to achieve the purpose of enabling and disabling the JTAG function.

## 5.4 Register description

### 5.4.1 Register List

![image-20201026133314628](image-20201026133314628.png)

### 5.4.2 Software clock gating enable register

![image-20201026133854314](image-20201026133854314.png)
![image-20201026133931458](image-20201026133931458.png)
![image-20201026134012302](image-20201026134012302.png)
![image-20201026134041274](image-20201026134041274.png)

### 5.4.3 Software clock mask register

![image-20201026134128768](image-20201026134128768.png)

### 5.4.4 Software reset control register

![image-20201026134200995](image-20201026134200995.png)
![image-20201026134228264](image-20201026134228264.png)
![image-20201026134307077](image-20201026134307077.png)
![image-20201026134346820](image-20201026134346820.png)
![image-20201026134419076](image-20201026134419076.png)
![image-20201026134448559](image-20201026134448559.png)
![image-20201026134519456](image-20201026134519456.png)

### 5.4.5 Clock divider configuration register

![image-20201026135629212](image-20201026135629212.png)
![image-20201026135702463](image-20201026135702463.png)
![image-20201026135739043](image-20201026135739043.png)

### 5.4.6 Debug Control Register

![image-20201026135820411](image-20201026135820411.png)

### 5.4.7 I2S clock control register

![image-20201026135915434](image-20201026135915434.png)
![image-20201026135942886](image-20201026135942886.png)
![image-20201026140022611](image-20201026140022611.png)

# 6. DMA module

## 6.1 Function overview

DMA is used to provide high-speed data transfer between peripherals and memory and between memory and memory. Data can be moved quickly through DMA without any CPU operation. The CPU resources saved in this way will not affect the CPU to perform other instructions.

DMA is mounted on the AHB bus, supports up to 8 channels, 16 hardware peripheral request sources, and supports linked list structure and register control.

## 6.2 Main features

- -Amba2.0 standard bus interface, 8 DMA channels
- -Support DMA operation based on memory linked list structure
- -Support 16 hardware peripheral request sources
- -Support 1,4-burst operation mode
- -Support byte, half-word, word as unit transmission operation
- -Support source and destination addresses unchanged or increasing in order or configurable to cycle operation within a predefined address range
- -Supports data transmission methods from memory to memory, memory to peripherals, and peripherals to memory

## 6.3 Function description

### 6.3.1 DMA channel

W600 supports a total of 8 DMA channels. DMA channels do not interfere with each other and can run simultaneously. Different DMA channels can be selected for different data streams.

Each DMA channel is allocated in a different register address offset segment, and you can directly select the address segment of the corresponding channel for configuration and use.

The register configuration modes of different channels are completely the same.

![image-20201026140242571](image-20201026140242571.png)

### 6.3.2 DMA data flow

8 DMA channels can realize a one-way data transmission link between source and destination.

The source and destination addresses of DMA can be set to three modes: unchanged, incremental or circular after each DMA operation is completed:

- -DMA_CTRL[2:1] controls how the source address changes after each DMA operation;
- -DMA_CTRL[4:3] controls how the destination address changes after each DMA operation.

DMA can set the transport unit of byte, half-word, and word. The final quantity of data to be transported is an integer multiple of the transport unit, which can be set by DMA_CTRL[6:5].

DMA can set how many units of data to be transferred at a time through burst, and select 1 or 4 units of data to be transferred at a time through DMA_CTRL[7]. Transfer 4 words of data

DMA can set the number of Bytes to start DMA transmission each time, the maximum is 65535 Bytes, which can be set by DMA_CTRL[23:8].

### 6.3.3 DMA cycle mode

DMA cycle address mode means that after setting the source and destination addresses of DMA, the data transfer will jump after reaching the set cycle boundary.
To the loop start address, the loop will be executed until it reaches the set transmission byte.

The source and destination addresses of the circular address mode need to be set with the SRC_WRAP_ADDR and DEST_WRAP_ADDR registers, and communicate
Use WRAP_SIZE to set the loop length value.

### 6.3.4 DMA transfer mode

DMA supports 3 transfer modes:

- -Memory to memory
     Both the source address and the destination address are configured as the memory address to be transferred, and DMA_MODE[0] is set to 0 in software mode.
- -Memory to peripheral
     The source address is set to the memory address, the destination address is set to the peripheral address, DMA_MODE[0] is set to 1, hardware mode,
   DMA_MODE[5:2] select the peripheral used.
- -Peripheral to memory
     The source address is set to the peripheral address, the destination address is set to the memory address, DMA_MODE[0] is set to 1, hardware mode,
   DMA_MODE[5:2] select the peripheral used.

### 6.3.5 DMA peripheral selection

When using the transfer method from peripheral to memory or memory to peripheral, in addition to the corresponding peripheral needs to be set to DMA TX or RX
In addition, DMA_MODE[5:2] also needs to select the corresponding peripheral.

Note: Because there are 3 UART ports, when the UART uses DMA, it is also necessary to select the corresponding one through UART_CH[1:0]
UART.

### 6.3.6 DMA linked list mode

DMA supports linked list working mode. Through the linked list mode, we can move down in advance when DMA transfers the current linked list memory data
A linked list is filled with data. After the DMA finishes moving the current linked list, it judges that the next linked list is valid and can directly move the next linked list.
data. Linked lists can effectively improve the efficiency of DMA and CPU coordination.

Linked list operation mode: Set DMA as linked list work mode through DMA_MODE[1] register, then set DESC_ADDR register
Set it to the start address of the linked list structure, and then enable DMA through the CHNL_CTRL register. When the DMA processing is complete
After the move, the software informs the DMA that there is still valid data in the linked list by setting the valid flag, and the DMA is based on the valid flag of the linked list.
Process the next data to be moved.

### 6.3.7 DMA interrupt

An interrupt can be generated when DMA transfer is completed or burst, and the INT_MASK register can mask the interrupt corresponding to the DMA channel.

After the DMA corresponding interrupt is generated, the current interrupt status can be queried through the INT_SRC register, indicating what is currently being generated.
The corresponding status bit needs software to write 1 to clear 0.

## 6.4 Register description

### 6.4.1 Register List

![image-20201026140842967](image-20201026140842967.png)
![image-20201026140933649](image-20201026140933649.png)

### 6.4.2 Interrupt Mask Register

![image-20201026141023288](image-20201026141023288.png)
![image-20201026141047516](image-20201026141047516.png)

### 6.4.3 Interrupt Status Register

![image-20201026141128304](image-20201026141128304.png)

### 6.4.4 UART selection register

![image-20201026141158244](image-20201026141158244.png)

### 6.4.5 DMA source address register

![image-20201026141253667](image-20201026141253667.png)

### 6.4.6 DMA destination address register

![image-20201026141326588](image-20201026141326588.png)

### 6.4.7 DMA cycle source start address register

![image-20201026141349004](image-20201026141349004.png)

### 6.4.8 DMA loop destination start address register

![image-20201026141416561](image-20201026141416561.png)

### 6.4.9 DMA cycle length register

![image-20201026141442315](image-20201026141442315.png)

### 6.4.10 DMA channel control register

![image-20201026141634140](image-20201026141634140.png)
![image-20201026141658202](image-20201026141658202.png)

### 6.4.11 DMA mode selection register

![image-20201026141757728](image-20201026141757728.png)
![image-20201026141831587](image-20201026141831587.png)

### 6.4.12 DMA data flow control register

![image-20201026141921754](image-20201026141921754.png)
![image-20201026141951360](image-20201026141951360.png)
![image-20201026142024882](image-20201026142024882.png)

### 6.4.13 DMA transfer byte count register

![image-20201026142105602](image-20201026142105602.png)

### 6.4.14 DMA linked list entry address register

Table 29 DMA linked list entry address register

![image-20201026142139513](image-20201026142139513.png)

### 6.4.15 DMA current destination address register

![image-20201026142216017](image-20201026142216017.png)

# 7. General hardware encryption module

## 7.1 Function overview

The encryption module automatically completes the encryption of the source address space data of the specified length, and automatically writes the encrypted data back to the specified destination address space after completion; supports SHA1/MD5/RC4/DES/3DES/AES/CRC/PRNG.

## 7.2 Main features

- -Support SHA1/MD5/RC4/DES/3DES/AES/CRC/PRNG encryption algorithm
- -DES/3DES supports ECB and CBC two modes
- -AES supports ECB, CBC and CTR three modes
- -CRC supports four modes: CRC8, CRC16_MODBUS, CRC16_CCITT and CRC32
- -CRC supports input/output reverse
- -SHA1/MD5/CRC supports continuous multi-packet encryption
- -Pseudo-random number supports continuous generation of 16-bit and 32-bit random numbers, and supports seed

## 7.3 Function description

### 7.3.1 SHA1 encryption

Hardware SHA1 calculation can be performed on continuous multi-packet data, the calculation result is stored in the register, and the encryption result of the previous packet can be used as the initial value of the next packet.

### 7.3.2 MD5 encryption

Hardware MD5 calculation can be performed on continuous multiple packets of data, the calculation result is stored in the register, and the encryption result of the previous packet can be used as the next packet
Initial value.

### 7.3.3 RC4 encryption

Support RC4 encryption and decryption.

### 7.3.4 DES encryption

Support DES encryption and decryption, support ECB and CBC two modes.

### 7.3.5 3DES encryption

Support 3DES encryption and decryption, support ECB and CBC two modes.

### 7.3.6 AES encryption

It supports AES encryption and decryption, and supports ECB, CBC and CTR three modes.

### 7.3.7 CRC encryption

The hardware CRC calculation can be performed on continuous multi-packet data, the calculation result is stored in the register, and the encryption result of the previous packet can be used as the next packet
Initial value, supports four modes of CRC8, CRC16_MODBUS, CRC16_CCITT and CRC32, and supports input/output reverse.
CRC32 calculation formula is as follows:

1. CRC-32: 0x04C11DB7
X32+X26+X23+X22+X16+X12+X11+X10+X8+X7+X5+X4+X2+X+1
Commonly used in ZIP, RAR, IEEE 802 LAN/FDDI, IEEE 1394, PPP-FCS and other protocols.

2. CRC-16: supports two polynomials
2.1: 0X1021
X16 + X12 + X5 + 1
Commonly used in ISO HDLC, ITU X.25, V.34/V.41/V.42, PPP-FCS CCITT and other protocols.

2.2: 0X8005
X16 + X15 + X2 + 1
Commonly used in USB, ANSI X3.28, SIA DC-07 and other protocols.

3. CRC-8: 0X207
x8+x2+x1+1

### 7.3.8 PRNG pseudo random number

It can continuously generate 16-bit or 32-bit pseudo-random numbers, supports random seeds, and stores random results in registers.

## 7.4 Register description

### 7.4.1 Register List

![image-20201026142730177](image-20201026142730177.png)
![image-20201026142755633](image-20201026142755633.png)

### 7.4.2 Configuration Register

![image-20201026142932654](image-20201026142932654.png)
![image-20201026142949824](image-20201026142949824.png)
![image-20201026143016895](image-20201026143016895.png)

### 7.4.3 Control Register

![image-20201026143108774](image-20201026143108774.png)

### 7.4.4 Status Register

![image-20201026143137639](image-20201026143137639.png)

# 8. RSA encryption module

## 8.1 Function overview

RSA computing hardware coprocessor, providing Montgomery (FIOS algorithm) modular multiplication function. Cooperate with RSA software library to realize RSA algorithm.
Supports 128-bit to 2048-bit modular multiplication.

## 8.2 Main features

- -Support 128-bit to 2048-bit modular multiplication (modular multiplication length is an integer multiple of 32 bits)
- -Support D*D; X*Y; D*Y; X*X and other 4 modular multiplication modes

## 8. Function description

### 8.3.1 Modular multiplication function

RSA computing hardware coprocessor, providing Montgomery (FIOS algorithm) modular multiplication function. Cooperate with RSA software library to realize RSA algorithm. Supports 128-bit to 2048-bit modular multiplication.

## 8.4 Register description

### 8.4.1 Register List

![image-20201026143315629](image-20201026143315629.png)

### 8.4.2 Data X Register

XBUF corresponds to the buffer of data X (2048bit), and the corresponding haddr value is 0000h~00fch. The corresponding rules are as follows:

![image-20201026143350284](image-20201026143350284.png)

### 8.4.3 Data Y register

YBUF corresponds to the buffer of data Y (2048bit), and the corresponding haddr value is 0100h~01fch. The corresponding rules are as follows:

![image-20201026143414308](image-20201026143414308.png)

### 8.4.4 Data M register

MBUF corresponds to the buffer of data M (2048bit), and the corresponding haddr value is 0200h~02fch. The corresponding rules are as follows:

![image-20201026143440363](image-20201026143440363.png)

### 8.4.5 Data D register

DBUF corresponds to the buffer of data D (2048bit), and the corresponding haddr value is 0300h~03fch. The corresponding rules are as follows:

![image-20201026143504522](image-20201026143504522.png)

### 8.4.6 RSA Control Register

RSACON, RSA control register, the actual physical space is a 32bit register.

![image-20201026143542607](image-20201026143542607.png)

### 8.4.7 Parameter MC Register

|  Bit   | Access |                         Instructions                         | Reset value |
| :----: | :----: | :----------------------------------------------------------: | :---------: |
| [31:0] |   WO   | RSAMC corresponds to the parameter MC (32bit). The reset value is all 0. The readout value is all 0s. |    32’h0    |

### 8.4.8 Parameter N register

RSAN corresponds to the parameter N (7bit). The N value is the value of the modulo multiplication length divided by 32. That is, if you call 1024-bit modular multiplication operation, you need to set N=32. When writing to this register, take the lower 7 bits as valid data, and when reading, the upper 25 bits are 0. The reset value is all 0.

![image-20201026144741883](image-20201026144741883.png)

# 9. GPIO module

## 9.1 Function overview

The GPIO controller implements the software configuration of GPIO properties, enabling users to conveniently operate GPIO.

Each GPIO can be individually configured by software, set it as input port, output port, set its floating, pull-up, pull-down state, set its rising edge, falling edge, double edge, high level, low level interrupt trigger mode .

## 9.2 Main features

- -Support GPIO software configuration
- -Support GPIO interrupt configuration
- -Up to 17 GPIOs available

### 9.3 Function description

The GPIO provided in W600 is divided into two groups, one is GPIOA, and the other is GPIOB. The start addresses of GPIOA and GPIOB registers are different, but their functions are the same.

When the user wants to use a specific IO as a software-controlled GPIO, set the corresponding position in the GPIO multiplexing selection register to 0, that is
can.

The GPIO direction control register is used to control the direction of the GPIO. 1 means the corresponding GPIO is used as an output pin, and 0 means the corresponding GPIO is used as an input pin.

The GPIO pull-up and pull-down control register is used to control the pull-up and pull-down functions of the corresponding IO. This register is active low, set to 0 means open the corresponding IO
The pull-up and pull-down function is set to 1 to turn off the pull-up and pull-down function. Each IO has only one pull-up and pull-down state. Please refer to the IO multiplexing table for the attributes of IO.

When the GPIO data register is set to input state, it indicates the level of input IO. When set to output state, 1 or 0 can be written.
Set the output level of IO. This register is controlled by the GPIO data enable register. The GPIO data register can only be read and written when the GPIO data enable register is set to 1.

The GPIO module provides input signal detection function. High and low level detection and up and down can be realized by configuring the registers related to GPIO interrupt
Edge transition detection. When the input signal of the corresponding IO meets the preset conditions, such as high-level trigger or rising edge trigger, it will
Trigger GPIO interrupt and report to MCU for processing. The MCU needs to clear the corresponding interrupt status to avoid false triggering of the interrupt.

## 9.4 Register description

### 9.4.1 Register List

![image-20201026144958707](image-20201026144958707.png)

![image-20201026145024198](image-20201026145024198.png)
![image-20201026145037879](image-20201026145037879.png)

### 9.4.2 GPIO data register

![image-20201026145150906](image-20201026145150906.png)

![image-20201026145201725](image-20201026145201725.png)

### 9.4.3 GPIO data enable register

![image-20201026145702411](image-20201026145702411.png)

![image-20201026145735151](image-20201026145735151.png)
![image-20201026145753077](image-20201026145753077.png)

### 9.4.4 GPIO direction control register

![image-20201026145832161](image-20201026145832161.png)

### 9.4.5 GPIO Up-Down Control Register

![image-20201026145902321](image-20201026145902321.png)

![image-20201026145928905](image-20201026145928905.png)
![image-20201026145952504](image-20201026145952504.png)

### 9.4.6 GPIO multiplexing selection register

![image-20201026150021872](image-20201026150021872.png)

![image-20201026150041819](image-20201026150041819.png)
![image-20201026150102855](image-20201026150102855.png)

### 9.4.7 GPIO multiplexing selection register 1

![image-20201026150156452](image-20201026150156452.png)

### 9.4.8 GPIO multiplexing selection register 0

![image-20201026150225650](image-20201026150225650.png)

### 9.4.9 GPIO interrupt trigger mode configuration register

![image-20201026150305208](image-20201026150305208.png)
![image-20201026150318016](image-20201026150318016.png)

![image-20201026150344127](image-20201026150344127.png)

### 9.4.10 GPIO interrupt edge trigger mode configuration register

![image-20201026150408768](image-20201026150408768.png)

### 9.4.11 GPIO interrupt upper and lower edge trigger configuration register

![image-20201026150445919](image-20201026150445919.png)
![image-20201026150500672](image-20201026150500672.png)

### 9.4.12 GPIO interrupt enable configuration register

![image-20201026150544151](image-20201026150544151.png)

### 9.4.13 GPIO raw interrupt status register

![image-20201026150612537](image-20201026150612537.png)

### 9.4.14 GPIO interrupt status register after shielding

![image-20201026150637312](image-20201026150637312.png)

### 9.4.15 GPIO interrupt clear control register

![image-20201026150707642](image-20201026150707642.png)

# 10. High-speed SPI device controller

## 10.1 Function overview

Compatible with the general SPI physical layer protocol, the host can access the device at a high speed by agreeing on the data format for interaction with the host, and the maximum supported operating frequency is 50MHZ.

## 10.2 Main features

- -Compatible with universal SPI protocol
- -Optional level interrupt signal
- -Supports up to 50Mbps rate
- -Simple frame format, full hardware analysis and DMA

## 10.3 Function description

### 10.3.1 Introduction to SPI Protocol

SPI works in a master-slave mode. Usually there is a master device and one or more slave devices. At least 4 wires are required. In fact, 3 wires are also available (for unidirectional transmission). They are SDI (data input), SDO (data output), SCLK (clock), CS (chip select).
(1) SDI-Serial Data In, serial data input
(2) SDO-Serial Data Out, serial data output
(3) SCLK-Serial Clock, clock signal, generated by the master device
(4) CS-Chip Select, slave device enable signal, controlled by master device.

Among them, CS is the control signal whether the slave chip is selected by the master chip, that is, only when the chip select signal is a predetermined enable signal (high potential or low potential), the master chip can operate on this slave chip. This makes it possible to connect multiple SPI devices on the same bus.

In addition to the above 4 signal lines, HSPI also adds an additional INT line. When the slave device has data to upload, a next line is generated.
The interruption of the falling edge realizes the active reporting of data.

SPI communication is completed through data exchange. Data is transmitted bit by bit. SCLK provides clock pulses. SDI and SDO are based
Data transmission is completed at this pulse. The data is output through the SDO line, and the data changes on the rising or falling edge of the clock.
Edge or rising edge is read. To complete a bit of data transmission, the input also uses the same principle. Therefore, at least 8 clock signal changes (upper edge and lower edge are one time) are required to complete 8-bit data transmission.

The SCLK signal line is controlled by the master device, and the slave device cannot control the signal line. In an SPI-based device, there is at least one master device.

### 10.3.2 SPI working process

The HSPI inside the chip works with the wrapper controller. The wrapper controller integrates DMA, and the data exchange between the HSPI internal FIFO and the internal buffer of the chip is realized through DMA. This operation is implemented by hardware, and the software does not need to care about the data sending and receiving process, it only needs to configure the sending and receiving data linked list and operate the corresponding registers of the wrapper controller.

For a detailed introduction to the wrapper controller, please refer to the relevant chapters.

## 10.4 Register description

### 10.4.1 HSPI chip internal operation register list

![image-20201026150955752](image-20201026150955752.png)

#### 10.4.1.1 HSPI FIFO clear register

![image-20201026151039181](image-20201026151039181.png)

#### 10.4.1.2 HSPI configuration register

![image-20201026151108765](image-20201026151108765.png)

#### 10.4.1.3 HSPI mode configuration register

![image-20201026151134276](image-20201026151134276.png)

#### 10.4.1.4 HSPI Interrupt Configuration Register

![image-20201026151230748](image-20201026151230748.png)
![image-20201026151249485](image-20201026151249485.png)

#### 10.4.1.5 HSPI Interrupt Status Register

![image-20201026151319842](image-20201026151319842.png)

#### 10.4.1.6 HSPI Data Upload Length Register

![image-20201026151350291](image-20201026151350291.png)

### 10.4.2 Host access HSPI controller register list

The host side accesses the SPI interface register through a fixed SPI command format. The command length is fixed at one byte, and the data length is fixed at two bytes.

![image-20201026151431611](image-20201026151431611.png)
![image-20201026151454796](image-20201026151454796.png)

#### 10.4.2.1 HSPI Get Data Length Register

![image-20201026151533163](image-20201026151533163.png)

#### 10.4.2.2 HSPI send data flag register

![image-20201026151606498](image-20201026151606498.png)
![image-20201026151628697](image-20201026151628697.png)

#### 10.4.2.3 HSPI Interrupt Configuration Register

![image-20201026151704970](image-20201026151704970.png)

#### 10.4.2.4 HSPI Interrupt Status Register

![image-20201026151733589](image-20201026151733589.png)

#### 10.4.2.5 HSPI data port 0

![image-20201026151817398](image-20201026151817398.png)

#### 10.4.2.6 HSPI data port 1

![image-20201026151901008](image-20201026151901008.png)
![image-20201026151922367](image-20201026151922367.png)

#### 10.4.2.7 HSPI command port 0

![image-20201026152420658](image-20201026152420658.png)

#### 10.4.2.8 HSPI command port 1

![image-20201026152447406](image-20201026152447406.png)

### 10.4.3 High-speed SPI device controller interface timing

Mainly describe the SPI read and write timing, and how the main SPI interacts with HSPI.

#### 10.4.3.1 Data format

The data format is divided into two parts: command field and data field, as shown in the figure below. The fixed length of the command field is 8bit, and the length of the data field varies according to different access objects. See below for details.
The highest bit of the command field is the read and write flag bit, and the remaining 7 bits are the address.

- -0 means to read data from the back 7bit address
- -1 means write data to the back 7bit address

![image-20201026152544607](image-20201026152544607.png)

The data field of this module only supports two lengths. The upper computer SPI access interface configuration register (Table 2), the data field length is 16bit; data is transmitted through the ports (data port 0, data port 1, command port 0 and command port 1), The length of the data field is an integer multiple of 32bit;
The following figure shows the timing diagram of the read-write interface configuration register. The default configuration of the slave device is little-endian mode.

![image-20201026152954718](image-20201026152954718.png)

![image-20201026153014878](image-20201026153014878.png)

The following figure is a timing diagram of reading and writing data. The length of the data field is an integer multiple of 32 bits. The figure shows the length of only one word.

![image-20201026153054089](image-20201026153054089.png)

![image-20201026153113611](image-20201026153113611.png)

Note: There can be no waiting time between the command and the data, that is, after the command field is transmitted, the data can be transmitted immediately, and no extra idle clock or idle time is required. There is a time delay, but no idle clock can appear.

#### 10.4.3.2 Timing

This module supports half-duplex, and the supported timing is divided into 4 types according to the clock phase and sampling point. The following sequence only gives the phase and sampling relationship of the clock. It should be noted that the chip supports (CPOL=0, CPHA=0) by default.

Note: There can be no waiting time between the command and the data, that is, after the command field is transmitted, the data can be transmitted immediately, and there is no need for extra idle clock or idle time. Time delay is fine, but no idle clock can appear.

![image-20201026153216564](image-20201026153216564.png)

![image-20201026153244430](image-20201026153244430.png)

![image-20201026153305542](image-20201026153305542.png)

![image-20201026153325286](image-20201026153325286.png)

#### 10.4.3.3 Interrupt

The interrupt signal is sent from the slave device to the master device, triggered by the SPI_INT pin, and active at low level.
spi_int mainly informs the spi host that there is data or commands to upload. The interface registers that the spi host cares about when processing interrupts are:

- SPI_INT_HOST_MASK

- SPI_INT_HOST_STTS

- RX_DAT_LEN

Note: Each uploaded frame corresponds to an interrupt. Only after the current frame to be uploaded is transmitted, if there are still frames to be uploaded, a new interrupt will be generated at this time. The figure below is a way to handle interrupts.

![image-20201026153417556](image-20201026153417556.png)

#### 10.4.3.4 Main SPI data sending and receiving workflow

![image-20201026153502252](image-20201026153502252.png)

Note: The length of the data sent must be in words. If it is not a whole word, fill in 0 to complete it.

![image-20201026153553461](image-20201026153553461.png)

Note: The length of the issued command must be in words. If it is not a whole word, fill in 0 to complete it.

![image-20201026153629726](image-20201026153629726.png)

The flow of upstream data is the same as that of upstream commands.

It should be noted here that the length of the upstream data must be in words. If the effective length is not a whole word, the extra data at the end can be thrown away.

It should be noted that there are two channels of data and command between the master and the slave to exchange data, and the user can choose one channel or both of them as needed. The maximum data length of one interaction of the command channel is 256 bytes, and the maximum data length of one interaction of the data channel is 1500 bytes. The data length limit is controlled by the slave device. If the length exceeds the limit, the data structure of the slave device will be destroyed.

# 11. SDIO device controller

## 11.1 Function overview

W600 integrates the SDIO device interface, as a slave device, completes the data interaction with the host. A 1024byte asynchronous FIFO is integrated internally to complete the data interaction between the host and the chip.

## 11.2 Main Features

- -Compatible with SDIO card specification 2.0
- -Support host speed 0~50MHz
- -Supports blocks up to 1024 bytes
- -Support 1 bit SD and 4 bit SD mode

## 11.3 Function description

### 11.3.1 SDIO bus

The SDIO bus is similar to the USB bus. The SDIO bus also has two ends. One end is the host side and the other end is the device side. The design of HOST-DEVICE is used to simplify the design of the DEVICE. All communications are started by the HOST end. of. On the DEVICE side, as long as it can parse the HOST command, it can communicate with the HOST. The HOST of SDIO can connect to multiple DEVICEs.

In the SDIO bus definition, the DAT1 signal line is multiplexed as an interrupt line. In the 1BIT mode of SDIO, DAT0 is used to transfer data, and DAT1 is used as an interrupt line. In the 4BIT mode of SDIO, DAT0-DAT3 are used to transmit data, and DAT1 is multiplexed as an interrupt line.

### 11.3.2 SDIO commands

On the SDIO bus, the HOST side initiates the request, and then the DEVICE side responds to the request. The request and response will contain data information:

- -Command: The command used to start transmission is sent from the HOST end to the DEVICE end, and the command is sent through the CMD signal line;
- -Response: The response is returned by DEVICE as a response to Command. It is also transmitted through the CMD line;
- -Data: Data is transmitted in both directions. It can be set to 1-wire mode or 4-wire mode. Data is transmitted through the DAT0-DAT3 signal line.

For each operation of SDIO, HOST initiates a CMD on the CMD line. For some CMDs, DEVICE needs to return a Response, while others do not.
For the read command, HOST will first send a command to DEVICE, and then DEVICE will return a handshake signal. At this time, when HOST receives the response handshake signal, it will place the data on the 4-bit data line. At the same time, a CRC check code will be followed. When the entire read transfer is completed, HOST will send another command to notify DEVICE that the operation is complete, and DEVICE will return a response at the same time.

For write commands, HOST will first send a command to DEVICE, and then DEVICE will return a handshake signal. At this time, when HOST receives the response handshake signal, it will place the data on the 4-bit data line. At the same time, a CRC check code will be followed. When the entire write transfer is completed, HOST will send another command to notify DEVICE that the operation is complete, and DEVICE will return a response at the same time.

### 11.3.3 SDIO internal storage

The SDIO device has a fixed memory map, including general information area (CIA) and special function area (function unique area).
The registers in the CIA include I/O port functions, interrupt generation and port work information. You can perform related operations on the registers defined by the CIA by reading and writing function 0. The CIA contains three aspects of information including CCCR, FBR and CIS. Among them, CCCR defines SDIO card
The host can check the SDIO card and operate the port by operating CCCR. The address of CCCR
It is 0X00-0XFF. FBR defines the operations from port function 1 to port function 7 supported, including the requirements and functions of each port,
For power control, etc., the address of FBR is 0Xn00-0Xnff (where n is the functional port number). CIS defines some information structure of the card. The address is 0X1000-0X17FFF. CIS has public CIS and each functional port's respective CIS. The initial address of public CIS is in the CIS Pointer field of CCCR, and the CIS of each port function is in each functional port. In the CIS Pointer domain of FBR.
The memory map of CIA is shown below.

![image-20201026154009733](image-20201026154009733.png)

Refer to the following for the description of each register in the CIA. To learn more about CIA, please refer to the SDIO protocol specification.

## 11.4 Register description

### 11.4.1 Register List

### 11.4.2 SDIO Fn0 register

The Fn0 register is a register specified by the SDIO protocol, and its address range is: 0x00000~0x1FFFF, 128K in total. The starting address is 0x00000.
The Fn0 register is accessed by the SDIO host through the CMD52 command, the offset address is the access address, and the function number is 0.

![image-20201026154111125](image-20201026154111125.png)

![image-20201026154122523](image-20201026154122523.png)

#### 11.4.2.1 SDIO CCCR register and FBR1 register list

![image-20201026154317545](image-20201026154317545.png)
![image-20201026154442594](image-20201026154442594.png)
![image-20201026154538339](image-20201026154538339.png)
![image-20201026154649503](image-20201026154649503.png)
![image-20201026154722072](image-20201026154722072.png)
![image-20201026154813944](image-20201026154813944.png)
![image-20201026154849703](image-20201026154849703.png)
![image-20201026154925039](image-20201026154925039.png)
![image-20201026154953459](image-20201026154953459.png)
![image-20201026155041063](image-20201026155041063.png)
![image-20201026155057832](image-20201026155057832.png)
![image-20201026155124246](image-20201026155124246.png)
![image-20201026155147575](image-20201026155147575.png)
![image-20201026155215701](image-20201026155215701.png)
![image-20201026155239552](image-20201026155239552.png)

### 11.4.3 SDIO Fn1 register

The Fn1 register is the address space allocated to function1 by the SDIO protocol, and its address range is: 0x00000~0x1FFFF, 128K in total. Since the internal AHB bus address width of the chip is 32 bits, SDIO cannot use the 17-bit address to directly access the chip. Therefore, in the design, an address mapping needs to be completed. The specific mapping relationship is as follows: (FN1 access space)

![image-20201026155353038](image-20201026155353038.png)

The driver should avoid accessing the space beyond the above range. Doing so may bring unexpected results.

The first address space register is inside SDIO and can only be accessed by SDIO HOST; access to other address spaces will be mapped to other spaces inside the chip according to the description.

This section only introduces the registers in the SDIO 0x0000 ~ 0x00FF address space. These registers are directly accessed by the SDIO host through the CMD52 command. The offset address is the access address and the function number is 1.

![image-20201026155449985](image-20201026155449985.png)
![image-20201026155535851](image-20201026155535851.png)
![image-20201026155603248](image-20201026155603248.png)

#### 11.4.3.1 SDIO AHB interface slave device register

The following registers are used when the SDIO slave device is initialized.
When transmitting data, it needs to be used in conjunction with the wrapper controller. For parts of the wrapper controller, refer to the HSPI part of the documentation.

![image-20201026155644742](image-20201026155644742.png)
![image-20201026155708345](image-20201026155708345.png)
![image-20201026155733036](image-20201026155733036.png)
![image-20201026155806243](image-20201026155806243.png)
![image-20201026155829446](image-20201026155829446.png)
![image-20201026160016206](image-20201026160016206.png)
![image-20201026160044998](image-20201026160044998.png)
![image-20201026160138377](image-20201026160138377.png)
![image-20201026160229882](image-20201026160229882.png)

# 12. HSPI/SDIO Wrapper controller

## 12.1 Function overview

Cooperate with the interface controller (SDIO and HSPI) to complete the DMA operation of data between the host and the internal cache of the chip. Including the software and hardware interactive control of the upstream and downstream data buffers, the filling and releasing of the sending and receiving buffers, the generation of the upstream data interruption and so on.

Both SDIO and HSPI exchange data with the host computer through the wrapper controller, and their control commands and processes are the same. For the convenience of description, some registers are prefixed with SDIO. The corresponding register operations are also applicable to HSPI

It should be noted that the prefix is the SDIO_TX related register, which controls the device to receive data, and the SDIO_RX related register, which controls the device to send data.

For the cmd field in the register, it is only distinguished from the data frame from the description. It does not mean that the command channel can only transmit commands.
Used to transfer data. The difference between command and data here is that the command channel has only one buffer area, and the buffer length is generally less than
256 bytes, and the data channel has multiple buffer areas, and the length of each buffer area exceeds 1K. Multiple buffers form a linked list structure, with
The body length is configured by software. Due to the linked list buffer structure of the data frame, the transmission rate will be faster than the command channel.

## 12.2 Main features

- -Support word-aligned data movement
- -Support DMA function
- -Support linked list structure management
- -Support interrupt generation
- -Up to 4096 bytes of data can be received

## 12.3 Function description

### 12.3.1 Uplink data receiving function

The upstream direction refers to the direction in which the master device (SDIO or HSPI) sends data to the slave device (W600).

When the master device sends data to the slave device, after the SDIO or HSPI module receives the data, it will link the data to the receiving BD through WRAPPER, and generate an interrupt to notify the application software to process the data.

Receive BD descriptor:

![image-20201026160515178](image-20201026160515178.png)

When the SDIO module or HSPI module of W600 detects that the receive enable is valid, it reads RXBD and judges the Vld flag.

### 12.3.2 Downlink data transfer function

When W600 has data to send data to the master device, the software first prepares the sending description, and then informs WRAPPER to move the data. WRAPPER informs the master device to read the device to be sent through the interrupt signal of SDIO or HSPI. After the transmission is completed, WRAPPER generates a transmission completion interrupt notification program.

Send BD descriptor:

![image-20201026160559728](image-20201026160559728.png)

## 12.4 Register description

### 12.4.1 Register List

![image-20201026160700378](image-20201026160700378.png)
![image-20201026160716571](image-20201026160716571.png)

### 12.4.2 WRAPPER interrupt status register

![image-20201026160801887](image-20201026160801887.png)

## 12.4.3 WRAPPER interrupt configuration register

![image-20201026160823851](image-20201026160823851.png)

### 12.4.4 WRAPPER Uplink command ready register

![image-20201026160845734](image-20201026160845734.png)

### 12.4.5 WRAPPER Downlink command buf ready register

![image-20201026160913877](image-20201026160913877.png)
![image-20201026160928643](image-20201026160928643.png)

### 12.4.6 SDIO TX Link Enable Register

![image-20201026160959164](image-20201026160959164.png)

### 12.4.7 SDIO TX Link Address Register

![image-20201026161020789](image-20201026161020789.png)

### 12.4.8 SDIO TX Enable Register

![image-20201026161043614](image-20201026161043614.png)

### 12.4.9 SDIO TX Status Register

![image-20201026161104468](image-20201026161104468.png)

### 12.4.10 SDIO RX Link Enable Register

![image-20201026161125094](image-20201026161125094.png)

### 12.4.11 SDIO RX link address register

![image-20201026161150589](image-20201026161150589.png)

### 12.4.12 SDIO RX enable register

![image-20201026161219492](image-20201026161219492.png)
![image-20201026161237097](image-20201026161237097.png)

### 12.4.13 SDIO RX Status Register

![image-20201026161307293](image-20201026161307293.png)

### 12.4.14 WRAPPER CMD BUF base address register

![image-20201026161329708](image-20201026161329708.png)

### 12.4.15 WRAPPER CMD BUF SIZE register

![image-20201026161355620](image-20201026161355620.png)

# 13. SPI controller

## 13.1 Function overview

SPI is the abbreviation of Serial Peripheral Interface. SPI is a high-speed, full-duplex, and synchronous communication bus. The communication principle of SPI is very simple. It works in a master-slave mode. This mode usually has a master device and one or more slave devices.
There are less 4 wires, in fact 3 wires are also available (for unidirectional transmission), including SDI (data input), SDO (data output), SCLK (clock), CS (chip select).

## 13.2 Main Features

- -It can be used as both SPI master and SPI slave
- -The transmit and receive channels each have 8 word depth FIFO
- -The master supports 4 formats of motorola spi (CPOL, CPHA), TI timing, macrowire timing
- -The slave supports 4 formats of motorola spi (CPOL, CPHA)
- -Support full duplex and half duplex
- -The master device supports bit transmission, and the maximum supports 65535bit transmission
- -The slave device supports transmission modes of various length byte
- -The maximum clock frequency of spi_clk input from the device is 1/6 of the system APB clock

## 13.3 Function description

### 13.3.1 Master-slave configurable

The SPI controller not only supports the device as the SPI communication master device, but also supports the device as the SPI communication slave device. The master and slave roles of the device can be switched back and forth by setting Bit2 of the SPI_CFG register.

### 13.3.2 Multiple mode support

As a master device, by setting Bit1 (CPHA) and Bit0 (CPOL) of the SPI_CFG register, it can transmit data in the four formats of MOTOROLA SPI respectively. CPOL is used to determine the level of the SCK clock signal when it is idle. CPOL=0, the idle level is low, and when CPOL=1, the idle level is high. CPHA is used to determine the sampling time, CPHA=0, sampling at the first clock edge of each cycle, CPHA=1, sampling at the second clock edge of each cycle. You can also set the TRANS_MODE register to set the master device to transmit data in TI timing or microwire timing. The length of the transmitted data under both timings is adjustable.

As a slave device, it only supports the four formats of MOTOROLA SPI, and the format selection is also achieved by setting the same registers as when acting as a master device.

### 13.3.3 Efficient data transmission

FIFO memory is a first-in-first-out dual-port buffer, that is, the first data that enters it is removed first, and one of the memory
The input port, the other port is the output port of the memory. The SPI controller integrates two (one for each transceiver) FIFO memory with a depth of 8 words to increase the data transmission rate, process a large number of data streams, and match systems with different transmission rates, thereby improving system performance. The trigger level of RXFIFO and TXFIFO can be set by setting Bit[8:6] and Bit[4:2] of the MODE_CFG register to meet the performance requirements under different transmission rates. After the trigger level of FIFO is triggered, interrupt or DMA can be triggered to move data from memory to TXFIFO or move data from RXFIFO to memory.

## 13.4 Register description

### 13.4.1 Register List

![image-20201026161656092](image-20201026161656092.png)

### 13.4.2 Channel Configuration Register

![image-20201026161725073](image-20201026161725073.png)
![image-20201026161755820](image-20201026161755820.png)
![image-20201026161906834](image-20201026161906834.png)
![image-20201026161933152](image-20201026161933152.png)
![image-20201026161957528](image-20201026161957528.png)

### 13.4.3 SPI Configuration Register

![image-20201026162053039](image-20201026162053039.png)
![image-20201026162113253](image-20201026162113253.png)
![image-20201026162229693](image-20201026162229693.png)
![image-20201026162259924](image-20201026162259924.png)
![image-20201026162341568](image-20201026162341568.png)
![image-20201026162402055](image-20201026162402055.png)

### 13.4.4 Clock Configuration Register

![image-20201026162442473](image-20201026162442473.png)

### 13.4.5 Mode Configuration Register

![image-20201026162528161](image-20201026162528161.png)
![image-20201026162551559](image-20201026162551559.png)

### 13.4.6 Interrupt Control Register

![image-20201026162713477](image-20201026162713477.png)
![image-20201026162739690](image-20201026162739690.png)
![image-20201026162801846](image-20201026162801846.png)

### 13.4.7 Interrupt Status Register

![image-20201026162853352](image-20201026162853352.png)
![image-20201026162916940](image-20201026162916940.png)
![image-20201026162939932](image-20201026162939932.png)

### 13.4.8 SPI Status Register

![image-20201026163041826](image-20201026163041826.png)
![image-20201026163053659](image-20201026163053659.png)

### 13.4.9 SPI Timeout Register

![image-20201026163122016](image-20201026163122016.png)

### 13.4.10 Data Transmission Register

![image-20201026163151896](image-20201026163151896.png)
![image-20201026163201418](image-20201026163201418.png)

### 13.4.11 Transfer Mode Register

![image-20201026163248878](image-20201026163248878.png)
![image-20201026163319522](image-20201026163319522.png)
![image-20201026163343830](image-20201026163343830.png)
![image-20201026163401049](image-20201026163401049.png)

### 13.4.12 Data Length Register

![image-20201026163438294](image-20201026163438294.png)

### 13.4.13 Data Receive Register

![image-20201026163458201](image-20201026163458201.png)

# 14. I2C controller

## 14.1 Function overview

The I2C bus is a simple, bidirectional two-wire synchronous serial bus. It only needs two wires to transmit between devices connected to the bus
information.

The master device is used to start the bus to transmit data and generate a clock to open the device for transmission. At this time, any addressed device is regarded as a slave device. The relationship between master and slave, sending and receiving on the bus is not constant, but depends on the data transfer direction at this time. If the host wants to send data to the slave device, the host first addresses the slave device, then actively sends the data to the slave device, and finally the host terminates the data transfer; if the host wants to receive data from the slave device, the master device first addresses the slave device. Then the host receives the data sent from the device, and finally the host terminates the receiving process. under these circumstances. The host is responsible for generating the timing clock and terminating data transmission.

## 14.2 Main Features

- -APB bus protocol standard interface
- -Can only be used as a master device controller
- -I2C working rate can be configured, 100KHz~400KHz
- -Multiple GPIOs can be multiplexed into I2C communication interface
- -Quickly output and detect timing signals

# 14.3 Function description

### 14.3.1 Transmission rate selection

By setting the register PRERlo and the register PRERhi, the data transmission rate on the I2C bus can be configured from 100KHz to 100KHz.
The integer division value of any bus frequency between 400KHz.

### 14.3.2 Interrupt and start and stop controllable

The I2C controller can be enabled or disabled by setting Bit6 of the register CTR to generate interrupts, and the I2C controller can be started or stopped at any time by setting Bit7.

### 14.3.3 Fast output and detection signal

The controller can quickly output or detect the bus START signal, bus STOP signal, bus ACK signal, and bus NACK signal by setting the corresponding bit of the register CR_SR. In master mode, the I2C interface initiates data transfer and generates a clock signal. A serial data transmission always starts with a start signal and ends with a stop signal. Once the start signal is generated on the bus, the master mode is selected.

## 14.4 Register description

### 14.4.1 Register List

![image-20201026163718688](image-20201026163718688.png)

### 14.4.2 Clock divider register_1

![image-20201026163745786](image-20201026163745786.png)

### 14.4.3 Clock divider register_2

![image-20201026163808151](image-20201026163808151.png)
![image-20201026163818918](image-20201026163818918.png)

### 14.4.4 Control Register

![image-20201026163900238](image-20201026163900238.png)

### 14.4.5 Data Register

![image-20201026163919849](image-20201026163919849.png)

### 14.4.6 Transceiver Control Register

![image-20201026163959800](image-20201026163959800.png)
![image-20201026164049114](image-20201026164049114.png)
![image-20201026164112992](image-20201026164112992.png)

### 14.4.7 TXR read register

![image-20201026164204584](image-20201026164204584.png)
![image-20201026164216020](image-20201026164216020.png)

### 14.4.8 CR readout register

![image-20201026164242080](image-20201026164242080.png)

# 15. I2S controller

## 15.1 Function overview

I2S (Inter-IC Sound) is a bus standard for audio data transmission between digital audio equipment (such as CD players, digital sound processors, digital TV sound systems). It adopts the design of independent wires to transmit clock and data signals. By separating data and clock signals, it avoids the distortion induced by time difference and saves users the cost of purchasing professional equipment that resists audio jitter. The standard I2S bus cable is composed of 3 serial wires: 1 is a time division multiplexing (TDM) data wire; 1 is a word selection wire; 1 is a clock wire.

## 15.2 Main Features

- -Implement I2S interface, support I2S and PCM protocol
- -Support amba APB bus interface, 32bit single read and write operations
- -Support master-slave mode
- -Support 8, 16, 24, 32 bit wide, the highest sampling frequency is 128KHz
- -Support mono and stereo modes
- -Compatible with I2S and MSB justified data formats, compatible with PCM A/B format
- -Support DMA request read and write operations, only support word operations

## 15.3 Function description

### 15.3.1 Multiple mode support

You can set the data format to I2S format, MSB justified format, PCM A format, or PCM B format by setting Bit[25:24] of the I2S Control register; you can select mono or stereo by setting Bit[22] of the I2S Control register mode. The bit width of the data transmission word can be set by setting Bit[5:4] of the I2S Control register, which can be set to 8bit, 16bit, 24bit, 32bit.

### 15.3.2 Zero Crossing Detection

By setting Bit[17:16] of the I2S Control register, you can set whether to enable the zero-crossing detection function of the left and right channels; by setting Bit[9:8] of the I2S_IMASK register, you can set whether the zero-crossing detection function of the left and right channels generates an interrupt. If the detection function is enabled and the interrupt is enabled, when a zero-crossing phenomenon is detected, the program will execute the interrupt subroutine, and the corresponding bit of the I2S_INT_FLAG register Bit[9:8] will be set to 1.

### 15.3.3 Efficient data transmission

FIFO memory is a first-in-first-out dual-port buffer, that is, the first data that enters it is removed first. One of the memory's input ports and the other is the memory's output port. The I2S controller integrates two FIFO memories with a depth of 8 words (one for each transceiver) to increase the data transmission rate, process a large number of data streams, and match systems with different transmission rates, thereby improving system performance. The trigger level of RXFIFO and TXFIFO can be set by setting Bit[14:12] and Bit[11:9] of the I2S Control register to meet the performance requirements under different transmission rates. After the trigger level of FIFO is triggered, interrupt or DMA can be triggered to move data from memory to TXFIFO or move data from RXFIFO to memory.

## 15.4 Register description

### 15.4.1 Register List

![image-20201026164819475](image-20201026164819475.png)

### 15.4.2 Control Register

![image-20201026164944875](image-20201026164944875.png)
![image-20201026165012373](image-20201026165012373.png)
![image-20201026165114236](image-20201026165114236.png)
![image-20201026165149496](image-20201026165149496.png)
![image-20201026165235524](image-20201026165235524.png)
![image-20201026165313985](image-20201026165313985.png)

### 15.4.3 Interrupt Mask Register

![image-20201026165427423](image-20201026165427423.png)
![image-20201026165453765](image-20201026165453765.png)
![image-20201026165616855](image-20201026165616855.png)
![image-20201026165638216](image-20201026165638216.png)

### 15.4.4 Interrupt Flag Register

![image-20201026165911031](image-20201026165911031.png)
![image-20201026170011695](image-20201026170011695.png)
![image-20201026170028859](image-20201026170028859.png)
![image-20201026170146414](image-20201026170146414.png)
![image-20201026170200831](image-20201026170200831.png)

### 15.4.5 Status Register

![image-20201026170238247](image-20201026170238247.png)

### 15.4.6 Data Transmission Register

![image-20201026170306349](image-20201026170306349.png)

# 16. UART module

## 16.1 Function overview

UART is a universal serial data bus used for asynchronous communication. The bus supports two-way communication and can realize full-duplex transmission and reception.

W600 has 2 groups of ordinary UART ports (uart0 and uart1). Various baud rate settings can be achieved through fine clock division combination, and the maximum communication rate is 2Mbps. W600 UART can be used in conjunction with hardware DMA to realize efficient asynchronous data transmission.

## 16.2 Main Features

- -Comply with APB bus interface protocol, full duplex asynchronous communication mode
- -Support interrupt or polling working mode
- -Support DMA Byte transmission mode, send and receive each 32-byte FIFO
- -Programmable baud rate, maximum support 2Mbps
- -5-8bit data length, and parity polarity can be configured
- -1 or 2 stop bits can be configured
- -Support RTS/CTS flow control
- -Support Break frame sending and receiving
- -Support Overrun, parity error, frame error, rx break frame interrupt indication

## 6.3 Function description

### 16.3.1 UART baud rate

Asynchronous communication does not have the same clock source for reference on both sides, so both parties need to send and receive data at the negotiated baud rate. W600 can realize fine baud rate control through the baud rate setting register BAUD_RATE_CTRL register. BAUD_RATE_CTRL[15:0] is named ubdiv, BAUD_RATE_CTRL[19:16] is named ubdiv_frac, the wave that needs to be set
Baudrate, the calculation formula is as follows:
ubdiv = apbclk / (16 * baudrate) – 1 //Take an integer
ubdiv_frac = (apbclk% (baudrate * 16)) / baudrate // take an integer
Take APB clock 40MHz, baud rate 19200bps as an example:
ubdiv = 40000000 / (16 * 19200) – 1 = 129
ubdiv_frac = (40000000% (19200* 16)) / 19200 = 3
According to the above formula to calculate the APB clock 40MHz and the baud rate is 19200bps, the baud rate register should be set as:
BAUD_RATE _CTRL = (3<<16) | 129 = 0x0003_0081.

### 16.3.2 UART data format

- Data length
  The UART of W600 supports configurable data lengths of 5bit, 6bit, 7bit, and 8bit. The definition of data length is as follows:

![image-20201026170629631](image-20201026170629631.png)

Normal UART communication consists of 1bit start bit, 1bit stop bit and the middle data bit, and the middle data bit is configurable. W600 supports 5bit, 6bit, 7bit, 8bit 4 kinds of length data bits can be configured. Choose the data bit length according to the actual application.

- Stop bit
  The UART of W600 supports 1bit stop bit and 2bit stop bit configurable, which can be configured according to actual needs, as follows:

![image-20201026170710029](image-20201026170710029.png)

- Parity bit
  The function of the parity bit is to check the correctness of the data. W600 can set odd, even and no check.
  The calculation method of odd parity: If the number of current data bit 1 is odd, the odd parity bit is 0; if the number of current data 1 is even, the odd parity bit is 1. In short, an odd number of ones is guaranteed.
  The calculation method of even parity: If the current data bit 1 is an odd number, the even parity bit is 1, and if the current data bit 1 is an even number, the even parity bit is 0. In short, an even number of ones is guaranteed.

![image-20201026170802846](image-20201026170802846.png)

### 16.3.3 UART hardware flow control

W600 UART supports hardware flow control in RTS/CTS mode. The main purpose of flow control is to prevent the data in UART fifo from being lost because the software is too late to process. RTS and CTS are used correspondingly, as shown in the figure below:

![image-20201026170834702](image-20201026170834702.png)

The hardware flow control of W600 is controlled by the AUTO_FLOW_CTRL register. When hardware flow control AUTO_FLOW_CTRL[0]
When it is 1, W600 will set the flow control according to the number of data in rxfifo set by AUTO_FLOW_CTRL[4:2]. If the number is greater than the set number, RTS will be pulled high, and other devices will no longer send data to W600. A certain number of RTS is pulled down, and other devices continue to send data to W600. When AUTO_FLOW_CTRL[0] is 0, the software sets the level of RTS through AUTO_FLOW_CTRL[1].

When W600 sends data, it can judge whether the current CTS has changed through interrupts, and query the CTS status through FIFO_STATUS[12] to determine whether to continue sending data to other devices.

### 16.3.4 UART DMA transfer

The UART of W600 supports DMA transfer mode. During DMA transfer, you need to configure the DMA_CTRL register in the UART register list to enable the DMA of the UART. At the same time, you need to configure UART_FIFO_CTRL to configure how many bytes are left in txfifo and rxfifo to trigger DMA transfer.

The source or destination address of DMA is set to TX_DATA_WINDOW or RX_DATA_WIDNOW. For the setting of other DMA registers, please refer to the DMA register chapter.

Note: UART DMA transfer can only be set to Byte mode, half_word and word transfer modes are not supported.

### 16.3.5 UART Interrupt

UART supports interrupt operation modes, including fifo empty, fifo reaching the set trigger value, CTS change, error, etc. will generate UART interrupt. The required interrupt can be set through the INT_MASK register.
After the UART interrupt is generated, the current interrupt status can be queried through INT_SRC and the cause of the interrupt is triggered. Software write 1 to clear 0.

## 16.4 Register description

### 16.4.1 Register List

![image-20201026172122850](image-20201026172122850.png)

### 16.4.2 Data Flow Control Register

![image-20201026172157454](image-20201026172157454.png)
![image-20201026172225967](image-20201026172225967.png)

### 16.4.3 Automatic hardware flow control register

![image-20201026172304559](image-20201026172304559.png)

### 16.4.4 DMA setting register

![image-20201026172343348](image-20201026172343348.png)
![image-20201026172412928](image-20201026172412928.png)

### 16.4.5 FIFO Control Register

![image-20201026172954703](image-20201026172954703.png)

#### 16.4.6 Baud rate control register

![image-20201026173343079](image-20201026173343079.png)
![image-20201026173408050](image-20201026173408050.png)

### 16.4.7 Interrupt Mask Register

![image-20201026173445917](image-20201026173445917.png)

### 16.4.8 Interrupt Status Register

![image-20201026173524267](image-20201026173524267.png)
![image-20201026173549818](image-20201026173549818.png)

### 16.4.9 FIFO Status Register

![image-20201026173629651](image-20201026173629651.png)

### 16.4.10TX start address register

![image-20201026174339171](image-20201026174339171.png)
![image-20201026174801649](image-20201026174801649.png)

### 16.4.11 RX Start Address Register

![image-20201026175152044](image-20201026175152044.png)

# 17. UART&7816 module

## 17.1 Function overview

UART&7816 module is compatible with UART function and 7816 interface function.

W600 supports 1 set of UART&7816 multiplexing interface (uart2). When used as UART, various baud rate settings can be realized through fine clock frequency division combination, and the maximum communication rate is 2Mbps.

The W600 UART&7816 interface can be used with hardware DMA to realize efficient data transmission.

## 17.2 Main Features

- Comply with APB bus interface protocol, support UART asynchronous full-duplex and 7816 asynchronous half-duplex communication modes;

  - -Support interrupt or polling work mode;
- -Support DMA Byte transmission mode, send and receive each 32-byte FIFO;
  - -Serial port function:
- -Programmable baud rate, maximum support 2Mbps
  - -5-8bit data length, and parity polarity can be configured
- -1 or 2 stop bits can be configured
  - -Support RTS/CTS flow control
- -Support Break frame sending and receiving
  - -Support Overrun, parity error, frame error, rx break frame interrupt indication

- 7816 interface function:
  - -Compatible with ISO-7816-3 T=0.T=1 mode
  - -Compatible with EVM2000 protocol
  - -Configurable guard time (11 ETU-267 ETU)
  - -Forward/reverse agreement, software configurable
  - -Support send/receive parity check and retransmission function
  - -Support 0.5 and 1.5 stop bits configurable


## 17.3 UART function description

Refer to Chapter 16 UART Function Module Description.

## 17.4 7816 functional description

### 17.4.1 7816 Introduction

ISO7816 is an international standard smart card protocol. The protocol specifies smart card physical characteristics, dimensions and interfaces, electrical signals and transmission protocols, commands, and security.

W600 mainly implements the ISO 7816-3 electrical signal and transmission protocol, and supports T0 and T1 cards. Through the 7816 interface of W600, users can not care about the signal communication logic of clock and data, and can directly interact with the smart card for data and commands. Regarding smart card data and command interaction, users need to refer to the ISO7816-4 protocol to implement.

### 17.4.2 7816 interface

W600 mainly integrates two interfaces of smart card clock and data to realize the communication electrical signal logic of data and commands. In actual smart card applications, there are three signals, RST, VCC, and GND. RST can be controlled by ordinary GPIO, which is mainly used when the smart card is powered on and reset. VCC can be directly connected to a 3.3V power supply, or through GPIO with other circuits to control the on and off of the smart card VCC.

![image-20201026175731550](image-20201026175731550.png)

### 17.4.3 7816 Configuration

When used as a 7816 interface, relevant configuration is required:

- -Set the interface working mode, UART_LIN_CTRL[24] is set to 1, and the current interface is selected as 7816 mode;
- -Set 7816 MSB or LSB transmission mode, UART_LIN_CTRL[3] is set to 1, through UART_LIN_CTRL[3] to choose whether the 7816 interface is in MSB mode (bit7 is transmitted first) or LSB mode (bit0 is transmitted first);
- -Set stop bits, UART_LIN_CTRL[2] can choose 0.5 or 1.5 stop bits for smart card;
- -Select the card type, UART_LIN_CTRL[8] can select T0 card or T1 card;
- -Configure the smart card communication timeout time, set the timeout time through WAIT_TIME, and the data is not received when the data is received overtime a timeout interrupt is generated.

### 17.4.4 7816 Clock Configuration

The smart card clock refers to the clock provided to the smart card through the CLK pin, which is set by BAUD_RATE_CTRL[21:16]. The calculation method is as follows:

![image-20201026180626422](image-20201026180626422.png)

fsc_clk: CLK that needs to be provided to the smart card;
fclk_apb: system APB bus clock;
clk_div: The clock division factor that needs to be set to BAUD_RATE_CTRL[21:16]
Because clk_div can only take integers, in order to reduce the error, we'd better adopt the calculation method of rounding. C language calculation will lose the decimal part when rounding. The conversion method of C language rounding is as follows:
clk_div = (fclk_apb + fsc_clk)/(2 * fsc_clk)-1;

### 17.4.5 7816 rate setting

There is a time unit ETU in the smart card, and the smart card transmits data and commands according to this time unit. The setting of ETU is set by BAUD_RATE_CTRL[15: 0], the calculation method is as follows:

![image-20201026180714660](image-20201026180714660.png)

f: the CLK of our smart card;
Both F and D are parameters given by the smart card.
In fact, the ubdiv of BAUD_RATE_CTRL[15: 0] we need to set is F/D. The above formula is only for calculating ETU for your reference. When we actually set it, we only need to set ubdiv = F/D. F and D can be queried by the following table.

![image-20201026180956701](image-20201026180956701.png)

### 17.4.6 7816 Power-on Reset

![image-20201026181020130](image-20201026181020130.png)

The figure above is the timing diagram of the smart card power-on reset. The initial state of CLK and IO is low, we need to configure it to GPIO mode and pull it low. After VCC is pulled high, CLK and IO are configured to 7816 mode and then controlled by 7816. Finally, we need to manually pull the RST pin high to complete the reset process. The configuration steps are as follows:

- -I/O, CLK, RST are configured as normal GPIO mode and kept low;
- -Set 7816 to T=0 mode;
- -Control VCC power on through GPIO;
- -Configure I/O and CLK to 7816 mode, and 7816 drives clock and data;
- -Configure 7816 clock frequency and allow clock output;
- -Set the RST pin and wait to receive ATR data. If ATR data is not received within 40,000 clocks, the deactivation process will be executed.
- -The card is deactivated.

### 17.4.7 7816 Warm reset

![image-20201026181131887](image-20201026181131887.png)

As shown in the figure above, the process of warm reset is very simple. In normal working mode, pull the RST pin low for 400 cycles. The configuration steps are as follows:

- -Keep VCC powered on;
- -Pull down the RST pin for at least 400 clock cycles;
- -Pull the RST pin high and wait for ATR data to be received. If ATR data is not received within40,000 clocks, the deactivation process will be executed.
- -The card is deactivated.

### 17.4.8 7816 Inactivation process

![image-20201026181213642](image-20201026181213642.png)

As shown in the figure above, after RST is pulled low, CLK and IO need to be configured as normal IO mode and pulled low, and finally the VCC power supply is turned off.
The steps are as follows:

- -Keep VCC powered on;
- -Pull down the RST pin;
- -Configure CLK and IO as GPIO mode and pull it low;
- -Control VCC power down through GPIO;

### 17.4.9 7816 Data Transmission

The sequence of 7816 data transmission has been completed by W600 hardware, no user operation is required. If the user wants to know the specific content of this part,
Please refer to the provisions in the ISO7816-3 protocol.

![image-20201026181258567](image-20201026181258567.png)

### 17.4.10UART&7816 DMA transfer

W600's UART&7816 supports DMA transfer mode. During DMA transfer, you need to configure the DMA_CTRL register in the UART&7816 register list to enable UART DMA. At the same time, you need to configure UART_FIFO_CTRL to configure how many bytes remaining in txfifo and rxfifo trigger DMA transfer.
The source or destination address of DMA is set to TX_DATA_WINDOW or RX_DATA_WIDNOW. For the setting of other DMA registers, refer to the DMA register chapter.

Note: UART&7816 DMA transmission can only be set to Byte mode, half_word and word transmission modes are not supported.

### 17.4.11UART&7816 interrupt

UART&7816 supports interrupt operation modes, including fifo empty, fifo reaching the set trigger value, CTS change, error, etc. will generate UART&7816 interrupt. You can set the required interrupt through the INT_MASK register.

After the UART&7816 interrupt is generated, the current interrupt status can be queried through INT_SRC, and the cause of the interrupt is triggered. Software write 1 to clear 0.

## 17.5 Register description

### 17.5.1 Register List

![image-20201026182117621](image-20201026182117621.png)
![image-20201026182142688](image-20201026182142688.png)

### 17.5.2 Data Flow Control Register

![image-20201026182413319](image-20201026182413319.png)
![image-20201026182437741](image-20201026182437741.png)
![image-20201026182452959](image-20201026182452959.png)

### 17.5.3 Automatic hardware flow control register

![image-20201026182537422](image-20201026182537422.png)
![image-20201026182558897](image-20201026182558897.png)

### 17.5.4 DMA Setting Register

![image-20201026182635476](image-20201026182635476.png)

### 17.5.5 FIFO Control Register

![image-20201026182726435](image-20201026182726435.png)
![image-20201026182901415](image-20201026182901415.png)

### 17.5.6 Baud Rate Control Register

![image-20201026182928757](image-20201026182928757.png)

### 17.5.7 Interrupt Mask Register

![image-20201026182950438](image-20201026182950438.png)

### 17.5.8 Interrupt Status Register

![image-20201026183024792](image-20201026183024792.png)
![image-20201026183045848](image-20201026183045848.png)

### 17.5.9 FIFO Status Register

![image-20201026183122265](image-20201026183122265.png)

### 17.5.10 TX Start Address Register

![image-20201026183142187](image-20201026183142187.png)

### 17.5.11 RX Start Address Register

![image-20201026183203610](image-20201026183203610.png)

### 17.5.12 7816 Guard Time Register

![image-20201026183230114](image-20201026183230114.png)

### 17.5.13 7816 Timeout Time Register

![image-20201026183307990](image-20201026183307990.png)

# 18. Timer module

## 18.1 Function overview

The timer contains a 32-bit auto-loaded counter, which is driven by the system clock after frequency division. W600 has 6 completely independent timers. Realize precise timing time and interrupt function, which can be used for delay or periodic event processing.

## 18.2 Main Features

-6 completely independent timers

-32-bit auto load counter

-The timing unit can be configured as ms, us

-Single timing or repeat timing function can be realized

-Timer interrupt function

## 18.3 Function description

The timer module consists of 6 completely independent timers, which do not affect each other, and 6 channels can work at the same time.

The system clock is divided by the frequency division coefficient to obtain the us standard clock, which is used as the input clock of the counter. The timing unit can be configured to two levels: us and ms.

The timing value is a 32-bit configurable register that can meet the needs of different timing durations. Each timer corresponds to an interrupt. When the timing time is met, if the interrupt function is enabled, an interrupt request will be generated, which can be used to process periodic events.

### 18.3.1 Timing function

The timing function means that according to the user set time, when the time is up, a hardware interrupt is generated to notify the user to implement a specific function. Timing trigger supports two types: single and periodic. One can be used to process single events, and the other can be used to process periodic events.
The user obtains the APB bus clock frequency according to the frequency division factor of the system clock, sets the timer's reference microsecond count configuration register (TMR_CONFIG), sets the timing value, configures the timing unit, working mode, enables interrupts, and then starts the timing function. When the time is up, the program enters the timer interrupt processing function to clear the interrupt.

### 18.3.2 Delay function

Delay function means that the user can keep the program in a waiting state according to the countdown function of the timer, and the program will not continue to run until the timing is completed.

## 18.4 Register description

### 18.4.1 Register List

![image-20201026183505248](image-20201026183505248.png)

### 18.4.2 Standard us configuration register

![image-20201026183528680](image-20201026183528680.png)

### 18.4.3 Timer Control Register

![image-20201026183618433](image-20201026183618433.png)
![image-20201026183630480](image-20201026183630480.png)

### 18.4.4 Timer 1 timing value configuration register

![image-20201026183706686](image-20201026183706686.png)

### 18.4.5 Timer 2 Timing Value Configuration Register

![image-20201026183753367](image-20201026183753367.png)

### 18.4.6 Timer 3 Timing Value Configuration Register

![image-20201026183816016](image-20201026183816016.png)

### 18.4.7 Timer 4 Timing Value Configuration Register

![image-20201026183839055](image-20201026183839055.png)

### 18.4.8 Timer 5 Timing Value Configuration Register

Table 168 Timer 5 timer value configuration register

![image-20201026183916542](image-20201026183916542.png)

### 18.4.9 Timer 6 Timing Value Configuration Register

![image-20201026183941562](image-20201026183941562.png)

# 19. Power Management Module

## 19.1 Function overview

PMU realizes the switching of chip hardware working state and power management during the state switching process, and provides timer, real-time clock and 32K clock at the same time.

## 19.2 Main Features

- -Provide chip power control
- -Provide timer function
- -Provide real-time clock control
- -Provide 32K RC oscillator calibration function

## 19.3 Function description

### 19.3.1 Full chip power control

The PMU module controls the chip's power switch, including 40M start-up circuit, BandGap, digital PLL, voltage detection circuit, and digital circuit LDO.
When the chip is powered on, the PMU module guides each module to turn on the power sequentially according to the preset power-on sequence;
When the software configuration register enters the sleep mode, guide each functional module to turn off the power in turn according to the safe power-off sequence;
Three wake-up modes are provided in sleep mode: Timer wake-up, RTC wake-up or wake up by pulling the special WAKEUP pin high.

### 19.3.2 Wake-up mode

The PMU supports 3 wake-up modes, Timer wake-up, RTC wake-up and external IO wake-up.

#### Timer wake up

Before the software sets the sleep mode, configure the Timer0 module in the PMU and set the sleep time. When the system enters sleep mode, when
When Timer0 reaches the sleep time, it will wake up the system and generate a corresponding Timer interrupt. After the system resumes operation, you need to write ‘1’ to the corresponding status bit in the interrupt status register to clear the interrupt status, otherwise, it will be awakened by interrupt immediately after entering the sleep mode next time;

#### RTC wake up

Before the software sets the sleep mode, configure the RTC module in the PMU and set the sleep time. When the system enters the sleep mode, when the RTC timer reaches the sleep time, it will wake up the system and give the corresponding RTC interrupt. After the system resumes operation, please write ‘1’ to the corresponding status bit in the interrupt register 0x14 to clear the interrupt status, otherwise, it will be awakened by interrupt immediately after entering the sleep mode next time;

### External IO wake up

After the software sleeps, the PMU will detect a specific Wakeup pin, and the external controller can wake up the system by pulling this IO high and give the corresponding IO wakeup interrupt. The PMU no longer detects the IO status after leaving the sleep mode. After the system resumes operation, please write ‘1’ to the corresponding status bit in the interrupt register 0x14 to clear the interrupt status, otherwise, it will be awakened by interrupt immediately after entering the sleep mode next time;

### 19.3.3 Timer0 Timer

Configure the timer enable signal and timing time through the AHB register. First set the timer value, then set the timer enable BIT to start the timer
The timer generates an interrupt when the timer time is reached, and the software clears the interrupt flag by writing to BIT0 of the status register.

### 19.3.4 Real-time clock function

Reference real-time clock module.

### 19.3.5 32K clock source switching and calibration

The W600 chip integrates a 32K RC oscillator as the clock source of the PMU module.
Due to changes in working environment and temperature, the output frequency of the 32K RC oscillator may change, causing timing deviations. Therefore, the 32K RC oscillator calibration function and the 32K clock switching function are introduced into the PMU module to correct the timing deviation.

#### 1) Switching of 32K clock source

The 32K clock can be switched from the 32K RC oscillator to the 32K clock divided by the 40M clock by setting bit3 of the PS_CR register to 1. However, when the chip enters sleep mode, because the 40M clock will be turned off, bit3 will be automatically cleared to 0. If the firmware still needs to use the precise timing function after waking up, it needs to reset bit3 to 1.

#### 2) Calibration of 32K RC oscillator circuit

First set bit2 of PS_CR register to 0, and then set bit2 of PS_CR register to 1.
After the calibration is completed, the 32K RC oscillator will be relatively accurate. But if you want more accurate timing, it is recommended to use a 32K clock obtained by dividing the 40M clock.

## 19.4 Register description

### 19.4.1 Register List

![image-20201026184401057](image-20201026184401057.png)
![image-20201026184425163](image-20201026184425163.png)

### 19.4.2 PMU Control Register

![image-20201026184918718](image-20201026184918718.png)
![image-20201026184950840](image-20201026184950840.png)

### 19.4.3 PMU Timer 0

![image-20201026185019627](image-20201026185019627.png)

### 19.4.4 PMU interrupt source register

![image-20201026185044402](image-20201026185044402.png)

# 20. Real-time clock module

## 20.1 Function overview

RTC is a BCD counter/timer provided by the PMU module. The two 32-bit registers contain seconds, minutes, hours, day, month, and year.
The binary coded decimal format representation (BCD) can automatically correct the month of 28, 29 (leap year), 30, and 31 days.

Under the corresponding software configuration, RTC can not only provide clock and calendar function, but also can be used as a timer. When the timer reaches the set time, an RTC interrupt will be generated, which can be used to wake up the system in sleep state.

The RTC module has two clock sources that can be configured: 40M clock frequency division and internal 32K clock. It can be specifically used by software configuration during normal operation
Which clock source; only 32K clock can be used in sleep state. If the RTC clock source in the normal working state is obtained by dividing the 40M clock, it will automatically switch to the 32K clock after entering the sleep state, and the 32K clock will still be used after the system is awakened. Therefore, as long as the power supply voltage remains within the working range, the RTC module will not stop working regardless of whether the module is in a normal working state or in a sleep state.

## 20.2 Main features

- -Provide timing function
- -Provide timing function
- -Provide timing interrupt
- -Interrupt to wake up the system

## 20.3 Function description

### 20.3.1 Timing function

The initial value of day, hour, minute, and second can be configured in RTC configuration register 1, the initial value of year and month can be configured in RTC configuration register 2, and the timing function can be enabled in RTC configuration register 2.

After the RTC timer function is enabled, read the RTC configuration register 1 to get the current day, hour, minute, and second value, and read the RTC configuration register.
Set register 2 to get the current year and month values.

### 20.3.2 Timing function

The timing values of day, hour, minute, and second can be configured in RTC configuration register 1, the year and month timing values can be configured in RTC configuration register 2, and the timing function can be enabled in RTC configuration register 1.

When the RTC timer reaches the timing time, an RTC interrupt will be generated. At this time, setting the RTC interrupt bit of the PMU interrupt source register to 1 can clear the interrupt status.

When the system enters sleep mode, the interrupt generated by the RTC timer will wake up the system.

## 20.4 Register description

### 20.4.1 Register List

The RTC module has a total of two 32-bit dedicated registers, and the RTC interrupt status needs to query the PMU interrupt source register.

![image-20201027090917849](image-20201027090917849.png)

### 20.4.2 RTC Configuration Register 1

![image-20201027090951269](image-20201027090951269.png)

### 20.4.3 RTC Configuration Register 2

![image-20201027091017381](image-20201027091017381.png)

# 21. Watchdog module

## 21.1 Function overview

Realize the "watchdog" function. Designed for global reset when the system crashes.

The "watchdog" will generate a periodic interrupt. The system software will clear the interrupt flag after the interrupt is generated. If it is not cleared after its set time, it will generate a hard reset signal to reset the system.

## 21.2 Main features

- -Provide timing function
- -Provide reset function
- -Provide timing interrupt

## 21.3 Function description

### 21.3.1 Timing function

After setting the timer value to the register WD_LD, set BIT0 of WDG_CTRL to 1 to start the timer, and the WDG module will generate a timer interrupt when the time is up to notify the program to process. If the BIT0 of the WD_CLR register is not cleared, a periodic interrupt will be generated.

The value of WD_LD is based on the APB clock unit, and the APB clock is divided from the 160M clock.

### 21.3.2 Reset function

After setting the chip timing value WD_LD, start the timing and reset function (set BIT1/BIT0 of WDG_CTRL), the WDG module starts the countdown, when the timing is up, WDG will generate a timing interrupt, and if the BIT0 of WD_CLR is not cleared, the chip will be in the timing time A reset signal is generated in the next cycle.

## 21.4 Register description

### 21.4.1 Register List

![image-20201027092720172](image-20201027092720172.png)
![image-20201027092751443](image-20201027092751443.png)

### 21.4.2 WDG Timing Value Load Register

![image-20201027092823262](image-20201027092823262.png)

### 21.4.3 WDG Current Value Register

![image-20201027092844814](image-20201027092844814.png)

### 21.4.4 WDG Control Register

![image-20201027092908828](image-20201027092908828.png)

### 21.4.5 WDG Interrupt Clear Register

![image-20201027092932688](image-20201027092932688.png)

### 21.4.6 WDG Interrupt Source Register

![image-20201027092951195](image-20201027092951195.png)

### 21.4.7 WDG Interrupt Status Register

![image-20201027093012635](image-20201027093012635.png)

# 22. PWM controller

## 22.1 Function overview

PWM is a method of digitally encoding the analog signal level. Through the use of high-resolution counters, the duty cycle of the square wave is modulated to encode the level of a specific analog signal. The PWM signal is still digital, because at any given moment, the full amplitude
The DC power supply is either completely (ON) or completely absent (OFF). The voltage or current source is applied to the analog load in a repetitive pulse sequence of on (ON) or off (OFF). When it is on, it is when the DC power supply is added to the load, and when it is off, it is when the power supply is disconnected. As long as the bandwidth is sufficient, any analog value can be encoded using PWM.

## 22.2 Main features

- -Supports 2-channel input signal capture function (PWM0 and PWM4 two channels)
- -Input signal capture function supports interrupt interactive mode and DMA transfer mode; DMA mode supports word-by-word operation
- -Supports 5-channel PWM signal generation function
- -5-channel PWM signal generation supports single generation mode and auto-load mode
- -Support 5-channel braking function
- -PWM output frequency range: 3Hz~160kHz
- -The maximum precision of the duty cycle: 1/256, the width of the counter inserted into the dead zone: 8bit
- -Support channel 0 channel 1 synchronization function, support channel 2 channel 3 synchronization function
- -Support the complementary and non-complementary modes of channel 0 and channel 1, and support the complementary and non-complementary modes of channel 2 and channel 3
- -Support 5-channel synchronization function

## 22.3 Function description

### 22.3.1 Input signal capture

The PWM controller supports the signal capture function of two channels. The capture function of channel 0 can be activated by setting Bit24 of the PWM_CTL register, and the capture function of channel 4 can be activated by setting Bit1 of the PWM_CAP2CTL register. You can also set whether to flip the level of the captured signal. After the channel captures the corresponding signal, the capture number is updated to the corresponding capture register PWM_CAPDAT (channel 0 capture number) and PWM_CAP2DAT (channel 4 capture number).

### 22.3.2 DMA transfer capture number

After the capture function is enabled on channel 0 or channel 4, the count of the capture register can be quickly transferred to the memory through the DMA channel to speed up user processing.

### 22.3.3 Support single and automatic loading modes

The five output channels of the PWM controller all support single output mode and auto-load mode. In single load mode, after the channel outputs a waveform with a specified period, it will no longer output PWM waves; in auto-load mode, after the channel outputs a waveform with a specified period, it will automatically reload the number of cycles to continue generating PWM waves.

### 22.3.4 Multiple output modes

The PWM controller supports independent output mode, that is, each channel outputs independently without mutual interference; supports dual-channel synchronization mode, that is, one channel
The output is completely consistent with the output of another channel; supports five-channel synchronization mode, the output of channel 1 to channel 4 is completely consistent with the output of channel 0; supports dual-channel complementary output, that is, the waveform output by one channel and the waveform output by the other channel Completely opposite; support the dead zone setting that is often used in complementary mode, the length of the dead zone can be set up to 256 clock cycles; support brake mode, when the brake port detects the specified level, the output channel will output the already set Brake level.

Multiple output modes are flexibly configurable, satisfying users' various application scenarios related to PWM.

## 22.4 Register description

### 22.4.1 PWM Register List

![image-20201027093257720](image-20201027093257720.png)

### 22.4.2 Clock divider register_01

![image-20201027093341507](image-20201027093341507.png)

### 22.4.3 Clock divider register_23

![image-20201027093407770](image-20201027093407770.png)

### 22.4.4 Control Register

![image-20201027093440165](image-20201027093440165.png)
![image-20201027093502887](image-20201027093502887.png)
![image-20201027093539971](image-20201027093539971.png)
![image-20201027093602252](image-20201027093602252.png)
![image-20201027093619985](image-20201027093619985.png)

### 22.4.5 Period Register

![image-20201027093729395](image-20201027093729395.png)
![image-20201027093804005](image-20201027093804005.png)

### 22.4.6 Cycle Number Register

![image-20201027093848545](image-20201027093848545.png)
![image-20201027093904471](image-20201027093904471.png)

### 22.4.7 Compare Register

![image-20201027093954371](image-20201027093954371.png)
![image-20201027094019463](image-20201027094019463.png)

### 22.4.8 Dead Band Control Register

![image-20201027094100965](image-20201027094100965.png)
![image-20201027094120552](image-20201027094120552.png)

### 22.4.9 Interrupt Control Register

![image-20201027094153564](image-20201027094153564.png)
![image-20201027094209393](image-20201027094209393.png)

### 22.4.10 Interrupt Status Register

![image-20201027094314271](image-20201027094314271.png)
![image-20201027094328802](image-20201027094328802.png)

### 22.4.11 Channel 0 capture register

![image-20201027094358300](image-20201027094358300.png)

### 22.4.12 Brake Control Register

![image-20201027094516117](image-20201027094516117.png)
![image-20201027094530981](image-20201027094530981.png)

### 22.4.13 Clock Divider_4

![image-20201027094620066](image-20201027094620066.png)
![image-20201027094715416](image-20201027094715416.png)

### 22.4.14 Channel 4 Control Register_1

![image-20201027094812527](image-20201027094812527.png)
![image-20201027094829550](image-20201027094829550.png)
![image-20201027094845933](image-20201027094845933.png)

### 22.4.15 Channel 4 Capture Register

![image-20201027094929418](image-20201027094929418.png)

### 22.4.16 Channel 4 Control Register
![image-20201027095115504](image-20201027095115504.png)
![image-20201027095207594](image-20201027095207594.png)
![image-20201027095231913](image-20201027095231913.png)

# 23. QFLASH controller

## 23.1 Function overview

W600 has a built-in QFLASH controller, which provides bus-based QFLASH read/write operations, provides access arbitration for system bus and data bus, and realizes CACHE-based QFLASH read operations.

## 23.2 Main features

- -Support QFLASH command reading
- -Support QFLASH command writing
- -Support QFLASH command erase
- -Support the CACHE mode reading of QFLASH

## 23.3 Function description

## 23.4 Register description

### 23.4.1 Register List

![image-20201027095454704](image-20201027095454704.png)

### 23.4.2 Command Information Register

![image-20201027095549512](image-20201027095549512.png)
![image-20201027095603027](image-20201027095603027.png)

### 23.4.3 Command Start Register

![image-20201027095635703](image-20201027095635703.png)

## 23.5 Common Commands of QFLASH

![image-20201027095724488](image-20201027095724488.png)

# 24. Appendix 1. Chip pin definition

## 24.1 Chip pinout

![image-20201027095751376](image-20201027095751376.png)

## 24.2 Chip pin multiplexing relationship

![image-20201027095839080](image-20201027095839080.png)
![image-20201027095901018](image-20201027095901018.png)

# Disclaimer and copyright notice

The information in this article, including the URL address for reference, is subject to change without notice.

The document is provided "as is" and does not bear any guarantee responsibility, including any guarantee for marketability, suitability for a specific purpose, or non-infringement, and any guarantee mentioned elsewhere in any proposal, specification or sample. This document does not take any responsibility, including the responsibility for infringement of any patent rights caused by using the information in this document. This document does not grant any license for the use of intellectual property rights in estoppel or other ways, whether express or implied.

The Wi-Fi Alliance member logo is owned by the Wi-Fi Alliance.

All brand names, trademarks and registered trademarks mentioned in this article are the property of their respective owners, and it is hereby declared.

# Note

Due to product upgrades or other reasons, the contents of this manual may be changed. Shenzhen Sibo Zhilian Technology Co., Ltd. reserves the right to modify the contents of this manual without any notice or prompt. This manual is only used as a guide. Shenzhen Sibo Zhilian Technology Co., Ltd. does its best to provide accurate information in this manual, but it does not ensure that the content of the manual is completely free of errors. All statements, information and suggestions in this manual do not constitute any explicit indications. Or implied guarantee.
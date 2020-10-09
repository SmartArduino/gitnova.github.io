# *Multi-function Adapter*

# ***1. Product Introduction***

## ***1.1 Performance And Technical Indicators***

![wps1](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps1.jpg) 

●Full speed USB device interface, compatible with USB V2.0;

●USB bus power supply, no external power supply required;

●Support 5V power supply voltage or 3.3V power supply voltage output;

●Support 3.3V TTL, 5V TTL level output;

●Support asynchronous serial port (UART mode):

Ø Emulate standard serial port, used to upgrade the original serial peripheral device, or add additional serial port through USB

Ø The serial port application program under the Windows operating system on the computer side is fully compatible without modification

Ø Hardware full-duplex serial port, built-in transceiver buffer, support communication baud rate 50bps ~ 2Mbps

Ø Support 5, 6, 7 or 8 data bits, support odd parity, even parity, blank, flag and no parity

Ø Support transmission rate control signals such as serial port transmission enable, serial port ready to receive and MODEM contact signal

Ø RS232, RS485, RS422 and other interfaces are provided through an external level conversion module

Ø Support indirect access to serial EEPROM memory of CH341 by standard serial communication

●Support printing parallel port expansion:

Ø Standard USB printing port, used to upgrade the original parallel port printer, compatible with relevant USB specifications

Ø Compatible with Windows operating system, no driver is required under Windows 2000 and XP, and the application is fully compatible

Ø Support various standard parallel printers, optional low-speed printing and high-speed printing

 

Ø Support two-way communication of IEEE-1284 specification, support one-way and two-way transmission printer

●Support parallel port expansion:

Ø Provide two interface modes: EPP mode and MEM mode

ØEPP mode provides AS#, DS#, WR# and other signals, similar to EPP V1.7 or EPP V1.9

ØMEM mode provides A0, RD#, WR# and other signals, similar to memory read-write mode

●Support synchronous serial port (I2C/SPI mode):

ØUsing FlexWireTM technology, flexible and diverse 2-wire to 5-wire synchronous serial port can be realized through software

ØAs Host/Master host end, support 2-wire and 4-wire common synchronous serial interface

Ø2 line interface provides two signal lines SCL and SDA, supports 4 transmission speeds

●Support WINDOWS 98/ME/2000/XP/Server 2000/VISTA/Server 2008/Win7 32-bit/64-bit, pass Microsoft digital signature authentication

●Dimensions: 75 x 33 x 13mm

●PCB size: 55 x 33 x 1.6mm

●Working temperature: -40°C-+85°C

## ***1.2 Typical Application***

●I2C bus test, I2C interface component register reading and writing, EEPROM storage data reading and writing

●SPI bus test, SPI interface FLASH chip read and write, single chip program download

●Serial port program debugging, MCU download, STC ISP download

## ***1.3 Communication Protocol Conversion***

●USB and I2C bus interface protocol conversion;

●USB and SPI bus interface protocol conversion;

●USB and UART serial communication protocol conversion;

## ***1.4 Product List***

●ALL IN ONE USB to I2C/UART/SPI adapter motherboard

# **2.** ***The Shape And Interface Description***

## **2.1** ***Product Sppearance***

![wps2](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps2.jpg) 

## ***2.2 Definition Of Adapter External Interface***

This adapter is a multi-functional product, including SPI interface, I2C interface, UART interface, I2C and UART interface, asynchronous serial interface reserved interface, parallel printing interface, etc.

### ***2.2.1 SPI Interface (XH2.54MM Straight Pin)***

![wps3](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps3.png) 

![wps4](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps4.jpg) 

### ***2.2.2 I2C Interface (PH2.25MM Pin Header)***

![wps5](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps5.jpg) 

![wps6](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps6.jpg) 

### ***2.2.3 UART Interface (PH2.25 Pin Header)***

![wps7](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps7.jpg) 

### ***2.2.4 I2C And UART Interface (XH2.5MM Curved Pin)***

![wps8](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps8.jpg) 

### ***2.2.5 Asynchronous Serial Port Reserved Interface***

The asynchronous serial port, the full-signal reserved interface of UART, is located in the middle of the front of the adapter mainboard. There are 20 jacks in total, which can be installed with dual-row 2.54MM pitch pins or DC3-20P simple horn socket.

![wps9](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps9.jpg) 

### ***2.2.6 Printer Parallel Port***

The reserved port for the parallel port of the printer is located in the middle of the back side of the adapter main board. There are a total of 20 jacks, which share the same port with the asynchronous serial port. You can install dual-row 2.54MM pitch pins or DC3-20P simple horn socket.

![wps10](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps10.jpg) 

![wps11](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps11.jpg) 

The adapter also supports parallel connection

## ***2.3 Function Switch***

Which function the adapter uses is determined by the power-on initialization state of the adapter's USB conversion chip. The initialization process completes the function configuration of the chip, and the function switch needs to re-power the adapter (re-plugging).

### ***2.3.1 I2C/SPI And UART Function Configuration***

The ALL IN ONE adapter function switching jumper is located next to the USB interface, and the common functions can be switched by adjusting the position of the jumper.

The configuration of I2C and SPI functions is the same, as![wps12](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps12.jpg);The UART serial port function is configured as![wps13](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps13.jpg)

### ***2.3.2 MEM/EPP And Other Function Configuration***

The adapter can directly configure the function of the chip through the connection combination of SCL and SDA pins.

![wps14](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps14.jpg) 

Note: When the I2C function is not applicable, the I2C connection must be disconnected from the target computer, otherwise the configuration of other functions of the chip may be affected.

## ***2.4 I/O Level Selection***

The USB chip of the adapter supports 3.3V and 5V working voltages. Therefore, the TTL level of the adapter's output interface IO signal can be switched between 3.3V TTL and 5V TTL by adjusting the chip's working voltage.

### ***2.4.1 3.3V I/O Level Selection***

3.3V TTL IO level is achieved by adjusting the Level Select jumper cap on the right side of the chip on the 3.3V side, as shown in the figure below:

![wps15](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps15.jpg) 

### ***2.4.2 5V I/O Level Selection***

The 5V TTL IO level is realized by placing the Level Select jumper cap on the right side of the chip on the 5V side, as shown in the figure below:

![wps16](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps16.jpg) 

## ***2.5 External Interface Power Supply Voltage Selection***

The adapter can provide external power supply voltage consistent with the IO signal level, or a 5V power supply voltage independent of the IO signal level, or it can not provide external power output. This function can be realized by adjusting the PWR-SEL jumper located between the two white sockets.

### ***2.5.1 5V Supply Voltage***

Put the PWR-SEL red jumper cap on the 5V side, and the voltage of the adapter output interface VDD is 5V, which has nothing to do with the current working voltage of the chip. The configuration is shown below:

![wps17](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps17.jpg) 

### ***2.5.2 3.3V Supply Voltage***

Put the PWR-SEL red jumper cap on the VCC side, and the voltage of the adapter output interface VDD will be consistent with the current working voltage of the chip. The configuration is shown below:

![wps18](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps18.jpg) 

To output a 3.3V power supply voltage, the chip operating voltage must be set to 3.3V

 

## ***2.6 Indicator***

The indicator lights are located on both sides of the SPI interface. After the adapter is powered on, there will be a short configuration time. After the USB chip completes the function configuration, the different function indicator lights will have different states, which can determine whether the function configuration of the USB chip is successful , And the working status of the USB chip.

 

### ***2.6.1 I2C/SPI Function Indicator Status***

When the adapter is configured for I2C and SPI functions, the indicator status is the same, the red indicator light is TNOW

Always on, the green indicator light RDY.

### ***2.6.2 UART Function Indicator Status***

When the adapter is configured for UART serial port function, the red indicator light is off and the green indicator light RDY is on.

The TNOW indicator flashes when there is data transmission on the serial port.

Third, the upper computer application software

# ***3. Driver Installation***

There are two adapter drivers: parallel port driver and serial port driver. Adapter when using different functions

Appropriate driver will be called automatically, no conflict will occur. Therefore, no matter what function is used, it is recommended to install both drivers.

## ***3.1 Parallel Port Driver Installation***

Open the data package, find the folder where the driver is stored, and double click CH341PAR.EXE to start the parallel port

Driver installation:

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![wps19](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps19.png) |

Click Install, wait a few seconds, the "Driver pre-installation succeeded!" window pops up, click OK to finish installation.

![wps20](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps20.png)

## ***3.2 Serial Port Driver*** 
***Installation***

Open the data package, find the folder where the driver is stored, and double-click CH341SER.EXE to start the parallel port driver installation:

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![wps21](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps21.png) |

Click Install, wait a few seconds, the "Driver pre-installation succeeded!" window pops up, click OK to complete the installation.

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![wps22](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps22.png) |

## ***3.3 I2C Application Software***

### ***3.3.1 USB I2C Host Computer Software***

The software has two sub-pages, I2C interface and EEPROM read-write interface, the interface is as follows:

![wps23](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps23.png) 

I2C interface interface

![wps24](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps24.png) 

EEPROM read and write interface

### ***3.3.2 I2C Interface***

The software reads and writes the I2C compatible two-wire synchronous serial port in streaming mode, and calls the API in the driver interface

The USBIO_StreamI2C function is described in detail as follows:

BOOLWINAPI USBIO_StreamI2C( // Process I2C data stream, 2-wire interface, clock line is SCL pin data

ULON   Index, // Specify CH341 device sequence

G     WriteLeng // The number of data bytes to be written

ULON   // Point to a buffer, place the data to be written out, the first byte is usually the I2C device address and read and write direction

ULON   iReadLeng // Number of data bytes to be read

G     oReadBuffer ); // Point to a buffer, after returning it is the number read

***Data input***

Length (<400H): The number of data bytes to be written in the data buffer, expressed in hexadecimal, and the number of bytes is less than 400H.

Data: To be written into the data buffer, all numbers are expressed in hexadecimal, and the first byte is the I2C slave address, for example: A0000102030405060708

A0 is the I2C address of the slave device, 00 is the address of the writing start position, and the following 01~08 are the data to be written sequentially.

***Data Read***

Length (<400H): The number of data bytes to be read, expressed in hexadecimal, and the number of bytes is less than 400H.

Data: The read data buffer, all numbers are expressed in hexadecimal. Example: Read and write 24C02 EERPOM

Read the data in slave A0 from position 00:

![wps25](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps25.jpg) 

Write 01~08 data from the 00 position of A0

![wps26](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps26.jpg) 

Read the data just written from the 00 position of A0.

### ***3.3.3 EEPROM Read And Write***

EEPROM reading and writing are realized by calling the EEPROM dedicated API function in the driver library:



BOOLWINAPI USBIO_ReadEEPROM( // Read data block from EEPROM, speed is about 56K words

![wps27](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps27.jpg) iEepromID, //Specify EEPROM model

 _TYPE   iAddr, // refers to the address of the data unit

ULONG  iLength, // The number of data bytes to be read

ULONG  oBuffer ); points to a buffer, and after returning, the read data

BOOLWINAPI USBIO_WriteEEPROM( // write data block to EEPROM

![wps28](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps28.jpg) 

Exaple: Write 16 bytes of data from address 8 of 24C02, as follows:

![wps29](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps29.jpg) 

To read the data just written, just fill in the starting address of the data unit as 8 and the length as F (sixteen

Base), click Read, the result is as follows:

![wps30](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps30.jpg) 

This software provides source code, located in the software directory Resource, for reference for secondary development of I2C upper computer software.

### ***3.3.4 USB IIC&SPI Host Computer Software (I2C Part)***

This software mainly demonstrates I2C and SPI functions, has a rich menu interface, and is stored in

USB2IIC&SPI_EXE folder. The I2C interface menu is as follows:

![wps31](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps31.jpg) 

The I2C protocol test interface is as follows, the driver library function API called by the software is

USBIO_StreamI2C, the read and write principle is the same as USB2I2C software, but the interface is different.

![wps32](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps32.jpg) 

The 0x under the address is just the data header, indicating that the data format is hexadecimal. The read and write data buffer starts from 0. Double-click the position in the buffer and enter the data to be written after the value in the status display box.

Note: The write data length and read data length are in decimal format, which is different from USB2I2C.

The I2C protocol communication interface is as follows, and the operation method is the same as the protocol test page.

![wps33](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps33.jpg) 

For detailed operation examples of this software, please refer to "USB2IIC&SPI User Manual".

This software provides the accompanying SDK source code, located under the folder USB2IIC&SPI_SDK.

 

## ***3.4 SPI Application Software***

See the table below for SPI working mode:

![wps34](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps34.jpg) 

The adapter SPI interface works with SPI Mode0 by default, and the clock is fixed at 2MHz. The timing diagram is shown in the figure below:

![wps35](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps35.jpg) 

 

### ***3.4.1 USB SPI Host Computer Software***

The software calls the USBIO_StreamSPI4 interface library API function in the driver library to read and write the SPI-compatible 4-wire synchronous serial port in stream mode. The interface is as follows:

![wps36](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps36.jpg) 

The number of data bytes (in hexadecimal notation) is less than 40H, and the write-out and read-in data share a buffer.

This software selects CS0 as the chip select signal.

This software provides source code, located in the software directory Resource, for reference for secondary development of I2C host computer software.

BOOLWINAPI USBIO_Stre mSPI4( // Process SPI data stream, 4-wire interface, time line is DCK/D3 pin, output data is DOUT/D5 pin, input data line is DIN/D7 pin, chip select line is D0/D1 /D2, the speed is about 68K bytes

/* SPI timing: DCK/D3 pin is the clock output, the default is low level, DOUT/D5 pin is out during the low level before the rising edge of the clock, and DIN/D7 pin is high before the falling edge of the clock Enter during peacetime*/

ULONG iIndex, // point to CH341 device number

ULONG iChipSelect, // Chip select control, if bit 7 is 0, chip select control is ignored, 7

If it is 1, the parameter is valid: bit 1 bit 0 is 00/01/10 respectively select D0/D1/D2 pins as active low chip select

ULONG iLength, // The number of data bytes to be transmitted

PVOID ioBuffer ); // Point to a buffer, place the data to be written out from DOUT, and return the data read in DIN

BOOLWIN USBIO_SetStream( // Set the serial port stream mode

API iIndex, // Specify CH341 device program

ULON iMode ); //Set mode, see below

// Bit 1-Bit 0: I2C interface speed/SCL frequency, 0=low speed/20KHz, 01=standard/100KHz (default value), 10=high speed

/400KHz,11 = high speed /750KHz

// Bit 2: SPI I/O number/I pin, 0=single input single output (D3 clock/5 output/D7 input) (default value), 1=dual input output

(D3 clock/D5 out D4 out/D7 in D6 in)

// bit 7: bit sequence in SPI byte, 0=low bit first, 1=high bit before

// other reserved, must be 0

Example: Read and write X5045

Read the status register of X5045, the command code is: 05 (Hex), 00 (Hex, in fact, this byte can be filled arbitrarily, just to generate the necessary SCK

![wps37](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps37.jpg) 

2 is the byte length to be read and written, 0500 is the data to be written from MOSI, after clicking the Read/Write button, the data returned from MISO is obtained, as shown in the figure below:

![wps38](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps38.jpg) 

### ***3.4.2 USB IIC&SPI Host Computer Software (SPI P*art)***

The USB IIC&SPI software SPI interface menu is as follows:

![wps39](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps39.jpg) 

The SPI protocol test interface is as follows. The driver library function API called in this part is USBIO_StreamSPI4. The reading and writing principle is the same as that of the USB2SPI software, except the interface( is different)

![wps40](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps40.jpg)Address 0x is the data header, which means that the data format is hexadecimal. The read and write data buffer starts from 0. Double-click the position in the buffer and enter the data to be written after the value in the status display box.

Note: The write data length and read data length are in decimal format, which is different from USB2SPI.

The SPI protocol communication interface is as follows, and the operation mode is the same as the protocol test page.

![wps41](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps41.jpg) 

For detailed operation examples of this software, please refer to "USB2IIC&SPI User Manual".

This software provides the accompanying SDK source code, located under the folder USB2IIC&SPI_SDK.

## ***3.5 UART Serial Port Software***

The adapter supports simplex, half-duplex, or full-duplex asynchronous serial communication. Serial data includes 1 low-level start bit, 5 to 9 data bits, 1 or 2 high-level stop bits, and supports odd/even/mark/blank checking. Support common communication baud rates: 50, 75, 100, 110, 134.5, 150, 300, 600, 900, 1200, 1800, 2400, 3600, 4800, 9600, 14400, 19200, 28800, 33600, 38400, 56000, 57600 , 76800, 115200, 128000, 153600, 230400, 460800, 921600, 1500000, 2000000, etc. The baud rate error of the serial port sending signal is less than 0.3%, and the allowable baud rate error of the serial port receiving signal is not less than 2%.

In the Windows operating system on the computer side, the driver of the adapter can emulate a standard serial port, so most of the original serial port applications are completely compatible and usually do not require any modification.

A variety of commonly used serial port softwares are collected in the adapter data package, which are generally placed in the USB2UART folder.

![wps42](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/MultifunctionAdapter/wps42.jpg) 

 
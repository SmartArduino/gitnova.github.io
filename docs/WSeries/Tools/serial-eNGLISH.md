<center><font size=10> Serial debugging assistant </center></font>

<center> From SZDOIT</center>

# 1. Introduction

**Download tool features**

1.  Support automatic identification of IMG files, FLS files, RBL files, SECBOOT files, etc.;
2. Support erasing user parameter area;
3. Support **2Mbps** high-speed serial download;
4. Support to read MAC address information before downloading;
5. Support continuous downloading, with an interval of 5 seconds, continuous downloading;
6. Support automatic device reset after download (requires serial port hardware connection support).
7. Support gain value information reading and writing, support model selection and custom configuration;
8. Support the old version of SECBOOT (before SDK V2.8) update, need to download twice.
9. Support download list, select the corresponding date, you can view the download file corresponding to the selected date.
10. Support firmware packaging function, the packaged EXE supports custom titles;

**Serial tool features**

1. Support hardware reset W600;
2. Support receiving time printing;
3. Support custom baud rate;
4. Support serial port abnormal interrupt prompt;
5. Support multi-text sending history display;
6. Support automatic conversion when receiving data\n to \r\n;
7. Support custom multi-text configuration and multi-text cyclic transmission;
8. Support receiving data saving, optional saving as hex or text;
9. Support multi-text annotation function, F2 rename, Enter to confirm, ESC to cancel;
10. Salute to the interface [Ding Ding serial port tool] (http://www.daxia.com/sscom), thanks to the classics, this tool still needs to learn in terms of data processing stability.
11. Interface salute [丁丁串口工具](http://www.daxia.com/sscom) Thanks to the classics, this tool still needs to learn in terms of data processing stability。

**Other features**

1.  Support permanent automatic update;
2. Support the self-adaptive size of the startup window according to the resolution and ratio;
3. When the serial port list is pulled down, the description information of the corresponding serial port can be displayed;
4. Support displaying online resources, you can quickly find some commonly used information;
5. Support product selection, double-click to view the detailed IO definition and function reuse of the corresponding module;

# 2. Interface demo

**Download demo**

![img](download_demo.gif)

**Multi-text sending demo**

![img](at_demo.gif)

**Packing function  demo**

![package](package.gif)

**Custom multi-text button demo**

![package](comment.gif)

# 3. Download

[Latest version download address](https://download.w600.fun/tool/ThingsTurn_Serial_Tool.7z)

# 4. common problem

*   Need to install [DotNetFx40 Framework](https://www.microsoft.com/en-us/download/details.aspx?id=17718) framework;

*   The serial port needs to download and install the corresponding serial port driver according to the actual chip model


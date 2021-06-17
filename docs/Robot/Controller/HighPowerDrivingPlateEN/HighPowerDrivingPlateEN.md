<center size=20>High power DC brush motor drive board Datasheet</center>

## 1. The Profile

![wps1](wps1.png)



![wps2](wps2.png)

## 2. The Limit Parameter

![wps3](wps3.png)

## 3. Limit Parameter

![wps4](wps4.png)

## 4. Control Mode

### 4.1 Electromodulation Mode of Aircraft Model

![wps5](wps5.png)

### 4.2 Potentiometer Control Mode (Use of the sample program)

![wps6](wps6.png)

### 4.3 Control of PM

![wps7](wps7.png)

## 5. Wiring Instructions

### 5.1 WiFi Connection

| Arduino UNO R3 | Big Power Board |
| :------------: | :-------------: |
|       6        |     A（S）      |
|       7        |     B（S）      |
|       5V       |     B（+）      |
|      GND       |     B（—）      |

| Arduino UNO R3 | Big Power Board | WiFi  Module |
| :------------: | :-------------: | :----------: |
|       TX       |      ----       |      RX      |
|       RX       |      ----       |      TX      |
|      ----      |     A（+）      |     VCC      |
|      ----      |     A（-）      |     GND      |

![wps8](wps8.png)

### 5.2 The Bluetooth Connection

| Arduino UNO R3 | Big Power Board |
| :------------: | :-------------: |
|       6        |     A（S）      |
|       7        |     B（S）      |
|       5V       |     B（+）      |
|      GND       |     B（—）      |

| Arduino UNO R3 | Big Power Board | Bluetooth |
| :------------: | :-------------: | :-------: |
|       TX       |      ----       |    RX     |
|       RX       |      ----       |    TX     |
|      ----      |     A（+）      |    VCC    |
|      ----      |     A（-）      |    GND    |

![wps9](wps9.png)

### 5.3 The Handle Connection

| Arduino UNO R3 | Big Power Board |
| :------------: | :-------------: |
|       6        |     A（S）      |
|       7        |     B（S）      |
|       5V       |     B（+）      |
|      GND       |     B（—）      |

| Arduino UNO R3 | Big Power Board | Handle Receiver |
| :------------: | :-------------: | :-------------: |
|       10       |      ----       |       CS        |
|       11       |      ----       |       CMD       |
|       12       |      ----       |       CLK       |
|       13       |      ----       |       DAT       |
|      ----      |     A（+）      |       VCC       |
|      ----      |     A（-）      |       GND       |

![wps10](wps10.png)

![wps11](wps11.png)

## 6. Control Instructions

Please refer to the details, they use the same：https://gitnova.com/#/Robot/Controller/ps2/4motor16servo?id=arduino-ps2-controller-kit --->Usage for App
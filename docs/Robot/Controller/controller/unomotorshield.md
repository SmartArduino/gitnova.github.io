<center> <font size=10> User Manual for Motor Shield of Arduino UNO </font></center>

<center> from SZDOIT </center>




# Introduction

2-way Motor && 16-way Servo Drive Shield is a compatible with Arduino UNO R3 and ESPduino development board. This module can be inserted directly into the Arduino UNO and/or ESPduino. But if using ESPduino, you can develop quickly and conveniently a tank/car chassis controlled by WiFi. More details, please see [the link](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/[https://www.vvdoit.com/szdoit-2-channel-motor-%EF%BC%86-16-channel-servo-controller-expansion-board-servos-motors-control-module-drive-board-for-arduino-p2591823.html](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/https://www.vvdoit.com/szdoit-2-channel-motor-＆-16-channel-servo-controller-expansion-board-servos-motors-control-module-drive-board-for-arduino-p2591823.html)).

This driver shield can control 2-way DC motor (4.5~18v) and 16-way servo (5-18V),  which is very suitable for the control of mobile robot with robotic arm. This board is designed by using L293DD, which can drive directly 2-way DC motor or 1-way stepping motor. Its max current can be 1.2A.

16-way servo is controlled by IIC interface on the board.
The IO interfaces is used as the control interface for Arduino UNO and ESPduino. Thus, just the four ports D6, D7, D8, and D9( as for ESPduino, it is D12, D13, D14, D15) is defined as PWMB ( speed for motor B), DIRB (the turn direction for motor B)PWMA(speed for motor A), andDIRA ( the turn direction for motor B). The humanized design is used the power switch, which can make one on/off the power conveniently.

The board can directly be used to control the intelligent robot by Bluetooth (pre-server) and/or WiFi. More details, please visit:
 www.vvdoit.com

# Specifications

* POWER:
* Power for motor(VM): 4.5V～36V, can power separately;
* Power for servo(VS): 5～18V, can power separately;
* How to use power connection: very important!
  * If short VM and VIN, only can control the motor with 6-18V;
  * If short VS and VIN, that it's meaningless;
  * If short VM and VIN, and short VS and 5V, then CAN control the 2-way motor (with 6-18V) and 16-way 5V servo at the same time.

* Working Current Io：≤1.2A;
* Max power consumption:4W（T=90℃）;
* Input for control signal: High level: 2.3V≤VIH≤VIN; low level: -0.3V≤VIL≤1.5V
* Working temperature: -25℃～＋125℃;
* Driven mode: double big power H bridge driver;
* Weight: about 46g

![](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/https://ae01.alicdn.com/kf/HTB1XcdedOjQBKNjSZFnq6y_DpXaa.jpg)

# DataSheet

Manual: [download](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/https://github.com/SmartArduino/ESPboard/blob/master/DataSheetforMotorServo.pdf)

# Servo Test

## Experimental materials

One espdueno board, one Arduino 2 Motor &amp; &amp; 16 servo drive shield expansion board, one battery box, two 3.7V dry batteries and one steering gear;

## Hardware connection

Plug the expansion board into the espdueno board correspondingly, install the positive and negative poles of the battery box power supply of the two batteries to connect the VS and GND of the expansion board respectively (two interfaces on the right side), use a short-circuit block (the jumper cap is inserted on the VIN and vs close to the power supply of the expansion board (the middle two of the four pins)), and the rudder line is correspondingly inserted into the 16 channel rudder pin of the expansion board (the yellow line is the signal line, connected with PWM, the red line connected with VS, and the green line) Color line connected to GND);

![2way16servoshield1](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/2way16servoshield1.jpg)

![2way16servoshield2](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/2way16servoshield2.jpg)

## Experimental principle

Through the chip integrated on the expansion board, PWM wave is output to control the forward and reverse of the steering gear, so as to realize the control of the steering gear;

## Source code

```
/***************************************************
  示例：16伺服舵机。
  效果：伺服向前转180度，然后向转180度....
  by DOIT. http://www.doit.am
****************************************************/
#include <Wire.h>
#include <ServoDriver.h>

ServoDriver pwm = ServoDriver();

#define SERVOMIN  102 // 这是“最小”脉冲长度计数（满分4096）0度
#define SERVOMAX  512 // 这是“最大的”脉冲长度计数（满分4096）180度

// 重要提示：舵机号＃
uint8_t servonum = 0;

void setup()
{
  pwm.begin();
  pwm.setPWMFreq(50);  // 舵机在50Hz运行
}

void loop()
{
  // 在一个时间驱动一台舵机
  for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++)
  {
    pwm.setPWM(servonum, 0, pulselen);
  }
  delay(2000);
  for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--)
  {
    pwm.setPWM(servonum, 0, pulselen);
  }
  delay(2000);
}
```

# Reminder

- If short VM and VIN, only can control the motor with 6-18V;
- If short VS and VIN, that it's meaningless;
- If short VM and VIN, and short VS and 5V, then CAN control the 2-way motor (with 6-18V) and 16-way 5V servo at the same time.

# Applications

* with ESPduino board
![2way16servoshield3](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/2way16servoshield3.jpg)

* with Arduino board
![2way16servoshield4](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/2way16servoshield4.jpg)

* with DT-06 wifi board
![2way16servoshield5](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/2way16servoshield5.jpg)

# Notation

  Since the different generation batch, we now have the following different model about this shield. But the only difference is marked in the following picture, i.e., some pins location are different. 

![espduinoControllerV2](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/espduinoControllerV2.jpg)

![espduinoControllerV3](https://github.com/SmartArduino/document/raw/master/docs/Robot/Controller/espduinoControllerV3.jpg)
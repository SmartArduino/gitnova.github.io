<center> <font size=10> User Manual for Robot Arm of Car </font></center>

<center> from SZDOIT </center>

# Introduction

This manual is for robot arm and car chassis. But the installation, please search the assemble manual in this site. Here, we provide the connection and source code for robot arm and smart car chassis.

**Note that, this manual is for all our robot arm and car chassis, but not limited to the following picture.**

![cararm1](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/cararm1.jpg)

# 4 channel motor shield and 16 channel servo shield



The data shield can be checked at [the datasheet for motor shield](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/https://www.gitnova.com/24-channel-motor-shield-kit/).

![ps26](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/ps26.jpg)

Especially, when you connect the shield. Please note the following.

- If the voltage is bigger than 5V, and you don't need the servo, can and only can connect the VM (voltage for motor) and GND. Cannot connect the VS (voltage for servo), since the voltage of servo is smaller than 5V.
- If you want to use 5v for the servo, please use jumper cap to connect 5V and VS; VM and VIN are connected together.
- The servo interface is from PWM0-PWM15, as shown in the above picture.
- PWM8-PWM15 can be used for the servo centre. Note that, before install the servo to the robot arm, please adjust the servo to the centre.

# Robot Arm and Servo Installation

The source code and connection are suitable for lower 8 dof robot arm. 

![cararm2](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/cararm2.jpg)

After you install the servo to the arm frame (note the servo centre), you can connect the servo to the board.

J1-----PWM0

J2-----PWM1

J3 -----PWM2

J4-----PWM3

J5-----PWM4

J6-----PWM5

J7-----PWM6

J8-----PWM7

**Warm Reminder**

Pwm1-pwm2 are connected to J2 and J3. Since the two servos are installed symmetrically, it is necessary to ensure that the output shaft (i.e. the end with metal gear) of the installed servos rotates in the opposite direction with the same rotation angle. Connect to pwm1-pwm2 before the steering gear is installed to the mechanical arm. Plug in the WiFi module to open the mobile app. Select SG1 and SG2 to control pwm1-pwm2 pin. Observe whether the rotation meets the above requirements after turning on the disc.

- Sg0-sg7 controls pwm0-pwm7 with an angle of 0-180 degrees. SG1 controls pwm1-pwm2 at the same time as SG2, but in the opposite direction. It is suitable for J2 and J3.
  If you buy parts, especially the newer, it is easy to make installation errors. Always assemble according to these instructions when installing
  Key tips are as follows:
  During assembly, the steering gear angle must be adjusted to the middle position. Please connect the steering gear to pwm8-pwm15 interface for middle position adjustment. After adjusting the middle position, the initial position of the steering gear is to adjust the middle position.
- In the assembly process, pay special attention to the relative position of the steering gear and the bracket. When the steering gear is installed, the output shaft of the steering gear (that is, the end with metal gear) cannot rotate. Please assemble in strict accordance with the assembly requirements.
- Be sure to install from j1to J8, and use the mobile app for debugging while installing.

# Usage for App 

The download address is at: https://www.gitnova.com/24-channel-motor-shield-kit/, choose v1.3 version.

![cararm3](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/cararm3.jpg)

Two mode:

arm mode: just control the servo, shown in the above picture.

car mode: just control the car, and the functions shown in the app are for car chassis, e.g., control car move, low speed, high speed.

![cararm4](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/cararm4.jpg)

# Source code

Some head files can be downed from the following link: [source code](https://github.com/SmartArduino/document/raw/master/docs/Robot/FrameChassis/cararm/https://github.com/SmartArduino/DOITWiKi/blob/master/armcarhead.zip).

**The main program in Arduino with wifi (or bluetooth)**

```
#include "doit_moter.h"
#include "doit_app.h"
#include "doit_servo.h"

volatile int angle_step;
volatile int J0;
volatile int J1;
volatile int J2;
volatile int J3;
volatile int J4;
volatile int J5;
volatile int J6;
volatile int J7;
volatile int J8;
volatile int J9;
volatile int J10;
volatile int J11;
volatile int J12;
volatile int J13;
volatile int J14;
volatile int J15;
volatile int Speed_Mode;

#define PWMA 9
#define DIRA 8
#define PWMB 6
#define DIRB 7
#define PWMC 5
#define DIRC 4
#define PWMD 3
#define DIRD 2
MOTER moter;
APP app;
SERVO servo;
void forward() {
  if (Speed_Mode == 0) {
    moter.setspeed(1,1,100);
    moter.setspeed(2,1,100);

  }
  if (Speed_Mode == 1) {
    moter.setspeed(1,1,255);
    moter.setspeed(2,1,255);

  }
}

void back() {
  if (Speed_Mode == 0) {
    moter.setspeed(1,0,100);
    moter.setspeed(2,0,100);

  }
  if (Speed_Mode == 1) {
    moter.setspeed(1,0,255);
    moter.setspeed(2,0,255);

  }
}

void right() {
  if (Speed_Mode == 0) {
    moter.setspeed(1,0,100);
    moter.setspeed(2,1,100);

  }
  if (Speed_Mode == 1) {
    moter.setspeed(1,0,255);
    moter.setspeed(2,1,255);

  }
}

void left() {
  if (Speed_Mode == 0) {
    moter.setspeed(1,1,100);
    moter.setspeed(2,0,100);

  }
  if (Speed_Mode == 1) {
    moter.setspeed(1,1,255);
    moter.setspeed(2,0,255);

  }
}

void setup(){
  moter.init(PWMA,DIRA,PWMB,DIRB,PWMC,DIRC,PWMD,DIRD);
  angle_step = 5;
  J0 = 90;
  J1 = 90;
  J2 = 90;
  J3 = 90;
  J4 = 90;
  J5 = 90;
  J6 = 90;
  J7 = 90;
  J8 = 90;
  J9 = 90;
  J10 = 90;
  J11 = 90;
  J12 = 90;
  J13 = 90;
  J14 = 90;
  J15 = 90;
  Speed_Mode = 0;
  Serial.begin(9600);
  servo.init();
  // Servo 0 Angle init
  servo.setdegree(0,J0,0);
  delay(0);
  // Servo 1 Angle init
  servo.setdegree(1,J1,0);
  delay(0);
  // Servo 2 Angle init
  servo.setdegree(2,J2,0);
  delay(0);
  // Servo 3 Angle init
  servo.setdegree(3,J3,0);
  delay(0);
  // Servo 4 Angle init
  servo.setdegree(4,J4,0);
  delay(0);
  // Servo 5 Angle init
  servo.setdegree(5,J5,0);
  delay(0);
  // Servo 6 Angle init
  servo.setdegree(6,J6,0);
  delay(0);
  // Servo 7 Angle init
  servo.setdegree(7,J7,0);
  delay(0);
  // Servo 8 Angle init
  servo.setdegree(8,J8,0);
  delay(0);
  // Servo 9 Angle init
  servo.setdegree(9,J9,0);
  delay(0);
  // Servo 10 Angle init
  servo.setdegree(10,J10,0);
  delay(0);
  // Servo 11 Angle init
  servo.setdegree(11,J11,0);
  delay(0);
  // Servo 12 Angle init
  servo.setdegree(12,J12,0);
  delay(0);
  // Servo 13 Angle init
  servo.setdegree(13,J13,0);
  delay(0);
  // Servo 14 Angle init
  servo.setdegree(14,J14,0);
  delay(0);
  // Servo 15 Angle init
  servo.setdegree(15,J15,0);
  delay(0);
}

void loop(){
  // moter pin init
  app.serial_process();
  if (app.button_pressed(car_move_up)) {
    forward();

  }
  if (app.button_pressed(car_move_down)) {
    back();

  }
  if (app.button_pressed(car_move_left)) {
    left();

  }
  if (app.button_pressed(car_move_right)) {
    right();

  }
  if (app.button_pressed(car_speed_right)) {
    Speed_Mode = 0;

  }
  if (app.button_pressed(car_speed_left)) {
    Speed_Mode = 1;

  }

  // Servo 0 Angle + angle_step
  if (app.button_pressed(servo_0_left)) {
    J0 = J0 + angle_step;
    if (J0 > 180) {
      J0 = 180;

    }
    servo.setdegree(0,J0,0);
    delay(30);

  }
  // Servo 0 Angle - angle_step
  if (app.button_pressed(servo_0_right)) {
    J0 = J0 - angle_step;
    if (J0 < 0) {
      J0 = 0;

    }
    servo.setdegree(0,J0,0);
    delay(30);

  }

  // Servo 1 and 2 Angle + angle_step but they has the different direction
  if (app.button_pressed(servo_1_left)) {
    J1 = J1 + angle_step;
    if (J1 > 180) {
      J1 = 180;

    }
    servo.setdegree(1,(180 - J1),0);
    delay(0);
    servo.setdegree(2,J1,0);
    delay(30);

  }
  // Servo 1 and 2 Angle - angle_step but they has the different direction
  if (app.button_pressed(servo_1_right)) {
    J1 = J1 - angle_step;
    if (J1 < 0) {
      J1 = 0;

    }
    servo.setdegree(1,(180 - J1),0);
    delay(0);
    servo.setdegree(2,J1,0);
    delay(30);

  }

  // Servo 1 and 2 Angle + angle_step but they has the different direction
  if (app.button_pressed(servo_2_left)) {
    J1 = J1 + angle_step;
    if (J1 > 180) {
      J1 = 180;

    }
    servo.setdegree(1,(180 - J1),0);
    delay(0);
    servo.setdegree(2,J1,0);
    delay(30);

  }
  //  Servo 1 and 2 Angle - angle_step but they has the different direction
  if (app.button_pressed(servo_2_left)) {
    J1 = J1 - angle_step;
    if (J1 < 0) {
      J1 = 0;

    }
    servo.setdegree(1,(180 - J1),0);
    delay(0);
    servo.setdegree(2,J1,0);
    delay(30);

  }

  // Servo 3 Angle + angle_step
  if (app.button_pressed(servo_3_left)) {
    J3 = J3 + angle_step;
    if (J3 > 180) {
      J3 = 180;

    }
    servo.setdegree(3,J3,0);
    delay(30);

  }
  // Servo 3 Angle - angle_step
  if (app.button_pressed(servo_3_right)) {
    J3 = J3 - angle_step;
    if (J3 < 0) {
      J3 = 0;

    }
    servo.setdegree(3,J3,0);
    delay(30);

  }

  // Servo 4 Angle + angle_step
  if (app.button_pressed(servo_4_left)) {
    J4 = J4 + angle_step;
    if (J4 > 180) {
      J4 = 180;

    }
    servo.setdegree(4,J4,0);
    delay(30);

  }
  // Servo 4 Angle - angle_step
  if (app.button_pressed(servo_4_right)) {
    J4 = J4 - angle_step;
    if (J4 < 0) {
      J4 = 0;

    }
    servo.setdegree(4,J4,0);
    delay(30);

  }

  // Servo 5 Angle + angle_step
  if (app.button_pressed(servo_5_left)) {
    J5 = J5 + angle_step;
    if (J5 > 180) {
      J5 = 180;

    }
    servo.setdegree(5,J5,0);
    delay(30);

  }
  // Servo 5 Angle - angle_step
  if (app.button_pressed(servo_5_right)) {
    J5 = J5 - angle_step;
    if (J5 < 0) {
      J5 = 0;

    }
    servo.setdegree(5,J5,0);
    delay(30);

  }

  // Servo 6 Angle + angle_step
  if (app.button_pressed(servo_6_left)) {
    J6 = J6 + angle_step;
    if (J6 > 180) {
      J6 = 180;

    }
    servo.setdegree(6,J6,0);
    delay(30);

  }
  // Servo 6 Angle - angle_step
  if (app.button_pressed(servo_6_right)) {
    J6 = J6 - angle_step;
    if (J6 < 0) {
      J6 = 0;

    }
    servo.setdegree(6,J6,0);
    delay(30);

  }

  // Servo 7 Angle + angle_step
  if (app.button_pressed(servo_7_left)) {
    J7 = J7 + angle_step;
    if (J7 > 180) {
      J7 = 180;

    }
    servo.setdegree(7,J7,0);
    delay(30);

  }
  // Servo 7 Angle - angle_step
  if (app.button_pressed(servo_7_right)) {
    J7 = J7 - angle_step;
    if (J7 < 0) {
      J7 = 0;

    }
    servo.setdegree(7,J7,0);
    delay(30);

  }

  // Servo 8 Angle + angle_step
  if (app.button_pressed(servo_8_left)) {
    J8 = J8 + angle_step;
    if (J8 > 180) {
      J8 = 180;

    }
    servo.setdegree(8,J8,0);
    delay(30);

  }
  // Servo 8 Angle - angle_step
  if (app.button_pressed(servo_8_right)) {
    J8 = J8 - angle_step;
    if (J8 < 0) {
      J8 = 0;

    }
    servo.setdegree(8,J8,0);
    delay(30);

  }

  // Servo 9 Angle + angle_step
  if (app.button_pressed(servo_9_left)) {
    J9 = J9 + angle_step;
    if (J9 > 180) {
      J9 = 180;

    }
    servo.setdegree(9,J9,0);
    delay(30);

  }
  // Servo 9 Angle - angle_step
  if (app.button_pressed(servo_9_right)) {
    J9 = J9 - angle_step;
    if (J9 < 0) {
      J9 = 0;

    }
    servo.setdegree(9,J9,0);
    delay(30);

  }

  // Servo 10 Angle + angle_step
  if (app.button_pressed(servo_10_left)) {
    J10 = J10 + angle_step;
    if (J10 > 180) {
      J10 = 180;

    }
    servo.setdegree(10,J10,0);
    delay(30);

  }
  // Servo 10 Angle - angle_step
  if (app.button_pressed(servo_10_left)) {
    J10 = J10 - angle_step;
    if (J10 < 0) {
      J10 = 0;

    }
    servo.setdegree(10,J10,0);
    delay(30);

  }

  // Servo 11 Angle + angle_step
  if (app.button_pressed(servo_11_left)) {
    J11 = J11 + angle_step;
    if (J11 > 180) {
      J11 = 180;

    }
    servo.setdegree(11,J11,0);
    delay(30);

  }
  // Servo 11 Angle - angle_step
  if (app.button_pressed(servo_11_right)) {
    J11 = J11 - angle_step;
    if (J11 < 0) {
      J11 = 0;

    }
    servo.setdegree(11,J11,0);
    delay(30);

  }

  // Servo 12 Angle + angle_step
  if (app.button_pressed(servo_12_left)) {
    J12 = J12 + angle_step;
    if (J12 > 180) {
      J12 = 180;

    }
    servo.setdegree(12,J12,0);
    delay(30);

  }
  // Servo 12 Angle - angle_step
  if (app.button_pressed(servo_12_right)) {
    J12 = J12 - angle_step;
    if (J12 < 0) {
      J12 = 0;

    }
    servo.setdegree(12,J12,0);
    delay(30);

  }

  // Servo 13 Angle + angle_step
  if (app.button_pressed(servo_13_left)) {
    J13 = J13 + angle_step;
    if (J13 > 180) {
      J13 = 180;

    }
    servo.setdegree(13,J13,0);
    delay(30);

  }
  // Servo 13 Angle - angle_step
  if (app.button_pressed(servo_13_left)) {
    J13 = J13 - angle_step;
    if (J13 < 0) {
      J13 = 0;

    }
    servo.setdegree(13,J13,0);
    delay(30);

  }

  // Servo 14 Angle - angle_step
  if (app.button_pressed(servo_14_left)) {
    J14 = J14 + angle_step;
    if (J14 > 180) {
      J14 = 180;

    }
    servo.setdegree(14,J14,0);
    delay(30);

  }
  // Servo 14 Angle + angle_step
  if (app.button_pressed(servo_14_right)) {
    J14 = J14 - angle_step;
    if (J14 < 0) {
      J14 = 0;

    }
    servo.setdegree(14,J14,0);
    delay(30);

  }

  // Servo 15 Angle + angle_step
  if (app.button_pressed(servo_15_left)) {
    J15 = J15 + angle_step;
    if (J15 > 180) {
      J15 = 180;

    }
    servo.setdegree(15,J15,0);
    delay(30);

  }
  // Servo 15 Angle - angle_step
  if (app.button_pressed(servo_15_right)) {
    J15 = J15 - angle_step;
    if (J15 < 0) {
      J15 = 0;

    }
    servo.setdegree(15,J15,0);
    delay(30);

  }

}
```


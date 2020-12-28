<center> <font size=10> User Manual for 9v DC Motor </font></center>

<center> from SZDOIT </center>

## 1. 9V 25GA-370 Motor Parameters:

- Name: 25mm DC carbon brush motor (with Hall sensor code disc)
- Output rate: 150 ± 10% rpm
- Load current: 200mA (Max)
- Stall current: 4500mA (max)
- Locking torque: 9.5kgNaN
- Load speed: 100 ± 10% rpm
- Load torque: 3000gNaN
- Load current: 1200mA (Max)
- Load noise: 56dB
- Working voltage: 9V
- Shaft extension size: 14.5mm
- Axial clearance: 0.05-0.50mm
- Screw size: M3.0
- Shaft diameter: phi4mm, D3.5
- Code wheel parameters: 2 pulses / turn
- Sensor working voltage: 3-5V

![9vmotor2](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotor2.jpg)

![9vmotor3](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotor3.jpg)

![9vmotor1](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotor1.jpg)

## 2. Motor Connection

The connection is show in the following picture.

![9vmotorconnection](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotorconnection.jpg)

**Hall sensor:**

  This motor has Hall sensor, which can measure the velocity, and give out a feedback. If let the interface (or plug) face to our face, from left to right, the interface meanings are VM (power for motor), GM (grand for motor), V (power for Hall sensor), G (grand for Hall sensor), S1 (the output signal for the 1st Hall sensor), S2 (the output signal for the 2nd Hall sensor)

![sensor](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/sensor.png)

## 3. How to Test the Motor

There are two methods.

### 3.1 Use Oscilloscope

When power on the motor, and connect to the Hall sensor of motor, you will see the following wave. This way is very simple.

![9vmotor4](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotor4.jpg)

### 3.2 Use Arduino

#### 3.2.1 Connect to UNO

![motorcode](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/motorcode.png)

#### 3.2.2 Test Code

```
/*
 * How to test encoder with Arduino
 * url: http://osoyoo.com/?p=30267
 */
 #define outputA 6
 #define outputB 7
 int counter = 0; 
 int aState;
 int aLastState;  
 void setup() { 
   pinMode (outputA,INPUT);
   pinMode (outputB,INPUT);
   
   Serial.begin (9600);
   // Reads the initial state of the outputA
   aLastState = digitalRead(outputA);   
 } 
 void loop() { 
   aState = digitalRead(outputA); // Reads the "current" state of the outputA
   // If the previous and the current state of the outputA are different, that means a Pulse has occured
   if (aState != aLastState){     
     // If the outputB state is different to the outputA state, that means the encoder is rotating clockwise
     if (digitalRead(outputB) != aState) { 
       counter ++;
     } else {
       counter --;
     }
     Serial.print("Position: ");
     Serial.println(counter);
   } 
   aLastState = aState; // Updates the previous state of the outputA with the current state
 }

```

From the monitor, you can see the output data.

**Very important, when you install the motor to the car chassis, Please choose the M3*6 screw to fix the motor. By our experience, if you choose the screw is too long, the motor would be stalled, and cannot be run.**

![9vmotorconnection1](https://github.com/SmartArduino/document/raw/master/docs/Robot/Engine/9vMotor/9vmotorconnection1.jpg)



## Contact Us

- E-mails: [yichone@doit.am](mailto:yichone@doit.am), [yichoneyi@163.com](mailto:yichoneyi@163.com)
- Skype: yichone
- WhatsApp:+86-18676662425
- Wechat: 18676662425
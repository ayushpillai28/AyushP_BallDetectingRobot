# Autonmous Robot with Raspberry Pi
I am working on a Raspberry Pi Machine Learning model with the eventual goal of creating a fully autonmous car.
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ayush P | Groton School | Engineer| Incoming Junior

[IMG_043085BC47E1-1](https://user-images.githubusercontent.com/88009393/129366499-97aa5389-fd44-4cf9-81eb-213e4fdb8f92.jpeg)

# Final Milestone
For my final milestone I wanted to incorporate an ultrasonic sensor to my car as well as modify the stop sign code to make my robot more autonomous. I added an ultrasonic sensor to my robot and created a program that the robot would stop if there was anything less that 10 cm away from the robot. Once the object was removed the robot would continue to move. My stop sign code modifications included making the robot stop for two seconds once it recognizes a stop sign. I also modified the area of red necessary for the robot to classify the object as a stop sign, allowing me to move the rpbpt to the left of the sign so I don't have to pick up the sign. When I combined the modified stop sign code and ultrasonic code, it created a program that the robot would move forward until it sees the stop sign, it would then stop for two seconds, and then continue to move forward. However if the robot sees any object less than 10 cm away at any point, most commonly at the stop sign, it will stop until the object is out of the sight of the ultrasonic sencor.

[![Final Milestone]

# Second Milestone
My second milestone involved using the ultrasonic sensors and the camera module to detect other objects that may be in the path of the robot. After connecting the ultrasonic sensor to the rasperry pi, I created a program that would measure the distance the robot is from an object. Since the robot will have ultrasonic sensors on the sides and the front, this gives it the ability to recognize other vehicles or pedestrians that may crash into it and act accordingly. The camera module is used to detect objects as well but it differs from the ultrasonic sensor because it can also recognize what object it is detecting. By using OpenCV, I created a program that would allow the camera module to detect red and green as well as the shape of the object. For example, if there was a red stop sign ahead, the robot would recognize the hexagon shape and the color red and the robot would stop. This program can be expanded to other colors and shaped to recognize speed limits, traffic light colors, and other signs that are necessary to regulate traffic.

<iframe width="560" height="315" src="https://www.youtube.com/embed/OFlSCI2MN3I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# First Milestone
  

My first milestone was programming my motors to move change direction. Once I set up the Rasperry Pi, I connected the motor driver and the motors to the raspberry pi. I then used those pins to create my code. To make sure all the wires connecting the motors to the motor driver were well connected, I used a saughtering iron to connect the wires to the The first step to my code was to get the motors to move forwards and backwards and stop. Once I completed that task, I moved onto turning left and right. After my code was complete and the motors were functional, I assembled the chassis so I could see the robot in action instead of just the motors.
<iframe width="560" height="315" src="https://www.youtube.com/embed/HMRqWIDqAzk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# Diagram of Raspberry Pi Attachments
![Diagram](https://user-images.githubusercontent.com/88009393/127663961-c232e023-24a3-4d40-ae7d-74458c57592e.png)

# Python Code for the Stop Sign and Ultrasonic Program

```python
import RPi.GPIO as GPIO
from time import sleep

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

class Motor():
    def __init__(self,Ena,In1,In2,Enb,In3,In4): #initialization function that will run the first time
        self.Ena = Ena
        self.In1 = In1
        self.In2 = In2
        self.Enb = Enb
        self.In3 = In3
        self.In4 = In4
        GPIO.setup(self.Ena,GPIO.OUT)
        GPIO.setup(self.In1,GPIO.OUT)
        GPIO.setup(self.In2,GPIO.OUT)
        GPIO.setup(self.Enb,GPIO.OUT)
        GPIO.setup(self.In3,GPIO.OUT)
        GPIO.setup(self.In4,GPIO.OUT)
        self.pwm = GPIO.PWM(self.Ena,100)
        self.pwm = GPIO.PWM(self.Enb,100)
        self.pwm.start(0)
        
    def moveF(self,x=50,t=0):
        GPIO.output(self.In1,GPIO.LOW)
        GPIO.output(self.In2,GPIO.HIGH)
        GPIO.output(self.In3,GPIO.LOW)
        GPIO.output(self.In4,GPIO.HIGH)
        self.pwm.ChangeDutyCycle(x) #default speed is 50 but the user can change it 
        sleep(t)
              
    def moveB(self,x=50,t=0):
        GPIO.output(self.In1,GPIO.HIGH)
        GPIO.output(self.In2,GPIO.LOW)
        GPIO.output(self.In3,GPIO.HIGH)
        GPIO.output(self.In4,GPIO.LOW)
        self.pwm.ChangeDutyCycle(x) #default speed is 50 but the user can change it 
        sleep(t)
        
    def stop(self,t=0):
        self.pwm.ChangeDutyCycle(0)
        GPIO.output(self.In1,GPIO.LOW)
        GPIO.output(self.In2,GPIO.LOW)
        GPIO.output(self.In3,GPIO.LOW)
        GPIO.output(self.In4,GPIO.LOW)
        sleep(t)
        
motor1 = Motor(22,27,17,23,24,25)

while True:
    motor1.moveF(30,3)
    motor1.stop(2)
    motor1.moveB(30,3)
    motor1.stop(2)
```

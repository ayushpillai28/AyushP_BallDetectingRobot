# Ball Detecting Robot with Raspberry Pi
I am working on a Raspberry Pi Machine Learning model which will detect a ball and a robot will move towards it.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ayush P | Groton School | Engineer| Incoming Junior

![Headstone Image]
![Name of final image]  
# Final Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint. 

[![Final Milestone]

# Second Milestone
My second milestone involved using the ultrasonic sensors and the camera module to detect other objects that may be in the path of the robot. After connecting the ultrasonic sensor to the rasperry pi, I created a program that would measure the distance the robot is from an object. Since the robot will have ultrasonic sensors on the sides and the front, this gives it the ability to recognize other vehicles or pedestrians that may crash into it and act accordingly. The camera module is used to detect objects as well but it differs from the ultrasonic sensor because it can also recognize what object it is detecting. By using OpenCV, I created a program that would allow the camera module to detect red and green as well as the shape of the object. For example, if there was a red stop sign ahead, the robot would recognize the hexagon shape and the color red and the robot would stop. This program can be expanded to other colors and shaped to recognize speed limits, traffic light colors, and other signs that are necessary to regulate traffic.

[![Third Milestone]
# First Milestone
  

My first milestone was programming my motors to move change direction. Once I set up the Rasperry Pi, I connected the motor driver and the motors to the raspberry pi. I then used those pins to create my code. To make sure all the wires connecting the motors to the motor driver were well connected, I used a saughtering iron to connect the wires to the The first step to my code was to get the motors to move forwards and backwards and stop. Once I completed that task, I moved onto turning left and right. After my code was complete and the motors were functional, I assembled the chassis so I could see the robot in action instead of just the motors.
<iframe width="560" height="315" src="https://www.youtube.com/embed/HMRqWIDqAzk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# Diagram of Raspberry Pi Attachments
![Diagram](https://user-images.githubusercontent.com/88009393/127663961-c232e023-24a3-4d40-ae7d-74458c57592e.png)

# Python Code for the Motors

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
# Python Code for the Ultrasonic Sensor

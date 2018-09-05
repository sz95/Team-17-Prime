# Lab 1: Introduction to Arduino and Robot Assembly

## Goal

The goal of this Lab was to learn how to use the Arduino Uno and the Arduino IDE.  We did so through implementing the following procedures, that all came together to allow us to have our robot complete a simple, autonomous task.

## Internal Blink

[Watch the video!](https://drive.google.com/file/d/1AitKiP5LDuS085Qc87MSYno-bPexnUOw/view?usp=sharing)



~~~
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
~~~

## External Blink

![external led](/images/lab1/external_led_blink.gif)

~~~
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(8, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(8, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(8, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
~~~

## Potentiometer Serial Read

![potentiometer to serial port](/images/lab1/pot_serial.gif)

~~~
int sensorPin = A0;
int sensorValue=0;

void setup() {

  Serial.begin(9600);
}

// the loop function runs over and over again forever
void loop() {
  sensorValue = analogRead(sensorPin);
  Serial.print(sensorValue);
  Serial.println(" ");
  delay(1000);                       // wait for a second

}
~~~

## Potentiometer to LED

![potentiometer to LED intensity](/images/lab1/pot_led.gif)

~~~
int sensorPin = A0;
int sensorValue=0;
void setup() {
  pinMode(9, OUTPUT);
  Serial.begin(9600);
}

// the loop function runs over and over again forever
void loop() {
  sensorValue = analogRead(sensorPin);
  Serial.print(sensorValue);
  Serial.println(" ");
  analogWrite(9, sensorValue/4);   // turn the LED on (HIGH is the voltage level)
  delay(5);                       // wait for a second
}
~~~

## Potentiometer to Servo

![potentiometer to servo motor](/images/lab1/pot_motor.gif)

~~~
#include <Servo.h>
Servo myservo; 

int sensorPin = A0;
int sensorValue=0;
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  //pinMode(9, OUTPUT);
  myservo.attach(9);
  Serial.begin(9600);
  
}

// the loop function runs over and over again forever
void loop() {
  sensorValue = analogRead(sensorPin);
  sensorValue = map(sensorValue, 0, 1023, 0, 180); 
  myservo.write(sensorValue); 
  delay(15);                       // wait 
}
~~~

## Robot Assembly and Driving in a Square

![assembled robot](/images/lab1/robot.jpg)

https://drive.google.com/file/d/1TNmG1FMpcSOZAJzGpEx64XWEyMJwZd1h/view?usp=sharing

~~~
#include <Servo.h>
Servo left;
Servo right; 

int sensorPin = A0;
int sensorValue=0;

void setup() {
  left.attach(10);
  right.attach(9);  
  Serial.begin(9600);
  
}

// the loop function runs over and over again forever
void loop() {
  forward();
  delay(2000);
  turn();
  delay(1350);
  
}

void forward() {
  left.write(95);
  right.write(85);
  
}

void back() {
  right.write(95);
  left.write(85);
  
}

void turn() {
  right.write(95);
  left.write(95);
}
~~~

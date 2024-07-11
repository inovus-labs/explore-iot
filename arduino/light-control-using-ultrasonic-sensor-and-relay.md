# Automated Light Control using Ultrasonic Sensor and Relay

This project utilizes an Arduino Uno development board along with an ultrasonic sensor and a relay module to create an automated light control system. The system turns on the light connected to the relay if the ultrasonic sensor detects an object within 50 cm. This README provides a comprehensive guide to set up and use the system effectively.

## Components Required

* Arduino Uno
* Ultrasonic sensor (HC-SR04)
* Relay module
* Jumper wires
* Light bulb or LED with appropriate power source

## Circuit Diagram

Ensure to connect the components as shown in the circuit diagram:

![Circuit Diagram](https://github.com/inovus-labs/explore-iot/assets/145148320/f8d8352d-931c-4e8b-adde-2e10e8ab1eab)

1. Connect the VCC and GND of the ultrasonic sensor to the 5V and GND pins of the Arduino Uno.
2. Connect the TRIG pin of the ultrasonic sensor to pin 9 of the Arduino Uno.
3. Connect the ECHO pin of the ultrasonic sensor to pin 8 of the Arduino Uno.
4. Connect the IN pin of the relay module to pin 7 of the Arduino Uno.
5. Connect the relay module's VCC and GND to the 5V and GND of the Arduino Uno.
6. Connect the light bulb or LED to the relay module.

## Code

Upload the following code to the Arduino Uno using the Arduino IDE:

```cpp
const int trigPin = 9; 
const int echoPin = 8; 
const int relay=7;
void setup() {
  Serial.begin(9600);   // Initialize serial communication for debugging
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(relay,OUTPUT);
}

void loop() {
  long duration;
  int distance;

  // Trigger the ultrasonic sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Measure the duration of the echo signal
  duration = pulseIn(echoPin, HIGH);

  // Convert the duration to distance (in cm)
  distance = duration * 0.034 / 2;
  
  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  digitalWrite(relay,HIGH);
    if(distance<=50)
  {
    digitalWrite(relay,LOW);
    delay(5000);
  }
  else
  {
    digitalWrite(relay,HIGH);
  }
  delay(100); // delay before the next measurement
}
```

## Setting Up

1. Install the Arduino IDE from the official [Arduino website](https://www.arduino.cc/).
2. Connect the Arduino Nano to your computer via USB.
3. Open the Arduino IDE and paste the code above into a new sketch.
4. Select the appropriate board and port from the Tools menu.
5. Click the upload button to upload the code to the Arduino Nano.

## Usage

Once the code is uploaded, the system will continuously monitor the distance detected by the ultrasonic sensor. If the sensor detects an object within 50 cm, the relay will activate, turning on the light. If the object moves beyond 50 cm, the relay will deactivate, turning off the light.

## Troubleshooting

* Ensure all connections are secure and correct.
* Check the power supply for the Arduino Nano and the relay module.
* Use the Serial Monitor in the Arduino IDE to debug and monitor the distance readings from the ultrasonic sensor.
* If the light turns on when the ultrasonic sensor detects a distance greater than 50 cm, switch the `LOW` written for the relay to `HIGH` and vice versa (i.e., change `digitalWrite(RELAY_PIN, LOW)` to `digitalWrite(RELAY_PIN, HIGH)` and `digitalWrite(RELAY_PIN, HIGH)` to `digitalWrite(RELAY_PIN, LOW)`).

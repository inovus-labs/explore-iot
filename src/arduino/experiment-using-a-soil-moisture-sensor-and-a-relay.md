# 🌟 Experiment using a Soil Moisture Sensor and a Relay

This project utilizes an Arduino Uno development board along with a soil moisture sensor and a relay module to create an automated soil moisture control system. The system turns on the water pump connected to the relay if the soil moisture sensor detects a moisture level below a specified threshold. This README provides a comprehensive guide to set up and use the system effectively.

### Components Required

* Arduino Uno
* Soil moisture sensor
* Relay module
* Jumper wires
* Water pump or similar device with appropriate power source
* LED (Optional)

### Circuit Diagram

Ensure to connect the components as shown in the circuit diagram:

![Circuit Diagram](https://github.com/inovus-labs/explore-iot/assets/145148320/a62fb787-7abc-4e2e-beeb-c1b35073d1f6)

1. Connect the VCC and GND of the soil moisture sensor to the 5V and GND pins of the Arduino Uno.
2. Connect the analog output of the soil moisture sensor to the A5 pin of the Arduino Uno.
3. Connect the IN pin of the relay module to pin 7 of the Arduino Uno.
4. Connect the relay module's VCC and GND to the 5V and GND of the Arduino Uno.
5. Connect the water pump to the relay module.
6. Connect the positive leg of the LED to pin 2 of the Arduino Uno and the negative leg to the GND via a current-limiting resistor.

### Code

Upload the following code to the Arduino Uno using the Arduino IDE:

```cpp
int green = 2;  //led
#define sensorPin A5
int relay = 7;

void setup() {  
  Serial.begin(9600);
  pinMode(green, OUTPUT);
  pinMode(relay, OUTPUT);
}

void loop() {
  int moisture = analogRead(sensorPin);
  Serial.print("Analog output: ");
  Serial.println(moisture);

  if (moisture < 900) {//value to be adjusted  based on the readings..
    Serial.println("Status: Soil is wet");
    digitalWrite(green, HIGH); // LED
    digitalWrite(relay, LOW);  // Relay
    delay(1000);
  } else {
    digitalWrite(green, LOW); // LED
    digitalWrite(relay, HIGH); // Relay
  }

  Serial.println();
  delay(1000);
}

```

### Setting Up

1. Install the Arduino IDE from the official [Arduino website](https://www.arduino.cc/).
2. Connect the Arduino Uno to your computer via USB.
3. Open the Arduino IDE and paste the code above into a new sketch.
4. Select the appropriate board and port from the Tools menu.
5. Click the upload button to upload the code to the Arduino Uno.

### Usage

Once the code is uploaded, the system will continuously monitor the soil moisture level detected by the sensor. If the moisture level is below the threshold (900), the relay will activate, turning on the water pump. If the moisture level is above the threshold, the relay will deactivate, turning off the water pump. The LED will provide a visual indication of the soil moisture status.

### Troubleshooting

* Ensure all connections are secure and correct.
* Check the power supply for the Arduino Uno and the relay module.
* Use the Serial Monitor in the Arduino IDE to debug and monitor the moisture readings from the soil moisture sensor.
* If the water pump turns on when the moisture level is above the threshold, switch the `LOW` written for the relay to `HIGH` and vice versa (i.e., change `digitalWrite(RELAY_PIN, LOW)` to `digitalWrite(RELAY_PIN, HIGH)` and `digitalWrite(RELAY_PIN, HIGH)` to `digitalWrite(RELAY_PIN, LOW)`).
* Adjust the Moisture Threshold: If the soil moisture level detected by the sensor is not suitable for your plants, adjust the threshold value in the code. Change the value `900` in the condition `if (moisture < 900)` to the desired threshold that matches your soil and plant requirements.

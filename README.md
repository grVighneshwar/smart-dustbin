# smart-dustbin
## Project Overview
This Smart Dustbin is an automated system designed to improve cleanliness and hygiene by providing a touchless method for disposing of waste. It uses an ultrasonic sensor to detect the presence of a person or object near the dustbin, and a servo motor to automatically open and close the lid. The system is controlled by an Arduino microcontroller, which processes the input from the ultrasonic sensor and activates the servo motor accordingly.

This project is ideal for households, offices, and public places, where minimizing physical contact with waste disposal units can significantly reduce the spread of germs.

## Key Features
- **Touchless Operation:** The dustbin opens automatically when a person or object comes within a predefined distance, eliminating the need for physical contact.
- **Efficient Servo Control:** The servo motor smoothly opens and closes the lid, ensuring reliability and longevity of the system.
- **Low Power Consumption:** Powered by an Arduino, the system consumes minimal energy, making it ideal for continuous use.
- **Easy to Implement:** Simple circuitry and affordable components make this project easy to build and deploy in any environment.
  
## Hardware Components
- **Ultrasonic Sensor (HC-SR04):** Measures the distance of an approaching object to trigger the opening of the dustbin.
- **Servo Motor (SG90):** Controls the lid of the dustbin, opening and closing it based on input from the ultrasonic sensor.
- **Arduino:** Manages the sensor data and controls the servo motor.
- **Power Supply:** Powers the Arduino and the connected components.
## Circuit Description
The ultrasonic sensor is connected to the Arduino to continuously monitor the distance of any object in front of the dustbin. When the sensor detects an object within a specified range (e.g., 20 cm), the Arduino signals the servo motor to rotate and open the lid. After a short delay, the lid closes automatically.

## Future Enhancements
- **Battery-Powered Operation:** Adding a battery pack to make the system completely portable.
- **Trash Level Detection:** Integrating a second ultrasonic sensor inside the dustbin to measure the fill level and alert the user when it's time to empty the bin.
- **Mobile Notification:** Adding a Wi-Fi module to send notifications when the dustbin is full or needs maintenance.
- **Solar Power Integration:** Using solar panels to power the dustbin, making it energy-independent.
```
#include <Servo.h>

// Define the pins for the ultrasonic sensor and servo motor
const int trigPin = 9;
const int echoPin = 10;
Servo dustbinLid;

void setup() {
  // Set up the ultrasonic sensor pins
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // Attach the servo motor to pin 3
  dustbinLid.attach(3);
  
  // Start with the lid closed
  dustbinLid.write(0);
  
  // Begin serial communication (optional)
  Serial.begin(9600);
}

void loop() {
  // Measure distance from ultrasonic sensor
  long duration, distance;
  
  // Send a pulse from the trigger pin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the pulse from the echo pin
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance in cm
  distance = (duration * 0.034) / 2;
  
  // If the distance is less than 20 cm, open the lid
  if (distance < 20) {
    dustbinLid.write(90);  // Open the lid to 90 degrees
    delay(3000);           // Keep the lid open for 3 seconds
    dustbinLid.write(0);   // Close the lid
  }

  delay(100);  // Small delay to prevent constant triggering
}
```
## Applications
- Households: Automate waste disposal in kitchens or bathrooms to reduce contact with trash cans.
- Public Spaces: Can be implemented in public areas like parks, malls, and airports to encourage hygienic waste disposal.
- Offices: Used in workspaces to promote cleanliness and limit germ transmission.

## Conclusion
The Smart Dustbin project provides a simple yet effective way to improve hygiene by minimizing direct contact with trash bins. With its affordable components and easy-to-implement design, it can be scaled for various environments. The future enhancements listed offer opportunities to further improve the functionality and usability of the system.

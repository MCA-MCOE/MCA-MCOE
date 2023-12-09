#include <Servo.h>

// Define ultrasonic sensor pins
const int trigPin = 9;
const int echoPin = 10;

// Define motor driver pins
const int leftMotorPin1 = 2;
const int leftMotorPin2 = 3;
const int rightMotorPin1 = 4;
const int rightMotorPin2 = 5;

// Create Servo object to control the steering
Servo steeringServo;

void setup() {
  // Initialize serial communication
  Serial.begin(9600);

  // Set up ultrasonic sensor pins
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // Set up motor driver pins
  pinMode(leftMotorPin1, OUTPUT);
  pinMode(leftMotorPin2, OUTPUT);
  pinMode(rightMotorPin1, OUTPUT);
  pinMode(rightMotorPin2, OUTPUT);

  // Attach the servo to pin 6
  steeringServo.attach(6);
}

void loop() {
  // Measure the distance using the ultrasonic sensor
  int distance = getDistance();

  // Check if there is an obstacle in front
  if (distance < 20) {
    // If an obstacle is detected, stop the car
    stopCar();
  } else {
    // If no obstacle, move the car forward
    moveForward();
  }

  // Print the distance to the serial monitor
  Serial.print("Distance: ");
  Serial.println(distance);

  delay(100);
}

int getDistance() {
  // Trigger the ultrasonic sensor to send a pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Measure the time it takes for the echo to return
  int duration = pulseIn(echoPin, HIGH);

  // Convert the time to distance in centimeters
  int distance = duration * 0.034 / 2;

  return distance;
}

void moveForward() {
  // Move both left motors forward
  digitalWrite(leftMotorPin1, HIGH);
  digitalWrite(leftMotorPin2, LOW);

  // Move both right motors forward
  digitalWrite(rightMotorPin1, HIGH);
  digitalWrite(rightMotorPin2, LOW);

  // Optionally, you can adjust the steering to keep the car on course
  steeringServo.write(90);
}

void stopCar() {
  // Stop both left motors
  digitalWrite(leftMotorPin1, LOW);
  digitalWrite(leftMotorPin2, LOW);

  // Stop both right motors
  digitalWrite(rightMotorPin1, LOW);
  digitalWrite(rightMotorPin2, LOW);

  // Optionally, you can turn the steering to avoid the obstacle
  steeringServo.write(45);

  delay(1000); // Wait for a second

  // Resume moving forward after avoiding the obstacle
  moveForward();
}

#define leftSensorPin 2 // Left IR sensor pin
#define rightSensorPin 3 // Right IR sensor pin

#define motorLeft1 5 // Motor 1 (left) pin 1
#define motorLeft2 4 // Motor 1 (left) pin 2
#define motorRight1 7 // Motor 2 (right) pin 1
#define motorRight2 6 // Motor 2 (right) pin 2

int motorSpeed = 150; // Adjust speed (0-255)

void setup() {
  pinMode(leftSensorPin, INPUT);
  pinMode(rightSensorPin, INPUT);
  pinMode(motorLeft1, OUTPUT);
  pinMode(motorLeft2, OUTPUT);
  pinMode(motorRight1, OUTPUT);
  pinMode(motorRight2, OUTPUT);
}

void loop() {
  int leftVal = digitalRead(leftSensorPin);
  int rightVal = digitalRead(rightSensorPin);

  if (leftVal == LOW && rightVal == LOW) { // Both sensors on line (go forward)
    moveForward();
  } else if (leftVal == LOW && rightVal == HIGH) { // Sharp right turn needed
    turnLeft();
  } else if (leftVal == HIGH && rightVal == LOW) { // Sharp left turn needed
    turnRight();
  } else { // Both sensors off line (stop)
    stopMotors();
  }
}

void moveForward() {
  digitalWrite(motorLeft1, HIGH);
  digitalWrite(motorLeft2, LOW);
  digitalWrite(motorRight1, HIGH);
  digitalWrite(motorRight2, LOW);
  analogWrite(motorLeft1, motorSpeed);
  analogWrite(motorRight1, motorSpeed);
}

void turnLeft() {
  digitalWrite(motorLeft1, LOW);
  digitalWrite(motorLeft2, HIGH);
  digitalWrite(motorRight1, HIGH);
  digitalWrite(motorRight2, LOW);
  analogWrite(motorRight1, motorSpeed);
  delay(100); // Adjust turning duration as needed
}

void turnRight() {
  digitalWrite(motorLeft1, HIGH);
  digitalWrite(motorLeft2, LOW);
  digitalWrite(motorRight1, LOW);
  digitalWrite(motorRight2, HIGH);
  analogWrite(motorLeft1, motorSpeed);
  delay(100); // Adjust turning duration as needed
}

void stopMotors() {
  digitalWrite(motorLeft1, LOW);
  digitalWrite(motorLeft2, LOW);
  digitalWrite(motorRight1, LOW);
  digitalWrite(motorRight2, LOW);
}

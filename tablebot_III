// Phase III TABLEBot Code

#include <Servo.h>               // Load "Servo" library
Servo servoLeft;                 // Left drive servo
Servo servoRight;                // Right drive servo
const int BumpLeft = 4;          // Left bumper Pin 4
const int BumpRight = 5;         // Right bumper Pin 5
int BumpStateLeft = 0;           // Set Left Bump State value
int BumpStateRight = 0;          // Set Right Bump State value
int pingPin1 = 10;               // Set Ping Sensor Pin
int pingPin2 = 11;               // Set Ping Sensor Pin
long raw_distance1;               // Value for Raw Distance Ping Pulse
long raw_distance2;               // Value for Raw Distance Ping Pulse
int val6 = 0;                    // Value for Left Front IR
int val7 = 0;                    // Value for Right Front IR
int val8 = 0;                    // Value for Left Rear IR
int val9 = 0;                    // Value for Right Rear IR
int x = 0;                       // Counter Variable
int y = 0;                       // Counter Variable

void setup() {
  Serial.begin(9600);                   // Setup serial monitor for debug
  servoLeft.attach(2);                  // Set left servo to pin 2
  servoRight.attach(3);                 // Set right servo to pin 3
  pinMode(BumpLeft, INPUT_PULLUP);             // Set BumperLeft to input with pullup resistor
  pinMode(BumpRight, INPUT_PULLUP);            // Set BumperRight to input with pullup resistor
}

void loop() {

  BumpStateLeft = digitalRead(BumpLeft);
  //  Serial.println (BumpStateLeft, DEC);
  if (BumpStateLeft == 0) {
    goal();
  }

  BumpStateRight = digitalRead(BumpRight);
  //  Serial.println (BumpStateRight, DEC);
  if (BumpStateRight == 0) {
    goal();
  }

  read_ping1();

  if (raw_distance1 < 700) {
    goal();
  }

  if (raw_distance1 < 5000) {
    read_ping2();
  }

  if (raw_distance2 - 500 > raw_distance1) {
    forward();
  }

  if (raw_distance1 > 5000) {

    x = 0;
    while (x < 100) {
      clockwise();
      x++;
    }
    x = 0;
    while (x < 100) {
      stop();
      x++;
    }
    y++;
    if (y > 10) {
      x = 0;
      while (x < 200) {
        forward();
        x++;
        y = 0;
      }
    }
  }
}

void read_ping1() {
  pinMode(pingPin1, OUTPUT);
  digitalWrite(pingPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(pingPin1, HIGH);
  delayMicroseconds(5);
  digitalWrite(pingPin1, LOW);

  pinMode(pingPin1, INPUT);
  raw_distance1 = pulseIn(pingPin1, HIGH);

  Serial.print(raw_distance1);
  Serial.println();
  delay(10);
}

void read_ping2() {
  pinMode(pingPin2, OUTPUT);
  digitalWrite(pingPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(pingPin2, HIGH);
  delayMicroseconds(5);
  digitalWrite(pingPin2, LOW);

  pinMode(pingPin2, INPUT);
  raw_distance2 = pulseIn(pingPin2, HIGH);

  Serial.print(raw_distance2);
  Serial.println();
  delay(10);
}

void stop() {
  servoLeft.write(90);
  servoRight.write(90);
  delay (2);
  //  ir_check();
}

void left_forward() {
  servoLeft.write(180);
  servoRight.write(90);
  delay (2);
  //  ir_check();
}

void left_reverse() {
  servoLeft.write(0);
  servoRight.write(90);
  delay (2);
  //  ir_check();
}

void right_forward() {
  servoLeft.write(90);
  servoRight.write(0);
  delay (2);
  //  ir_check();
}

void forward() {
  servoLeft.write(180);
  servoRight.write(0);
  delay(2);
  ir_check();
}

void counterclockwise() {
  servoLeft.write(0);
  servoRight.write(0);
  delay(2);
  //  ir_check();
}

void right_reverse() {
  servoLeft.write(90);
  servoRight.write(180);
  delay (2);
  //  ir_check();
}

void clockwise() {
  servoLeft.write(180);
  servoRight.write(180);
  delay(2);
  //  ir_check();
}

void reverse() {
  servoLeft.write(0);
  servoRight.write(180);
  delay(2);
  //  ir_check();
}

void ir_check() {
  val6 = digitalRead(6);
  //  Serial.println(val6);              // debug value
  if (val6 == 1) {

    x = 0;
    while (x < 100) {
      stop();
      x++;
    }

    x = 0;
    while (x < 100) {
      reverse();
      x++;
    }

    x = 0;
    while (x < 200) {
      clockwise();
      x++;
    }
  }

  val7 = digitalRead(7);
  //  Serial.println(val7);             // debug value
  if (val7 == 1) {

    x = 0;
    while (x < 100) {
      stop();
      x++;
    }

    x = 0;
    while (x < 100) {
      reverse();
      x++;
    }

    x = 0;
    while (x < 100) {
      counterclockwise();
      x++;
    }
  }
}

void goal() {

  read_ping2();
  if (raw_distance2 > 5000) {

    x = 0;
    while (x < 100) {
      clockwise();
      x++;
    }
    x = 0;
    while (x < 100) {
      stop();
      x++;
    }
    y++;
    if (y > 10) {
      x = 0;
      while (x < 200) {
        forward();
        x++;
        y = 0;
      }
    }
  }

  if (raw_distance2 < 5000) {
    forward();
  }

  if (raw_distance2 < 1500) {

    dance();
  }

  loop();
}

void dance() {

  x = 0;
  while (x < 400) {
    reverse();
    x++;
  }
  x = 0;
  while (x < 400) {
    clockwise();
    x++;
  }

  end();
}

void end() {

  stop();
  end();

}

#include <Servo.h>

Servo myservo;  // JAW // create servo object to control a servo // twelve servo objects can be created on most boards
Servo myservo2; // MANE // this is where you declare how many servos you need. (next one would have a 3 on it)
Servo myservo3; // MANE 2 // with each coorelating code you need to make sure to link it ot the correct servo
Servo myservo4; // EYES

int pos = 0;    // variable to store the servo position (tells where the final pos # is)

#include <Adafruit_NeoPixel.h>
#define PIN 13
#define NUMPIXELS 2

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  myservo.attach(9);   //JAW
  myservo2.attach(10); // MANE
  myservo3.attach(11); // MANE 2
  myservo4.attach(13); // EYES
  Serial.begin(9600);
  pixels.begin();
}

void loop() {
  

  //JAW:
  for (pos = 0; pos <= 180; pos += 1) {
    myservo.write(pos);
  delay(10);
}
for (pos = 180; pos >= 0; pos -= 1) {
  myservo.write(pos);
  delay(30);
}

//MANE:
  int pos;
  for (pos = 10; pos <= 170; pos += 1) {
    myservo2.write(pos);
    myservo3.write(pos);
    delay(5);
  }
  int i = 0;
  int distance = analogRead(A0);

//EYES:
  Serial.println(distance);

  if (distance < 200) {
    pixels.setPixelColor(0, pixels.Color (150, 0, 0));
    pixels.setPixelColor(1, pixels.Color (150, 0, 0));
  }
  else {
    pixels.setPixelColor(0, pixels.Color(random(0, 150), random(0, 150), random(0, 150)));
    pixels.setPixelColor(1, pixels.Color(random(0, 150), random(0, 150), random(0, 150)));

  }
  pixels.show();
}

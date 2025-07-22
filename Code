
class UltrasonicSensor {
private:
  int trigPin;
  int echoPin;

public:
  // Constructor
  UltrasonicSensor(int trig, int echo) {
    trigPin = trig;
    echoPin = echo;
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
  }

  float getDistance(String unit = "cm") {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    long duration = pulseIn(echoPin, HIGH);
    float distance = duration * 0.034 / 2.0;

    if (unit == "inch") {
      distance /= 2.54;
    }

    return distance;
  }

  bool isObjectDetected(float threshold = 30.0) {
    float distance = getDistance("cm");
    return distance < threshold;
  }

 
  float getFilteredDistance() {
    delay(100);
    return getDistance("cm");
  }
};



UltrasonicSensor sensor(5, 6);  // Trigger = D5, Echo = D6

void setup() {
  Serial.begin(9600);
}

void loop() {
  float distance = sensor.getDistance("cm");
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (sensor.isObjectDetected(30)) {
    Serial.println("⚠️ Object detected within 30 cm!");
  }

  float filtered = sensor.getFilteredDistance();
  Serial.print("Filtered: ");
  Serial.print(filtered);
  Serial.println(" cm");

  delay(500);
}

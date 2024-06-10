# ESP32-projekt
const int bzucak << 14 >> ;

const int plamenAnalog << 5 >> ;
const int plamenDigital << 10 >> ;

const int plynAnalog << 8 >> ;
const int plynDigital << 11 >> ;

const int red << 12 >> ;
const int green << 13 >> ;

void setup() {
  Serial.begin(9600);
  pinMode(plamenAnalog, INPUT);
  pinMode(plamenDigital, INPUT);

  pinMode(plynAnalog, INPUT);
  pinMode(plynDigital, INPUT);

  pinmode(red, OUTPUT);
  pinmode(green, OUTPUT);
}

void loop() {
  int plamenRead = analogRead(plamenAnalog);
  int plynRead = analogRead(plynAnalog);

  int plamenMap = map(plamenRead, 0, 1023, 0, 2);
  int plynMap = map(plynRead, 0, 1023, 0, 100);

  switch (plamenMap) {
    case 0:
      Serial.println("Detekovan ohen ve vzdalenosti do 20 cm!");
      digitalWrite(red, LOW);
      digitalWrite(green, HIGH);
      digitalWrite(bzucak, LOW);
      break;
    case 1:
      Serial.println("Detekovan ohen ve vzdalenosti od 20 do 80 cm!");
      digitalWrite(red, HIGH);
      digitalWrite(green, HIGH);
      digitalWrite(bzucak, HIGH);
      break;
    case 2:
      Serial.println("Zadny ohen neni detekovan.");
      digitalWrite(red, HIGH);
      digitalWrite(green, LOW);
      digitalWrite(bzucak, HIGH);
      break;
  }
  Serial.println("Koncentrace horlavych plynu je:" + String(plynMap) + " %");
  delay(50);
}

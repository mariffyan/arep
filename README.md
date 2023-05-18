const int pinLED = 13;
const int pinLDR = A1;
const int pinDO = 2;
const int pinAO = A0;
int val_analog;
int val_digital;
int enA = 9;
int in1 = 8;
int in2 = 7;
int enB = 3;
int in3 = 5;
int in4 = 4;

void setup() {
Serial.begin(9600);
pinMode(pinLED, OUTPUT);
pinMode(pinLDR, INPUT);
pinMode(pinDO, INPUT);
pinMode(pinAO, INPUT);
pinMode(enA, OUTPUT);
pinMode(enB, OUTPUT);
pinMode(in1, OUTPUT);
pinMode(in2, OUTPUT);
pinMode(in3, OUTPUT);
pinMode(in4, OUTPUT);
digitalWrite(in1, LOW);
digitalWrite(in2, LOW);
digitalWrite(in3, LOW);
digitalWrite(in4, LOW);
}

void inside() {
digitalWrite (pinLED, HIGH);
analogWrite(enA,125);
digitalWrite(in1,LOW);
digitalWrite(in2,HIGH);
analogWrite(enB,125);
digitalWrite(in3,LOW);
digitalWrite(in4,HIGH);
Serial.println("go in"); 
}

void outside() {
digitalWrite (pinLED, LOW);
analogWrite(enA,125);
digitalWrite(in1,HIGH);
digitalWrite(in2,LOW);
analogWrite(enB,125);
digitalWrite(in3,HIGH);
digitalWrite(in4,LOW);
Serial.println("go out");
}

void off() {
analogWrite(enA,0);
digitalWrite(in1,LOW);
digitalWrite(in2,LOW);
analogWrite(enB,0);
digitalWrite(in3,LOW);
digitalWrite(in4,LOW);
Serial.println("off");
delay(5000);
}

void loop() {

int ldrStatus = analogRead(pinLDR);
Serial.print("ldr : ");
Serial.println(ldrStatus);
val_digital=digitalRead(pinDO);
val_analog=analogRead(pinAO);
Serial.println(val_analog);
delay(1000);

if (digitalRead(pinLED)==HIGH) {
if (ldrStatus > 20){
if (val_digital == HIGH) {
outside(); delay(400);
off(); delay(2000);
}
}
}
else if (ldrStatus <= 20) {
inside(); delay(400);
off(); delay(2000);
}
else if (ldrStatus > 20) {
if (val_digital == LOW) {
inside(); delay(400);
off(); delay(2000);
}
}
}

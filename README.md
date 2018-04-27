# smart-black-box
#include <SoftwareSerial.h>

SoftwareSerial mySerial(2, 3); // RX, TX

const int trigPin = 5;
const int echoPin = 6;
const int ir = 4;

long duration;2
int distance;

char a[72];
char b[7]="$GPRMC";
unsigned int c=0;
int e,i=0;

int ir_read;

void setup() 
{
Serial.begin(9600);
  mySerial.begin(9600);
  
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(ir, INPUT);
}

void loop() {
//for(i=0;i<200;i++)
{
  if(Serial.available())
{
  a[c]=Serial.read();
  //Serial.println(a[c]);
  c++;
  if(c<7)
  {
    if(a[c-1]!=b[c-1])
    {
          c=0;
     } 
  }
  if(c==70)
  {
    c=0;
    Serial.print("Lat: ");
    Serial.print(a[19]);
    Serial.print(a[20]);
    Serial.print(a[21]);
    Serial.print(a[22]);
    Serial.print(a[23]);
    Serial.print(a[24]);
    Serial.print(a[25]);
    Serial.print(a[26]);
    Serial.print(a[27]);
    Serial.print(a[28]);
    Serial.print('\n');
    Serial.print("Lon: ");
    Serial.print(a[32]);
    Serial.print(a[33]);
    Serial.print(a[34]);
    Serial.print(a[35]);
    Serial.print(a[36]);
    Serial.print(a[37]);
    Serial.print(a[38]);
    Serial.print(a[39]);
    Serial.print(a[40]);
    Serial.print(a[41]);
    Serial.print(a[42]);
    Serial.print('\n');


      digitalWrite(trigPin, LOW);
delayMicroseconds(2);

digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);

distance= duration*0.034/2;

Serial.print("Distance: ");
Serial.println(distance);

if(distance<10)
{
    Serial.println("u r crossing limit");
mySerial.println("AT");
mySerial.println("AT+CMGF=1");
delay(1000);
mySerial.println("AT+CMGS=\"+919791452158\"");
mySerial.print("u r crossing limit");

    mySerial.print("Lat:");
    mySerial.print(a[19]);
    mySerial.print(a[20]);
    mySerial.print(a[21]);
    mySerial.print(a[22]);
    mySerial.print(a[23]);
    mySerial.print(a[24]);
    mySerial.print(a[25]);
    mySerial.print(a[26]);
    mySerial.print(a[27]);
    mySerial.print(a[28]);
    mySerial.print(',');
    mySerial.print("Lon: ");
    mySerial.print(a[32]);
    mySerial.print(a[33]);
    mySerial.print(a[34]);
    mySerial.print(a[35]);
    mySerial.print(a[36]);
    mySerial.print(a[37]);
    mySerial.print(a[38]);
    mySerial.print(a[39]);
    mySerial.print(a[40]);
    mySerial.print(a[41]);
    mySerial.print(a[42]);


mySerial.println(char(26));
delay(2000);
}

ir_read = digitalRead(ir);
//Serial.println("ir:");
Serial.println(ir_read);
if(ir_read==0)
{
Serial.println("no vibration detected");
}
else
{
 Serial.println("vibration detected");
mySerial.println("AT");
mySerial.println("AT+CMGF=1");
delay(1000);
mySerial.println("AT+CMGS=\"+919791452158\"");
mySerial.println("vibration detected");

    mySerial.print("Lat:");
    mySerial.print(a[19]);
    mySerial.print(a[20]);
    mySerial.print(a[21]);
    mySerial.print(a[22]);
    mySerial.print(a[23]);
    mySerial.print(a[24]);
    mySerial.print(a[25]);
    mySerial.print(a[26]);
    mySerial.print(a[27]);
    mySerial.print(a[28]);
    mySerial.print(',');
    mySerial.print("Lon: ");
    mySerial.print(a[32]);
    mySerial.print(a[33]);
    mySerial.print(a[34]);
    mySerial.print(a[35]);
    mySerial.print(a[36]);
    mySerial.print(a[37]);
    mySerial.print(a[38]);
    mySerial.print(a[39]);
    mySerial.print(a[40]);
    mySerial.print(a[41]);
    mySerial.print(a[42]);                                         

mySerial.println(char(26));
delay(2000);
}

    delay(500);
  }
  }  


  
}

}

# immediate-animal-recognition-using-ml-approches

const int trigPin = 10;
const int echoPin = 11;
long duration;
int distance;
#include <SoftwareSerial.h>

SoftwareSerial mySerial(9, 8); //rx tx 

void setup() 
{
  pinMode(trigPin, OUTPUT);
  mySerial.begin(9600);   // Setting the baud rate of GSM Module 
 
  pinMode(echoPin, INPUT); 
  Serial.begin(9600); 
}

void loop() 
{
  dist();
}
void dist()
{
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance= duration*0.034/2;
  Serial.println(distance);
  if(distance<10)
  {
    delay(200);
    Serial.println("The Person is detected sending message through gsm");
     
     //gsm code below
     mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
        delay(1000);  // Delay of 1000 milli seconds or 1 second
        mySerial.println("AT+CMGS=\"+xxxxxxxxxxx\"\r"); // Replace x with mobile number
        delay(1000);
        mySerial.println("Intruder detected alert!. ");// The SMS text you want to send
        delay(100);
        mySerial.println((char)26);// ASCII code of CTRL+Z
        delay(1000);
    delay(5000);
    
  }
}

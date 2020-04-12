/*
 Programmable Robotic Arm Using a Infrared Remote
 CS 207 project
 Yunseok Kim
 April 9, 2020
 */

#include <IRremote.h> //IR remote library by Ken Shirriff
#include <Servo.h>

//Servo motors
Servo servo1;
Servo servo2;
Servo servo3;

//IR remote sensor pin
const int RECV_PIN = 4;

//servo position start at 90 degrees
int pos = 90;

//last code received
unsigned long lastCode;

//IR receiver and results object
IRrecv irrecv(RECV_PIN);
decode_results results;

//Save positions for servos
int servo1PosSaves[] = {1,1,1,1,1};
int servo2PosSaves[] = {1,1,1,1,1};
int servo3PosSaves[] = {1,1,1,1,1};

//LED pins
const int LED1 = 2;
const int LED2 = 3;
const int LED3 = 7;
const int LED4 = 8;
const int LED5 = 13;

//counter variable for position recording
int recordPosition = 0;

void setup() 
{
  //attach servos to pin
  servo1.attach(5); 
  servo2.attach(6);
  servo3.attach(9);

  //set LEDs as outputs
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(LED4, OUTPUT);
  pinMode(LED5, OUTPUT);

  //start receiver
  irrecv.enableIRIn();

  //set serial printing
  Serial.begin(9600);

  //start servos at 90 degrees
  servo1.write(pos);
  servo2.write(pos);
  servo3.write(pos);
}

void loop()
{
  if(irrecv.decode(&results)) //check if code received
  {
    if(results.value == 0xFFFFFFFF)
    {
      //if repeat, then use last code received
      results.value = lastCode;
    }

    if(results.value == 0xFF10EF) //left button
    {
      //left button pressed
      lastCode = results.value;
      //move left 2 degrees
      pos += 2;
      //stop position above 180
      if(pos>180){pos = 180;}
      servo1.write(pos);
    }

    if(results.value == 0xFF5AA5) //right button
    {
      //right button pressed
      lastCode = results.value;
      //move right 2 degrees
      pos -= 2;
      //stop position below 0
      if (pos<0){pos=0;}
      servo1.write(pos);
    }

    if(results.value == 0xFF22DD) // 4 button on remote
    {
      //4 button pressed
      lastCode = results.value;
      //move left 2 degrees
      pos += 2;
      //stop position above 180
      if(pos>180){pos = 180;}
      servo2.write(pos);
    }

    if(results.value == 0xFFC23D) // 6 button on remote
    {
      //6 button pressed
      lastCode = results.value;
      //move right 2 degrees
      pos -= 2;
      //stop position below 0
      if (pos<0){pos=0;}
      servo2.write(pos);
    }

    if(results.value == 0xFF6897) // * button on remote
    {
      //* button pressed
      lastCode = results.value;
      //move left 2 degrees
      pos += 2;
      //stop position above 180
      if(pos>180){pos = 180;}
      servo3.write(pos);
    }

    if(results.value == 0xFFB04F) //# button on remote
    {
      //# button pressed
      lastCode = results.value;
      //move right 2 degrees
      pos -= 2;
      //stop position below 0
      if (pos<0){pos=0;}
      servo3.write(pos);
    }
    
    //Add delay to prevent false readings
    delay(30);
    //receive the next value
    irrecv.resume();

    //Keep count of how many times okay is pressed on remote and save position of servos
    if(results.value == 0xFF38C7){ 
    recordPosition++;
    switch(recordPosition){
      case 1:
        servo1PosSaves[0] = pos;
        servo2PosSaves[0] = pos;
        servo3PosSaves[0] = pos;
        digitalWrite(LED1, HIGH);
        Serial.println("Pos 1 Saved");
        break;
      case 2:
         servo1PosSaves[1] = pos;
         servo2PosSaves[1] = pos;
         servo3PosSaves[1] = pos;
         digitalWrite(LED2, HIGH);
         Serial.println("Pos 2 Saved");
         break;
      case 3:
         servo1PosSaves[2] = pos;
         servo2PosSaves[2] = pos;
         servo3PosSaves[2] = pos;
         digitalWrite(LED3, HIGH);
         Serial.println("Pos 3 Saved");
         break;
      case 4:
         servo1PosSaves[2] = pos;
         servo2PosSaves[2] = pos;
         servo3PosSaves[2] = pos;
         digitalWrite(LED4, HIGH);
         Serial.println("Pos 4 Saved");
         break;
      case 5:
         servo1PosSaves[2] = pos;
         servo2PosSaves[2] = pos;
         servo3PosSaves[2] = pos;
         digitalWrite(LED5, HIGH);
         Serial.println("Pos 5 Saved");
         break;
  }

    //if 0 is pressed on remote, replay the saved positions
    if(results.value == 0xFF9867)
    {
      for(int i = 0; i < 5; i++)
      {
        servo1.write(servo1PosSaves[i]);
        servo2.write(servo2PosSaves[i]);
        servo3.write(servo3PosSaves[i]);
        delay(1050);
      }
    }
    delay(300);
    }
  } 
}

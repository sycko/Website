---
layout: page
title: "Electronics Blog"
date: 2014-09-08 11:37
comments: true
sharing: true
footer: true
---

Week 4
---

In this lab we used our first Lab's code as an oscillator. This made a very basic monophonic squarewave synth that can hit different notes. My breadboard could only fit five buttons and therefore could only play 5 programmable notes. 

In addition to programming different notes, we also used the "void playFrequency(int freq)" function in order to tidy up our code. This function allowed us to use one line of code instead of four when programming the frequency of each note being played.

My final code is below:

```
int oscillatorPin = 13;

int gNoteButtonPin = 8;
int aNoteButtonPin = 9;
int bNoteButtonPin = 10;
int cNoteButtonPin = 11;
int dNoteButtonPin = 12;

//you can find the frequency of different notes here:
//http://www.phy.mtu.edu/~suits/notefreqs.html
int middleGFrequency = 196;
int middleAFrequency = 220;
int middleBFrequency = 246;
int middleCFrequency = 261;
int middleDFrequency = 294;

void setup() {
   pinMode(oscillatorPin, OUTPUT);
   pinMode(gNoteButtonPin, INPUT);
   pinMode(aNoteButtonPin, INPUT);
   pinMode(bNoteButtonPin, INPUT);
   pinMode(cNoteButtonPin, INPUT);
   pinMode(dNoteButtonPin, INPUT);
}

void loop() {

   if(digitalRead(cNoteButtonPin) == HIGH) {

      playFrequency(middleCFrequency);

   } else if(digitalRead(dNoteButtonPin) == HIGH) {

      playFrequency(middleDFrequency);
     
   } else if(digitalRead(bNoteButtonPin) == HIGH) {

      playFrequency(middleBFrequency);
     
   } else if(digitalRead(aNoteButtonPin) == HIGH) {

      playFrequency(middleAFrequency);
      
   } else if(digitalRead(gNoteButtonPin) == HIGH) {

      playFrequency(middleGFrequency);

   } else {
      //do some other stuff if you want anything to happen
 }
}

void playFrequency(int freq) {
   digitalWrite(oscillatorPin, HIGH);
   delayMicroseconds(1000000 / freq / 2);
   digitalWrite(oscillatorPin, LOW);
   delayMicroseconds(1000000 / freq / 2);
}
```

Week 3
---
Part 1

``` 
int ledPin = 13;
int potVal = 0;
 
int currentMidiChannel = 3;
int currentMidiNote = 0;
int currentMidiVelocity = 127;
 
void setup() {
  pinMode(ledPin, OUTPUT);
}
 
void loop() {
   
  digitalWrite(ledPin, HIGH);
  delay(100);
  digitalWrite(ledPin, LOW);
   
  //analogRead() returns a number between 0 and 1023
  potVal = analogRead(1);
  //a midi note can only be between 0 and 127, same with a midi velocity
  currentMidiNote = potVal/8;
   
  usbMIDI.sendNoteOn(currentMidiNote, currentMidiVelocity, currentMidiChannel);
  delay(1000);
  usbMIDI.sendNoteOff(currentMidiNote, 0, currentMidiChannel);
}
```

Part 4

``` 
int led = 13;
int buttonPin = 12;
int potVal = 0;
int currentMidiChannel = 3;
int currentMidiNote = 0;
int currentMidiVelocity = 127;
int buttonPin2 = 11;

void setup() {
   Serial.begin(9600);
   pinMode(led, OUTPUT);
   pinMode(buttonPin, INPUT);
   pinMode(buttonPin2, INPUT);
 }
 
void loop() {
   if(digitalRead(buttonPin) == HIGH) {
 
      potVal = analogRead(1); //read the analog values from the potometer
      currentMidiNote = 60;
      Serial.println(potVal);
      currentMidiVelocity = potVal/8;
 
      digitalWrite(led, HIGH);
      delay(1000);
      digitalWrite(led, LOW);
      
   if(digitalRead(buttonPin2) == HIGH)
 
      potVal = analogRead(1); //read the analog values from the potometer
      currentMidiNote = 67;
      Serial.println(potVal);
      currentMidiVelocity = potVal/8;
 
      digitalWrite(led, HIGH);
      delay(1000);
      digitalWrite(led, LOW);
 
  usbMIDI.sendNoteOn(currentMidiNote, currentMidiVelocity, currentMidiChannel);
  delay(1000);
  usbMIDI.sendNoteOff(currentMidiNote, 48, currentMidiChannel);
 
   } else if(digitalRead(buttonPin) == LOW) {
 
      digitalWrite(led, LOW);
      Serial.println("off");
   }
}
```

Week 2
---
Question 2b

``` 
int led = 13; //create a variable called led with a value of 13
int buttonPin = 12; //create a variable called buttonPin with a value of 12
int potVal = 0; //create a variable called potVal with a value of 0
 
void setup() { //setup for the led and button
//   Serial.begin(9600);
   pinMode(led, OUTPUT); //sets the led to behave as an output
   pinMode(buttonPin, INPUT); //sets the button to behave as an input
}
 
void loop() { //sends no information back to the loop
   if(digitalRead(buttonPin) == HIGH) { //if the buttonPin is read to be receiving voltage
 
      potVal = analogRead(1); //the potVal is set to change the signal
//      Serial.println(potVal);
 
      digitalWrite(led, HIGH); //turns led on
      delay(potVal); //the delay is set to the potVal
      digitalWrite(led, LOW); //turns led off
      delay(potVal); //the delay is set to the potVal
 
   } else if(digitalRead(buttonPin) == LOW) { //if the buttonPin is read to be receiving no voltage
 
      digitalWrite(led, LOW); //the led is off
//      Serial.println("off");
   }
}
```
Question 2c

``` 
int led = 13; //create a variable called led with a value of 13
int buttonPin = 12; //create a variable called buttonPin with a value of 12
int potVal = 0; //create a variable called potVal with a value of 0
int led2 = 11; //create a variable called led2 with a value of 11
 
void setup() { //setup for the led and button
//   Serial.begin(9600);
   pinMode(led, OUTPUT); //sets the led to behave as an output
   pinMode(led2, OUTPUT); //sets the led2 to behave as an output
   pinMode(buttonPin, INPUT); //sets the button to behave as an input
}
 
void loop() { //sends no information back to the loop
   if(digitalRead(buttonPin) == HIGH) { //if the buttonPin is read to be receiving voltage
 
      potVal = analogRead(1); //the potVal is set to change the signal
//      Serial.println(potVal);
 
      digitalWrite(led, HIGH); //turns led on
      digitalWrite(led2, LOW); //turns led2 off
      delay(potVal); //the delay is set to the potVal
      digitalWrite(led, LOW); //turns led off
      digitalWrite(led2, HIGH); // turns led2 on
      delay(potVal); //the delay is set to the potVal
 
   } else if(digitalRead(buttonPin) == LOW) { //if the buttonPin is read to be receiving no voltage
 
      digitalWrite(led, LOW); //the led is off
//      Serial.println("off");
   }
}
```

Week 1
---

<a href=http://www.instructables.com/id/Arcade-Button-MIDI-Controller/?ALLSTEPS >These</a> are instructions for a MIDI controller built using an Arduino microcontroller.  This controller can send and receive MIDI messages to your PC, and allows you to control your software program such as Traktor. The white arcade buttons you see in the picture are the inputs and each button is mapped to a different sound/signal. When a button is pressed, it sends a signal to the software which is then sent to the listener.

<a href=http://www.instructables.com/id/LED-Dance-Room/?ALLSTEPS >This</a> is a guide to build an Audio Visualizer using an Arduino microcontroller.  This visualizer receives audio from the microphone jack of your computer, allowing it to accept it’s own sound fed back, or sound from any other audio playing device. The change in sound causes the lights to pulse and change.

<a href=http://www.instructables.com/id/Music-Party-Facebook-Connected-Arduino-Powered-/ >This</a> is an automatically shuffling music player run by an Arduino microcontroller. A RFID reader reads the unique ID of whatever device/card was placed near it. The signal is then sent to the Arduino microcontroller, which sends a signal to the music server. Once that process is completed the preferred music of the device/card owner is added to playlist to be shuffled.

<a href=http://www.instructables.com/id/Electronic-Music-Box-Powered-by-Arduino-sort-of/ >This</a> is the design for a music box powered by an Arduino microcontroller. The music is stored on a piece of paper and read through the device. As the paper passes through the device an infrared light reads the black and white marking on the paper and sends a signal to be played by the music box.

<a href=http://www.instructables.com/id/This-Is-Your-Brain-On-Music/step3/Beat-detection-music-visualization-Arduino-and-Pro/ >This</a> is a design for a musical beat detector controlled by an Arduino microcontroller. The designer uses processing to register the sound, which is then transmitted to the visualizer. By using processing, the designer doesn't have to worry about white noise. To get different colors, the designer assigned colors to different buckets. When a beat lands in a certain bucket, that color is displayed.

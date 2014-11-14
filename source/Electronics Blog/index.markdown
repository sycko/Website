---
layout: page
title: "Electronics Blog"
date: 2014-09-08 11:37
comments: true
sharing: true
footer: true
---

Week 10
---
```
int oscillatorPin = 8;
int sensorVal = 0;
int mappedSensorVal = 0;



void setup() {
   pinMode(oscillatorPin, OUTPUT);
   pinMode(sensorVal, INPUT);
  
}

void loop() {
   
   sensorVal = analogRead(0); {
   mappedSensorVal = map(sensorVal, 150, 550, 65, 523);


      digitalWrite(oscillatorPin, HIGH);
      delayMicroseconds(1000000 / mappedSensorVal / 2);
      digitalWrite(oscillatorPin, LOW);
      delayMicroseconds(1000000 / mappedSensorVal / 2);
     
   } 
}

void playFrequency(int freq) {
   digitalWrite(oscillatorPin, HIGH);
   delayMicroseconds(1000000 / freq / 2);
   digitalWrite(oscillatorPin, LOW);
   delayMicroseconds(1000000 / freq / 2);
}
```

In regards to my final project, I am planning on making a button MIDI controller. Allowing me to use it as a makshift keyboard, or any other MIDI instrument. For this project I will need a couple of items that I don't already have. Including a 4x4 Adafruit Trellis Monochrome Driver, a silicone elastomer 4x4 button keypad. I will also need 4 10k potentiometers, LEDs, cutters, and jumper wires. I look forward to completing this project and using it in the future.

Week 9
---
```
IntervalTimer oscTimer;
volatile int oscPin = 8;
 
int led1Pin = 9;
int led2Pin = 10;
int led3Pin = 11;
int led4Pin =12;

int buttonPin1 = 7;
int buttonPin2 = 19;

 
int numSteps = 4;
int tempo = 100;
volatile int currentFrequency = 261;
volatile int oscCounter = 0;
volatile int oscState = HIGH;
 
void setup() {
  pinMode(oscPin, OUTPUT);
  pinMode(led1Pin, OUTPUT);
  pinMode(led2Pin, OUTPUT);
  pinMode(led3Pin, OUTPUT);
  pinMode(led4Pin, OUTPUT);
  pinMode(buttonPin1, INPUT);
  pinMode(buttonPin2, INPUT);
 
  oscTimer.begin(playNote, 1);
}


 
void loop() {
 if(digitalRead(buttonPin1) == LOW) { 
   for(int i=0; i<numSteps; i++) {
      setCurrentStep(i);
      delay(analogRead(0));
   }
 }
   else if(digitalRead(buttonPin1) == HIGH) {
     for(int i=3; i<numSteps && i>=0; i--) {
       setCurrentStep(i);
       delay(analogRead(0));
   } 
  }
   if(digitalRead(buttonPin2) == HIGH) {
     Serial.println('hello');
     for(int i=0; i<numSteps; i++) {
       long stepValue = random(0,4);
       setCurrentStep((int)stepValue);
       delay(analogRead(0));
       
     }
   }
}
 
void setCurrentStep(int stepNum) {
  setCurrentLed(stepNum);
  setTone(stepNum);
  }
 
void setTone(int stepNum) {
  int currentPotVal;
  if(stepNum == 0) {
    currentPotVal = analogRead(4);
  }
  if(stepNum == 1) {
    currentPotVal = analogRead(3);
  }
  if(stepNum == 2) {
    currentPotVal = analogRead(2);
  }
  if(stepNum == 3) {
    currentPotVal = analogRead(1);
  }
 
  currentFrequency = 50 + currentPotVal;
  
}

void setCurrentLed(int stepNum) {
  turnOffAllLeds();
  turnOnLed(stepNum);
}

void turnOnLed(int stepNum) {
  if(stepNum == 0) {
    digitalWrite(led1Pin, HIGH);
  }
  else if(stepNum == 1) {
    digitalWrite(led2Pin, HIGH);
  }
  else if(stepNum == 2) {
    digitalWrite(led3Pin, HIGH);
  }
  else if(stepNum == 3) {
    digitalWrite(led4Pin, HIGH);
  }
}

void turnOffAllLeds() {
  digitalWrite(led1Pin, LOW);
  digitalWrite(led2Pin, LOW);
  digitalWrite(led3Pin, LOW);
  digitalWrite(led4Pin, LOW);
}
 
void playNote() {
 
  volatile int stepsForNote = 1000000 / currentFrequency / 2;
 
  oscCounter++;
  if(oscCounter >= stepsForNote) {
    oscCounter = 0;
  }
  if(oscCounter == 0) {
 
    if(oscState == HIGH) {
      digitalWrite(oscPin, LOW);
      oscState = LOW;
    }
    else if(oscState == LOW) {
      digitalWrite(oscPin, HIGH);
      oscState = HIGH;
    }
  }
}  
```

If I wanted to make a more advanced sequencer I could have it controlled by my DAW, or have it input MIDI into my DAW. In addition I could have multiple notes being played at the same time in a sequence, or I could have arpeggios happening on each note in the sequence.

It would be nice to know how to change the sound of each note (square, sine, sawtooth), in addition it would be cool to know how to change the sound of each note with a potometer, or being able to gradually change the harshness of the sound.


Week 8
---
```
#include <SPI.h>
 
IntervalTimer timer1;
IntervalTimer timer2;
boolean osc1State = LOW;
boolean osc2State = LOW;
 
int maxDigipotVal = 255;
 
const int osc1Pin = 7;
int slave1SelectPin = 10;
int digipot1FadeSpeed = 0;
unsigned long nextDigipot1Step = 0;
String digipot1State = "attack";
int currentDigipot1Val = 0;

 
const int osc2Pin = 8;
int slave2SelectPin = 9;
int digipot2FadeSpeed = 0;
unsigned long nextDigipot2Step = 0;
String digipot2State = "attack";
int currentDigipot2Val = 0;


void setup() {
  SPI.begin();
  Serial.begin(9600);
  pinMode(osc1Pin, OUTPUT);
  pinMode(osc2Pin, OUTPUT);
  pinMode(slave1SelectPin, OUTPUT);
  pinMode(slave2SelectPin, OUTPUT);
  digitalWrite(slave1SelectPin, HIGH);  
  digitalWrite(slave2SelectPin, HIGH);
  timer1.begin(playNote1, 1000000/261/2);  
  timer2.begin(playNote2, 1000000/440/2);  
}
 
void loop() {
  doADSR1();
  doADSR2();
}
 
void doADSR1() {
   
  if(millis() > nextDigipot1Step) { //if millis is greater than the nextDigipot1Step
 
    if(digipot1State == "attack") { //if the digipot1State is set to attack
      currentDigipot1Val = currentDigipot1Val + 1; //the currentDigipot1Val will be euqal to itself +1
      if(currentDigipot1Val == maxDigipotVal) { //if the currentDigipot1Val equals the maxDigipotVal
        digipot1State = "decay"; //change the digipot1State to decay
      }
    } else if(digipot1State == "decay") { //if the digipot1State is set to decay
      currentDigipot1Val = currentDigipot1Val - 1; //subtract 1 from the currentDigipot1Val
      digitalPotWrite(slave1SelectPin, currentDigipot1Val); //the digitalPotWrite responds to the slave1SelectPin and the current Digipot1Val      
      if(currentDigipot1Val == 0) { //if the currentDigipot1Val is 0
        digipot1State = "attack"; //change the digipot1state to attack
      }      
    }
   
    digipot1FadeSpeed = analogRead(0) / 100 + 1; //the digipot1FadeSpeed is read from the analog potometer
    nextDigipot1Step = millis() + digipot1FadeSpeed; //the nextDigipot1step is equal the millis plus digipot1Fade Speed
    digitalPotWrite(slave1SelectPin, currentDigipot1Val); //the digitalPotWrite responds to the slave1SelectPin and the current Digipot1Val
    
  }  
}
void doADSR2() {
  
  if(millis() > nextDigipot2Step) {
 
    if(digipot2State == "attack") {
      currentDigipot2Val = currentDigipot2Val + 1;
      if(currentDigipot2Val == maxDigipotVal) {
        digipot2State = "decay";
      }
    } else if(digipot2State == "decay") {
      currentDigipot2Val = currentDigipot2Val - 1;
      digitalPotWrite(slave2SelectPin, currentDigipot2Val);      
      if(currentDigipot2Val == 0) {
        digipot2State = "attack";
      }      
    }
   
    digipot2FadeSpeed = analogRead(1) / 100 + 1;  
    nextDigipot2Step = millis() + digipot2FadeSpeed;
    digitalPotWrite(slave2SelectPin, currentDigipot2Val);
    
  }  
  }
  
void playNote1() {
  if (osc1State == LOW) {
    osc1State = HIGH;
  } else {
    osc1State = LOW;
  }
  digitalWrite(osc1Pin, osc1State);
}
 
void playNote2() {
  if (osc2State == LOW) {
    osc2State = HIGH;
  } else {
    osc2State = LOW;
  }
  digitalWrite(osc2Pin, osc2State);
}
 
void digitalPotWrite(int ssPin, int val) {
  digitalWrite(ssPin, LOW);
  SPI.transfer(0);
  SPI.transfer(val);
  digitalWrite(ssPin, HIGH);
}
```

Week 7
---
```

#include <SPI.h>
 
IntervalTimer oscTimer;
 
int buttonPin = 7;
int oscillatorPin = 8;
int slaveSelectPin = 10;
 
boolean ledState = LOW;
int digipotHighestStep = 127;
int attackVal = 0;
int sustainVal = 0;
int decayVal = 0;

 
void setup() {
  pinMode(oscillatorPin, OUTPUT);
  pinMode(buttonPin, INPUT);
  pinMode(slaveSelectPin, OUTPUT);
 
  SPI.begin();
  digitalWrite(slaveSelectPin, HIGH);  
  digitalPotWrite(0);
   
  //don't mess with this, just leave it
  oscTimer.begin(playNote, 1000000/261/2);
}
 
void loop() {
 if(digitalRead(buttonPin) == HIGH) {
    attack();
    sustain();
    decay();
 }
 else if(digitalRead(buttonPin) == LOW) {
       digitalWrite(oscillatorPin, LOW);    
    }  
}

void attack() {    
    attackVal = analogRead(0);
    for(int i=0; i<=digipotHighestStep; i++) {
      attackVal = analogRead(0);    
      digitalPotWrite(i);
      delay(attackVal/50);
   }  
  }

void sustain() {
  sustainVal = analogRead(0);
  delay(sustainVal);
}

void decay() {
  decayVal = analogRead(0);
  for(int i=digipotHighestStep; i<=digipotHighestStep && i>0; i--) {
    decayVal = analogRead(0);
    digitalPotWrite(i);
    delay(decayVal/50);
  }
}

void digitalPotWrite(int val) {
  digitalWrite(slaveSelectPin, LOW);
  SPI.transfer(0);
  SPI.transfer(val);
  digitalWrite(slaveSelectPin, HIGH);
}
 
//this is for the oscillator. don't touch this function.
void playNote() {
  if (ledState == LOW) {
    ledState = HIGH;
  } else {
    ledState = LOW;
  }
  digitalWrite(oscillatorPin, ledState);
}

```

Week 6
---

MIDI Out Final Part

```
int ledPin = 13;
int oscillatorPin = 14;
int oscillator2Pin = 14;
int potVal = 0;
int pot = 15;
int buttonPin = 16;
 
int midiChannel = 3;
 
int currentMidiVelocity = 0;
int currentMidiNote = 0;
float currentFrequency = 0;
 
//this is an array of mote frequencies mapped
//to MIDI notes.  It's crucial to what we're doing
//but don't worry about it for now unless you
//really want to
int midiFreqs[] = {8, 8, 9, 9, 10, 10, 11, 12, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24, 25, 27, 29, 30, 32, 34, 36, 38, 41, 43, 46, 48, 51, 55, 58, 61, 65, 69, 73, 77, 82, 87, 92, 97, 103, 110, 116, 123, 130, 138, 146, 155, 164, 174, 184, 195, 207, 220, 233, 246, 261, 277, 293, 311, 329, 349, 369, 391, 415, 440, 466, 493, 523, 554, 587, 622, 659, 698, 739, 783, 830, 880, 932, 987, 1046, 1108, 1174, 1244, 1318, 1396, 1479, 1567, 1661, 1760, 1864, 1975, 2093, 2217, 2349, 2489, 2637, 2793, 2959, 3135, 3322, 3520, 3729, 3951, 4186, 4434, 4698, 4978, 5274, 5587, 5919, 6271, 6644, 7040, 7458, 7902, 8372, 8869, 9397, 9956, 10548, 11175, 11839, 12543};
 
void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(oscillatorPin, OUTPUT);
  pinMode(buttonPin, INPUT);
   
  //These two things here are called 'event handlers'.  Their one
  //argument is another function.  They set it so that when
  //you get a noteOn or noteOff event, the function you use
  //as the argument immediately runs one time.
  usbMIDI.setHandleNoteOn(onReceiveNoteOnMessage); 
  usbMIDI.setHandleNoteOff(onReceiveNoteOffMessage); 
}
 
void loop() {
  //you need this happening every loop for the event handlers
  //to work, just trust me
  usbMIDI.read();
  //this is defined below and should be self explanatory
  doAudio();
  
}
 
void onReceiveNoteOnMessage(byte channel, byte note, byte velocity) {
  if(channel == midiChannel) {
    currentMidiNote = note;
    currentMidiVelocity = velocity;
  }
}
 
void onReceiveNoteOffMessage(byte channel, byte note, byte velocity) {
  if(channel == midiChannel) {
    currentMidiVelocity = 0;
  }
}
 
void doAudio() {
  //a noteOff message always has a velocity of zero
  if(currentMidiVelocity == 0) {              
    digitalWrite(ledPin, LOW);
  //otherwise its greater than 0 so its a noteOn, we play a note
  } else {
    digitalWrite(ledPin, HIGH);
    playToneFromMidiNote();
    
  }
}
 
void playToneFromMidiNote() {
  currentFrequency = getFreqFromMidiNote(currentMidiNote);
  playFrequency(currentFrequency);
}
 
void playFrequency(int freq) {
  digitalWrite(oscillatorPin, HIGH);
  delayMicroseconds(1000000 / freq / 2);
  digitalWrite(oscillatorPin, LOW);
  delayMicroseconds(1000000 / freq / 2);
  if(digitalRead(buttonPin) == HIGH) {
    potVal = analogRead(pot);
    digitalWrite(oscillatorPin, HIGH);
    delay(potVal / freq * 2);
    digitalWrite(oscillatorPin, LOW);
    delay(potVal / freq * 2); 
  }
}
int getFreqFromMidiNote(int theNote) {
  return midiFreqs[theNote];
}
```

Week 5
---

Part 1a

```
int ledPin = 13;
 
void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
}
 
void loop() {
  for(int i = 0; i < 10; i++) {
    Serial.println(i);
    digitalWrite(ledPin, HIGH);
    delay(250);
    digitalWrite(ledPin, LOW);
    delay(250);
  }
 
  delay(5000);
}

//The function "for(int i = 0; i < 10; i++)" is telling us how many times the LED blinks in a loop. The smaller number is subtracted from the bigger number to get the specified amount of blinks per loop. There is also a five second delay between loops.
```

Part 1b

```
int ledPin = 13; //creates an integer value called ledPin at a value of 13
int led2Pin = 14; //creates an integer value called led2Pin at a value of 14
 
void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT); //sets ledPin to OUTPUT
  pinMode(led2Pin, OUTPUT); //sets led2Pin to OUTPUT
}
 
void loop() {
  for(int i = 0; i < 10; i++) { //says the light will blink 10 times before the loop resets
    Serial.println(i);
    blinkLED(ledPin, 500); //ledpin will blink for .5 seconds
    blinkLED(led2Pin, i * 100); //led2Pin will blink for whatever i is set to multiplied by 100 milliseconds
  }
 
  delay(5000); //delays for 5 seconds before looping again
}
 
void blinkLED(int blinkPin, int blinkLength) { //Creates a function that is called blinkLED. It will accept integer values called blinkPin and blinkLength
  digitalWrite(blinkPin, HIGH); //turns blinkPin on
  delay(blinkLength); //sets the time that the blinkPin will be on
  digitalWrite(blinkPin, LOW); //turns blinkPin off
  delay(blinkLength); //sets the time that the blinkPin will be off
}
```

Part 2

```
int ledPin = 13;
int led2Pin = 14;
int led3Pin = 15;
int buttonPin = 12;
 
//an unsigned long is type of variable just like int,
//but it can hold much bigger numbers, which can
//be useful sometimes
unsigned long millisecondsSinceReset = 0;
 
void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  pinMode(led2Pin, OUTPUT);
  pinMode(led3Pin, OUTPUT);
  pinMode(buttonPin, INPUT);
}
 
void loop() { //creates a loop
 
  millisecondsSinceReset = millis(); //millisecondsSinceReset is set to equal millis which is equal to the number of milliseconds since you last reset your teensy
 
  if(millisecondsSinceReset < 3000) { //if it has been less than 3 seconds since the last reset
    digitalWrite(ledPin, HIGH); //ledPin will be HIGH
    digitalWrite(led2Pin, LOW); //led2Pin will be LOW
    digitalWrite(led3Pin, LOW); //led3Pin will be LOW
  } else if (millisecondsSinceReset < 5000) { //if it has been less that 5 seconds since the last reset but more than 3 seconds
    blinkLED(led2Pin, 150); //led2Pin will blink every .15 seconds
  } else if (millisecondsSinceReset < 10000) { //if it has been less that 10 seconds since the last reset but more than 5 seconds
    blinkLED(led3Pin, 100); //led3Pin will blink every .1 seconds
  } else { //anything after 10 seconds
    digitalWrite(ledPin, LOW); //ledPin will be LOW
    digitalWrite(led2Pin, LOW); //led2Pin will be LOW
    digitalWrite(led3Pin, HIGH); //led3Pin will be HIGH
  }
}
 
void blinkLED(int blinkPin, int blinkLength) {
  digitalWrite(blinkPin, HIGH);
  delay(blinkLength);
  digitalWrite(blinkPin, LOW);
  delay(blinkLength);
}
```

Part 3

```
int oscillatorPin = 14;
int ledPin = 13;
int buttonPin = 12;
 
unsigned long triggerTime = 0;
 
int middleCFrequency = 261;
int middleDFrequency = 294;
 
void setup() {
pinMode(oscillatorPin, OUTPUT);
pinMode(ledPin, OUTPUT);
pinMode(buttonPin, INPUT);
}
 
void loop() {
 
  if(digitalRead(buttonPin) == HIGH) {
 
    digitalWrite(ledPin, HIGH);
 
    triggerTime = millis();
    while(millis() < triggerTime + 1000) {
      playFrequency(middleCFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleDFrequency);
    }
 
    delay(200);
 
  } else {
    digitalWrite(ledPin, LOW);
  }
}
 
void playFrequency(int freq) {
  digitalWrite(oscillatorPin, HIGH);
  delayMicroseconds(1000000 / freq / 2);
  digitalWrite(oscillatorPin, LOW);
  delayMicroseconds(1000000 / freq / 2);
}
```

Part 4. This is my code that play the begging of "Ode to Joy". As you push the buttonPin it will send a signal to play through all the prescribed playFrequencies, pausing at specified times in order to give the right effects. <a href=https://www.youtube.com/watch?v=ENKacB-hghM&list=UU6CqOBUWgHrd4C1X4tnKVfQ >Here</a> is the link to the video of my code in action.

```
int oscillatorPin = 14;
int ledPin = 13;
int buttonPin = 12;
 
unsigned long triggerTime = 0;
 
int middleEFrequency = 329;
int middleFFrequency = 349;
int middleGFrequency = 392;
int middleDFrequency = 293;
int middleCFrequency = 261;
 
void setup() {
pinMode(oscillatorPin, OUTPUT);
pinMode(ledPin, OUTPUT);
pinMode(buttonPin, INPUT);
}
 
void loop() {
 
  if(digitalRead(buttonPin) == HIGH) {
 
    digitalWrite(ledPin, HIGH);
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleEFrequency);
    }
    
   delay(5);
    
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleEFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleFFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleGFrequency);
    }
 
    delay(5);
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleGFrequency);
    }
 
    delay(5);
 
     triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleFFrequency);
    }
    
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleEFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleDFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleCFrequency);
    }
 
    delay(5);
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleCFrequency);
    }
    
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleDFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleEFrequency);
    }
 
   delay(5);
 
    triggerTime = millis();
    while(millis() < triggerTime + 750) {
      playFrequency(middleEFrequency);
    }
 
    triggerTime = millis();
    while(millis() < triggerTime + 250) {
      playFrequency(middleDFrequency);
    }
 
    delay(5);
 
    triggerTime = millis();
    while(millis() < triggerTime + 500) {
      playFrequency(middleDFrequency);
    }
 
    delay(200);
 
  } else {
    digitalWrite(ledPin, LOW);
  }
}
 
void playFrequency(int freq) {
  digitalWrite(oscillatorPin, HIGH);
  delayMicroseconds(1000000 / freq / 2);
  digitalWrite(oscillatorPin, LOW);
  delayMicroseconds(1000000 / freq / 2);
}

```
Week 4
---

In this lab we used our first Lab's code as an oscillator. This made a very basic monophonic squarewave synth that can hit different notes. My breadboard could only fit five buttons and therefore could only play 5 programmable notes. 

In addition to programming different notes, we also used the "void playFrequency(int freq)" function in order to tidy up our code. This function allowed us to use one line of code instead of four when programming the frequency of each note being played. The "void playFrequency" function tells us that it is creating a fucntion called "playFrequency". The "int freq" argument says that this function will accept an outside value in the form of integer, called frequency.

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

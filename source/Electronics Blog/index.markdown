---
layout: page
title: "Electronics Blog"
date: 2014-09-08 11:37
comments: true
sharing: true
footer: true
---
Analog Final Project
---
My project is an interpretation of the stylophone. It is basically an eight key synthesizer triggered by a stylus creating a sound when it comes in contact with a metal plate. Each individual metal plate is set to play a certain note, from C4 up to C5. In other words, it plays an entire octave. There are two different ways in which the notes can be played. The first is as a straight tone. The second has a tremolo that adds a little bit of texture to the sound.

<a href=https://www.youtube.com/watch?v=b3lEFg9Umf8 > Here</a> is a video of my project.

<a href=https://drive.google.com/file/d/0B9QjEv0QrVUkT0NBbkFESmtHUjdpT010UmMydUdWRm44S1Uw/view?usp=sharing > Here</a> is an audio recording of my project.

I began by creating an oscillator. The schematic for an oscillator is as follows: 

{% img https://stevesanalogelectronicslab.files.wordpress.com/2015/03/op-amp-square-and-triangle-wave1.png %}

Each of the triangles in the schematic designate Operational Amplifiers. OP Amps are essentially voltage amplifying devices designed to be used with external feedback components between its output and input terminals. For the external feedback components, I used resistors and capacitors. By using the output frequency formula:

    Output Frequency = (1/(4*Rt*C))*(R2/R1)

I was able to calculate the proper resistance of each of the eight notes needed to create the synthesizer. My calculations are as follows:

    C 261Hz = 1/(4*R*.000001 farads)*(10) = 9578 Ohms
    D 293Hz = 1/(4*R*.000001 farads)*(10) = 8532 Ohms
    E 329Hz = 1/(4*R*.000001 farads)*(10) = 7598 Ohms
    F 343Hz = 1/(4*R*.000001 farads)*(10) = 7288 Ohms
    G 392Hz = 1/(4*R*.000001 farads)*(10) = 6377 Ohms
    A 440Hz = 1/(4*R*.000001 farads)*(10) = 5681 Ohms
    B 493Hz = 1/(4*R*.000001 farads)*(10) = 5070 Ohms
    C 523Hz = 1/(4*R*.000001 farads)*(10) = 4780 Ohms


And this is the portion of the schematic, covering my oscillator:

{% img http://i.imgur.com/Coj6gWT.png %}

The stylus can be seen in the large 8 pin box of this schematic. It essentially completes the connection when it touches any of the 8 metal plates. Once the connection is completed, a signal is sent though a Voltage Controlled Amplifier.

With a VCA, it is possible to take any input or output signal and input it into the VCA, and then use that signal to control the volume of another audio signal. My VCA used an extremely slow version of the original oscillator I posted above:

{% img https://stevesanalogelectronicslab.files.wordpress.com/2015/03/op-amp-square-and-triangle-wave1.png %}

In order to slow the oscillator down I had to increase R1 to 47 kOhms and R2 to 100 kOhms. This this slows the oscillation down to about 5 hz. When the signal is being received, it interacts with the normal speed oscillations and creates a tremolo (or frequency modulation) effect.

There is a switch alternating the VCA between receiving the slowed signal (aka creating a tremolo) and receiving no signal (aka groud or the normal signal from the original oscillator). This allows for two different sounds in the synthesizer. 
This is the schematic for just the VCA (top) and the Tremolo (bottom):

{% img http://i.imgur.com/klqS0cq.png %}

Both signals are run through the master output of the VCA, which in this case is another OP Amp.

<a href=https://www.circuitlab.com/circuit/4xzx9j/screenshot/1024x768/ > Here</a> is the complete schematic of my project.


Analog Lab 10
---

 <a href=https://www.circuitlab.com/circuit/86m57f/screenshot/1024x768/ > Here</a> is the schematic for the second part of my final lab. I am now 2/3 of the way to finishing the project. I added a voltage controlled amplifier to the oscillator, so that it now has a tremolo effect. For the remainder of my project I need to add the rest of the notes to the keyboard, as well as the stylus and contact pads. This should be a difficult task as I already have the calculations for my notes.

 <a href=https://www.youtube.com/watch?v=EFAR073jV4c > Here</a> is a video of my project in action thus far.
Analog Lab 9
---
Here is the first portion of my final lab. I started out with an oscillator similar to the one we originally made in class. Instead of a potentiometer I ran various resistors in stead to create a consistent note. Although the note being played is a C, it is significantly lower than I expected. I need to re-evaluate my calculations and make sure everything is correct.

Over the next few weeks I plan on adding the remaining 11 notes as well as the contact pad for each note to be played. I also plan on adding a VCA for added effect to the device.

<a href=https://www.circuitlab.com/circuit/x9sd6f/final-project-part-1/ > Here</a> is the schematic I have thus far, and <a href=https://www.youtube.com/watch?v=AGE-b2b5wRw > here</a> is a video of my project in action.

Analog Lab 8
---

For this lab we were turning sound into light.

We started by building a half-wave precision rectifier. This cicuit cuts the signal in half at the 0, only allowing a positive signal as opposed to a positive and negative signal. It allows very low level signals to be rectified with little error.

Next we made an <a href=https://www.youtube.com/watch?v=CQTgt1I_cuI >envelope follower.</a> This created a level that followed the waveform as we changed the volume of the signal. it allowed us to change the threshold at which the light is being turned on and off.

Finally we built a comparator circuit <a href=https://www.youtube.com/watch?v=Cbn_Oybo9S0 > Here</a> is a video of the circuit in action, the light responds to certain volumes produced by the audio signal.

If I wanted the light to respond to certain frequencies such as a bass drum, or high hat, I would put a lowpass or highpass filter (respectively), that only allowed certain frequencies to affect the LED.

Analog Lab 7
---

For this lab we were using sensors. I tried reading the resistance of my sensor with a VU meter and read it as 10 kOhms to 400 kOhms, but when I read the resistance when the sensor was int he circuit it read 10 Ohms to 100 kOhms.

<a href=https://www.youtube.com/watch?v=XCQpfnpX3ak >Here</a> is a video of my circuit working.

My final project is going to be a "pocket" synthesizer that plays 12 different notes. There will be 12 resistors that are attached to 12 different metal, or tinned, plates. There will also be a stylus attaced to the synth so that when the user presses the stylus to any of the 12 tinned plates, a note will be played through the output speaker. I am also planning on having 2 different potentiometers. One that controls the pitch of the notes, allowing different octaves to be played, and the other which will put a tremolo on the notes being played, if the user should want one.

{% img http://i.imgur.com/r3ZhEUK.jpg %}

Tentative Parts List:
1x Speaker
1x output jack
1x pen for stylus
12x resistors of different values
2x potentiometers
Wire
Solder (tin)
9V Battery
Battery Snap

Analog Lab 6
---
For this lab we made basic oscillators using OP Amps. 

<a href=https://www.circuitlab.com/circuit/fk2vuh/op-amps-ii-oscillators/ >Here</a> is the schematic for my OP Amp operating with two switches allowing the square wave and triangle wave to be played at selected times.

<a href=https://www.youtube.com/watch?v=Maf37Zd-jiY >Here</a> is a video of the oscillators working, both a square wave, and a triagle wave.

Analog Lab 5
---
For this lab I built a non-inverting OP Amp.

My calculations for the resistor are as follows:
    2 = (1+R/1000)
    1 = R/1000
    1000 = R

Below is a picture of the oscilloscope showing my OP Amp.

{% img http://i.imgur.com/4ETeuBv.jpg %}



My calculations for the potentiometer are as follows:
    11 = 1 + R/1000
    10 = R/1000
    100000 = R

<a href=https://www.youtube.com/watch?v=9XVxOeRa64M >Here</a> is a video of my OP Amp working with a potentiometer.


Analog Lab 4
---

For this lab we gathered the basic knowledge needed to read and use an oscilloscope. Below is a picture of how I setup my oscilloscope.

{% img http://i.imgur.com/Y7h8PGY.jpg %}

I used the Vert Mode switch to position the ground of each channel. The ground was moved using the position knobs above each volt/div knob. The volt/div appears to zoom in and out on the waveform, I determined that .2 was the best setting to get an overall idea of what the waveform looked like, and what it was doing.

In addition I had to set the volume on my computer. As the volume got louder the peaks of the waveform got higher as well. I found that mid volume worked best, it gave me peaks about where the picture above shows the peaks at.

Next we connected a resistor and capacitor (in that order). This created a highpass filter. As I jumped up an octave the RC cut the peak in half and wavelength. When I reversed the capacitor and resistor, it created a lowpass filter. As I jumped an octave the RC circuit the wavelength was halved.

Below is a picture of my planned final project design. I am planning on making a basic synthesizer. Each button will be connected to a specific resistor than, when pressed, will create a specific frequency. Each of the pots will control some sort of effect, I was thinking of maybe using an LFO and a filter, but that is subject to change

{% img http://i.imgur.com/RqgWvKC.jpg %}

Analog Lab 3
---

<a href=https://www.circuitlab.com/circuit/2v4nvn/lab-3-revisited// >Here</a> is the revisited schematic for lab 3. I had the wrong values for both my potentiometers and capcitors.


<a href=https://www.circuitlab.com/circuit/89u55b/highpass-and-lowpass-filter/ >Here</a> is my schematic for a highpass and lowpass filter run through a switch.

For my final project I could do a more complex lowpasss filter for an instrument. It could be plugged into a guitar or similar instrument and controlled by either a potentiometer or a pedal.

In terms of more complex projects, I could create my own analog synthesizer. Possibly a keyboard set up of buttons, each button being pressed creates a different pitches square wave (or any particular waveform).

When looking at modern analog synthesizers I would really like to know how a stylophone works. It is a pocket synthesizer that has a unique way of operating, by reading a stylus. I would love to take one apart, but I'm not sure I would be able to put it back together again!

Analog Lab 2
---
<a href=https://www.circuitlab.com/circuit/rj4s49/analog-electronics-lab-2-w-switch/ >This</a> is the schematic for my audio circuit with a switch.

<a href=https://www.circuitlab.com/circuit/5jcqc8/analog-electronics-lab-2-w-volume-knob/ >This</a> is the schematic for my audio circuit with a potentiometer set to volume.

<a href=https://www.circuitlab.com/circuit/8gyman/analog-electronics-lab-2-w-potentiometer/ >This</a> is the schematic for my audio circuit with a potentiometer set to pan between left and right.

Analog Lab 1
---
For this lab we were creating a circuit where two LEDs were controlled by a switch and potentiometer. <a href=https://www.youtube.com/watch?v=Bm4_MvlVYoM >Here</a> is the video of my circuit working, and <a href=https://www.circuitlab.com/circuit/3uzj6m/cicuit-1-for-electronics-lab/ >here</a> is the circuit diagram.

In addition to circuit construction we also looked into how multimeters work. These tools are essential to troubleshooting circuits. They allow us to see if each connection in a circuit is getting voltage or not, as well as the amount of voltage they are getting. In addition to voltage, many multimeters can also read current and resistance.

We also researched some of the past final projects that students before us have done. Here are some of my favorites: <a href=https://sarahbeilenson.wordpress.com/2014/05/09/final-report-tremolo-effect-pedal/ >this</a> tremolo effect pedal which gives a steady variation in amplitude to a guitar that was being played. There are two potentiometers on the device that changed the speed and depth of the tremolo. <a href=http://kenzoperronelectronicslab.blogspot.com/2014/05/final-project-report_8.html >This</a> piezoelectric audio trigger which allows the user to trigger bits of sound from either a square-wave oscillator or an audio input. If you tap or press the piezoelectric disk taped to the breadboard, the circuit will let out the oscillator the audio input. The final project that peaked my interest was <a href=https://matthewlauelectronicslab.wordpress.com/2014/05/08/final-lab-report/ >this</a> triangle wave synthesizer. This was a simple triangle wave synthesizer with two voices, a built in tremolo effect, and an active low-pass filter.

Analog Troubleshooting List
---
Here is where I will post all the troubleshooting I do in Analog Circuitry. Each lab that has troubleshooting will have it's own subtitle.



Final Digital Project Report
---
For my final project I created a MIDI contorller. Simply put this device has 16 buttons that send different MIDI notes to any electronic instrument that reads MIDI. I mainly plan on using it with my Digital Audio Workstation as a makeshift MIDI keyboard, making it easier to play melodies and record certian patterns. In addition to sending MIDI notes, it also has 4 potentiometers that can be mapped to various effects. I currently have the potentiometers set to a vinyl hiss, reverb, delay, and filter.

In terms of the code itself, it is fairly straightforward. I needed to include a new library to make sure everything works. This is due to the fact that I am using a new piece of equipment called an Adafruit Trellis. This is an open source backlight keypad driver that can easily be used by many different devices. In addition to the Trellis, I also have 4 potentiometers that can be programmed to control different effects. At the moment the effects I am using are a filter, a delay, some reverb, and vinyl noise. In the loop of the code I have the teensy constantly checking to see if a button has been pressed. If a button is pressed, its LED will light up and it will send a MIDI note to the Digital Audio Workstation (DAW) at full velocity. If a button is not pressed the LED will not be on, and send a signal to the DAW at a velocity of 0.

Each of the potentiometers is set to a certain channel and analog pin. Thus allowing each effect to be have seperate controls and values.

Below is my code, commented for better understanding:

```
#include <Wire.h> //include the library called Wire.h
#include <Adafruit_Trellis.h> //include the library called Adafruit_Trellis.h

#define LED     13 //define LED as a constant interval at 13

Adafruit_Trellis trellis; //create an instance of Adafruit_Trellis and call it trellis

const int CHANNEL = 1; //the interval CHANNEL will always equal 1

unsigned long prevReadTime = 0L; //create an unsigned long called prevReadTime
int autoFilter = 0; //create an interval called autoFilter
int reverb = 0; //create an interval called reverb
int delayPot = 0; //create an interval called delayPot
int vinyl = 0; //create an interval called vinyl

int autoFilterChannel = 1; //create an interval called autoFilterChannel at channel 1
int reverbChannel = 2; //create an interval called reverbChannel at channel 2
int delayPotChannel = 3; //create an interval called delayPotChannel at channel 3
int vinylChannel = 4; //create an interval called vinylChannel at channel 4

int autoFilterChangeVal = 0; //create an interval called autoFilterChangeVal
int reverbChangeVal = 0; //create an interval called reverbChangeVal
int delayPotChangeVal = 0; //create an interval called delayPotChangeVal
int vinylChangeVal = 0; //create an interval called called vinylChangeVal

int lastautoFilterChangeVal = 0; //create an interval called lastautoFilterChangeVal
int lastreverbChangeVal = 0; //create an interval called lastreverbChangeVal
int lastdelayPotChangeVal = 0; //create an interval called lastdelayPotChangeVal
int lastvinylChangeVal = 0; //create an interval called lastvinylChangeVal

int note[] = {
  60, 61, 62, 63,
  56, 57, 58, 59,
  52, 53, 54, 55,
  48, 49, 50, 51
}; //assigns the midi notes that will be played by the keypad

void setup() {
  pinMode(LED, OUTPUT); // LED is set to output
  trellis.begin(0x70); //begin using the trellis
  trellis.clear(); //clear the trellis
  trellis.writeDisplay(); //write to and display the trellis
 
 
}

void loop() {
  unsigned long t = millis(); //create an unsigned long called 't' and set it equal to millis
  if((t - prevReadTime) >= 20L) { //if t minus the prevReadTime is less than or equal to 20L (20 milliseconds)
    if(trellis.readSwitches()) { //look at the trellis readSwitches
      
      for(int i=0; i<16; i++) { //for every interval called 'i' where 'i' is less than 16, add 1
        if(trellis.justPressed(i)) { //if 'i' has just been pressed on trellis
          usbMIDI.sendNoteOn(note[i], 127, CHANNEL); //send the midi value of 'i' at a velocity of 127 to CHANNEL
         
          trellis.setLED(i); //turn on trellis LED at 'i'
        } else if(trellis.justReleased(i)) { //if the trellis button has just been released
          usbMIDI.sendNoteOff(note[i], 0, CHANNEL); //send the midi value of 'i' at a velocity of 0 to CHANNEL
          trellis.clrLED(i); //clear the trellis LED at 'i'
        }
      }
      trellis.writeDisplay(); //write to and display the trellis
    }
    lastvinylChangeVal = vinylChangeVal; //set lastvinylChangeVal equal to vinylChangeVal
    vinyl = analogRead(0); //vinyl's values are taken from analog out 0 (potentiometer 1)
    vinylChangeVal = vinyl/8; //vinylChangeVal is set to vinyl divided by 8
    if(vinylChangeVal != lastvinylChangeVal) { //i vinylChangeVal does not equal lastvinylChangeVal
      usbMIDI.sendControlChange(15, vinylChangeVal, vinylChannel); //send a control change at control 15 at a value equal to vinylChangeVal at the vinylChannel
    }    
    lastdelayPotChangeVal = delayPotChangeVal; //set lastdelayPotChangeVal equal to delayPotChangeVal
    delayPot = analogRead(1); //delayPot's values are taken from analog out 1 (potentiometer 2)
    delayPotChangeVal = delayPot/8; //delayPotChangeVal is set to delayPot divided by 8
    if(delayPotChangeVal != lastdelayPotChangeVal) { //if delayPotChangeVal does not equal lastdelayPotChangeVal
      usbMIDI.sendControlChange(14, delayPotChangeVal, delayPotChannel); //send a control change at control 14 at a value equal to delayPotChangeVal at the delayPotChannel
    }
    lastreverbChangeVal = reverbChangeVal; //set lastreverbChangeVal equal to reverbChangeVal
    reverb = analogRead(2); //reverb's values are taken from analog out 2 (potentiometer 3)
    reverbChangeVal = reverb/8; //reverbChangeVal is set to reverb divided by 8
    if(reverbChangeVal != lastreverbChangeVal) { //if reverbChangeCal does not equal lastreverbChangeVal
      usbMIDI.sendControlChange(13, reverbChangeVal, reverbChannel); //send a control change at control 13 at a value equal to reverbChangeVal at the reverbChannel
    }
    lastautoFilterChangeVal = autoFilterChangeVal; //set lastautoFilterChangeVal equal to autoFilterChangeVal
    autoFilter = analogRead(3); //autoFilter's values are taken from analog out 3 (potentiometer 4)
    autoFilterChangeVal = autoFilter/8; //autoFilterChangeVal is set to autoFilter divided by 8
    if(autoFilterChangeVal != lastautoFilterChangeVal) { //if autoFilterChangeVal does not equal lastautoFilterChangeVal
      usbMIDI.sendControlChange(12, autoFilterChangeVal, autoFilterChannel); //send a control change at control 12 at a value equal to autoFilterChangeVal at the autoFilterChannel
    }
    
    
    prevReadTime = t; //prevReadTime is set to 1
    
  }
  while(usbMIDI.read()); //so long as it is reading MIDI, the loop will continue
}
```

<a href=https://www.youtube.com/watch?v=RYuDbqb9Dz8 >Here</a> is a video of my project in action! (The hissing noise you hear during part of the video is intentional, it is one of the effects, the vinyl hiss.)

Digital Lab 11
---
I am currently waiting on certain parts for my final project to be delivered. I hope to have all the parts necessary byt the beginning of next week. I plan to review the features I want to include in my code, which we learned from previous labs. Sadly I don't have a video yet to show the capabilitites of my project, but I hope to have one soon. By the end of thanksgiving break I hope to have all the circuitry and assembling done with my project and focus solely on the coding itself. 

Digital Lab 10
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

Digital Lab 9
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


Digital Lab 8
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

Digital Lab 7
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

Digital Lab 6
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

Digital Lab 5
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
Digital Lab 4
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

Digital Lab 3
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

Digital Lab 2
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

Digital Lab 1
---

<a href=http://www.instructables.com/id/Arcade-Button-MIDI-Controller/?ALLSTEPS >These</a> are instructions for a MIDI controller built using an Arduino microcontroller.  This controller can send and receive MIDI messages to your PC, and allows you to control your software program such as Traktor. The white arcade buttons you see in the picture are the inputs and each button is mapped to a different sound/signal. When a button is pressed, it sends a signal to the software which is then sent to the listener.

<a href=http://www.instructables.com/id/LED-Dance-Room/?ALLSTEPS >This</a> is a guide to build an Audio Visualizer using an Arduino microcontroller.  This visualizer receives audio from the microphone jack of your computer, allowing it to accept it’s own sound fed back, or sound from any other audio playing device. The change in sound causes the lights to pulse and change.

<a href=http://www.instructables.com/id/Music-Party-Facebook-Connected-Arduino-Powered-/ >This</a> is an automatically shuffling music player run by an Arduino microcontroller. A RFID reader reads the unique ID of whatever device/card was placed near it. The signal is then sent to the Arduino microcontroller, which sends a signal to the music server. Once that process is completed the preferred music of the device/card owner is added to playlist to be shuffled.

<a href=http://www.instructables.com/id/Electronic-Music-Box-Powered-by-Arduino-sort-of/ >This</a> is the design for a music box powered by an Arduino microcontroller. The music is stored on a piece of paper and read through the device. As the paper passes through the device an infrared light reads the black and white marking on the paper and sends a signal to be played by the music box.

<a href=http://www.instructables.com/id/This-Is-Your-Brain-On-Music/step3/Beat-detection-music-visualization-Arduino-and-Pro/ >This</a> is a design for a musical beat detector controlled by an Arduino microcontroller. The designer uses processing to register the sound, which is then transmitted to the visualizer. By using processing, the designer doesn't have to worry about white noise. To get different colors, the designer assigned colors to different buckets. When a beat lands in a certain bucket, that color is displayed.

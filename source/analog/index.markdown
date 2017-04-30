---
layout: page
title: "Analog Electronics"
date: 2014-09-08 11:37
comments: true
sharing: true
footer: true
---
Analog Final Project
---
My project is an interpretation of the <a href=http://en.wikipedia.org/wiki/Stylophone > stylophone</a>. The project is basically an eight key synthesizer triggered by a stylus creating a sound when it comes in contact with a metal plate. Each individual metal plate is set to play a certain note, from C4 up to C5. In other words, it plays an entire octave. There are two different ways in which the notes can be played. The first is as a straight tone. The second has a tremolo that adds a little bit of texture to the sound.

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


# LiveJS : FrankenJS

* Hi, my name is Sam
* and my name is Tim

our story is split into 3 chapters and by the end you will know how to use the web to do an audio / visual live performance.

And now it's part 1: Sam

---

# Part 1: Sam

## Game Boy music

Let's talk about a passion of mine.

I use the Nintendo Game Boy to create music, which is commonly referred to as Chiptune.  

(*next slide (gig pic)*)

I've played shows with my music all over Europe and it sounds a little like this:

(*PLAY MUSIC*)
(*next slide*)

I've been doing this for about 8 years now, and just a couple of years ago I wanted to create visuals to go with my music and shows.

(*next slide*)

As there is no direct MIDI output from the software I use on Game Boy, I researched how to analyse audio using JavaScript in the browser.

## WebAudio analysing

The WebAudio API is an adaptable system for controlling, analysing and processing audio on the web.  

We start off with an **audio context**, and add from there.  
(**change**)

For basic usage, a source is needed and a destination.  
Sources can be either ```<audio>```,
(**change**)
an oscillator or a stream.  

(**change**)

The destination is usually your speakers, but can be any audio output your system supports.

In between the input and output we can add other nodes such as effects (reverb, biquad filter, panner, compressor), gain nodes and, what I needed for visualisation, analyser nodes.

(*ANALYSER NODE INFORMATION*)

You can do a lot with the Analyser node on its own but there comes a point where I needed a more refined value to work with.  

(*next slide*)

I use Meyda, an audio processing library.  

Meyda can return far more advanced audio analysis (*LIST OF MEYDA'S FEATURES*) and the two which are most useful to me are:

* (**change**) ZCR, the Zero Cross Rate
* (**change**) RMS, Root Mean Squared

ZCR is great for detecting high frequency percussive elements such as high hats and RMS is very good at detecting the kick drum in a song.

## modV origins

Now that I had a WebAudio figured out, I could combine the values from Meyda with drawing shapes using Canvas.  

(*change*)

I made a modular framework for mixing different visual outputs, called...

## modV

modV stands for Modular Visualisation. It is an Open Source audio visualisation environment written in JavaScript and runs in Google Chrome.

(**change**)

The program's development started 2 years ago and it is the result of my adventure into audio visualisation using JavaScript.

Before I show it to you, I'm going to go over the technologies used within modV to create the visualisations.

### Canvas

CanvasRenderingContext2D, or Canvas 2D for short, is used for drawing simple shapes and copying image data onto ```<canvas>```.

Incredibly, ```<canvas>``` counts as image data too, so we can draw Canvas back onto itself.  
If we stretch the image as well we can create the the age old effect of infinite video loops: the tunnel effect.

(*change slide*)

Usually in modV, I use Canvas2D to create source blocks of colour and lines that can be manipulated by the other modV Module types.

(*change slide*)

(*change slide*)

### WebGL

modV uses WebGL in two different ways.  

I've used THREE.js as modV's 3D engine.  

THREE.js is a very powerful 3D engine using WebGL. It's the most popular library for 3D in the browser for its ease of use and its broad set of features.

Any 3D models seen within modV will use THREE.js.


### GLSL

modV can also process anything drawn onto the screen as a WebGL texture and modify that using OpenGL Shader Language, GLSL for short. GLSL code runs on client's graphics processor.

This allows for incredible effects that would otherwise not be possible using Canvas2D.


## Modules: Putting all of this together

So, we've covered the visualisation technologies - but how can we put all of this together in an ***EASY TO USE*** API?

That's where the modular part of modV comes in.  

(*switch to modV*)

modV has a collection of three different types of Modules at the moment:

* Module2D - Canvas2D
* Module3D - THREE.js (WebGL)
* ModuleShader - GLSL (WebGL)

(*Show off Module Types in Demo 5 - 10 seconds 🎉*)

When combined, these Modules can create some stunning visuals.

(*DEMO TIME*)

(*switch to slides*)

Thank you.

Now it's Part 2: TIM!

---

# Part 2: Tim

## NERDDISCO

* My two biggest passions are music visualizations and experimenting with web technologies
* To combine both these passions into one project I started NERD DISCO more than two years ago
* It's using Web Audio and Canvas to create visualizations, but as Sam already talked about that in depth, I will focus on the hardware side of NERD DISCO.

## 1. MIDI

* Let's start with MIDI, which stands for **Musical Instrument Digital Interface**
* It's a standard that defines a data protocol and adapters
* And it's main purpose is to connect electronic instruments, computers and other MIDI devices with each other
* In the browser we have the **Web MIDI API**, which makes it possible to use any MIDI device over USB, like this **Novation Launch Control**
* We only need to **requestMIDIAccess**
* And listen to **MIDIMessageEvent**'s
* For example if I push a button on the **Launch Control** you will get a **MIDIMessageEvent**
* This means we can use any MIDI device to control software in the browser

## 2. LED

Another main part of NERD DISCO are LEDs and because I love to create prototypes, I build this LED curtain:

It consists of

* 8 strips with 30 LED per strip, the LEDs I'm using are called NeoPixel. The cool thing about them is that they can display any RGB color we want
* To manage the LED strips I'm using a microcontroller called FadeCandy and it was only build to control NeoPixels
* The FadeCandy is connected over USB to a Raspberry PI and the Raspberry PI is running a Node.js-app, which can send data to the FadeCandy over USB and creates a WebSocket-Server, so I can control the Raspberry PI over WIFI from my computer

### FadeCandy to LED

* And to create visualizations, it works like this:
* If we want to turn on the first LED to red, we send an array of 3-byte values to the FadeCandy
* In this case 255, 0, 0, which stands for red, green and blue
* If we want to turn on the second LED to green, we send another 3-byte value to the strip
* In this case 0, 255, 0
* This goes on and on from LED to LED; from strip to strip
* So it's just one big array of colors




## 3. DMX512

* The third thing that is part of NERD DISCO is DMX512
* It's commonly used for professional stage lightning, like you can see in this theatre: all the lights and lasers are controlled using DMX

* DMX stands for **Digitial Multiplex**
* The 512 stands for 512 channels

* A network of DMX devices is called a DMX Universe
* A DMX universe consists of a sender device (that sends all the data) and multiple devices that receive the data
* Each device has a unique address and a specific amount of channels

* My DMX512 universe consists of a USB DMX Interface, because I can't send DMX data directly from the browser (there is no API yet)
* And I can send data over USB to this USB DMX Interface
* I also have 2 PAR lights, which you can see on the left & on the right of this table
* Each of these lights have 3 channels (one for red, one for green and one for blue)
* And a bubble machine (which has two channels)

* And the data is expected like this:
* We create an Object

(*first PAR light*)
* The first device has the address of 1 and we want to turn it on in red, so we send 255, 0, 0 -> which is red

(*second PAR light*)
* The second device has an address of 4 and we want to turn it green, so we send 0, 255, 0 to it

(*bubble machine*)
* The bubble machine has an address of 16 and to turn it on, we have to send 255 for the motor on channel 16 and 255 for the fan on channel 17



**TIM:** And now it's part 3: Sam & Tim

---

# Part 3: Sam + Tim

**SAM:** A couple of months ago, Tim and I met through Live:JS: A collective of audio and visual artists. I asked Tim: Oh, wouldn't it be nice to combine our projects?

**TIM:** I said: YES, that is a good idea. Why don't we do this and meet each other for a Hack Weekend?

**SAM:** We added MIDI controller assignments in modV and grabbed the Canvas data to send it over WebSockets to Tim's project nerdV, which controls the NERDDISCO LED Curtain and DMX lighting!

## LiveJS

**TIM**: You will see and hear the result of our hack weekend in the following minutes. Sam will play one of his own songs live and I will control modV with my MIDI devices.

(*Load preset with Grab Canvas*)
(*Sam plays one of his songs*)
(*Tim VJs*)

---

# The End

**TIM:** You can find us online on livejs.network

**SAM:** If have any question just tweet @livejs_network

**TIM:** Thank you very much. This is the End.

**SAM:** GOOOOOOOOOD BYE!

✨

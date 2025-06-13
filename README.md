# RingTheBell
Demo - use YX5200 to create sounds for the strongman carnival ring the bell game.

**Table Of Contents**
* [Top](#ringthebell "Top")
* [The Idea](#the-idea "The Idea")
* [Schematic](#schematic "Schematic")
* [Code - Arduino](#code-\--arduino "Code - Arduino")
* [Code - ESP32](#code-\--esp32 "Code - ESP32")

## The Idea
[Top](#ringthebell "Top")<br>
This will create sounds for the strongman carnival ring the bell game.

There will be two LOW-active inputs (either from buttons or another processor):
- when the mallet hits to start the weight climbing
- when the weight rings the bell at the top

It is silent until it sees the mallet hit.<br>
Then it starts a rising sound of finite duration.
- If the "ring the bell" input happens while the rising sound is active, the sound is interrupted and the ring the bell sound starts. That sound continues until it finishes.
- If the rising sound finishes before the "ring the bell" sound, then silence until another input happens.

There are two ways to compile, which use different I/O pins:
- as an ESP32 (but not ESP32-S3 which uses different pins)
- as an Arduino Nano or Uno

## Schematic
[Top](#ringthebell "Top")<br>

## Code - Arduino
[Top](#ringthebell "Top")<br>

## Code - ESP32
[Top](#ringthebell "Top")<br>


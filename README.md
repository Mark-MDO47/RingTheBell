# RingTheBell
Demo - use YX5200 to create sounds for the strongman carnival ring the bell game.

**Table Of Contents**
* [Top](#ringthebell "Top")
* [The Idea](#the-idea "The Idea")
  * [ESP32 Over-The-Air Update - OTA](#esp32-over\-the\-air-update-\--ota "ESP32 Over-The-Air Update - OTA")
* [Schematic](#schematic "Schematic")
* [Code](#code "Code")
* [Sounds](#sounds "Sounds")

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

### ESP32 Over-The-Air Update - OTA
If compiled for an ESP32, the code will include the Over-The-Air Update (OTA) capability. This is implemented so it is always-on, not using the ESP-NOW commands from the following descriptions.
- https://github.com/Mark-MDO47/DuelWithBanjos/blob/master/code/DuelWithBanjos/OTA_story.md
- https://github.com/Mark-MDO47/UniRemote/blob/master/code/mdo_use_ota_webupdater/README.md

The Arduino Nano and Uno do not natively support this OTA capability.

## Schematic
[Top](#ringthebell "Top")<br>
This "wiring schematic" shows connections for both the Arduino Nano and an ESP32 development board.

Note that I did not show a switch/button for the ESP32 OTA control signal since the code is configured to automatically prepare that without input.

<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic.png" width="800" alt="Ring the Bell schematic">

## Code
[Top](#ringthebell "Top")<br>
The code is in the ./code/ area split into several directories. The *.ino file is in ./code/RingTheBell/RingTheBell.ino.

TBS - I will put a README in the code directory.

## Sounds
[Top](#ringthebell "Top")<br>
https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/sounds/README.md

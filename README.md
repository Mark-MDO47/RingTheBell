# RingTheBell
Demo - use YX5200 to create sounds for the strongman carnival ring the bell game.

**Table Of Contents**
* [Top](#ringthebell "Top")
* [The Idea](#the-idea "The Idea")
  * [ESP32 Over-The-Air Update - OTA](#esp32-over\-the\-air-update-\--ota "ESP32 Over-The-Air Update - OTA")
* [Schematic](#schematic "Schematic")
* [Code](#code "Code")
* [Sounds](#sounds "Sounds")
* [Parts List](#parts-list "Parts List")
  * [ESP32 version](#esp32-version "ESP32 version")
  * [Arduino NANO/UNO version](#arduino-nanouno-version "Arduino NANO/UNO version")

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
If compiled for an ESP32, the code will include the Over-The-Air Update (OTA) capability. This is implemented so it is always-on, not using the ESP-NOW commands from the following descriptions (which are from other projects).
- https://github.com/Mark-MDO47/DuelWithBanjos/blob/master/code/DuelWithBanjos/OTA_story.md
- https://github.com/Mark-MDO47/UniRemote/blob/master/code/mdo_use_ota_webupdater/README.md

The Arduino Nano and Uno do not natively support this OTA capability.

## Schematic
[Top](#ringthebell "Top")<br>
This "schematic wiring diagram" shows connections for both the Arduino Nano and an ESP32 development board.
- I sometimes call my schematics "schematic wiring diagrams" because I don't follow the rules of the standards organizations, although I reserve the right to just call them schematics.
  - I show all the connections as wires and show the pins of chips/modules all together and arranged the same as physical top view instead of separated/organized by function since I use my "schematic" to do the actual wiring of my project.
  - I tend to forget to hook up some of the power and ground connections if I use the standard schematic methods instead of showing the wire.

Notes
- I did not show a switch/button for the ESP32 OTA control signal since the code is configured to automatically prepare that without input.
- **TBR** I am using resistors to drop the voltage from YX5200 5V to ESP32 3.3V (to avoid damage to ESP32) but I am also testing to see if I can run reliably using the ESP32 3.3V serial TX without voltage translation.
  - I have experienced inconsistent behavior using the 3.3V output on WS2812B LEDs.
- The 1K resistor in the path to the YX5200 RX line prevents coupling of digital noise into the sound output.
- I did not include external power for these prototype designs; I assume they will be powered from the USB

<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic.png" width="800" alt="Ring the Bell schematic">

## Code
[Top](#ringthebell "Top")<br>
The code is in the ./code/ area split into several directories. The *.ino file is in ./code/RingTheBell/RingTheBell.ino.<br>
A directory of the code can be found here:
- https://github.com/Mark-MDO47/RingTheBell/tree/master/code

## Sounds
[Top](#ringthebell "Top")<br>
The sounds and a description of how to create/adjust sounds and how to copy them to the MicroSD card for the YX5200 can be found here:<br>
- https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/sounds/README.md

## Parts List
[Top](#ringthebell "Top")<br>

### ESP32 version
[Top](#ringthebell "Top")<br>

| Title | Descrip | URL | each |
| --- | --- | --- | --- |
| ESP32 | 1 @ ESP32 Devkit V1 ESP-WROOM-32 (or any ESP32 WiFi capable module except an ESP-32-S3) | https://www.amazon.com/Hosyond-ESP-WROOM-32-Development-Microcontroller-Compatible/dp/B0C7C2HQ7P/ref=sr_1_4 | $3.50 |
| YX5200 | 1 @ Sound Module with MicroSD (TF) card socket | https://www.amazon.com/Organizer-YX5200-DFPlayer-Supporting-Arduino/dp/B07XXYQBNS/ref=sr_1_1 | $2.00 |
| MicroSD card | 1 @ 32GByte or smaller MicroSD card formatted as FAT32 | TBS | TBS |
| speaker |  Metal Shell Round Internal Magnet Speaker 2W 8 Ohm approx 1 inch | https://www.amazon.com/dp/B0177ABRQ6 | $2.80 |
| resistors | 1 @ 1.0-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT1K00/1741314 | $0.10 |
| resistors | 2 @ 3.3-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT3K30/1741376 | $0.10 |
| resistors | 2 @ 6.65-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/RNF14FTD6K65/1682364 | $0.10 |
| **maybe TBR** SN74HCT125N | 1 @ Non-inverting 5.5V buffer 14-pin DIP | https://www.digikey.com/en/products/detail/texas-instruments/SN74HCT125N/376860 | $0.63 |

### Arduino NANO/UNO version
[Top](#ringthebell "Top")<br>

| Title | Descrip | URL | each |
| --- | --- | --- | --- |
| NANO | Arduino NANO or UNO or clone | TBS | TBS |
| YX5200 | 1 @ Sound Module with MicroSD (TF) card socket | https://www.amazon.com/Organizer-YX5200-DFPlayer-Supporting-Arduino/dp/B07XXYQBNS/ref=sr_1_1 | $2.00 |
| MicroSD card | 1 @ 32GByte or smaller MicroSD card formatted as FAT32 | TBS | TBS |
| speaker |  Metal Shell Round Internal Magnet Speaker 2W 8 Ohm approx 1 inch | https://www.amazon.com/dp/B0177ABRQ6 | $2.80 |
| resistors | 1 @ 1.0-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT1K00/1741314 | $0.10 |



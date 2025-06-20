# RingTheBell
Demo - use YX5200 to create sounds for the strongman carnival ring the bell game.

**Table Of Contents**
* [Top](#ringthebell "Top")
* [The Idea](#the-idea "The Idea")
  * [ESP32 Over-The-Air Update - OTA](#esp32-over\-the\-air-update-\--ota "ESP32 Over-The-Air Update - OTA")
* [Schematic](#schematic "Schematic")
  * [Nano/Uno - YX5200 PWR at 5V UART at 5V - Works Reliably](#nanouno-\--yx5200-pwr-at-5v-uart-at-5v-\--works-reliably "Nano/Uno - YX5200 PWR at 5V UART at 5V - Works Reliably")
  * [ESP32 - YX5200 PWR at 5V UART at 5V - Works Reliably](#esp32-\--yx5200-pwr-at-5v-uart-at-5v-\--works-reliably "ESP32 - YX5200 PWR at 5V UART at 5V - Works Reliably")
  * [ESP32 - YX5200 PWR at 5V UART at 3.3V - Not Reliable](#esp32-\--yx5200-pwr-at-5v-uart-at-33v-\--not-reliable "ESP32 - YX5200 PWR at 5V UART at 3.3V - Not Reliable")
  * [ESP32 - YX5200 PWR at 3.3V UART at 3.3V - Not Reliable](#esp32-\--yx5200-pwr-at-33v-uart-at-33v-\--not-reliable "ESP32 - YX5200 PWR at 3.3V UART at 3.3V - Not Reliable")
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
- as an ESP32 (but not ESP32-S3 which uses different pins; only exception I know)
- as an Arduino Nano or Uno

### ESP32 Over-The-Air Update - OTA
[Top](#ringthebell "Top")<br>
If compiled for an ESP32, the code will include the Over-The-Air Update (OTA) capability. By default, this is implemented so it is always-on, not requiring the ESP-NOW commands from the following descriptions (which are from other projects) nor the optional button push.
- https://github.com/Mark-MDO47/DuelWithBanjos/blob/master/code/DuelWithBanjos/OTA_story.md
- https://github.com/Mark-MDO47/UniRemote/blob/master/code/mdo_use_ota_webupdater/README.md

NOTE: The **Arduino Nano** and **Arduino Uno** do not natively support this OTA capability.

## Schematic
[Top](#ringthebell "Top")<br>
This "schematic wiring diagram" shows connections for both the Arduino Nano and an ESP32 development board.
- I sometimes call my schematics "schematic wiring diagrams" because I don't follow the rules of the standards organizations, although I reserve the right to just call them schematics.
  - I show all the connections as wires and show the pins of chips/modules all together and arranged the same as physical top view instead of separated/organized by function since I use my "schematic" to do the actual wiring of my project.
  - I tend to forget to hook up some of the power and ground connections if I use the standard schematic methods instead of showing the wire.

Notes
- I did not show a switch/button for the ESP32 OTA control signal since the code is configured to automatically prepare that without input
- I am using resistors to drop the voltage from YX5200 5V to ESP32 3.3V (to avoid damage to ESP32)
- The 1K resistor in the path to the YX5200 RX line prevents coupling of digital noise into the sound output
- I did not include external power for these prototype designs; I assume they will be powered from the USB
- I have a reliable version for Nano/Uno and for ESP32, plus two ESP32 variations that do now work reliably

### Nano/Uno - YX5200 PWR at 5V UART at 5V - Works Reliably
[Top](#ringthebell "Top")<br>
Here with a Nano/Uno and with the YX5200 using 5V for power and 5V on the UART interface - works reliably.<br>
<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic_Nano.png" width="500" alt="Ring the Bell Schematic with Nano - works reliably">

### ESP32 - YX5200 PWR at 5V UART at 5V - Works Reliably
[Top](#ringthebell "Top")<br>
Here with an ESP32 and with the YX5200 using 5V for power and 5V on the UART interface - works reliably.<br>
<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic_ESP32.png" width="700" alt="Ring the Bell Schematic with ESP32; YX5200 5V Power 5V UART - Works Reliably">

### ESP32 - YX5200 PWR at 5V UART at 3.3V - Not Reliable
[Top](#ringthebell "Top")<br>
Here with an ESP32 and with the YX5200 using 5V for power and 3.3V on the UART interface - not reliable. The YX5200 often ignores commands from the ESP32.<br>
<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic_ESP32_pwr5_uart3.3.png" width="500" alt="Ring the Bell Schematic with ESP32; YX5200 5V Power 3.3V UART - Not Reliable">

### ESP32 - YX5200 PWR at 3.3V UART at 3.3V - Not Reliable
[Top](#ringthebell "Top")<br>
Here with an ESP32 and with the YX5200 using 3.3V for power and 3.3V on the UART interface - not reliable. The YX5200 often ignores commands from the ESP32.<br>
<img src="https://github.com/Mark-MDO47/RingTheBell/blob/master/resources/images/RingTheBellSchematic_ESP32_pwr3.3_uart3.3.png" width="500" alt="Ring the Bell Schematic with ESP32; YX5200 3.3V Power 3.3V UART - Not Reliable">

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
| ESP32 | 1 @ ESP32 Devkit V1 ESP-WROOM-32 (or just about any ESP32 WiFi capable module **except an ESP-32-S3**) | https://www.amazon.com/Hosyond-ESP-WROOM-32-Development-Microcontroller-Compatible/dp/B0C7C2HQ7P/ref=sr_1_4 | $3.50 |
| YX5200 | 1 @ Sound Module with MicroSD (TF) card socket | https://www.amazon.com/Organizer-YX5200-DFPlayer-Supporting-Arduino/dp/B07XXYQBNS/ref=sr_1_1 | $2.00 |
| MicroSD card | 1 @ 32GByte or smaller MicroSD card formatted as FAT32; shown is 16GB example | https://www.amazon.com/dp/B08KSSX9PH | $3.75 |
| speaker |  Metal Shell Round Internal Magnet Speaker 2W 8 Ohm approx 1 inch | https://www.amazon.com/dp/B0177ABRQ6 | $2.80 |
| resistors | 1 @ 1.0-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT1K00/1741314 | $0.10 |
| resistors | 2 @ 3.3-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT3K30/1741376 | $0.10 |
| resistors | 2 @ 6.65-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/RNF14FTD6K65/1682364 | $0.10 |
| SN74HCT125N | 1 @ Non-inverting 5.5V buffer 14-pin DIP | https://www.digikey.com/en/products/detail/texas-instruments/SN74HCT125N/376860 | $0.63 |

### Arduino NANO/UNO version
[Top](#ringthebell "Top")<br>

| Title | Descrip | URL | each |
| --- | --- | --- | --- |
| NANO | Arduino NANO (or UNO) or clone | https://www.aliexpress.us/item/3256805941736729.html | $1.40 |
| YX5200 | 1 @ Sound Module with MicroSD (TF) card socket | https://www.amazon.com/Organizer-YX5200-DFPlayer-Supporting-Arduino/dp/B07XXYQBNS/ref=sr_1_1 | $2.00 |
| MicroSD card | 1 @ 32GByte or smaller MicroSD card formatted as FAT32; shown is 16GB example | https://www.amazon.com/dp/B08KSSX9PH | $3.75 |
| speaker |  Metal Shell Round Internal Magnet Speaker 2W 8 Ohm approx 1 inch | https://www.amazon.com/dp/B0177ABRQ6 | $2.80 |
| resistors | 1 @ 1.0-KOhm 1/4 watt through-hole resistors | https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT1K00/1741314 | $0.10 |



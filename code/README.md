# Code

**Table Of Contents**
* [Top](#code "Top")
* [Introduction](#introduction "Introduction")
* [RingTheBell](#ringthebell "RingTheBell")
* [lib_commonDFcode](#lib_commondfcode "lib_commonDFcode")
* [lib_DFPlayerMini](#lib_dfplayermini "lib_DFPlayerMini")
* [lib_mdo_use_ota](#lib_mdo_use_ota "lib_mdo_use_ota")

## Introduction
[Top](#code "Top")<br>
The code is divided into several subdirectories as shown below<br>
| Directory | Description |
| --- | --- |
| [code/RingTheBell](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/RingTheBell "RingTheBell - the *.ino containing #defines to define compile options") | The *.ino file for RingTheBell.<br>  Has #define statements to control choice of Arduino NANO/UNO or ESP32 target.<br>  **void DFsetup_pins_serial()** - defines pins and inits serial port for YX5200 DFPlayer. Includes code that handles SoftwareSerial for Arduino NANO/UNO and Hardware Serial for ESP32. |
| [code/lib_commonDFcode](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_commonDFcode "lib_commonDFcode") | lib_commonDFcode - This is where (almost all) the routines are that I wrote to handle calls to DFPlayerMini. Significant ones are<br>  **void DFsetup()** - call after calling **DFsetup_pins_serial**; will set baud rate to 9600 internally, choose SD card operation, and set default volume.<br>  **void  DFstartSound(uint16_t p_SoundNum, uint16_t p_Volume)** - starts requested *.wav file, interrupting any playing sound file. Also sets volume level.<br>  **uint8_t DFcheckSoundDone()** - returns TRUE if previous sound is complete. Takes into account that HW BUSY signal may not start until >=40 milliseconds after DFstartSound(). |
| [code/lib_DFPlayerMini](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_DFPlayerMini "lib_DFPlayerMini") | lib_DFPlayerMini - The source code for the DFRobot driver for the DFPlayer module.<br>  Available with Arduino IDE but I did a lot of debugging over the years inserting modified code here so I just always include it.<br>  Has its own separate license in file LICENSE_for_DFRobot_code.txt |
| [code/lib_mdo_use_ota](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_mdo_use_ota "lib_mdo_use_ota") | lib_mdo_use_ota - My ESP32 Over-The-Air Update (OTA) code to make it easy to use OTA.<br>  Originally from https://github.com/Mark-MDO47/UniRemote/tree/master/code/mdo_use_ota_webupdater |


## RingTheBell
[Top](#code "Top")<br>

### ESP32 Over-The-Air Update - OTA
[Top](#code "Top")<br>
If compiled for an ESP32, the code will include the Over-The-Air Update (OTA) capability. By default, this is implemented so it is always-on, not requiring the ESP-NOW commands from the following descriptions (which are from other projects) nor the optional button push.
- https://github.com/Mark-MDO47/DuelWithBanjos/blob/master/code/DuelWithBanjos/OTA_story.md
- https://github.com/Mark-MDO47/UniRemote/blob/master/code/mdo_use_ota_webupdater/README.md

ESP32 OTA compilation is controlled by the following **#define** statements in **RingTheBell.ino**
```C
#define MDO_USE_OTA  1 // zero to not use, non-zero to use OTA ESP32 Over-The-Air software updates
#define FORCE_OTA_ON_IF 1 // ESP32: non-zero to force OTA to be on always without needing the pin ONLY if MDO_USE_OTA is also on
```

If you want to compile for ESP32 with OTA enabled you need to create a file **gitignore_wifi_key.h** with the following definitions (I suggest using the ".gitignore" file so this does not accidentally show up in your public repository; see below after the #define statements).
```C
#define WIFI_PWD "password for your local wifi"
#define WIFI_SSID "SSID for your local WiFi"
#define WIFI_OTA_WEB_USR "username to be able to do OTA"
#define WIFI_OTA_WEB_PWD "password to be able to do OTA"
```

You could optionally add this line at the end of your **.gitignore** file to prevent any file or directory starting with gitignore from being saved to the repository. Can save some embarassment.
```
gitignore*
```

NOTE: The **Arduino Nano** and **Arduino Uno** do not natively support this OTA capability.

## lib_commonDFcode
[Top](#code "Top")<br>

## lib_DFPlayerMini
[Top](#code "Top")<br>

## lib_mdo_use_ota
[Top](#code "Top")<br>
This code is an attempt to make the ESP32 Over-The-Air Update (OTA) capability easy to use. It comes from my UniRemote project. Details can be found here:
- https://github.com/Mark-MDO47/UniRemote/tree/master/code/mdo_use_ota_webupdater

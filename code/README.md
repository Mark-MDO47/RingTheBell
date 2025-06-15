# Code

**Table Of Contents**

## Introduction
The code is divided into several subdirectories as shown below
| Directory | Description |
| --- | --- |
| [code/RingTheBell](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/RingTheBell "RingTheBell - the *.ino containing #defines to define compile options") | The *.ino file for RingTheBell.<br>  Has #define statements to control choice of Arduino NANO/UNO or ESP32 target.<br>  **void DFsetup_pins_serial()** - defines pins and inits serial port. Includes code that handles SoftwareSerial for Arduino NANO/UNO and Hardware Serial for ESP32. |
| [code/lib_commonDFcode](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_commonDFcode "lib_commonDFcode") | lib_commonDFcode - This is where (almost all) the routines are that I wrote to handle calls to DFPlayerMini. Significant ones are<br>  **void DFsetup()** - call after pins are defined and serial port init'ed; will set baud rate to 9600 internally, choose SD card operation, and set default volume.<br>  **void  DFstartSound(uint16_t p_SoundNum, uint16_t p_Volume)** - starts requested *.wav file, interrupting any playing sound file. Also sets volume level.<br>  **uint8_t DFcheckSoundDone()** - returns TRUE if previous sound is complete. Takes into account that HW BUSY signal may not start until >=40 milliseconds after DFstartSound(). |
| [code/lib_DFPlayerMini](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_DFPlayerMini "lib_DFPlayerMini") | lib_DFPlayerMini - The source code for the DFRobot driver for the DFPlayer module.<br>  Available with Arduino IDE but I did a lot of debugging over the years inserting modified code here so I just always include it.<br>  Has its own separate license in file LICENSE_for_DFRobot_code.txt |
| [code/lib_mdo_use_ota](https://github.com/Mark-MDO47/RingTheBell/tree/master/code/lib_mdo_use_ota "lib_mdo_use_ota") | lib_mdo_use_ota - My ESP32 Over-The-Air Update (OTA) code to make it easy to use OTA.<br>  Originally from https://github.com/Mark-MDO47/UniRemote/tree/master/code/mdo_use_ota_webupdater |


## RingTheBell

## lib_commonDFcode

## lib_DFPlayerMini

## lib_mdo_use_ota

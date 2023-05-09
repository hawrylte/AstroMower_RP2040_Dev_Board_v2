# AstroMower RP2040 Dev Board v2
## About
RP2040 Development Board to explore programming capability of Raspberry Pi [RP2040](https://www.raspberrypi.com/products/rp2040/) MCU for use in future projects.

## Hardware
  * 2 Layer PCB with parts populated on both sides

  * Spacing of pin headers is 0.9" to use on standard breadboard.

  * PCB Overall Dimensions 1.05" W X 1.95" L

  * USB-C Interface

  * Resistor and Capacitor sizes are 0603 and 0805 with hand solder footprints

  * Incorporates Neopixel addressable LED

  * 8 MB QSPI Flash

  * All parts ordered through Digi-Key

  * Developed in [KiCad 7.0](https://www.kicad.org/)

  * DRC for Manufacture through [OSHPARK](https://oshpark.com/)

## Software
### ***SOFTWARE UNDER DEVELOPMENT***
### MicroPython
MicroPython firmware for board can be downloaded directly or built from source.

***Instructions for building from source on Debian based system***

Building from source requires MicroPython source. Installation of this mirrors instructions found in Raspberry Pi [Raspberry Pi Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

Create *pico* directory
```
mkdir pico
cd pico
```
Then clone the *micropython* git repository
```
git clone https://github.com/micropython/micropython.git --branch master
```
Fetch additional submodules required for a RP2 MCU board
```
cd micropython
make -C port/rp2 submodules
```
To build *micropython* additional tools are required
```
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essentials libstdc++-arm-none-eabi-newlib
```
Bootstrap a special tool for MicroPython builds
```
make -C mpy-cross
```
***Load Board Specific Files for AstroMower Board***

Download *AstroMower RP2040 Dev Board v2* git repositiry
```
cd ..
git clone https://github.com/hawrylte/AstroMower_RP2040_Dev_Board_v2.git
```
Move specific board files to proper locations in *MicroPython* source files
```
cp -r AstroMower_RP2040_Dev_Board_v2/src/ASTROMOWER_RP2040_DEV_BOARD_V2 micropython/ports/rp2/boards/ASTROMOWER_RP2040_DEV_BOARD_V2
cp -r AstroMower_RP2040_Dev_Board_v2/src/astromower_rp2040_dev_board_v2.h micropython/lib/pico-sdk/src/boards/include/boards/astromower_rp2040_dev_board_v2.h
```
Build the port we need for RP2040 and specify our particular board to be built
```
cd micropython/ports/rp2
make BOARD=ASTROMOWER_RP2040_DEV_BOARD_V2
```
Copy UF2 Firmware from *MicroPython* build directory to *pico* directory
```
cd ../../..
cp micropython/ports/rp2/build-ASTROMOWER_RP2040_DEV_BOARD_V2/firmware.uf2 AstroMower_RP2040_Dev_Board_MicroPython_firmware.uf2
```
### C/C++


***Instructions for setting up PICO-SDK from source on Debian based system***

Setting up the *pico-sdk* mirrors instructions found in Raspberry Pi [Gettting Stated with Raspberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

Create *pico* directory
```
mkdir pico
cd pico
```
Then clone the *pico-sdk* and the *pico-examples* git repositories
```
git clone http://github.com/raspberrypi/pico-sdk.git --branch master
cd pico-sdk
git submodule update --init
cd ..
git clone http://github.com/raspberrypi/pico-examples.git --branch master
```
To build *pico-examples* additional tools are required
```
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essentials libstdc++-arm-none-eabi-newlib
```
Download *AstroMower RP2040 Dev Board v2* git repositiry
```
git clone https://github.com/hawrylte/AstroMower_RP2040_Dev_Board_v2.git
```
Move specific board files to proper locations in *MicroPython* source files
```
cp -r AstroMower_RP2040_Dev_Board_v2/src/astromower_rp2040_dev_board_v2.h pico-sdk/src/boards/include/boards/astromower_rp2040_dev_board_v2.h
```
***Instructions for building Blink example from PICO-EXAMPLES from source on Debian based system***
***AstroMower Dev Board v2 does not have a discrete LED for Blink to run, but this shows the process of building a C/C++ program for the AstroMower Dev Board v2***
Change to *pico-examples* directory and make *build* directory.
```
cd pico-examples
mkdir build
cd buid
```
Set *PICO-SDK-PATH*
```
export PICO-SDK-PATH=../../pico-sdk
```
Prepare cmke build directory and identify board to build program for.
```
cmake .. -DPICO_BOARD=astromower_rp2040_dev_board_v2
cd blink
make -j4
```
*blink.elf* is used by the debugger
*blink.uf2* is the program and can be dragged onto the RP2040 USB Mass Storage Device


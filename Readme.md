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

Building from source required PICO-SDK source and MicroPython source. Installation of these mirrors instructions found in Raspberry Pi [Gettting Stated with Raspberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) and [Raspberry Pi Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

Create *pico* directory
```
mkdir pico
cd pico
```
Then clone the *pico-sdk* and *pico-examples* git reposiories
```
git clone https://github.com/raspberrypi/pico-sdk.git --branch master
cd pico-sdk
git submodule update --init
cd ..
git clone https://github.com/raspberrypi/pico-examples.git --branch master
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
To build the *pico-examples* and *micropython* additional tools are required
```
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essentials libstdc++-arm-none-eabi-newlib
```
Bootstrap a special tool for MicroPython builds
```
make -C mpy-cross
```
***Load Board Specific Files for AstroMower Board***

Build the port we need for RP2040 and specify our particular board to be built
```
cd ports/rp2
make BOARD=ASTROMOWER_RP2040_DEV_BOARD_V2
```


## License
This hardware is licensed under the CERN Open Hardware License Version 2.0, Strongly Reciprocal Variant (CERN-OHL-S). See license.txt for additional information.


---
title: Beginning LPC1114FN28 with Arch Board
date: 2014/5/11
tags:
- mbed
- LPC1114
- CMSIS-DAP
---

It's cool that LPC1114FN28 based on ARM Cortex-M0 uses DIP package. We enjoy playing LPC1114 with a breadboard, wires, LEDs and etc. Programming LPC1114 is quite easy with an Arch board as a CMSIS DAP interface. To download a new binary into LPC1114 is just to drag-n-drop the binary file into "MBED" drive.

![](http://xiongyihui.github.io/Arch/images/Arch&LPC1114.jpg)


### Setup Hardware
Use Arch board as an mbed interface and connect Arch with LPC1114 through SWD interface or UART interface.

 Arch board   | LPC1114 
------------- | -------------
 P0_11 (A0)   | nRESET
 P0_12 (A1)   | SWCLK
 P0_13 (A2)   | SWDIO
 P0_18 (D0)   | RXD
 P0_19 (D1)   | TXD

### Turn Arch into mbed Interface
[The Arch board](https://mbed.org/users/seeed/notebook/Arch_V1_1/) is an mbed enabled development board for rapid prototyping. It can also be used as a CMSIS DAP interface(SWD/JTAG debug adapter, USB to UART bridge). We just need a specific firmware.

1. Download [mbed interface firmware for Arch board](https://github.com/xiongyihui/CMSIS-DAP/raw/lpc11u24/interface/mdk/lpc11u24/lpc11u24_lpc1114_if_mbed.bin).
2. Connect Arch with PC, long press Arch's button and replace firmware.bin with the new firmware in "CRP DISABLD" drive.
3. Quick press the button. "MBED" drive will pop up.
4. Install [the mbed interface driver](http://mbed.org/handbook/Windows-serial-configuration) to enable USB to UART function

### Develop
1. In "MBED" drive, there is a "MBED.HTM" file which will lead to mbed.org.
2. Add LPC1114FN28 to mbed compiler.
3. On mbed compiler, it's easy to write code, import libraries and share programs.
4. Compile and download a binary into "MBED" drive. The program will run!

![](https://mbed.org/media/uploads/screamer/compiler-overview.png)


### Resources
1. [CMSIS DAP interface](https://mbed.org/handbook/CMSIS-DAP)
2. [Getting started with mbed LPC1114](https://mbed.org/users/ytsuboi/notebook/getting-started-with-mbed-lpc1114/)

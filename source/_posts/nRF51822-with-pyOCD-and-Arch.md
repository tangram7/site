---
title: nRF51822 with pyOCD and Arch Board
date: 2014/3/31
tags: 
- mbed
- nRF51822
- CMSIS-DAP
---

I'm quite excited that Bluetooth Low Energy (nRF51822) is comming to mbed. So I'm exploring what we can do with BLE (nRF51822). Preparing tools to get started with new things is always the beginning.

Here we use [CMSIS-DAP](https://github.com/mbedmicro/CMSIS-DAP) and [pyOCD](https://github.com/mbedmicro/pyOCD). [CMSIS-DAP](https://github.com/mbedmicro/CMSIS-DAP) is the software running on mbed interface to provide drag-n-drop, USB2UART communication and SWD debug. pyOCD is an Open Source python library or programming and debugging ARM Cortex-M microcontrollers using CMSIS-DAP.

First, use [Arch](http://mbed.org/platforms/Seeeduino-Arch/) as an mbed interface to run [CMSIS-DAP](https://github.com/mbedmicro/CMSIS-DAP). 

1. Download [mbed interface firmware for Arch](https://github.com/xiongyihui/CMSIS-DAP/raw/lpc11u24/interface/mdk/lpc11u24/lpc11u24_nrf51822_if_mbed.bin).
2. Connect Arch with PC, long press Arch's button and replace firmware.bin with the new firmware in "CRP DISABLD" drive on windows. use `dd if=lpc11u24_nrf51822_if_mbed.bin of={path-to}/firmware.bin conv=notrunc` on [Linux/Mac](http://mbed.org/users/seeed/notebook/programming-seeeduino-arch/)
3. Quick press the button. "MBED" drive will pop up.
4. Install the [mbed interface driver](http://mbed.org/handbook/Windows-serial-configuration) for windows to enable USB2UART function

![CMSIS-DAP debug adapter](http://xiongyihui.github.io/assets/images/debug_adapter.png)

Second, setup pyOCD for nRF51822. We need pyOCD, pyUSB(Linux) or pyWinUSB(Windows) and [flash_nrf51822.py](https://github.com/xiongyihui/pyOCD/raw/master/util/flash_nrf51822.py)

On Ubuntu

```
sudo apt-get install python-setuptools
sudo easy_install pyusb
sudo easy_install pyocd
wget https://github.com/xiongyihui/pyOCD/raw/master/util/flash_nrf51822.py
```

On windows, install pyWinUSB instread of pyUSB.


Third, flash softdevice hex file or application binary file to nRF51822.

The softdevice hex file include two parts --- Code Region 0(CR0) and User Information Configuration Registers(UICR). Here we use arm-none-eabi-objcopy to divide the hex file into two binary files for CR0 and UICR. It's done in flash_nrf51822.py, so we just need to keep arm-none-eabi-objcop in the PATH variable. 

To flash softdevice hex, just run
```
sudo python flash_nrf51822.py -s softdevice.hex
```

To flash an application binary
```
sudo python flash_nrf51822.py -a {application.bin}
```





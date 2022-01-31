# wch-ch32v307-makefile

## Overview

This repository contains a blinky project for the [WCH CH32V307V-EVT-R1 development board](https://github.com/openwch/ch32v307) based on the CH32V307 RISC-V microcontroller. 
This repository is based on the [stm32-makefile repository](https://github.com/bbrown1867/stm32-makefile), created for developing simple Makefile based projects for microcontrollers.

The project uses:

* GNU Make (Build System) 
* [Mounriver Studio Toolchain Bundle](http://file.mounriver.com/tools/MRS_Toolchain_Linux_x64_V1.30.tar.xz)
  * GCC RISC-V Compiler and Debugger (riscv-none-embed-)
  * OpenOCD-WCH (Debug)
  
## User Guide

### Setup

* Install the toolchain bundle downloaded from the Mounriver website. Edit Makefile to change path variables `TOOLCHAIN_ROOT` and `OPENOCD_ROOT` to the gcc toolchain and openocd bin directory. Rename directories to avoid spaces in path string. 
* Add the following lines to `/etc/udev/rules.d/60-openocd.rules` or similar. Run `sudo udevadm control --reload` and replug device to USB.
 
            SUBSYSTEM=="usb", ATTR{idVendor}="1a86", ATTR{idProduct}=="8010", GROUP="plugdev"
    
* Add the following line to `~/.gdbinit`, so as to enable auto gdb initialization. Modify `<path>` to point to current directory.

            add-auto-load-safe-path <path>/wch-ch32v307-makefile/.gdbinit
    
* Connect USB-C Cable to P9. Insert Jumper wire between PA0 and LED1 headers.
    
### Build and Debug

* Simply run `make` to build the project.
* In another terminal, start the GDB server by running `make gdb-server_openocd`.  GDB Server probably has to be restarted after every code download step, otherwise seems to hang. 
* Run `make gdb-client` to download the code and start debugging.
* Optionally, open a serial terminal to view the `printf` function calls.
  * For example, run `pyserial`: `python -m serial - 115200` and then select the port labeled "WCH-Link".

<img src="https://user-images.githubusercontent.com/192318/151754584-6fd61b7c-d893-481f-911f-1fce58c17661.png" width=800 height=300>
<img src="https://user-images.githubusercontent.com/192318/151754587-f8825640-0322-4ca8-8d48-71745b1fd9a1.png" width=700 height=500>

     


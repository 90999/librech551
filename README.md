LibreCH551
----------

An __open-source__ command line flasher program and SDK library for WCH(Nanjing QinHeng Corp.)'s CH55x family.
[Our Wiki contains a lot of useful tips, it's worth to check out!](../../wiki/Home)

The CH55x is a series of 8051 microcontroller with dedicated USB peripheral. CH553/CH554 can be programmed as a USB host.
The cheapest one, CH551 only costs 1.5 CNY in retail. It is the ultimate and ideal solution for many low-end USB applications.

Up to now, we have tested out CH551 and CH554, all functions work fine except option byte.

If someone want to help me, please __start__, __fork__ and support more chips, Thanks!


TODO
------------
Implement UART programming function for CH554 working on USB Host mode (It is very simple to realize: just add serial port interface to the program and 0x619e, accumulate checksum in packet tail).

Implement new CH55x ISP protocol (bootloader version > 2.30), now we have no chip shipped with new bootloader: WCH's FAE said that they will send chips with new bootloader after Apr.2018.

Contributions are always welcome.

Command Line Parameters
------------
* __-f \<filename\>__ Erase the code flash and download binary codes to CH55x, note that this tool only accepts `.bin` files, `.hex` files will not be accepted.
The Eclipse SDCC environment with the setup [described in our wiki](../../wiki/Setup-SDCC-developing-environment-with-Eclipse) automatically generates `.bin` file. To convert a hex file to bin file, on Linux, use `objdump`, on Windows, use `hex2bin.exe` in [`win_tools.zip`](../../wiki/win_tools.zip).
* __-g__ Execute the user program after downloading
* __-e__ Erase chip only
* __-D \<filename\>__ Read data flash to a file
* __-d \<filename\>__ Write the content of a file to data flash

For Linux Users
----------

* Build: Type `make` in `usbisp` directory.
* Install:Type `make install` in `usbisp` directory, you can also pass DESTDIR to the script to set installation path. 
* Linux does not require a specific driver for this program.

For Windows Users
----------
* The Tool pack for Windows is avaliable [here](../../wiki/win_tools.zip).
* The wiki page "[Setup SDCC developing environment with Eclipse](../../wiki/Setup-SDCC-developing-environment-with-Eclipse)" demonstrates how to setup an IDE for better code editing.
* On Windows, CH554 ISP mode requires a libusb driver implementation to enable direct device access for librech551.

__Driver Installation__

1. Connect your CH55x to one of USB ports on your PC, make sure the MCU enters ISP mode.
2. Launch zadig (included in [`win_tools.zip`](../../wiki/win_tools.zip)), open `Options` menu and click `List All Devices`, 
you should be able to find your CH55x (Usually names `USB Module`), optionally you can change its name by check the `Edit` box. 
3. Double check that the USB ID is correct, USB ID is VID plus PID, for CH554, the USB ID is `4348 55E0`.
4. Select `libusb-win32` and click `Install Driver`, quit Zadig after driver installation.
* Note: due to unknown reason, sometimes the `libusbK` driver won't work on some machine with very new USB 3.1 controller. 
If your PC can not recognize the USB ISP device, try `winusb` or `libusb-win32` instead.

__Build Executables__
* Generate EXE file for Microsoft Windows requires __Microsoft Visual Studio 2017__ and __Windows Kits 10.0.15063.0 or above__.
If your system does not meet the stated requirement, go to Microsoft's website and download the installer for __Microsoft Visual Studio 2017 Community Version__.
* It is possible to compile the source with legacy Visual Studio although it is not officially supported.
1. Download the entire repository and unzip to anywhere you like
2. Navigate to `msvc` folder and create a folder called `libusb` under `msvc` directory
3. Go to <https://github.com/libusb/libusb/releases> to get the latest __stable__ binary snapshots of libusb(e.g. [libusb v1.0.21](https://github.com/libusb/libusb/releases/tag/v1.0.21)), download the file with extension `7z` or `tar.bz`, then unzip it to `msvc\libusb`. Now your `msvc\libusb` should contain at least these folders : `MS32`, `MS64` and `include`
4. Launch `msvc\librech551.sln` and choose your targeting platform (e.g. Release x64), then start compiling.

License
----------

GPLv3

Author(s)
----------

[Zhiyuan Wan](https://github.com/rgwan) <h@iloli.bid>

[Rikka0w0](https://github.com/rikka0w0)

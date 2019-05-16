# About
Product based repository that includes information, links and files to get you started 
# Bluetera Platform [<img align="right" img src="images/IOTERA-By-TENSOR-1_w100.png" alt="Logo"/>](https://israeli.achler.org/lotera/) 
Bluetera is an open source IoT platform for the development of smart and connected products. Bluetera platform is comprised of three main elements that are the building blocks of most IoT systems:
* Tiny hardware-based sensor hub to collect and analyze data; 
* wireless communication to link between the digital and physical side;
* SDK for major operating systems to build the software.

This walkthrough provides a high-level guide for using the Bluetera platform. The repositories, referenced below, provide the necessary code, documentation and examples to develop your own projects.


This walkthrough provides a high level guide for using the bluetera platform. dedicated repositories, refferenced below, provide the necessary documentation to develope your own projects.

<a name="up"></a>
# Table of Contents
1. [References](#references) to Bluetera platform repositories.
2. [System](#system) overview.
   1. [Hardware](#hw)
   2. [Firmware](#fw)
   3. [Software](#sw)
3. System [Guides](#guides).
   1. Windows BLE [driver](#win_ble) installation
   2. Firmware [update / debug](#fw_dbg)
   3. Firmware Over-the-air [update](#fw_oau)
   4. Windows [demo](#win_demo)
4. [Contributing](#cont).
5. [License](#license).
<a name="references"></a>

# References [^](#up)
Firmware [repository](https://bitbucket.org/tensor-tech/bluetera/src/master/firmware/).  
Windows SDK repository.  
Android SDK [repository](https://bitbucket.org/tensor-tech/bluetera_sdk/src/master/). 
<a name="system"></a>
# System Overview [^](#up) 
The Blutera platform includes the following major components 
* Bluetera module 
* Bluetera FW
* Blutera SDK 
* BLE CSR 4.0 dongle (for widows and Linux)
  
 ![Blutera Platfor](images/bluetera_platform.jpg)
 
 <a name="hw"></a>
 ## Hardware  module [^](#up)
 The Bluetera hardware module is a tiny sensor hub based on an Arm microcontroller, Inertial Motion Unit, Power Management Unit and a peripheral Extension Unit.

 The module includes the following features. 
   * Tiny Module (26mm diameter)
   * Nordic nrf52832/40 based module with ARM M4F Processor. 
   * Invensense ICM-20648/9 6-axis IMU (gyro and accelerometer)  
   * Wireless communication : BLE 4.0/5.0/Thread
   * Power management unit with battery chargering capabilities 
   * Litium-Ion 50mAh rechargable battery 
   * Pheripheral extensions via digital, Analog, I2C, SPI, UART, PWM etc support 
   * Schematics for 3D printed casings
  
<a name="fw"></a>
## Firmware [^](#up)
The Bluetera firmware is an open source project with code and libraries that can be used as a staging point for complicated products. Further research and development is done  using the standard Nordic IDE.
  
The firmware includes the following features.
* Events scheduler
* BLE stack and APIs
* IMU support - 50hz quaternion and acceleration data, 
* Dedicated IMU service.
* Protobuf for command and control functionality (TBR)
* SPI & I2C (TBR)
* SD card at 1khz support (TBR)
* Online and Offline modes of operation (TBR)
* Gyro & Acceleration at 1khz (TBR)
* Triggered and Programable Sliding windows with for buffering data at up-to 1 KHz (TBR)
  
<a name="sw"></a>
## Software [^](#up)
The Bluetera software is an open source project with code and libraries. It supports the most popular operating systems and come with examoles of usage.
  
The software includes the following features:
   
* SDK for Windows, Linux and Android
* SDK for MAC and ioS (TBR)
* Prioprietory BLE stack for Windows (7/8/10) and Linux  
* IMU Control
* Multi devices control
* Online and offline modes of operation (TBR
* Protobuf support (TBR)
* Open source Logger App for windows
* Open source demo Apps  
* IMU Calibration functions (TBR)

<a name="guides"></a>
# System guides [^](#up)

<a name="win_ble"></a>
## Windows (BLE driver installation)
1. Insert CSR Dongle into a free USB port
2. Download ZADIG USB driver installer 
3. Insert the supplied CSR 4.0 BLE dongle to free USB port
4. Run ZADIG (1) 

![BLE Driver](images/zadig1.jpg)
5. Choose Options => List All Devices (2)

![BLE Driver](images/zadig2.jpg)
6. Choose CSR 4.0 BLE dongle (3)
7. Make sure WinUSB driver is chosen (4)
8. Press Replace Driver (5) 

![BLE Driver](images/zadig3.jpg)

<a name="fw_dbg"></a>
## Firmware Update / Firmware Debug (Wired) [^](#up)
1. Prerequisite : 
* Bluetera module (either with or without battery)
* Nordic development board for nRF52832 [PCA100040](https://www.nordicsemi.com/DocLib/Content/User_Guides/nrf52832_dk/latest/UG/nrf52_DK/intro). 
* A Windows 10 machine, with the following software: 
  * Segger J-Link software for Nordic - download [here](https://www.segger.com/downloads/jlink#J-LinkSoftwareAndDocumentationPack) 
  * nRF command line tools - download [here](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF5-Command-Line-Tools/Download#infotabs)
2. Preperation
  * Solder 4 wires to Bluetera pads - VCC, GND, CLK and SIO, shown on the right side of the following image: 
  
  ![Bluetera Extensions](images/bluetera_PRG_w300.jpg)
* prepare the PCA10040 board: 
  *  make sure SW8 is off
  *  SW9 (nRF power source) should be on 'VDD'
  *  SW6 of 'DEFAULT'
  *  connect the GND_DETECT pin of header P20 to GND pin of header P1
*  connect the wires to the PCA10040 board. (connection is slightness different with or without battery - see below). In both cases, connect:
   *  Bluetera GND to P1, GND pin
   *  Bluetera  VCC to P20, VTG pin
   *  Bluetera  CLK to P20, SWD_CLK pin
   *  Bluetera  SIO to P20, SWD_IO pin
   *  **When no battery is connected to the Bluetera, you should also connect  Bluetera VCC to P20, VDD_nRF. Otherwise - don't.** Following images illustrate the connection without battery: 
     
![Bluetera No Bat](images/bluetera_PRG_4_w300.jpg)
3. Programming:
  * Connect the PCA10040 board to a PC via USB.
  * Turn it on (SW6), and wait until drivers are installed
  * If all works well, you should see a new virtual hard-drive named 'JLINK' has been added to your machine
  * Unzip the firmware folder from here, to your working directory (e.g. C:\firmware)
  * Double-click on ..\flash_all.bat (e.g. C:\firmware\flash_all.bat), and wait for completion
  * Turn off the board, and disconnect the Bluetera - it is now programmed
      
<a name="fw_oau"></a>
## Firmware Update (Over The Air) [^](#up)
1. Prerequisite : Initial FW with a Boot loader.   
2. Get Nordic NRF Connect App from the Android / IoS App store 

![Blutera Platfor](images/NRF.jpg)

3. Get the latest FW update (app_dfu_package.zip) and store on your mobile 
4. Turn Bluetera device on – observe that the BLUE Led is blinking slowly (1-sec rate)
5. Scan for Bluetooth devices and find BLUETERA (1) 

![Blutera Platform](images/NRF1.jpg)

6. Connect to device – Observe that the BLUE Led is blinking faster BLUETERA 
7. Click on the DFU button (Adjutant to the DICONNECT Menu item in NRF App) (2) 

![Blutera Platform](images/NRF2.jpg)

8. Select a new Distribution packet (ZIP) (3) 

![Blutera Platform](images/NRF3.jpg) 

![Blutera Platform](images/NRF4.jpg)

9. Bootloader should begin – Click on the BLUETERA device to observe progress

![Blutera Platform](images/NRF5.jpg)

10. Wait till update process completes 

<a name="win_demo"></a>
# Initial Usage (Windows Iotera Logger Demo) [^](#up)
Iotera logger demo is a Windows open source app that illustraits the usage of the IMU module and data logging. The source code and app can be found in the following repository <Link>
1. Prerequisite:
 * Machine with windows operating system 
 * Bluetera device with firmware that fits the Logger APIs
 * BLE CSR Dongle and driver 
 * Logger demo software 
2. Usage:
* Run ../ioteraDemo.exe
* The followinbg window should open 

![Blutera Logger](images/logger-1.jpg)

* Click Logging and enable. You can also set the log path 

![Blutera Logger](images/logger-2.jpg)

* Click start (1). The app should pair to the first BT module it detects (2) and outline its MAC number 

![Blutera Logger](images/logger-3.jpg)

* You can stop the logging and also reset the cube by clicking the corresponding button at menu (1)
* The data section (3) presents Acceleration data (3 axis); Quaternion data and Euler angles - all in realtime (default data sampling is 50hz)
* The graphical section (4) presents a rotating cube (based on quaternion)
* The logger records the data into a CSV file which you can export and analyze 

<a name="cont"></a> 
# Contributing [^](#up)
1. Boaz Aizenshtark
2. Tomer Abramovich
3. Avi Rabinovich

<a name="license"></a> 
# License [^](#up)
1. [MIT](https://choosealicense.com/licenses/mit/)

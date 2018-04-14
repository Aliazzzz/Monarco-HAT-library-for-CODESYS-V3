# Monarco-HAT-library-for-CODESYS-V3
![Alt text](https://tienda.opiron.com/107-home_default/curso-de-codesys.jpg "CODESYS")
![Alt text](http://linuxgizmos.com/files/rex_monarcohat1.jpg "Monarco HAT")


CODESYS V3 Library for Monarco IO HAT

The Monarcvo Hat is an industrial graded Hat ideally suited for Home, IOT or small industrial projects. 
It was lacking a proper CODESYS V3 library, so I decided to write it to fill in the gap.
So, using C & Java Node-JS code examples and documentation from Monarco and after lots of reading and coding, this is the end-result. I decided that it maybe of use for other people, Therefore, I released it under the "Unlicense" agreement. It may still contain bugs (not too much I hope!). If you spot a bug, tell me. Feel free to contribute!

PS: I am not connected with Monarco.io or CODESYS in any way. I wrote this library out of hobbyism and for fun (self-education). 

# Information about current version: V2.0.0.0;
- Works as an IO driverL:All interaction are done via IO and parameters, no function Block calls are needed.
- Breaks compatibilty with earlier version v1.0.0.0, however improves greatly on ease of use.

# Information about previous versions;
https://github.com/Aliazzzz/Monarco-HAT-library-for-CODESYS-V3/blob/master/VERSIONS.md

# The main components are;
- .package file (CODESYS installer) which contains all below mentioned files in a user friendly installer, together with the "unlicense" agreement;
- .devdesc.xml,
- .Library,
- Example.project file.

# Prerequisitories;
- A Raspberry pi with the Monarco HAT,
- CODESYS IDE with Raspberry Pi .package installed,

# Hardware installation;
Attach Monarco HAT to Raspberry Pi and power it up; 

    sudo cat /proc/device-tree/hat/vendor
    
should return "REX Controls" 

    sudo cat /proc/device-tree/hat/product

should return "Monarco HAT"

# Disable system console on UART

    sudo sed 's/ console=serial0,[0-9]\+//' -i /boot/cmdline.txt
    sudo reboot

# Install essential tools
    
    sudo apt update
    sudo apt install git

# Flash Monarco HAT EEPROM (to avoid manual installation of overlay)
sudo git clone https://github.com/monarco/monarco-hat-firmware-bin

    cd monarco-hat-firmware-bin
    ./monarco-eeprom.sh update

# Install CODESYS runtime component on pi (Demo or licensed)
Follow Codesys online help steps, its easy!

https://help.codesys.com/webapp/_rbp_install_runtime;product=CODESYS_Control_for_Raspberry_Pi_SL;version=3.5.12.0

# Monarco codesys package installation;
Either install the Monarco codesys package (double clik it) or via CODESYS Package Manager, or

Install the loose components via the Library / Device Repository, found under Tools menu option in CODESYS IDE.

# Attach Codesys to the RS485 UART, 
Switch to etc direcory and edit the CODESYSControl.cfg;

    cd etc/
    sudo nano CODESYSControl.cfg

Add the following lines;
    
    [SysCom] Linux.Devicefile=/dev/ttyAMA

Now save and Quit nano. 

Now you can use the HAT, RS-485 and the Real-Time Clock from within a CODESYS IEC application. 
Access the RS485 UART via a comlib of you own flavour (like CAA SerialCOM library)

# Run Codesys Project
Open the provided example project file,

Check/Set SPI master parameters:

    Mode 0,
    SPI bits 8,
    Speed(Hz) 1000000 (=1MHz) => can be set up to 4 MHz, slower speeds avoid chance of crc errors

Compile, run it an enjoy!
